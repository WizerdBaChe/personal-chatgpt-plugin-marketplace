---
xi: 1
what: "Fiber-to-Chip Passive Alignment & Attachment (光纖對晶片被動對準與固定) — Fiber-to-chip passive alignment and attachment: datum chain, alignment error budget, adhesive/cure perturbation, thermo-mechanical drift, array worst-channel metrics"
tags: [srg-domain, 領域框架, base]
aliases: ["passive alignment", "被動對準", "被動對位", "semi-passive alignment", "active alignment", "fiber attach", "fiber attachment", "pigtailing", "alignment error budget", "alignment tolerance budget", "core-to-mode offset", "core-clad concentricity", "光纖中心高度", "光纖高度", "seated fiber height", "fiber centre height", "wedge half-angle", "35.26°", "epoxy/adhesive fiber attach", "cure-induced drift", "worst-channel insertion loss", "channel uniformity", "photonic wire bond", "alignment-free coupler", "Telcordia GR-1221", "thermal cycling IL drift"]
date: 2026-08-26
status: live
profile_type: base
parent: "-"
---
# Domain Profile: Fiber-to-Chip Passive Alignment & Attachment (光纖對晶片被動對準與固定)

> Scope of applicability: The complete datum-transfer chain for edge-coupled (端面耦合) photonic
> packages — **mechanical datum → optical-core placement → adhesive fixation → thermo-mechanical
> drift** — for single fibers and fiber array units (FAU), on-chip grooves, interposers, and
> submounts. Covers what determines where the fiber core ends up relative to the waveguide mode
> centre, and whether it stays there for the product's life.
> Scientific nature: Guided-mode overlap theory in the Gaussian approximation, rigid-body contact
> mechanics of a cylinder in a wedge, statistical tolerance propagation, polymer cure shrinkage and
> viscoelasticity, CTE-mismatch thermo-mechanics.
> Engineering nature: Photonic packaging and assembly process design, alignment-budget engineering,
> adhesive/dispense process control, telecom qualification testing (Telcordia GR-series), yield and
> cost-per-coupled-channel analysis.
>
> **Domain boundary / cluster membership** — member of the **photonic-packaging** sibling
> cluster (four peer base profiles partitioning one assembly; split tabulated in
> `_routing.md` § Clusters, deliberately flat — no parent profile exists or should be built).
> This profile owns the *placement and fixation* problem. It does NOT own how the groove is cut
> (→ `v_groove_fabrication.md`), how the on-chip mode is expanded (→ `adiabatic_taper_ssc.md`),
> nor module-level qualification (→ `siph_packaging_reliability.md`). See Cross-Domain Links
> for the split and the conflicts between them.
>
> Profile metadata:
> - Profile ID: PHOT-FCPA-001
> - Profile version: 0.2 (first authoring + a second verification pass closing the three open items;
>   every literature anchor re-verified against a primary source — see §7b Provenance & correction log)
>   v0.3, 2026-08-26: §3.7 currency pass — 11 of 12 rows re-resolved, three missing DOIs added, three
>   arXiv versions pinned, the [Lo2003] authorship-merge error corrected, [Corning2013] left honestly
>   unverified (host still 403)
> - Last updated: 2026-08-26
> - Author(s) / Maintainer(s): User (NTU graduate researcher) supplied the source packet, compiled
>   via a Perplexity research session; restructured, language-normalized, and citation-verified into
>   `scientific-research-guide/domains/` by Claude (Opus 5)
>
> Primary source types:
> - Textbooks: (not yet incorporated — recommend Snyder & Love, *Optical Waveguide Theory*, or
>   Okamoto, *Fundamentals of Optical Waveguides*, for the overlap-integral formalism)
> - Review articles: Marchetti et al. 2019 (*Photonics Research*, coupling-strategy review)
> - Methods / standards papers: Marcuse 1977 (Gaussian splice-loss analysis); Khan et al. 2020
>   (*APL Photonics*); Lin et al. 2023 (*APL Photonics*); Kumar & Cardenas 2025 (*Optics Express*);
>   Telcordia GR-1221-CORE / GR-326-CORE (referenced via `v_groove_fabrication.md`, not re-verified here)
> - Other: Corning SMF-28® Ultra product information sheet PI-1424-AEN (fiber geometry tolerances);
>   Springer book chapter Lee & Lo 2007 (epoxy flow in V-groove passive alignment)
>
> Notes for AI use:
> - Intended use: cross-checking claims about what passive alignment can and cannot deliver, how an
>   alignment error budget is assembled, how the adhesive/cure step perturbs a nominally passive
>   alignment, and which reliability metric actually governs a multi-channel package.
> - **Validation status — read before reusing any citation from this profile.** The source packet was
>   an AI-research-tool output carrying nine footnote URLs. All nine were re-resolved against primary
>   sources over two passes (2026-08-24). Findings: **three of nine had the wrong first author** (the
>   papers are real; the attributed authors are not their authors), **two had materially wrong
>   titles**, one had its mechanism mischaracterized, one merged a trade-off pair into a false range,
>   one attributed a paper's *background description of prior practice* to the paper's own
>   demonstrated method, and **one causal mechanism was withdrawn outright** as unsourced. The packet
>   also contained a geometry error (see Node 1 constraint 2 and its Node 6 row). Every surviving claim
>   in Nodes 1–6 carries an `[Author Year]` key resolved in §7b; the per-anchor audit is in the
>   **Provenance & correction log** at the end of §7b. Do not re-import the original packet's
>   attributions.
> - **Profile version 0.2 (2026-08-24, second pass).** Resolved the three items the first pass left
>   open: [Lo2003] identity and its withdrawn buoyancy causation, [Kumar2025] title/DOI plus promotion
>   into Node 5, and [Chen1997] promotion into Node 1/6. Two new pitfall rows and three new Node 5 rows
>   came directly out of that verification — i.e. checking the citations produced content, it did not
>   just police it.
> - Optional external tool slot: if a local literature corpus or reference-manager MCP is available
>   (a Zotero MCP, `prism`, an Obsidian vault), prefer it for retrieving the full texts named in §7b.
>   Absent any such tool, this profile is fully usable from its own tables; the §7b access tags state
>   exactly how much of each source was read.

---

## Citation convention (applies to Nodes 0–6)

Every inline citation is a human-resolvable `[Author Year]` key with a matching row in the **Source
Ledger (§7b)**; every quantitative claim states its conditions (material system, method, wavelength,
temperature, fiber type) in the same breath as the number. Full rationale: `_template.md`
"Citation convention" and `domain-expansion-guide.md` §3.2. This profile is the second documented
case of the failure those rules exist to prevent — here it was author misattribution rather than
opaque index numbers, so §7b additionally records what each citation was *originally claimed to be*.

Claims marked `[synthesis]` are this profile's own derivation from cited premises, not something any
single source states — they are labeled so a reader can re-derive rather than re-cite them.

---

## 0. Terminology & Chinese glosses (added section — not part of the required seven nodes)

> Rationale for adding this node: this domain's Chinese literature is split between Taiwan and
> mainland conventions, and three terms in the source packet used mainland renderings that are wrong
> for a Taiwan-context thesis. The profile body is English (it is machine-consumed domain reasoning);
> this table is the single place where the Chinese equivalents live, so a Chinese-language deliverable
> can be produced without re-guessing terminology. Preference order: 國家教育研究院樂詞網 official
> rendering > Taiwan semiconductor/photonics industry usage > literal translation.

| English term | 中文（臺灣） | Meaning in this domain | Translation note |
|---|---|---|---|
| Passive alignment | 被動對準（業界亦稱被動對位） | Final position set by pre-defined mechanical features and controlled assembly tolerances, not by optical-feedback search | 「對準」為樂詞網對 alignment 的通行譯法；「對位」為產線口語，可用但宜統一 |
| Active alignment | 主動對準 | Position found by measuring optical power / IL and closing the loop on x, y, z, θx, θy, θz before fixing | — |
| Edge coupling / butt coupling | 端面耦合／對接耦合 | Fiber endface faces the chip edge waveguide facet directly | — |
| Grating coupling | 光柵耦合 | Near-vertical coupling via a diffractive grating; enables wafer-level test | — |
| Fiber array unit (FAU) | 光纖陣列單元 | Multiple fibers held at fixed pitch, coupled to a multi-channel PIC in one operation | — |
| Cladding / core | 包覆層（包層）／纖芯 | The 125 µm glass cylinder the groove actually locates, vs. the ~9 µm mode-carrying centre | 勿將 cladding 譯為「披覆」（該詞指 coating 塗覆層） |
| Coating | 塗覆層 | The 242 µm polymer layer stripped before seating | 與 cladding 區分，兩者中文極易混用 |
| Core-clad concentricity error | 纖芯–包層同心度誤差 | Offset between the core centre and the cladding cylinder's geometric centre | — |
| Mechanical datum | 機械基準 | Geometric face, groove, stop, or edge used to define and transfer position | — |
| Optical datum | 光學基準 | Reference tied to the actual mode centre / waveguide centre | — |
| Anisotropic wet etching | **非等向性**濕蝕刻 | Crystal-plane-selective etch that terminates the groove on {111} | ⚠ 來源素材作「各向異性」，為中國大陸用法；臺灣官方與教科書用「非等向性」 |
| Spot-size converter (SSC) | 光斑尺寸轉換器（模斑轉換器） | On-chip structure expanding the guided mode to match the fiber | — |
| Inverse taper | 反錐形波導 | Waveguide narrowed toward the facet so the mode delocalizes and expands | — |
| Mode field diameter (MFD) | 模場直徑 | Spatial extent of the mode; governs the overlap integral | — |
| Overlap integral | 重疊積分 | The field-overlap expression giving coupling efficiency η | — |
| Insertion loss (IL) | 插入損耗 | Total power loss added by inserting the component into the path | — |
| Return loss (RL) | 回波損耗（亦譯反射損耗） | Reflected power relative to incident, at the facet/gap | 樂詞網兩種譯法並存；同一份文件內擇一即可 |
| Alignment tolerance | 對準容差 | Positional/angular deviation permitted at a stated excess-loss threshold (e.g. 1 dB) | 必須連同「軸向」與「dB 門檻」一起陳述才有意義 |
| Tolerance stack-up | 公差堆疊 | Accumulation of independent placement errors along the datum chain | — |
| Epoxy shrinkage | 環氧樹脂固化收縮 | Volumetric contraction on cure, displacing the fiber | — |
| Creep / stress relaxation | **潛變**／應力鬆弛 | Time-dependent deformation of the adhesive under sustained load | ⚠ 來源素材作「蠕變」，為中國大陸用法；臺灣機械工程官方用「潛變」 |
| Delamination | 分層剝離 | Loss of adhesion at an interface, often channel-selective in an array | — |
| Coefficient of thermal expansion (CTE) | 熱膨脹係數 | Material length change per K; mismatch drives post-cycling offset and stress | — |
| Thermal cycling / damp heat | 溫度循環／高溫高濕 | Qualification stresses (e.g. −40 to +85 °C; 85 °C/85 % RH) | — |
| Co-packaged optics (CPO) | 共封裝光學 | Optical engine co-packaged with the switch/compute ASIC; the high-channel-count driver for this domain | — |
| Link budget | 鏈路預算 | System-level power accounting that the worst channel, not the mean, must satisfy | — |

---

## 1. Theoretical Framework Anchoring

### Core first principles

| Scale/problem type | Foundational theory | Core physical quantity |
|------------|---------|-----------|
| Fiber–waveguide interface | Overlap integral of two normalized guided fields | Coupling efficiency η; coupling loss L_c = −10·log₁₀η |
| Misalignment sensitivity | Gaussian-beam mismatch analysis of splices/joints [Marcuse1977] | 1-dB tolerance per axis (lateral, vertical, longitudinal, tilt) |
| Fiber seating in a groove | Rigid-body contact of a cylinder in a symmetric wedge | Fiber-axis pose (x, y, θ) as a function of groove opening and fiber radius |
| Datum transfer through the package | Statistical tolerance propagation (worst-case sum vs. RSS) | Distribution of core-to-mode offset, not a single nominal value |
| Fixation | Polymer cure shrinkage + viscoelastic relaxation | ΔIL_cure; long-term monotonic drift |
| Post-assembly life | CTE-mismatch thermo-mechanics, moisture diffusion | ΔIL(T, ΔT, N_cycle, RH, t) |
| Multi-channel array | Per-channel link budget and extreme-value statistics | Worst-channel IL; channel-to-channel uniformity; yield |

### What "passive" precisely means

In the literature, *passive alignment* does **not** mean "no metrology" or "no precision equipment."
The operative definition is that **the final optical alignment is determined by pre-defined mechanical
features and controlled assembly tolerances rather than by optical-feedback iterative optimization.**
The distinction is real and graded: Bernabé et al. describe explicitly *"semi-passive"* strategies
using etched silicon microparts as ferrule holders, in which some axes are mechanically constrained
and others are still set with feedback [Bernabé2012]. When a user says "passive," ask which axes are
mechanically constrained and which (if any) still use feedback — the answer changes the entire error
budget.

### Alignment error budget (the profile's organizing equation)

The position of the fiber core relative to the waveguide's effective mode centre is a sum of
independent contributions, each owned by a different process step:

```
r_core→mode = r_fiber/core + r_groove + r_groove→wg + r_assembly + r_cure + r_thermal
```

| Term | Physical origin | Where it is bounded / measured | Typically owned by |
|---|---|---|---|
| `r_fiber/core` | Core-clad concentricity + cladding diameter tolerance | Fiber datasheet: 125.0 ± 0.7 µm cladding, ≤ 0.5 µm core-clad concentricity, ≤ 0.7 % non-circularity (Corning SMF-28® Ultra) [Corning2013] | Fiber vendor — **irreducible by the packaging house** |
| `r_groove` | Groove opening width, sidewall angle, bottom rounding, roughness, particles | Cross-sectional SEM, profilometry, white-light interferometry | Groove process → `v_groove_fabrication.md` |
| `r_groove→wg` | Lithographic overlay between the groove level and the waveguide level | Overlay metrology; test structures. **Reducible to zero by construction** when groove and waveguide are co-defined in the same lithography/etch step, as opposed to a separately-fabricated groove carrier bonded on later [Chen1997] | PIC fab |
| `r_assembly` | Seating force, end-stop contact, lid/clamp pressure, fixture repeatability | Pre-cure IL scan; in-situ position monitoring | Assembly process |
| `r_cure` | Adhesive flow, capillary rise, shrinkage on cure, residual stress | ΔIL measured pre- vs. post-cure (both required) | Attach process |
| `r_thermal` | CTE mismatch, moisture uptake, creep/stress relaxation, self-heating | ΔIL after each qualification stress | Materials + design |

A study that characterizes only `r_groove` ("does the groove hold the fiber?") has addressed one of
six terms. Warn the user when a proposed scope collapses to one term.

### Inviolable physical constraints (the AI should warn the user here)

1. **The mechanical datum locates the cladding cylinder; the optical mode lives at the core.** No
   improvement in groove geometry removes the core-clad concentricity error, specified as ≤ 0.5 µm on
   standard single-mode fiber (Corning SMF-28® Ultra, Dimensional Specifications) [Corning2013]. That
   is already the same order as an inverse-taper edge coupler's entire 1-dB budget (~±0.5 µm, see
   `adiabatic_taper_ssc.md` Node 5), so it must appear explicitly in any passive budget.
2. **On a self-terminated {111} groove the fiber height is set by the mask opening width, not by the
   etch depth.** With the {111} sidewall at 54.74° to the (100) surface (see `v_groove_fabrication.md`
   Node 1), the wedge half-angle from the bisector is α = 90° − 54.74° = **35.26°** and the included
   groove angle is **70.53°**. A cylinder of radius r seated on both walls has its centre at
   d = r/sin α = **1.732 r** above the apex; for r = 62.5 µm, d = 108.3 µm. Since a fully-formed groove
   of top opening W has depth D = (W/2)·tan 54.74° = 0.7071 W, the centre height above the wafer
   surface is h = 1.732 r − 0.7071 W, giving **dh/dW = −0.707 µm per µm of opening-width error**
   [synthesis, from the 54.74° {111} constraint]. A 1 µm CD/etch-bias error therefore consumes most of
   an edge coupler's vertical budget.
3. **Passive alignment cannot beat the sum of its datum-transfer errors.** With no optical feedback,
   the error budget *is* the loss distribution — there is no step later in the flow that recovers a
   term that was left uncontrolled.
4. **Mode mismatch is a floor that mechanical precision cannot lower.** Perfect seating still leaves
   the overlap-integral loss between a ~10 µm-MFD fiber mode and a sub-µm PIC mode. Reducing it
   requires a mode converter (→ `adiabatic_taper_ssc.md`), not a better groove.
5. **The adhesive is a load-bearing functional element, not a neutral fixture.** It is simultaneously a
   mechanical constraint, a stress-transfer medium, an optical medium if it sits in the gap, a moisture
   pathway or barrier, and a CTE-mismatch source. Any of the five can dominate ΔIL.

> **Decision point (mandatory Tier 0 confirmation)**: when the user describes a passive-alignment
> study, the AI must confirm:
> "Is your goal (A) reaching a target insertion loss at t = 0 (an *optical/geometry* problem — overlap,
> tolerance, datum transfer) / (B) *holding* that loss across qualification life (a *materials and
> thermo-mechanics* problem — cure, creep, CTE, moisture) / (C) minimizing total cost per coupled
> channel versus active alignment (a *yield, cycle-time, and test-economics* problem)?"
> The three goals demand different metrics, different experiments, and different sample counts; a
> design optimal for (A) is routinely the wrong choice for (B) or (C).

---

## 2. Measurement Tool Inventory

### Optical characterization of the interface

| Measurement target | Tool | Output information | Applicable conditions | Common misuse | Source [Key] |
|---------|------|---------|---------|---------|---------|
| Coupling / insertion loss per facet | Tunable laser or SLED + power meter, with a reference path or cutback structure | IL (dB) per facet after de-embedding waveguide propagation loss | Requires a de-embedding structure; polarization state must be fixed and stated | Reporting total measured loss as "coupling loss" without subtracting propagation and second-facet loss; not stating TE/TM. Khan et al. state their figures are "minimum measured values of loss per coupler **after correcting for waveguide propagation loss** in the optical path" [Khan2020, §Results] | [Khan2020] |
| Spectral IL / bandwidth | SLED or swept laser + OSA, polarization control | IL vs. λ; 1-dB and 3-dB bandwidth | Broadband source must exceed the expected bandwidth — otherwise the bandwidth is extrapolated, not measured | Quoting an extrapolated bandwidth as measured. Khan et al.'s ">250 nm" is explicitly *extrapolated*, the measured quantity being a 1-dB bandwidth >100 nm [Khan2020, §Results] | [Khan2020] |
| Return loss / facet reflectance | Optical reflectometer, OFDR, or circulator + power meter | RL (dB); reflection location | Needs enough dynamic range to separate facet reflection from connector reflections upstream | Reporting RL without stating whether the gap is air-filled or index-matched — the two differ by orders of magnitude | [synthesis] |
| Longitudinal gap length | Fabry–Pérot ripple period in the transmission spectrum | Gap length inferred from free spectral range | Requires a resolvable etalon between two partially reflecting facets | Mistaking gap-induced FP ripple for the device's own spectral response | [synthesis] |
| Alignment tolerance per axis | Piezo micro-positioning stage sweep (experiment) or 3D-FDTD misalignment sweep (simulation) | Loss-vs-offset curve; 1-dB and 3-dB tolerance window per axis | Axes must be swept independently; tolerances are asymmetric | Quoting one "alignment tolerance" number with no axis and no dB threshold (see `adiabatic_taper_ssc.md` Node 2, same trap) | [Lin2023] |

### Geometric and positional metrology of the assembled package

| Measurement target | Tool | Output information | Applicable conditions | Common misuse | Source [Key] |
|---------|------|---------|---------|---------|---------|
| As-built groove cross-section | Cross-sectional SEM, stylus/optical profilometry, white-light interferometry, confocal metrology | Real W, D, α, bottom radius | Destructive for SEM — plan sample sequence accordingly | Substituting nominal mask geometry for measured geometry in the error budget | → `v_groove_fabrication.md` Node 2 |
| Seated-fiber position in a *cured* package | X-ray micro-CT; IR transmission microscopy through the silicon | Non-destructive 3D fiber position after attach | IR route requires a silicon (IR-transparent) path; CT resolution must beat the µm-scale budget | Inferring post-cure position from pre-cure optical microscopy — the displacement of interest happens *during* cure | [synthesis] |
| Fiber-core placement error relative to groove datum | Vendor FAU specification, incoming inspection | Core placement error (~0.5 µm class) | Vendor-sourced figure; see the sibling profile's caveat | Treating a vendor typical as a guaranteed worst case | → `v_groove_fabrication.md` Node 5 |

### Assembly-process and cure monitoring

| Measurement target | Tool | Output information | Applicable conditions | Common misuse | Source [Key] |
|---------|------|---------|---------|---------|---------|
| Cure-induced drift | In-situ IL monitoring through the coupled path during UV tack and thermal cure | ΔIL_cure = IL_post − IL_pre; time-resolved | The only way to attribute drift to the cure step rather than to seating | Measuring IL only after cure, which makes `r_cure` unobservable and silently reassigns its magnitude to `r_assembly` | [synthesis] |
| Adhesive volume / placement repeatability | Calibrated dispenser with volumetric or gravimetric check; post-dispense imaging | Dispensed volume, wet footprint, meniscus position | Viscosity is temperature-dependent — log ambient conditions | Specifying an adhesive by trade name only, with no volume, **dispense architecture** (top-dispense vs. canal/reservoir side-fill — they load the fiber differently), viscosity, or cure schedule recorded | [Lo2003] |
| UV dose delivered | UV radiometer at the work plane | mJ/cm² actually received | Lamp output drifts; shadowing by the fixture is common | Recording exposure *time* instead of delivered dose. Khan et al. show the coupler's insertion loss depends on the SU8 cap profile, "adjusted by the UV exposure time, with longer exposure leading to a thicker, longer cap" [Khan2020, §Results] — dose is a first-order optical parameter, not a housekeeping detail | [Khan2020] |

### Reliability / qualification stress

| Measurement target | Tool | Output information | Applicable conditions | Common misuse | Source [Key] |
|---------|------|---------|---------|---------|---------|
| Temperature-cycling stability | Thermal-cycling chamber (e.g. −40 to +85 °C), ideally with in-situ optical monitoring | ΔIL, ΔRL vs. cycle count; hysteresis | Telcordia GR-series pass criteria apply for telecom deployment | Measuring only before and after the whole cycle set — a transient or a step at cycle 12 is then invisible | → `v_groove_fabrication.md` Node 5 |
| Damp-heat / moisture stability | 85 °C / 85 % RH chamber | Gradual IL/RL change; adhesion degradation | Long duration; needs unstressed controls aged in parallel | Attributing all drift to moisture without a dry-aged control | [synthesis] |
| Mechanical shock & vibration | Shock table, vibration shaker | Position shift, abrupt IL steps | Fixture resonances can dominate — instrument the fixture | Testing a bare coupon whose stiffness differs from the product housing | [synthesis] |

---

## 3. Standard Modeling & Experimental Toolchain

```
Geometry / process model
→ Input:  measured {W_top, D, α, R_bottom, P_Vgroove} + fiber {r ± tol, concentricity}
→ Output: seated fiber pose {x_f, y_f, θ_f} and its distribution (NOT a nominal point)
    ↓
Optical model
→ Input:  fiber mode + chip mode (from the SSC/taper design, → adiabatic_taper_ssc.md)
→ Tools:  EME (eigenmode expansion, 本徵模展開), 3D-FDTD, BPM, or an FEM mode solver + overlap integral
→ Output: IL(x, y, z, θ, λ, polarization) — a sensitivity surface, not a single nominal IL
    ↓
Assembly & cure study (DOE)
→ Input:  adhesive type, dispensed volume, dispense location, UV dose, thermal-cure profile,
          cap/clamp design, insertion force, end-stop geometry
→ Output: ΔIL_cure distribution, post-cure RL, channel uniformity, measured displacement
    ↓
Reliability transfer function
→ Input:  qualification stresses (T, ΔT, N_cycle, RH, t, P_optical, P_electrical)
→ Output: ΔIL(stress) mapped onto a named failure mechanism (crack / creep / moisture /
          CTE hysteresis / delamination), plus the worst-channel statistic for arrays
```

Each stage's output is the next stage's input **as a distribution**. Collapsing any stage to its
nominal value is the single most common way this chain produces a design that passes simulation and
fails at yield.

---

## 4. Domain-Specific Fitting & Analysis Methods

| Method | Applicable question | Applicable conditions | Common error | Correct approach | Source [Key] |
|---|---|---|---|---|---|
| Gaussian-approximation misalignment model | How much loss does a given offset/tilt/gap cause? | Both modes near-Gaussian; small offsets relative to the mode radii. Marcuse's analysis rests on the observation that single-mode fiber modes are "very nearly gaussian in shape regardless of the fiber type," reducing splice loss to the corresponding Gaussian-beam loss [Marcuse1977, abstract] | ⚠ Applying it to a strongly non-Gaussian inverse-taper or SSC output mode, or to large tilts, and reporting the result as the tolerance | Use the Gaussian form for scoping and sensitivity ranking; verify the final number with a full-vectorial overlap or 3D-FDTD sweep on the actual mode profile | [Marcuse1977] |
| 1-dB tolerance extraction from a scan | What is the real per-axis tolerance of *this* build? | A dense loss-vs-offset scan on one axis at a time, at fixed polarization and wavelength | ⚠ Taking two points either side of the peak and interpolating; sweeping two axes simultaneously | Fit the full scan (Gaussian or measured-mode overlap), report the axis, the dB threshold, and the wavelength/polarization with the number | [synthesis] |
| Tolerance stack-up: worst-case sum vs. RSS | What total core-to-mode offset should the design assume? | RSS is valid only for terms that are independent and roughly symmetric | ⚠ Applying RSS to systematic terms. Etch bias, overlay, and cure shrinkage are *biased* (they push one direction) — RSS on them understates the real offset | Separate systematic (add as signed bias) from random (combine in RSS); state which term was treated which way | [synthesis] |
| ΔIL_cure attribution | Did the cure move the fiber, and by how much? | Requires IL measured pre-cure, during cure, and post-cure on the same unit | ⚠ Reporting only final IL and calling a good number "process capability" | Report ΔIL_cure = IL_post − IL_pre as its own metric and correlate it against dispensed volume, shrinkage, cure temperature, and cap constraint | [synthesis] |
| Arrhenius / time-temperature analysis of drift | Can accelerated ageing predict field life? | One dominant thermally-activated mechanism over the fitted range | ⚠ Fitting a single activation energy across mixed mechanisms — an adhesive crack gives an abrupt IL *step*, creep gives a *monotonic* ramp; a single Ea over both is meaningless | Classify the ΔIL time-series shape first (step vs. ramp vs. cyclic hysteresis), fit only within one mechanism, and say which mechanism the Ea belongs to | [synthesis] |
| Extreme-value / worst-channel statistics for arrays | What IL does the system actually see? | Multi-channel FAU; per-channel IL recorded individually | ⚠ Reporting mean IL and standard deviation for a package whose link budget is set by max(IL) | Report worst-channel IL and the full per-channel distribution; the mean is a process-monitoring statistic, not an acceptance criterion | [synthesis] |
| FP-ripple period → gap length | How large is the residual air gap? | A resolvable etalon exists between two partially-reflecting facets | ⚠ Reading the ripple as device spectral response | Convert the free spectral range to an optical path length, then to a physical gap using the medium index (air vs. index-matching adhesive) | [synthesis] |

---

## 5. Domain-Specific Quality Metrics

| Metric | Abbreviation | Physical meaning | Typical value range | Conditions (material/method/wavelength/temp…) | Source [Key] |
|------|------|---------|------------|------|------|
| Coupling loss per coupler | CL | Power lost at one fiber–chip interface | 1.1 dB (forked coupler) / 1.4 dB (conventional taper) | Capped adiabatic tapered fiber to **sub-micron silicon nitride** waveguide; minimum measured values per coupler *after correcting for waveguide propagation loss*; SU8 cap | [Khan2020] |
| Packaged-device coupling loss | — | Same, after the fiber is permanently attached | 1.3 dB | Same platform and structure as above, packaged (vs. 1.1 dB unpackaged forked coupler) — the ~0.2 dB delta is the packaging penalty | [Khan2020] |
| 3-dB / 1-dB optical bandwidth | — | Wavelength span within the stated excess loss | Forked coupler: 90 nm (3-dB, measured). Conventional taper: >100 nm 1-dB measured, **>250 nm 3-dB extrapolated** (beyond the measurement apparatus range) | Same SiN platform; note the **trade-off**: the low-loss forked structure has the *narrower* bandwidth. These are two designs, not a "1.1–1.4 dB / >90–250 nm" range | [Khan2020] |
| 1-dB misalignment tolerance, edge coupler | — | Offset causing 1 dB excess loss | ~0.5 µm | Reported as the comparison baseline for edge couplers in a cryogenic-packaging method comparison | [Lin2023, Table] |
| 1-dB misalignment tolerance, grating coupler | — | As above, grating route | ~2 µm | Same comparison table | [Lin2023, Table] |
| Misalignment tolerance, photonic wire bond | — | As above, free-form polymer bridge | ">30 µm in all axis"; the paper contrasts this with "the 0.5 – 2 µm tolerance of the other methods using grating couplers or edge couplers" and notes "the assembly process does not require any active alignment" | Polymer photonic wire bond, SMF-28 fiber array to tapered silicon waveguide; a separate passage gives ">30 µm of x-y tolerance, >100 µm of tolerance along optical axis" | [Lin2023, §Results] |
| Cryogenic per-bond insertion loss | IL | Loss through one photonic wire bond at cryogenic temperature | 2.7 ± 0.1 dB at 5 K (before accounting for 0.7 ± 0.2 dB excess measurement loss per PWB); abstract-level claim: "less than 2 dB per connection" | 1550 nm, polarization-scrambler method, SMF-28 to silicon photonic chip; operation demonstrated down to **970 mK**; transmission "slightly degrades from 300 K to 5 K… and returns back to its original value after warming up" | [Lin2023] |
| Cladding diameter | — | The cylinder the groove actually locates | 125.0 ± 0.7 µm | Corning SMF-28® Ultra, Dimensional Specifications. Via the 1.732 lever of constraint 2, ±0.35 µm of radius error alone maps to ≈0.61 µm of vertical core motion [synthesis] | [Corning2013] |
| Core-clad concentricity | — | Core offset from the cladding's geometric centre | ≤ 0.5 µm | Same datasheet; **irreducible by packaging** | [Corning2013] |
| Cladding non-circularity | — | Departure of the cladding from a perfect circle | ≤ 0.7 % | Same datasheet; matters because two-point wedge seating assumes a circular cross-section | [Corning2013] |
| Coating diameter / coating-clad concentricity | — | The polymer layer stripped before seating | 242 ± 5 µm; coating-cladding concentricity < 12 µm | Same datasheet — the 12 µm figure is why *residual coating* in the groove is a first-order seating error, not a cosmetic one | [Corning2013] |
| Demonstrated passive-alignment accuracy (chip-to-chip, state of the art) | — | How well a purely passive platform can register two chips | 260 nm lateral, 240 nm height; −2.4 dB chip-to-chip optical link loss | Alignment structures written on the **chip backside at wafer scale**, using an **elastic-averaging** scheme (many compliant contacts averaging out individual feature error, rather than exact-constraint kinematic seating). Figures from the authors' lab summary, not the article text — see §7b access tag | [Kumar2025] |
| Fiber-limited floor for the same comparison | — | Why chip-to-chip and fiber-to-chip passive alignment do not scale together | Platform accuracy 260 nm vs. fiber core-clad concentricity ≤ 500 nm | `[synthesis]` from [Kumar2025] + [Corning2013]: a passive platform can now register two *chips* to better than the fiber's own core-to-cladding tolerance. For chip-to-chip the platform is the limiting datum; for **fiber**-to-chip the **fiber** becomes the limiting datum, and buying a better platform stops helping. Check which regime the user is in before recommending a precision upgrade | [synthesis] |
| Elimination of the groove-to-waveguide overlay term | — | Whether `r_groove→wg` exists at all in the budget | Reducible to zero *by construction* when groove and waveguide are co-defined | "The waveguide channels aligned to the center of the V-grooves are also processed together with the V-grooves using the same photolithography and etching technology," explicitly contrasted with "the use of silicon V-grooves as fiber carrier… in which V-groove and devices are made on different substrate and bonded together later" — demonstrated on a **polymer waveguide** platform, with no coupling-loss figure reported [Chen1997, abstract] | [Chen1997] |
| Worst-channel insertion loss | IL_worst | max over channels of per-channel IL | Application-set, not a literature constant | The governing acceptance metric for multi-channel FAU/CPO packages, because one bad channel limits the transceiver link budget [synthesis] | [synthesis] |
| Post-stress IL drift | ΔIL | Change in IL after a qualification stress | Telcordia pass criteria (±0.5 dB IL, ±0.2 dB PDL) are recorded in the sibling profile — cross-reference rather than re-quote | Telcordia GR-series thermal cycling for telecom deployment; **not re-verified in this profile's own pass**. Pointer re-homed 2026-08-24: the criteria now live with the qualification profile, which owns acceptance criteria | → `siph_packaging_reliability.md` Node 5 (verification history originates in `v_groove_fabrication.md` §7b) |
| Polymer waveguide propagation loss (interposer route) | — | Loss per unit length in an interposer's polymer waveguide | 1.92 dB/cm at 1310 nm | Glass interposer with polymer optical waveguides, flip-chipped PIC, no active alignment | [Boucaud2024] |
| Turning-mirror + grating-coupler loss (interposer route) | — | Coupling loss of the vertical redirection path | 18.7 dB | Same glass-interposer assembly — a cautionary datum: an alignment-tolerant architecture can carry a very large optical price | [Boucaud2024] |

---

## 6. Common Assumption Pitfalls

| Pitfall | Trigger condition | How to recognize it | Correct approach | Source [Key] |
|------|---------|---------|---------|---------|
| Using the 54.74° {111}-to-surface angle as the wedge half-angle in h = r/sin α | User computes seated-fiber height on a KOH/TMAH Si V-groove | The computed centre height comes out ≈76.6 µm for a 125 µm fiber instead of ≈108.3 µm — a ~32 µm error, ~50× the whole alignment budget | The half-angle from the bisector is α = 90° − 54.74° = 35.26° (included angle 70.53°); h = r/sin 35.26° = 1.732 r. **This exact error was present in the source packet for this profile** | [synthesis], premise → `v_groove_fabrication.md` Node 1 |
| Believing the etch *depth* sets the fiber height | User proposes to tune fiber height by etching deeper | Depth is quoted as the control knob for vertical alignment on a self-terminated {111} groove | For a fully-formed {111} groove, depth is slaved to opening width (D = 0.7071 W); the height above the surface is h = 1.732 r − 0.7071 W, so **mask CD and etch bias**, not depth, are the control variables (dh/dW = −0.707) | [synthesis] |
| "Passive alignment" = no measurement, no precision equipment | User frames passive vs. active as cheap-vs-expensive | Cost argument made with no error budget attached | Passive means the *final* position comes from mechanical features rather than optical-feedback search; "semi-passive" schemes constrain some axes mechanically and still use feedback on others [Bernabé2012]. Ask which axes are which | [Bernabé2012] |
| Treating the mechanical datum as the optical datum | User says the groove "locates the fiber" and stops there | The budget has no concentricity term | The groove locates the 125 µm cladding cylinder; the mode is at the core, offset by ≤0.5 µm of concentricity error that no groove improvement removes | [Corning2013] |
| Ignoring residual coating or particles at the seating line | Fiber prepared by stripping, then placed without a cleanliness spec | Sporadic outlier channels with no process correlation | Coating-cladding concentricity is <12 µm — a coating remnant is a ten-µm-class seating error, i.e. it dominates every other term at once | [Corning2013] |
| Treating the adhesive as a neutral fixture | Study scope is "V-groove profile vs. coupling loss" | No dispense volume, viscosity, wetting angle, dispense architecture, cure schedule, or cap design recorded | Adhesive flow exerts real forces on a seated fiber, and the sign depends on the dispense architecture: with top dispensing "another cover plate is usually required to press the fiber against the walls of the V-groove", whereas with a canal/reservoir side-fill "the flow of epoxy can align the optical fiber by the surface tension" [Lo2003, abstract]. Separately, the three contact points "experience a considerable amount of stress due to the contraction and expansion of the adhesive" over life [EP1308760, background]. Record adhesive parameters as experimental variables, not consumable details. ⚠ Do **not** state fiber float-up/buoyancy as the reason for the cover plate — that causation is unsourced (see §7b withdrawal) | [Lo2003], [EP1308760] |
| Measuring IL only after cure | Assembly DOE reports a single IL per unit | No ΔIL_cure column anywhere in the data | Measure pre-cure, in-situ during cure, and post-cure; without the pre-cure value, `r_cure` is silently folded into `r_assembly` and the DOE cannot separate them | [synthesis] |
| Expecting the groove to fix mode mismatch | User reports high IL with a geometrically perfect groove | Loss is flat against alignment improvements | Mode-overlap loss is a floor set by MFD mismatch; it requires an SSC/inverse taper, not a better groove → `adiabatic_taper_ssc.md` | [Marchetti2019] |
| Quoting "alignment tolerance" with no axis and no dB threshold | Any comparison of coupling schemes | A single µm number stands alone in a table | Always state axis, threshold, wavelength, polarization. The published contrast is ~0.5 µm (edge), ~2 µm (grating), >30 µm (photonic wire bond) — the numbers are only comparable because the source states a common basis [Lin2023] | [Lin2023] |
| Reporting mean IL for a fiber array | Multi-channel FAU results summarized as "average 0.8 dB" | No worst-channel figure and no per-channel table | The link budget is set by the worst channel; report max and the distribution, and state channel count | [synthesis] |
| Assuming an interposer or alignment-tolerant architecture is automatically better | User proposes moving the datum off the PIC to relax tolerance | Loss budget not recomputed for the new path | Relaxing alignment can cost a lot of light: a glass-interposer route with a turning mirror reports 18.7 dB through mirror + grating coupler, with 1.92 dB/cm polymer waveguide loss at 1310 nm [Boucaud2024]. Alignment tolerance and insertion loss are traded, not both won | [Boucaud2024] |
| Attributing a paper's description of *conventional practice* to its own demonstrated method | User cites "Khan/APL Photonics 2020" for a KOH V-groove of depth ≈ fiber radius | The claim is presented as the paper's result rather than its background | Khan et al. describe the conventional approach — "V-grooves are etched in the chip leading up to the waveguide… usually etched with hot potassium hydroxide and extend into the surface of the silicon chip by roughly the fiber radius (62.5 µm)" — and immediately note "this fabrication is not compatible with all integrated photonics processes," then present a *different* method (capped adiabatic tapered fiber + forked on-chip waveguide). **The source packet for this profile made exactly this attribution error** | [Khan2020, §Introduction] |
| Reading "the fiber is entirely self-aligned by the V-groove" as an optical result | User cites early V-groove self-alignment work as evidence that the coupling problem is solved | The claim of self-alignment appears with no coupling-loss figure attached | The original statement — "The fiber placed in the V-groove is entirely self-aligned in both vertical and lateral directions" [Chen1997, abstract] — is a claim about **geometric degrees of freedom being removed**, on a polymer-waveguide platform, with no IL reported in the abstract. Geometric constraint eliminates `r_assembly`; it does nothing to `r_fiber/core`, `r_cure`, or `r_thermal`. Ask for the measured IL distribution before treating self-alignment as a loss result | [Chen1997] |
| Buying platform precision when the fiber is the limiting datum | User proposes tighter grooves/stages to improve a fiber-to-chip package | The proposed improvement is smaller than ~0.5 µm, with no mention of fiber geometry tolerance | Below roughly the fiber's own core-clad concentricity (≤ 0.5 µm) and cladding-diameter tolerance (±0.35 µm radius, levered ×1.732 into height), platform improvements stop moving the core. State-of-the-art chip-to-chip passive platforms already register to 260 nm lateral / 240 nm height [Kumar2025] — better than the fiber allows. Redirect to fiber selection/screening, or to enlarging the mode (→ `adiabatic_taper_ssc.md`) | [Kumar2025], [Corning2013] |
| Assuming an "alignment-free" coupler removes the tolerance problem rather than relocating it | User cites alignment-free/self-aligning interconnect work as a solution | No statement of what the new dominant error term is | The alignment-free evanescent coupler engineers a translationally-invariant interaction by intersecting waveguides at an angle [Bandyopadhyay2021] — the tolerance moves from placement to angle/gap control and to the added interface's own loss. Ask which term the architecture is actually trading away | [Bandyopadhyay2021] |

---

## 7a. Literature Anchors

| Type | Reference | Why it matters |
|------|------|-------|
| Foundational method | Marcuse, D., "Loss Analysis of Single-Mode Fiber Splices," *Bell System Technical Journal* 56(5), 703–718 (1977) | The canonical Gaussian-approximation treatment of offset, tilt, and gap loss — the analytical backbone of every alignment-tolerance estimate in this domain |
| Review | Marchetti, R., Lacava, C., Carroll, L., Gradkowski, K., Minzioni, P., "Coupling strategies for silicon photonics integrated chips [Invited]," *Photonics Research* 7(2), 201 (2019) | The standard entry point covering edge coupling, grating coupling, mode converters, and V-groove-enabled passive alignment in one framework |
| Method / measured data | Khan, S., Buckley, S.M., Chiles, J., Mirin, R.P., Nam, S.W., Shainline, J.M., "Low-loss, high-bandwidth fiber-to-chip coupling using capped adiabatic tapered fibers," *APL Photonics* 5, 056101 (2020) | Quantitative, condition-stated coupling-loss and bandwidth data on SiN, plus an explicit statement of the conventional KOH V-groove practice and its process-compatibility limits |
| Architecture comparison | Lin, B., Witt, D., Young, J.F., Chrostowski, L., "Cryogenic optical packaging using photonic wire bonds," *APL Photonics* 8, 126109 (2023) | The cleanest published side-by-side of misalignment tolerance across coupling schemes (edge ~0.5 µm / grating ~2 µm / PWB >30 µm), and a worked case of alignment tolerance bought at the cost of a different failure mode |
| Assembly / process | Lee, S.W.R., Lo, C.C., "Passive Alignment of Optical Fibers in V-grooves with Low Viscosity Epoxy Flow," in Suhir, Lee & Wong (eds.), *Micro- and Opto-Electronic Materials and Structures*, Springer (2007) | The attach step treated as a fluid-mechanics and process problem rather than a bonding afterthought — the origin of this profile's "adhesive is not a neutral fixture" constraint |
| Practice boundary | Bernabé, S., Porte, H., et al., "In-plane pigtailing of silicon photonics device using 'semi-passive' strategies," IEEE (2012) | Defines the practical middle ground between passive and active alignment, which is where most real production processes actually sit |
| State-of-the-art benchmark | Kumar, S., Cardenas, J., "Passive alignment platform for electro-optic, photonic, and micro-optic systems," *Optics Express* 33(23), 48160 (2025), DOI 10.1364/OE.577054 | The current answer to "how good can purely passive get?" — 260 nm lateral / 240 nm height via wafer-scale backside structures and elastic averaging. Use it to calibrate whether a proposed precision improvement is even reachable, and to see where the fiber's own tolerance takes over as the limit |

---

## 7b. Source Ledger

> Legend — **Access tag**: `[full]` full text read · `[partial]` preview/excerpt/supplementary only ·
> `[abstract]` abstract/metadata only · `[secondary]` known only via another source.
> **Verification status**: ✅ Confirmed against the primary source · `~` Approximate (corroborated in
> general, exact figure not independently pinned) · ⚠ Unconfirmed · ❌ Withdrawn.
> **Verified (date)** (`domain-expansion-guide.md` §3.7): when this row's claim was last checked
> against the primary source — not the source's own publication year.
>
> **2026-08-26 currency pass** (audit trail: `reports/2026-08-26-scientific-research-guide-source-currency-pass.md`).
> All twelve source rows were checked in the two 2026-08-24 passes logged below, then re-resolved a
> third time on 2026-08-26 against Crossref, the arXiv API, and publisher/vendor/patent pages — never
> a search-engine summary. That pass confirmed every bibliographic identity, found **no errata or
> retractions**, added three missing DOIs ([Boucaud2024], [Bernabé2012], and the conference-side DOI
> for [Lo2003]), pinned exact arXiv versions for the three preprints ([Khan2020], [Lin2023],
> [Bandyopadhyay2021] — each has only v1, so the pin is trivial but now explicit), and **caught one
> defect both earlier audits missed**: [Lo2003]'s Full-citation cell presented a six-author conference
> paper and its two-author (Lee & Lo) 2007 Springer chapter as one byline-preserving republication.
> They are not the same byline. One row, [Corning2013], could **not** be re-verified — the official
> host still 403s and the mirrors tried were unreachable or undecodable — so its Verified (date) stays
> at the 2026-08-24 act that actually read the content, marked as blocked rather than blanket-stamped.

| Key | Full citation | Identifier | Access tag | Verification status | Verified (date) | Locator | Used in (Node/row) |
|---|---|---|---|---|---|---|---|
| [Marcuse1977] | Marcuse, D., "Loss Analysis of Single-Mode Fiber Splices," *Bell Syst. Tech. J.* 56(5), 703–718 (1977) | DOI 10.1002/j.1538-7305.1977.tb00534.x; archive.org/details/bstj56-5-703 | [abstract] | ✅ Identity, venue, pagination and the Gaussian-mode premise confirmed 2026-08-24; the explicit offset-loss expression was **not** read in full text. Re-confirmed against Crossref metadata 2026-08-26 (title/author/venue/pages/date exact match); no erratum/retraction field present | 2026-08-26 | Abstract | 1 (principles), 4 (Gaussian model), 7a |
| [Marchetti2019] | Marchetti, R., Lacava, C., Carroll, L., Gradkowski, K., Minzioni, P., "Coupling strategies for silicon photonics integrated chips [Invited]," *Photonics Research* 7(2), 201 (2019) | DOI 10.1364/PRJ.7.000201 | [abstract] | ✅ Identity, full author list, venue, DOI confirmed 2026-08-24. Title corrected: carries the "[Invited]" designation. Re-confirmed against Crossref metadata 2026-08-26 (exact match, all 5 authors in order); no erratum/retraction field present | 2026-08-26 | Article metadata | 6 (mode-mismatch row), 7a |
| [Khan2020] | Khan, S., Buckley, S.M., Chiles, J., Mirin, R.P., Nam, S.W., Shainline, J.M., "Low-loss, high-bandwidth fiber-to-chip coupling using capped adiabatic tapered fibers," *APL Photonics* 5, 056101 (2020) | DOI 10.1063/1.5145105; arXiv:2002.00729v1 (sole existing version, submitted 2020-01-21) | [full] | ✅ All quoted sentences and numbers extracted verbatim from the arXiv full text 2026-08-24. Re-confirmed against Crossref + arXiv API metadata 2026-08-26 (all 6 authors, venue, article no. exact match); no v2 exists; targeted search found no erratum/correction notice | 2026-08-26 | Abstract; §Introduction (V-groove/KOH sentence); §Results (loss, bandwidth, SU8 cap) | 2 (optical, UV dose), 5 (CL, packaged CL, bandwidth), 6 (attribution pitfall), 7a |
| [Lin2023] | Lin, B., Witt, D., Young, J.F., Chrostowski, L., "Cryogenic optical packaging using photonic wire bonds," *APL Photonics* 8, 126109 (2023) | arXiv:2307.07496v1 (sole existing version, submitted 2023-07-14); ADS 2023APLP....8l6109L | [full] | ✅ Tolerance figures, comparison table, IL and temperature extracted verbatim from the arXiv full text 2026-08-24. Re-confirmed against arXiv API metadata 2026-08-26 (all 4 authors exact match); no v2 exists; targeted search found no retraction/erratum | 2026-08-26 | §Introduction (>30 µm x-y, >100 µm axial); §Results (">30 µm in all axis"); comparison table; §Results (2.7 ± 0.1 dB at 5 K); abstract (970 mK) | 2 (tolerance sweep), 5 (three tolerance rows, cryo IL), 6 (axis/threshold row), 7a |
| [Corning2013] | Corning® SMF-28® Ultra Optical Fiber, Product Information sheet PI1424, issued March 2013 (© 2013 Corning Incorporated) | Corning PI-1424-AEN (vendor datasheet) | [full] | ✅ Dimensional Specifications block extracted verbatim from the datasheet PDF 2026-08-24. ⚠ Read from a **third-party mirror** of the March 2013 issue — Corning's own host returned HTTP 403 in this pass. Glass-geometry tolerances are historically stable across revisions, but re-check against the current Corning-hosted sheet before using these numbers in a submitted acceptance spec. **Re-verification attempted 2026-08-26 and failed**: corning.com's current PI-1424-AEN path still returns 403, one third-party mirror refused the connection, and a second was fetched but could not be decoded this session — the numbers were NOT re-confirmed, and the 2026-08-24 verification stands unchanged. `review-when:` corning.com serves this sheet without a 403, or a PI-1424 revision newer than March 2013 is issued | 2026-08-24 (⚠ not re-verified 2026-08-26 — attempted, blocked) | Table: Dimensional Specifications (Glass Geometry / Coating Geometry) | 1 (constraint 1, budget table), 5 (four fiber-geometry rows), 6 (datum + coating rows) |
| [Boucaud2024] | Boucaud, J.-M., Durand, C., Gianesello, F., Bucci, D., Broquin, J.-E., Dubois, E., "Glass interposer for heterogeneous integration of flip-chipped photonic and electronic integrated circuits," *Appl. Phys. Lett.* 125, 054101 (2024) | DOI 10.1063/5.0221309; HAL hal-04665935 | [abstract] | ✅ Identity, authors, venue confirmed; the 1.92 dB/cm and 18.7 dB figures are **abstract/summary-level**, not read in the full text. ⚠ The source packet's characterization of this work as *fiber-to-interposer passive butt alignment* is **wrong**: the scheme uses a polymer waveguide + integrated turning mirror redirecting light vertically into a flip-chipped PIC's **grating coupler**. Re-confirmed 2026-08-26 via Crossref (all 6 authors, venue, page, issued 2024-07-29 exact match); the DOI was missing from the Identifier cell and is now recorded; no erratum/relation field present | 2026-08-26 | Abstract / summary | 5 (two interposer rows), 6 (interposer-tolerance-cost row) |
| [Bernabé2012] | Bernabé, S., Porte, H., et al., "In-plane pigtailing of silicon photonics device using 'semi-passive' strategies," IEEE (2012) | DOI 10.1109/ESTC.2012.6542171; IEEE Xplore document 6542171 | [abstract] | ✅ Identity confirmed. Title corrected: the published title is "…using 'semi-passive' **strategies**", not "…semi-passive **alignment** strategies" as the packet had it. Re-confirmed 2026-08-26 via Crossref: the venue is the "2012 4th Electronic System-Integration Technology Conference (ESTC)", and the full 11-author byline (Bernabé, Porte, Roux, Blind, Kopp, Lasfargues, Borel, Gindre, Gabette, Nicolas, Fédéli) is consistent with this row's "et al."; DOI resolved and added | 2026-08-26 | Abstract | 1 ("what passive means"), 6 (passive≠no-metrology row), 7a |
| [Lo2003] | Lo, J.C.C., Yung, C.S., Lee, S.W.R., Lee, S.H.K., Wu, J.S., Yuen, M.M.F., "Passive alignment of optical fiber in a V-groove with low viscosity epoxy flow," *2003 ASME International Mechanical Engineering Congress*, Washington DC (2003), DOI 10.1115/IMECE2003-43902. **A related but separately-authored publication** — Lee, S.W.R., Lo, C.C., "Passive Alignment of Optical Fibers in V-grooves with Low Viscosity Epoxy Flow," in Suhir, E., Lee, Y.C., Wong, C.P. (eds.), *Micro- and Opto-Electronic Materials and Structures*, Springer (2007), DOI 10.1007/0-387-32989-7_26 — covers the same topic but carries **only two** of the six conference-paper authors (S.W. Ricky Lee and C.C. Lo). It is not a byline-preserving republication and must not be cited as if it shared the six-author list | HKUST research portal record; conference DOI 10.1115/IMECE2003-43902; book chapter DOI 10.1007/0-387-32989-7_26 (2 authors: Lee & Lo) | [abstract] | ✅ **for the cover-plate practice** — abstract read verbatim: "The epoxy is dispensed from the top of the V-groove and another cover plate is usually required to press the fiber against the walls of the V-groove." ✅ **for the flow-as-alignment-force finding** — "It is observed that the flow of epoxy can align the optical fiber by the surface tension." ❌ **for the buoyancy mechanism** — see the withdrawal note below. **Corrected 2026-08-26**: the earlier caveat that book-chapter authorship "was not independently confirmed" is now resolved — Crossref and an independent search both give the 2007 chapter's byline as Lee & Lo only (two authors), not the six-author conference list, so the Full-citation cell no longer implies a shared byline. The conference paper's own DOI (10.1115/IMECE2003-43902) was recovered from the HKUST portal in the same pass. Convention ruling (2026-08-26): the two publications stay under ONE key with the authorship difference spelled out, rather than splitting into `[Lo2003]` + `[Lee2007]` — every Node 6 quote is sourced to the conference abstract, so no Node-level citation changes either way | 2026-08-26 | Conference abstract (HKUST research portal), full text | 2 (dispense row), 6 (adhesive row) |
| [EP1308760] | "Fibre array with V-groove substrate and cover press plate," European patent application EP1308760A1. Applicant: Samsung Electronics Co., Ltd.; inventors Byung-Gil Jeong, Hyun-Chae Song, Seung-Wan Lee; published 2003-05-07 (filed 2002-10-31) | EP1308760A1 (Google Patents) | [partial] | ✅ Background section read. Engineering-context source (a patent, not peer-reviewed) — used only for what the industry states the cover plate and adhesive do. Verbatim: the three contact points "experience a considerable amount of stress due to the contraction and expansion of the adhesive B, which was injected to the contact points during the fabrication process." Notably, this source attributes the failure mode to **adhesive contraction/expansion stress**, *not* to fiber float-up. Re-confirmed verbatim 2026-08-26 via Google Patents; applicant, inventors and publication date added (not previously recorded) | 2026-08-26 | Background / prior art | 6 (adhesive row) |
| ❌ *(withdrawn claim, no key)* | "Epoxy flow buoyancy lifts the fiber out of the V-groove, which is why a cover plate is required" — asserted by the source packet and cited to the Springer chapter | — | — | ❌ **Withdrawn 2026-08-24.** Checked against three sources, none of which supports the causal claim: (1) [Lo2003]'s abstract states the cover-plate practice with **no cause given**; (2) the same paper's own finding runs the opposite way — epoxy flow *aligns* the fiber by surface tension; (3) [EP1308760]'s background attributes the contact-point problem to adhesive contraction/expansion stress, not lifting. A web-search summary layer did assert the buoyancy causation when queried, with no quotable locator — that summary is precisely the kind of generated-causation artifact this ledger exists to stop. Do not re-add without a primary source that states it. Spot-checked again 2026-08-26 against fresh fetches of both [Lo2003] and [EP1308760]: the withdrawal still holds — neither source has since surfaced a buoyancy causation statement | 2026-08-26 (spot-check; not a source row) | — | Removed from Node 6 (replaced by the sourced framing) |
| [Bandyopadhyay2021] | Bandyopadhyay, S., Englund, D., "Alignment-free photonic interconnects," arXiv:2110.12851 (2021) | arXiv:2110.12851v1 (sole existing version, submitted 2021-09-28) | [abstract] | ✅ Identity confirmed; the mechanism (translationally-invariant evanescent interaction via angled waveguide intersection) is stated in the abstract. Re-confirmed 2026-08-26 via the arXiv API (both authors, title and mechanism exact match); no v2 exists and no peer-reviewed journal version was found — this is still a preprint. `review-when:` this preprint appears in a peer-reviewed venue (a related patent application, US 2022/0146749 published 2022-05-12, was found but is not peer review) | 2026-08-26 | Abstract | 6 (alignment-free row) |
| [Kumar2025] | Kumar, S., Cardenas, J., "Passive alignment platform for electro-optic, photonic, and **micro-optic systems**," *Optics Express* 33(23), 48160 (2025), published 2025-11-06 | DOI 10.1364/OE.577054 | [secondary] | ✅ Title, authors, venue, volume/issue/page, publication date and DOI confirmed via Crossref 2026-08-24. **The packet's title — "…and electronic chiplets" — is wrong.** The quantitative results (260 nm lateral / 240 nm height alignment; −2.4 dB chip-to-chip optical link loss; alignment structures written on the chip **backside at wafer scale** using an **elastic-averaging** scheme) are taken from the authors' own lab page, not from the article text (Optica's page is behind a JS/login wall in this environment) — hence `[secondary]`. ⚠ The packet's "SiO₂-on-Si interposer" detail was **not** found in any accessible source. Follow-up by the same group: Kumar, Liyanaarachchi & Cardenas, "Passive Alignment Platform for Sub-Micron Precision in Packaging Electro-Optic Devices," CLEO 2026, JTu.59, DOI 10.1364/CLEO_AT.2026.JTu.59. Re-confirmed 2026-08-26 via Crossref (exact match); Optica's article page was re-attempted and is still JS-gated, so the quantitative figures remain lab-page-sourced. `review-when:` the *Optics Express* full text becomes readable — then re-source 260 nm / 240 nm / −2.4 dB from the article itself | 2026-08-26 (identity only; figures still `[secondary]`) | Crossref metadata; Cardenas Lab publication summary | 5 (state-of-the-art passive-alignment row), 7a |
| [Chen1997] | Chen, A., Ziari, M., Steier, W.H., "Passive alignment of optic fiber array using silicon V-grooves monolithically integrated with polymer waveguide devices," *Organic Thin Films for Photonics Applications* (OTFA) 1997, paper ThE.21 | opg.optica.org/abstract.cfm?uri=OTFA-1997-ThE.21 | [abstract] | ✅ Full abstract read verbatim 2026-08-24. Key sentences: "The waveguide channels aligned to the center of the V-grooves are also processed together with the V-grooves using the same photolithography and etching technology" and "The fiber placed in the V-groove is entirely self-aligned in both vertical and lateral directions." ⚠ Two conditions the packet dropped: the platform is a **polymer waveguide device**, not silicon photonics; and the abstract reports **no coupling-loss figure**, so "entirely self-aligned" is a claim about geometric constraint, not a measured optical result. Re-attempted 2026-08-26: the Optica abstract page confirmed title, all three authors, conference name/location/dates and paper number, but returned content as a paraphrase — so the exact quoted sentences above were **not** independently re-extracted word-for-word this pass | 2026-08-26 (identity only; verbatim wording not re-extracted) | Abstract | 1 (budget table, overlay term), 6 (self-alignment≠optical-alignment row) |

### Provenance & correction log (the source packet's nine anchors, audited 2026-08-24)

| Packet claim | Verdict | Correction applied |
|---|---|---|
| "[^1] Chen et al. 1997, *Passive alignment of optic fiber array using silicon V-groove*" | Title truncated; platform mischaracterized | Full title restored; noted as a **polymer waveguide** result |
| "[^2] Marchetti et al. 2019, *Photonics Research*" | ✅ Correct | "[Invited]" added; DOI resolved |
| "[^3]" (bare Springer DOI, no author or title) | Unresolvable as given | Resolved to Lo, Yung, Lee, Lee, Wu & Yuen (ASME IMECE 2003; Springer chapter 2007) — full author list recovered from the HKUST record |
| "[^3]" mechanism: 「epoxy 流動造成的浮力可能將光纖從 V-groove 抬起，因此需要額外 cover plate」 | ❌ **Causation withdrawn** (2nd pass, 2026-08-24) | The *consequent* is verbatim-confirmed ("another cover plate is usually required to press the fiber against the walls of the V-groove"); the *cause* is not stated by that source, and two further sources point elsewhere — the same paper reports epoxy flow **aligning** the fiber by surface tension, and [EP1308760] attributes contact-point damage to adhesive contraction/expansion. Node 6 row rewritten around what is actually sourced |
| "[^7] Kumar et al. 2025, *Passive alignment platform for electro-optic, photonic, and **electronic chiplets***" | ❌ **Title wrong** (2nd pass) | Crossref: "…and **micro-optic systems**", Kumar & Cardenas, *Opt. Express* 33(23) 48160, DOI 10.1364/OE.577054. Promoted into Node 5 with 260 nm / 240 nm / −2.4 dB from the authors' lab summary; the packet's "SiO₂-on-Si interposer" detail was not found and is **not** carried over, while the actual named mechanism (backside wafer-scale structures + elastic averaging) was missing from the packet |
| "[^1] Chen et al. 1997" | ✅ Promoted (2nd pass) | Full abstract read; now supports two Node entries — co-definition of groove and waveguide in one lithography step eliminates the overlay term, and "entirely self-aligned" is a geometric claim carrying no reported coupling loss |
| "[^4] **Theurer et al.** 2020, *Low-loss, high-bandwidth fiber-to-chip coupling using capped, tapered fibers*" | ❌ **Wrong authors** | Actual authors: Khan, Buckley, Chiles, Mirin, Nam, Shainline (NIST). Title: "…capped **adiabatic** tapered fibers" |
| Same paper: "1.1–1.4 dB per coupler, >90 nm, estimated >250 nm" | Trade-off flattened into a range | Split: 1.1 dB ↔ 90 nm (forked); 1.4 dB ↔ >250 nm extrapolated (conventional taper); packaged device 1.3 dB |
| Same paper: "為維持封裝機械完整性…其範例採 KOH 蝕刻，V-groove 深度約達 fiber radius" | Context inverted | The paper states this as **conventional practice it is departing from**, immediately adding that it "is not compatible with all integrated photonics processes." Recorded as a pitfall in Node 6 |
| "[^5] Boucaud et al. 2024… 強調 fiber 到 glass interposer 的 passive butt alignment" | Title wrong; mechanism wrong | Title is "…flip-chipped **photonic and electronic** integrated circuits"; the route is a turning mirror into a **grating coupler**, not butt/edge coupling. Loss figures added as a cautionary datum |
| "[^6] Bernabé et al. 2012" | ✅ Correct paper | Title corrected ("strategies", not "alignment strategies") |
| "[^7] Kumar et al. 2025" | ✅ Correct paper | Kumar **& Cardenas** (two authors); no claim drawn pending full text |
| "[^8] **Billah et al.** 2021, *Alignment-free photonic interconnects*" | ❌ **Wrong authors** | Actual authors: Bandyopadhyay & Englund (MIT). ("Billah" is associated with photonic **wire bonding**, a different technique) |
| "[^9] **Kück et al.** 2023, *Cryogenic optical packaging using photonic wire bonds*" | ❌ **Wrong authors** | Actual authors: Lin, Witt, Young, Chrostowski (UBC) |
| Same paper: ">30 µm transverse tolerance, 5 K 以下仍可運作" | ✅ Confirmed, with a caveat on the temperature figure | ">30 µm in all axis" verified verbatim. Temperature: the paper demonstrates operation **down to 970 mK**; the 4–5 K figures are the measurement points |

> **Methodological note worth carrying forward — the retrieval layer errs in both directions.**
> This audit caught one of each, on the same summarizing layer that sits between a query and the raw
> source:
> - **False negative.** An ar5iv-rendered full-text query returned "NOT FOUND" for the >30 µm
>   tolerance; extracting the PDF text directly located the sentence verbatim. A negative result from
>   a summarizing layer is not evidence of absence — confirm withdrawals against raw text before
>   deleting a claim.
> - **False positive.** Asked why a V-groove fiber array needs a cover plate, the same class of layer
>   returned a confident causal answer ("the fiber may be lifted up by the buoyancy of epoxy flow")
>   with **no quotable locator**, while the primary abstract states the practice and gives no cause at
>   all. A fluent causal sentence with no locator is a generated bridge between two real facts, not a
>   finding.
>
> Operational rule: **a claim may be added or removed only against text you can quote with a
> locator.** Summaries are for finding candidates, never for settling them. Note that the original
> source packet's buoyancy claim is most likely this same artifact, one generation earlier.

---

## Cross-Domain Links

### Closest Related Domain Profiles

| Profile name | Overlap dimensions | Typical use split |
|------|------|-------|
| `v_groove_fabrication.md` (V-Groove Fabrication) | first principles ({111} crystallography), measurement tools (groove metrology), application targets (FAU) | Use **that** profile for *how the groove is cut* — etch chemistry, sidewall angle and roughness, corner compensation, process selection. Use **this** profile for *what the groove does to the optical result* — how groove geometry propagates into core position, and everything downstream of seating (adhesive, cure, drift). The 54.74° constraint is *sourced* there and *consumed* here |
| `adiabatic_taper_ssc.md` (Adiabatic Taper & SSC) | first principles (mode overlap), quality metrics (coupling loss, 1-dB tolerance), application targets (edge coupling) | Use **that** profile for *how the mode is expanded and matched* — CMT, adiabaticity, SSC architecture, MFD-vs-density trade-off. Use **this** profile for *how the fiber gets to the mode and stays there* — datum chain, attach, qualification drift. A high-tolerance SSC and a precise groove are complements, not substitutes: the SSC sets the size of the target, this profile determines where the arrow lands |
| `silicon_photonics_device_physics.md` (SiPh Active Device Physics) | quality metrics (link budget, CPO), application targets | Use **that** profile for the active devices whose performance the link budget accounts for (modulators, Ge photodetectors, integrated/hybrid lasers) and for the budget itself; use **this** profile for the passive coupling interface that feeds them. The handoff is explicit: this profile's **worst-channel IL** is a line item in that profile's link budget, so a per-channel coupling number must be reconciled against the budget's margin before it is called acceptable |
| `siph_packaging_reliability.md` (Silicon Photonics Packaging & Reliability, 矽光子封裝與可靠度) | quality metrics (worst-channel IL, post-stress ΔIL), measurement tools (qualification chambers, in-situ optical monitoring), first principles (CTE-mismatch thermo-mechanics) | **Split settled 2026-08-24 — route by observable + scope.** Use **this** profile for the optical observable at ONE fiber–chip interface and the alignment/attach chain that moves it: ΔIL/ΔRL, cure-induced drift, per-channel and worst-channel array statistics ("how much did this coupling degrade, and why did the fiber move?"). Use **that** profile for module-level qualification planning, acceleration factors and their models (Arrhenius / Coffin–Manson / Peck / Weibull), failure-mechanism attribution across the whole package, and thermal architecture ("what stress matrix qualifies this module, and what acceleration factor applies?"). Neither absorbs the other's rows — shared concepts are pointers, never a second copy of a number |
| `adhesives_polymer_reliability.md` (Adhesives & Polymer Reliability) | first principles (cure shrinkage, viscoelasticity, CTE mismatch), measurement tools (qualification chambers) | Use **this** profile when the observable is optical (ΔIL, ΔRL) and the datum-chain/attach-process is the subject. Use **that** profile for material-level questions — degree of cure, Tg, moisture-uptake modeling, adhesion/fracture-mode chemistry — where the optical path is not itself the measurement |

### Boundary & ownership notes

- The three photonics-interface profiles (`v_groove_fabrication`, `adiabatic_taper_ssc`, and this one)
  intentionally partition one physical assembly into **cutting / mode-matching / placing-and-holding**.
  When a user's question spans two of them, load both and say which one owns the governing constraint.
- Cross-profile numbers are referenced, not copied. Telcordia thresholds and vendor FAU placement
  specs live in `v_groove_fabrication.md`; the SSC-side MFD and 1-dB tolerance figures live in
  `adiabatic_taper_ssc.md`. Re-quoting them here would create a second, un-versioned copy of a number
  whose verification status is recorded elsewhere.

---

## Cross-Domain Conflict Notes

| Issue / constraint | Other profile(s) involved | Potential conflict | AI confirmation question |
|------|------|-------|-------|
| Who owns the alignment budget | `v_groove_fabrication.md`, `adiabatic_taper_ssc.md` | The groove profile optimizes geometric precision; the SSC profile optimizes tolerance by enlarging the mode; this profile says the binding constraint may be neither (fiber concentricity, cure shrinkage). Three profiles can each propose a different "fix" for the same excess loss | "Before choosing a fix — have you measured which term dominates: groove geometry, mode mismatch, fiber concentricity, or cure-induced drift? If the budget has not been decomposed, the first task is decomposition, not optimization" |
| Groove geometry optimum vs. optical optimum | `v_groove_fabrication.md` | A groove tuned for process robustness (wider opening, more etch margin) moves the fiber centre vertically at −0.707 µm per µm of opening width — the process-friendly choice can be the optically worst one | "Is the groove opening width currently set by etch-process capability or by the optical vertical-alignment target? Those two criteria pull in opposite directions here" |
| MFD enlargement vs. channel pitch | `adiabatic_taper_ssc.md`, `siph_packaging_reliability.md` | Enlarging the mode to relax this profile's placement tolerance reduces achievable channel density — a direct trade against CPO's I/O-density goal | "Are you optimizing for a single low-loss channel or for a high-channel-count array where pitch dominates? The tolerance-vs-density trade has no free direction" |
| Destructive vs. non-destructive verification sequence | `v_groove_fabrication.md` | Cross-sectional SEM of the groove destroys the very sample whose post-cure fiber position you may want to measure later by CT | "Do you need this sample again after the cross-section? If the post-attach or post-cycling position matters, run non-destructive metrology (X-ray CT, IR microscopy) first and cross-section last" |
| Time-zero loss vs. life-end loss | `siph_packaging_reliability.md` (stress side); `adhesives_polymer_reliability.md` (material side) | An adhesive chosen for minimum cure shrinkage (best t = 0 IL) may have the worse creep or moisture behaviour (worst end-of-life ΔIL) | "Is the acceptance criterion initial IL, or IL after the full qualification sequence? The adhesive choice can invert between the two" |
