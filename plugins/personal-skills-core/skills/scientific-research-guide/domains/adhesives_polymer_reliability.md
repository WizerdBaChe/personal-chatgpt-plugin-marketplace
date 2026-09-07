---
xi: 1
what: "Adhesives & Polymer Reliability (粘合劑與高分子可靠性) — Adhesives & polymer reliability for photonic-packaging bonds: cure chemistry, Tg, moisture diffusion, hygrothermal damage, interfacial fracture/fatigue"
tags: [srg-domain, 領域框架, base]
aliases: ["adhesive", "epoxy", "粘合劑", "環氧", "degree of cure", "固化度", "UV cure", "UV-curable adhesive", "UV固化", "cationic epoxy", "dual-cure", "glass transition", "Tg", "moisture diffusion", "吸濕", "moisture uptake", "Fickian diffusion", "Dual-Fick", "Carter-Kibler", "hygrothermal ageing", "濕熱老化", "hydrolysis", "水解", "cohesive failure", "內聚破壞", "interfacial failure", "界面破壞", "mixed failure", "混合失效", "fatigue debonding", "疲勞脫黏", "lap shear", "refractive index vs cure", "refractive index vs moisture", "shadow-cure", "cure shrinkage", "adhesion force", "HAST adhesion"]
date: 2026-08-25
status: live
profile_type: base
parent: "-"
---
# Domain Profile: Adhesives & Polymer Reliability (粘合劑與高分子可靠性)

> Scope of applicability: The adhesive/epoxy material itself — cure chemistry, glass transition,
> moisture transport, hygrothermal damage, and interfacial fracture/fatigue — for photonic-packaging
> bonds (fiber–chip, fiber–V-groove, lid/cover attach, fiber-array epoxy). Covers what the material
> *is* and how it degrades; does not own the resulting fiber displacement or module-level
> qualification test matrix.
> Scientific nature: Polymer network formation (addition/cationic/radical polymerization), glass
> transition and segmental mobility, Fickian and non-Fickian moisture diffusion, hygro-mechanical
> stress, interfacial/cohesive fracture mechanics, conversion-dependent refractive index.
> Engineering nature: Optical-adhesive material selection, cure-schedule/process-window design,
> moisture and UV-cure reliability verification, failure-mode attribution (cohesive vs. interfacial
> vs. fatigue).
>
> **Domain boundary / cluster membership** — 5th member of the **photonic-packaging** sibling
> cluster (split tabulated in `_routing.md` § Clusters; the cluster was registered flat for four
> members on 2026-08-24 and a fifth member was added 2026-08-25 after re-running the same
> intersection test — see the Clusters table for the added row). This profile owns the **adhesive
> material and interface-reliability** problem: cure kinetics, Tg, moisture diffusion, hygrothermal
> damage, and cohesive/interfacial fracture. It does NOT own how the groove is cut
> (→ `v_groove_fabrication.md`), how the on-chip mode is expanded (→ `adiabatic_taper_ssc.md`), the
> resulting fiber displacement or datum-chain error budget (→ `fiber_chip_passive_alignment.md`), or
> the module-level qualification test matrix and acceleration models
> (→ `siph_packaging_reliability.md`). This profile fills the "Adhesives & Polymer Reliability
> (未建檔)" slot both of those two profiles reserved for it — see their Cross-Domain Links, now
> updated to point here.
>
> Profile metadata:
> - Profile ID: PHOT-ADPR-001
> - Profile version: 0.1 (first authoring, merged from two independently produced literature
>   packets — a first-pass research-materials draft and a deep+broad verification/expansion pass)
> - Last updated: 2026-08-25
> - Author(s) / Maintainer(s): User supplied two source packets (own literature-search sessions);
>   restructured, merged, and citation-consolidated into `scientific-research-guide/domains/` by
>   Claude (Sonnet 5)
>
> Primary source types:
> - Textbooks: (not yet incorporated — recommend a polymer-composites moisture-diffusion text or
>   Ferry-class viscoelasticity treatment for the Fickian/non-Fickian formalism behind Node 1/4)
> - Review articles: Gillet et al. 2022 (*Polymers*, moisture-diffusion parameter statistics);
>   Hassanpour & Karbhari 2024 (*Polymers*, moisture-uptake models and mechanisms)
> - Methods / standards papers: Hodgin 2004 (fiber-optic epoxy DSC/DMA/TMA/lap-shear); Chen et al.
>   2018 (UV/thermal dual-cure FT-IR); Lam, Uddin & Chan 2008 (adhesive-bonded fiber-array
>   reliability); Uddin et al. 2006 (UV-cure shadowing/delamination); Howard et al. 2010
>   (conversion-dependent refractive index); Lim et al. 2005 (moisture-vs-index at 1550 nm);
>   Jiang et al. 2025 (PLC splitter force-cycling fatigue)
> - Other: NTT-AT Keytech optical-adhesive FAQ (vendor process guidance)
>
> Notes for AI use:
> - Intended use: cross-checking what an optical adhesive's cure state, moisture history, and
>   interface condition actually prove, and preventing a material-level claim from being applied
>   outside the formulation/geometry/wavelength it was measured under.
> - **Validation status.** Both source packets came from literature-search sessions, not an opaque
>   AI-index research tool — every inline citation already carried an `[Author Year]` key and a
>   resolvable identifier at authoring time, so this profile did not have to re-resolve wrong
>   authors/titles the way three earlier profiles in this SKILL did. What the packets differ on is
>   **verification depth for two sources**: the first packet marked Lam2008 and Uddin2006 as
>   "pending primary source" (only a secondary mention existed); the second packet located and read
>   Lam2008's full text and Uddin2006's abstract directly. This profile carries the fuller,
>   confirmed version; see the Provenance note in §7b. Two further sources (Kim2003, RSC2026) remain
>   abstract/snippet-only and are flagged inline wherever cited — no numeric claim is drawn from them.
> - Optional external tool slot: if a local literature corpus or reference-manager MCP is available
>   (a Zotero MCP, `prism`, an Obsidian vault), prefer it for retrieving the full texts flagged
>   `[abstract]` in §7b (notably Kim2003 and Lim2005's full pages 339–344). Absent any such tool this
>   profile is fully usable from its own tables; §7b states exactly how much of each source was read.

---

## Citation convention (applies to Nodes 0–6)

Every inline citation is a human-resolvable `[Author Year]` key with a matching row in the
**Source Ledger (§7b)**; every quantitative claim states its conditions (material system, method,
wavelength, temperature, moisture state, sample geometry) in the same breath as the number. Full
rationale: `_template.md` "Citation convention" and `domain-expansion-guide.md` §3.2.

Claims marked `[synthesis]` are this profile's own derivation from cited premises, not something a
single source states.

---

## 0. Terminology & Chinese glosses

> Rationale: the same convention as the sibling packaging profiles' §0 — the profile body is
> English (machine-consumed domain reasoning), and this table is the single place the Chinese
> equivalents live. Preference order: 國家教育研究院樂詞網 official rendering > Taiwan
> polymer/photonics industry usage > literal translation. ⚠ marks a mainland/Japanese-derived
> rendering that is wrong for a Taiwan-context thesis.

| English term | 中文（臺灣） | Meaning in this domain | Translation note |
|---|---|---|---|
| Degree of cure | 固化度 | Fraction of reacted functional groups / relative residual exotherm | — |
| Glass transition temperature (Tg) | 玻璃轉移溫度 | Network transition from glassy to rubbery segmental mobility | — |
| Post-cure | 後固化 | Additional thermal treatment after initial (often UV) cure to raise conversion/Tg | — |
| Cationic polymerization | 陽離子聚合 | Epoxy cure mechanism; continues after irradiation via retained photoacid | — |
| Radical polymerization | 自由基聚合 | Acrylate cure mechanism; stops when radical generation ends; oxygen-inhibited at the surface | — |
| Shadow-cure / shadowing | 遮蔽固化不均 | Spatially nonuniform cure caused by geometric blocking of UV light | — |
| Moisture absorption / adsorption | 吸收／吸附 | Bulk penetration vs. surface accumulation of moisture | 兩者常被混用，需分開陳述 |
| Fickian diffusion | Fick 擴散 | Classical single-mechanism diffusion model | — |
| Non-Fickian / anomalous diffusion | 非 Fick／異常擴散 | Diffusion rate comparable to polymer segmental mobility; multi-stage or damage-coupled uptake | — |
| Dual-Fick / Carter–Kibler model | 雙階段 Fick／Carter–Kibler 模型 | Two-stage moisture uptake model (bound + free water, or relaxation-controlled) | — |
| Bound water / free water | 束縛水／自由水 | Polar-site-associated water vs. water in voids/microcracks, with different desorption kinetics | — |
| Hygroscopic expansion | 吸濕膨脹 | Dimensional/strain response to absorbed moisture | — |
| Hydrolysis | **水解** | Chemical scission of the polymer network by water | ⚠ 勿作「加水分解」（日文用法） |
| Cohesive failure | 內聚破壞 | Fracture within the bulk adhesive | — |
| Interfacial / adhesive failure | 界面破壞 | Fracture at the adhesive–substrate interface | — |
| Mixed failure | 混合失效 | Spatially co-occurring cohesive and interfacial failure | — |
| Fatigue debonding | 疲勞脫黏 | Progressive interface failure under cyclic load | — |
| Photoelastic effect | 彈光效應 | Stress-induced refractive-index/birefringence change | — |
| Return loss (RL) | 回波損耗 | Reflected optical power relative to incident, used here as an in-situ damage sensor | 與 `fiber_chip_passive_alignment.md` §0 一致 |
| Response-surface methodology | 反應曲面法 | Multi-axis DOE optimization method (e.g. index, conversion, adhesion, CTE jointly) | — |

---

## 1. Theoretical Framework Anchoring

### Core first principles

| Scale/problem type | Foundational theory | Core physical quantity |
|---|---|---|
| Cure & network formation | Addition/cationic polymerization of epoxy, or radical polymerization of acrylate; crosslink density sets segmental mobility | Degree of cure α, residual reaction exotherm, Tg |
| Moisture uptake & transport | 1-D Fickian diffusion in a plate as a default; non-Fickian/anomalous diffusion when segmental mobility, voids, or interfacial wicking compete with the diffusion rate itself [Hassanpour2024, §1–2] | Diffusion coefficient D, saturation uptake Msat, thickness h, uptake shape (single- vs. two-stage) |
| Hygrothermal damage | Water causes reversible plasticization and irreversible hydrolysis; swelling and material mismatch generate a compressive-near-surface / tensile-inward stress field, not a scalar offset [Hassanpour2024, §2] | ΔTg, hygro-strain ε = β(Mt−M0), interfacial/cohesive crack initiation |
| Optical coupling layer | n(λ, T, α, moisture) governs optical path; UV cure fields are spatially nonuniform (depth, angle, wavelength, cladding–adhesive index contrast) [Uddin2006, Abstract] | n(λ,T,α,cw), transmittance/fluorescence, α(x,y,z) |
| Interface fracture & fatigue | Cohesive vs. interfacial vs. mixed fracture; in-situ optical readout can be more sensitive than final mechanical fracture [Jiang2025, §3.1.2] | Cohesive/interfacial failure fraction, ΔIL(cycle), cycles-to-optical-failure vs. cycles-to-mechanical-failure |

In the Gillet et al. literature-statistics review, Fickian behavior can describe plate-sample M(t)
in terms of D, h, and Msat, but the authors emphasize that many epoxies show two-stage absorption
requiring Dual-Fick or Carter-Kibler-class models rather than a presumed single Fickian curve
[Gillet2022]. Hassanpour and Karbhari extend this: gravimetric "moisture uptake" can represent
competing mass gain (sorbed water) and mass loss (leached low-molecular-weight species), and uptake
and desorption need not be exact reverse processes [Hassanpour2024, §2].

### Inviolable physical constraints (the AI should warn the user here)

1. **Operating/verification temperature cannot be judged against dry-state Tg alone.** Water breaks
   secondary interchain bonds, lowers Tg, and causes swelling/stress concentration; the constraint
   is on the wet/aged Tg relative to the working and verification temperature, not the as-cured dry
   value [Gillet2022]. A coupon that returns near its dry mass after a bake is not automatically
   chemically undamaged, and a residual mass difference cannot alone prove hydrolysis — pair mass
   curves with spectroscopy, DMA/DSC, and failure-surface evidence [Hassanpour2024, §2].
2. **UV cure fields are spatially nonuniform; a nominal dose does not certify full-volume cure.**
   Radiant exposure H = I×t does not prove identical local polymerization because the sample has a
   depth-, angle-, and wavelength-dependent intensity field; cladding/adhesive refractive-index
   mismatch changes shadowing and thereby cure uniformity in V-groove fiber-array geometries
   [Uddin2006, Abstract]. Free-radical UV acrylates additionally suffer oxygen inhibition at
   exposed surfaces; UV-cationic epoxies avoid oxygen inhibition but commonly still need thermal
   post-cure for full adhesive performance [Chen2018].
3. **Low degree of cure is not disclosed by "initial fixture success."** A high-Tg two-part
   fiber-optic epoxy held at 80 °C/1 h showed 50.7% unreacted material by DSC residual-heat
   analysis, with lap-shear strength of 1280 psi versus 2533 psi at 120–150 °C/1 h — a specific,
   unnamed supplier's formulation under ASTM D1002-01 at 23±2 °C; not generalizable to all optical
   epoxies, but the *shape* of the trap (low-temperature/short-time cure looking adequate at t = 0)
   generalizes [Hodgin2004, p. 110, Table I].
4. **Moisture transport model choice is a diagnostic question, not a default.** Linear early M vs.
   √t with a stable plateau and no morphology change may justify a classical Fickian fit; two
   slopes, delayed secondary uptake, mass increase followed by loss at high temperature, or strongly
   direction-dependent uptake each point to a different mechanism (dual-mode/relaxation/bound-water,
   leaching/hydrolysis/degradation, or interfacial wicking respectively) and require a different
   model and different corroborating measurement [Hassanpour2024, §2, decision-tree table].
5. **Refractive index is a function of cure state, temperature, and moisture — never a single
   datasheet number.** Howard et al. measured a linear relation (r²=0.976) between degree of
   conversion and resin index in a dimethacrylate system, with index/filler matching occurring at
   ~58% conversion [Howard2010]; a vendor FAQ correctly requires stating wavelength for any quoted
   index (measurements listed at 403–1550 nm) [NTTATFAQ, Q18]. Neither of these transfers its
   *numeric* value to a telecom optical epoxy at 1310/1550 nm — only the *mechanism* transfers.
6. **A single shear-strength number cannot stand for interfacial reliability.** Fatigue-cycled PLC
   optical splitters showed optical-interconnection failure within the first few cycles while
   mechanical fracture occurred after ~6000 cycles under the same loading — the in-situ optical
   endpoint was more sensitive than the final mechanical break, and the fracture itself was mixed
   cohesive/interfacial [Jiang2025, §3.1.2, §3]. Failure-mode evidence (cohesive vs. interfacial vs.
   mixed, imaged) is required alongside any strength number.

> **Decision point (mandatory Tier 0 confirmation)**: when the user describes an optical adhesive or
> bonding-material question, the AI must confirm:
> "Is your adhesive (A) a **UV acrylate / free-radical** system, (B) a **UV-cationic epoxy or
> UV+thermal dual-cure epoxy**, or (C) a **pure thermal-cure epoxy**? These three differ in shadow-cure
> risk, shrinkage behavior, post-cure need, and moisture-reliability path." Also request: bond-line
> thickness, target wavelength/band, substrate materials (Si/SiO₂, glass, ceramic, metal, fiber
> coating), and the working/verification temperature and humidity — the answer changes which Node 4
> fitting method and which Node 5 metric apply.

---

## 2. Measurement Tool Inventory

### Cure, transition, and dimensional response

| Measurement target | Tool | Output information | Applicable conditions | Common misuse | Source [Key] |
|---|---|---|---|---|---|
| Residual reaction / degree of cure | DSC | Residual exotherm, α, Tg | Uncured and cured samples of the *same* formulation must share a consistent baseline/scan rate | Treating a single Tg reading as sufficient evidence of cure state without measuring residual exotherm | [Hodgin2004] |
| Viscoelastic transition | DMA | Storage/loss modulus, Tg window | Must state mode, frequency, ramp rate, specimen geometry | Comparing Tg values defined differently (DSC midpoint vs. DMA peak) as if commensurable | [Hodgin2004] |
| Thermal dimensional change | TMA | CTE, dimensional transition near Tg | Report the slope below and above Tg separately | Quoting one CTE with no statement of whether the Tg transition was crossed | [Hodgin2004] |
| UV/thermal conversion mapping | FT-IR / Raman (peak-specific) | Functional-group conversion by cure stage (e.g. acrylate C=C, maleimide C=C, epoxy) | Must specify peak assignment, baseline, light intensity, exposure time, post-bake step | Reporting "UV cured" with no shadow-region or residual-epoxy measurement | [Chen2018] |

### Moisture and hygrothermal response

| Measurement target | Tool | Output information | Applicable conditions | Common misuse | Source [Key] |
|---|---|---|---|---|---|
| Moisture uptake curve | Gravimetry / Karl Fischer titration | M(t), Msat, optionally water speciation (bound vs. free) | Must record RH or immersion medium, temperature, sample thickness, and dry-mass baseline | Reporting D or Msat without thickness/boundary conditions; treating uptake/desorption as exact mirror processes [Hassanpour2024, §2] | [Gillet2022], [Hassanpour2024] |
| Hygroscopic-strain field | Dimensional/strain gauge tracking during conditioning | ε(t), swelling-driven stress inference | Requires paired thermal-strain control to separate hygroscopic from thermal contribution | Assuming swelling is negligible without checking; β must be assigned per material/exposure, not assumed universal [Hassanpour2024, §2, Eq. 2] | [Hassanpour2024] |

### Optical quality and moisture–index coupling

| Measurement target | Tool | Output information | Applicable conditions | Common misuse | Source [Key] |
|---|---|---|---|---|---|
| Transmission/absorption, fluorescence, yellowing | UV-Vis / fluorescence spectroscopy | λ-specific transmission and color/cure-state change | Must state wavelength, cure/aging state; visible-light clarity ≠ telecom-band performance | Using visible transparency as evidence of 1310/1550 nm performance | [Hodgin2004] |
| Refractive index vs. conversion/temperature | Abbe-type refractometer | n(conversion, T) linear/slope relation | Room-temperature Abbe-line measurement; dental/visible-photopolymer system in the cited method | Extrapolating a visible-line dental-composite dn/dα or dn/dT to a telecom epoxy without re-measurement | [Howard2010] |
| Refractive index vs. moisture at telecom wavelength | Return-loss method via OTDR | n(t, moisture, T) at 1.55 µm during desorption | Method demonstrated at 120 °C on an acrylate-based optical adhesive; full paper not retrieved — treat reported slopes as abstract-level only | Citing the quoted slopes as design-ready values without confirming geometry/uncertainty from the original pages | [Lim2005] |
| Wavelength-resolved index (vendor) | Vendor Abbe/prism measurement across bands | n at 403–1550 nm | Vendor documentation, not peer-reviewed; correct requirement (state wavelength) but not independent performance evidence | Quoting a single vendor "n" with no wavelength | [NTTATFAQ] |

### Interface mechanical, fatigue, and fracture

| Measurement target | Tool | Output information | Applicable conditions | Common misuse | Source [Key] |
|---|---|---|---|---|---|
| Bond strength and failure mode | Tensile / lap-shear / clamped-shear + fracture microscopy | Strength (psi/N/mm²) plus cohesive/interfacial/mixed failure fraction | Must state substrate, surface condition, bond thickness, load rate, thermal/moisture preconditioning | Comparing strengths across different bond thickness or substrate as if the adhesive alone varied | [Hodgin2004], [Lam2008] |
| Fatigue debonding under cyclic load | Force/displacement cycling rig + in-situ IL/RL monitoring | ΔIL(cycle), cycles-to-optical-failure, cycles-to-mechanical-failure, fracture-surface classification | Requires in-situ optical readout synchronized with load; optical endpoint may precede mechanical fracture by orders of magnitude in cycle count | Using only end-of-test mechanical fracture as the failure criterion, missing the earlier optical failure [Jiang2025, §3.1.2] | [Jiang2025] |
| Cure-field uniformity (UV geometry) | Analytical ray tracing + FTIR/Raman conversion mapping | Local UV intensity/shadow map correlated with local conversion | Applies to V-groove/array geometries with adhesive–cladding index contrast | Assuming the cured region is uniform because the nominal dose was met | [Uddin2006] |

---

## 3. Standard Modeling Toolchain

```text
Formulation, equivalence ratio, light dose / thermal history
→ DSC / FT-IR / Raman
    → Output: degree of cure α, residual reaction heat, Tg, per-functional-group conversion
        ↓
Moisture and temperature exposure + gravimetry / Karl Fischer / TMA / DMA
    → Input: sample thickness h, RH or immersion medium, temperature, exposure time
    → Output: M(t), Msat, D (or non-Fickian parameters), wet Tg, dimensional change
        ↓
Optical measurement: Abbe refractometer / prism coupling / ellipsometry / OTDR return-loss method
    → Input: cure state α, temperature, moisture content cw, wavelength
    → Output: n(λ,T,α,cw), transmittance, fluorescence/yellowing
        ↓
Interface mechanical & fatigue test with in-situ optical readout
    → Output: failure location and mode (cohesive/interfacial/mixed), ΔIL(cycle) damage trace,
      strength retention after environmental stress
```

For thin bond lines, diffusion identification must include sample thickness h and the exposed
boundary condition in the fit. Gillet et al. treat D and h as jointly controlling the time term in
the Fickian form, using Msat, tsat, and D as the basic parameters over 90 papers/448 datasets
restricted to reversible gravimetric uptake with saturation or Fick-derived two-stage behavior — the
compilation should not be applied directly to already-hydrolyzed, continuously mass-losing, or
plateau-free bond lines [Gillet2022, §1–2].

---

## 4. Domain-Specific Fitting Methods

| Method | Applicable question | Applicable conditions | Common error | Correct approach | Source [Key] |
|---|---|---|---|---|---|
| Fickian plate-diffusion fit | Extract D, Msat from a monotonic, near-single-stage uptake curve | Known sample thickness and exposed-face geometry; curve must show an identifiable plateau | ⚠️ Treating any moisture curve as Fickian by default | Check for two-stage or plateau-free shape first; switch to Dual-Fick/Carter-Kibler if present | [Gillet2022], [Hassanpour2024] |
| Dual-Fick / Carter-Kibler / Langmuir-type fit | Model two-stage uptake, bound-water, or relaxation-controlled sorption | Time window must cover both early and late uptake stages | ⚠️ Claiming mechanism from curve-fit goodness alone (e.g. a well-fitting polynomial) | Use a model with physically interpretable parameters and report identifiability, not just fit quality | [Gillet2022], [Hassanpour2024] |
| DSC residual-exotherm degree of cure | Determine cure completeness / post-cure need | Requires a fully-uncured baseline sample of the identical formulation | ⚠️ Substituting oven-set temperature for measured cure degree | Compute α = 1 − ΔH_res/ΔH_uncured (or equivalent) per formulation and process window | [Hodgin2004] |
| UV+thermal dual-cure FT-IR conversion tracking | Separate UV-stage and thermal-stage conversion per functional group | Must specify peak, baseline, irradiance, exposure time, post-bake schedule | ⚠️ Reporting only "UV cured" without shadow-region or residual-epoxy conversion | Track acrylate/maleimide/epoxy (or system-specific) peaks separately across the full cure history | [Chen2018] |
| Conversion–index linear regression | Relate refractive index to degree of conversion in a specific formulation | Same resin system, same wavelength/measurement method, multiple conversion points | ⚠️ Applying a fitted slope from one (e.g. dental, visible-line) resin system to a different formulation or wavelength | Re-measure n vs. α for the specific formulation and wavelength of interest; use the cited method only as a mechanism template | [Howard2010] |
| Moisture–index correlation (return-loss/OTDR) | Relate optical index change to moisture content at a telecom wavelength | Requires a resolvable OTDR return-loss trace during desorption/absorption; specimen geometry stated | ⚠️ Quoting the reported slopes as generally valid before the exact index-extraction model, geometry, and uncertainty are confirmed from the full paper | Reproduce the method on the formulation of interest; treat published slopes as a starting hypothesis, not a design value | [Lim2005] |
| Arrhenius / Peck humid-aging extrapolation | Compare degradation rate across temperature/humidity for one mechanism | Must first confirm the failure mode and material state have not changed between conditions | ⚠️ Extrapolating HAST/PCT to field life without confirming mechanism identity (this is the same trap `siph_packaging_reliability.md` Node 1 constraint 1 states for the module level) | Use multi-temperature/humidity data plus fracture/chemistry evidence to confirm mechanism consistency before fitting; defer the model-selection logic itself to `siph_packaging_reliability.md` Node 4 | ⚠ No standardized acceleration factor for photonic-packaging adhesive bonds specifically was found in either source packet — treat any quoted factor as formulation- and geometry-specific until confirmed |

---

## 5. Domain-Specific Quality Metrics

| Metric | Abbreviation | Physical meaning | Typical value range | Conditions (material/method/wavelength/temp…) | Source [Key] |
|---|---|---|---|---|---|
| Degree of cure | α | Fraction of reacted groups / relative residual exotherm | No universal threshold | High-Tg two-part fiber-optic epoxy (unnamed supplier), DSC residual heat: 49.3% cured at 80 °C/1 h; 99.8% cured at 120 °C/2 h | [Hodgin2004, p. 110, Table I] |
| Glass transition temperature | Tg | Onset of high segmental-mobility regime | Formulation-specific | Same epoxy: 87 °C at 80 °C/1 h cure, 110 °C at 120 °C/1 h, 119.4 °C at 150 °C/1 h | [Hodgin2004, p. 110, Table I] |
| Equilibrium moisture uptake | Msat | Relative mass gain after hygrothermal exposure | Highly formulation-dependent | 448 epoxy/epoxy-composite datasets restricted to reversible, Fickian/two-stage uptake: 75% of individuals below 4% uptake; material/RH/temperature not unified across the set — a database descriptor, not a design value | [Gillet2022, §3.1] |
| Diffusion coefficient | D | Moisture-transport rate parameter | No universal threshold | DGEBA-based subgroup (217 entries, heterogeneous source conditions), median 5.23×10⁻⁷ mm²/s; not extrapolable to a specific thin optical bond line | [Gillet2022, §3.2, Table 2] |
| Lap-shear strength | LSS | Apparent shear strength of an overlap joint | No universal threshold | Unnamed two-part high-Tg fiber-optic epoxy, ASTM D1002-01, 23±2 °C: 1280 / 1533 / 2533 psi after 80 °C/1 h, 120 °C/1 h, 150 °C/1 h cure respectively | [Hodgin2004, p. 111, Table II] |
| CTE and Tg (fiber-array adhesives) | — | Thermal-mechanical mismatch drivers vs. a 0.55 ppm/°C quartz/silica package | Formulation-specific | Adhesive I: CTE 55 ppm/°C, Tg 145 °C; Adhesive II: CTE 10.7 ppm/°C, Tg 129 °C — 16-fiber quartz V-groove/lid package | [Lam2008, §2.1.1, Table 1] |
| Adhesion force before/after HAST | — | Quartz-slide shear adhesion, moisture-stress degradation | No universal threshold | Adhesive II, 200 µm bond line: 14.28 N/mm² before HAST; 4.28 N/mm² after 121 °C/100% RH/2 atm/8 h HAST (~70% decrease) | [Lam2008, §2.3, §3.3] |
| Plasma-treated adhesion (confound-control datum) | — | Surface-preparation effect on post-HAST adhesion | Retained for failure attribution only — process ownership is `v_groove_fabrication.md`/`fiber_chip_passive_alignment.md`, not this profile | Highest post-HAST value in the screening table: 5.82 N/mm², Ar+O₂ plasma, 400 mTorr, 400 W RF, 30 min; AFM roughening 47.2 Å for that condition | [Lam2008, §3.3, Table 2] |
| Insertion-loss/delta-core-pitch after thermal shock | — | Fiber-array optical and geometric degradation | Application-specific | 0 ↔ 100 °C, 15 cycles, 5 min dwell, <10 s transfer (Telcordia GR-1221-CORE-style); delta core pitch <0.5 µm before, up to 0.6 µm after; n=11 (LTPD 20%); higher-CTE Adhesive I degraded more at 1.55 µm (<±0.05 dB accuracy) | [Lam2008, §2.2.1, §3.1.1–3.1.2] |
| Conversion-dependent refractive index slope | dn/dα | Sensitivity of index to cure conversion | Mechanism-transfer only, not a numeric transfer | Bis-GMA/TEGDMA 70/30 dimethacrylate, r²=0.976; index/filler match at ~58% conversion; n_D²² = 1.5216±0.0003 unfilled; dn/dT = −2.66×10⁻⁴ °C⁻¹ (73% conversion) vs. −4.33×10⁻⁴ °C⁻¹ (uncured monomer), 20–65 °C | [Howard2010] |
| Moisture-dependent refractive-index slope (telecom) | dn/dcw | Index sensitivity to moisture content at 1.55 µm | ⚠ Abstract-level only, non-transferable numerically without the full paper | Acrylate-based optical adhesive, OTDR return-loss method, 120 °C: ≈−1×10⁻⁴ per % moisture at low uptake; ≈−7×10⁻⁶ per % moisture above 10% dry-weight uptake | [Lim2005] |
| Adhesive elastic modulus (fatigue-tested PLC bond) | E | Stiffness of the UV-acrylate bond in a real device | Device-specific | 20 MPa, cured 10 mW/cm² for 5 min; cycles-to-optical-failure: first few cycles at Fmax=10 N; cycles-to-mechanical-failure: ~6000 | [Jiang2025, §2.1–2.2, Table 1; §3.1.2] |
| Fluorinated UV-adhesive multi-axis optimization | — | Joint index/conversion/wet-adhesion/CTE optimization space | ⚠ No numeric value extracted — abstract/snippet access only | Response-surface methodology over fluorinated epoxy and fluorinated epoxy-acrylate systems; full article needed before quoting any number | [Kim2003] |

---

## 6. Common Assumption Pitfalls

| Pitfall | Trigger condition | How to recognize it | Correct approach | Source [Key] |
|---|---|---|---|---|
| "The moisture curve must be Fickian — just fit one D" | User says "用 Fick 算這支膠的水氣擴散" or asks to fit a single diffusion coefficient without checking curve shape | M–√t plot has two slopes, no plateau, or loses mass after an initial gain | Check for a stable plateau and single-stage shape first; switch to Dual-Fick/Carter-Kibler, and treat hydrolysis/leaching as a separate mechanism when mass later decreases | [Gillet2022, §1–2], [Hassanpour2024, §2] |
| "UV cured for N seconds = fully cured through the whole volume" | User plans to move straight from a short UV exposure into reliability testing | Shadowed regions (fixture, metal, thick bond line, opaque substrate) exist and residual functional groups were never measured there | Measure FTIR/DSC separately in exposed and shadowed regions; for UV-cationic or dual-cure systems, evaluate whether thermal post-cure is needed for full performance | [Uddin2006, Abstract], [Chen2018, §2–3] |
| "Refractive-index matching only needs the datasheet room-temperature n" | User says "兩個材料室溫 n 一樣就不會有光學問題" with no wavelength, temperature, or moisture state stated | No wavelength/temperature/cure-state/moisture condition is attached to the quoted n | Build an n(λ,T,α,moisture) matrix for the actual formulation; a vendor number without a stated wavelength is not usable evidence [NTTATFAQ, Q18] | [Howard2010], [Lim2005], [NTTATFAQ] |
| "Higher post-bake temperature is always more reliable" | User proposes raising post-cure temperature "as high as possible" with no upper-bound evidence | No TGA/degradation, yellowing, shrinkage, or substrate-tolerance data accompanies the proposal | Bound the cure window using residual exotherm, Tg, optical loss/yellowing, shrinkage, and interfacial strength together; verify the substrate's own thermal tolerance separately | [Hodgin2004], [Chen2018] |
| "Dry-state Tg above the working temperature is sufficient" | User states "Tg 比工作溫度高就已足夠" with no wet/aged data | No post-hygrothermal DMA/TMA or strength-retention measurement exists | Add wet/aged Tg, swelling, hydrolysis, and interfacial-crack evidence; dry Tg alone does not bound hygrothermal performance | [Gillet2022, §1] |
| "One lap-shear number proves interfacial reliability" | User reports a single shear-strength value as the reliability conclusion, with no failure-mode classification | No cohesive/interfacial/mixed fraction, no fracture image, no environmental precondition stated | Report failure-mode fraction with imaging, bond thickness, and pre/post-environmental strength retention, not a bare strength number | [Hodgin2004], [Lam2008] |
| "A nominal UV dose (I×t) certifies uniform cure across the geometry" | User quotes total radiant exposure (mJ/cm²) as the cure-completeness metric for a V-groove or shadowed geometry | No ray-tracing, shadow-map, or spatially resolved FTIR/Raman conversion evidence is provided | Model or measure the local intensity field (depth, angle, wavelength, cladding/adhesive index contrast); identical nominal dose does not guarantee identical local polymerization | [Uddin2006, Abstract] |
| "Static shear strength predicts fatigue/cyclic life" | User extrapolates a single static lap-shear or pull-test result to cyclic/fatigue service life | No cycle-resolved optical or mechanical data exists | Use cycle-resolved in-situ IL/RL alongside mechanical cycling; optical failure can precede mechanical fracture by orders of magnitude in cycle count, and the failure is often mixed cohesive/interfacial | [Jiang2025, §3, §5.3] |
| "Mass recovery after bake proves no chemical damage; residual mass loss proves hydrolysis" | User uses a simple before/after mass comparison as the sole hygrothermal-damage verdict | No FTIR/Raman, TGA/DSC, or dry–wet–redry mechanical data accompanies the mass curve | Pair mass curves with spectroscopy and mechanical retention data; competing sorption/leaching processes make mass alone ambiguous in either direction | [Hassanpour2024, §2] |
| "Lower CTE is always the better adhesive choice" | User selects an adhesive purely to minimize CTE mismatch against the substrate | No modulus, strain-to-failure, or fracture-toughness comparison accompanies the CTE argument | Treat CTE, modulus, wet Tg, cure shrinkage, fracture toughness, and optical response as a joint selection criterion — a lower-CTE adhesive can have worse strain-to-failure and shift the failure mode | [Lam2008, Table 1, §3.1] |
| "A filler that fixes CTE/modulus is a free improvement" | User adds filler to adjust CTE or modulus without checking optical scattering | No haze/scatter or insertion-loss-at-wavelength measurement after the filler change | Filler size distribution, aggregation, and resin–filler Δn can increase scattering even when the matrix conversion/index match is otherwise controlled; qualify with particle characterization and wavelength-specific loss mapping | [Howard2010], §6.3 (RSC2026 boundary caution) |

---

## 7a. Literature Anchors

| Type | Reference | Why it matters |
|---|---|---|
| Review | Gillet, C.; Tamssaouet, F.; Hassoune-Rhabbour, B.; Tchalla, T.; Nassiet, V. (2022). "Parameters Influencing Moisture Diffusion in Epoxy-Based Materials during Hygrothermal Ageing—A Review by Statistical Analysis." *Polymers*, 14(14), 2832. | Statistical, cross-literature grounding for Fickian/Dual-Fick/Carter-Kibler model choice and plausible Msat/D ranges |
| Review | Hassanpour, B.; Karbhari, V. M. (2024). "Characteristics and Models of Moisture Uptake in Fiber-Reinforced Composites: A Topical Review." *Polymers*, 16(16), 2265. | The mechanistic bridge from "moisture uptake" to bound/free water, non-Fickian regimes, and hygro-mechanical stress — the source of this profile's clearest decision tree |
| Methods/application paper | Hodgin, M. J. (2004). "Epoxies for OptoElectronic Packaging; Applications and Material Properties." *Journal of Microelectronics and Electronic Packaging*, 1(2), 108–116. | Direct, condition-stated DSC/TMA/DMA/lap-shear data on a real fiber-optic epoxy, and the profile's clearest low-degree-of-cure trap |
| Primary study | Lam, K. W.; Uddin, M. A.; Chan, H. P. (2008). "Reliability of Adhesive Bonded Optical Fiber Array for Photonic Packaging." *Journal of Optoelectronics and Advanced Materials*, 10(10), 2539–2546. | The most directly photonic-packaging-relevant quantitative source: CTE/Tg, thermal-shock core-pitch drift, HAST adhesion-force degradation, plasma-treatment confound data |
| Primary study | Uddin, M. A.; Chan, H. P.; Tsun, T. O.; Chan, Y. C. (2006). "Uneven Curing Induced Interfacial Delamination of UV Adhesive-Bonded Fiber Array in V-Groove for Photonic Packaging." *Journal of Lightwave Technology*, 24(3), 1342–1349. | Establishes the cure-field/optical-propagation mechanism linking adhesive index selection to mechanical delamination — the profile's clearest UV-shadowing constraint |

---

## 7b. Source Ledger

> Legend — **Access tag**: `[full]` full text read · `[partial]` preview/excerpt/supplementary only ·
> `[abstract]` abstract/metadata only · `[secondary]` known only via another source citing it ·
> `[vendor]` manufacturer page.
> **Verification status**: ✅ Confirmed against the primary source · `~` Approximate (general claim
> corroborated, exact figure not independently pinned) · ⚠ Unconfirmed · ❌ Withdrawn.
> **Verified (date)** (`domain-expansion-guide.md` §3.7): when this row's claim was last checked
> against the primary source — not the source's own publication year. All rows were checked
> 2026-08-25 during this profile's authoring/merge pass, then re-verified 2026-08-26 in a
> dedicated currency pass (full audit trail:
> `reports/2026-08-26-adhesives-polymer-reliability-source-currency-check.md`) — that pass found
> and corrected a wrong author on [Lim2005] and upgraded [Kim2003]'s bibliographic identity from
> incomplete to fully resolved. `review-when:` notes flag rows whose currency depends on a
> specific future event, not a generic "re-check later."

| Key | Full citation | Identifier | Access tag | Verification status | Verified (date) | Locator (section/table/fig/page) | Used in (Node/row) |
|---|---|---|---|---|---|---|---|
| [Gillet2022] | Gillet, C.; Tamssaouet, F.; Hassoune-Rhabbour, B.; Tchalla, T.; Nassiet, V. (2022). "Parameters Influencing Moisture Diffusion in Epoxy-Based Materials during Hygrothermal Ageing—A Review by Statistical Analysis." *Polymers* 14(14): 2832. | DOI 10.3390/polym14142832 | [full] | ✅ Confirmed; re-checked 2026-08-26, no retraction/erratum found, still actively cited by 2024+ literature | 2026-08-26 | Abstract; §1; §2 eqs. (1)–(6), Table 1; §3.1; §3.2 Table 2 | 0, 1, 3, 4, 5, 6, 7a |
| [Hodgin2004] | Hodgin, M. J. (2004). "Epoxies for OptoElectronic Packaging; Applications and Material Properties." *Journal of Microelectronics and Electronic Packaging* 1(2): 108–116. | DOI 10.4071/1551-4897-1.2.108; full text: imapsjmep.org/article/39822 | [full] | ✅ Confirmed | 2026-08-26 — light re-confirmation only (not re-read in full this pass) | pp. 109–111; Table I (p. 110); Table II (p. 111); pp. 113–114, Tables VI–VII | 1, 2, 4, 5, 6, 7a |
| [Chen2018] | Chen, C.; Li, B.; Wang, C.; Iwasaki, S.; Kanari, M.; Lu, D. (2018). "UV and Thermal Cure Epoxy Adhesives." In *Epoxy Adhesives*, IntechOpen. | DOI 10.5772/intechopen.81402 | [full] | ✅ Confirmed | 2026-08-26 — light re-confirmation only (not re-read in full this pass) | Abstract; §1; §2; §3 Table 1; §4 Table 2; §5 | 0, 1, 2, 4, 6 |
| [Lam2008] | Lam, K. W.; Uddin, M. A.; Chan, H. P. (2008). "Reliability of Adhesive Bonded Optical Fiber Array for Photonic Packaging." *Journal of Optoelectronics and Advanced Materials* 10(10): 2539–2546. | joam.inoe.ro/articles/reliability-of-adhesive-bonded-optical-fiber-array-for-photonic-packaging/fulltext | [full] | ✅ Confirmed — full text read directly (upgraded from "pending primary source" in the first source packet; see Provenance note below); re-checked 2026-08-26, no retraction/correction found via CityUHK Scholars + joam.inoe.ro | 2026-08-26 | §§1–4; Table 1; Table 2; pp. 2540–2546 | 1, 5, 6, 7a |
| [Uddin2006] | Uddin, M. A.; Chan, H. P.; Tsun, T. O.; Chan, Y. C. (2006). "Uneven Curing Induced Interfacial Delamination of UV Adhesive-Bonded Fiber Array in V-Groove for Photonic Packaging." *Journal of Lightwave Technology* 24(3): 1342–1349. | DOI 10.1109/JLT.2005.863329 | [abstract] | ✅ Confirmed at abstract level — read directly (upgraded from "unconfirmed, book title/venue incomplete" in the first source packet; see Provenance note below). Re-fetched verbatim from opg.optica.org 2026-08-26: still no figure-specific or numerical Δn threshold in the abstract — confirmed absent, not merely unread | 2026-08-26 — `review-when:` full text becomes accessible (would let the Δn threshold be extracted) | Abstract | 1, 2, 6, 7a |
| [Hassanpour2024] | Hassanpour, B.; Karbhari, V. M. (2024). "Characteristics and Models of Moisture Uptake in Fiber-Reinforced Composites: A Topical Review." *Polymers* 16(16): 2265. | DOI 10.3390/polym16162265 | [full] | ✅ Confirmed | 2026-08-26 — light re-confirmation only (not re-read in full this pass) | Abstract; §§1–3; Table 1; Eq. (2) | 0, 1, 4, 6, 7a |
| [Howard2010] | Howard, B.; Wilson, N. D.; Newman, S. M.; Pfeifer, C. S.; Stansbury, J. W. (2010). "Relationships between Conversion, Temperature and Optical Properties during Composite Photopolymerization." *Acta Biomaterialia* 6(6): 2053–2059. | DOI 10.1016/j.actbio.2009.11.006 | [full] | ✅ Confirmed. Dental Bis-GMA/TEGDMA/barium-glass system — mechanism-only analogy for photonics; numeric values are non-transferable to a telecom epoxy | 2026-08-26 — light re-confirmation only (not re-read in full this pass) | Abstract; Materials and Methods; Results and Discussion, Fig. 2, Table 1 | 1, 2, 4, 5, 6 |
| [Lim2005] | Lim, S.; Priyadarshi, A.; Rajoo, R.; Wong, E. H.; Mhaisalkar, S. G.; Kripesh, V. (2005). "Methodology to Study the Effect of Moisture on Refractive Index of Optical Adhesive." *Proceedings of SPIE* 5852: 339–344. | DOI 10.1117/12.621989 | [abstract] | ✅ Title/DOI verified; author list corrected 2026-08-26 (Crossref API returned six authors — the fifth author is Mhaisalkar, not "Gupta," and a sixth author, Kripesh, was previously missing entirely; see the currency-check report). ⚠ Full paper (pp. 339–344) still not retrieved — quoted slopes and method remain abstract-level only | 2026-08-26 — `review-when:` pp. 339–344 obtained (would upgrade the quoted slopes from abstract-level to full-text-verified) | SPIE metadata/abstract | 2, 4, 5 |
| [NTTATFAQ] | NTT-AT Keytech Corporation. "FAQ about Optical Adhesives." n.d. | keytech.ntt-at.com/en/adhesive/faq_ad.html | [vendor] | ✅ Page directly read; re-fetched 2026-08-26, still live, all three previously-quoted statements (UV-cationic post-irradiation cure, 403–1550 nm index measurement, 2–3 °C/min post-cure ramp) verified word-for-word unchanged. Vendor process guidance only, no independent performance endorsement | 2026-08-26 — `review-when:` vendor page content changes (undated vendor FAQs are edited without notice) | Q8–Q20 | 1, 2, 6 |
| [Jiang2025] | Jiang, L.; Zheng, Y.; Zeng, K.; Tang, X. (2025). "Response Analysis of PLC Optical Splitters Under Force Cyclic Loading." *Micromachines* 16(4): 449. | DOI 10.3390/mi16040449 | [full] | ✅ Confirmed | 2026-08-26 — light re-confirmation only (not re-read in full this pass) | Abstract; §§2–4; Table 1; Fig. 5 discussion | 1, 2, 5, 6, 7a |
| [Kim2003] | Kim, H. K.; Kim, J. G.; Cho, J. D.; Hong, J. W. (2003). "Optimization and Characterization of UV-Curable Adhesives for Optical Communications by Response Surface Methodology." *Polymer Testing* 22(8): 899–906. | DOI 10.1016/S0142-9418(03)00038-2 | [abstract/partial] | Bibliographic identity fully resolved 2026-08-26 via ScienceDirect + Crossref (upgraded from an incomplete author list/volume/pages/DOI). ⚠ Content remains unread — a search-engine AI summary surfaced a specific numeric claim (UCM/colloidal-silica optimum weight fractions) that was NOT independently verified against the actual text and is deliberately NOT entered here (see the currency-check report's rationale); no numeric claim is drawn from this source | 2026-08-26 — `review-when:` full article text obtained (would allow the actual optimization results to be extracted) | Page title, ScienceDirect/Crossref metadata | 5, 6 |
| [RSC2026] | Koh, K.; Sohn, H. (2026). "Thermally Stable Network-Structured Polysiloxane Hybrimers with High Refractive Index for Optical Applications." *RSC Advances*. | pubs.rsc.org/ra/article/16/3/2384-2392/908731 | [abstract] | ⚠ Abstract-level LED-encapsulation evidence only (450/520/635 nm, different device context); author names added 2026-08-26. Retained solely as a material-space boundary caution, not a performance benchmark | 2026-08-26 | Abstract | 6 (boundary reference only) |

### Provenance note (merge of two source packets, 2026-08-25)

This profile merges a first-pass "research-materials" packet with a second "deep + broad" literature
packet produced independently. Both packets used human-resolvable `[Author Year]` citations from the
start — neither carried the opaque AI-index defect documented in `domain-expansion-guide.md` §3.2 —
so no author/title corrections were required. The one substantive change between the two packets:

| First-packet status | Second-packet finding | Disposition here |
|---|---|---|
| Lam2008 listed as "Pending primary source... not directly read in this task" | Full text located and read (§§1–4, Table 1, Table 2) | Upgraded to `[full]` ✅; quantitative CTE/Tg/adhesion-force/thermal-shock data now populate Nodes 1 and 5 |
| Uddin2006 listed as "user-provided lead only... title/venue/authors beyond surname/year unconfirmed" | Full bibliographic record identified and abstract read directly | Upgraded to `[abstract]` ✅; the UV-shadowing/index-contrast mechanism now anchors Node 1 constraint 2 and a Node 6 pitfall |

No claim from either packet was withdrawn; the second packet's five additional sources
(Hassanpour2024, Howard2010, Lim2005, NTTATFAQ, Jiang2025) and two boundary-only sources (Kim2003,
RSC2026) were added net-new.

### Currency-check addendum (2026-08-26)

A dedicated verification pass (`literature-search-extract` Mode 2, full audit trail in
`reports/2026-08-26-adhesives-polymer-reliability-source-currency-check.md`) re-checked all 12
ledger entries against their primary sources: no retraction/erratum was found for any of them, and
no 2024–2026 paper was found that supersedes a core claim. Two corrections came out of that pass —

| Row | Error found | Correction |
|---|---|---|
| [Lim2005] | Fifth author was misrecorded as "Gupta, S. G."; a sixth author (Kripesh, V.) was missing entirely | Crossref API confirmed the correct six-author list: Lim, Priyadarshi, Rajoo, Wong, **Mhaisalkar**, Kripesh |
| [Kim2003] | Author list, volume, pages, and DOI were all incomplete/unresolved | ScienceDirect + Crossref resolved the full identity: Kim, Kim, Cho, Hong; *Polymer Testing* 22(8):899–906; DOI 10.1016/S0142-9418(03)00038-2 |

A search-engine AI summary encountered during the Kim2003 re-check additionally offered a specific
numeric claim (UCM/colloidal-silica optimum weight fractions) with no quotable locator in the
actual text — this was deliberately **not** entered into the ledger, per the same
retrieval-layer-can-fabricate-a-bridge caution already documented in
`fiber_chip_passive_alignment.md`'s own provenance log.

---

## Cross-Domain Links

### Closest Related Domain Profiles

| Profile name | Overlap dimensions | Typical use split |
|---|---|---|
| `fiber_chip_passive_alignment.md` (Fiber-to-Chip Passive Alignment & Attachment) | first principles (cure shrinkage, viscoelasticity, CTE mismatch), quality metrics (ΔIL_cure) | Use **this** profile for what the adhesive *is* and how it degrades — cure state, Tg, moisture transport, hygrothermal damage, cohesive/interfacial failure mode. Use **that** profile for what the adhesive *does to the fiber's position* — dispense architecture, ΔIL_cure attribution, datum-chain error budget. That profile's "adhesive is a load-bearing functional element" constraint is this profile's premise |
| `siph_packaging_reliability.md` (Silicon Photonics Packaging & Reliability) | first principles (hygrothermal/CTE-mismatch mechanics), measurement tools (qualification chambers, HAST/PCT/thermal-shock), quality metrics (ΔIL, acceleration models) | Use **this** profile for material-level cure/moisture/fracture evidence and for whether a stress condition is even naming the adhesive's real failure mechanism. Use **that** profile for the module-level test matrix, standard designations (JEDEC/Telcordia), and acceleration-model selection (Arrhenius/Coffin-Manson/Peck/Weibull) — this profile does not repeat that model-selection logic, only flags where an adhesive result must confirm mechanism identity before it feeds an AF calculation |
| `v_groove_fabrication.md` (V-Groove Fabrication) | measurement tools (surface/interface metrology), application targets (fiber-array bonds) | Surface preparation and cleaning process ownership stays with the fabrication/attachment profiles; this profile retains plasma-treatment adhesion data only as a confound-control datum for failure attribution, not as a process recommendation |

### Boundary & ownership notes

- This profile fills the "Adhesives & Polymer Reliability" slot that `fiber_chip_passive_alignment.md`
  and `siph_packaging_reliability.md` both reserved as "未建檔" — their Cross-Domain Links now point
  here instead of to a placeholder.
- Cross-profile numbers are referenced, not copied: the fiber-array attach process (dispense
  architecture, ΔIL_cure) lives in `fiber_chip_passive_alignment.md`; the qualification test matrix
  and acceleration models live in `siph_packaging_reliability.md`. This profile owns the material
  chemistry, cure state, moisture transport, and fracture-mode evidence that those two profiles cite
  but do not re-derive.
- Surface-preparation process ownership (plasma cleaning, pre-bond cleanliness) is NOT claimed here:
  the Lam2008 plasma-treatment adhesion data (Node 5) is retained strictly as a confound-control
  datum, because an apparent "resin reliability" result can actually be a contamination-controlled
  interface failure if surface condition was not recorded.

---

## Cross-Domain Conflict Notes

| Issue / constraint | Other profile(s) involved | Potential conflict | AI confirmation question |
|---|---|---|---|
| Raising post-cure Tg vs. optical/positional drift | `fiber_chip_passive_alignment.md` | Higher cure temperature or longer post-bake can raise degree of cure and Tg, but the accompanying shrinkage/CTE mismatch can worsen fiber-position drift — this profile does not predict displacement | "Is your primary acceptance criterion the adhesive's own cure/moisture state, or the resulting fiber position? A cure schedule optimal for one can be suboptimal for the other. What is the acceptable cure-temperature ceiling given the substrate and fixture?" |
| UV cure-field uniformity vs. process throughput | `fiber_chip_passive_alignment.md`, `v_groove_fabrication.md` | A fast, low-dose UV tack that satisfies assembly throughput may leave shadowed regions under-cured, deferring the reliability problem to the field | "Does this bond geometry have shadowed regions (fixture, metal cladding, thick bond line)? If so, has conversion been measured there specifically, not just at the exposed face?" |
| Time-zero adhesive selection vs. end-of-life adhesive behavior | `siph_packaging_reliability.md`, `fiber_chip_passive_alignment.md` | An adhesive chosen for minimum cure shrinkage (best t=0 IL) may have worse wet-Tg, creep, or hydrolysis behavior (worst end-of-life ΔIL) — this is the same tension both sibling profiles already flag from their own side | "Is the acceptance criterion initial IL/positional accuracy, or IL after the full qualification sequence? The adhesive choice can invert between the two, and this profile's Node 5 CTE/adhesion-force data should be read against whichever criterion governs" |
| Acceleration-model applicability to adhesive-specific mechanisms | `siph_packaging_reliability.md` | A module-level Arrhenius/Peck fit assumes one dominant mechanism; an adhesive can independently exhibit plasticization (reversible), hydrolysis (irreversible), and interfacial fatigue (cycle-driven) simultaneously, which are not one mechanism | "Has failure analysis identified which adhesive-level mechanism (plasticization, hydrolysis, or fatigue debonding) the module-level acceleration model is assumed to represent? A single Ea across mixed adhesive mechanisms is not meaningful" |
