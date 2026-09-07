---
xi: 1
what: "Inorganic MicroLED Devices — Inorganic microLED pixel/optoelectronic device profile"
tags: [srg-domain, 領域框架, base]
aliases: ["microLED", "micro-LED", "micro LED", "µLED", "sidewall effect", "pixel EQE", "AlGaInP red microLED", "InGaN microLED"]
date: 2026-08-26
status: live
profile_type: base
parent: "-"
---
# Domain Profile: Inorganic MicroLED Devices

> Scope of applicability: Inorganic microLED pixels and arrays, especially InGaN/GaN blue-green devices and AlGaInP red devices; size effects, sidewall damage, passivation, epitaxy, optical extraction, and electro-optical characterization.
> Scientific nature: Semiconductor quantum-well recombination, carrier transport, surface-state physics, optical extraction, and thermal/current-density scaling.
> Engineering nature: Pixel fabrication, sidewall/passivation process integration, calibrated electro-optical testing, optical modeling, and display-relevant device comparison.
>
> Profile metadata:
> - Profile ID: microled.domain.v1
> - Profile version: 1.2 (Source Ledger backfilled 2026-08-24; §3.7 currency pass 2026-08-26 — all six rows re-resolved against Crossref, author lists recovered, one title corrected, one access tag upgraded)
> - Last updated: 2026-08-26
> - Author(s) / Maintainer(s): Scientific Research Guide integration pass
>
> Primary source types:
> - Textbooks: Semiconductor light-emitting-device and optoelectronics textbooks when a canonical definition is needed
> - Review articles: MicroLED size effects, sidewall mitigation, epitaxy, and device integration reviews
> - Methods / standards papers: Calibrated EQE/IQE/LEE, TRPL, far-field, thermal, and lifetime methodologies
> - Other: Primary pixel/process papers; display metrics only when their calibration and duty cycle are explicit
>
> Notes for AI use:
> - Intended use: Route material-specific microLED size, sidewall, passivation, recombination, optical, and electro-thermal questions
> - Validation status / usage note: Integrated from the supplied packet and targeted literature; material and process study numbers are not universal targets

This profile covers semiconductor microLED device physics and device-level characterization. It does not cover OLED or QLED pixels, backplane mass-transfer engineering as a standalone topic, or display-system color management unless they are needed to interpret a pixel measurement.

## 1. Theoretical Framework Anchoring

### 1.1 Device and material boundary

MicroLED downscaling changes the perimeter-to-area ratio, carrier spreading, optical extraction, thermal boundary, and the relative importance of surface states. The dominant mechanism is material- and process-dependent:

| Device family | Representative active structure | Dominant questions |
|---|---|---|
| InGaN/GaN blue-green | n-cladding, InGaN multiple quantum wells, p-cladding and current-spreading layers | How do etched sidewalls, polarization fields, carrier leakage, recombination and extraction change with pixel size? |
| AlGaInP red | InGaP quantum wells with AlGaInP barriers/cladding and a p-GaP or related current-spreading/window layer | How do high surface recombination, carrier diffusion, current spreading and passivation affect red-pixel efficiency? |
| Process or geometry variant | Via-hole, mesa, trench, RIE-free, selective-epitaxy, ion-implanted or passivated pixel | Which new surface, thermal, optical, or contact boundary did the process create? |

The 2025 review [Advanced technologies in InGaN micro-LED fabrication to mitigate the sidewall effect](https://doi.org/10.1038/s41377-025-01751-y) treats sidewall damage and mitigation as a coupled fabrication and device-physics problem. It also cautions that epitaxy and packaging affect EQE, so EQE alone cannot rank fabrication techniques.

### 1.2 Shared physical chain

| Layer of reasoning | Governing idea | Observable or extracted quantity |
|---|---|---|
| Epitaxy and band structure | Direct-gap III-nitride or III-phosphide quantum wells set emission energy, carrier confinement and polarization or band-offset conditions | Wavelength, linewidth, layer thickness, composition, strain |
| Carrier injection and transport | Contact resistance, current spreading, leakage and current crowding determine the local carrier density | I-V, current density map, ideality, series resistance |
| Recombination | Radiative, Shockley-Read-Hall, Auger and surface-related channels compete | Lifetime, IQE, droop, temperature and current dependence |
| Size and perimeter effect | As the pixel shrinks, sidewall perimeter and damaged volume become a larger fraction of the active area | P/A, perimeter length, size-dependent EQE and leakage |
| Surface chemistry and passivation | Dangling bonds, native oxide, etch residues and Fermi-level pinning can create nonradiative pathways | Surface composition, SRV, trap response, recovery after treatment |
| Optical extraction | Internal emission is modified by absorption, cavity, scattering, refractive index and collection geometry | LEE, far-field, spectrum, angular pattern, EQE |
| Thermal and high-current behavior | Self-heating and current crowding alter recombination and spectral output | Junction temperature, droop, wavelength shift, power stability |

### 1.3 Inviolable constraints

1. Shrinking a pixel raises the sidewall-to-active-area contribution, but the measured change is not automatically caused by sidewall recombination. Current spreading, optical collection, heating, epitaxy and contact geometry must be controlled.
2. AlGaInP red and InGaN blue-green devices must not be assigned one universal surface-recombination velocity, diffusion length, passivation response, or EQE target.
3. Etch damage, native oxide, dangling bonds, residues and Fermi-level pinning are candidate mechanisms; they are not proven by a size-dependent EQE curve alone.
4. IQE, LEE, injection efficiency and EQE must be defined and measured with a calibrated optical path. EQE is not a pure material or sidewall metric.
5. TRPL lifetime is not, by itself, a unique surface-recombination measurement. It must be interpreted with geometry, excitation, carrier density, temperature, and a recombination model.
6. A passivation or RIE-free process may reduce one damage channel while introducing another interface, absorption, strain, contamination, or contact limitation.
7. Via-hole and mesa RIE create new sidewalls. Their geometry, etch chemistry, residue, and passivation must be included in the pixel-level model.
8. A display-level brightness comparison is not a device-level EQE comparison unless pixel size, duty cycle, current density, optical collection, packaging, and thermal boundary are matched.

### 1.4 Decision point (mandatory Tier 0 confirmation)

Before giving a detailed recommendation, identify:

- Material route: AlGaInP red, InGaN blue-green, or another material system.
- Scale: single pixel, wafer test structure, or array/display integration.
- Target: sidewall-loss diagnosis, passivation, epitaxy, optical extraction, electrical injection, reliability, or display performance.
- Evidence target: analytical size scaling, TCAD/rate-equation model, calibrated device measurement, or process comparison.

## 2. Measurement Tool Inventory

| Measurement target | Tool | Output information | Applicable conditions | Common misuse | Source [Key] |
|---|---|---|---|---|---|
| Epitaxy and layer stack | Cross-sectional TEM, SEM, AFM, XRD, composition analysis | MQW thickness, roughness, interfaces, strain, layer composition | Sampling position, orientation, calibration, destructive status | Inferring uniformity from one cross-section | — (general technique knowledge) |
| Surface chemistry and residues | XPS, ToF-SIMS, EDS, surface microscopy | Oxide, elemental residue, passivation coverage, depth profile | Sputter energy, calibration, surface preparation, depth resolution | Treating a surface or sputter artifact as a bulk defect density | — (general technique knowledge) |
| Pixel geometry | SEM, FIB-SEM, profilometry, AFM | Pixel width, sidewall angle, height, via-hole and mesa geometry | Metrology calibration and sampling across the wafer | Using nominal mask size instead of fabricated optical/electrical size | — (general technique knowledge) |
| DC electrical | I-V, leakage, contact or transfer structures | Series resistance, leakage, ideality, current density tolerance | Temperature, polarity, sweep rate, compliance, area definition | Calling leakage current a recombination rate without a transport model | — (general technique knowledge) |
| Optical power and spectrum | Calibrated I-V-L, spectrometer, integrating sphere or calibrated collection | Optical power, wavelength, linewidth, EQE | Calibration, collection solid angle, spectral response, packaging | Comparing uncalibrated output or different collection geometries | — (general technique knowledge) |
| Recombination lifetime | TRPL, time-resolved electroluminescence, µPL or CL | Effective lifetime and spatial/current dependence | Excitation density, repetition rate, temporal response, temperature | Equating one lifetime with a unique SRV | — (general technique knowledge) |
| IQE and LEE | Temperature-dependent or calibrated optical method, integrating sphere, optical model | IQE, LEE, injection efficiency, uncertainty | Optical calibration, refractive-index model, packaging and collection definition | Solving for one factor from an underdetermined product | — (general technique knowledge) |
| Angular emission | Angle-resolved far-field and polarization-resolved collection | Emission pattern, divergence, polarization, cavity effects | Angular calibration, polarization optics, wavelength, aperture | Calling a collection artifact an intrinsic extraction gain | — (general technique knowledge) |
| Size and current scaling | Current-density-EQE, power-density, temperature and size series | Droop, size effect, current crowding and thermal trend | Same process, duty cycle, temperature, pulse/DC mode, geometry | Mixing current with current density or comparing red to blue without controls | RinP2022_AlGaInP |
| Thermal behavior | Thermoreflectance, calibrated IR/Raman, electrical thermal extraction | Junction temperature and thermal resistance | Emissivity/calibration, duty cycle, heat sink and boundary conditions | Assigning a spectral shift to quantum-well physics without temperature data | — (general technique knowledge) |

## 3. Standard Modeling Toolchain

### 3.1 Modeling chain

~~~text
epitaxy and quantum-well stack
    -> pixel geometry, etch and passivation
    -> electrical transport and recombination model
    -> optical extraction or far-field model
    -> calibrated I-V-L, lifetime, EQE and size-series data
    -> coupled electro-thermal and display-relevant interpretation
~~~

| Stage | Minimum inputs | Useful outputs | Boundary condition |
|---|---|---|---|
| Epitaxy | Layer thickness/composition, doping, strain/polarization assumptions, contacts | Band alignment, confinement and emission estimate | Do not infer layer composition from emission wavelength alone |
| Pixel/process geometry | Pixel width, perimeter, sidewall angle, etched depth, via-hole, passivation and contacts | Local current density, sidewall area and optical boundary | Use fabricated dimensions and include corner/sidewall regions |
| Electrical/recombination model | Mobility, SRH/radiative/Auger terms, SRV, traps, injection and thermal model | Carrier density, current crowding, lifetime, droop | Fit multiple observables, not EQE alone |
| Optical model | Layer stack, complex refractive indices, sidewall roughness, collection geometry | LEE, far-field, absorption and cavity effects | Separate intrinsic extraction from packaging and detector collection |
| Calibration and validation | I-V-L, TRPL, spectrum, EQE, size and temperature series | Parameter posterior or residuals, mechanism discrimination | Preserve uncertainty and identifiability limits |

The process family in the supplied packet includes mesa or via-hole RIE, sidewall treatment, passivation, and optical/electrical characterization. BCl3/Ar RIE residue, native oxide, oxidation, and treatment-specific chemistry are process-dependent observations to verify with surface analysis, not universal assumptions. The packet's exact size-series percentages, including the stated 6-by-6 to 56-by-56 micrometer area-loss comparison, and any unlabelled process recipe are not carried into the profile as general facts without a traceable primary citation.

### 3.2 Recombination and efficiency bookkeeping

Use explicit definitions. A useful bookkeeping relation is:

~~~text
EQE = injection efficiency x IQE x LEE
~~~

The product is only meaningful when each factor is defined consistently and the measurement is calibrated. In many experiments, the factors are not independently identifiable without extra measurements or a validated model.

## 4. Domain-Specific Fitting Methods

| Method | Applicable question | Applicable conditions | Common error | Correct approach | Source [Key] |
|---|---|---|---|---|---|
| Perimeter-to-area or size-effect fit | Does performance scale with sidewall exposure? | Same material, epitaxy, process, temperature, current density and geometry family | Fitting pixel width alone or mixing shape and current-density changes | Include P/A and perimeter length; test residuals and a non-sidewall control | RinP2022_AlGaInP |
| Rate-equation or TRPL fit | Which radiative, SRH, Auger or surface channel is consistent with lifetime data? | Excitation density, temporal response, temperature and carrier-density model | Reporting SRV from one lifetime trace | Fit multiple sizes or powers and report parameter correlation | APL2017_SRH_Auger |
| I-V-L and ideality/series extraction | Is loss electrical, recombination-related, or thermal? | Calibrated power, voltage, current, temperature and duty cycle | Calling all sublinear light output “Auger” or all leakage “sidewall” | Compare pulsed/DC, temperature and current-density series | — (general technique knowledge) |
| IQE, LEE and EQE extraction | Which stage of the efficiency chain changed? | Calibrated optical path and a defined refractive-index/collection model | Inferring LEE or IQE from EQE alone | Measure or constrain the other factors and propagate uncertainty | — (general technique knowledge) |
| Current-density-EQE fit | Where does efficiency droop or roll-off begin? | Same pixel and thermal boundary, specified pulsed/DC mode | Comparing current rather than current density or ignoring self-heating | Report both current density and junction temperature | — (general technique knowledge) |
| Far-field or cavity fit | Did the layer stack or sidewall change angular extraction? | Accurate angle calibration, optical constants, stack, aperture and polarization | Treating detector acceptance as far-field pattern | Calibrate collection and compare with an optical model | — (general technique knowledge) |
| TCAD sidewall-trap fit | What sidewall state density or energy is compatible with a size series? | Geometry, trap model, contact/current spreading and thermal model | Fitting only EQE and overclaiming a unique trap density | Constrain with I-V, TRPL, leakage, spectral and size-series data | — (general technique knowledge) |
| Passivation comparison | Did a treatment reduce the targeted surface pathway? | Matched fabrication, passivation thickness/coverage, aging and measurement | “Passivated” interpreted as “damage-free” | Include untreated, process-control, aging and surface-chemistry evidence | OE2020_RedPassivation |

## 5. Domain-Specific Quality Metrics

There is no single universal microLED performance range. Report the study conditions and
material system before presenting a number. Table restructured 2026-08-24 to the shared
schema (see `domain-expansion-guide.md` §3.3) — "How to report it" maps to **Conditions**,
"Range status or anchored example" maps to **Typical value range** (inline links extracted to
**Source [Key]**), and **Suspicious comparison** is kept as a bonus column.

| Metric | Abbreviation | Physical meaning | Typical value range | Conditions | Source [Key] | Suspicious comparison |
|---|---|---|---|---|---|---|
| Pixel size | — | Fabricated lateral dimension, shape, and active area of a single pixel | Research studies use sub-10-µm to tens-of-µm pixels; size alone is not a quality target. The AlGaInP size-effect study used 160, 80, 40, 20 and 10 µm pixels | Fabricated lateral size, shape, height, P/A and active area | RinP2022_AlGaInP | Treating the same nominal width as the same P/A across shapes and sidewall profiles |
| External quantum efficiency | EQE | Fraction of injected carriers converted to emitted photons, injection × IQE × LEE | The 2025 review reports many process- and material-specific examples; no universal target is defined here | Wavelength, current density, temperature, duty cycle, optical calibration and packaging | Liu2025_Review | Ranking a process from EQE alone while epitaxy, collection or package differs |
| Internal quantum efficiency and light-extraction efficiency | IQE, LEE | The two factors composing EQE alongside injection efficiency | No universal range accepted here; the two factors can be underdetermined from EQE alone | Define extraction method, optical model, refractive indices and uncertainty | — (general technique knowledge) | Treating a model-derived LEE as a direct measurement |
| Surface recombination velocity | SRV | Rate constant for non-radiative recombination at exposed/damaged surfaces | No universal range accepted; red AlGaInP and blue-green InGaN must remain separate until conditions are matched | Material, orientation, surface treatment, temperature and model convention | OE2020_RedPassivation | Transferring a fitted SRV from one material or geometry to another |
| TRPL lifetime | — | Effective time-resolved photoluminescence decay constant | No universal range accepted; lifetime is an effective observable | Excitation density, time window, fitted model, temperature and spatial position | — (general technique knowledge) | Calling a longer lifetime proof of lower SRV without carrier-density controls |
| Droop | — | Efficiency roll-off at high current density | Study-specific; separate Auger, leakage, current crowding and heating hypotheses | Current density, temperature, pulse/DC mode, duty cycle and wavelength | — (general technique knowledge) | Comparing droop at different temperatures or current definitions |
| Spectral and angular output | — | Peak wavelength, linewidth, and angular emission pattern | Study-specific; far-field and EQE must be calibrated separately | Peak wavelength, linewidth, angular coordinate, polarization and collection aperture | — (general technique knowledge) | Calling a detector-acceptance change an extraction improvement |
| Leakage and series resistance | — | Reverse-bias leakage current and forward series resistance | Study-specific; process and sidewall controls are required | Reverse-bias/current criterion, area, temperature and contact geometry | — (general technique knowledge) | Comparing leakage current without area or bias normalization |

## 6. Common Assumption Pitfalls

> Table header renamed 2026-08-24 to match the shared schema — "Trigger"→"Trigger condition",
> "Recovery"→"Correct approach", Source [Key] added. "Why it fails" kept as-is (mechanism,
> distinct from the canonical "How to recognize it" symptom column) — see
> `domain-expansion-guide.md` §3.3.

| Pitfall | Trigger condition | Why it fails | Correct approach | Source [Key] |
|---|---|---|---|---|
| Perimeter-to-area effect treated as the only size effect | EQE falls with smaller pixels and sidewall loss is declared | Current spreading, heating, optical collection, epitaxy and contact geometry can co-vary | Match material/process and fit P/A with electrical, lifetime and thermal controls | RinP2022_AlGaInP |
| Red and blue-green behavior merged | One SRV or diffusion length is quoted for all colors | AlGaInP and InGaN have different materials, defects, carrier transport and process responses | Split the model and literature evidence by material family | — (general technique knowledge) |
| RIE damage inferred from EQE alone | Etched pixels show lower EQE | EQE includes injection, IQE and LEE and is package-dependent | Add surface chemistry, leakage, TRPL and optical controls | Liu2025_Review |
| Native oxide treated as a universal mechanism | Surface oxidation is used as the sole explanation | Oxide composition, exposure, material and passivation are not fixed | Verify with surface analysis and an aging/treatment series | — (general technique knowledge) |
| Passivation assumed perfect | ALD, oxidation, ion implantation or another treatment is labelled “healing” | The treatment can leave traps, alter optics, or add an interface and stress | Compare coverage, chemistry, thickness, leakage, lifetime and aging | — (general technique knowledge) |
| Via-hole sidewall ignored | Via-hole etch is introduced but only the top mesa is modeled | New sidewalls change area, current path, leakage and optical loss | Add via geometry and sidewall passivation to the model and metrology | — (general technique knowledge) |
| TRPL lifetime equated with SRV | One lifetime trace is converted directly to SRV | Lifetime also depends on bulk, radiative, Auger, excitation and geometry terms | Use a rate model with multiple sizes, powers or temperatures | — (general technique knowledge) |
| EQE used to solve an underdetermined product | EQE changes and IQE or LEE is assigned uniquely | EQE combines injection, IQE and LEE | Add calibrated power, temperature, angle, optical modeling or independent IQE | — (general technique knowledge) |
| Current confused with current density | Larger and smaller pixels are compared at the same current | Local carrier density and heating differ with area | Report current density, active area, duty cycle and junction temperature | — (general technique knowledge) |
| Droop assigned to Auger by default | High-current roll-off is observed | Leakage, carrier overflow, crowding and self-heating can mimic it | Use temperature, pulse/DC, spectrum, lifetime and model discrimination | — (general technique knowledge) |
| Far-field collection artifact | A treatment changes measured angular output | Aperture, detector acceptance and polarization optics may have changed | Calibrate the angular system and compare with an optical model | — (general technique knowledge) |
| Exact process recipe copied | A packet lists BCl3/Ar, TMAH, oxidation or passivation steps | Etch and surface response are tool-, orientation- and stack-dependent | Preserve the recipe as source-specific until a primary process paper is available | — (general technique knowledge) |
| Unresolved packet term expanded by guess (TDEL, “front-light collection”) | User mentions TDEL or “front-light collection” without a source | The term appears with no definition and no original context; the source packet left both unresolved | Preserve the term as unresolved; request the original source context or run a targeted literature search before interpreting it (promoted from header prose 2026-08-25) | — (packet-intake guardrail) |

## 7a. Literature Anchors

1. “Advanced technologies in InGaN micro-LED fabrication to mitigate the sidewall effect,” *Light: Science & Applications* 14, 64 (2025). [DOI](https://doi.org/10.1038/s41377-025-01751-y)
2. “Recent Advances on GaN-Based Micro-LEDs,” *Micromachines* 14, 991 (2023). [DOI](https://doi.org/10.3390/mi14050991)
3. “Physical mechanisms on the size-effect in GaN-based Micro-LEDs,” *Micro and Nanostructures* 177, 207542 (2023). [DOI](https://doi.org/10.1016/j.micrna.2023.207542)
4. “Size effects of AlGaInP red vertical micro-LEDs on silicon substrate,” *Results in Physics* 36, 105449 (2022). [DOI](https://doi.org/10.1016/j.rinp.2022.105449)
5. “Improved performance of AlGaInP red micro-light-emitting diodes with sidewall treatments,” *Optics Express* 28, 5787–5793 (2020). [DOI](https://doi.org/10.1364/OE.384127)
6. “Shockley-Read-Hall and Auger non-radiative recombination in GaN based LEDs: A size effect study,” *Applied Physics Letters* 111, 022104 (2017). [DOI](https://doi.org/10.1063/1.4993741)

## 7b. Source Ledger (backfilled 2026-08-24 per `domain-expansion-guide.md` §3.2)

> Like `gan_power_device.md`, this profile already used resolvable DOI links throughout. This ledger tabulates the existing 7a citations.
>
> Legend — **Access tag**: `[full]` full text read · `[partial]` preview/excerpt/supplementary only ·
> `[abstract]` abstract/metadata only · `[secondary]` known only via another source citing it ·
> `[vendor]` manufacturer page.
> **Verification status**: ✅ Confirmed against the primary source · `~` Approximate (general claim
> corroborated, exact figure not independently pinned) · ⚠ Unconfirmed · ❌ Withdrawn.
> **Verified (date)** (`domain-expansion-guide.md` §3.7): when this row's claim was last checked
> against the primary source — not the source's own publication year.
>
> **2026-08-26 currency pass** (audit trail: `reports/2026-08-26-scientific-research-guide-source-currency-pass.md`).
> All six rows' bibliographic identity was independently re-resolved against the Crossref API, and
> checked for errata/retractions (none found). That pass: recovered the **author lists**, which every
> row previously omitted; **corrected a dropped word** in `APL2017_SRH_Auger`'s title (here and in
> 7a #6); **upgraded** `Liu2025_Review` from `[abstract]` to `[full]` via its open PMC copy and
> confirmed the §1.1 EQE-ranking caution at full-text level; and **repaired the "Used in" column**,
> which had been systematically under-populated — four keys are cited by Nodes 1–6 `Source [Key]`
> cells that the ledger did not list. Two rows' publisher pages blocked automated fetch, so their
> Node-level claims rest on secondary/abstract-tier corroboration and say so in-cell; that is a real
> limitation, not a full-text confirmation.

| Key | Full citation | Identifier | Access tag | Verification status | Verified (date) | Locator | Used in |
|---|---|---|---|---|---|---|---|
| Liu2025_Review | Liu, Z., Cao, H., Tang, X., Liu, T., Lu, Y., Jiang, Z., Xiao, N., Li, X., "Advanced technologies in InGaN micro-LED fabrication to mitigate the sidewall effect," Light Sci. Appl. 14, 64 (2025) | DOI: 10.1038/s41377-025-01751-y | [full] (open on PMC11762326, CC BY 4.0 — upgraded from [abstract] 2026-08-26) | ✅ Confirmed (2026-08-24 via search; 2026-08-26 re-resolved via Crossref + full text read on PMC — the §1.1 "EQE alone cannot rank fabrication techniques" caution is supported near-verbatim) | 2026-08-26 | Whole paper (full text) | §1.1 review citation; Node 5 EQE row; Node 6 "RIE damage inferred from EQE alone" row |
| Micromachines2023_GaNMicroLED | Zhang, Y., Xu, R., Kang, Q., Zhang, X., Zhang, Z.-h., "Recent Advances on GaN-Based Micro-LEDs," Micromachines 14, 991 (2023) | DOI: 10.3390/mi14050991 | [abstract] (MDPI page returned HTTP 403 to automated fetch 2026-08-26; the publisher-wide gold-OA status was not independently confirmed, so no upgrade was asserted) | ✅ Confirmed (Crossref: title, full author list, journal, volume, article no., year) | 2026-08-26 | Whole paper | 7a #2 |
| MicroNano2023_SizeEffect | Wu, Z., Ren, K., Zhang, X., An, Y., Yin, L., Lu, X., Guo, A., Zhang, J., "Physical mechanisms on the size-effect in GaN-based Micro-LEDs," Micro Nanostruct. 177, 207542 (2023) | DOI: 10.1016/j.micrna.2023.207542 | [abstract] (access level not re-observed 2026-08-26 — no Nodes 1–6 claim depends on this row) | ✅ Confirmed (Crossref: title, full author list, journal, volume, article no., year) | 2026-08-26 | Whole paper | 7a #3 |
| RinP2022_AlGaInP | Fan, K., Tao, J., Zhao, Y., Li, P., Sun, W., Zhu, L., Lv, J., Qin, Y., Wang, Q., Liang, J., Wang, W., "Size effects of AlGaInP red vertical micro-LEDs on silicon substrate," Results Phys. 36, 105449 (2022) | DOI: 10.1016/j.rinp.2022.105449 | [abstract] (ScienceDirect returned HTTP 403 to automated fetch 2026-08-26) | ✅ Confirmed for bibliographic identity (Crossref). ⚠ The 160/80/40/20/10 µm pixel series and the shrink-EQE trend are corroborated only at **secondary tier** (press coverage of this same study), not from the primary full text — do not cite as full-text-confirmed | 2026-08-26 · review-when: full text becomes accessible (then upgrade the pixel-series claim from secondary to primary) | Whole paper | Node 2 "Size and current scaling" row; Node 4 "Perimeter-to-area or size-effect fit" row; Node 5 "Pixel size" row (160/80/40/20/10 µm pixels); Node 6 "Perimeter-to-area effect treated as the only size effect" row |
| OE2020_RedPassivation | Wong, M. S., Kearns, J. A., Lee, C., Smith, J. M., Lynsky, C., Lheureux, G., Choi, H., Kim, J., Kim, C., Nakamura, S., Speck, J. S., DenBaars, S. P., "Improved performance of AlGaInP red micro-light-emitting diodes with sidewall treatments," Opt. Express 28, 5787–5793 (2020) | DOI: 10.1364/OE.384127 | [abstract] (Optica served only a JS shell 2026-08-26; abstract read from an indexing record) | ✅ Confirmed for bibliographic identity (Crossref; the end page 5793 was not independently re-confirmed and was not contradicted). Attribution consistent at abstract level — the Node 5 SRV row asserts no number, so no figure can be over-claimed from it | 2026-08-26 · review-when: full text becomes accessible | Whole paper | Node 4 "Passivation comparison" row; Node 5 "Surface recombination velocity" row |
| APL2017_SRH_Auger | Olivier, F., Daami, A., Licitra, C., Templier, F., "Shockley-Read-Hall and Auger non-radiative recombination in GaN based LEDs: A size effect study," Appl. Phys. Lett. 111, 022104 (2017) | DOI: 10.1063/1.4993741 | [abstract] (AIP full text paywalled; not accessed 2026-08-26) | ✅ Confirmed (Crossref identity; **title corrected 2026-08-26** — the word "A" was missing here and in 7a #6) | 2026-08-26 | Whole paper | Node 4 "Rate-equation or TRPL fit" row |

## Cross-Domain Links

### Closest Related Domain Profiles

| Related profile | Link | Boundary |
|---|---|---|
| Vertical GaN power devices | Shared GaN fabrication vocabulary, RIE/ALD/passivation and possible TCAD infrastructure | MicroLED metrics are recombination, optical extraction, current density and thermal; do not import power-device BV/RON criteria |
| Topological insulator / Bi2Se3 material | Shared surface-state and optical characterization vocabulary only in specialized experiments | A microLED sidewall state is not a topological surface state |
| Plasmonic waveguide | Shared optical mode, angular collection and near-field modeling vocabulary | LEE/EQE calibration and SPP propagation loss are different measurement problems |

### Cross-Domain Conflict Notes

| Issue / constraint | Other profile(s) involved | Potential conflict | AI confirmation question |
|---|---|---|---|
| RIE/passivation appears in both device families | gan_power_device.md | Similar process names do not imply identical sidewall chemistry, thermal budget, or success metric | “Is this process being optimized for power-device interface/blocking behavior or microLED recombination/optical behavior?” |
| Optical field or near-field language overlaps | plasmonic_waveguide.md | LEE/EQE and SPP propagation loss use different calibration and collection definitions | “Are we measuring pixel extraction or a bound plasmonic mode?” |
| Surface-state terminology overlaps | topological_insulator/bi2se3_material.md | A semiconductor sidewall defect is not a topological surface state | “What material and band-structure evidence supports the surface-state label?” |

(The packet's unresolved terms TDEL and “front-light collection” are guarded by the last Node 6
row above.)
