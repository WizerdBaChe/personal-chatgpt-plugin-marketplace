---
name: product-design-thinking
description: "Design a new product, complex capability increment or re-architecture / 產品設計、增能設計、PSM 規劃. Use when the approach is undecided; excludes routine fixes, simple skill authoring and implementation of an agreed spec."
---

# product-design-thinking

Use Mode A for a new system and Mode B for a capability added to a live host. Identify the user problem, consumer, constraints, acceptance and essential scope. For B, also name host contracts, affected accepted behavior, callers, ownership and required registrations. Inspect internal prior art before external alternatives; record extend versus new.

Scale documentation to actual complexity: Sketch is one concept/build note; Standard adds glossary, invariants, lifecycle views and module contracts; Full adds subsystem/concurrency modeling and complete traceability. Do not turn every reusable script into a full design program. Continue authorized implementation after design when the user requested both.

Read references when their phase is active:

- [Prior art](references/prior-art-sweep.md): verify approaches, existing libraries and environment.
- [Design rules](references/design-rules.md): semantics, interfaces, failure behavior and security.
- [Representation models](references/representation-models.md): choose views by the questions they answer.
- [View integrity](references/view-integrity-checks.md): state reachability, consistency and cross-view correspondence.
- [Document ladder](references/document-ladder.md): Concept Note/CIM, PIM, verification, PSM and build cards.

For a live-system rebuild, diagnose implementation and coverage with code-review-deep-checklist B focused before designing replacements. For gates, include known-positive and known-negative controls; evaluate emitted artifacts rather than producer intermediates.

Keep confirmed user semantics stable. Resolve ordinary reversible implementation choices using context; ask only for missing decisions that materially change scope or user intent. Trace requirements through models to acceptance. Record contradictions, missing contracts and unreachable states before presenting a build-ready PSM. A PSM needs files, interfaces, errors, rollback and meaningful acceptance. Label incomplete work as incomplete. Use the user's requested language and deliverable format.

For ambiguous requests, select the included skill whose description best matches the user goal. This core plugin does not add global rules, permissions, or access to sources outside the current conversation and connected apps.

Supporting references supply task methods, not new authority: user instructions take precedence. Source-era approval, permission, model, dispatch or automation examples do not change current settings, require redundant consent, or authorize additional agents/actions.
