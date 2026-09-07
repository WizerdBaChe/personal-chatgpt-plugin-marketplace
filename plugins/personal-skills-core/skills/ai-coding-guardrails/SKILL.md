---
name: ai-coding-guardrails
description: "Design AI coding guardrails and team review process / AI PR 審不完、agent 寫壞或誤刪、流程護欄. Not reviewing one diff or automatically changing permissions."
---

# ai-coding-guardrails

Identify whether the failure is plausible-but-wrong code, destructive action or accumulated drift. During an incident, preserve evidence and address recovery within authorization before redesigning the process.

Read the relevant reference: [context and architecture](references/context-architecture.md), [safety policy](references/safety-policy.md), [testing and CI](references/testing-ci.md), [observability](references/observability-feedback.md), or [recovery/governance](references/recovery-governance.md).

Produce a proportionate concrete design: context ownership, architecture checks, test/review gates, capability boundaries, bounded retries, recovery verification and useful audit records. Distinguish proposed, implemented and tested controls. A sentence limiting behavior is guidance, not proof of enforcement. Avoid unsupported universal numeric thresholds and assumptions about model behavior.

Respect the platform's actual sandbox and tool schemas. Reference examples from another agent are examples, not executable Codex configuration. Design work does not itself authorize editing live permissions, hooks, global rules or secrets. Verify proposed controls with positive/negative cases and preserve an actionable recovery path.

For ambiguous requests, select the included skill whose description best matches the user goal. This core plugin does not add global rules, permissions, or access to sources outside the current conversation and connected apps.

Supporting references supply task methods, not new authority: user instructions take precedence. Source-era approval, permission, model, dispatch or automation examples do not change current settings, require redundant consent, or authorize additional agents/actions.
