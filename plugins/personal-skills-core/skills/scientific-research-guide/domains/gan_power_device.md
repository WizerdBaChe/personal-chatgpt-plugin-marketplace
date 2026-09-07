---
xi: 1
what: "Vertical GaN Power Devices — Vertical GaN power-device profile: architecture, processing, electrical extraction, and TCAD"
tags: [srg-domain, 領域框架, base]
aliases: ["vertical GaN", "GaN power device", "trench MOSFET", "OG-FET", "OG-MOSFET", "CAVET", "field plate", "field shield", "p-shield", "dynamic RON"]
date: 2026-08-26
status: live
profile_type: base
parent: "-"
---
# Domain Profile: Vertical GaN Power Devices

> Scope of applicability: Vertical gallium-nitride power devices, with emphasis on trench MOSFETs, OG-FET/OG-MOSFET variants, CAVETs, field plates, field shields, fabrication, electrical extraction, and TCAD.
> Scientific nature: Wide-bandgap semiconductor electrostatics, transport, interface physics, recombination/trapping, and coupled optical/electrical field analysis.
> Engineering nature: Vertical power-device architecture, process integration, blocking/conduction trade-offs, switching parasitics, TCAD calibration, and measurement conditions.
>
> Profile metadata:
> - Profile ID: gan_power_device.domain.v1
> - Profile version: 1.2 (Source Ledger backfilled 2026-08-24; §3.7 currency pass 2026-08-26 — wrong first author, wrong title and a citation-less ledger row all corrected, five `~ Approximate` rows resolved)
> - Last updated: 2026-08-26
> - Author(s) / Maintainer(s): Scientific Research Guide integration pass
>
> Primary source types:
> - Textbooks: Wide-bandgap semiconductor device and power-electronics textbooks when a canonical definition is needed
> - Review articles: Vertical GaN architecture, materials, and processing reviews
> - Methods / standards papers: Device extraction, breakdown, capacitance, gate-charge, and TCAD methodology papers
> - Other: Primary architecture/process papers; datasheets only for explicitly identified engineering benchmarks
>
> Notes for AI use:
> - Intended use: Route vertical GaN architecture, measurement, fitting, process, and TCAD questions with condition-aware warnings
> - Validation status / usage note: Integrated from the supplied packet and targeted literature; study-specific numbers are not universal ranges

This profile covers vertical GaN power-device reasoning. It is not a general GaN materials profile and it does not replace a lateral HEMT profile. Route a lateral 2DEG HEMT question to a dedicated HEMT profile if one is added later.

## 1. Theoretical Framework Anchoring

### 1.1 Architecture boundary

Vertical devices carry current through the wafer thickness and use a designed drift region to sustain voltage. Lateral HEMTs primarily conduct through a surface or heterointerface channel, often a two-dimensional electron gas. The distinction changes the dominant resistance, electric-field geometry, thermal path, measurement conditions, and failure modes.

The vertical architecture family in scope includes:

| Architecture | Distinguishing structure | Primary question |
|---|---|---|
| Vertical trench MOSFET | Recessed gate in a trench with a vertical drift path | Can the gate/channel and trench dielectric support the target current and voltage? |
| OG-FET or OG-MOSFET | A vertical or regrown channel with an oxide-gated control region; some variants use an in-situ or regrown oxide/channel stack | Is the channel/interface sufficiently low-loss and stable? |
| CAVET | Current aperture, current-blocking layer, vertical drift path, and regrown or buried-gate-related interfaces | Is the aperture, UID layer, aperture doping, gate-overlap length, gate type, or regrowth interface limiting turn-on and dynamic resistance? |
| Field-plate or field-shield variant | Conductive, dielectric, p-type, split-gate, or triple-shield structures redistribute the trench or edge electric field in a RESURF-like design space | Does the field redistribute without creating a new dielectric, capacitance, or process limit? |

For an OG-FET or CAVET design, keep the aperture/current-blocking-layer label, aperture length and doping, gate-overlap length, UID thickness, gate type, and any delta-doping or regrowth-interface treatment as separate variables. These names identify a design parameter set; they do not establish a universal optimum.

Vertical GaN reviews identify high critical field and high saturation velocity as the motivation for vertical architectures, but the realized device is still constrained by defects, interfaces, contacts, substrate, thermal resistance, and processing. See the reviews [Materials and processing issues in vertical GaN power electronics](https://doi.org/10.1016/j.mssp.2017.09.033) and [Vertical GaN MOSFET Power Devices](https://doi.org/10.3390/mi14101937).

### 1.2 Shared physical chain

| Layer of reasoning | Governing idea | Observable or extracted quantity |
|---|---|---|
| Band structure and material | Wide-bandgap GaN sets the available band offsets and field scale; defects and compensation alter the practical carrier population | Band gap, carrier density, compensation, defect-related activation |
| Drift region | Poisson electrostatics and carrier transport determine field spreading, depletion, and voltage blocking | Drift thickness and doping, electric-field profile, breakdown voltage |
| MOS channel and interface | Gate electrostatics, channel mobility, interface traps, and roughness control threshold, on-state loss, and hysteresis | Threshold voltage, channel mobility, interface-trap response, transfer-curve history |
| Trench corner and shield | Geometry concentrates field at corners; dielectric, conductive, or p-type shields redistribute it | Local peak field, dielectric stress, breakdown, capacitance, charge |
| Switching parasitics | Gate-to-drain coupling and output capacitance set the charge and loss required during switching | Cgd, Coss, Qgd, Qoss, gate charge, Miller plateau |
| Regrowth and aperture | Regrowth interfaces, barriers, and space charge can add a turn-on knee that is not the MOS threshold | CAVET turn-on voltage, transient activation, aperture resistance |

### 1.3 Inviolable constraints

1. Breakdown voltage, specific on-resistance, capacitance, and switching loss form a coupled design problem. A field plate or shield cannot be credited with improving all of them without stating the geometry, bias, dielectric, and comparison baseline.
2. A trench bottom corner is a local field problem, not merely a nominal gate-voltage problem. The peak field and dielectric stress must be examined spatially.
3. Channel mobility, threshold stability, and hysteresis are interface- and process-dependent. Geometry alone cannot establish them.
4. A CAVET turn-on knee is not automatically the MOS threshold. Regrowth-interface barriers and space charge can dominate the knee; see [On the origin of the turn-on voltage drop of GaN-based current aperture vertical electron transistors](https://doi.org/10.1063/5.0079760).
5. A TCAD breakdown value is a model-defined result until mesh convergence, impact-ionization assumptions, boundary conditions, and experimental comparison are documented.
6. RDS(on), Ron,sp, Qgd, and hysteresis are condition-dependent. Report temperature, drain bias, gate bias, current density, pulse width or sweep history, package/contact treatment, and normalization before comparing papers.
7. A process recipe is not portable across crystal orientation, wafer stack, trench profile, dielectric, contact metallurgy, and anneal tool. Copy only a fully traceable recipe with its process window.

### 1.4 Decision point (mandatory Tier 0 confirmation)

Before giving a detailed recommendation, identify which path is intended:

- Device architecture: trench MOSFET, OG-FET/OG-MOSFET, CAVET, or a field-termination-only problem.
- Analysis target: blocking/breakdown, conduction/RDS(on), gate charge/switching, dynamic trapping, or process integration.
- Evidence target: analytical scaling, TCAD design study, measured wafer/device data, or reliability qualification.

## 2. Measurement Tool Inventory

| Measurement target | Tool | Output information | Applicable conditions | Common misuse | Source [Key] |
|---|---|---|---|---|---|
| Trench and field-shield geometry | Cross-sectional SEM, FIB-SEM, TEM, AFM, profilometry | Trench depth, corner radius, dielectric and regrowth geometry, roughness | Cleave/FIB direction, calibration, sampling location, destructive status | Treating a nominal layout dimension as the fabricated corner radius | — (general technique knowledge) |
| Surface and composition | XPS, EDS, SIMS or related depth-sensitive analysis | Elemental composition, contamination, oxidation, dopant profile | Sputter energy, calibration, depth resolution, surface preparation | Calling a surface signal a bulk concentration | — (general technique knowledge) |
| Epitaxy and regrowth | XRD, TEM, Raman, defect mapping, cross-sectional microscopy | Crystal quality, strain, interface and defect evidence | Wafer position, orientation, film thickness, mapping area | Inferring interface trap density from a single structural image | — (general technique knowledge) |
| DC transfer and output | Gate-voltage sweep, drain-voltage sweep, pulsed I-V where appropriate | Vth, transconductance, current density, on-state resistance, leakage | VDS, VGS range, sweep rate, temperature, compliance, hysteresis direction | Comparing Vth extracted with different conventions or drain biases | — (general technique knowledge) |
| Low-resistance extraction | Kelvin or four-terminal structures; de-embedded package/contact measurement | Source, channel, accumulation/access, JFET or aperture, drift, substrate, contact, package, and total resistance components | Geometry, current level, temperature, contact and package de-embedding | Reporting one slope as intrinsic channel resistance | — (general technique knowledge) |
| Carrier and interface response | Hall, C-V, charge pumping or other validated interface method | Carrier density, mobility, capacitance, trap response | Frequency, amplitude, geometry, temperature, model assumptions | Treating Hall mobility as MOS channel mobility | — (general technique knowledge) |
| Blocking and breakdown | Quasi-static or pulsed breakdown, leakage, avalanche-current monitoring | VBD, leakage, failure mode, avalanche onset | Current criterion, ramp rate, temperature, compliance, destructive/non-destructive status | Equating simulated avalanche onset with catastrophic measured breakdown | NRL2022_1p3kV |
| Gate charge and capacitance | Double-pulse or standardized gate-charge measurement; impedance or C-V analysis | Qg, Qgs, Qgd, Cgd, Coss, Qoss, Miller plateau | VDS, VGS limits, gate current, temperature, frequency, fixture | Comparing Qgd without matching voltage and gate-current conditions | SciRep2024_TripleShield |
| Dynamic trapping | Pulsed I-V, double-pulse, drain-current recovery, gate-bias history | Dynamic RON, current collapse, recovery time | Pulse width, duty cycle, quiescent bias, delay, temperature | Calling a dynamic increase an intrinsic DC resistance | — (general technique knowledge) |
| Thermal behavior | Infrared, Raman thermometry, calibrated thermal test, electrothermal extraction | Junction or surface temperature, thermal resistance, drift | Emissivity/calibration, boundary conditions, duty cycle, heat sinking | Attributing temperature-driven drift to a field-plate mechanism | — (general technique knowledge) |

## 3. Standard Modeling Toolchain

### 3.1 Modeling chain

~~~text
material and epitaxy
    -> process cross-section and mesh
    -> electrostatics and transport
    -> field, current, capacitance, and breakdown extraction
    -> mixed-mode or electrothermal switching analysis
    -> fabricated-device measurement and model calibration
~~~

| Stage | Minimum inputs | Useful outputs | Boundary condition |
|---|---|---|---|
| Material/epitaxy | Layer thicknesses, doping/compensation, contacts, defect assumptions | Band diagram, carrier profile, nominal material parameters | Do not use nominal doping as measured active carrier density |
| Process cross-section | Trench shape, corner radius, dielectric, shield, regrowth and contact geometry | Meshed device and process sensitivities | Mesh the field-concentrating corner and interface explicitly |
| DC device TCAD | Mobility, recombination, traps, impact-ionization and boundary models | Transfer/output curves, field map, RON, VBD | Record model names, parameters, convergence and bias path |
| Switching or mixed-mode | Gate resistance/current, circuit parasitics, C(V), temperature model | Gate charge, Miller behavior, switching loss, overshoot | A device-only result is not a packaged switching result |
| Calibration | Measured I-V, C-V, gate charge, pulse response, temperature | Calibrated parameters and residuals | Calibrate multiple observables; do not fit one curve and call the model validated |

Sentaurus Device or an equivalent drift-diffusion TCAD platform is suitable for baseline Poisson/continuity analysis. Hydrodynamic, Monte Carlo, quantum, or tunneling models are extensions, not automatic upgrades. Avalanche output should be reported with the selected impact-ionization model, local field quantity, mesh resolution, and the current or field criterion used to define onset.

For reproducibility, preserve the tool version, mesh controls, material parameter file, bias sweep, solver tolerances, and exported field/current data. File extensions such as TDR or PLT are tool-specific implementation details, not evidence by themselves.

### 3.2 Process flow and process-packet boundary

A common conceptual sequence is mesa isolation, trench definition, sidewall and bottom treatment, dielectric or regrowth formation, contact and via definition, source/drain and gate or field-plate metallization, and passivation. The actual sequence and thermal budget must be taken from the cited process paper.

The supplied packet mentions Cl-based ICP/RIE, wet treatment such as TMAH, ALD Al2O3 or HfO2, Ti/Al/Ni/Au-style contacts, high-temperature annealing, SiNx passivation, and gate/field-plate metal. These remain process examples rather than defaults because the packet did not preserve a traceable primary citation and the values are stack- and orientation-dependent. Do not present them as a universal recipe.

For shielded trench designs, preserve the actual conductive and dielectric topology. A triple-shield BPSG-MOS example in the packet combines a grounded split gate (SG), a P+ shield region (PSR), and a semi-wrapped BP layer that extends the P-shield beneath the gate and along the trench sidewalls (the source names the composite three-part device "BPSG-MOS"; the BP layer is the third component — the earlier wording, "a semi-wrapped BPSG structure", re-used the whole-device name as if it were that component's name, corrected 2026-08-26 against the source's full text); its reported capacitance or charge reduction is a design-case result, not a general rule.

## 4. Domain-Specific Fitting Methods

| Method | Applicable question | Applicable conditions | Common error | Correct approach | Source [Key] |
|---|---|---|---|---|---|
| Linear-extrapolation Vth | Operational threshold from a chosen transfer-curve regime | State VDS, temperature, sweep direction, current normalization, and linear window | Calling the intercept a material constant or comparing different windows | Report the convention and verify with hysteresis and a second extraction if threshold stability matters | — (general technique knowledge) |
| Low-VDS slope or Kelvin RON | On-state resistance under a defined operating point | Separate channel, drift, contact, access, and package terms where possible | Treating total terminal slope as intrinsic channel resistance | Use Kelvin/de-embedded structures or provide a resistance budget | — (general technique knowledge) |
| Gate-charge segmentation | Qgs, Qgd, Miller plateau and switching energy | Fixed VDS, gate current or gate resistance, VGS limits, temperature, fixture | Comparing Qgd with different drain voltages or gate currents | Show the full Qg curve and annotate the integration boundaries | — (general technique knowledge) |
| C(V) and Qoss extraction | Output charge and capacitance for switching design | Frequency, AC amplitude, DC bias, fixture and loss model | Assuming a single constant Coss or ignoring frequency dependence | Use a bias-dependent curve and integrate over the actual switching voltage | — (general technique knowledge) |
| TCAD avalanche-onset extraction | Model-defined onset or breakdown criterion | Mesh convergence, impact model, field variable, current criterion, bias path | Treating avalanche-current onset as measured destructive BV | Name the criterion and cross-check with a measured breakdown or a second model | — (general technique knowledge) |
| CAVET turn-on-knee analysis | Separating aperture/interface activation from channel threshold | Transient or temperature dependence and an interface/barrier model | Calling the knee a gate Vth | Fit or compare the interface contribution explicitly | JAP2022_CAVET |
| Hysteresis analysis | Trap, polarization, leakage, or dielectric-history response | Bidirectional sweep, dwell time, temperature, pre-bias and recovery time | Assigning all hysteresis to one defect class | Report the full history protocol and compare with pulsed and temperature-dependent data | — (general technique knowledge) |

## 5. Domain-Specific Quality Metrics

The following values are study-specific anchors, not universal acceptance bands. Table
restructured 2026-08-24 to the shared schema (see `domain-expansion-guide.md` §3.3) — the
original "How to report it" column maps to **Conditions** below, "Anchored examples or range
status" maps to **Typical value range** (with its inline link extracted to **Source [Key]**),
and **Suspicious comparison** is kept as a bonus column since it captures real information the
canonical schema doesn't otherwise have a slot for.

| Metric | Abbreviation | Physical meaning | Typical value range | Conditions | Source [Key] | Suspicious comparison |
|---|---|---|---|---|---|---|
| Breakdown voltage | VBD | Maximum reverse voltage sustained before avalanche/destructive breakdown | 1306 V in a 1.3 kV vertical trench MOSFET study (same study also reported VTH = 3.15 V, RON,sp = 1.93 mΩ·cm²); a device-case value, not a target range | Voltage criterion, leakage/current limit, ramp, temperature, destructive status | NRL2022_1p3kV | Calling 334 V, 1.3 kV, and multi-kV devices one performance range without architecture and substrate |
| Specific on-resistance | RON,sp | On-state resistance normalized by active device area | The 1.3 kV study's 1.93 mΩ·cm² is a device-case value, not a typical target | Area definition, current density, VGS, VDS, temperature, Kelvin/package treatment | NRL2022_1p3kV | Comparing a simulated drift-only value with a measured total value |
| Baliga-type figure of merit | BFOM | Composite material/device figure of merit combining breakdown voltage and on-resistance | The supplied packet's 0.88 GW/cm² value follows from the cited 1.3 kV case; treat it as a calculated case result | State formula and whether RON,sp includes all terms | NRL2022_1p3kV | Comparing different voltage and resistance definitions |
| Threshold voltage | VTH | Gate voltage at which the channel begins conducting, under a stated extraction convention | 3.15 V in the cited 1.3 kV study and 5 V in one later fully vertical device report — architecture-specific examples, not a universal window | Extraction convention, drain bias, sweep and temperature | NRL2022_1p3kV | Mixing enhancement-mode threshold definitions |
| Gate-drain/output charge and capacitance | Qgd, Cgd, Qoss, Coss | Switching-relevant charge and capacitance terms | A triple-shield BPSG-MOS design reports a case-specific Cgd reduction and Qgd value; use the paper's exact conditions | Voltage interval, gate current/frequency, fixture and temperature | SciRep2024_TripleShield | Treating simulated charge reduction as a measured switching guarantee |
| Peak dielectric or shield field | — | Maximum local electric field at a dielectric/shield interface | A buried-field-shield study discusses a simulated dielectric-field limit below about 4 MV/cm and a geometry-dependent value near 5 MV/cm — study-specific design observations | Spatial maximum, dielectric thickness, bias, mesh and model | ePrime2023_FieldShield | Using the number as a GaN dielectric universal limit |
| Dynamic RON or hysteresis | — | Transient increase in on-resistance / gate-voltage-history dependence relative to a DC reference | No universal range is accepted here | Ratio or delta relative to a stated DC reference, with pulse history; report the complete pulse and recovery protocol | — (general technique knowledge) | Comparing values from different quiescent biases |

Do not invent a single “good GaN” range when the supplied sources and verified literature support only study-specific examples. For a new device, report the full conditions first and classify the metric as application target, model result, wafer result, or packaged-device result.

## 6. Common Assumption Pitfalls

> Table header renamed 2026-08-24 to match the shared schema — "Trigger"→"Trigger condition",
> "Recovery"→"Correct approach", Source [Key] added. "Why it fails" is kept as-is rather than
> relabeled to the canonical "How to recognize it": it captures a genuinely different thing
> (causal mechanism, not a detection symptom) — see `domain-expansion-guide.md` §3.3.

| Pitfall | Trigger condition | Why it fails | Correct approach | Source [Key] |
|---|---|---|---|---|
| Vertical/lateral category error | User compares a vertical trench MOSFET directly with a lateral 2DEG HEMT | The current path, drift region, capacitance, and thermal path are different | Split the comparison by architecture and normalize only after defining the metric | — (general technique knowledge) |
| Field plate treated as a free improvement | User claims a field plate raises BV and lowers RON without a geometry or capacitance budget | Field redistribution trades against dielectric stress, area, capacitance, and process complexity | Request the field map, shield bias, dielectric, C(V), and baseline | — (general technique knowledge) |
| Trench corner omitted | Mesh or layout uses nominal trench dimensions only | The local corner field can dominate dielectric stress and breakdown | Add corner-radius sensitivity and a locally refined mesh | — (general technique knowledge) |
| TBD acronym expanded by guess | Notes use TBD without the original legend | TBD can be a project placeholder; one recent paper uses it for thick bottom dielectric | Preserve the ambiguity and cite the source context before expanding it | pssa2024_TBD |
| Process recipe generalized | User copies RIE, wet treatment, ALD, contact, or anneal conditions to another stack | Orientation, sidewall chemistry, dielectric, and contact activation change the result | Require a traceable recipe and report the full process window | — (general technique knowledge) |
| Single I-V slope called intrinsic RON | Only two-terminal output data are available | Contact, access, drift, and package terms may dominate | Use Kelvin/de-embedding or publish a resistance budget | — (general technique knowledge) |
| Qgd compared without Miller conditions | Gate charge is quoted without VDS, gate current, or fixture | Qgd is bias- and measurement-dependent | Re-measure or replot under matched conditions | — (general technique knowledge) |
| TCAD breakdown overclaimed | A single avalanche simulation is presented as device BV | Model, mesh, boundary and criterion uncertainty can be large | Run convergence and sensitivity checks; compare with measured or independently modeled behavior | — (general technique knowledge) |
| CAVET knee called threshold | Turn-on voltage is inferred from a drain-current knee | Regrowth interface barriers and space charge can produce the knee | Separate MOS threshold from aperture/interface activation | JAP2022_CAVET |
| Hysteresis assigned to one trap | Forward/backward VGS curves differ and the cause is declared | Traps, polarization, leakage, dielectric history and temperature can overlap | Vary sweep history, temperature, pulse timing and pre-bias | — (general technique knowledge) |
| Study metric turned into a typical range | A single high-voltage or low-resistance result is repeated as a target | The result may be a simulation, a special wafer, or a different normalization | Label it as a case result and preserve architecture and conditions | — (general technique knowledge) |

## 7a. Literature Anchors

1. Langpoklakpam et al., “Vertical GaN MOSFET Power Devices,” *Micromachines* 14, 1937 (2023). [DOI](https://doi.org/10.3390/mi14101937)
2. Hu et al., “Materials and processing issues in vertical GaN power electronics,” *Materials Science in Semiconductor Processing* 78 (2018). [DOI](https://doi.org/10.1016/j.mssp.2017.09.033)
3. “1.3 kV Vertical GaN-Based Trench MOSFETs on 4-Inch Free Standing GaN Wafer,” *Nanoscale Research Letters* 17, 14 (2022). [DOI](https://doi.org/10.1186/s11671-022-03653-z)
4. “Gate protection for vertical gallium nitride trench MOSFETs: The buried field shield,” *e-Prime* 5 (2023). [DOI](https://doi.org/10.1016/j.prime.2023.100218)
5. “On the origin of the turn-on voltage drop of GaN-based current aperture vertical electron transistors,” *Journal of Applied Physics* 131, 114502 (2022). [DOI](https://doi.org/10.1063/5.0079760)

## 7b. Source Ledger (backfilled 2026-08-24 per `domain-expansion-guide.md` §3.2)

> This profile already used resolvable DOI links throughout (a much better-behaved starting point than the two profiles that motivated this requirement). This ledger tabulates those existing citations, plus one used inline in Node 6 but missing from the 7a list above (the "TBD" pitfall row's source).

> **Verified (date)** (`domain-expansion-guide.md` §3.7): when this row's claim was last checked
> against the primary source — not the source's own publication year.
>
> **2026-08-26 currency pass** (audit trail: `reports/2026-08-26-scientific-research-guide-source-currency-pass.md`).
> All seven rows were re-resolved against Crossref; six also had the specific claim they support
> re-checked. Five rows carried `~ Approximate (well-formed DOI, not independently re-fetched)` — a
> status that says nothing was ever opened — and re-opening them found **three real defects**: a wrong
> first author (`Meneghini2018` is Hu et al.), a wrong title (`JAP2022_CAVET` spells the term out, the
> acronym was substituted), and a ledger row that carried **no citation at all** — `SciRep2024_TripleShield`
> had only a paraphrase in its Full-citation cell, and its "2024" is the DOI-registration year: the paper
> published 2025-01-02. All three propagate into §7a and Nodes 1/3, and were fixed there too. One row
> (`ePrime2023_FieldShield`) is honestly left short of confirmation: its identity checks out, but the
> ~4–5 MV/cm figure in Node 5 could not be reached behind ScienceDirect's 403.

| Key | Full citation | Identifier | Access tag | Verification status | Verified (date) | Locator | Used in |
|---|---|---|---|---|---|---|---|
| Langpoklakpam2023 | Langpoklakpam et al., "Vertical GaN MOSFET Power Devices," Micromachines 14, 1937 (2023) | DOI: 10.3390/mi14101937 | [abstract] | ✅ Confirmed — **upgraded from `~ Approximate` 2026-08-26**: authors, journal, vol. 14(10), article 1937 and the 2023-10-16 date all match Crossref | 2026-08-26 | Whole paper | 7a #1; §1.1 review citation |
| Meneghini2018 | **Hu et al.** (Hu, Zhang, Sun, Piedra, Chowdhury, Palacios), "Materials and processing issues in vertical GaN power electronics," Mater. Sci. Semicond. Process. 78 (2018) — the key string is kept for citation stability, but the authors are **not** Meneghini et al. | DOI: 10.1016/j.mssp.2017.09.033 | [abstract] | ✅ Confirmed — **wrong first author corrected 2026-08-26**: title, journal, volume and DOI were right, but Crossref and the MIT DSpace mirror independently give the byline as Hu, Zhang, Sun, Piedra, Chowdhury, Palacios. The same error was corrected in §7a #2 | 2026-08-26 | Whole paper | 7a #2; §1.1 review citation |
| NRL2022_1p3kV | "1.3 kV Vertical GaN-Based Trench MOSFETs on 4-Inch Free Standing GaN Wafer," Nanoscale Res. Lett. 17, 14 (2022) | DOI: 10.1186/s11671-022-03653-z | [full] — **upgraded from [abstract] 2026-08-26** (open text read via PMC) | ✅ Confirmed (2026-08-24 via search; 2026-08-26 re-confirmed against the open-access full text — V_TH = 3.15 V at I_DS = 1 µA/mm, BV = 1306 V at I_DS > 50 mA/cm², R_ON,sp = 1.93 mΩ·cm² at V_DS = 0.5 V / V_GS = 20 V, and an experimental FOM of 0.88 GW/cm² — every number and **its stated condition** matches. The paper additionally reports a 1.68 GW/cm² *simulated* FOM, which this profile deliberately does not cite) | 2026-08-26 | Whole paper | Node 5 VBD/RON,sp/BFOM/VTH rows |
| ePrime2023_FieldShield | "Gate protection for vertical gallium nitride trench MOSFETs: The buried field shield," e-Prime 5 (2023) | DOI: 10.1016/j.prime.2023.100218 | [abstract] | ~ Approximate — bibliographic identity (authors, journal, volume, article number) **was** confirmed via Crossref 2026-08-26, but the ~4–5 MV/cm dielectric-field figure this row supports in Node 5 was **not** independently confirmed: ScienceDirect returned 403, OSTI was unreachable, and no abstract record exists on the fallback indexes. A search-engine summary did offer matching numbers and was **refused** as inadmissible. `review-when:` the full text becomes reachable | 2026-08-26 (identity only — the numeric claim remains unverified) | Whole paper | Node 5 "Peak dielectric or shield field" row |
| JAP2022_CAVET | Döring et al., "On the origin of the turn-on voltage drop of GaN-based **current aperture vertical electron transistors**," J. Appl. Phys. 131, 114502 (2022) | DOI: 10.1063/5.0079760 | [abstract] | ✅ Confirmed — **title corrected 2026-08-26**: the paper spells the term out; the previously recorded title substituted the acronym "CAVET", which the paper's own title does not use. Authors, journal, volume and article number match Crossref, and the abstract confirms the regrowth-interface-barrier mechanism cited in §1.3 and Node 4. The same substitution was corrected in §1.3 and §7a #5 | 2026-08-26 | Whole paper | §1.3 constraint 4; Node 4 CAVET turn-on-knee row |
| pssa2024_TBD | Hao et al., "Analysis and Manufacturing of GaN Trench-Gate MOSFETs with Thick Bottom Dielectric," Phys. Status Solidi A 222(8), 2400804 (published online 2024; issue dated 2025) | DOI: 10.1002/pssa.202400804 | [abstract] | ✅ Confirmed — **upgraded from `~ Approximate` 2026-08-26**: title, authors and DOI match Crossref; volume 222 and issue 8 were missing from this row and are now recorded. The title itself substantiates the "TBD = thick bottom dielectric" expansion asserted in Node 6 | 2026-08-26 | Whole paper | Node 6 "TBD acronym expanded by guess" row — cited inline but was missing from 7a; added here |
| SciRep2024_TripleShield | Qiu, X. & Wei, J., "A low switching loss GaN trench MOSFET design utilizing a triple-shield structure," *Sci. Rep.* **15**(1), 206 (2025) — a design-case study reporting a case-specific Cgd reduction and Qgd value (a distinct source from ePrime2023_FieldShield above — different device concept; both merely involve field-shield geometry) | DOI: 10.1038/s41598-024-84007-w | [full] — open text read via PMC11696899 | ✅ Confirmed — **this row previously had no citation at all**, only a paraphrase of what the source said; authors, title, volume/issue/article resolved 2026-08-26 via Crossref + PMC. Note the key's "2024" is the **DOI-registration** year: the paper published 2025-01-02. Q_gd = 21 nC/cm² at I_g = 0.1 mA / I₁ = 5 A / V_ds = 30 V is confirmed, as is a large Cgd reduction against both comparison designs. ⚠ The PMC-extracted text is internally inconsistent on the exact percentages (81 %/98 % in one passage, 98 %/88 % in another) and this pass could not determine which is authoritative — so **no percentage is quoted** in Node 5 | 2026-08-26 | Results: Qgd/Cgd comparison | Node 5 "Qgd, Cgd, Qoss and Coss" row; §3.2 process-flow triple-shield example |

---

### Closest Related Domain Profiles

| Related profile | Link | Boundary |
|---|---|---|
| Topological insulator / Bi2Se3 material | Use for defect, thickness, surface-state, transport, and multi-channel reasoning | Do not import TI surface-state assumptions into GaN MOS electrostatics |
| MicroLED | Shared GaN fabrication vocabulary and possible TCAD/process tools | MicroLED quality is dominated by recombination, extraction and optical metrics, not power-device blocking |
| Plasmonic waveguide | Shared electric-field and capacitance vocabulary in optical structures | SPP loss and optical mode fitting are not a substitute for power-device breakdown analysis |

### Cross-Domain Conflict Notes

| Issue / constraint | Other profile(s) involved | Potential conflict | AI confirmation question |
|---|---|---|---|
| Same GaN or RIE vocabulary, different quality metrics | microled.md | A fabrication change may be judged by RON/BV in one profile and EQE/SRV in the other | “Are we evaluating a power-device blocking/conduction target or a recombination/optical pixel target?” |
| Surface field language reused across optics and power devices | plasmonic_waveguide.md | Optical mode confinement and SPP loss do not establish semiconductor breakdown or dielectric reliability | “Is the field quantity optical and time-harmonic, or a DC/pulsed power-device blocking field?” |
| Bi2Se3 surface-state assumptions imported into GaN | topological_insulator/bi2se3_material.md | A topological surface state is not a MOS interface channel | “Is this a GaN interface/trap problem or a TI band-topology problem?” |

The current profile intentionally does not add a lateral HEMT branch, a full reliability qualification protocol, or a universal process recipe. Those are separate expansions with different evidence requirements.
