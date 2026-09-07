# Diagram carriers and checks
Use Mermaid for small auto-layout sketches; use explicit SVG coordinates or native PPTX shapes
when alignment, containment or spatial order is part of the meaning. Use the available Presentations
skill for slide mechanics and visualize for interactive in-conversation explanations. Site building
and hosting follow the available Sites skills when applicable.
Before rendering, create a structural source model. Check the delivered artifact for node/edge count,
valid anchors, readable labels, bounds, overlap and missing markers. Geometry checks must inspect
emitted output; appearance requires a rendered view. If a renderer/tool is unavailable, report that
specific check as unverified. A user acceptance decision is separate from an agent's inspection.
For standalone HTML, use a responsive viewport and suitable zoom/pan when needed. Avoid clipping,
unusable tiny type and left-anchored wasted width. Native editable slides keep shapes/connectors
editable instead of baking every diagram into a picture. Use the requested template and aspect ratio.
Deliver regeneration source and evidence gaps with the figure. For a precision deliverable, a hash
receipt can tie validation to the emitted file; any later edit invalidates that receipt.
The original archdiag and browser-pane hook were environment integrations and are not dependencies
of this migrated skill. Their general diagram checks are expressed above without claiming installed
enforcement. A more specialized renderer may be used only after inspecting its current interface.
