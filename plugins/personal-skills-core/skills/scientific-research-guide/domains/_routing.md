# Domain Routing Manifest

> Single source of truth for **which domain files exist** and **when to load each**.
> Gate A Step 0 (SKILL.md) consults this file before loading any Layer-B content.
> Keep it terse — this file is read on every domain-triage turn. One row per file.

## How Gate A uses this manifest

### The four rungs in full (moved from SKILL.md 2026-09-06, BODY_CAP trim)

SKILL.md keeps the ladder's shape and the rule that a fuzzy question is routed
rather than guessed; these are the matching rules each rung depends on.

1. **Literal anchor hit** — the user's wording contains a row's trigger keyword
   → load; standing triggers fire normally. Match **case-sensitively** (`TI`,
   `RIN`, `SPP` and 35 other short acronyms hit inside ordinary words once
   lower-cased) but **variant-insensitively**: compare in Unicode NFKC, so
   `Bi₂Se₃` matches the manifest's `Bi2Se3`, `Z2` matches `Z₂`, `μLED` matches
   `µLED`, and a full-width or superscript spelling matches its plain form. The
   manifest lists ONE spelling per term and relies on this.
2. **Scope match, no literal hit** (vague/fuzzy phrasing): match the described
   physical system and observable against the rows' `Covers / role` column and
   the Clusters/disambiguation sections below. Exactly one candidate → load it
   and **state the routing basis in one line** ("loading X — the question is
   about ⟨scope⟩") so a misroute is visible and correctable; never answer
   silently from a guessed profile.
3. **Two-plus candidates** (typically within a cluster) → ask ONE routing
   question taken from the relevant disambiguation table's own axis (those
   tables are pre-written clarification scripts), instead of speculatively
   loading several profiles. A question genuinely spanning two profiles still
   loads both and states which owns the governing constraint. **Exception** —
   on a pure retrieval turn (Step 0.5) do NOT block the handoff with a routing
   question: pick the best-scope candidate as search context and state the basis.
4. **No candidate** → proceed with the generic framework and say so; do not
   improvise domain-expert claims without Gate B verification.

Never compensate for a missed fuzzy match by adding broad manifest keywords —
keywords are precision anchors (a false load is worse than prose routing, see
§ Maintenance); recall for fuzzy phrasing is owned by this ladder.

### The load sequence

1. **Identify domain** — match the user's field against the `base` rows' triggers.
2. **Load the base profile** — always load the matched domain's base profile alongside
   the tier framework. Its standing triggers — Node 6's `Trigger condition` rows (primary),
   Node 1's constraints + Decision point, the Node 2/4 warning columns, and the Conflict
   Notes questions (`domain-expansion-guide.md` §3.6) — become standing if-then rules for
   the whole turn.
3. **Scan sub-profiles of that domain** — for every `sub-profile` row whose parent is the
   matched domain, check its load trigger against the user's wording. On a match, **load it
   and activate its own standing triggers** (they fire like the base profile's).
4. **Pull references on demand only** — `reference` / `boundary` rows are loaded only when
   the specific topic is explicitly engaged; they carry no standing triggers. A `boundary`
   row's job is to route the user *out* to a sibling domain when they cross the edge.
5. **Fuzzy questions (no literal keyword hit)** — the keyword column is a precision anchor,
   not the whole recall path. Route by the `Covers / role` column plus the Clusters /
   disambiguation sections below, per SKILL.md Step 0's resolution ladder: one candidate →
   load with a stated routing basis; several → ask the disambiguation table's own axis
   question; none → generic framework. Never widen recall by adding broad keywords
   (§ Maintenance). *Authoring consequence*: write `Covers / role` in the asker's frame
   (what the question is about) — it doubles as the fuzzy-routing index.

**How a keyword is compared (the matching rule).** Case-**sensitive** — `TI`, `RIN`, `SPP`
and 35 other short ASCII acronyms match inside ordinary words once lower-cased, measured
2026-08-26 over the eval prompts. Variant-**insensitive** — put both the user's wording and
the keyword into Unicode NFKC before comparing, so the compatibility spellings of one term
are one term: `Bi₂Se₃` = `Bi2Se3`, `Z₂` = `Z2`, `µLED`(U+00B5) = `μLED`(U+03BC), `cm²` = `cm2`,
full-width `Ｂｉ２Ｓｅ３` = `Bi2Se3`. A row therefore lists **one** spelling of a term and
never a variant list — see § Maintenance. `tools/routing_sim.py` implements exactly this.

Type semantics are defined in `domain-expansion-guide.md` §2 (the two-gate decision tree).

## Manifest

| Type | File | Parent | Load trigger (keywords) | Covers / role | Active triggers? |
|---|---|---|---|---|---|
| base | `plasmonic_waveguide.md` | — | SPP, plasmonics, surface plasmon, nanophotonic waveguide, SERS, near-field optics | Plasmonic/SPP waveguide domain profile | yes (Node 6) |
| base | `topological_insulator.md` | — | topological insulator, TI, Z₂, Bi2Se3, quantum spin Hall, Dirac surface state, QAHE, Majorana | Topological-insulator domain profile | yes (Node 6) |
| base | `gan_power_device.md` | — | vertical GaN, GaN power device, trench MOSFET, OG-FET, OG-MOSFET, CAVET, field plate, field shield, p-shield, dynamic RON | Vertical GaN power-device profile: architecture, processing, electrical extraction, and TCAD | yes (Node 6) |
| base | `microled.md` | — | microLED, micro-LED, micro LED, µLED, sidewall effect, pixel EQE, AlGaInP red microLED, InGaN microLED | Inorganic microLED pixel/optoelectronic device profile | yes (Node 6) |
| base | `v_groove_fabrication.md` | — | V-groove, V槽, fiber array unit, FAU, KOH etch, TMAH etch, anisotropic wet etch, DRIE V-groove, Bosch process groove, fiber alignment groove, 54.74°, silicon crystallographic groove | V-groove fabrication for optical fiber alignment: crystallographic wet etch, DRIE, laser ablation, mechanical dicing process selection | yes (Node 6) |
| base | `adiabatic_taper_ssc.md` | — | adiabatic taper, spot-size converter, SSC, mode converter, inverse taper, down-taper, edge coupler, GRIN coupler, coupled mode theory, CMT, MFD matching, MFD, mode field diameter, Petermann II, fiber-to-chip coupling, spot size conversion | Adiabatic taper / spot-size conversion in integrated photonics: CMT, adiabaticity criteria, SSC architectures, packaging alignment-tolerance trade-offs | yes (Node 6) |
| base | `fiber_chip_passive_alignment.md` | — | passive alignment, 被動對準, 被動對位, semi-passive alignment, active alignment, fiber attach, fiber attachment, pigtailing, alignment error budget, alignment tolerance budget, core-to-mode offset, core-clad concentricity, 光纖中心高度, 光纖高度, seated fiber height, fiber centre height, wedge half-angle, 35.26°, epoxy/adhesive fiber attach, cure-induced drift, worst-channel insertion loss, channel uniformity, photonic wire bond, alignment-free coupler, Telcordia GR-1221, thermal cycling IL drift | Fiber-to-chip passive alignment and attachment: datum chain, alignment error budget, adhesive/cure perturbation, thermo-mechanical drift, array worst-channel metrics | yes (Node 6) |
| base | `silicon_photonics_device_physics.md` | — | silicon photonics, SiPh, 矽光子, silicon modulator, ring modulator, MZI modulator, plasma dispersion, Soref-Bennett, carrier depletion, carrier injection, electro-absorption, Franz-Keldysh, QCSE, V_piL, extinction ratio, Ge photodetector, Ge-on-Si, germanium photodiode, avalanche photodiode, APD, responsivity, dark current, heterogeneous laser, III-V on Si, hybrid laser, quantum dot laser, threshold current, slope efficiency, RIN, linewidth, link budget, CPO, co-packaged optics | Silicon photonics ACTIVE device physics: integrated light sources, modulators, Ge photodetectors, and the carrier-photon-thermal chain linking device metrics to a link budget | yes (Node 6) |
| base | `siph_packaging_reliability.md` | — | silicon photonics packaging, photonic packaging, 光子封裝, 封裝可靠度, CPO, co-packaged optics, 共封裝光學, optical engine, reliability qualification, 可靠度驗證, Telcordia, GR-468, GR-1221, JEDEC JESD22, HAST, HTOL, THB, temperature cycling, thermal shock, accelerated life test, 加速壽命試驗, acceleration factor, Arrhenius, Coffin-Manson, Peck model, Weibull, delamination, 分層剝離, underfill, microbump, hybrid bonding, RDL, warpage, TIM, thermal crosstalk, 熱串擾, junction temperature, thermal resistance, failure mechanism, failure analysis, known-good die, KGD | Silicon photonics packaging & reliability: module-level qualification, stress-test matrix, physics-of-failure models, CPO thermal architecture, failure-mechanism attribution | yes (Node 6) |
| base | `adhesives_polymer_reliability.md` | — | adhesive, epoxy, 粘合劑, 環氧, degree of cure, 固化度, UV cure, UV-curable adhesive, UV固化, cationic epoxy, dual-cure, glass transition, Tg, moisture diffusion, 吸濕, moisture uptake, Fickian diffusion, Dual-Fick, Carter-Kibler, hygrothermal ageing, 濕熱老化, hydrolysis, 水解, cohesive failure, 內聚破壞, interfacial failure, 界面破壞, mixed failure, 混合失效, fatigue debonding, 疲勞脫黏, lap shear, refractive index vs cure, refractive index vs moisture, shadow-cure, cure shrinkage, adhesion force, HAST adhesion | Adhesives & polymer reliability for photonic-packaging bonds: cure chemistry, Tg, moisture diffusion, hygrothermal damage, interfacial fracture/fatigue | yes (Node 6) |
| reference | `plasmonic_waveguide/terminology_and_geometry.md` | plasmonic_waveguide | SP, SPP, SPR, LSP, LSPR, LSPP, IMI, MIM, MIN, HPW, Au film, Au grating, coupling loss, propagation loss | Terminology, geometry, and loss-accounting reference | no |
| sub-profile | `plasmonic_waveguide/active_modulation.md` | plasmonic_waveguide | plasmonic modulator, graphene modulator, ITO, ENZ, epsilon-near-zero, depletion, accumulation, bias-induced spectral shift, topological modulator | Active-material and bias-to-spectrum validation traps | yes (Node 6) |
| boundary | `plasmonic_waveguide/split_ring_resonators.md` | plasmonic_waveguide | SRR, split-ring resonator, LSRR, negative index, metamaterial, metasurface | Boundary to electromagnetic metamaterials; corrects unsupported SRR equivalences | no |
| sub-profile | `topological_insulator/bi2se3_material.md` | topological_insulator | Bi2Se3, bismuth selenide, Se vacancy, bulk conduction, quintuple layer, ultrathin film, BCB, BVB, SSB, Dirac point, band bending, intercalation | Material-scoped sub-profile: Bi₂Se₃ band labels, bulk conduction, thickness gap, and surface chemistry | yes (Node 6) |
| sub-profile | `topological_insulator/bi2se3_plasmonic_photoresponse.md` | topological_insulator | Dirac plasmon, Bi2Se3 plasmon, plasmon polariton, CPGE, LPGE, photogalvanic, polarization-resolved photocurrent, spin-momentum locked photocurrent, Bi2Se3 waveguide | Method sub-profile: Bi₂Se₃ plasmon channels, waveguide coupling, symmetry, and photogalvanic-response traps | yes (Node 6) |
| sub-profile | `topological_insulator/wal_hln_transport.md` | topological_insulator | WAL, weak antilocalization, HLN, HNL, Hikami-Larkin-Nagaoka, magnetoconductance, Hall measurement, phase coherence | Phenomenon/method sub-profile: WAL/HLN applicability and Hall-channel traps | yes (Node 6) |
| sub-profile | `topological_insulator/surface_and_composition_characterization.md` | topological_insulator | UPS, XPS, SECO, secondary electron cutoff, work function, EDS, EDX, elemental mapping, surface oxidation | Method sub-profile: surface/work-function/chemical-state/composition measurement traps | yes (Node 6) |
| sub-profile | `topological_insulator/device_fabrication.md` | topological_insulator | PMMA 950, electron-beam lithography, EBL, mesa, Hall bar, TFT response, KOH, consort, COMSOL, CST, etching | Method sub-profile: TI device process, geometry, and tool-identification traps | yes (Node 6) |
| reference | `silicon_photonics_device_physics/terminology.md` | silicon_photonics_device_physics | 中文術語, 翻譯, terminology, 電光 vs 電漿色散, 線寬 (linewidth vs CD), 異質整合 vs 混合整合, 消光比 vs 偏振消光比, 量子效率, T₀ vs T₀*, 響應度 vs 靈敏度 | English↔中文 term map for SiPh active devices + naming traps where the Chinese rendering itself causes a physics error | no |
| sub-profile | `silicon_photonics_device_physics/ring_resonator_thermal_control.md` | silicon_photonics_device_physics | ring thermal drift, 環形諧振腔熱控制, 熱致波長漂移, athermal ring, 無熱化環形, TiO2 cladding, titanium oxide cladding, liquid crystal cladding, LC cladding, ring heater, heater tuning efficiency, wavelength locking, thermal dithering, TDWS, mW/FSR, ring-to-ring thermal crosstalk, microring thermal crosstalk, Kij crosstalk matrix, thermal RC model ring | Ring-resonator thermal control: local thermo-optic drift, passive athermalization, heater tuning/feedback locking, WDM ring-to-ring thermal crosstalk, detuning-to-link-impairment chain | yes (Node 6) |
| sub-profile | `adiabatic_taper_ssc/freespace_mirror_relay.md` | adiabatic_taper_ssc | concave micromirror, curved micromirror, 凹面微鏡, 曲面側壁鏡, etched mirror facet, parabolic sidewall, parabolic-mirror collimator, micromirror collimator, slab free propagation region, FPR, free-space mirror relay, optical interposer, glass interposer, fiber socket, Two Stigmatic Points, off-axis astigmatism, TIR facet, sidewall verticality, photonic Damascene, crack-free SiN thickness, V-groove stationary width, 駐點槽寬, fold angle, beam turn angle, 折返角, 光束轉角, cone TIR, Goos-Hänchen, GH phase, near-Littrow, echelle angle, Z-fold, Z 字路徑, confocal parameter, collimated arm | Fiber-to-chip coupling relayed by etched curved mirrors in a planar slab: mirror sizing (f/z_R), which geometry off-axis astigmatism actually applies to (in-slab = cylindrical, no astigmatism), fold-angle limits from cone-TIR + GH phase gradient, echelle angles NOT transferable to single-mirror folds, collimated-arm length costs, roughness-to-loss model choice, the out-of-plane blind spot, SiN thickness ceiling on glass, and glass-interposer prior art | yes (Node 6) |

<!--
Add rows as content is authored. Only list files that ACTUALLY EXIST (Gate A will try to
load what it finds here). Row templates for the other two content types:

| sub-profile | `topological_insulator/wal.md`     | topological_insulator | WAL, weak antilocalization, HLN, Hikami-Larkin-Nagaoka, magnetoconductance | Phenomenon/method sub-profile: HLN-fit pitfalls | yes (Node 6) |
| sub-profile | `topological_insulator/hoti.md`    | topological_insulator | HOTI, higher-order topological, hinge state, corner state, nested Wilson loop | New-territory sub-profile: higher-order bulk-boundary | yes (Node 6) |
| boundary    | `topological_insulator/spt_vs_topological_order.md` | topological_insulator | SPT, symmetry-protected, topological order, long-range entanglement, anyon | Boundary note: routes OUT to a future intrinsic-topological-order domain | no |
-->

## Clusters

> A **sibling cluster** is N peer base profiles that partition ONE physical system — each pair
> passes Gate 1's divergence conditions against the other, so no shared parent exists (a base
> built on their thin intersection would be a fake parent). Shape definition, intersection
> test, and registration requirements: `domain-expansion-guide.md` §2. One entry per cluster.

| Cluster | Members (each owns…) | Ruling |
|---|---|---|
| **photonic-packaging** — one fiber-to-chip/CPO assembly, partitioned | `v_groove_fabrication` (cutting the groove) · `adiabatic_taper_ssc` (matching/expanding the mode) · `fiber_chip_passive_alignment` (placing and holding the fiber) · `siph_packaging_reliability` (proving the module survives) · `adhesives_polymer_reliability` (the bonding material itself: cure, moisture, fracture) | **Deliberately flat — settled 2026-08-24 for four members; a fifth member (`adhesives_polymer_reliability`) was added 2026-08-25 after re-running the same intersection test.** First principles, toolsets, and metric sets are pairwise disjoint across all five (the new member's toolset — DSC/DMA/TMA/Karl Fischer/Fickian diffusion modeling — and metrics — α, Tg, Msat, D, lap-shear — overlap with none of the other four); only the application target, IL/RL observables, and Telcordia vocabulary are shared. A `photonic_packaging.md` parent remains rejected as a fake parent. Do not build one, and do not re-ask. Routing between members: the two disambiguation sections below |

## Disambiguation: the five photonic-packaging interface profiles

`v_groove_fabrication` / `adiabatic_taper_ssc` / `fiber_chip_passive_alignment` /
`siph_packaging_reliability` / `adhesives_polymer_reliability` deliberately partition one physical
assembly. Their trigger keywords overlap, so route by **what the question is about**, not by which
word appeared:

| The question is about… | Load |
|---|---|
| Cutting the groove — etchant, sidewall angle, roughness, corner compensation, process selection | `v_groove_fabrication.md` |
| Matching/expanding the optical mode — taper adiabaticity, SSC architecture, MFD, coupling efficiency | `adiabatic_taper_ssc.md` |
| Getting the fiber to the mode and keeping it there — datum chain, error budget, adhesive/cure process, drift, array worst-channel | `fiber_chip_passive_alignment.md` |
| Proving the assembled module survives — stress matrix, standards selection, acceleration models, failure-mechanism attribution, CPO thermal architecture | `siph_packaging_reliability.md` |
| The bonding material itself — cure kinetics/degree of cure, Tg, moisture diffusion modeling, adhesion/fracture mechanism, refractive index vs. cure or moisture | `adhesives_polymer_reliability.md` |

The last two overlap most and were split by agreement (2026-08-24): **route by observable + scope** —
"how much did this coupling degrade, and why did the fiber move?" → `fiber_chip_passive_alignment.md`
(one interface, the attach chain); "what stress matrix qualifies this module, and what acceleration
factor applies?" → `siph_packaging_reliability.md` (whole package, qualification and lifetime).
Telcordia pass criteria are homed in `siph_packaging_reliability.md` Node 5; the other three point
there rather than carrying copies.

When a question spans two, load both and state which one owns the governing constraint. Each profile's
Cross-Domain Links section carries the same split from its own side.

## Where "Photonic Packaging & Co-Packaged Optics" lives (settled 2026-08-24)

There is no separate `cpo.md`, and there should not be one. **CPO is not a fifth profile — it is the
hardest operating point of the four profiles above plus `silicon_photonics_device_physics.md`.**
`siph_packaging_reliability.md` is its registered owner: that file explicitly fills the slot
`fiber_chip_passive_alignment.md` originally reserved as "Photonic Packaging & Co-Packaged Optics
(未建檔)". Load it whenever the subject is the co-packaged module as a whole.

`CPO` / `co-packaged optics` / `共封裝光學` appear as trigger keywords in **two** base rows, so the
keyword alone does not route. Split by what the question actually asks for:

| A CPO question about… | Load |
|---|---|
| Thermal architecture, ASIC-to-photonics gradient, TIM/lid/cold-plate, qualification matrix, acceleration model, KGD / burn-in / rework / serviceability | `siph_packaging_reliability.md` |
| The link budget and the devices inside it — laser output vs. $T_j$, ring resonance drift, modulator ER/$V_\pi$, PD responsivity and dark current | `silicon_photonics_device_physics.md` |
| Channel pitch vs. mode size (I/O density), edge-coupler architecture | `adiabatic_taper_ssc.md` |
| Fiber-array attach at the module edge — datum chain, cure drift, worst-channel IL | `fiber_chip_passive_alignment.md` |
| How the fiber-array groove itself is cut | `v_groove_fabrication.md` |

The common CPO question spans the first two ("the ASIC ran hotter and the link closed worse") —
load **both**. A hot ASIC simultaneously lowers laser power, drifts ring resonance and raises PD
dark current: one shared cause, three observables, not three independent problems.

*review-when:* a profile is added whose trigger list also contains `CPO` — add its row here in the
same change, or the keyword goes ambiguous again.

## Known keyword overlaps (lint exception register)

> **This table is the ONLY exception source for `tools/profile-lint.py`'s `KEYWORD-OVERLAP`
> check.** A pair listed here is a reviewed, intended overlap and is not reported; any other
> cross-domain overlap is reported as a WARN.
>
> It is maintained by hand, deliberately. The obvious alternative — deriving the exceptions by
> scanning the two disambiguation sections below for file names — was tried and rejected on
> 2026-08-26: that scan harvests `cpo.md` from the section whose entire purpose is to declare
> that `cpo.md` must never exist, and its two sections together cover 6 of the 10 base profiles,
> which would blanket-exempt 15 of the 45 base-pairs — precisely the pairs the eval suite's
> collision history is about. An instrument may only rule on what it can DETERMINE; prose cannot
> determine intent, so the exemption is declared as a property of the manifest instead of
> inferred from prose. Same-domain pairs (a base and its own sub-profile/reference) are exempt
> in code and are not listed here.
>
> Adding a row is a routing decision, not a lint fix: it asserts that both files loading together
> is the behaviour you want. If it is not, change the keyword instead.
>
> **The `Overlapping keyword` column holds the SHORT (contained) keyword — Row A's — never the
> containing one.** One row therefore covers every containing spelling at once: `thermal crosstalk`
> exempts the pair for both `ring-to-ring thermal crosstalk` and `microring thermal crosstalk`,
> and a second row naming a containing spelling would exempt nothing. Enforced, not remembered:
> `profile-lint.py` FAILs any row that suppresses nothing — i.e. where the two named rows have no
> overlap on that keyword at all. Naming a real keyword is not enough; a containing spelling is a
> real keyword of a real row and still silences nothing, which is exactly the mistake this catches.
> Keywords here are compared in the same NFKC-folded space as everything else, so the spelling
> in this column need not match the manifest's byte-for-byte.

| Row A | Row B | Overlapping keyword | Why the overlap is intended | Recorded |
|---|---|---|---|---|
| `silicon_photonics_device_physics.md` | `siph_packaging_reliability.md` | `CPO` | Settled 2026-08-24 — see § Where "Photonic Packaging & Co-Packaged Optics" lives. CPO questions routinely span both (a hot ASIC lowers laser power *and* is a thermal-architecture question); the keyword deliberately does not route on its own, the disambiguation table does. | 2026-08-24 |
| `silicon_photonics_device_physics.md` | `siph_packaging_reliability.md` | `co-packaged optics` | Same ruling as the `CPO` row — the spelled-out form must behave identically to the acronym. | 2026-08-24 |
| `silicon_photonics_device_physics.md` | `siph_packaging_reliability.md` | `silicon photonics` | `silicon photonics` is contained in `silicon photonics packaging`, so a packaging question also loads the device-physics profile. Accepted: the packaging profile's own scope is a silicon-photonics module, and the disambiguation table owns the split. Narrowing the device-physics row's anchor would cost far more recall than the extra load costs. | 2026-08-26 |
| `siph_packaging_reliability.md` | `fiber_chip_passive_alignment.md` | `Telcordia` | Both are photonic-packaging cluster members, and § Disambiguation states outright that "Telcordia pass criteria are homed in `siph_packaging_reliability.md` Node 5; the other three point there rather than carrying copies." A Telcordia question raised from the alignment side is *supposed* to reach the owner. | 2026-08-26 |
| `siph_packaging_reliability.md` | `fiber_chip_passive_alignment.md` | `GR-1221` | Same ruling as the `Telcordia` row — `GR-1221` is contained in the alignment row's `Telcordia GR-1221`. | 2026-08-26 |
| `siph_packaging_reliability.md` | `adhesives_polymer_reliability.md` | `HAST` | Cluster members. `HAST` is contained in the adhesives row's `HAST adhesion`; the stress standard is owned by the packaging profile while the adhesion observable is owned by the material profile, so both loading is the designed answer. Eval case 13 is exactly this shape and graded correct with both loaded. | 2026-08-26 |
| `adhesives_polymer_reliability.md` | `fiber_chip_passive_alignment.md` | `adhesive` | Cluster members; `adhesive` and `epoxy` are both contained in the alignment row's `epoxy/adhesive fiber attach`. The attach *process* is owned by the alignment profile and the *material* by the adhesives profile — § Disambiguation's last two rows are the split, and a question naming the attach adhesive legitimately touches both. | 2026-08-26 |
| `adhesives_polymer_reliability.md` | `fiber_chip_passive_alignment.md` | `epoxy` | Same ruling as the `adhesive` row. | 2026-08-26 |
| `siph_packaging_reliability.md` | `silicon_photonics_device_physics/ring_resonator_thermal_control.md` | `thermal crosstalk` | Same pair and same ruling as the three `silicon_photonics_device_physics.md` rows above — § Where "Photonic Packaging & Co-Packaged Optics" lives already splits this exact axis ("thermal architecture, ASIC-to-photonics gradient, TIM/lid/cold-plate" → packaging; "ring resonance drift" → device physics), and the two are one physical problem: `K_ij` is measured under a stated metal stack and package boundary condition, and the ring profile's own Node 2 requires that condition to travel with the number. Narrowing rejected: `thermal crosstalk` is exactly the phrase an asking user types (§ Maintenance), so the packaging profile would lose a core anchor to silence a load that is wanted. | 2026-08-26 |

*Scope note (corrected 2026-08-26):* the rows above are of two kinds. Five are **intra-cluster**
overlaps covered by the photonic-packaging cluster ruling in § Clusters ("Routing between members:
the two disambiguation sections below"). The four naming `silicon_photonics_device_physics` are
**not** — that profile is not a cluster member; they are covered instead by § Where "Photonic
Packaging & Co-Packaged Optics" lives, which rules that CPO questions span it and
`siph_packaging_reliability.md` and that the disambiguation table, not the keyword, does the
routing. Everything else stays undeclared and visible as a lint WARN until a human triages it.

*Triage record 2026-08-26 — the three overlaps this file previously listed as open are closed.*
`thermal crosstalk` was real and is declared above. The other two — `KOH` inside `KOH etch`, and
`depletion` inside `carrier depletion` — were **instrument false positives, not routing defects**,
and were removed by fixing the instrument rather than by declaring an intent nobody held: both
short keywords sit on a `sub-profile` row, Step 0 scans a sub-profile only when its parent domain
matched, and neither containing keyword reaches that parent's base row. `profile-lint.py` now
applies that reachability test (`routing_sim.rung1_reachability()`). Declaring them would have
recorded a false statement — that loading a topological-insulator process note on a
silicon-photonics V-groove question is wanted — in order to silence a warning.

## Maintenance

- SKILL.md must NOT hardcode domain file paths — it points here. When you add a domain
  file, add its row here in the same change; that is the only place the load list lives.
- `base` files stay lean (the 7-node profile = the domain's shared core). Specialized
  branches go in `sub-profile` rows, not the base file — see the decision tree.
- **A trigger keyword must be a word the *asking* user would type, not the answer.** Two rejected
  additions from the 2026-08-24 eval pass are worth not repeating: (a) `35.26°` alone was useless
  as a `fiber_chip_passive_alignment` trigger — a user who has made the wedge-half-angle error
  types `54.74°`, never the corrected value — and an English-only phrase does not fire on a
  Chinese prompt, so the Chinese form was added beside it; (b) generic packaging-timeline words
  (`封裝製程`, `封裝前後`, `封裝完之後`) were added to `siph_packaging_reliability` and then
  **reverted**: they matched three sibling profiles' core scenarios verbatim (a V-groove etch-angle
  question says `封裝製程`; a pre/post-attach IL question says `封裝前後`), so the row would have
  over-loaded across the whole cluster. That profile owns qualification and lifetime — a bare
  packaging-timeline word is not evidence of that scope. Where a cross-domain question cannot be
  caught by an honest keyword, let the two profiles' own Cross-Domain Links carry it; that is
  weaker routing but it does not manufacture false loads.
- **A spelling variant is not a broad keyword, and the trade runs the other way.** The rule above
  is about a keyword that means something *wider* than the row's scope. `Bi₂Se₃` beside `Bi2Se3`
  is the same term in a different codepoint: it cannot pull in a question the ASCII form would not
  have pulled in, so it cannot manufacture a false load — it can only recover a miss. User ruling
  2026-08-26: for this class a miss is the worse failure, because the consumer is an LLM that can
  discard an extra file but cannot read one that never loaded. **The fix is the matching rule, not
  the row** — matching is NFKC-folded (see § How Gate A uses this manifest), so list ONE spelling
  and let the fold cover the rest. Hand-listing variants is what the fold replaces: no such list is
  ever complete, and `profile-lint.py` reports a row carrying two spellings of one term as
  REDUNDANT-VARIANT.
- **Recall gaps are found by simulation, not by reading the row.** The 2026-08-26 triage found that
  `topological_insulator.md` had never listed `Bi2Se3` — the domain's single most typed material —
  so eval case 4's prompt matched no base row at all and the Bi₂Se₃ sub-profile was unreachable,
  while the eval's own recorded evidence claimed it loaded. Prose review had passed that row
  repeatedly. `tools/eval-impact.py`'s baseline is what surfaced it; run it after touching a row.

*review-when:* the Step-0 matching rule changes (case sensitivity, folding, or the two-level
scan). All three are stated in § How Gate A uses this manifest and implemented in
`tools/routing_sim.py`; if one moves and the other does not, both this section and the lint
calibration counts in `profile-lint.py`'s docstring are wrong.
