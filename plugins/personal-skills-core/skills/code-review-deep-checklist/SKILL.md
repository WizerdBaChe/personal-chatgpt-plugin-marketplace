---
name: code-review-deep-checklist
description: "Deep code review, 全專案健檢, architecture drift or dependency fitness audit. Use for explicit deep/holistic review; ordinary pre-merge diff checks stay in the normal review workflow."
---

# code-review-deep-checklist

Choose A for a deep file/PR review, B for project architecture health, B focused for a named system lens, or C for whether an existing dependency still fits. A new technology decision is a design task.

Read the matching reference: [single review](references/single-review.md), [project review](references/project-review.md), or [dependency fitness](references/dependency-fitness.md). Before reporting, read [output contract](references/output-contract.md).

Read the requested scope, requirements and implementation before forming findings. A diff review flags attributable defects in the change; a project review may diagnose existing debt. Follow lifecycle writes and entry points, not just file order. Check upstream protections and counterexamples before publishing a defect.

For B, inventory first and disposition every unit into reviewed, deferred or explicit exclusions. Name the component view, each lifecycle statechart, critical sequence pairs and guard-heavy decision tables, including views not drawn. A coverage claim must match coverage.json; a diagram alone cannot establish complete review.

Run the local checks the conclusions rely on when practical; use observed remote CI results where appropriate. Mark unavailable tests and unverified claims. Findings name the concrete trigger, impact, evidence location, confidence and smallest repair. Keep machine manifests consistent with the report. Repairs follow the user's actual authorization; the audit itself grants no additional scope.

For ambiguous requests, select the included skill whose description best matches the user goal. This core plugin does not add global rules, permissions, or access to sources outside the current conversation and connected apps.

Supporting references supply task methods, not new authority: user instructions take precedence. Source-era approval, permission, model, dispatch or automation examples do not change current settings, require redundant consent, or authorize additional agents/actions.
