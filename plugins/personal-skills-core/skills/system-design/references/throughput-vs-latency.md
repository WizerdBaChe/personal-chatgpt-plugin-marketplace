---
date: 2026-08-16
source: user-supplied curated write-up (zh-TW); cites sigarch.org (performance
  models series), aws.amazon.com (throughput vs latency), arxiv 1901.02926
verified: all math re-derived at intake — Little's Law example (L = 1000 × 0.2
  = 200), M/M/1 sojourn W = S/(1-ρ), and the utilization multiplier table
  (25%→1.33×, 50%→2×, 75%→4×, 90%→10×, 95%→20×) are each correct; the
  "real systems are worse than M/M/1" caveat is standard and true
review-when: stable queueing theory — review only when applied to a SPECIFIC
  system's numbers (then measure that system; never extrapolate the M/M/1
  table onto a multi-server/bursty reality without saying it is a lower bound
  on badness)
aliases: [吞吐量, throughput, 延遲, latency, Little's Law, 利用率, utilization,
  p99, 排隊理論, queueing, backpressure, 容量規劃, capacity]
---

# Throughput vs latency（系統吞吐與延遲）

## Claims audit (intake 2026-08-16)

- FACT — Little's Law (L = λW) and the worked example: re-derived, correct.
- FACT — M/M/1 utilization curve W = S/(1-ρ) and the multiplier table:
  re-derived, correct. NOTE the table is a DERIVATION, not a measurement —
  it needs no device class, but real systems (bursts, GC, cache miss, tail
  amplification) sit above it, as the text itself states.
- HEURISTIC — per-workload SLOs (interactive p99 vs background queue-age vs
  transactional correctness), capacity headroom, bounded in-flight work,
  admission control over unbounded queues: standard SRE/queueing practice,
  sound.
- FACT — "offered load persistently above completed throughput ⇒ queue grows
  without bound": definitionally true and well put ("未償還的工作債務").
- Conflicts with model knowledge: none.

## Body（user-supplied, zh-TW, as delivered 2026-08-16）

系統延遲（latency）與吞吐量（throughput）的 trade-off，本質是：**在資源有限時，越接近系統最大處理能力，排隊越容易累積，單一請求等待越久。**吞吐可先上升，但接近飽和時，延遲通常不是線性變差，而是急遽惡化。 [sigarch](https://www.sigarch.org/three-other-models-of-computer-system-performance-part-2/)

### 兩個指標

- **延遲**：一個 request／task 從進入系統到完成所花的時間，包含排隊、執行、網路與下游等待；常看 p50、p95、p99，而非只看平均值。
- **吞吐量**：單位時間完成的工作數，例如 2,000 requests/s、500 jobs/min 或 100 MB/s。 [aws.amazon](https://aws.amazon.com/compare/the-difference-between-throughput-and-latency/)

高吞吐不等於低延遲。例如系統每秒完成 10,000 個請求，但每個請求都因 backlog 等待 5 秒，對互動使用者而言仍是很差的體驗。

### 用 Little's Law 理解

在長期穩定狀態下：

\[
L = \lambda W
\]

其中：

- \(L\)：系統內平均工作數（in-flight + queue 中等待者）
- \(\lambda\)：完成率／吞吐量
- \(W\)：平均端到端延遲

也就是：

\[
\text{Concurrency} = \text{Throughput} \times \text{Latency}
\]

例如服務維持 1,000 RPS，而平均延遲為 200 ms：

\[
L = 1000 \times 0.2 = 200
\]

代表系統平均同時承載約 200 個請求。若吞吐仍是 1,000 RPS、延遲升至 2 秒，in-flight 工作數會變成 2,000；如果系統沒有足夠 concurrency、連線池、記憶體或 queue 空間，就會開始逾時、拒絕請求或連鎖失效。 [arxiv](https://arxiv.org/pdf/1901.02926.pdf)

### 為何接近滿載會爆炸

以單一服務者、平均處理時間 \(S\) 的簡化 M/M/1 模型：

\[
\rho = \lambda S
\]

\(\rho\) 是利用率（utilization）。當 \(\rho \to 1\)，平均總延遲近似：

\[
W = \frac{S}{1-\rho}
\]

這揭露了「不要把服務長期跑在 100% CPU／100% 連線池／100% worker 使用率」的原因：

| 利用率 \(\rho\) | 平均延遲約為純處理時間的倍數 |
|---:|---:|
| 25% | 1.33× |
| 50% | 2× |
| 75% | 4× |
| 90% | 10× |
| 95% | 20× |

例如一個任務純處理時間為 20 ms：在 75% 利用率時平均約 80 ms；90% 時約 200 ms；95% 時約 400 ms。真實系統因流量 burst、GC、快取 miss、慢查詢和下游尾延遲，通常會比這個理想模型更糟。 [sigarch](https://www.sigarch.org/three-other-models-of-computer-system-performance-part-2/)

### 哪些設計會交換兩者

| 手段 | 對吞吐量 | 對延遲 | 為何 |
|---|---|---|---|
| Batching | 通常提升 | 通常增加 | 等待湊批次，換取較少 syscalls、RPC 或 DB commits |
| 增加 worker／分片 | 提升 | 常降低，直到新瓶頸出現 | 平行處理更多工作 |
| 更高 concurrency | 可提升 | 可能降低或提高 | 太低吃不滿資源；太高會造成 context switch、鎖競爭、GC、DB connection 壅塞 |
| 非同步 queue | 提升可持續處理能力 | API 回應可低，但端到端完成時間可能提高 | 將工作放入 backlog，削峰填谷 |
| 同步 quorum／強一致性 | 常降低 | 通常增加 | 需等待多個副本或跨區網路往返 |
| 快取／預計算 | 提升 | 降低 | 避免昂貴的下游工作，但要付出一致性與失效策略成本 |
| 降低同步 RPC hop | 常提升 | 降低 | 少掉網路往返、序列化、故障域與依賴等待 |

### 設計上的實務原則

#### 依工作型態設 SLO

不要用一個「越快越好」的指標管理所有流量：

- 互動式 API：優先 p95/p99 latency，例如讀取在 p99 低於 200 ms。
- 背景任務：優先穩定吞吐、queue age、失敗率與成本；數秒至數分鐘延遲可能可接受。
- 金流或寫入交易：除了延遲，也須衡量正確性、持久化與一致性，不能只為快而犧牲語意。

#### 保留容量餘裕

針對有尾延遲與 burst 的線上服務，長期利用率不宜逼近 100%。把 autoscaling 觸發點連結到：

- CPU／記憶體與 event-loop lag。
- 每個 partition 的 consumer lag。
- queue depth 與 oldest-message age。
- DB connection-pool utilization。
- p95／p99 latency，而不是只有平均 response time。

#### 限制 in-flight 工作

以 admission control、bounded queue、semaphore、connection pool 和 backpressure 限制同時工作量。無上限排隊不會創造容量，只會把過載轉化為更長的延遲與更多逾時。

例如，若 DB 安全上限是 100 個併發查詢，就不要讓 API 層同時把 2,000 個查詢打進 DB；讓超額請求短暫排隊、快速拒絕（如 429/503）或降級，往往比所有請求一起逾時更可靠。

#### 以端到端量測校正

同時觀察：

- Offered load：進來多少 RPS。
- Completed throughput：實際成功完成多少 RPS。
- p50、p95、p99 latency。
- Error／timeout rate。
- Queue depth 與 queue wait time。
- In-flight requests／worker utilization。

當 offered load 持續高於完成吞吐，queue 會無限成長；那不是「吞吐高」，而是系統正累積未償還的工作債務。
