---
xi: 1
what: "Adiabatic Taper & Spot-Size Conversion in Integrated Photonics (漸變波導絕熱模態轉換與光纖-晶片耦合) — Adiabatic taper / spot-size conversion in integrated photonics: CMT, adiabaticity criteria, SSC architectures, packaging alignment-tolerance trade-offs"
tags: [srg-domain, 領域框架, base]
aliases: ["adiabatic taper", "spot-size converter", "SSC", "mode converter", "inverse taper", "down-taper", "edge coupler", "GRIN coupler", "coupled mode theory", "CMT", "MFD matching", "MFD", "mode field diameter", "Petermann II", "fiber-to-chip coupling", "spot size conversion"]
date: 2026-08-30
status: live
profile_type: base
parent: "-"
---
# Domain Profile: Adiabatic Taper & Spot-Size Conversion in Integrated Photonics (漸變波導絕熱模態轉換與光纖-晶片耦合)

> Scope of applicability: SiN (silicon nitride) / SOI (silicon-on-insulator) / InP / SiON integrated photonic waveguide taper design, fiber-to-chip and chip-to-chip coupling interfaces, and their packaging trade-offs.
> Scientific nature: Waveguide electromagnetics, coupled mode theory (CMT), adiabatic theorem for guided-wave systems.
> Engineering nature: Photonic packaging, alignment tolerance engineering, wafer-scale vs. serial (TPP) fabrication trade-offs, cost/yield analysis.
>
> Cluster membership: member of the **photonic-packaging** sibling cluster — this profile owns
> *how the optical mode is matched/expanded*; siblings own groove cutting
> (`v_groove_fabrication.md`), placement & fixation (`fiber_chip_passive_alignment.md`), and
> qualification (`siph_packaging_reliability.md`). Split tabulated in `_routing.md` § Clusters
> (deliberately flat — no parent profile exists or should be built).
>
> Profile metadata:
> - Profile ID: PHOT-TAPER-001
> - Profile version: v2.1 (2026-08-30 sixth pass — field-vs-intensity/MFD-convention packet intake: new N6 pitfall, N4 overlap-integral row re-sourced, 7 new Node 7b rows)
> - Last updated: 2026-08-30 (sixth pass — §3.7 currency: 8/8 prior rows unchanged; seven new Source Ledger rows added for a user-supplied explanatory packet on field-vs-intensity and MFD measurement convention, all anchors resolved against primary pages before entering Nodes 4/6, per `domain-expansion-guide.md` §9 step 2)
> - Last updated (fifth pass): 2026-08-26 (§3.7 currency: 8/8 rows re-resolved, two arXiv versions pinned, Weninger2026 upgraded to [full], Vanmol2020's dB-pair figure flagged unconfirmed, PHIX datasheet version flagged)
> - Author(s) / Maintainer(s): Compiled via Perplexity research session, user-directed; incorporated into scientific-research-guide domains/ by Claude
>
> Primary source types:
> - Textbooks: (not yet incorporated — recommend Okamoto "Fundamentals of Optical Waveguides" or Snyder & Love for CMT foundations)
> - Review articles: Taras et al. 2021 (*Advances in Physics: X* — corrected 2026-08-24 from "Nanophotonics"); Weninger et al. 2026 (*Light: Sci. Appl.*)
> - Methods / standards papers: Johnson et al. 2002 (*Phys. Rev. E*); Sethi et al. 2018 (*Optics Letters*); Vanmol et al. 2020 (*J. Lightwave Technol.* — corrected 2026-08-24 from "VUB")
> - Experimental / device demonstration: Zhang et al. 2025 (*Photonics*, MDPI) — a primary 1 W SSC design paper, not a comparison table (re-categorised 2026-08-26: the front matter still bundled it under "Other/datasheets", the same mischaracterisation the 2026-08-24 Node 7b backfill corrected inside the ledger); Weninger et al. 2025 (*J. Phys. Photonics*) — the GRIN coupler paper, cited in N2/N4/N5/N6 but previously missing from this list entirely
> - Other (e.g. datasheets, industry standards): PHIX SSC product datasheet (recorded as v1.0 2026-03 — see the Node 7b PHIX2026 row for an unresolved v1.1 version flag)
>
> Notes for AI use:
> - Intended use: Technical reference for cross-checking claims about taper physics, SSC (spot-size converter) architectures, and packaging alignment-tolerance trade-offs in follow-up conversations — including questions that also touch groove-based fiber fixturing (see Cross-Domain Links to `v_groove_fabrication.md`).
> - Validation status / usage note: First-round collection, with a targeted second-source cross-verification pass run 2026-08-24 via `literature-search-extract` on the four most load-bearing numeric claims (Section 5's GRIN alignment tolerance, SiN propagation loss, packaging cost share; Section 4's Sethi et al. taper numbers) — all four were corroborated by an independent source (see inline notes at each). One citation error was caught and fixed in that pass: the Sethi et al. taper paper (Node 7) is published in **Optics Letters**, not Optics Express as originally recorded. A follow-up spot-check (same date) additionally corroborated the Node 1 MFD-vs-density trade-off claim. A third pass (2026-08-24, user-supplied re-sourcing, spot-checked by this AI against the primary source) resolved the Node 6 "±0.5 µm / zero self-alignment" quote: it traces cleanly to Weninger et al. 2026 (already in Node 7), but the profile's original wording had conflated two distinct measurements from the same source sentence — a 1-dB optical vertical-misalignment tolerance and a separate mechanical solder-self-alignment failure threshold, both coincidentally ±0.5 µm. Both are now correctly split and cited (see Node 6). Numeric claims *not* covered by any pass (MFD ranges, coupling-loss ranges, other Section 6 pitfall specifics) remain single-source and provisional — do not assume the whole profile is now cross-verified. **Fourth pass, 2026-08-24 (schema backfill).** This profile predated the Node 7b Source Ledger requirement (`domain-expansion-guide.md` §3.2) and was brought onto the current schema: every Nodes 1–6 claim now carries a `[Key]` resolving to Node 7b, Node 4 was converted from prose-per-method to a table (§3.3), and Node 5 gained the mandatory Conditions column. Resolving the anchors against publisher metadata for the first time surfaced **three further venue/attribution defects** — Taras et al. is *Advances in Physics: X* not Nanophotonics; Vanmol et al. is *J. Lightwave Technol.* not "VUB"; Zhang et al. is a primary 1 W SSC design paper, not the "consolidated comparison table" this profile described — all recorded in Node 7b's backfill-corrections block. That the DOI beside the wrong Taras journal name was *correct* is why two earlier verification passes did not catch it: a self-consistent-looking cell is not a checked cell.

---

## 1. Theoretical Framework Anchoring

### Core first principles

| Scale / problem type | Foundational theory | Core physical quantity |
|------------|---------|-----------|
| Two coupled waveguides / taper cross-section evolution | Coupled Mode Theory (CMT, 耦合模態理論) | Propagation constants β1, β2; coupling coefficient κ; mixing angle θ = arctan(κ/Δ) |
| Arbitrary-geometry slow taper (incl. photonic crystal) | Adiabatic theorem for guided waves (Johnson et al. 2002) | Local guided mode existence at every z; requires mode to remain "propagating (nonevanescent) and guided at every point in the taper" |
| Full-field verification of taper geometry | Numerical solvers: FEM (COMSOL), FDTD (Lumerical/Tidy3D), EME, FDM | Transmission / coupling efficiency η, mode overlap integral |
| Fiber–chip mode-field matching | Overlap integral formalism | η = [4β1β2/(β1+β2)²]·[(∫E2E1*rdrdφ)²/(∫E1E1* rdrdφ ∫E2E2* rdrdφ)] |

### Inviolable physical constraints (the AI should warn the user here)

1. **Guided-mode continuity requirement**: "adiabatic transmission can only occur... if the operating mode is propagating (nonevanescent) and guided at every point in the taper" (Johnson et al. 2002). If any cross-section along the taper drops the mode into a radiative/evanescent regime with no guided solution, the adiabatic theorem does not apply, regardless of how slowly the geometry varies.
2. **Adiabaticity is governed by dθ/dz relative to Γ=√(Δ²+κ²), not by dW/dz alone**: the rigorous criterion is η ≡ (1/2Γ)(dθ/dz) ≪ 1 (Taras et al. 2021). A slow geometric taper does not automatically guarantee a small η if Δ (propagation-constant mismatch) is itself small near mode-crossing points.
3. **MFD (mode field diameter) vs. density trade-off is fundamental, not a design oversight**: "This tradeoff—the desire for larger MFDs to increase alignment tolerance... while simultaneously requiring smaller MFDs to increase connection and device density—is one of the most critical ones within photonic packaging." Any claim of a coupler that defeats this trade-off without cost (footprint, bandwidth, or process complexity) should be scrutinized. (Substantively corroborated 2026-08-24: independent packaging literature reports the same relationship quantitatively — e.g. intentionally enlarging beam diameter can widen lateral assembly tolerance from ~±2 µm to ±10–35 µm or more, at the cost of channel density. The quoted sentence itself was not found verbatim outside this profile's own cited Weninger et al. review, so treat the exact wording as attributed to that source, not independently re-verified word-for-word.)

> **Decision point (mandatory Tier 0 confirmation)**: when the user describes a taper design or coupling scheme,
> the AI must confirm:
> "Is your goal (A) analyzing physical adiabaticity/mode evolution correctness, (B) comparing packaging/alignment-tolerance trade-offs for a specific platform, or (C) evaluating a specific commercial product's specs against literature benchmarks?"
> The three goals correspond to entirely different analysis paths: (A) needs CMT/adiabatic-theorem-level rigor; (B) needs packaging-cost and yield literature; (C) needs datasheet vs. peer-reviewed benchmark cross-checking.

---

## 2. Measurement Tool Inventory

### Mode-field and coupling-loss characterization

| Measurement target | Tool | Output information | Applicable conditions | Common misuse | Source [Key] |
|---------|------|---------|---------|---------|---------|
| Coupling loss (TE/TM) | Laser + EDFA + polarization controller + photodetector, manual x/y/z fiber scan for max power | Per-facet coupling loss (dB) | Requires active alignment scan to locate peak transmission | Reporting loss without specifying whether TE or TM, or without de-embedding grating coupler loss | — (general technique knowledge) |
| High-power damage/loss behavior | Same setup + inline attenuator before photodetector | Coupling loss at elevated input power (e.g. 1 W) | Used to check thermal/nonlinear degradation at high power | Extrapolating low-power loss data to high-power regime without dedicated test | Zhang2025 |
| Spectral response / bandwidth | SLED (super-luminescent LED) + OSA (optical spectrum analyzer) | Insertion loss vs. wavelength curve | Needs broadband source; polarization wheels for TE/TM separation | Not isolating taper loss from grating coupler loss (requires patch-waveguide de-embedding) | — (general technique knowledge) |
| Isolated taper-only loss | Patch waveguide reference structure subtraction | Loss per taper transition (dB) | Only valid when patch and DUT share identical grating couplers | Assuming taper loss = total insertion loss without subtracting fixed coupler loss | Sethi2018 |

### Alignment tolerance and packaging metrics

| Measurement target | Tool | Output information | Applicable conditions | Common misuse | Source [Key] |
|---------|------|---------|---------|---------|---------|
| 1-dB / 3-dB lateral & vertical alignment tolerance | 3D-FDTD misalignment sweep (simulation) or physical micro-positioning stage (experiment) | Tolerance window (µm) for ≤1dB or ≤3dB excess loss | Must specify sweep direction (lateral/vertical/longitudinal) separately — tolerances are often asymmetric | Quoting a single "alignment tolerance" number without specifying axis or dB threshold | Weninger2025 |
| Active alignment throughput/yield | Loopback waveguide + real-time power monitoring during UV-epoxy cure | Bond position stability, cure-induced drift | Standard for high-Δn edge couplers with narrow tolerance | Ignoring epoxy shrinkage/expansion during cure as a yield-loss mechanism | Weninger2026 |

---

## 3. Standard Modeling Toolchain

```
Coupled Mode Theory (CMT) — analytical
→ Output: adiabaticity criterion η, crosstalk μ(ℓ) asymptotic scaling
    ↓
Mode solvers: EME (Eigenmode Expansion) / FDM (Finite Difference Method)
→ Input: waveguide cross-section geometry, refractive indices
→ Output: local mode profiles, effective index vs. z, taper length optimization
    ↓
Full-field solvers: FDTD (Lumerical, Tidy3D) / FEM (COMSOL)
→ Output: transmission spectra, alignment-tolerance sweeps, polarization-dependent loss, fabrication-tolerance Monte Carlo
    ↓
Experimental characterization: SLED+OSA or tunable laser + power meter, active-alignment rigs
→ Output: measured coupling loss, bandwidth, high-power reliability data
```

---

## 4. Domain-Specific Fitting Methods

> **Converted from prose-per-method to a table 2026-08-24**, per `domain-expansion-guide.md` §3.3
> (one row = one self-contained, greppable, citable fact). The Sethi taper-profile formula does not
> fit a table cell and is kept below the table as a formula note.

| Method | Applicable question | Applicable conditions | Common error | Correct approach | Source [Key] |
|---|---|---|---|---|---|
| Nonlinear (MMI-based) compact taper profile | Can I shorten this taper without paying the usual efficiency price? | Compact mode-size transitions where footprint reduction is prioritized over strict adiabaticity; relies on multi-mode interference (MMI) re-imaging rather than adiabatic mode evolution | ⚠️ Assuming any taper labeled "compact" or "short" must be non-adiabatic and therefore lossy. The 19.5 µm compact taper achieved 95% coupling efficiency vs. the 50 µm standard linear adiabatic taper it was compared against — but via a *different mechanism* (MMI), not by "cheating" adiabaticity (cross-verified 2026-08-24 directly against the paper: 95% efficiency at 19.5 µm, footprint reduced 50.8%, measured insertion loss <0.1 dB/transition, SiN photonic wire) | Explicitly distinguish "adiabatic mode evolution" designs from "MMI re-imaging" designs when comparing taper length vs. loss — they are not interchangeable design philosophies even when performance is comparable | Sethi2018 |
| GRIN (graded-index) coupler design | Which coupler class fits my physical integration geometry? | Chip-to-chip or fiber-to-chip coupling requiring a large vertical gap (>10 µm) for co-integration with electrical bumps, while keeping wafer-scale parallel processing (PECVD + i-line lithography, no TPP) | ⚠️ Assuming vertical/GRIN couplers and edge/inverse-taper couplers are interchangeable; GRIN couplers solve a fundamentally different geometry problem (out-of-plane chip-to-chip stacking across a gap) from in-plane fiber-to-waveguide edge coupling | Match coupler class to the physical integration geometry (in-plane edge vs. out-of-plane vertical) *before* comparing loss/tolerance numbers | Weninger2025 |
| Overlap-integral coupling-efficiency estimate | How much of this mode actually couples into the mating mode? | Both mode fields known (measured or simulated) at the same reference plane; scalar/weakly-guiding approximation acceptable | ⚠️ Computing overlap on mode *intensity* profiles instead of complex fields, which silently discards the phase-front mismatch that dominates at a gap or a tilted facet — a mode solver outputs the complex field itself (e.g. normalized so max `\|E\|²`=1), while any camera/profiler-based measurement only ever returns intensity `I=\|E\|²/2η`, never phase | Use the field overlap integral of Node 1 with matched reference planes; validate against a full-field (FDTD/EME) result before trusting it as a design number. If one side's field is only known from a beam-profiler/camera measurement, its phase-front curvature is unknown — treat the resulting overlap number as an upper bound, not an as-built prediction | WikipediaGaussianBeam2026, RPPhotonicsModeSolvers2026, AnsysFDE2026, RPPhotonicsBeamProfilers2026 |

**Sethi taper-profile formula** (does not fit a table cell): X = a(bz² + (1−b)z) + (1−a)·sin(cπz²/2),
with 0 ≤ a ≤ 1, −c/(c−2) ≤ b ≤ c/(c−2), c any odd integer ≥ 3; boundary conditions X(z=0)=0,
X(z=1)=1 [Sethi2018].

---

## 5. Domain-Specific Quality Metrics

> **Conditions column added 2026-08-24** per `domain-expansion-guide.md` §3.2/§3.3 — a number
> whose material platform, wavelength band, gap and dB threshold live only in prose is the exact
> shape of the citation-fidelity defect this SKILL has now hit four times.

| Metric | Abbreviation | Physical meaning | Typical value range | Conditions (platform/wavelength/geometry/threshold) | Source [Key] |
|------|------|---------|------------|------|------|
| Mode field diameter | MFD | Spatial extent of guided/free-space mode; governs overlap integral with mating mode | Fiber: ~10.4 µm (SMF-28); SiN waveguide: 1.5–3 µm; PIC wire waveguide: ~0.8–1.4 µm | Telecom band, single-mode; SMF-28 figure is the vendor nominal at 1550 nm. The SiN and wire-waveguide ranges are cross-design summaries, not one measured device — single-source and provisional. None of these rows states which width convention (1/e² intensity radius, FWHM, D4σ, or Petermann-II far-field transform) produced the figure — see N6's MFD-convention pitfall before comparing two MFD numbers as if commensurable | Zhang2025, PHIX2026 |
| Coupling loss | CL | Power loss at a single interface (dB), 10·log₁₀(1/η) | 0.25–1.5 dB depending on design | Per facet, telecom band; must state TE or TM and whether grating-coupler loss was de-embedded. Range spans several coupler classes — not comparable across classes without the geometry | Weninger2026, Sethi2018 |
| 1-dB alignment tolerance | — | Misalignment (µm) causing 1 dB excess loss, per axis | Edge/inverse taper: ±0.5–0.7 µm; GRIN: ±2.24–2.88 µm; expanded-beam micro-lens: up to ±0.8 µm baseline × ~35 | Per axis and per dB threshold — tolerances are asymmetric between lateral/vertical/longitudinal. GRIN figures: the source reports ≈±2.24 µm lateral / ≈2.38 µm vertical at an **11 µm gap**; the 2.88 µm upper bound was not independently re-derived and likely reflects a different gap/config point in that paper's full tolerance table (cross-verified 2026-08-24) | Weninger2025, Weninger2026 |
| Adiabaticity parameter | η | (1/2Γ)(dθ/dz), Γ=√(Δ²+κ²); ≪1 required for adiabatic transfer | Design-dependent; smaller η ⇒ longer device but lower crosstalk | Two-mode CMT framing; valid where the two-mode reduction holds. Not a measurable quantity — a design-time criterion | Taras2021 |
| Propagation loss | — | Material/waveguide loss per unit length | SiN SSC: 0.1 dB/cm | SiN platform, telecom band, vendor spec for an SSC interposer. Cross-verified 2026-08-24 against LioniX TriPleX SiN literature, which independently reports 0.1 dB/cm as achievable — down to sub-0.01 dB/cm in ultra-low-confinement platforms and ~0.4 dB/cm in other designs, so 0.1 dB/cm sits inside a corroborated, **platform-dependent** range rather than being a vendor-only figure | PHIX2026 |
| Packaging cost share | — | Fraction of total PIC manufacturing cost attributable to packaging/assembly/test | 70–80% | Industry-wide estimate for PIC manufacturing, not a per-product measurement; cross-verified 2026-08-24 against independent industry sources beyond the review (EPIC Photonics, PhotonDelta both cite "70–80% of total PIC manufacturing cost" / "up to 80% of unit cost"), so it is not a single-paper artifact — but it remains an estimate, not a measured figure | Weninger2026 |

---

## 6. Common Assumption Pitfalls

| Pitfall | Trigger condition | How to recognize it | Correct approach | Source [Key] |
|------|---------|---------|---------|---------|
| "Adiabatic = slow geometric taper, full stop" | User equates taper length directly with adiabaticity | No mention of local mode structure, Δn, or mode-crossing avoidance | Check whether the guided mode remains propagating and guided at every z; verify η≪1 via CMT, not just "the taper is long" | Johnson2002, Taras2021 |
| "Short taper must sacrifice efficiency" | User assumes taper length and coupling efficiency are monotonically linked | Comparing only taper length without checking underlying mechanism (adiabatic evolution vs. MMI re-imaging) | Distinguish adiabatic tapers from MMI-based compact tapers (Sethi et al.) | Sethi2018 |
| "Larger Δn always worse for alignment tolerance" | User assumes SOI (high Δn) is strictly worse than SiN (mid Δn) for packaging | Ignoring that inverse tapers and edge couplers on high-Δn platforms can still achieve low CL (0.25 dB) if tip geometry is optimized | Separate the "material platform Δn" variable from the "specific coupler geometry" variable — both affect MFD/tolerance independently | Weninger2026 |
| "Solder self-alignment degrades gracefully with misalignment" | User assumes passive self-alignment behaves like a continuous tolerance curve | Not accounting for reported threshold behavior | Note the documented case: measured solder self-alignment data showed a ±0.5 µm deviation between die and interposer "could cause zero self-alignment to occur" (Weninger et al. 2026, already in Node 7) — i.e., a non-linear, near-binary failure mode near the tolerance edge. **Citation resolved 2026-08-24**: the original quote in this profile had conflated this mechanical solder-self-alignment figure with a *separate* optical measurement from the same sentence in the source (see the new pitfall row below) | Weninger2026 |
| Conflating "1-dB optical vertical-misalignment tolerance" with "solder self-alignment failure threshold" | User cites "±0.5 µm" for a taper/SSC design without specifying which of two distinct measurements they mean | Both numbers happen to be ±0.5 µm and appear in the same source sentence, inviting a false equivalence | Weninger et al. 2026 reports them as two separate findings in one sentence: (1) "coupler simulations showed a 1-dB vertical misalignment tolerance of only ±0.5 μm" — an *optical* simulation result for the coupler itself; (2) "measured solder self-alignment data showed that a deviation of ±0.5 μm between the die and interposer could cause zero self-alignment to occur" — a *mechanical* assembly-yield result for solder-based self-alignment. They coincide numerically but describe different physical mechanisms (guided-mode coupling loss vs. solder-surface-tension capture range) on different sample sets; do not present one as evidence for the other, and do not treat ±0.5 µm as a universal adiabatic-taper tolerance constant (added 2026-08-24) | Weninger2026 |
| "Down-taper (fiber-side) and inverse-taper (chip-side) are the same structure" | User conflates fiber-tip tapers with chip-edge inverse tapers | Both are described generically as "taper" without specifying which physical object carries the structure | Down-tapers are fabricated ON the fiber tip (e.g., via 2PP/two-photon polymerization); inverse tapers are fabricated ON the PIC edge via lithography — confirm which substrate carries the taper before comparing yield/tolerance | Vanmol2020 |
| "Wafer-scale and TPP (two-photon polymerization) processes are equally scalable" | User assumes any taper/lens structure scales to high volume equally | Not distinguishing serial vs. parallel fabrication | TPP-based down-tapers/free-form couplers are fabricated serially (one device at a time); GRIN/SiN SSC/inverse tapers via PECVD+lithography are wafer-scale parallel processes | Weninger2025, Vanmol2020 |
| A quoted MFD, or any camera/beam-profiler "spot size," is treated as a direct measurement of the complex mode field | User says the spatial field distribution "can only be obtained by measurement," cites a beam-profiler/camera spot size and feeds it into a mode-overlap or coupling-efficiency argument as if it carried phase, or compares two MFD numbers from different sources (e.g. a fiber datasheet vs. a simulated waveguide mode) without checking which width convention each used | A bare MFD/beam-width number with no stated convention; an argument that treats "we measured the beam" as equivalent to "we know the complex field" | A beam profiler or camera outputs only intensity I=\|E\|²/2η — never phase. A reported beam width is a *derived* number under one of several non-interchangeable conventions (1/e² intensity radius, FWHM, or the ISO D4σ second-moment definition), and for fiber MFD specifically the standard route (TIA-EIA-455-191) transforms a measured *far-field intensity* distribution through the Petermann II integral under an assumed Gaussian-like mode — it is not a direct field readout. Two MFD figures are comparable only when both used the same convention, and any Petermann-II-derived MFD carries unflagged systematic error if the real mode has significant non-Gaussian content (higher-order admixture, aberrated wavefront) | OphirMFD2026, NewportGaussianOptics2026, OphirBeamSize2026 |

---

## 7a. Literature Anchors

> Curated reading list. The citation *registry* — the resolution key for every `[Key]` used in
> Nodes 1–6 — is Node 7b below.

| Type | Reference | Why it matters |
|------|------|-------|
| Foundational theorem | Johnson et al., "Adiabatic theorem and continuous coupled-mode theory for efficient taper transitions in photonic crystals," *Phys. Rev. E* 66, 066608 (2002) | Establishes the rigorous guided-mode existence condition for adiabaticity in arbitrary (incl. strongly-grated) geometries |
| Review / theory | Taras et al., "Shortcuts to adiabaticity in waveguide couplers – theory and implementation," *Advances in Physics: X* 6(1), 1894978 (2021) | Full CMT derivation of adiabaticity criterion η and crosstalk asymptotic scaling μ∝ℓ^−2(m+1) |
| Experimental / SiN taper | Sethi, Kallega, Haldar & Selvaraja, "Compact broadband low-loss taper for coupling to a silicon nitride photonic wire," *Optics Letters* 43(14), 3433 (2018) | Demonstrates a non-adiabatic MMI-based compact taper outperforming a standard adiabatic linear taper in length |
| Experimental / high-power SSC | Zhang, Zhang, Zhang & Yang, "Silicon Nitride Spot-Size Converter with Coupling Loss < 1.5 dB for Both Polarizations at 1W Optical Input," *Photonics* 12(1), 5 (2025) | One of the few SiN SSC studies reporting 1 W high-power data for both polarizations |
| Fiber-side down-taper | Vanmol et al., "Mode-field Matching Down-Tapers on Single-Mode Optical Fibers for Edge Coupling Towards Generic Photonic Integrated Circuit Platforms," *J. Lightwave Technol.* 38(17), 4834–4842 (2020) | Defines the down-taper as a fiber-tip-printed structure, decoupled from PIC design. ⚠ **The "1.34 dB/facet vs 2.31 dB for lensed fiber" figure this row used to state outright is unconfirmed** (2026-08-26 currency pass): the accessible abstract reports "up to 1.43 dB improvement" for 4 of 5 platforms and nowhere gives that pair, and the full text was unreachable on three routes. Do not quote the pair until someone with JLT access reads the tables. `review-when:` the JLT full text becomes accessible |
| Packaging review | Weninger et al., "Advances in waveguide to waveguide couplers for 3D integrated photonic packaging," *Light: Sci. Appl.* 15(1) (2026) | Comprehensive coupler-class comparison; establishes the 70–80% packaging cost share and the MFD/density trade-off framing |
| GRIN coupler design | Weninger, Duessel, Serna, Kimerling & Agarwal, "Graded index couplers for next generation chip-to-chip and fiber-to-chip photonic packaging," *J. Phys. Photonics* 8(1), 015005 (2025) | Quantitative benchmarking of GRIN vs. edge/evanescent/grating/free-form couplers on CL, tolerance, bandwidth, footprint |
| Industry datasheet | PHIX Photonics, "PHIX Spot Size Converters" datasheet v1.0, March 2026 | Commercial SiN SSC interposer specs: MFD down to 1.5 µm, 127/250 µm pitch, 2.8–4.9 mm length, 0.1 dB/cm propagation loss |

---

## 7b. Source Ledger (added 2026-08-24 — the resolution key for every `[Key]` used in Nodes 1–6)

> Legend — **Access tag**: `[full]` full text read · `[partial]` preview/excerpt only · `[abstract]`
> abstract/metadata only · `[secondary]` known via another source citing it.
> **Verification status**: ✅ Confirmed (checked against the source or its publisher metadata
> record) · `~` Approximate (general claim corroborated; exact figure not independently
> re-derived) · ⚠ Unconfirmed · ❌ Withdrawn.
>
> **Backfill corrections (2026-08-24)** — this profile predated the Node 7b requirement
> (`domain-expansion-guide.md` §3.2) and its anchors had never been resolved against publisher
> metadata. Doing so during the backfill turned up **three venue/attribution defects**:
> 1. **Taras et al. 2021** was recorded as *Nanophotonics*. The DOI in the same cell
>    (10.1080/23746149.2021.1894978) belongs to ***Advances in Physics: X*** 6(1), 1894978 — the
>    DOI was right and the journal name was wrong, so the entry looked self-consistent enough to
>    survive two earlier verification passes.
> 2. **Vanmol et al. 2020** was recorded with venue "VUB (2020)" — an *institution*, not a venue.
>    Published in ***Journal of Lightwave Technology*** 38(17), 4834–4842.
> 3. **Zhang et al. 2025** was recorded with no title and no author list beyond "E. Zhang et al.",
>    and was described as a "consolidated comparison table" paper. It is a *primary* SSC design
>    paper — "Silicon Nitride Spot-Size Converter with Coupling Loss < 1.5 dB for Both
>    Polarizations at 1W Optical Input" — so citing it as a survey table misrepresented what it is.
>
> Also completed: **Sethi et al. 2018**'s author list was missing its fourth author
> (S. K. Selvaraja). The Optics-Letters venue correction made by an earlier pass is confirmed here
> against Crossref.

> **Verified (date)** (`domain-expansion-guide.md` §3.7): when this row's claim was last checked
> against the primary source — not the source's own publication year.
>
> **2026-08-26 currency pass** (audit trail: `reports/2026-08-26-scientific-research-guide-source-currency-pass.md`).
> All eight rows were re-resolved against Crossref and/or the arXiv API; **no erratum or retraction**
> was found. All three of the 2026-08-24 backfill corrections (Taras venue, Vanmol venue, Zhang
> paper-type) were independently re-confirmed rather than re-stated, and the two load-bearing numeric
> checks were reproduced from primary text: Sethi2018's 95 % / 19.5 µm / 50.8 % figures from the
> preprint, and Weninger2026's ±0.5 µm split — the optical 1-dB tolerance and the mechanical
> solder-self-alignment threshold really are two separate sentences, so the earlier un-conflating was
> right. New this pass: two arXiv preprints gained version pins, Weninger2026 was upgraded to `[full]`
> via its open PMC copy, and **Vanmol2020's "1.34 dB/facet vs 2.31 dB" figure could not be found** in
> any accessible text — it is now flagged rather than left standing unqualified.
>
> **2026-08-30 packet intake (seventh Node-7b addition, sixth profile pass)** — a user-supplied
> explanatory Q&A packet on field-vs-intensity and MFD measurement convention was resolved per
> `domain-expansion-guide.md` §9 step 2 before any claim entered Nodes 4/6: all seven anchors were
> fetched directly and their quoted sentences confirmed verbatim, except `rp-photonics.com`'s two
> pages and the Ansys FDE-solver page, which returned HTTP 403 on direct fetch — those three quotes
> were instead corroborated via a web-search cache snippet reproducing the same sentence, so they are
> tagged `[secondary]` / `~` Approximate rather than `[full]` / ✅ Confirmed. No erratum/retraction
> applicable (none of the seven is a peer-reviewed article).

| Key | Full citation | Identifier | Access tag | Verification status | Verified (date) | Locator | Used in (Node/row) |
|---|---|---|---|---|---|---|---|
| Johnson2002 | S. G. Johnson, P. Bienstman, M. A. Skorobogatiy, M. Ibanescu, E. Lidorikis & J. D. Joannopoulos, "Adiabatic theorem and continuous coupled-mode theory for efficient taper transitions in photonic crystals," *Phys. Rev. E* 66(6), 066608 (2002) | DOI: 10.1103/PhysRevE.66.066608 | [abstract] | ✅ Confirmed (full author list and article number verified 2026-08-24) | 2026-08-26 — identity re-resolved against Crossref; no erratum/retraction signal | Guided-mode existence condition for adiabaticity | N1 principles table + constraint 1; N6 row 1; N7a |
| Taras2021 | A. K. Taras, A. Tuniz, M. A. Bajwa, V. Ng, J. M. Dawes, C. G. Poulton & C. M. de Sterke, "Shortcuts to adiabaticity in waveguide couplers – theory and implementation," ***Advances in Physics: X*** 6(1), 1894978 (2021) | DOI: 10.1080/23746149.2021.1894978 | [abstract] | ✅ Confirmed — **venue corrected 2026-08-24** from the previously recorded "Nanophotonics"; the correction was **independently re-confirmed** against Crossref 2026-08-26, not merely re-stated | 2026-08-26 — identity re-resolved against Crossref; no erratum/retraction signal | CMT derivation of η and crosstalk scaling | N1 constraint 2; N5 adiabaticity row; N6 row 1; N7a |
| Sethi2018 | P. Sethi, R. Kallega, A. Haldar & S. K. Selvaraja, "Compact broadband low-loss taper for coupling to a silicon nitride photonic wire," *Optics Letters* 43(14), 3433 (2018); preprint arXiv:1711.09831v1 (sole existing version, posted 2017-11-27) | DOI: 10.1364/OL.43.003433 | [full] | ✅ Confirmed (95% efficiency at 19.5 µm vs. a 50 µm linear taper, 50.8% footprint reduction, <0.1 dB/transition — cross-verified against the paper 2026-08-24; author list completed same date) | 2026-08-26 — identity re-resolved against Crossref + the arXiv API, version pinned to v1 (only version extant); the Node 4 numbers were **independently reproduced** from the preprint abstract this pass; no erratum/retraction signal | Results: taper profile, efficiency and footprint comparison | N2 taper-only-loss row; N4 row 1 + formula note; N5 CL row; N6 row 2; N7a |
| Zhang2025 | E. Zhang, Y. Zhang, L. Zhang & X. Yang, "Silicon Nitride Spot-Size Converter with Coupling Loss < 1.5 dB for Both Polarizations at 1W Optical Input," *Photonics* 12(1), 5 (2025) | DOI: 10.3390/photonics12010005 | [abstract] | ✅ Confirmed — **title, full author list and paper type corrected 2026-08-24** (Crossref issue date is 2024-12 for the January 2025 issue) | 2026-08-26 — identity re-resolved against Crossref; full-text re-access attempted and blocked (HTTP 403 on both the MDPI page and the PDF), so the access tag was **not** upgraded; no erratum/retraction signal | Abstract: 1 W input, both polarizations, CL < 1.5 dB | N2 high-power row; N5 MFD row; N7a |
| Vanmol2020 | K. Vanmol, K. Saurav, V. Panapakkam, H. Thienpont, N. Vermeulen, J. Watte & J. Van Erps, "Mode-field Matching Down-Tapers on Single-Mode Optical Fibers for Edge Coupling Towards Generic Photonic Integrated Circuit Platforms," ***J. Lightwave Technol.*** 38(17), 4834–4842 (2020) | DOI: 10.1109/JLT.2020.2997090 | [abstract] | ✅ Confirmed — **venue corrected 2026-08-24** from "VUB (2020)" (an institution, not a venue); full author list added — the venue correction was **independently re-confirmed** against Crossref 2026-08-26. ⚠ New this pass: the "1.34 dB/facet vs 2.31 dB lensed fiber" figure is **unconfirmed** — the accessible abstract instead states "measured improvement in coupling efficiency up to 1.43 dB" for 4 of 5 platforms, and the full text was unreachable (VUB repository blocked, ResearchGate 403). The figure is neither confirmed nor refuted; it is flagged wherever it appears rather than deleted. `review-when:` the JLT full text becomes accessible | 2026-08-26 — identity (authors/venue/pages) re-resolved; the dB-figure claim is flagged unresolved, not re-derived | Down-taper definition; ⚠ the dB-pair figure — see Verification status | N6 rows 6–7; N7a |
| Weninger2026 | D. Weninger, S. Serna, L. Ranno, L. Kimerling & A. Agarwal, "Advances in waveguide to waveguide couplers for 3D integrated photonic packaging," *Light: Sci. Appl.* 15(1) (2026) | DOI: 10.1038/s41377-025-02048-w | [full] — **upgraded from [partial] 2026-08-26** (open text read via PMC12756286) | ✅ Confirmed (citation verified 2026-08-24; the two ±0.5 µm figures were split and re-attributed in an earlier same-day pass — see N6 rows 4–5). The full text was **re-read verbatim** 2026-08-26 and reproduces both ±0.5 µm sentences, the 70–80 % cost-share sentence and the MFD-vs-density trade-off sentence, so the earlier un-conflating is confirmed correct. The 70–80 % cost share stays `~` Approximate: corroborated by independent industry sources, but it is an industry estimate, not a measurement | 2026-08-26 — Crossref + Crossmark ("document is current", no retraction) + full open text via PMC | Coupler-class comparison; the sentence carrying both ±0.5 µm figures | N1 constraint 3; N2 active-alignment row; N5 CL, tolerance and cost-share rows; N6 rows 3–5; N7a |
| Weninger2025 | D. Weninger, C. Duessel, S. Serna, L. Kimerling & A. Agarwal, "Graded index couplers for next generation chip-to-chip and fiber-to-chip photonic packaging," *J. Phys. Photonics* 8(1), 015005 (2025); preprint arXiv:2503.00121v1 (sole existing version, posted 2025-02-28) | DOI: 10.1088/2515-7647/ae1648 | [partial] | ✅ Confirmed (peer-reviewed venue, volume and article number resolved 2026-08-24, superseding the arXiv-only record). The ±2.24 µm lateral / 2.38 µm vertical 1-dB tolerance at an 11 µm gap is ✅; independently reproduced from the preprint abstract this pass; the 2.88 µm upper bound in N5 remains ⚠ Unconfirmed — not re-derived from the paper's full tolerance table. ⚠ Open reconciliation (2026-08-26 supersession scan): a same-group paper — Weninger, Serna, Ranno, Kimerling & Agarwal, *Adv. Eng. Mater.* 27(4) (2024), DOI 10.1002/adem.202402095 — reports a **tighter ±1.60 µm** lateral 1-dB tolerance. Whether that is the same coupler class as the ±2.24 µm figure cited here was **not** determined (abstracts only), so nothing was changed or added; someone comparing the two full texts should rule on it before the ±2.24 µm number is presented as *the* GRIN benchmark | 2026-08-26 — identity re-resolved against Crossref + the arXiv API, version pinned to v1; no erratum/retraction signal | Tolerance table; GRIN vs. other coupler-class benchmark | N2 tolerance row; N4 row 2; N5 tolerance row; N6 row 7; N7a |
| PHIX2026 | PHIX Photonics Assembly, "PHIX Spot Size Converters" product datasheet v1.0, March 2026 | Vendor datasheet (no DOI) | [partial] | ⚠ Unconfirmed as an independent source — a vendor datasheet, not peer-reviewed. Its 0.1 dB/cm SiN figure was separately corroborated against LioniX TriPleX platform literature (see N5 Conditions), so the *number* is `~` Approximate even though the *document* is unverified. This pass re-fetched the document and reconfirmed all four cited numbers (MFD to 1.5 µm, 127/250 µm pitch, 2.8–4.9 mm length, 0.1 dB/cm). ⚠ **§3.7 version flag:** a text extraction of the live PDF returned "Version 1.1, August 2026", inconsistent with the v1.0 / March 2026 recorded here — **not confirmed** (the direct binary fetch failed; this came from one third-party extraction only). `review-when:` someone opens the vendor PDF directly and reads its version footer — if it is v1.1, every number above must be re-checked against that issue | 2026-08-26 — numbers re-checked against the vendor document; the version/date field re-check was inconclusive | Product spec sheet | N5 MFD and propagation-loss rows; N7a |
| WikipediaGaussianBeam2026 | Wikipedia, "Gaussian beam" article, revision consulted 2026-08-30 | https://en.wikipedia.org/wiki/Gaussian_beam | [full] | ✅ Confirmed — quote "the corresponding intensity (or irradiance) distribution is given by I(r,z)=\|E(r,z)\|²/2η" fetched and read directly 2026-08-30. A live wiki page, not a fixed edition — treat as background-physics confirmation of the standard I=\|E\|²/2η relation, not as an authoritative citation for a novel or contested claim | 2026-08-30 — fetched directly | Field-vs-intensity relation for a Gaussian beam | N4 overlap-integral row |
| OphirMFD2026 | Ophir Optronics, "Measurement of Mode-Field Diameters" (technical note), consulted 2026-08-30 | https://www.ophiropt.com/en/n/measurement-of-mode-field-diameters | [full] | ✅ Confirmed — both quotes fetched and read directly 2026-08-30: "the MFD represents a measure of the transverse extent of the electromagnetic field intensity of the mode in a fiber cross-section," and "as outlined in TIA-EIA Standard 191, once the far-field intensity distribution is obtained, the MFD is generated from the Petermann II integral." This profile has not independently read TIA-EIA-455-191 itself — the standard's existence and role are cited as Ophir reports them, not re-derived from the standard's own text | 2026-08-30 — fetched directly; `review-when:` someone reads TIA-EIA-455-191 directly, upgrading this from a secondary report of the standard | Petermann-II / far-field-intensity derivation of fiber MFD | N5 MFD row Conditions; N6 new MFD-convention row |
| NewportGaussianOptics2026 | Newport (MKS Instruments), "Gaussian Beam Optics" technical note, consulted 2026-08-30 | https://www.newport.com/n/gaussian-beam-optics | [full] | ✅ Confirmed — quote "the parameter ω0, usually called the Gaussian beam radius, is the radius at which the intensity has decreased to 1/e² or 0.135 of its axial, or peak value" fetched and read directly 2026-08-30 | 2026-08-30 — fetched directly | 1/e² intensity-radius convention for Gaussian beam width | N6 new MFD-convention row |
| OphirBeamSize2026 | Ophir Photonics, "How Do You Calculate Laser Beam Size?" (blog/technical note), consulted 2026-08-30 | https://www.ophiropt.com/blog/calculate-laser-beam-size/ | [full] | ✅ Confirmed — fetched and read directly 2026-08-30; quotes on the 1/e² method ("~86% of the laser power is contained within the 1/e² width"), FWHM ("the diameter between the two points at which the intensity is half the peak"), and D4σ ("distance between the 4σ values... the ISO standard method for maximum accuracy") all confirmed on-page | 2026-08-30 — fetched directly | Non-interchangeability of 1/e², FWHM and D4σ beam-width conventions | N6 new MFD-convention row |
| RPPhotonicsBeamProfilers2026 | RP Photonics Encyclopedia, "Beam Profilers" article, consulted 2026-08-30 | https://www.rp-photonics.com/beam_profilers.html | [secondary] — direct fetch returned HTTP 403; quote corroborated via a web-search cache snippet reproducing the sentence verbatim, not by reading the live page | `~` Approximate (search-cache corroboration, not a direct page read) | 2026-08-30 — corroborated via search cache only; `review-when:` a direct fetch of the page succeeds, upgrading to [full]/✅ | A beam profiler measures the optical *intensity* profile, not the field | N4 overlap-integral row |
| RPPhotonicsModeSolvers2026 | RP Photonics Encyclopedia, "Mode Solvers" article, consulted 2026-08-30 | https://www.rp-photonics.com/mode_solvers.html | [secondary] — direct fetch returned HTTP 403; quote corroborated via a web-search cache snippet, not by reading the live page | `~` Approximate (search-cache corroboration, not a direct page read) | 2026-08-30 — corroborated via search cache only; `review-when:` a direct fetch of the page succeeds, upgrading to [full]/✅ | A mode solver computes the electromagnetic field distribution directly, not just intensity | N4 overlap-integral row |
| AnsysFDE2026 | Ansys Optics, "MODE - Finite Difference Eigenmode (FDE) solver introduction," consulted 2026-08-30 | https://optics.ansys.com/hc/en-us/articles/360034917233-MODE-Finite-Difference-Eigenmode-FDE-solver-introduction | [secondary] — direct fetch returned HTTP 403; the field-normalization statement ("the maximum electric field intensity \|E\|² is 1") was corroborated via a web-search cache snippet, not by reading the live page | `~` Approximate (search-cache corroboration, not a direct page read) | 2026-08-30 — corroborated via search cache only; `review-when:` a direct fetch of the page succeeds, upgrading to [full]/✅ | Mode solvers normalize and output the complex field, not a measured intensity image | N4 overlap-integral row |

---

## Cross-Domain Links

### Closest Related Domain Profiles

| Profile name | Overlap dimensions | Typical use split |
|------|------|-------|
| `silicon_photonics_device_physics.md` (Silicon Photonics Device Physics) | first principles (CMT, mode solvers), measurement tools (FDTD/FEM), application targets (CPO link budget) | Use taper profile for coupling/packaging-specific questions; use device-physics profile for modulator/detector/laser active-device questions. The two meet at the link budget: this profile owns the L_fiber/chip term, the device-physics profile owns P_laser, L_mod and P_sens — do not credit the same recovered margin to both (added 2026-08-24 when that profile was authored) |
| `siph_packaging_reliability.md` (Silicon Photonics Packaging & Reliability, 矽光子封裝與可靠度) | quality metrics (coupling loss, alignment tolerance, packaging cost share), application targets (CPO systems) | Use this taper profile for single-interface coupling-mechanism questions and **time-zero** coupling performance; use the packaging/reliability profile for system-level I/O density, thermal architecture, qualification, and **end-of-life** coupling. A larger MFD relaxes thermally induced misalignment sensitivity too — that is a reliability argument this profile does not make |
| Quantum/Cold-Atom Waveguide Coupling (未建檔) | measurement tools (evanescent coupling), first principles (mode overlap) | Use taper profile for classical dielectric waveguides; defer to atomic/quantum waveguide profile when guiding medium is a matter wave rather than a dielectric mode |
| `fiber_chip_passive_alignment.md` (Fiber-to-Chip Passive Alignment & Attachment) | quality metrics (coupling loss, 1-dB alignment tolerance), first principles (mode overlap), application targets (edge-coupled packages, FAU) | Use this taper/SSC profile for *how the mode is expanded and matched* (adiabaticity, MFD, coupling efficiency — i.e. how big the target is); use the passive-alignment profile for *how the fiber gets to that mode and stays there* (datum chain, alignment error budget, adhesive cure, thermo-mechanical drift, array worst-channel IL — i.e. where the arrow lands). This profile's 1-dB tolerance numbers are the *input* to that profile's error budget; note that its irreducible fiber terms (core-clad concentricity ≤0.5 µm) are already the same order as an inverse taper's whole budget |
| `v_groove_fabrication.md` (V-Groove Fabrication) | application targets (fiber-to-chip coupling packages, e.g. CPO transceivers) | Use this profile for *how the optical mode is matched/converted* (taper geometry, CMT adiabaticity, MFD/coupling-loss/alignment-tolerance trade-offs); use the V-groove profile for *how the fiber channel is mechanically cut and positioned* — the two are typically co-designed in the same fiber-array-unit (FAU) package but solve different physics problems (guided-mode adiabaticity vs. mechanical fixturing) |

---

## Cross-Domain Conflict Notes

| Issue / constraint | Other profile(s) involved | Potential conflict | AI confirmation question |
|------|------|-------|-------|
| MFD vs. density trade-off framing | `siph_packaging_reliability.md` (the built Photonic Packaging & CPO owner) | Taper-level analysis may recommend maximizing MFD for tolerance, while the module/system level may require minimizing pitch for I/O density — these can give opposite design guidance for the same waveguide. That profile adds a third direction: a larger MFD also relaxes *thermally induced* misalignment sensitivity, so the trade is tolerance vs. density vs. drift, not a two-way one | "Are you optimizing this taper for a single-channel low-loss target, for a high-channel-count system where pitch/density constraints dominate, or for post-stress drift in a CPO package? Those three point in different directions and only one can be the primary" |
| Adiabaticity criterion vs. practical fabrication tolerance | `silicon_photonics_device_physics.md` | A theoretically "adiabatic" design (large η margin) may still fail in practice due to sidewall roughness or lithography CD (critical dimension) variation not captured by the ideal CMT model | "Do you need the idealized adiabaticity condition (design theory) or the fabrication-tolerance-inclusive performance (as-built device)?" |
| Groove-level mechanical tolerance vs. taper-level optical tolerance | `v_groove_fabrication.md` | The taper/SSC profile's 1-dB alignment tolerance (µm-scale) assumes the fiber is already held at a known position; the V-groove profile's achievable placement precision (etch-depth/width control, not sidewall roughness) is the actual mechanical budget feeding into that tolerance — conflating "optical tolerance the coupler can absorb" with "mechanical precision the groove delivers" hides which one is the real bottleneck | "Are you asking what alignment error the taper/SSC design can tolerate, or what placement precision the V-groove process actually delivers — because the achievable mechanical precision may already exceed or fall short of the optical tolerance budget?" |
