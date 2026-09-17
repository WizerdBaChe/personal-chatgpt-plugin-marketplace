# Personal ChatGPT Plugin Marketplace

> 中文是預設閱讀版本；English 可在本頁下方展開。

## 這個 repository 是什麼

這是 `personal-web` repository marketplace，提供一個可跨 ChatGPT 與 Codex 使用的 portable plugin：`personal-skills-core`。

目前 `main` 已包含可公開分發的 plugin package，但「GitHub repository marketplace」和 OpenAI universal Plugins Directory 是不同的發現面。要讓一般 ChatGPT 使用者在官方目錄搜尋到，仍需要完成官方送審、審查與發布。

這個 plugin 是 skills-only package。它只使用對話內容、使用者提供的檔案，以及使用者已啟用的 connected apps；不要求本機檔案系統、shell、local executable、MCP server 或私人服務。

## 內含的 12 個 workflows

- AI coding guardrails
- Audience adaptation and UI copy
- Deep code review
- Shared design systems
- Traceable diagrams
- Product design
- Project retrospectives
- Frontend rendering performance
- Scientific research methodology
- Defensive security audit
- Backend systems design
- Workflow checkpoints

## Plugin package 結構

~~~text
plugins/personal-skills-core/
├── plugin.json                  # portable ChatGPT/Codex manifest
├── .codex-plugin/plugin.json    # Codex compatibility fallback
├── LICENSE                      # MIT license for the plugin package
└── skills/                      # 12 independently discoverable workflows
~~~

OpenAI 目前建議的 portable package 以 plugin 根目錄的 `plugin.json` 為入口；`.codex-plugin/plugin.json` 留作 Codex 相容 fallback。`skills/` 會由 portable package 自動發現。參考 [OpenAI — Package your plugin](https://developers.openai.com/plugins/build/plugins)。

`.agents/plugins/marketplace.json` 是 repository marketplace catalog，不是 plugin payload。它只負責告訴 Codex 要去哪裡找到 `plugins/personal-skills-core/`。

## 如何安裝與使用

### A. 從 ChatGPT/Codex universal Plugins Directory 安裝

這條路徑要等 plugin 完成 OpenAI 官方送審並發布後才會生效。

1. 在 ChatGPT 的 Plugins/Apps 目錄搜尋 `Personal Skills Core`。
2. 開啟 plugin 詳情，確認 publisher 與 repository。
3. 選擇 **Install**。
4. 開一個新的 chat，直接描述需求，例如：

   - 「請用 `product-design-thinking` 幫我把這個功能整理成產品規格。」
   - 「請用 `security-deep-checklist` 審查這份 deployment plan。」
   - 「請用 `audience-fit` 把這段內容改成主管看得懂的版本。」

5. 若需求同時符合多個 workflows，plugin 會依請求內容選最相關的 workflow；你也可以直接在訊息中點名 workflow。

目前 GitHub `main` 還不代表 universal Plugins Directory 已發布。官方流程是 submit → review → publish；完整要求見 [OpenAI — Submit plugins](https://developers.openai.com/plugins/deploy/submission)。

### B. 從 ChatGPT workspace 的 repository marketplace 安裝

這是 workspace 管理員可用的 repository 分發方式，不等同於官方 universal directory。

1. 管理員開啟 **Workspace settings → Plugins → Marketplaces**。
2. 匯入 GitHub repository：`WizerdBaChe/personal-chatgpt-plugin-marketplace`。
3. 使用 `main` branch。
4. 在 `Personal Web` marketplace 中找到 **Personal Skills Core**。
5. 選擇 **Install**。
6. 開新的 web chat 測試，不要只沿用已經載入舊 plugin catalog 的 chat。

如果你是一般個人 ChatGPT account，而且看不到 repository marketplace，這不是 repository 結構錯誤；請改用 universal directory（發布後）或個別 `.skill` upload 路徑。

### C. 在 Codex 安裝 repository marketplace

在 PowerShell 執行：

~~~powershell
codex plugin marketplace add WizerdBaChe/personal-chatgpt-plugin-marketplace --ref main --sparse .agents/plugins --sparse plugins
codex plugin add personal-skills-core@personal-web
codex plugin list
~~~

預期會看到：

~~~text
personal-skills-core@personal-web    installed, enabled    0.1.1
~~~

更新 repository 後，先刷新 marketplace，再重新安裝：

~~~powershell
codex plugin marketplace upgrade personal-web
codex plugin add personal-skills-core@personal-web
~~~

完成後重開 Codex，並用新的 task/thread 測試。新 thread 是確認新 skills 已被載入的重要步驟。

### D. 在個人 ChatGPT Web 上傳單一 skill

個人 ChatGPT Web 的 upload UI 通常是「skill upload」，不是整個 repository plugin marketplace。這條路徑要把 12 個 workflow 各自當成一個 `.skill` archive 上傳，不是拆成 28 個。

1. 取用 `plugins/personal-skills-core/skills/<skill-name>/`。
2. 保留 archive 的根目錄 `<skill-name>/`。
3. 確認根目錄內有 `SKILL.md`。
4. 在 ChatGPT 開啟 **Skills → Create → Upload from computer**。
5. 一次上傳一個 `.skill`。
6. 安裝後開新的 chat，再用自然語言測試。

本 repository 的 `skill-upload-bundles/` 是本機 ignored build output，不會被推到 GitHub。若要自行重建 12 個 upload archives，可在 repository root 的 PowerShell 執行：

~~~powershell
$repo = (Get-Location).Path
$skillsRoot = Join-Path $repo 'plugins/personal-skills-core/skills'
$out = Join-Path $repo 'skill-upload-bundles'
New-Item -ItemType Directory -Force -Path $out | Out-Null

Get-ChildItem -LiteralPath $skillsRoot -Directory | ForEach-Object {
    $zip = Join-Path $out ($_.Name + '.skill')
    Compress-Archive -LiteralPath $_.FullName -DestinationPath $zip -CompressionLevel Optimal -Force
}
~~~

要送交 OpenAI plugin submission portal，使用同一個 ignored build output 裡的 `personal-skills-core-0.1.1.plugin.zip`。它是從 Git-tracked plugin package 建立的完整 archive，包含 root `plugin.json`、Codex fallback、MIT `LICENSE` 與 12 個 skills；不要直接壓縮包含 `_excluded-local-first/` 的本機工作目錄。

## 安裝後怎麼用

不用輸入特殊 command。直接描述工作即可，例如：

- 「幫我設計一個新的 data-review workflow，先列 acceptance criteria。」
- 「請用 `code-review-deep-checklist` 審查這個 diff，分開列出 finding、evidence 與 deferred checks。」
- 「請用 `diagram-authoring` 把這段系統描述成 sequence diagram。」
- 「請用 `scientific-research-guide` 區分已證實、推論與尚未驗證的內容。」

如果 plugin 沒有自動選到正確 workflow，直接點名 skill 名稱即可。所有 workflows 都要求在缺少證據時明確說明，不應假設可以讀取使用者的本機資料。

## 常見問題

### 搜尋不到 plugin

先分辨你使用的是哪一個 surface：

- GitHub repository：只能提供 source。
- Codex repository marketplace：可由 Codex 安裝。
- ChatGPT workspace marketplace：需要 workspace 管理員匯入。
- Universal Plugins Directory：需要官方審查並發布後才會出現。

把 repository 推到 `main` 不會自動讓它出現在 universal directory。

### 顯示安裝失敗或安裝後無法載入

依序確認：

1. 使用的是完整 plugin path，而不是只選到 `.agents/plugins/marketplace.json`。
2. `plugins/personal-skills-core/plugin.json` 與 `.codex-plugin/plugin.json` 都是有效 JSON。
3. archive 是以 skill folder 為根目錄，且包含 `SKILL.md`。
4. 安裝或更新後重新開啟 chat/task。
5. 目標 account/workspace 是否允許該安裝 surface。
6. 不要把 local-only skill、MCP config 或本機 executable 混進公開 package。

### 為什麼不是拆 28 個？

目前公開 package 明確包含 12 個 workflows，所以可上傳或測試的獨立 `.skill` 也是 12 個。`references/`、domain profiles 與其他支援文件是各 workflow 的內容，不是額外的 top-level skills。

## 公開送審前 checklist

在 OpenAI submission form 上傳前，請確認：

- publisher identity 已驗證。
- license 已選定為 MIT，而且和兩份 plugin manifest 及 `plugins/personal-skills-core/LICENSE` 一致。
- 已準備 public website、support、privacy policy、terms of service URL。
- 已準備 logo/category 與 starter prompts。
- 已準備至少 5 個 positive test cases 與 3 個 negative test cases。
- package 不含 secrets、私人路徑、local-only integration 或不必要的權限。

本版本選用 MIT。License 是送審／上傳時的法律選擇；若日後要改 license，不要只改 README，應同步更新 root `plugin.json`、`.codex-plugin/plugin.json`、`plugins/personal-skills-core/LICENSE` 與 repository root `LICENSE`，再重新上傳 package。

## Intentionally excluded

下列能力仍留在 local `personal-skill-suite`，沒有偷偷降級成公開 skill：

- Windows cleanup
- local asset/vault access
- Obsidian access
- local CAD/modeling
- local media tooling
- filesystem graph queries
- configuration edits
- script-based paper/literature pipelines

這些能力如果要跨 ChatGPT Web 分發，應另行設計 remote MCP app、authentication、data boundary 與 approval model。

## English

<details>
<summary>Expand the English guide</summary>

### What this repository is

This repository is the `personal-web` repository marketplace for `personal-skills-core`, a portable plugin that can be distributed across ChatGPT and Codex.

The current `main` branch contains the public plugin package. A GitHub repository marketplace and the OpenAI universal Plugins Directory are separate discovery surfaces. A normal ChatGPT user will not see this plugin in the official directory until the package has been submitted, reviewed, and published.

The plugin is skills-only. It uses conversation context, user-provided files, and enabled connected apps. It does not require a local filesystem, shell, executable, MCP server, or private local service.

### The 12 included workflows

- AI coding guardrails
- Audience adaptation and UI copy
- Deep code review
- Shared design systems
- Traceable diagrams
- Product design
- Project retrospectives
- Frontend rendering performance
- Scientific research methodology
- Defensive security audit
- Backend systems design
- Workflow checkpoints

### Package layout

~~~text
plugins/personal-skills-core/
├── plugin.json                  # portable ChatGPT/Codex manifest
├── .codex-plugin/plugin.json    # Codex compatibility fallback
├── LICENSE                      # MIT license for the plugin package
└── skills/                      # 12 independently discoverable workflows
~~~

The portable package uses the root `plugin.json`. `.codex-plugin/plugin.json` remains as a Codex compatibility fallback, and the root `skills/` directory is automatically discovered. See [OpenAI — Package your plugin](https://developers.openai.com/plugins/build/plugins).

`.agents/plugins/marketplace.json` is the repository marketplace catalog. It is not part of the plugin payload.

### Install from the universal Plugins Directory

This route becomes available after official submission and publication:

1. Search for `Personal Skills Core` in the ChatGPT Plugins/Apps directory.
2. Confirm the publisher and repository on the details page.
3. Select **Install**.
4. Start a new chat and describe the task.
5. Name a workflow explicitly when you want a specific one.

The GitHub `main` branch is not the same thing as a published universal directory listing. See [OpenAI — Submit plugins](https://developers.openai.com/plugins/deploy/submission).

### Install from a ChatGPT workspace repository marketplace

1. Open **Workspace settings → Plugins → Marketplaces** as a workspace administrator.
2. Import `WizerdBaChe/personal-chatgpt-plugin-marketplace`.
3. Select the `main` branch.
4. Install **Personal Skills Core** from the `Personal Web` marketplace.
5. Start a new web chat to test it.

If a personal ChatGPT account cannot see repository marketplaces, that is an account/workspace surface limitation, not necessarily a repository layout failure. Use the universal directory after publication or individual skill upload instead.

### Install in Codex

Run in PowerShell:

~~~powershell
codex plugin marketplace add WizerdBaChe/personal-chatgpt-plugin-marketplace --ref main --sparse .agents/plugins --sparse plugins
codex plugin add personal-skills-core@personal-web
codex plugin list
~~~

After repository updates:

~~~powershell
codex plugin marketplace upgrade personal-web
codex plugin add personal-skills-core@personal-web
~~~

Restart Codex and use a new task/thread so the updated skills are loaded.

### Upload one skill to personal ChatGPT Web

Individual ChatGPT Web upload is generally a skill-upload path, not a repository marketplace import. Upload one `.skill` archive per workflow:

1. Use `plugins/personal-skills-core/skills/<skill-name>/`.
2. Keep `<skill-name>/` as the archive root.
3. Keep `SKILL.md` at the skill root.
4. Open **Skills → Create → Upload from computer**.
5. Upload one skill at a time.
6. Start a new chat and test it.

The ignored `skill-upload-bundles/` directory is a local build output. It is not part of the GitHub package. Rebuild the 12 archives with:

~~~powershell
$repo = (Get-Location).Path
$skillsRoot = Join-Path $repo 'plugins/personal-skills-core/skills'
$out = Join-Path $repo 'skill-upload-bundles'
New-Item -ItemType Directory -Force -Path $out | Out-Null

Get-ChildItem -LiteralPath $skillsRoot -Directory | ForEach-Object {
    $zip = Join-Path $out ($_.Name + '.skill')
    Compress-Archive -LiteralPath $_.FullName -DestinationPath $zip -CompressionLevel Optimal -Force
}
~~~

For the OpenAI plugin submission portal, use the ignored build output `personal-skills-core-0.1.1.plugin.zip`. It is created from the Git-tracked plugin package and contains the root `plugin.json`, Codex fallback, MIT `LICENSE`, and all 12 skills. Do not zip the working directory directly if it contains `_excluded-local-first/`.

### Use the plugin after installation

No special command is required. Describe the work naturally, or name a workflow:

- `product-design-thinking`
- `security-deep-checklist`
- `audience-fit`
- `diagram-authoring`
- `scientific-research-guide`

The workflows must state when evidence is missing and must not assume access to a user's local files.

### Troubleshooting

- GitHub source, Codex repository marketplace, ChatGPT workspace marketplace, and the universal directory are different surfaces.
- A GitHub push to `main` does not automatically publish a universal directory listing.
- After install or update, use a new chat/task.
- Keep the archive root and `SKILL.md` location correct.
- Do not include local-only skills, MCP configuration, executables, secrets, or private paths.

There are 12 public workflows, so there are 12 independent `.skill` upload packages. References and domain profiles are supporting content inside those workflows, not additional top-level skills.

### Public submission checklist

Before uploading to the OpenAI submission form:

- Verify the publisher identity.
- Confirm the selected MIT license and make both manifests and `plugins/personal-skills-core/LICENSE` agree.
- Prepare public website, support, privacy, and terms URLs.
- Prepare logo/category, starter prompts, and at least five positive plus three negative test cases.
- Remove secrets, private paths, local-only integrations, and unnecessary permissions.

This release uses MIT. The license is a legal upload-time choice. Do not change only the README; update both manifests and the package `LICENSE` before re-uploading.

</details>

## Official references

- [OpenAI — Package your plugin](https://developers.openai.com/plugins/build/plugins)
- [OpenAI — Submit plugins](https://developers.openai.com/plugins/deploy/submission)
