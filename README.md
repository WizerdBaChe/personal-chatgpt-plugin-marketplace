# Personal ChatGPT Plugin Marketplace

This repository is the `personal-web` marketplace: the publishable counterpart to the local Codex personal skill suite. It deliberately contains only workflows that can operate in ChatGPT Web without access to a Windows filesystem, shell, locally installed executable, or private local service.

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

## Intentionally excluded

The existing local `personal-skill-suite` remains the source for workflows that need local execution or data: Windows cleanup, local asset/vault access, Obsidian access, local CAD, local media tooling, filesystem graph queries, configuration edits, and script-based paper/literature pipelines.

Those workflows need a separately designed remote MCP app before they can be made available on ChatGPT Web. They are not silently downgraded in this plugin.

`_excluded-local-first/` is local staging material only and is ignored by Git. It is retained to document the first portability cut, but is not part of the publishable plugin.

## Distribute through a GitHub marketplace

1. Create a private GitHub repository from this directory and push it.
2. In an eligible ChatGPT workspace, have an administrator import the repository as a plugin marketplace from **Workspace settings > Plugins > Marketplaces**.
3. Install `Personal Skills Core` from the marketplace and test it in a new web chat.

This is the appropriate distribution route for a workspace-managed plugin catalog and for Codex. In Codex, add the marketplace with both `.agents/plugins` and `plugins` included in any sparse checkout.

## Install on an individual ChatGPT Web account

The ChatGPT Web Skills interface accepts individual `.skill`, `.zip`, or `SKILL.md` uploads; it does not expose a personal GitHub marketplace-import control on every account type. Upload each folder under `plugins/personal-skills-core/skills/` as its own `.skill` archive through **Skills > Create > Upload from computer**. ChatGPT scans each uploaded skill before it is installed.

`skill-upload-bundles/` is a local, ignored build output for this upload path. It is not part of the GitHub marketplace source.

Do not add an `.mcp.json` file to this plugin merely to reach local tools: that can make a plugin desktop-only. Add a remote MCP app only after defining authentication, data boundaries, allowed actions, and an approval model.
