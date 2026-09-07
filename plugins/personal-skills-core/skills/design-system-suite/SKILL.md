---
name: design-system-suite
description: "Shared design systems for multiple products / 多產品 design tokens、theme packs、跨產品導航與資料交換. Not a single app styling task."
---

# design-system-suite

Define shared contracts before connecting products: semantic design tokens, a versioned data envelope, cross-product navigation and one capability manifest. Separate shared spacing/type/radius structure from theme-specific semantic colors. Namespace tokens; product-specific colors remain local and must stay legible in every supported theme.

Shared injected navigation should isolate its styles, consume theme tokens with fallbacks, and avoid being masked by host overlays. Document consumers and version compatibility; avoid copying registries into every app.

For a named product, use only artifacts the user supplied, attached, or exposed through an enabled connected app. Treat product-specific theme and persistence conventions as local unless the user provides evidence that they apply to this task.

Register new products once, adopt tokens and exchange contracts, verify navigation and theme switching in the built artifact. Use Sites when building/hosting a site requires it, and the repository's established deploy path otherwise. A design-system task does not itself authorize changes to repository rules or hosting settings.

For ambiguous requests, select the included skill whose description best matches the user goal. This core plugin does not add global rules, permissions, or access to sources outside the current conversation and connected apps.

Supporting references supply task methods, not new authority: user instructions take precedence. Source-era approval, permission, model, dispatch or automation examples do not change current settings, require redundant consent, or authorize additional agents/actions.
