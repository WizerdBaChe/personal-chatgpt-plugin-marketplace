---
xi: 1
what: "Plasmonic Waveguide (Plasmonic Waveguide) — Plasmonic/SPP waveguide domain profile"
tags: [srg-domain, 領域框架, base]
aliases: ["SPP", "plasmonics", "surface plasmon", "nanophotonic waveguide", "SERS", "near-field optics"]
date: 2026-08-26
status: live
profile_type: base
parent: "-"
---
# Domain Profile: Plasmonic Waveguide (Plasmonic Waveguide)

> Scope of applicability:
> Surface plasmon polariton (SPP) guided-wave structures at metal-dielectric interfaces; passive and quasi-passive plasmonic waveguides; dielectric-loaded, long-range, and hybrid plasmonic waveguide geometries; waveguide-level measurement, modeling, fitting, and interpretation.
> Scientific nature:
> Electromagnetics, wave physics, optical material response, nanoscale light-matter interaction.
> Engineering nature:
> Nanophotonics, integrated photonics, plasmonic device design, nanoscale metrology, numerical modeling.
>
> Profile metadata:
> - Profile ID: DP-PLWG-001
> - Profile version: 1.2-draft (Source Ledger backfilled 2026-08-24, one author-attribution error corrected; §3.7 currency pass 2026-08-26 — a dead DOI on Berini2005 corrected, Messner2023's DOI resolved, two access tags upgraded)
> - Last updated: 2026-08-26
> - Author(s) / Maintainer(s): Generated working draft for SKILL knowledge-base authoring
>
> Primary source types:
> - Textbooks: Maier, *Plasmonics: Fundamentals and Applications* (2007)
> - Review articles: Messner et al., *Plasmonic, photonic, or hybrid? Reviewing waveguide geometries for electro-optic modulators* (2023); Kumar et al. (Bozhevolnyi corresponding), *Dielectric-loaded plasmonic waveguide components: Going practical* (2013) — attribution corrected 2026-08-26; this line still carried the "Holmgaard and Bozhevolnyi" error that Node 7a fixed on 2026-08-24, an example of a correction that did not propagate out of the node it was made in
> - Methods / standards papers: Johnson and Christy, *Optical Constants of the Noble Metals* (1972); Berini et al., *Characterization of long-range surface-plasmon-polariton waveguides* (2005)
> - Other (e.g. datasheets, industry standards): Thin-film permittivity measurements and geometry-specific numerical benchmarking studies
>
> Notes for AI use:
> - Intended use: Foundational reference for reasoning about plasmonic waveguide physics, modeling, measurement, and interpretation before moving to active-device applications.
> - Terminology supplement: if a local terminology/glossary vault is available, consult it
>   before answering a pure what-does-this-term-mean question — precise per-term definition
>   cards with source tiers and dispute flags are more reliable there than a profile's own
>   prose. This domain's lookup key (DomainPath) is `photonics/`; the reference
>   implementation as of 2026-08 is LexiconVault. This is a swappable slot, not a hard
>   dependency (see `domain-expansion-guide.md` §3.1) — without one, fall back to this
>   file's own Node 1 terminology and to `plasmonic_waveguide/terminology_and_geometry.md`.
> - Validation status / usage note: Suitable as a baseline domain profile for passive and quasi-passive waveguide analysis; modulator-specific metrics such as extinction ratio and electro-optic bandwidth are intentionally out of scope.

---

## 1. Theoretical Framework Anchoring

### Core first principles

| Scale / problem type | Foundational theory | Core physical quantity |
|------------|---------|-----------|
| Metal optical response | Maxwell equations with complex constitutive relations | Complex permittivity \(\varepsilon(\omega)\), refractive index, loss tangent |
| Free-electron-dominated metal response | Drude or Drude-Lorentz description, with caution at optical frequencies | Plasma frequency, damping rate, interband contribution |
| Single metal-dielectric interface | Boundary-condition solution for surface plasmon polaritons | SPP wave vector, penetration depth, modal confinement |
| Guided plasmonic structure | Eigenmode theory in open, lossy waveguides | Effective index, complex propagation constant, mode area |
| Real fabricated waveguide | Perturbation from roughness, finite thickness, substrate asymmetry, and coupling structures | Propagation loss, coupling efficiency, fabrication tolerance |

### Core definitions and baseline equations

For a planar metal-dielectric interface, the SPP dispersion relation is commonly written as

$$
k_{SPP} = k_0 \sqrt{\frac{\varepsilon_m \varepsilon_d}{\varepsilon_m + \varepsilon_d}}
$$

where $k_0 = \omega/c$, $\varepsilon_m$ is the metal permittivity, and $\varepsilon_d$ is the dielectric permittivity.

The complex propagation constant is typically written as

$$
\beta = \beta' + i\beta''
$$

where $\beta'$ governs phase propagation and $\beta''$ governs attenuation. A common propagation-length definition is

$$
L_{prop} = \frac{1}{2\beta''}
$$

for power decay to $1/e$.

The existence of a bound SPP mode at a simple interface typically requires a metal with negative real permittivity and a magnitude relationship that allows an interface-bound TM-polarized solution.

### Inviolable physical constraints (the AI should warn the user here)

1. **Confinement-loss trade-off**: stronger subwavelength confinement generally increases overlap with lossy metal regions and therefore increases propagation loss.
2. **Momentum-matching constraint**: free-space illumination does not usually satisfy the in-plane momentum required for direct SPP excitation, so prisms, gratings, edges, or near-field couplers are required.
3. **Material-data validity constraint**: optical-frequency Au and Ag behavior cannot be treated reliably by a simplistic Drude-only fit for final results; interband transitions matter.
4. **Scale-validity constraint**: when feature sizes approach the deep-nanometer regime, nonlocal response, spill-out, and other beyond-local effects can invalidate purely local classical models.
5. **Geometry sensitivity constraint**: substrate asymmetry, thin-film morphology, and sidewall roughness can shift mode properties enough that ideal symmetric models become misleading.

> **Decision point (mandatory Tier 0 confirmation)**: when the user describes a plasmonic waveguide design problem,
> the AI must confirm:
> "Is your priority (A) longest propagation length, (B) strongest confinement, or (C) the best confinement-loss trade-off?"
> The three goals correspond to different geometries, materials, and validation strategies.

---

## 2. Measurement Tool Inventory

### Mode and field characterization

| Measurement target | Tool | Output information | Applicable conditions | Common misuse | Source [Key] |
|---------|------|---------|---------|---------|---------|
| Near-field intensity distribution | Near-field scanning optical microscopy (NSOM/SNOM) | Spatial field map, modal localization, decay profile | Subwavelength probe access and stable scanning | Treating probe-perturbed fields as the unperturbed native mode | — (general technique knowledge) |
| Leakage radiation from supported plasmonic modes | Leakage radiation microscopy (LRM) | Real-space and Fourier-space information on propagation and directionality | Structures with leakage into substrate or collection path | Assuming every guided mode is observable by leakage radiation | — (general technique knowledge) |
| Excitation condition at planar or thin-film interfaces | Attenuated total reflection (ATR) / prism coupling | Reflectivity dip versus angle or wavelength, resonance condition | Prism-coupled or Kretschmann-like structures | Interpreting dip position without accounting for metal thickness sensitivity | — (general technique knowledge) |
| Mode profile and coupling behavior | Far-field imaging with designed out-couplers | Relative mode content and coupling trends | Structures with engineered scattering or grating outputs | Confusing out-coupler efficiency variation with intrinsic propagation change | — (general technique knowledge) |

### Propagation and loss characterization

| Measurement target | Tool | Output information | Applicable conditions | Common misuse | Source [Key] |
|---------|------|---------|---------|---------|---------|
| Propagation length | Spatial decay measurement from near-field or distributed out-scattering | \(L_{prop}\), decay constant | Single dominant mode and known out-scattering behavior | Fitting geometric scattering loss and intrinsic propagation loss as one quantity | — (general technique knowledge) |
| Waveguide attenuation | Cut-back method | Propagation loss per unit length after separating coupling loss | Multiple nominally identical lengths | Using a single device length and calling total insertion loss "waveguide loss" | Berini2005 (waveguide-level cut-back framing) |
| Coupling efficiency | Input-output power measurement with known launch geometry | Launch efficiency into the guided plasmonic mode | Reproducible couplers and reference structures | Mixing coupling variation with intrinsic waveguide performance | — (general technique knowledge) |
| Thin-film optical constants for model input | Ellipsometry | Complex permittivity or refractive index of deposited films | Separate calibration films or representative fabrication stacks | Extracting bulk constants from a patterned device structure | JohnsonChristy1972 (canonical bulk-constant anchor being cautioned against for patterned structures) |

### Geometry and fabrication characterization

| Measurement target | Tool | Output information | Applicable conditions | Common misuse | Source [Key] |
|---------|------|---------|---------|---------|---------|
| Lateral dimensions and pattern fidelity | SEM | Width, spacing, edge roughness trend | Conductive coating or charge management as needed | Treating SEM edge visibility as exact sidewall metrology | — (general technique knowledge) |
| Surface height and roughness | AFM | Height profile, RMS roughness, local topography | Accessible top surfaces | Using AFM to infer buried interface quality directly | — (general technique knowledge) |
| Cross-sectional stack and interface quality | TEM cross-section / FIB-assisted sectioning | Layer thickness, buried geometry, interface continuity | Destructive sample prep accepted | Ignoring FIB-induced damage or redeposition artifacts | — (general technique knowledge) |

---

## 3. Standard Modeling Toolchain

```
Analytical / semi-analytical interface or simplified waveguide model
→ Output: dispersion, penetration depth, trend-level confinement-loss behavior
    ↓
Eigenmode FEM or frequency-domain mode solver
→ Input: geometry, experimentally grounded permittivity, substrate stack
→ Output: effective index, complex propagation constant, field profile, mode area
    ↓
FDTD or broadband full-wave simulation
→ Input: finite device geometry, couplers, discontinuities, material dispersion
→ Output: transmission trend, scattering, field evolution, coupling behavior
    ↓
RCWA (only for periodic gratings or periodic plasmonic structures)
→ Output: diffraction efficiencies, reflection / transmission spectra, phase response
```

### Toolchain interpretation rules

- Start with the simplest model that preserves the dominant physics.
- Use analytical or semi-analytical models for intuition and parameter scanning.
- Use eigenmode solvers when the main question concerns modal constants, confinement, and propagation loss.
- Use FDTD when discontinuities, couplers, finite sections, or broadband behavior dominate the question.
- Use RCWA only when periodicity is central; it is not a default waveguide solver.

### Material-model caution

The most important modeling input is usually the metal permittivity dataset. For Au and Ag in the optical regime, literature and experimental practice repeatedly show that realistic interband contributions are important and that Johnson and Christy data remain a standard anchor for noble-metal optical constants. Thin films and nanostructures may deviate from bulk-reference values due to morphology, grain structure, roughness, and surface scattering.

---

## 4. Domain-Specific Fitting Methods

> Reformatted 2026-08-24 from a `### Method name` + prose-field layout to a table, to match
> the other three base profiles (see `domain-expansion-guide.md` §3.3) — content unchanged.

| Method | Applicable conditions | Common error | Correct approach | Source [Key] |
|---|---|---|---|---|
| Propagation-length extraction from spatial decay | A single dominant guided mode is observed over a region where distributed scattering is either weak or independently characterized | ⚠️ Fitting the observed intensity decay without separating background light, local scattering hotspots, or multimode beating | Subtract background, inspect the data for multimode or oscillatory behavior, and fit only the spatial region where a physically meaningful exponential decay model is justified | — (general technique knowledge) |
| Cut-back extraction of propagation loss | A family of nominally identical waveguides with different lengths is available | ⚠️ Reporting total input-output loss from a single device as intrinsic waveguide attenuation | Fit total loss versus length so that the slope estimates propagation loss and the intercept absorbs launch and collection loss | Berini2005 |
| Permittivity fitting for simulation-ready material models | Dispersion models are needed for frequency-domain or time-domain simulations | ⚠️ Using a Drude-only fit for Au or Ag over the visible or near-infrared range and then treating the result as quantitatively final | Fit or import a model that reproduces experimentally validated optical-constant data over the actual operating band, and note whether the target is bulk, thin-film, or nanostructure behavior | JohnsonChristy1972 |
| Effective mode-area evaluation | Comparison of confinement across different waveguide geometries or materials | ⚠️ Comparing mode areas computed with inconsistent definitions, normalization choices, or energy-density conventions in lossy and dispersive media | State the mode-area definition explicitly, keep the same normalization across all compared cases, and avoid mixing literature values computed under incompatible conventions | — (general technique knowledge) |

---

## 5. Domain-Specific Quality Metrics

| Metric | Abbreviation | Physical meaning | Typical value range | Conditions | Source [Key] |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Propagation length | $L_{prop}$ | Distance over which guided power decays to $1/e$ | Strongly geometry- and wavelength-dependent; from very short sub-10-µm scales in highly confined structures to much longer values in long-range or hybrid designs | Geometry- and wavelength-dependent; single dominant mode assumed | — (general definition) |
| Propagation loss | $\alpha$ | Attenuation per unit length | Often reported in dB/µm, dB/mm, or $cm^{-1}$; unit choice must be stated explicitly | Unit convention must accompany any value | — (general definition) |
| Effective index | $n_{eff}$ | Modal phase constant normalized by free-space wave number | Usually larger than the cladding index for bound modes; complex in lossy structures | Real and imaginary parts should both be stated for lossy structures | — (general definition) |
| Effective mode area | $A_{eff}$ | Measure of modal confinement | Often far below the diffraction-limited area in strongly confined plasmonic modes | Definition/normalization convention must be stated | — (general definition) |
| Confinement factor | $\Gamma$ | Fraction of modal energy in a target region | Highly definition-dependent; must be tied to a specific region | Target region must be explicitly named | — (general definition) |
| Coupling efficiency | $\eta$ | Fraction of launched power coupled into the target guided mode | Strongly dependent on coupler design and alignment, not only on the waveguide core | Coupler design and alignment method must be stated | — (general definition) |
| Crosstalk | — | Unwanted power transfer between nearby channels | Most important in dense integration or coupled-waveguide layouts | Channel spacing and integration density | — (general definition) |
| Figure of merit | FOM | Composite balance of confinement and attenuation | Not universal; definition must be written explicitly each time | Exact formula must accompany any reported FOM | — (general definition) |

### Metric-usage rules

- Do not compare values across papers unless the metric definition and normalization are compatible.
- Never report a figure of merit without writing its exact formula.
- Keep waveguide metrics separate from modulator metrics such as extinction ratio, bandwidth, or energy per bit.

---

## 6. Common Assumption Pitfalls

| Pitfall | Trigger condition | How to recognize it | Correct approach | Source [Key] |
|------|---------|---------|---------|---------|
| Treating Drude-only Au/Ag as quantitatively final at optical frequencies | Visible or near-IR noble-metal modeling | Simulated resonance or loss disagrees strongly with standard optical-constant references | Use experimentally anchored optical constants or a validated Drude-Lorentz fit | JohnsonChristy1972 |
| Confusing coupling loss with propagation loss | Single-length transmission measurement | Reported loss changes dramatically with coupler redesign | Separate launch loss from propagation attenuation with cut-back or calibrated references | Berini2005 |
| Treating nanostructure permittivity as bulk permittivity without qualification | Thin films, nanowires, ultra-small gaps | Measured behavior is systematically lossier or shifted than simulation | Use thin-film or geometry-aware material data when available | — (general knowledge) |
| Ignoring substrate-induced asymmetry | Hybrid structures placed on dielectric substrates | Symmetric theory predicts behavior not seen in fabricated devices | Include the real substrate stack in the model and discuss asymmetry explicitly | — (general knowledge) |
| Ignoring roughness-driven scattering | Fabricated metal sidewalls or films with nontrivial morphology | Measured loss exceeds smooth-interface predictions | Measure roughness and treat scattering as a separate or additional loss channel | — (general knowledge) |
| Using insufficient mesh refinement at metal-dielectric boundaries | Full-wave simulation with strong field localization | Results change noticeably when mesh is refined | Apply local mesh refinement and perform convergence checks | — (general knowledge) |
| Assuming every measured bright spot represents the native guided mode | Near-field or scattering-based imaging | Hotspots move or change with probe position or out-scatter geometry | Validate mode identity through multiple observables, not one image alone | — (general knowledge) |
| Mixing passive waveguide metrics with active-device metrics | Discussion drifts toward modulators | Extinction ratio or drive conditions start appearing as primary criteria | Keep this profile waveguide-centered and move active-device optimization elsewhere | — (general knowledge) |
| Claiming long propagation together with extreme confinement at no stated cost | User reports or targets record propagation length AND deep-subwavelength confinement simultaneously | The pair would defeat the SPP confinement–propagation–loss trade-off; often the two numbers come from different structures or incompatible metric definitions | Ask for cross-validation by an independent method and the explicit metric conventions (mode-area definition, field vs. intensity decay length) before accepting the pair (moved from the abolished trigger checklist 2026-08-25) | — (general knowledge) |

---

## 7. Literature Anchors

| Type | Reference | Why it matters |
|------|------|-------|
| Foundational textbook | Maier, *Plasmonics: Fundamentals and Applications* (2007) | Standard introductory anchor for plasmonics, metal optics, and SPP fundamentals |
| Optical-constant reference | Johnson and Christy, *Optical Constants of the Noble Metals* (1972) | Canonical experimental dataset for Au and Ag optical constants |
| Waveguide characterization methods | Berini et al., *Characterization of long-range surface-plasmon-polariton waveguides* (2005) | Clear waveguide-level framing using attenuation, coupling efficiency, and confinement |
| Practical waveguide review | Kumar et al. (S. I. Bozhevolnyi, corresponding author), *Dielectric-loaded plasmonic waveguide components: Going practical*, Laser & Photonics Reviews 7, 938–951 (2013) — ⚠️ **corrected 2026-08-24**: this profile originally attributed the paper to "Holmgaard and Bozhevolnyi"; the verified author list is led by A. Kumar, with Bozhevolnyi as corresponding author. Holmgaard does not appear on this specific paper (he co-authored other, earlier DLSPP papers with Bozhevolnyi, which may be the source of the conflation) | Useful review for practical dielectric-loaded plasmonic-waveguide components |
| Comparative geometry review | Messner et al., *Plasmonic, photonic, or hybrid? Reviewing waveguide geometries for electro-optic modulators*, APL Photonics 8, 100901 (2023) | Valuable comparative framework for plasmonic, photonic, and hybrid geometries |
| Hybrid-geometry study | ⚠️ "Studies on asymmetric and hybrid plasmonic waveguides on substrates" — **not a real citation, a placeholder description** (flagged 2026-08-24); no specific paper was ever attached | Was intended to cover geometry sensitivity, substrate asymmetry, and confinement-loss balancing; needs a real replacement source before being relied on |

### Source Ledger (added 2026-08-24, backfilled per `domain-expansion-guide.md` §3.2)

> This profile's Nodes 1–6 were originally written as general domain-knowledge prose with **no inline `[Key]` citation markers** — none of the physics statements in Nodes 1–6 are tied to one specific paper; they represent consensus/textbook-level knowledge. This ledger therefore only tabulates the Node 7a reading list itself (spot-verified 2026-08-24), not per-claim inline citations. A future substantive edit to this profile should add inline `[Key]` markers to Nodes 1–6 where a claim is more specific than general consensus.

> **Verified (date)** (`domain-expansion-guide.md` §3.7): when this row's claim was last checked
> against the primary source — not the source's own publication year.
>
> **2026-08-26 currency pass** (audit trail: `reports/2026-08-26-scientific-research-guide-source-currency-pass.md`).
> Five of the six rows were re-resolved against Crossref (the sixth is the placeholder row, which has
> no source to check). The pass caught **a dead DOI**: `Berini2005` carried `10.1063/1.2010633`, which
> is not a registered DOI — the paper itself, its authors and its bibliographic data were all correct,
> so nothing but the identifier was wrong, and nothing in the 2026-08-24 "verified via search" check
> would have exposed it. Corrected to `10.1063/1.2008385` and independently re-confirmed by the main
> session against the Crossref API. `Messner2023`'s previously-unresolved DOI was located, and two
> access tags were upgraded. `Maier2007` stays `~ Approximate`: its ISBN/publisher record was
> re-resolved, but the textbook was not re-read, and identity-only checking does not earn a ✅ here.

| Key | Full citation | Identifier | Access tag | Verification status | Verified (date) | Locator | Used in |
|---|---|---|---|---|---|---|---|
| Maier2007 | Maier, S.A., *Plasmonics: Fundamentals and Applications*, Springer (2007) | ISBN 978-0-387-33150-8; DOI 10.1007/0-387-37825-1 (book record) | [secondary] (canonical textbook, not individually re-fetched) | ~ Approximate (canonical, well-known text; the ISBN/publisher/DOI record was re-resolved 2026-08-26 and no second edition exists, but the book itself was **not** re-read — identity-only checking does not upgrade this to ✅) | 2026-08-26 (identity only) | Whole textbook | Node 7a; general background for Node 1 |
| JohnsonChristy1972 | Johnson, P.B. & Christy, R.W., "Optical Constants of the Noble Metals," Phys. Rev. B 6, 4370–4379 (1972) | DOI: 10.1103/PhysRevB.6.4370 | [abstract] (still closed access — re-checked 2026-08-26, no open copy found) | ✅ Confirmed (2026-08-24 via search; 2026-08-26 re-resolved against the Crossref record — title, both authors, journal, volume, pages; no erratum) | 2026-08-26 | Whole paper | Node 7a; Node 3 "Material-model caution" |
| Berini2005 | Berini, P., Charbonneau, R., Lahoud, N., Mattiussi, G., "Characterization of long-range surface-plasmon-polariton waveguides," J. Appl. Phys. 98, 043109 (2005) | DOI: 10.1063/1.2008385 — **corrected 2026-08-26**; the previously recorded `10.1063/1.2010633` is not a registered DOI and returns 404 | [abstract] (still closed access — re-checked 2026-08-26) | ✅ Confirmed (2026-08-26: the corrected DOI resolves to this exact paper — title, all four authors in order, J. Appl. Phys. 98(4), article 043109, issued 2005-08-15; no erratum. Independently re-confirmed by the main session against the Crossref API, both that the old DOI 404s and that the new one resolves) | 2026-08-26 | Whole paper | Node 7a |
| Kumar2013 | Kumar, A. et al. (Bozhevolnyi, S.I., corresponding), "Dielectric-loaded plasmonic waveguide components: Going practical," Laser Photonics Rev. 7, 938–951 (2013) | DOI: 10.1002/lpor.201200113 | [full] — **upgraded 2026-08-26**: the article is open access (CC BY-NC 3.0) on the publisher site and the full text was read there, so it is no longer abstract-only | ✅ Confirmed, author correction applied (2026-08-24 — see flagged correction above); re-confirmed 2026-08-26 against the Crossref author list, which begins Kumar, Gosciniak, Volkov (no author count is asserted here — the verifying pass and the main session's own re-check disagreed on whether the record holds 15 or 16 names, and the count is not load-bearing) | 2026-08-26 | Whole paper | Node 7a |
| Messner2023 | Messner, A., Moor, D., Chelladurai, D., Svoboda, R., Smajic, J., Leuthold, J., "Plasmonic, photonic, or hybrid? Reviewing waveguide geometries for electro-optic modulators," APL Photonics 8, 100901 (2023) | DOI: 10.1063/5.0159166 — **resolved 2026-08-26** (previously recorded only as "DOI present on AIP site, not independently resolved") | [abstract] — the journal is fully CC-BY open access by publisher policy (checked 2026-08-26), but the article page itself returned HTTP 403 to automated fetch, so this is a **policy-level, not page-level** access statement and the tag is deliberately not upgraded to [full] | ✅ Confirmed (2026-08-24 via search; 2026-08-26 re-resolved against the Crossref record — title, full six-author list, journal, volume, article number, year; no erratum) | 2026-08-26 | Whole paper | Node 7a |
| — | ⚠️ "Studies on asymmetric and hybrid plasmonic waveguides on substrates" | none | none | ❌ Withdrawn-equivalent: never a real citation, flagged as placeholder | ⚠ not verifiable — no source exists to check | — | Node 7a (row retained as a record of what to replace) |

---

## Cross-Domain Links

### Closest Related Domain Profiles

| Profile name | Overlap dimensions | Typical use split |
|------|------|-------|
| Silicon photonics waveguides | first principles, modeling tools, fabrication tolerance | Prefer the silicon-photonics profile when metal loss is not central and dielectric guiding dominates |
| Plasmonic modulators | geometry, materials, application targets | Prefer this waveguide profile for passive modal reasoning; switch to the modulator profile when bias-driven performance metrics dominate |
| Nanofabrication metrology | measurement tools, interpretation logic | Prefer the metrology profile when the main uncertainty is whether fabricated geometry matches design intent |
| Optical sensing / SERS platforms | confinement, field enhancement, application targets | Prefer this profile for mode and loss interpretation; prefer the sensing profile when analyte interaction and enhancement statistics become primary |

### Boundary & ownership notes

- This profile should remain separate from a plasmonic-modulator profile because the governing metrics and decision logic are not the same.
- It is acceptable for the same geometry to appear in more than one profile, provided each profile evaluates it using different primary criteria.

---

## Cross-Domain Conflict Notes

| Issue / constraint | Other profile(s) involved | Potential conflict | AI confirmation question |
|------|------|-------|-------|
| Long propagation versus compact active functionality | Plasmonic modulators | A geometry that is attractive for long propagation may be suboptimal for strong active modulation or compact switching | Is the priority passive transport performance or active modulation performance? |
| Bulk optical constants versus fabricated thin-film behavior | Nanofabrication metrology | Bulk-reference permittivity may underpredict loss or misplace resonances in real thin films | Should the analysis assume textbook bulk data or fabrication-specific thin-film data? |
| Strong confinement versus sensing robustness | Optical sensing / SERS platforms | A geometry optimized for extreme confinement may be more fabrication-sensitive and less reproducible | Is peak local enhancement or robust reproducible performance the main goal? |

### How the AI should use these prompts

- These conflict prompts should be used early, before the AI commits to a geometry recommendation.
- If a user asks for "best" plasmonic waveguide performance without stating a metric, the AI should ask a clarification question instead of assuming a single universal optimum.
