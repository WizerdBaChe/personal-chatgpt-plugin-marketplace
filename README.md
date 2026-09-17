# Personal ChatGPT Plugin Marketplace

This repository is the `personal-web` marketplace: the publishable counterpart to the local Codex personal skill suite. It deliberately contains only workflows that can operate in ChatGPT Web without access to a Windows filesystem, shell, locally installed executable, or private local service.

For the reusable rule behind that boundary, see [Claude and Codex skill portability](docs/claude-codex-skill-portability-guide.md).

## Included plugin

`personal-skills-core` contains 12 portable workflows:

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

Every workflow must rely only on conversation context, user-provided files, and enabled connected apps. It must name unavailable evidence rather than implying local access.

## Plugin package layout

The installable plugin lives under `plugins/personal-skills-core/`. It carries the portable Agent Plugins manifest at the plugin root and retains `.codex-plugin/plugin.json` as a Codex compatibility fallback:

```text
plugins/personal-skills-core/
├── plugin.json                  # portable ChatGPT/Codex manifest
├── .codex-plugin/plugin.json    # Codex compatibility fallback
└── skills/                      # 12 bundled workflows
```

`.agents/plugins/marketplace.json` is the repository marketplace catalog; it is not part of the plugin payload. The repository marketplace and the universal public Plugins Directory are separate distribution surfaces.

## Intentionally excluded

The existing local `personal-skill-suite` remains the source for workflows that need local execution or data: Windows cleanup, local asset/vault access, Obsidian access, local CAD, local media tooling, filesystem graph queries, configuration edits, and script-based paper/literature pipelines.

Those workflows need a separately designed remote MCP app before they can be made available on ChatGPT Web. They are not silently downgraded in this plugin.

`_excluded-local-first/` is local staging material only and is ignored by Git. It is retained to document the first portability cut, but is not part of the publishable plugin.

## Distribute through a GitHub marketplace

1. Use this GitHub repository as a repo marketplace source. Keep it private for workspace-only distribution, or use the current public repository for testing and public-source sharing.
2. In an eligible ChatGPT workspace, have an administrator import the repository as a plugin marketplace from **Workspace settings > Plugins > Marketplaces**.
3. Install `Personal Skills Core` from the marketplace and test it in a new web chat.

This route is for a workspace-managed plugin catalog, repo distribution, and Codex. It does not by itself publish the plugin to the universal public Plugins Directory.

After the repository's `main` branch is available, add it to Codex with both the marketplace metadata and plugin payload included in the sparse checkout:

```powershell
codex plugin marketplace add WizerdBaChe/personal-chatgpt-plugin-marketplace --ref main --sparse .agents/plugins --sparse plugins
codex plugin add personal-skills-core@personal-web
```

Restart the Codex desktop app after adding or updating the marketplace, then install `Personal Skills Core` from the `Personal Web` source.

## Public ChatGPT and Codex directory

The plugin package is portable and skills-only: it has no bundled MCP server, local executable, hook, or private service dependency. To appear in the universal Plugins Directory shared by ChatGPT and Codex, submit the skills-only package through the OpenAI plugin submission portal. GitHub `main` and the repo marketplace make the source available for testing; they do not complete public review or publication.

Before submission, prepare a verified publisher identity, public listing/support/privacy/terms URLs, starter prompts, and five positive plus three negative test cases. See [OpenAI's plugin submission requirements](https://developers.openai.com/plugins/deploy/submission).

## Install on an individual ChatGPT Web account

The ChatGPT Web Skills interface accepts individual `.skill`, `.zip`, or `SKILL.md` uploads; it does not expose a personal GitHub marketplace-import control on every account type. Upload each folder under `plugins/personal-skills-core/skills/` as its own `.skill` archive through **Skills > Create > Upload from computer**. ChatGPT scans each uploaded skill before it is installed.

`skill-upload-bundles/` is a local, ignored build output for this upload path. It is not part of the GitHub marketplace source.

Do not add an `.mcp.json` file to this plugin merely to reach local tools: that can make a plugin desktop-only. Add a remote MCP app only after defining authentication, data boundaries, allowed actions, and an approval model.
