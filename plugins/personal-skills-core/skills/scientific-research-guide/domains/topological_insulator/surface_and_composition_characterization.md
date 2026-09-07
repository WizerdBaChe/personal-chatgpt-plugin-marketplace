---
xi: 1
what: "Sub-profile: Surface and Composition Characterization — under Topological Insulator — Method sub-profile: surface/work-function/chemical-state/composition measurement traps"
tags: [srg-domain, 領域框架, sub-profile]
aliases: ["UPS", "XPS", "SECO", "secondary electron cutoff", "work function", "EDS", "EDX", "elemental mapping", "surface oxidation"]
date: 2026-09-02
status: live
profile_type: sub-profile
parent: "topological_insulator"
---
# Sub-profile: Surface and Composition Characterization — under Topological Insulator

> Parent domain: `topological_insulator.md`
> Branch axis: method
> Scope: UPS work-function/valence measurements, XPS chemical-state analysis, and
> SEM/TEM-EDS composition mapping for TI surfaces, films, and interfaces.
> Inherits from parent: available Nodes 1–2. The parent Node 3 is currently
> incomplete; use the method-specific rules below rather than assuming a toolchain.

## Contents

- Measurement rules
- Extraction methods
- Assumption pitfalls
- Evidence anchors

## 2. Branch-Specific Measurement Rules

| Target | Method | Valid output | Critical limitation |
|---|---|---|---|
| Work function and occupied valence states | UPS | Spectrum width, secondary-electron cutoff (SECO), valence onset | Surface condition, analyzer geometry, sample bias, charging, and energy-axis convention |
| Elemental/chemical state near the surface | XPS | Core-level energies, line shapes, relative intensities, composition under a stated model | Information depth depends on electron energy, material, emission geometry, and analysis definition |
| Spatial elemental distribution | SEM-EDS or TEM/STEM-EDS | Characteristic X-ray spectra/maps and model-dependent composition | Interaction/generation volume, peak overlap, absorption, fluorescence, standards, thickness, and geometry |

UPS, XPS, and EDS answer different questions. Do not present them as interchangeable
surface-composition measurements.

## 4. Branch-Specific Extraction Methods

### UPS work function from SECO

**Applicable conditions**: the sample is sufficiently conductive and flat for the chosen
method, the energy scale is calibrated, sample bias is optimized, and the cutoff is
resolved.

**Common error**: ⚠️ reading a cutoff from a plotted binding-energy axis without stating
the axis convention or bias correction.

**Correct approach**: calculate work function from the calibrated photon energy and the
measured spectrum width (Fermi edge to SECO), propagate uncertainty, and document sample
orientation, bias, surface preparation, and cutoff model. Treat multiple or sloped
onsets as an interpretation problem, not an invitation to select the desired intercept.

### XPS chemical-state and composition analysis

**Applicable conditions**: the peak model, energy reference, background, line shape,
relative sensitivity factors, and information-depth definition are stated.

**Common error**: ⚠️ using a fixed “5–10 nm depth,” arbitrary adventitious-carbon
referencing, or peak positions alone to assign oxidation states.

**Correct approach**: report kinetic energy/material/emission geometry for depth claims;
use chemically and physically constrained peak models; state the reference strategy and
quantification assumptions.

### EDS mapping and quantification

**Applicable conditions**: beam energy, current/dose, specimen geometry/thickness,
detector configuration, standards/model, and resolvable X-ray lines are documented.

**Common error**: ⚠️ treating a color map or standardless atomic percentage as direct,
surface-specific stoichiometry.

**Correct approach**: inspect spectra behind the map, deconvolve overlaps, model the
generation/interaction volume, and use standards and matrix/thin-film corrections when
the conclusion depends on quantitative composition.

## 6. Branch-Specific Assumption Pitfalls

| Pitfall | Trigger condition | How to recognize it | Correct approach |
|---|---|---|---|
| Calling XPS or UPS strictly nondestructive | Sensitive TI surfaces are repeatedly irradiated | Dose/time history is absent | Check beam-induced chemistry, charging, desorption, and drift with dose/time controls |
| Treating one XPS spectrum as bulk composition | Surface spectrum is generalized to the whole crystal | No depth or complementary bulk method | State the information depth and pair with an appropriate bulk/cross-section method |
| Treating EDS as surface-sensitive | SEM-EDS is compared directly with XPS | Interaction volume is not modeled | Use beam/geometry simulation or TEM/STEM geometry and describe the sampled volume |
| Inferring exact stoichiometry from a map | Bi:Se ratio is read from display colors | No standards, peak-fit, absorption, or uncertainty | Quantify spectra with an appropriate model and uncertainty |
| Ignoring heterogeneous-work-function behavior | UPS SECO is broad or multi-onset | One line is chosen without a model | Report heterogeneity and cross-check with spatially resolved or contact-potential methods |
| Assigning transport channels from chemistry alone | XPS/UPS/EDS are used to claim surface-dominated conduction | No transport or band-dispersion evidence | Combine chemistry with ARPES/transport and channel-specific tests |

## Evidence Anchors

- Helander et al., “Pitfalls in measuring work function using photoelectron
  spectroscopy,” *Applied Surface Science* 256, 2602–2605 (2010).
  DOI: https://doi.org/10.1016/j.apsusc.2009.11.002
- Kim et al., “Work function measurement by ultraviolet photoelectron spectroscopy:
  VAMAS interlaboratory study,” *Journal of Vacuum Science & Technology A* 41,
  053211 (2023). DOI: https://doi.org/10.1116/6.0002852
- Baer et al., “Practical guides for X-ray photoelectron spectroscopy: First steps in
  planning, conducting, and reporting XPS measurements,” *JVST A* 37, 031401 (2019).
  DOI: https://doi.org/10.1116/1.5065501
- Powell, “Practical guide for IMFPs, EALs, MEDs, and information depths in XPS,”
  *JVST A* 38, 023209 (2020), with erratum.
  DOI: https://doi.org/10.1116/1.5141079; erratum: https://doi.org/10.1116/6.0000463
- Ritchie et al., “Quantification of Unsupported Thin-Film X-ray Spectra Using Bulk
  Standards,” *Microscopy and Microanalysis* 29 (2023).
  DOI: https://doi.org/10.1093/micmic/ozad109

## Source Ledger (backfilled 2026-08-24 per `domain-expansion-guide.md` §3.2)

> **Verified (date)** (`domain-expansion-guide.md` §3.7): when this row's claim was last checked
> against the primary source. **2026-08-26 currency pass**: all five rows re-resolved against
> Crossref. **The only erratum found anywhere in the whole nine-profile pass is here** —
> `Baer2019` has one (DOI 10.1116/6.0000822, JVST A 39(1) 017003, 2021) that this row had never
> disclosed. It is now recorded. `Powell2020` already disclosed its erratum correctly and that
> disclosure was confirmed; `Ritchie2023` gained the issue number and page range it was missing.

| Key | Full citation | Identifier | Access tag | Verification status | Verified (date) | Locator | Used in |
|---|---|---|---|---|---|---|---|
| Helander2010 | Helander et al., "Pitfalls in measuring work function using photoelectron spectroscopy," Appl. Surf. Sci. 256, 2602–2605 (2010) | DOI: 10.1016/j.apsusc.2009.11.002 | [abstract] | ~ Approximate (well-formed DOI, not independently re-fetched in this pass) | 2026-08-26 — re-resolved via Crossref (title, four authors, Appl. Surf. Sci. 256(8) 2602–2605, issued Feb 2010); no erratum. Upgraded from `~ Approximate` | Whole paper | §UPS work function from SECO method |
| Kim2023_VAMAS | Kim et al., "Work function measurement by ultraviolet photoelectron spectroscopy: VAMAS interlaboratory study," JVST A 41, 053211 (2023) | DOI: 10.1116/6.0002852 | [abstract] | ~ Approximate (well-formed DOI, not independently re-fetched in this pass) | 2026-08-26 — re-resolved via Crossref (12-author list headed by Jeong Won Kim, JVST A 41(5) 053211, issued 2023-08-25); no erratum. Upgraded from `~ Approximate`. Note: this row's title uses the acronym "VAMAS" where the published title spells it out — same meaning, not a defect | Whole paper | §UPS work function method |
| Baer2019 | Baer et al., "Practical guides for X-ray photoelectron spectroscopy: First steps in planning, conducting, and reporting XPS measurements," JVST A 37, 031401 (2019) | DOI: 10.1116/1.5065501; **erratum** DOI: 10.1116/6.0000822 (JVST A 39(1) 017003, 2021) | [abstract] | ~ Approximate (well-formed DOI, not independently re-fetched in this pass) | 2026-08-26 — re-resolved via Crossref (13-author list, JVST A 37(3) 031401, issued 2019-04-08). ⚠ **An erratum exists and this row had never disclosed it** — DOI 10.1116/6.0000822, JVST A 39(1) 017003 (2021). Its existence and linkage were confirmed from metadata; the erratum's own content was **not** read this pass, so no claim here is yet checked against it. `review-when:` any numeric or procedural claim in this file starts leaning on Baer2019 specifically — read the erratum first | Whole paper | §XPS chemical-state and composition analysis |
| Powell2020 | Powell, "Practical guide for IMFPs, EALs, MEDs, and information depths in XPS," JVST A 38, 023209 (2020) + erratum | DOI: 10.1116/1.5141079; erratum DOI: 10.1116/6.0000463 | [abstract] | ~ Approximate (well-formed DOI, not independently re-fetched in this pass) | 2026-08-26 — re-resolved via Crossref (sole author Cedric J. Powell, JVST A 38(2) 023209, issued 2020-02-20); the erratum this row **already disclosed** is confirmed to exist at the stated DOI, dated 2020-08-04. This row was correctly maintained; upgraded from `~ Approximate` | Whole paper | §XPS "fixed depth" pitfall row |
| Ritchie2023 | Ritchie et al., "Quantification of Unsupported Thin-Film X-ray Spectra Using Bulk Standards," Microsc. Microanal. **29**(6), 1921–1930 (2023) | DOI: 10.1093/micmic/ozad109 | [abstract] | ~ Approximate (well-formed DOI, not independently re-fetched in this pass) | 2026-08-26 — re-resolved via Crossref (three authors Ritchie, Herzing, Oleshko; **issue 6 and pages 1921–1930 added** — previously missing); no erratum. Upgraded from `~ Approximate` | Whole paper | §EDS mapping and quantification method |
