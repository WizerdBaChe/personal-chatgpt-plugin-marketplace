---
date: 2026-08-16
source: user-supplied curated write-up (zh-TW); cites aws.amazon.com
  (message-queue), docs.oracle.com (msg delivery), ibm.com (MQ features),
  learn.microsoft.com (queues-overview, priority-queue pattern)
verified: semantics checked against model knowledge + the cited vendor docs'
  standard positions at intake — point-to-point vs pub/sub, ack-after-process,
  visibility timeout, DLQ, at-least-once as the pragmatic default, transactional
  outbox: all stable industry practice, no volatile claims found
review-when: delivery-semantics landscape shifts (e.g., exactly-once becomes a
  commodity default across brokers); or the first time this file is used for a
  CONCRETE broker choice — it is deliberately broker-agnostic, and that use
  case needs a per-broker supplement
aliases: [訊息佇列, message queue, MQ, 事件驅動, event-driven, pub/sub, DLQ,
  死信佇列, outbox, 削峰, 非同步]
---

# Message queues（訊息佇列）

## Claims audit (intake 2026-08-16)

- FACT — component roles (producer/broker/consumer/ack/retry/DLQ), P2P vs
  pub/sub semantics: vendor-doc-backed, stable.
- FACT — at-least-once as the pragmatic default; consumers must be idempotent:
  standard across mainstream brokers.
- PATTERN — transactional outbox for the dual-write problem: standard, the
  four-step description is correct.
- HEURISTIC — 適合/不適合 lists (async jobs vs sync-result interactions,
  strong-consistency transactions, trivially small systems): sound judgment,
  context carried in the text.
- Conflicts with model knowledge: none.

## Body（user-supplied, zh-TW, as delivered 2026-08-16）

訊息佇列（Message Queue, MQ）是一種讓系統元件以**非同步**方式交換工作或事件的中介機制：生產者把訊息放進佇列，消費者在自己可處理時取出、成功完成後確認（ack）並移除。兩端不必同時在線，也不必直接互相呼叫。 [aws.amazon](https://aws.amazon.com/tw/message-queue/)

### 定義與核心角色

一則訊息通常是「要做什麼」或「發生了什麼」的資料，例如：

```json
{
  "eventId": "evt_123",
  "type": "order.created",
  "orderId": "O-8821",
  "occurredAt": "2026-08-16T15:30:00Z"
}
```

典型元件如下：

| 元件 | 職責 |
|---|---|
| Producer／Publisher | 產生事件或工作，將訊息送入 broker |
| Broker／Queue | 暫存、路由、保留訊息，必要時持久化 |
| Consumer／Worker | 拉取或接收訊息，執行業務處理 |
| Ack | Consumer 明確表示處理完成，broker 才能刪除訊息 |
| Retry／DLQ | 失敗時重試；反覆失敗的訊息送至死信佇列供排查 |

最常見的 queue 語意是 point-to-point：一則工作訊息通常由一個 consumer 成功處理；相對地，pub/sub 的 topic 模式可讓多個訂閱者各自收到同一事件。 [docs.oracle](https://docs.oracle.com/cd/E19957-01/819-2224/msg_delivery.html)

### 它要解決的目標

#### 1. 解耦服務

沒有 MQ 時，訂單服務可能同步呼叫付款、寄信、庫存、推薦等服務。任何下游變慢或失敗，都可能拖慢甚至使訂單 API 失敗。

使用 MQ 後，訂單服務只需可靠地發出 `order.created`；下游各服務各自消費並處理。程式之間不需要直接連線，也不必知道對方何時可接收工作。 [ibm](https://www.ibm.com/docs/zh-tw/ibm-mq/9.3.x?topic=queuing-main-features-benefits-message)

#### 2. 平滑流量尖峰

假設促銷瞬間湧入 10 萬個影像轉檔任務，但 worker 每分鐘僅能處理 1 萬個。MQ 會作為緩衝層，把工作先保存起來，worker 按可用容量逐步消化；也可依 backlog 長度水平擴充 consumer。這避免 API 或資料庫被瞬時流量壓垮。 [aws.amazon](https://aws.amazon.com/tw/message-queue/)

#### 3. 提升故障隔離與可靠性

Producer 成功把訊息交給可持久化的 broker 後，即使 consumer 暫時掛掉、重啟或網路中斷，訊息仍可待 consumer 恢復後處理。佇列可將通訊雙方與網路故障隔離，讓系統不必要求所有元件同步存活。 [learn.microsoft](https://learn.microsoft.com/zh-tw/dotnet/framework/wcf/feature-details/queues-overview)

#### 4. 非同步化長工作

請求端不應等待耗時任務，例如寄送大量通知、產生報表、OCR、影音轉碼、LLM 推論批次作業等。它可以快速回傳「已接受」，背景 worker 再透過 queue 處理。

#### 5. 控制工作調度

可藉由多個 queue、priority queue、consumer concurrency、延遲訊息與 rate limit，將高優先級任務先處理，或限制特定下游服務的負載。優先序佇列專門處理「重要性高於到達順序」的情境。 [learn.microsoft](https://learn.microsoft.com/zh-tw/azure/architecture/patterns/priority-queue)

### 如何達成這些目標

可靠 MQ 設計不只是「送進 queue、拿出來」；重點在交付語意與失敗處理。

| 機制 | 解決的問題 | 實務做法 |
|---|---|---|
| Durable message | Broker 或 consumer 重啟後遺失工作 | 訊息、queue、broker replication 使用持久化設定 |
| Ack after processing | Consumer 拿到就崩潰造成遺失 | 處理成功、資料已提交後才 ack |
| Visibility timeout | Consumer 崩潰但沒有 ack | 超時後訊息重新可見，由其他 worker 重試 |
| Retry with backoff | 暫時性網路、下游 API 故障 | 指數退避與 jitter，限制最大重試次數 |
| Dead-letter queue | 毒丸訊息無限重試 | 超過重試閾值轉入 DLQ，告警並人工或自動修復 |
| Idempotency | 至少一次投遞造成重複 | 用 `eventId`、唯一鍵或 inbox table 去重 |
| Backpressure | Consumer 跟不上 producer | 監測 queue depth、age、處理速率；擴 worker 或節流 producer |
| Schema versioning | Producer/consumer 演進破壞相容性 | 使用版本欄位、向後相容欄位變更、schema registry |

多數分散式 MQ 的務實預設是 **at-least-once delivery**：訊息可能重複，但盡量不遺失。因此 consumer 必須設計成冪等（idempotent），不能假定「一定只收到一次」。

### 具體例子：電商下單

同步耦合版本：

```text
Client → Order API → Payment API → Inventory API → Email API
```

任何一個下游慢、故障或逾時，都會直接影響下單請求。

事件驅動版本：

```text
Client → Order API → DB
                    └→ order.created → Message Broker
                                          ├→ Payment Worker
                                          ├→ Inventory Worker
                                          ├→ Notification Worker
                                          └→ Analytics Worker
```

此處 `Order API` 的關鍵難點是：不能出現「訂單已寫入資料庫，但事件沒送出」或「事件送出但訂單沒寫入」的雙寫不一致。常見解法是 **transactional outbox pattern**：

1. 在同一筆資料庫交易中，寫入 `orders` 與 `outbox_events`。
2. 背景 relay 將 outbox 事件可靠發布至 broker。
3. 成功發布後將 outbox 標記為已送出。
4. Consumer 使用事件 ID 去重並以冪等方式執行。

### 何時適合、不適合

適合：

- 背景工作、批次處理與非同步任務。
- 微服務之間的事件通知與工作分派。
- 流量波動大、需要削峰填谷的系統。
- 可接受最終一致性，且可設計重試與補償的流程。

不適合直接取代：

- 必須同步取得結果的互動，例如登入驗證、即時計價、使用者等待的查詢。
- 需要強一致、跨服務原子提交，且無法承擔延遲或補償邏輯的交易。
- 極簡單、單體、低流量且沒有預期擴張需求的系統；此時 queue 可能增加不必要的營運與除錯成本。

一句話：MQ 用「持久化的非同步中介層」換取系統的解耦、韌性與可擴展性；代價是你必須面對重複投遞、順序、可觀測性，以及最終一致性的工程複雜度。
