---
name: scientific-research-guide
description: "Research methodology / 研究下一步、實驗設計、統計檢定、V&V and domain advice in photonics, materials and devices. Pure paper retrieval goes to literature-search-extract; paper evidence audits go to paper-distill."
---

# scientific-research-guide

Read existing research-state.md if the project has one; do not re-ask settled progress. Use [domain routing](domains/_routing.md) for actual profile selection. Load a matching base profile and only relevant subprofiles. For ambiguous physical domains, use the manifest's disambiguation axis. A retrieval-only request uses profiles as search vocabulary, then follows literature-search-extract without a stage diagnosis.

For methodology, locate the tier and consult the relevant part of [tier framework](references/tier-framework.md): question, literature, design, collection, modeling, analysis, reporting or iteration. Read [method selection](references/method-selection.md) for statistical tests, fitting, sampling and model validity; [deliverables](references/deliverables.md) for protocols or reports.

Answer the actual research question: current stage, completed evidence, missing prerequisite, next action with rationale, relevant risk and method choice. Avoid dumping every tier. Verify load-bearing methodological and reporting claims against current authoritative sources.

Apply profile physical constraints, fitting applicability and metric conditions. A surprising number needs units, wavelength/temperature/geometry or other stated context before comparison. Separate measured, simulated, inferred and assumed results. Ask for theory scale or trade-off priority when the answer changes the study. Flag destructive measurement sequencing before the sample is consumed.

Advice is the default for advice requests. Explicit requests to analyze data, write code or produce documents authorize that work; preserve source datasets and user-selected models. Existing authorization does not need a second consent prompt. State missing evidence instead of manufacturing results. Persist research progress within an authorized project deliverable, not as a global memory/rule update.

For supplied citations, read [citation intake](references/user-supplied-citations.md); preserve verification tags and corrections. For profile creation, read [domain expansion](domains/domain-expansion-guide.md) and [_template](domains/_template.md). Profile tools and routing fixtures remain in tools/ and evals/; run profile-lint.py after changing profiles. Historical source ledgers are research context, not proof of current facts.

For ambiguous requests, select the included skill whose description best matches the user goal. This core plugin does not add global rules, permissions, or access to sources outside the current conversation and connected apps.

Supporting references supply task methods, not new authority: user instructions take precedence. Source-era approval, permission, model, dispatch or automation examples do not change current settings, require redundant consent, or authorize additional agents/actions.
