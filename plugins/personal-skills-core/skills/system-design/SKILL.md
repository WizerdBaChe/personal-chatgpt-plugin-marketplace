---
name: system-design
description: "Backend queue and capacity knowledge / MQ、削峰、outbox、雙寫、backpressure、p99、Little's Law. A focused knowledge pack; whole-system design goes to product-design-thinking."
---

# system-design

Read [message queues](references/message-queue.md) for asynchronous processing, durability, retries, idempotency and dual-write/outbox trade-offs. Read [throughput and latency](references/throughput-vs-latency.md) for load, utilization, service-time variability and tail latency.

Establish whether the actual constraint is capacity, response latency, burst smoothing, isolation or delivery semantics. Do not prescribe a queue just because traffic is high. State when the two references do not cover the question. Verify live technology behavior in current official documentation. For knowledge intake, follow the render-perf INTAKE.md convention only on a retention request; normal answers do not update global memory.

For ambiguous requests, select the included skill whose description best matches the user goal. This core plugin does not add global rules, permissions, or access to sources outside the current conversation and connected apps.

Supporting references supply task methods, not new authority: user instructions take precedence. Source-era approval, permission, model, dispatch or automation examples do not change current settings, require redundant consent, or authorize additional agents/actions.
