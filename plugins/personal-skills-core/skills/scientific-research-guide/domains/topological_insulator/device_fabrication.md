---
xi: 1
what: "Sub-profile: TI Device Fabrication and Geometry — under Topological Insulator — Method sub-profile: TI device process, geometry, and tool-identification traps"
tags: [srg-domain, 領域框架, sub-profile]
aliases: ["PMMA 950", "electron-beam lithography", "EBL", "mesa", "Hall bar", "TFT response", "KOH", "consort", "COMSOL", "CST", "etching"]
date: 2026-09-02
status: live
profile_type: sub-profile
parent: "topological_insulator"
---
# Sub-profile: TI Device Fabrication and Geometry — under Topological Insulator

> Parent domain: `topological_insulator.md`
> Branch axis: method
> Scope: PMMA electron-beam lithography, mesa/Hall-bar isolation, wet/dry etching,
> ambiguous KOH process notes, and simulation-tool identification for TI devices.
> Inherits from parent: available Nodes 1–2. The parent Node 3 is currently
> incomplete; use the method-specific rules below rather than assuming a toolchain.

## Contents

- Preparation rules
- Process-to-transport validation
- TFT/FET response handoff
- Assumption pitfalls
- Evidence anchors

## 2. Branch-Specific Preparation Rules

### PMMA 950-series resist

- Interpret `950` as the nominal high-molecular-weight PMMA resist family, not a complete
  recipe.
- Treat solids content, solvent, spin speed, bake, exposure dose, development, resist
  thickness, and lift-off stack as process-specific variables.
- Use the current supplier datasheet and the local tool's qualified process. Do not
  transplant the attachment's example dose, thickness, or bake recipe into a protocol.
- Check whether polymer residue, solvent exposure, heating, charging, or ion etching can
  alter the TI surface or contacts.

### Mesa and Hall-bar geometry

- A mesa electrically isolates the intended current path by removing or deactivating
  surrounding conductive material.
- Fabrication order is process-dependent. Do not claim that mesa etching is always the
  final step or always follows contacts/gates.
- Verify sidewall damage, redeposition, undercut, contact placement, leakage paths, and
  the as-fabricated dimensions used in transport calculations.

### KOH note

`KOH non-doped modulation`, `KOH crystal growth`, and `KOH separation` are not
recognized as one unambiguous process from the supplied text. KOH can serve different
roles in substrate etching, sacrificial release, cleaning, or material-specific
chemistry. Do not store a guessed mechanism as domain knowledge. Require the original
process flow, substrate/film stack, concentration, temperature, time, and intended
reaction before classifying it.

### Simulation-tool note

`consort` is unresolved. COMSOL Multiphysics, CST Studio Suite, and dedicated mode
solvers support different workflows. Confirm the actual program, module, solver type,
boundary conditions, and outputs before translating the note or reproducing a model.

## 4. Branch-Specific Validation Methods

### Process-to-transport validation

**Applicable conditions**: transport changes are interpreted after lithography, etching,
cleaning, passivation, or metallization.

**Common error**: ⚠️ attributing a resistance, mobility, WAL, or gating change to
intrinsic TI physics without a pre/post-process control.

**Correct approach**: compare unprocessed/control devices, characterize geometry and
surface chemistry, record thermal/chemical/beam history, and separate geometry/contact
effects from material-channel effects.

### TFT/FET response handoff

`TFT response` in the supplied notes is a device-level output, not a fabrication step
or a material identity. Before interpreting transfer or output curves, record the gate
stack and sweep protocol, leakage, hysteresis, channel geometry, contacts, temperature,
and whether the reported mobility is field-effect, Hall, or another defined quantity.
Route detailed transistor modeling to a future device-physics profile rather than
deriving it from Hall or surface-spectroscopy results alone.

## 6. Branch-Specific Assumption Pitfalls

| Pitfall | Trigger condition | How to recognize it | Correct approach |
|---|---|---|---|
| Copying a generic PMMA recipe | User asks for a “standard PMMA 950 process” | Tool, thickness, substrate, and target feature are absent | Start from supplier/local qualified process and run a dose/process matrix |
| Treating mesa dimensions as design values | Mobility or resistivity uses nominal geometry | No post-etch metrology | Use measured channel width/thickness and propagate uncertainty |
| Ignoring process-induced TI degradation | Transport changes after resist/etch processing | No unprocessed control or surface check | Add controls and surface/geometry characterization |
| Assuming KOH is non-doping | KOH exposure is called structural only | No post-process composition or transport evidence | Verify chemistry and electrical effect; do not infer from intent |
| Assuming `consort` means COMSOL | A misspelled tool name is normalized silently | No project file, screenshot, or solver output | Ask for provenance and identify the actual solver |
| Claiming a simulated mode from a software screenshot | No mesh, material data, boundary, or convergence evidence | Only a field image is shown | Require solver settings, complex material model, convergence, and independent checks |

## Evidence Anchors

- Kayaku Advanced Materials, PMMA positive-resist product page and current technical
  data-sheet landing page:
  https://kayakuam.com/product/structsure/pmma-positive-resists
  and https://tdsdownload.kayakuam.com/pmma-tds-download-landing-page-0
- Liu et al., “Magnetic topological insulator heterostructures: A review,”
  *Advanced Materials* 35, 2102427 (2023), including TI Hall-bar fabrication routes.
  DOI: https://doi.org/10.1002/adma.202102427
- NIST Hall-effect measurement guide for geometry, contacts, and van der Pauw
  assumptions:
  https://www.nist.gov/pml/nanoscale-device-characterization-division/popular-links/hall-effect

## Source Ledger (backfilled 2026-08-24 per `domain-expansion-guide.md` §3.2)

> **Verified (date)** (`domain-expansion-guide.md` §3.7): when this row's claim was last checked
> against the primary source. **2026-08-26 currency pass**: all three rows re-checked; no errata.
> `Liu2023_MagneticTI` was cited as "Liu et al." but has **exactly two authors**. The shared
> `NIST_HallGuide` page is live but now carries NIST's own "no longer updated" banner.

| Key | Full citation | Identifier | Access tag | Verification status | Verified (date) | Locator | Used in |
|---|---|---|---|---|---|---|---|
| KayakuPMMA | Kayaku Advanced Materials, PMMA positive-resist product page + technical datasheet landing page | kayakuam.com/product/structsure/pmma-positive-resists; tdsdownload.kayakuam.com/pmma-tds-download-landing-page-0 | [partial] (vendor page, not a paper) | ~ Approximate — **partially re-checked 2026-08-26**: the technical-datasheet landing page is confirmed live (PMMA and copolymer MMA(8.5)MAA resists offered); the product page returned HTTP 403 to automated fetch, so only one of the two recorded URLs was re-observed | 2026-08-26 (one of two vendor URLs re-observed; the other blocked) | Product/datasheet pages | §PMMA 950-series resist rules |
| Liu2023_MagneticTI | **Liu & Hesjedal**, "Magnetic topological insulator heterostructures: A review," Adv. Mater. **35**(27), 2102427 (2023) | DOI: 10.1002/adma.202102427 | [abstract] | ✅ Confirmed — **citation form corrected 2026-08-26**: Crossref gives **exactly two authors** (Jieyi Liu, Thorsten Hesjedal), so the previous "Liu et al." overstated the byline. Issue number added; no erratum | 2026-08-26 | Whole paper | §Mesa and Hall-bar geometry background |
| NIST_HallGuide | NIST, "Hall Effect Measurements," archived measurement guide | URL: nist.gov/pml/nanoscale-device-characterization-division/popular-links/hall-effect | [partial] (web guide, not a peer-reviewed paper) | ✅ Confirmed live 2026-08-26 — fetched, content matches the described scope. ⚠ The page now carries NIST's own "no longer updated, retained for reference" banner: treat it as a frozen archive, not current guidance. `review-when:` NIST publishes a replacement guide. (Same source also used in `wal_hln_transport.md`, where this row agrees) | 2026-08-26 | Whole guide | General Hall-bar geometry/contact assumptions |
