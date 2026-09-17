# Claude 與 Codex skill 可攜性通則

**狀態：** 可作為後續遷移與發布的工作準則
**適用範圍：** Claude Code、Codex（CLI／桌面版）、以及 ChatGPT Web 的 skill／plugin 發布判斷。
**不適用範圍：** MCP server 的 API 實作細節、各產品帳號功能是否已開通；這些都需在發布當下另外核對。

## 結論先行

Claude 與 Codex 的 skill **在語意層通常可共用，但在執行與發布層不保證通用**。

一份 skill 可視為三層資產：

| 層級 | 是否通常可共用 | 典型內容 | 何時需要調整 |
| --- | --- | --- | --- |
| 工作流程／專業知識 | 是 | 決策步驟、檢核表、輸出結構、術語、引用規則 | 領域目的、輸出讀者或品質標準改變時 |
| 執行契約 | 部分 | 可用工具、命令、路徑、檔案系統、網路、權限與確認行為 | 目標代理或執行環境不同時 |
| 發現與發布封裝 | 否 | skill 根目錄、plugin manifest、marketplace 註冊、帳號／workspace 安裝方式 | 換宿主、換目錄、換 distribution surface 時 |

因此，**不應把所有 Claude skill 逐份重寫後才「重送」到 Codex**。正確做法是先判定每份 skill 屬於哪一類：

1. **原封可攜**：只使用對話內容、使用者提供檔案與通用推理；保留內容，只做 metadata 與封裝轉接。
2. **可攜但需 adapter**：專業流程保留，但將工具名、路徑、命令、權限與輸入輸出改成目標環境能履行的契約。
3. **不可直接可攜**：依賴本機檔案、私有服務、憑證、hooks 或專屬 MCP；不要假裝可用。保留原版，另做 remote MCP／connector 或明確排除。

## 為什麼相同的 `SKILL.md` 仍可能必須調整？

### 1. 格式相似，不代表能力相同

兩邊都能以 Markdown 指令檔承載工作流程，且 `name`、`description`、逐步指引、參考文件等概念能對應。但 skill 文字往往隱含執行前提。例如：

```md
先用本機 Python 腳本掃描 D:\\vault，再以 git 提交結果。
```

這句專業意圖本身沒有問題；問題在於它同時宣告了 Windows 磁碟、Python、可寫入權限與 Git 身分。若目標是 ChatGPT Web，這些能力不存在；若目標是另一個 Codex sandbox，路徑、環境與核准策略也可能不同。

所以應改成可驗證的能力契約，例如：

```md
若本次環境已提供 vault 路徑與可執行 Python，先盤點並回報範圍；
否則請使用者上傳必要資料或清楚說明此步無法執行。未經明確要求不得提交或推送。
```

這不是降低能力，而是把隱含假設改成可被目標宿主誠實履行的行為。

### 2. 工具、權限與確認時機是宿主行為

Claude Code 與 Codex 都能在某些本機環境操作 shell、檔案與 Git，但工具名稱、可用參數、sandbox、approval policy、工作目錄及對外連線政策並非同一份契約。Claude Code 的 CLI 也以自身的 `--allowedTools`、`--disallowedTools` 和 permission mode 管理工具存取；不能把它們當成 Codex 的設定鍵。[^claude-cli]

同理，Codex 的 `AGENTS.md`、skills、plugins、sandbox 與 approval policy 形成另一套優先序與執行模型。把 Claude 的權限設定、hooks、MCP credential 或全域 runtime state 複製進 Codex skill payload，不只無法保證生效，也可能不必要地擴大權限範圍。

### 3. 路由規則不是技能正文

同一個需求可能命中多份 skill，例如「找論文」可指資料檢索、論文深讀或簡報敘事。原始 Claude trigger dictionary 的價值是處理歧義；它不是每份 skill 的真實規格。跨平台時應保留其意圖，並在目標宿主以自己的 routing entry 或各 `description` 重建可發現性。

這也是為什麼某些遷移會新增一個目標原生的路由 skill，而不是機械地複製所有 Claude 設定檔。

### 4. plugin 是容器；skill 是工作流程

OpenAI 的 plugin 文件明確把 plugin 定義為可組合 skills、MCP 與選用資源的可分發容器；每個 plugin 需要 `.codex-plugin/plugin.json`，而 `skills/`、MCP 設定與 lifecycle hooks 都是容器內的不同部件。[^openai-package]

這代表下列兩件事必須分開判斷：

- **skill 是否可用**：其工作流程與依賴能否在目標執行。
- **plugin 是否可安裝**：manifest、marketplace 目錄、版本、來源與帳號／workspace 是否支援該 distribution surface。

官方文件也指出，公開 plugin 可共用於 ChatGPT 與 Codex，但 local／repository marketplace 是作者測試或團隊發送的來源，且各 surface 的可用性可能不同。[^openai-package] GitHub 已 OAuth 連線只代表 GitHub connector 可授權使用；它不會自動把私有 repository 變成某個帳號可匯入的 plugin marketplace。

## Claude Code、Codex 與 ChatGPT Web 的實務差異

| 面向 | Claude Code | Codex 本機／桌面 | ChatGPT Web |
| --- | --- | --- | --- |
| 最適合的 skill 類型 | 終端、repo、專案工作流 | repo 與本機 agent 工作流；可由 plugin 擴充 | 對話、使用者檔案、已啟用 connector 的工作流 |
| 本機路徑與 shell | 常可用，但取決於本機與設定 | 常可用，但取決於 sandbox、工作目錄與核准策略 | 不可假設可用 |
| 專屬設定 | `CLAUDE.md`、settings、hooks、MCP 設定 | `AGENTS.md`、config、plugins、skills、sandbox | 帳號／workspace 設定、上傳 skills、plugins／connectors |
| 發現方式 | Claude 的 skill／plugin 載入規則 | skill roots、plugin manifest、marketplace | 已安裝 skill、workspace plugin／connector、產品功能開通狀態 |
| 安全邊界 | Claude 的 permission 與工具設定 | Codex approval policy 與 sandbox | 使用者授權的檔案／connector 範圍與產品 UI 政策 |

表格是能力模型，不是「任一環境永遠如此」的保證。部署前仍需用實際 session 驗證工具清單與權限。

## 何時必須改，何時不必改

### 不必改核心內容的情況

符合以下條件時，原始正文大多可直接沿用：

- 只依賴對話、使用者明確提供的檔案與公開／已啟用的資料來源。
- 不直接提及 Claude 專屬 tool 名稱、slash command、hook、設定檔或模型路由。
- 不假定固定絕對路徑、已存在的 venv、私有 connector、local executable 或未授權寫入。
- 將輸出品質寫成可檢驗的產物條件，而不是某產品特有的 UI 動作。

例子：UI 文案審查、架構圖敘事、設計系統評估、研究方法討論與專案 retrospective，通常可保留 80–95% 的領域正文。

### 必須做 adapter 的情況

以下任一項出現時，至少要調整執行段落：

- `~`、`C:\\...`、`/Users/...`、固定 repo 名稱或工作目錄。
- `Bash(...)`、Claude slash command、Claude hook、Claude settings key。
- 固定的 Python／Node／CLI 指令，卻未宣告如何發現 runtime 或如何處理缺失。
- 直接讀寫 credential、token、`.claude`、cache、全域設定或未明確授權的使用者資料。
- 假設 MCP server 已連線，卻未定義缺失時的 fallback、最小資料範圍與高影響操作確認點。
- 把「模型知道怎麼做」誤寫成「環境一定可以執行」。

### 必須拆分或改為 remote integration 的情況

下列 skill 不應只靠改文案就宣稱可移到 Web：

- 本機 vault／素材庫／CAD pipeline／媒體下載器。
- 必須執行公司內網程式、使用本機憑證或讀取私有目錄的流程。
- 依賴 Claude hook、session state、專屬 permission policy 才能正確運作的自動化。
- 需要持續存取資料源或代表使用者採取外部動作的流程。

處置選項依序為：保留 local-only skill；設計最小權限的 remote MCP／app；或把它拆成「Web 可做的分析／規劃 skill」與「需要本機 agent 的執行 skill」。不要把執行步驟靜默刪掉後還宣稱功能等價。

## 建議的可攜性設計：Core + Adapter + Integration

把可重用資產分三層管理，而不是讓每個平台長出不同版本的整份 skill：

```text
skill-core/          # 領域目標、決策規則、輸出品質、測試案例
adapters/
  claude-code.md     # Claude 特有的載入、工具與確認語意
  codex.md           # Codex 特有的工具、AGENTS、sandbox、plugin 規則
  chatgpt-web.md     # 僅使用對話、附件、已啟用 connector 的限制
integrations/
  remote-mcp/        # 需要服務端工具時，獨立定義認證、scope、approval
```

實作上不一定要真的維持這四個資料夾；重點是版本控制時能分辨「領域規格改了」與「某宿主 adapter 改了」。這可避免同一份內容在三個環境各自漂移。

## 遷移 SOP

### A. 先做能力盤點，不先複製

對每份來源 skill 填下列欄位：

| 欄位 | 要問的問題 |
| --- | --- |
| 使用者價值 | 不靠任何特定工具時，這份 skill 想完成什麼？ |
| 最小證據 | 必須有哪種檔案、資料、命令輸出或人類決策？ |
| 讀取能力 | 需要讀本機檔案、repo、網頁、connector，還是只有對話？ |
| 寫入能力 | 是否會改檔、提交、推送、傳送訊息或影響外部系統？ |
| 環境依賴 | 路徑、OS、runtime、MCP、credential、cache、hook？ |
| 安全與確認 | 哪些動作必須在目標宿主重新取得確認？ |
| 目標分類 | 原封可攜、需 adapter、或需要 integration／排除？ |

### B. 只遷移 skill payload，不遷移全域權限狀態

保留與 skill 直接相關的：`SKILL.md`、必要 script、reference、schema、範例與測試資料。

預設排除並另外審查：

- Claude／Codex 的全域設定檔與規則檔。
- hooks、session state、cache、衍生索引。
- MCP credential、token、cookie、個人資料與私有連線資訊。
- 只有某個工作站才成立的絕對路徑與 executable 假設。

### C. 重寫「能力聲明」，不改寫無關的專業規則

使用條件式、可檢驗的語句：

- 「若已提供 X，執行 Y；否則列出缺少的證據與替代方案。」
- 「僅在目標環境提供 shell／connector 時使用它；不可用時不模擬執行結果。」
- 「寫入、提交、推送、刪除、傳送等動作，僅在使用者明確要求且目標宿主允許時執行。」

避免：

- 「直接執行」「一定可讀取」「已授權所有工具」等跨宿主不成立的陳述。
- 用另一個代理的工具名稱當成通用規格。

### D. 以目標宿主的規則重建發現與封裝

- **Claude Code target**：依 Claude 的 skill／plugin 來源與專案設定處理；不要帶入 Codex marketplace metadata。
- **Codex target**：每個 skill 以目標要求的 frontmatter 與目錄驗證；多 skill 套件使用 `.codex-plugin/plugin.json` 與 marketplace layout。
- **ChatGPT Web target**：只發布可在 Web 履行的 core；本機依賴改走 remote MCP 或保留給 Codex／Claude 本機版。帳號與 workspace 是否可用 repo marketplace 要另外驗證。

### E. 驗證要分三種

| 驗證 | 問題 | 最小證據 |
| --- | --- | --- |
| 靜態 | skill 格式與引用完整嗎？ | frontmatter、連結、腳本 parse、manifest validator |
| 環境 | 目標 session 真的看得到嗎？ | 新 session 的 skill discovery、plugin installed/enabled、實際工具清單 |
| 行為 | 在能力受限時會誠實 fallback 嗎？ | 一個正常案例、一個缺依賴案例、一個高影響操作案例 |

綠色的靜態 validator 不代表 Web 可以讀本機檔案；同樣地，能安裝的 plugin 不代表每份 skill 的依賴都具備。

## 本次 Claude → Codex 遷移得到的實證

這個準則已在目前的 personal skill suite 實作過一次，而不是純理論：

- 盤點 28 個 Claude source skills，保留其領域工作流，另增加一個 Codex 原生 `skill-routing` 入口，成為 29 個 skills。
- 保留了 245 個經審查的 payload 檔案；不複製 Claude hooks、rules、permissions、MCP credentials、全域 runtime state、cache 與衍生索引。
- 驗證結果為 29/29 frontmatter、36 個 Python 檔可 parse、0 個 entry link 斷裂，且 Codex plugin manifest 通過驗證。
- 為 ChatGPT Web 再切出 12 個 portable workflows；需要本機 filesystem、executable 或私有服務的 skill 留在 local suite，而非降低後假裝等價。

所以答案不是「Claude skill 與 Codex skill 不通用」，而是：**其可通用的核心已被保留；不通用的是未明確寫出的宿主能力與發布機制。**

## 發布前一頁檢核表

- [ ] 本文是否只描述可由目標宿主實際提供的工具與資料？
- [ ] 所有絕對路徑、CLI 名稱、hook、設定鍵與 MCP 假設是否已列為 adapter／integration？
- [ ] 缺失依賴時，是否明確 fallback，而不是捏造執行成功？
- [ ] 寫入／外部動作是否保留目標宿主的確認與權限語意？
- [ ] 是否只打包 skill payload，而沒有夾帶 credential、cache 或全域設定？
- [ ] manifest／marketplace 與目標 product surface 是否各自驗證？
- [ ] 是否在新的目標 session 做過一個正常、一個缺依賴、一個高影響操作案例？

## 參考資料

[^openai-package]: [OpenAI Developers — Package your plugin](https://developers.openai.com/plugins/build/plugins)：plugin manifest、skills/MCP 組成，以及公開與 local/repository marketplace 的 surface 差異。
[^claude-cli]: [Anthropic — Claude Code CLI reference](https://docs.anthropic.com/en/docs/claude-code/cli-usage)：Claude Code 的工具 allow/disallow 與 permission mode 是 Claude 自己的 CLI 契約。
