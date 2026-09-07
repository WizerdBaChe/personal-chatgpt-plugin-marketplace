---
xi: 1
what: "Silicon Photonics Packaging & Reliability (矽光子封裝與可靠度) — Silicon photonics packaging & reliability: module-level qualification, stress-test matrix, physics-of-failure models, CPO thermal architecture, failure-mechanism attribution"
tags: [srg-domain, 領域框架, base]
aliases: ["silicon photonics packaging", "photonic packaging", "光子封裝", "封裝可靠度", "CPO", "co-packaged optics", "共封裝光學", "optical engine", "reliability qualification", "可靠度驗證", "Telcordia", "GR-468", "GR-1221", "JEDEC JESD22", "HAST", "HTOL", "THB", "temperature cycling", "thermal shock", "accelerated life test", "加速壽命試驗", "acceleration factor", "Arrhenius", "Coffin-Manson", "Peck model", "Weibull", "delamination", "分層剝離", "underfill", "microbump", "hybrid bonding", "RDL", "warpage", "TIM", "thermal crosstalk", "熱串擾", "junction temperature", "thermal resistance", "failure mechanism", "failure analysis", "known-good die", "KGD"]
date: 2026-08-26
status: live
profile_type: base
parent: "-"
---
# Domain Profile: Silicon Photonics Packaging & Reliability (矽光子封裝與可靠度)

> Scope of applicability: The assembled photonic module treated as **one multiphysics system** —
> Si PIC, light source, driver/receiver IC, electrical interconnect, fiber interface, substrate/
> interposer, thermal path and packaging materials — and whether it holds its optical, electrical and
> mechanical specifications through manufacturing, operating life, and accelerated stress. Covers
> co-packaged optics (CPO, 共封裝光學) as the hardest instance of the problem.
> Scientific nature: Thermoelasticity and CTE-mismatch mechanics, moisture diffusion and
> hygro-mechanics of polymers, thermo-optics of guided-wave devices, physics-of-failure statistics
> (acceleration models, Weibull).
> Engineering nature: Reliability qualification against telecom/semiconductor standards, stress-test
> matrix design, failure analysis, thermal and mechanical co-design, testability, repairability and
> known-good-die strategy.
>
> **Domain boundary / cluster membership — this profile is the module/system-level reliability
> owner.** It is the fourth member of the **photonic-packaging** sibling cluster (split
> tabulated in `_routing.md` § Clusters, deliberately flat — no parent profile exists or should
> be built) and fills the hand-off slot that
> `fiber_chip_passive_alignment.md` reserved as "Photonic Packaging & Co-Packaged Optics (未建檔)".
> **That reserved slot is closed: this file IS the registered home of the "Photonic Packaging &
> Co-Packaged Optics" domain. Do not create a separate `cpo.md`** — CPO is the hardest operating
> point of this family, not a fifth member. The keyword-level split (this profile vs.
> `silicon_photonics_device_physics.md`, which also triggers on `CPO`) is tabulated in
> `_routing.md` § *Where "Photonic Packaging & Co-Packaged Optics" lives*.
> It does NOT own how the groove is cut (→ `v_groove_fabrication.md`), how the on-chip mode is
> expanded (→ `adiabatic_taper_ssc.md`), or how the fiber is placed and fixed (→
> `fiber_chip_passive_alignment.md`). Rule of thumb for routing: **which knob is being turned?**
> An assembly-process knob (groove geometry, mode size, datum chain, dispense/cure recipe) belongs to
> one of those three. A stress / qualification / lifetime knob (test matrix, acceleration model,
> thermal architecture, standard selection, failure-mechanism attribution) belongs here.
>
> Profile metadata:
> - Profile ID: PHOT-PKGREL-001
> - Profile version: 0.1 (first authoring; every source in the packet re-resolved to a primary
>   record — see §7b Provenance & correction log)
> - Last updated: 2026-08-26 (§3.7 currency pass: 26/27 rows attempted; the papers came back clean and two were re-read in full, but **seven bare JEDEC designations still carry no issue letter** — jedec.org blocked every fetch route, so they are marked unconfirmed rather than pinned by guesswork. JESD22-B103 ⚠→✅ as B103B.01; GR-1221 Issue 3 is current; IEC 61300-1 Ed. 5.1:2024 pinned)
> - Author(s) / Maintainer(s): User supplied the source packet (「方向 2」, compiled via a Perplexity
>   research session); restructured to the seven-node schema, language-normalized, and
>   citation-resolved into `scientific-research-guide/domains/` by Claude (Opus 5)
>
> Primary source types:
> - Textbooks: (not yet incorporated — recommend a microelectronics-packaging reliability text, e.g.
>   Suhir/Lau-class treatments of solder fatigue and interfacial stress, for the mechanics behind
>   Node 4's models)
> - Review articles: Tan et al. 2023 (*Frontiers of Optoelectronics*, CPO status/challenges);
>   Yang et al. 2026 (*Advanced Photonics Nexus*, CPO thermal management); Bender et al. 2024
>   (*Micromachines*, packaging reliability testing); Carroll et al. 2016 (*Applied Sciences*,
>   photonic packaging)
> - Methods / standards papers: Lam et al. 2008 (adhesive-bonded fiber-array reliability);
>   Uddin et al. 2006 (UV-cure delamination in V-groove); Tian et al. 2024 (hygroscopic vs. thermal
>   delamination driving forces); Komma et al. 2012 (Si thermo-optic coefficient)
> - Other (industry standards): Telcordia GR-468-CORE, GR-1221-CORE; JEDEC JESD22 family;
>   IEC 60068 / IEC 61300; MIL-STD-883
>
> Notes for AI use:
> - Intended use: cross-checking claims about what a photonic package's qualification actually
>   proves, whether an acceleration model is being applied to a mechanism it fits, how CPO changes
>   the thermal problem, and which observable is the earliest honest indicator of a given failure
>   mechanism.
> - **Validation status — read before reusing any citation from this profile.** The source packet was
>   an AI-research-tool output whose inline citations were opaque footnote indices with URLs. All
>   load-bearing ones were re-resolved at authoring time (2026-08-24). **Four attribution errors were
>   found and corrected**: one paper's first author was wrong (the CPO thermal-management review is
>   by Yang et al., not "D. Chen"), one adhesive-fiber-array paper was attributed to the wrong author
>   group (Lam/Uddin/Chan, not "J. Tian" — that surname belongs to a *different* cited paper), one
>   review's title was wrong ("…Reliability: A Review" → "…Reliability **Testing**"), and **two JEDEC
>   standard designations were mis-mapped** (JESD22-A108 is Temperature/Bias/Operating Life, not
>   High-Temperature Storage — that is A103), plus one Telcordia scope error (GR-1221 covers *passive
>   optical components*, not fiber/cable components). The mis-mapped designations and the scope error
>   survive in Node 6 as pitfalls, because they are exactly the errors a reader of the same secondary
>   literature will make. Do not re-import the original packet's attributions.
> - Optional external tool slot: if a local literature corpus or reference-manager MCP is available
>   (a Zotero MCP, `prism`, an Obsidian vault), prefer it for retrieving the full texts named in §7b —
>   several entries here are `[abstract]`-tagged only. Absent any such tool this profile is fully
>   usable from its own tables; §7b states exactly how much of each source was read.

---

## Citation convention (applies to Nodes 0–6)

Every inline citation is a human-resolvable `[Author Year]` or standard-designation key with a
matching row in the **Source Ledger (§7b)**; every quantitative claim states its conditions
(material system, method, temperature/humidity/wavelength, sample basis) in the same breath as the
number. Full rationale: `_template.md` "Citation convention" and `domain-expansion-guide.md` §3.2.

Claims marked `[synthesis]` are this profile's own derivation from cited premises or standard
engineering formalism, not something a single source states. Rows marked
`— (general engineering knowledge)` are textbook-level formalism (heat-conduction network, Weibull
CDF) that needs no specific source but also may not be attributed to one.

---

## 0. Terminology & Chinese glosses (added section — not part of the required seven nodes)

> Rationale for adding this node: the same convention as `fiber_chip_passive_alignment.md` §0 — the
> profile body is English (machine-consumed domain reasoning), and this table is the single place
> where the Chinese equivalents live, so a Chinese-language deliverable can be produced without
> re-guessing terminology. Preference order: 國家教育研究院樂詞網 official rendering > Taiwan
> semiconductor/packaging industry usage > literal translation. ⚠ marks a rendering in the source
> packet that is mainland-Chinese or Japanese-derived usage and wrong for a Taiwan-context thesis.

| English term | 中文（臺灣） | Meaning in this domain | Translation note |
|---|---|---|---|
| Silicon photonics (SiPh) | 矽光子 | Photonic integrated circuits built on a silicon platform | 大陸作「硅光子」 |
| Photonic integrated circuit (PIC) | 光子積體電路 | Waveguides, modulators, detectors and couplers integrated on one chip | 大陸作「光子集成電路」 |
| Optical engine (OE) | 光學引擎 | The compact transceiver subassembly of PIC + EIC + fiber interface | — |
| Co-packaged optics (CPO) | 共封裝光學 | Optical engine packaged with (or immediately adjacent to) the switch/compute ASIC | — |
| Electronic IC (EIC) / driver / TIA | 電子晶片／驅動器／轉阻放大器 | The electrical half of the optical engine | TIA = transimpedance amplifier 轉阻放大器 |
| Heterogeneous integration | 異質整合 | Combining Si, III–V, Ge, glass, polymer and CMOS parts in one package | — |
| Reliability qualification | 可靠度驗證（鑑定） | Proving a target use environment is met with defined samples, stresses, duration and failure criteria | 臺灣用「可靠度」；大陸用「可靠性」 |
| Reliability assurance | 可靠度保證 | The whole management chain: design → materials → process control → test → failure analysis | — |
| Failure mechanism | 失效機制 | The physical/chemical/thermal/mechanical process that causes degradation | — |
| Failure mode | 失效模式 | The observable symptom (IL rise, bump crack, delamination) | 機制 vs 模式 必須分開陳述 |
| Accelerated life test | 加速壽命試驗 | Elevated stress used to compress long-term degradation into test time | — |
| Highly accelerated stress test (HAST) | 高加速溫濕應力試驗 | Pressurized high-temperature/high-humidity moisture test | 對應 JESD22-A110（偏壓）／A118（無偏壓） |
| Pressure cooker test (PCT) / autoclave | 高壓蒸煮試驗（高壓釜試驗） | Saturated-steam moisture test, typically 121 °C / 2 atm / 100 % RH | ⚠ 常被誤稱為 HAST，條件與機制不同（見 Node 6） |
| Temperature cycling (TC) | 溫度循環試驗 | Repeated slow high/low excursions; drives CTE fatigue | 對應 JESD22-A104 |
| Thermal shock (TS) | 熱衝擊試驗 | Rapid transfer between temperature extremes; more severe transient stress | 對應 JESD22-A106 |
| High-temperature operating life (HTOL) | 高溫操作壽命試驗 | Powered/biased operation at elevated temperature | 對應 JESD22-A108（溫度／偏壓／操作壽命） |
| High-temperature storage (HTS) | 高溫儲存試驗 | Unpowered high-temperature ageing | 對應 JESD22-A103（⚠ 非 A108） |
| Temperature–humidity–bias (THB) | 溫濕偏壓試驗 | Steady-state 85 °C/85 % RH with bias applied | 對應 JESD22-A101 |
| Coefficient of thermal expansion (CTE) | 熱膨脹係數 | Fractional dimensional change per K; mismatch accumulates interfacial stress | — |
| Thermal resistance $R_\theta$ | 熱阻 | Resistance of the heat path from source to ambient, K/W | — |
| Junction temperature $T_j$ | 接面溫度 | Temperature of the active region/junction | 大陸作「結溫」 |
| Thermal interface material (TIM) | 導熱介面材料 | Compliant layer conducting heat across a mechanical joint | 大陸作「熱界面材料」 |
| Heat spreader / lid | 均熱片／封裝蓋 | Package-level heat-spreading and mechanical cover | — |
| Interposer | 中介層 | Silicon/glass/organic layer routing between die and substrate | — |
| Delamination | 分層剝離（脫層） | Loss of adhesion at a material interface | 兩種譯法皆通行，同一文件內擇一 |
| Interfacial adhesion | 界面附著性 | Resistance of an interface to separation | — |
| Underfill | 底部填膠 | Polymer filling the flip-chip die–substrate gap to redistribute bump stress | — |
| Microbump | 微凸塊 | Micro-scale die-to-die / die-to-interposer electrical interconnect | — |
| Hybrid bonding | 混合鍵合 | Simultaneous dielectric-to-dielectric and metal-to-metal direct bonding | 亦見「混成鍵合」 |
| Redistribution layer (RDL) | 重佈線層 | Metal/dielectric layers relocating die I/O to package interconnect | — |
| Warpage | 翹曲 | Out-of-plane distortion of die/substrate/package | — |
| Creep / stress relaxation | **潛變**／應力鬆弛 | Time-dependent deformation under sustained load | ⚠ 素材作「蠕變」，為大陸用法；臺灣機械工程官方用「潛變」 |
| Fatigue | 疲勞 | Damage accumulation under cyclic strain | — |
| Hygroscopic swelling | 吸濕膨脹 | Dimensional expansion of a polymer as it absorbs moisture | — |
| Hydrolysis | **水解** | Chemical scission of a polymer by water | ⚠ 素材作「加水分解」，為日文用法；臺灣化學用「水解」 |
| Ionic contamination | 離子污染 | Mobile ions enabling corrosion and leakage | — |
| Electrochemical migration | 電化學遷移 | Bias- and moisture-driven metal migration across an insulator | — |
| Electromigration | 電遷移 | Current-density-driven mass transport in a conductor | — |
| Intermetallic compound (IMC) | 介金屬化合物 | Brittle phase growing at solder–metal interfaces | — |
| Thermo-optic coefficient (TOC) | 熱光係數 | dn/dT; dominates Si waveguide and resonator wavelength drift | — |
| Thermal crosstalk | 熱串擾 | Heating of one component by a neighbouring source through the package | — |
| Optical misalignment | 光學對準偏移（失準） | Relative displacement of fiber/coupler/waveguide degrading IL or RL | 「對準」用法與 `fiber_chip_passive_alignment.md` §0 一致 |
| Insertion loss / return loss | 插入損耗／回波損耗 | The two primary optical observables of packaging degradation | — |
| Known-good die (KGD) | 已知良品晶粒 | Die screened as good *before* it is committed to a high-value assembly | — |
| Activation energy $E_a$ | 活化能 | Arrhenius temperature sensitivity of a thermally activated mechanism | — |
| Acceleration factor (AF) | 加速因子 | Ratio of use-condition life to stress-condition life for one mechanism | — |
| Characteristic life $\eta$ / shape parameter $\beta$ | 特徵壽命／形狀參數 | Weibull scale and shape | — |
| Censored data | 設限資料 | Units that had not failed when the test stopped | 報告時必須標明，不可當成「無失效即通過」 |

---

## 1. Theoretical Framework Anchoring

### Core first principles

| Scale/problem type | Foundational theory | Core physical quantity |
|------------|---------|-----------|
| Single-die steady-state heating | Lumped thermal-resistance network | $T_j = T_a + P_{\mathrm{diss}}R_{\theta JA}$ — valid only when one dominant serial heat path exists |
| Package/system thermal field (CPO) | Distributed conduction + convection with multiple sources | $T(x,y,z,t)$; the ASIC-to-photonics gradient and its time dependence under traffic-driven power |
| Optical response to temperature | Thermo-optic effect + cavity thermal expansion | $\dfrac{d\lambda_{\mathrm{res}}}{dT}\approx\lambda_{\mathrm{res}}\left(\dfrac{1}{n_{\mathrm{eff}}}\dfrac{dn_{\mathrm{eff}}}{dT}+\alpha_{\mathrm{eff}}\right)$ |
| Interface stress from a temperature excursion | Linear thermoelasticity with CTE mismatch | $\Delta\varepsilon_{\mathrm{CTE}}=(\alpha_i-\alpha_j)\Delta T$ → interfacial shear, warpage, bump strain |
| Optical consequence of mechanical drift | Coupling-interface kinematics × mode-overlap integral | $\{\Delta x,\Delta y,\Delta\theta\}(T)\Rightarrow\Delta IL(T)$ — the bridge to `fiber_chip_passive_alignment.md` |
| Moisture in polymers and at interfaces | Fickian diffusion + hygroscopic swelling + vapor pressure | $C(x,t)$; hygro-strain $\beta\Delta C$, comparable in magnitude to thermal strain [Tian2024] |
| Life extrapolation from accelerated stress | Physics-of-failure acceleration models | $AF$ per mechanism ($E_a$, $\Delta T$, $RH$ exponent $n$) [Bender2024] |
| Population variability and censoring | Weibull statistics | $\beta$ (shape), $\eta$ (characteristic life), censored-unit accounting |

### Inviolable physical constraints (the AI should warn the user here)

1. **An acceleration factor is valid only if the same failure mechanism dominates at both stress and
   use conditions.** $AF$ is a per-mechanism quantity, not a per-test one [Bender2024, Table 1]. If
   failure analysis has not confirmed mechanism identity, an extrapolated field lifetime is a number
   with no physical referent — and the error is one-sided: a stress that activates a *new* mechanism
   under-predicts field life for the mechanism you actually care about.
2. **Arrhenius does not apply to strain-driven fatigue.** Thermally activated diffusion, oxidation
   and chemical ageing take Arrhenius; cyclic plastic strain takes Coffin–Manson
   ($AF=(\Delta T_{\mathrm{stress}}/\Delta T_{\mathrm{use}})^{C}$ in the tabulated AF form)
   [Bender2024, Table 1]. Choosing an $E_a$ for a temperature-cycling result is a category error, not
   a conservative approximation.
3. **A single lumped $R_{\theta JA}$ cannot represent a CPO package.** The extreme power density of
   the ASIC together with the temperature sensitivity of the photonic components is what makes
   thermal management "a critical bottleneck for CPO performance and reliability" [Yang2026,
   Abstract]. One resistance number cannot express a gradient between two co-packaged components
   whose temperatures matter for different reasons.
4. **Hygroscopic strain is not a second-order correction to thermal strain.** For epoxy moulding
   compounds conditioned at 60 °C / 60 % RH, the hygroscopic-expansion strain equals the thermal
   expansion strain over 0–55 °C or 150–175 °C, and the delamination driving force is the *sum* of
   thermal, moisture and vapor-pressure strains [Tian2024, §2.1.2]. A dry thermal-cycling result
   therefore cannot bound interfacial delamination for a package that will see humidity.
5. **Optical alignment is a mechanical state variable of the package.** Any interface that moves at
   the sub-micron scale changes IL. "Electrically qualified" is not "optically qualified"; the
   optical readout must be part of the stress test, not a bookend to it. (Consequence: a
   qualification plan with no in-situ or intermittent optical measurement cannot attribute a drift to
   a stress step.) [synthesis, premise → `fiber_chip_passive_alignment.md` Node 1]
6. **Telcordia GR-468/GR-1221 are assurance *frameworks*, not pass/fail labels.** GR-468-CORE covers
   optoelectronic devices used in telecommunications equipment [GR-468]; GR-1221-CORE covers
   *passive* optical components [GR-1221]. A claim of "passed Telcordia" that does not state device
   category, test conditions, sample size, preconditioning, acceptance criteria and the failure-
   analysis flow is unverifiable and must not be treated as evidence.
7. **The waveguide's effective thermo-optic coefficient is not the bulk material's.** Bulk Si has
   $dn/dT\approx1.8\times10^{-4}\ \mathrm{K^{-1}}$ at 300 K, 1550 nm [Komma2012]; the resonance drift
   of a real device is set by $dn_{\mathrm{eff}}/dT$, which depends on mode confinement, cladding and
   package-induced stress. Substituting the bulk number for the device number silently mis-predicts
   heater power and drift budget. [synthesis]

> **Decision point (mandatory Tier 0 confirmation)**: when the user describes a packaging-reliability
> study, the AI must confirm:
> "Is your goal (A) **qualifying a specific build** against a standard (evidence that a product meets
> a use environment), (B) **establishing a causal chain** design/process variable → local
> stress/temperature/moisture field → named failure mechanism → measurable optical/electrical
> degradation (a research claim), or (C) **thermal-mechanical co-design** of a CPO architecture
> (choosing an architecture, not measuring one)?"
> The three goals correspond to entirely different work: (A) needs a standards-anchored test matrix,
> sample plan and acceptance criteria; (B) needs in-situ multi-domain measurement plus failure
> analysis, and is where the publishable claim lives; (C) needs coupled thermal/mechanical/optical
> modelling before any sample exists.

---

## 2. Measurement Tool Inventory

### 2.1 In-situ / intermittent optical–electrical readout

| Measurement target | Tool | Output information | Applicable conditions | Common misuse | Source [Key] |
|---------|------|---------|---------|---------|---------|
| Insertion loss (IL), return loss (RL) | Tunable laser + power meter / OSA, per channel; reflectometer for RL | $\Delta IL$, $\Delta RL$ vs. stress step | Needs a stated re-mating repeatability; the same fiber path pre/post | Reporting pre/post only, so reversible thermo-optic drift cannot be separated from irreversible damage | [synthesis] |
| Per-channel array behaviour | Multi-channel switch + per-channel scan | Worst-channel $\Delta IL$, channel distribution, failure location vs. array position | Fiber-array packages; requires channel-indexed data retention | Reporting mean IL for the array — the link budget is set by the worst channel | [synthesis], → `fiber_chip_passive_alignment.md` Node 6 |
| Polarization-dependent loss (PDL) | Polarization controller/scrambler + power meter | PDL (dB) drift | Edge couplers and any birefringent path; stress can change birefringence | Treating PDL drift as measurement noise instead of a stress-induced birefringence signal | [synthesis] |
| Resonance/spectral response | Tunable laser sweep or SLED + OSA | $\Delta\lambda_{\mathrm{res}}$, ER, spectral ripple | Ring/WDM devices; temperature must be recorded with every sweep | Quoting a resonance shift without the die temperature at which it was measured | [Komma2012], [Weituschat2020] |
| Modulator health | Transfer-curve sweep + VNA | $V_\pi$, ER, $S_{21}$ bandwidth, bias point | Bias and temperature stated per sweep | Attributing bias drift to the modulator when the local thermal environment moved | [synthesis] |
| Photodetector health | I–V + responsivity + dark-current measurement | Dark current, responsivity, bandwidth | Dark current is strongly temperature dependent — must be temperature-referenced | Comparing dark current across stress steps taken at different chuck temperatures | [synthesis] |
| Laser health | L–I–V + optical spectrum analyzer | Threshold current, slope efficiency, output power, wavelength | Same heat-sink temperature every read; TEC state recorded | Reading L–I–V at a different mount temperature and calling the difference degradation | [Yang2026] |
| Link-level function | BER tester / eye diagram | BER, eye margin under traffic | Requires the powered module — pairs with HTOL-type stress | Using BER as the *only* readout: it saturates (pass) long after IL has started drifting | [synthesis] |
| Electrical interconnect integrity | Daisy-chain/Kelvin resistance, TDR, S-parameters | $\Delta R_{\mathrm{contact}}$, discontinuity location, RF loss | Daisy chains must be designed into the test vehicle before build | Expecting to add interconnect monitoring after the package is assembled | [Bender2024] |
| Thermal path integrity | Transient thermal / structure-function measurement, IR thermography | $R_\theta$ per layer, $T_j$, surface temperature map | IR needs emissivity calibration and line of sight; lids block it | Using a single $R_{\theta JA}$ for a package with two dissimilar heat sources | [Yang2026], [Kurata2025] |

### 2.2 Structural and failure-analysis tools (destructive status is decisive for test ordering)

| Measurement target | Tool | Output information | Applicable conditions | Common misuse | Source [Key] |
|---------|------|---------|---------|---------|---------|
| Interface delamination | C-SAM / scanning acoustic microscopy | Delamination map per interface | **Non-destructive**; needs a couplant and an accessible acoustic path | Running C-SAM only at end of test, losing the stress step at which delamination initiated | [Bender2024] |
| Internal voids, cracks, bump shape | X-ray / micro-CT | Void fraction, crack presence, bump geometry | **Non-destructive**; resolution limits for the finest microbumps | Assuming an X-ray-clean bump is fatigue-free — cracks below resolution are missed | [Bender2024] |
| Cross-section evidence for a mechanism | Mechanical cross-section + SEM; FIB for site-specific | Crack path, IMC thickness, interface separation | **Destructive** — terminates the sample | Placing cross-section mid-sequence, destroying the unit whose post-stress optical drift was the point | [synthesis] |
| Adhesion / attach strength | Fiber pull test, die/bump shear test | Pull force (N), shear strength | **Destructive**; surface preparation dominates the result | Comparing adhesion numbers across builds with different cleaning processes as if the adhesive were the variable | [Lam2008] |
| Surface chemistry / corrosion products | XPS / EDS / SEM-EDX | Elemental and chemical-state maps | Semi-destructive (sample prep, vacuum); surface-sensitive | Concluding "no corrosion" from a surface scan of an unexposed region | [synthesis] |
| Adhesive cure state and index match | Refractive-index measurement, cure monitoring | Index vs. cladding, degree of cure | Applies to UV-cured fiber attach | Ignoring index mismatch: uneven UV curing from index contrast is a documented delamination origin | [Uddin2006] |

### 2.3 Environmental stress equipment and standard designations

> Designations are load-bearing here — the same nickname maps to different conditions. Verify the
> designation, not the nickname.

| Stress | Standard designation | Representative condition | Applicable conditions | Common misuse | Source [Key] |
|---------|------|---------|---------|---------|---------|
| Temperature cycling | JEDEC JESD22-A104 | −65 → 150 °C, 1000 cycles (packaged-device qualification example) | CTE-fatigue, cracking, misalignment; ramp rate and dwell must be stated | Quoting "1000 cycles" without the temperature range or ramp/dwell | [Bender2024, Table 3], [JESD22-A104] |
| Thermal shock | JEDEC JESD22-A106 | −55 → 125 °C, 1000 cycles | Severe transient thermomechanical loading; liquid vs. air transfer differs greatly | Reporting thermal shock as if it were temperature cycling | [Bender2024, Table 3], [JESD22-A106] |
| High-temperature storage | JEDEC JESD22-A103 | 150 °C, 1000 h, unpowered | Material ageing, interdiffusion, adhesive degradation | ⚠ Calling this "A108" — A108 is the *biased/operating* test | [Bender2024, Table 3], [JESD22-A103] |
| Temperature/bias/operating life (HTOL) | JEDEC JESD22-A108 | Elevated temperature under bias/operation | Powered-state device + package lifetime | Presenting an unpowered ageing result as HTOL evidence | [JESD22-A108] |
| Steady-state temperature–humidity–bias | JEDEC JESD22-A101 | 85 °C / 85 % RH, 1000 h | Moisture + bias coupled failures (leakage, corrosion, ECM) | Omitting bias and still calling it THB | [Bender2024, Table 3], [JESD22-A101] |
| Biased HAST | JEDEC JESD22-A110 | **130 ± 2 °C dry bulb / 85 ± 5 % RH / wet bulb 124.7 °C / 33.5 psia (≈2.3 atm absolute) / 96 h** — read from the standard's own §3.1 table 2026-08-26. Other lettered conditions exist (the standard's §7 requires a "test condition letter" to be specified) but were not legible in the excerpt obtained; the commonly-quoted 96–264 h span covers those other letters and is **not** confirmed here | Accelerated moisture ingress with bias | ⚠ Reporting 121 °C/100 % RH/2 atm as "HAST" — those are autoclave/PCT conditions. ⚠ Also: quoting a duration without its condition letter | [JESD22-A110], [Bender2024, Table 3] |
| Unbiased HAST | JEDEC JESD22-A118 | 110–130 °C / 85 % RH / ~2 atm, no bias | Moisture-driven delamination and corrosion without electrical drive | Using unbiased results to claim coverage of bias-driven mechanisms | [JESD22-A118] |
| Pressure cooker / autoclave (PCT) | JEDEC JESD22-A102 | 121 °C / 2 atm / 100 % RH, 200 h | Saturated-steam moisture screen | Treating PCT and HAST as interchangeable — condensation regime differs | [Bender2024, Table 3], [JESD22-A102] |
| Mechanical shock | JEDEC JESD22-B104 (superseded by B110A) | Peak acceleration, pulse duration, axes | Fiber/connector mechanical robustness | Reporting shock without axis count and pulse shape | [JESD22-B104] |
| Vibration, variable frequency | JEDEC **JESD22-B103B.01**, "Vibration, Variable Frequency" (designation and issue confirmed 2026-08-26 against JEDEC's own hosted page title; the earlier ⚠ flag is cleared — and this is the only JESD22 row in this profile whose issue is actually pinned) | Frequency band, g level, duration, axes | Field transport and in-rack vibration | Quoting the designation without the profile | [JESD22-B103] |
| Optoelectronic-device qualification framework | Telcordia GR-468-CORE (Issue 2, Sept 2004) | Framework: device categories, stress suites, criteria | Telecom-grade optoelectronic devices (laser, receiver, transceiver) | Citing it as a single pass/fail label (see Node 6) | [GR-468] |
| Passive-optical-component qualification framework | Telcordia GR-1221-CORE | Framework for passive optical components | Fiber arrays, connectors and other passive parts | ⚠ Describing it as a "fiber/cable" standard — its scope is passive optical *components* | [GR-1221] |
| Product-level environmental testing | IEC 60068 family | Temperature, humidity, vibration, shock procedures | Equipment/product level rather than component | Mixing component-level and product-level acceptance criteria in one claim | [IEC60068] |
| Fiber-optic interconnect test procedures | IEC 61300 family | Basic test and measurement procedures for interconnecting devices | Connectors, fiber interfaces | Assuming it covers the active PIC as well | [IEC61300] |
| High-reliability microelectronics methods | MIL-STD-883 | Test-method source for hi-rel packaging | Where a customer imposes it; not a photonics-specific suite | Treating it as a substitute for optoelectronic-specific criteria | [MIL-STD-883] |

---

## 3. Standard Modeling Toolchain

```
Material property data (CTE α, modulus E(T), Tg, moisture diffusivity D and solubility,
adhesive cure shrinkage)
→ Output: the constitutive inputs; nothing downstream is more trustworthy than these
    ↓
Thermal model: package/system CFD or FEA driven by a POWER MAP, not a single power number
→ Input: per-die power map P_ASIC(t), P_EIC, P_laser; TIM/lid/heat-spreader/cold-plate stack
→ Output: T(x,y,z,t), ASIC→photonics gradient, thermal crosstalk, R_θ per layer
→ Trust condition: validated against IR thermography or transient-thermal structure functions
    ↓
Thermomechanical FEA (may be sequentially coupled with a Fickian moisture-diffusion solve)
→ Input: T-field (and C-field) from above, plus cure-shrinkage initial strain
→ Output: warpage, interfacial shear/peel stress, bump plastic strain range Δεp, fiber displacement
→ Trust condition: interface stress is mesh- and material-model-sensitive — report a convergence check
    ↓
Optical model (thermo-optic + misalignment → observable)
→ Input: local ΔT at each optical device; Δx/Δy/Δθ at the coupling interface
→ Output: Δλ_res, ΔIL, ΔER — i.e. the quantities the experiment can actually measure
→ Trust condition: uses dn_eff/dT for the real waveguide, not bulk dn/dT [Komma2012]
    ↓
Physics-of-failure life models (Node 4) + Weibull population statistics
→ Input: Δεp (Coffin–Manson), T and RH histories (Arrhenius/Peck), failure times with censoring
→ Output: AF, projected field life, β/η per failure mode
→ Trust condition: one model per MECHANISM, and mechanism identity confirmed by failure analysis
    ↓
Qualification test matrix (Node 2.3) and acceptance criteria
→ Output: the stress suite, sample plan, readout schedule, and pass/fail rules that will be reported
```

**Handoff caution.** The chain is only as strong as the power map at the top: a CPO thermal model
driven by an average ASIC power cannot produce the traffic-dependent transient that drives
power-cycling fatigue in the field. Feed it a time-resolved workload power profile, or state
explicitly that the model bounds steady state only. [synthesis, premise → [Yang2026]]

---

## 4. Domain-Specific Fitting Methods

| Method | Applicable question | Applicable conditions | Common error | Correct approach | Source [Key] |
|---|---|---|---|---|---|
| Arrhenius acceleration $AF=\exp\left[\frac{E_a}{k_B}\left(\frac{1}{T_{\mathrm{use}}}-\frac{1}{T_{\mathrm{stress}}}\right)\right]$ | How much does a higher temperature compress the life of *one* thermally activated mechanism? | Single dominant thermally activated mechanism (diffusion, oxidation, chemical ageing, IMC growth) | ⚠️ Choosing a convenient $E_a$ when the mechanism is unidentified; applying it to fatigue or to a mixed-mechanism population | Identify the mechanism by failure analysis first, then take $E_a$ from a mechanism-matched source (e.g. wire-bond-related failures 0.7–1.0 eV; electromigration 0.8 eV/atom in the Black-equation treatment). Report the $E_a$ used and its provenance beside every projected lifetime | [Bender2024, Table 1, §3.1, §3.2.2] |
| Coffin–Manson (low-cycle fatigue), strain form $N_f=C(\Delta\varepsilon_p)^{-m}$; tabulated AF form $AF=(\Delta T_{\mathrm{stress}}/\Delta T_{\mathrm{use}})^{C}$ | How many thermal cycles until a solder joint / microbump / metal interconnect fails? | Cyclic plastic strain dominates; a $\Delta\varepsilon_p$ estimate exists (usually from FEA) | ⚠️ Reporting an $N_f$ from the $\Delta T$ form while claiming it describes a *fiber-alignment* failure — the model describes the metallic/mechanical member, not the optical consequence | Use it for the mechanical member, then convert to the optical observable through a separate displacement→$\Delta IL$ model. State $C$/$m$ provenance; they are material- and structure-specific calibrations, not constants | [Bender2024, Table 1] |
| Peck temperature–humidity $AF=\left(\frac{RH_{\mathrm{stress}}}{RH_{\mathrm{use}}}\right)^{n}\exp\left[\frac{E_a}{k_B}\left(\frac{1}{T_{\mathrm{use}}}-\frac{1}{T_{\mathrm{stress}}}\right)\right]$ | How does a humidity test map onto field humidity exposure? | Moisture-driven mechanism, non-condensing, same mechanism at both conditions. Tabulated parameters: $n=3$, $E_a=0.9$ eV | ⚠️ Extrapolating from HAST/PCT where pressure, condensation and ionic transport differ from the use environment, without checking mechanism identity | Confirm by failure analysis that stress and use failures share a mechanism; state $n$ and $E_a$ used; treat pressurized-steam results as a screen, not as a calibrated field-life projection | [Bender2024, Table 1] |
| Eyring temperature–voltage $AF=AF(T)\exp[B(V_{\mathrm{stress}}-V_{\mathrm{use}})]$ | How does bias acceleration combine with temperature? | Bias-driven mechanisms (dielectric, ECM) with a calibrated $B$ | ⚠️ Applying a voltage term to an unbiased test result | Use only where the stress actually applied bias (JESD22-A101/A110), and report $B$'s source | [Bender2024, Table 1] |
| Weibull $F(t)=1-\exp[-(t/\eta)^{\beta}]$ | How is the failure population distributed; does $\beta$ indicate infant mortality, random, or wear-out? | Failure times for one failure mode; censoring explicitly handled | ⚠️ Fitting a Weibull to a zero-failure or few-failure test and quoting $\eta$ as if it were measured; pooling two failure modes into one fit | With no failures, report a lower confidence bound on life from the censored data instead of fitting; with mixed modes, fit per mode or use a competing-risk treatment. Always report sample size and censoring | — (general engineering knowledge) |
| Optical-drift trend fitting ($\Delta IL$ vs. stress step / time) | Is this drift reversible thermo-optic behaviour, monotonic degradation, or a step change? | Requires in-situ or per-step readout with the same optical path and stated repeatability | ⚠️ Fitting a trend line through pre/post pairs only — a step change and a slow creep are indistinguishable with two points | Take per-step data plus a return-to-room-temperature reading each step; classify by shape (hysteresis loop = reversible thermo-mechanics; monotonic = creep/ageing; step = fracture/delamination event) | [synthesis] |

---

## 5. Domain-Specific Quality Metrics

| Metric | Abbreviation | Physical meaning | Typical value range | Conditions (material/method/wavelength/temp…) | Source [Key] |
|------|------|---------|------------|------|------|
| Insertion-loss drift | $\Delta IL$ | $IL_{\mathrm{post}}-IL_{\mathrm{pre}}$; the primary packaging-degradation observable | Acceptance threshold is set per device category by the applicable framework and the product spec. The widely-cited passive-optical-component pass criterion is **±0.5 dB** (`~` — see §7b: not read from the standard document) | Post-environmental-stress change for the passive-optical-component category under GR-1221; a *threshold*, not a measured typical value. Every report must additionally state: stress step, wavelength, polarization/TE-TM, channel index, and the setup's re-mating repeatability | [GR-1221], [GR-468], [synthesis] |
| Polarization-dependent-loss drift | $\Delta PDL$ | Change in PDL after stress; sensitive to stress-induced birefringence | **±0.2 dB** pass criterion (`~`, same caveat as the row above) | Same category and basis as the IL criterion above — a threshold, not a measured typical value | [GR-1221] |
| Worst-channel insertion-loss drift | $\max_i \Delta IL_i$ | The array metric that the link budget actually sees | Report alongside $\sigma(IL_i)$ and the channel index of the worst unit | Multi-channel FAU packages; per-channel data must be retained, not averaged | [synthesis], → `fiber_chip_passive_alignment.md` Node 6 |
| Return-loss drift | $\Delta RL$ | Change in reflected power; sensitive to gaps, facet damage, index changes | Product-spec dependent | Same path and connector state pre/post; state whether an index-matching medium is present | [synthesis] |
| Resonance thermal drift | $d\lambda_{\mathrm{res}}/dT$ | Wavelength shift per kelvin of a Si resonator | ≈ 68.2 pm/K near 1550 nm for a silicon microring (⚠ single-source, see §7b) | Si microring, modelling study of microring thermometry, ~1550 nm | [Weituschat2020] |
| Bulk-silicon thermo-optic coefficient | $dn/dT$ | Material-level driver of all Si thermal drift | $\approx1.8\times10^{-4}\ \mathrm{K^{-1}}$ | Bulk Si, 1550 nm, 300 K, interferometric (Fabry–Pérot etalon) measurement — **not** the device $dn_{\mathrm{eff}}/dT$ | [Komma2012] |
| Passive athermalization | — | Negative-TOC cladding compensating Si's positive TOC | Demonstrated as a concept; quantitative performance is design-specific | Liquid-crystal cladding on Si photonic devices (concept-level claim, abstract-verified only) | [Ptasinski2014] |
| Temperature-cycling stress level | TC | Cyclic thermomechanical loading level | −65 → 150 °C, 1000 cycles | Packaged-device qualification example; 45 units/lot × 3 lots sample plan (⚠ sample plan single-source) | [Bender2024, Table 3] |
| Thermal-shock stress level | TS | Rapid-transition thermomechanical loading | −55 → 125 °C, 1000 cycles | Same table/basis as above | [Bender2024, Table 3] |
| Steady-state damp-heat with bias | THB | Moisture + bias coupled ageing | 85 °C / 85 % RH, 1000 h | Packaged-device qualification example (JESD22-A101 conditions) | [Bender2024, Table 3], [JESD22-A101] |
| Biased-HAST stress level | HAST | Pressurized accelerated moisture stress | 130 °C / 85 % RH, 100 h as a qualification example [Bender2024]. The standard's own condition, read from its §3.1 table 2026-08-26: **130 ± 2 °C / 85 ± 5 % RH / wet bulb 124.7 °C / 33.5 psia / 96 h** — note 33.5 psia is ≈2.3 atm absolute, so the widely-quoted "~2 atm" is a rounding, not the specified value | Non-hermetic packaged devices | [Bender2024, Table 3], [JESD22-A110] |
| Autoclave/PCT stress level | PCT | Saturated-steam moisture screen | 121 °C / 2 atm / 100 % RH, 200 h | Distinct condition set from HAST — see Node 6 | [Bender2024, Table 3], [JESD22-A102] |
| High-temperature storage level | HTS | Unpowered high-temperature ageing | 150 °C, 1000 h | JESD22-A103 conditions | [Bender2024, Table 3], [JESD22-A103] |
| Peck-model parameters | $n$, $E_a$ | Humidity exponent and activation energy for temperature–humidity acceleration | $n=3$, $E_a=0.9$ eV | As tabulated for the Peck AF model in a packaging-reliability review; not a universal constant | [Bender2024, Table 1] |
| Activation energy, wire-bond-related failures | $E_a$ | Arrhenius sensitivity of that mechanism | 0.7–1.0 eV | Wire-bond failure discussion in a packaging-reliability review | [Bender2024, §3.1] |
| Activation energy, electromigration | $E_a$ | Black-equation activation energy | 0.8 eV/atom | Electromigration treatment in the same review | [Bender2024, §3.2.2] |
| Hygroscopic-vs-thermal strain equivalence | — | Whether moisture strain is negligible against thermal strain | **Not negligible**: equal to thermal strain over 0–55 °C or 150–175 °C | Epoxy moulding compound (EMC), conditioned at 60 °C / 60 % RH | [Tian2024, §2.1.2] |
| High-temperature operating capability (SiPh transceiver) | — | Demonstrated harsh-environment operating capability of a SiPh transceiver | Reported for >100 °C environments, in excess of ten-year operation | Silicon-photonics optical transceiver, title-level claim (abstract access only) | [Kurata2025] |

> **Suspicious-range guidance.** Both directions need confirmation before interpretation: (a) a
> post-stress $\Delta IL$ *smaller than the measurement setup's own re-mating repeatability* is not a
> demonstration of stability — it is an unreported noise floor; (b) an abrupt single-step $\Delta IL$
> with no corresponding C-SAM or cross-section evidence is more often a measurement/handling artifact
> (connector, patch cord, contamination) than a package failure. Ask for the repeatability figure and
> the structural evidence before either result is written up. [synthesis]

---

## 6. Common Assumption Pitfalls

| Pitfall | Trigger condition | How to recognize it | Correct approach | Source [Key] |
|------|---------|---------|---------|---------|
| "Passed Telcordia" as a standalone claim | User writes that a package/module "passed GR-468" or "is Telcordia qualified" | No device category, condition set, sample size, preconditioning, acceptance criteria or FA flow appears anywhere near the claim | Treat GR-468/GR-1221 as assurance *frameworks*. Require the six missing items before the claim can be used as evidence; in a paper, print the actual conditions and criteria applied | [GR-468], [GR-1221] |
| GR-1221 described as a fiber/cable standard | User cites GR-1221-CORE for fiber or cable reliability | The stated scope in the user's text says "光纖／光纜元件" or "fiber/cable components" | GR-1221-CORE's scope is **passive optical components**; GR-468-CORE covers optoelectronic devices. **This exact error was present in the source packet for this profile** | [GR-1221], [GR-468] |
| PCT conditions reported as HAST | A "HAST" condition of 121 °C / 100 % RH / 2 atm appears | The RH is 100 % and the temperature is 121 °C — that is the saturated-steam autoclave point, not the HAST point | JESD22-A110 HAST practice is ~130 °C / 85 % RH / ~2 atm; 121 °C/2 atm/100 % RH is PCT (JESD22-A102). Condensation and ionic-transport regimes differ, so the acceleration models are not interchangeable. Report which was run | [JESD22-A110], [JESD22-A102], [Bender2024, Table 3] |
| THB conditions reported as HAST | A "HAST" condition of 85 °C / 85 % RH appears, with or without stated bias | The temperature is 85 °C, not ~130 °C, and no pressurization is stated | JESD22-A101 steady-state THB is 85 °C / 85 % RH (biased); JESD22-A110 HAST is a *pressurized* ~130 °C / 85 % RH / ~2 atm condition. 85/85 is the un-pressurized, lower-temperature test — a materially milder stress than HAST, so the two acceleration factors and exposure durations are not interchangeable. This is the same mislabeling shape as the 121 °C/100 % RH/2 atm-as-HAST row above, one condition set over | [JESD22-A101], [JESD22-A110], [Bender2024, Table 3] |
| "96 h HAST ≈ 1000 h of 85/85" quoted with no precondition | User justifies a short HAST as equivalent to a 1000 h THB | The equivalence appears as a bare ratio, with nothing said about how long the part takes to reach moisture-absorption equilibrium | The standard states this equivalence **only for parts that reach absorption equilibrium in 24 h or less**; parts needing longer at 130 °C/85 % RH must have the duration extended appropriately. Ask for the equilibration time before accepting the equivalence — for a thick or heavily-filled optical package it is the load-bearing assumption, and it is the one people drop | [JESD22-A110 §3.1 note 4] |
| HAST run above the moulding compound's wetted glass transition | A "HAST passed" result on a plastic-encapsulated or polymer-overmoulded part, with no Tg discussion | Nothing states the compound's effective Tg **under moisture**, only its dry Tg (if anything) | The standard itself cautions that moisture lowers the effective Tg, and that stressing above it can produce failure mechanisms **unrelated** to standard 85/85 — i.e. the acceleration model quietly stops applying. A HAST result above the wetted Tg is not a scaled-up 85/85 result; it is a different experiment | [JESD22-A110 §3.1 note 5] |
| HAST reported without its bias mode or die-temperature rise | A biased-HAST result gives conditions and duration but not whether bias was continuous or cycled, nor ΔT_ja | Two "130 °C/85 % RH/96 h biased HAST" results are compared as if identical | The standard makes the choice conditional and requires reporting: ΔT_ja < 50 °C **or** < 200 mW per DUT → continuous bias, no ΔT report; ΔT_ja ≥ 50 °C or ≥ 200 mW (and ΔT < 100 °C) → continuous, but ΔT_ja **must** be reported; ΔT_ja ≥ 100 °C → **cycled** bias and report. Cycled period: 2 h for packages ≥2 mm thick, 30 min for <2 mm, 50 % duty cycle. Without these, two HAST results are not comparable | [JESD22-A110 §3.2] |
| Electrical readout taken outside the post-HAST window | A pass is claimed from a measurement made days after the chamber | No date/time gap between end of ramp-down and electrical test is stated | Moisture desorbs after removal, so the standard bounds the readout: electrical test **within 48 h** of the end of ramp-down (and return-to-stress within 96 h for interim readouts). Sealing parts in moisture-barrier bags **without desiccant** runs the window clock at 1/3 speed, extending it to 144 h / 288 h. A measurement outside the window is not a valid readout of that stress | [JESD22-A110 §4.5] |
| Wrong JEDEC designation for the unpowered ageing test | User maps JESD22-A108 to "high-temperature storage" | The test description says unpowered/no-bias but the cited designation is A108 | A103 is High Temperature Storage Life; A108 is Temperature, Bias, and Operating Life. The distinction is whether bias-driven mechanisms were exercised at all. **This error was present in the source packet** | [JESD22-A103], [JESD22-A108] |
| Arrhenius applied with an assumed $E_a$ | User projects field life from an HTS/HTOL result and cannot name the mechanism | An $E_a$ appears with no mechanism attached, or a single $E_a$ is used for a mixed failure population | Identify the mechanism by FA first; take a mechanism-matched $E_a$ and report its provenance. If the mechanism is unknown, report the test result, not a projected lifetime | [Bender2024, Table 1] |
| Uniform-chamber test treated as representative of CPO field conditions | User plans TC/THB in a chamber and calls it a CPO reliability study | The test plan has no ASIC power map and no traffic-driven power cycling | The CPO-specific driver is the ASIC's extreme power density beside temperature-sensitive photonics [Yang2026]. Add workload-driven power cycling and a spatially resolved temperature measurement, or explicitly scope the claim to uniform-temperature behaviour | [Yang2026] |
| Mean IL reported for a fiber array | Multi-channel package results summarized as an average | No worst-channel figure, no per-channel table, no channel-index map | Report $\max_i\Delta IL_i$, the distribution, and where the worst channel sits (edge, near-hotspot, specific pitch) — the failure is usually channel-selective | [synthesis], → `fiber_chip_passive_alignment.md` |
| Humidity treated as an electrical-only stress | User's rationale for THB/HAST is corrosion and leakage only | The mechanical/interface section of the plan cites thermal cycling alone | Hygroscopic swelling is a mechanical driving force of comparable magnitude to thermal expansion (EMC at 60 °C/60 % RH: equal over 0–55 °C or 150–175 °C), and delamination is driven by the *sum* of thermal, moisture and vapor-pressure strains | [Tian2024, §2.1.2] |
| Adhesive failure framed as a materials-selection problem | User proposes to fix fiber-attach drift by changing adhesive brand/type | Nothing in the plan controls surface preparation or cure uniformity | Two process variables dominate published fiber-array attach reliability: bonded-surface contamination (plasma cleaning improves adhesion and reliability) [Lam2008] and uneven UV cure driven by adhesive–cladding index contrast [Uddin2006]. Fix the process before the material | [Lam2008], [Uddin2006] |
| Bulk $dn/dT$ used as the device thermal drift coefficient | User computes heater power or drift budget from $1.8\times10^{-4}\ \mathrm{K^{-1}}$ | A bulk material constant appears in a device-level drift calculation with no confinement/cladding correction | Use $dn_{\mathrm{eff}}/dT$ for the actual waveguide/resonator, and state how it was obtained (measurement or mode solve). Bulk Si at 1550 nm, 300 K is the *material* premise, not the device answer | [Komma2012] |
| Weibull fitted to a zero-failure test | User reports $\beta$ and $\eta$ from a qualification run where nothing failed | Suspiciously tidy parameters, no failure count stated, no censoring discussion | With no failures, report a censored-data lower confidence bound on life instead of fitting; state sample size and test duration. A fit with no failures is a number invented by the fitting routine | — (general engineering knowledge) |
| Pre/post-only optical readout | Stress plan measures IL before and after the chamber | The data set has exactly two points per unit per stress | Add per-step and return-to-room readings; only then can reversible thermo-optic drift, monotonic creep, and step-change fracture be distinguished (Node 4, last row). Optical metrics are the *earliest* indicator available in a photonic package — using them only as a bookend wastes their main advantage | [synthesis] |
| Destructive analysis scheduled mid-sequence | Test plan lists cross-section or pull test before the last stress step | The same unit is expected to yield post-stress optical data after a destructive step | Order non-destructive first (optical readout → C-SAM → X-ray), destructive last; or allocate separate sacrificial units per step and say so in the sample plan | [synthesis] |
| Serviceability assumed to be a manufacturing detail | User compares CPO with pluggable optics on loss/power only | No mention of KGD, burn-in placement, test access, rework or replacement granularity | In a high-value co-packaged assembly, field failure cannot be handled by swapping a module; KGD strategy, pre-assembly screening, test access and rework path change the optimal package architecture, so they belong in the reliability design, not downstream of it | [YangHung2025], [Tan2023] |

---

## 7a. Literature Anchors

| Type | Reference | Why it matters |
|------|------|-------|
| Review (domain entry point) | Carroll, L., et al., "Photonic Packaging: Transforming Silicon Photonic Integrated Circuits into Photonic Devices," *Applied Sciences* 6(12), 426 (2016) | The standard orientation to what photonic packaging has to solve simultaneously — optical alignment, electrical interconnect and thermal management — and why it is the industrialization bottleneck for Si PICs |
| Review (CPO architecture) | Tan, M., et al., "Co-packaged optics (CPO): status, challenges, and solutions," *Frontiers of Optoelectronics* 16, 1 (2023) | The comprehensive state-of-the-art survey of silicon-platform CPO, framing it as an interdisciplinary problem spanning devices, ICs, packaging, co-simulation and standardization |
| Review (CPO thermal) | Yang, Z., et al., "Thermal management in copackaged optics: from device assembly to system operation," *Advanced Photonics Nexus* 5(3), 034001 (2026) | The most directly on-point review for this profile: laser and fiber-array packaging thermal reliability, chip- and package-level thermal design, TIM and module cooling, in one framework |
| Review (packaging reliability method) | Bender, E., Bernstein, J.B., Boning, D.S., "Modern Trends in Microelectronics Packaging Reliability Testing," *Micromachines* 15(3), 398 (2024) | The shared test-and-model vocabulary: acceleration models with parameters (Table 1) and the standardized qualification condition set (Table 3) that this profile's Node 5 quotes |
| Qualification framework | Telcordia GR-468-CORE, *Generic Reliability Assurance Requirements for Optoelectronic Devices Used in Telecommunications Equipment* (Issue 2, Sept 2004) | The baseline framework for optoelectronic device qualification, and the document most often cited without its conditions — read it before citing it |
| Primary study (fiber attach) | Lam, K.W., Uddin, M.A., Chan, H.P., "Reliability of adhesive bonded optical fiber array for photonic packaging," *J. Optoelectron. Adv. Mater.* 10(10), 2539–2546 (2008) | The specific link from packaging *process* (surface contamination, plasma cleaning) to fiber-array reliability under environmental and mechanical stress |

---

## 7b. Source Ledger

> Legend — **Access tag**: `[full]` full text read · `[partial]` preview/excerpt/supplementary only ·
> `[abstract]` abstract/metadata only · `[secondary]` known only via another source citing it.
> **Verification status**: ✅ Confirmed against the primary record · `~` Approximate (corroborated in
> general; exact figure not independently pinned) · ⚠ Unconfirmed · ❌ Withdrawn.

> **Verified (date)** (`domain-expansion-guide.md` §3.7): when this row's claim was last checked
> against the primary source — not the source's own publication year.
>
> **2026-08-26 currency pass** (audit trail: `reports/2026-08-26-scientific-research-guide-source-currency-pass.md`).
> 26 of the 27 rows were attempted. The papers came back clean: 10 rows re-resolved against
> machine-readable records, with [Bender2024] and [Tian2024] re-read in full via PMC — every Table 1 /
> Table 3 / §2.1.2 number this profile quotes matches its source verbatim. **The standards did not.**
> Seven bare JEDEC designations (A101, A102, A103, A104, A108, A110, A118) still name **no issue
> letter**, which is precisely the §3.7 version-pinning defect: without the issue, a `review-when: the
> next revision` note is undecidable. jedec.org and every reseller mirror returned HTTP 403 to this
> pass, so those rows are marked **not confirmed** rather than pinned by guesswork — circumstantial
> evidence that later revisions exist is reported in the audit trail, not asserted here. What *was*
> settled: [JESD22-B103] went ⚠ → ✅ (B103B.01, Vibration/Variable Frequency, from JEDEC's own hosted
> page title), [GR-1221] Issue 3 is current (not Issue 2), [GR-468] Issue 2 (2004) remains current with
> no Issue 3, and [IEC61300]'s current edition is 5.1:2024.

| Key | Full citation | Identifier (DOI/arXiv/URL/standard no.) | Access tag | Verification status | Verified (date) | Locator | Used in (Node/row) |
|---|---|---|---|---|---|---|---|
| [Carroll2016] | Carroll, L., Lee, J.-S., Scarcella, C., Gradkowski, K., Duperron, M., Lu, H., Zhao, Y., Eason, C., Morrissey, P., Rensing, M., Collins, S., Hwang, H., O'Brien, P., "Photonic Packaging: Transforming Silicon Photonic Integrated Circuits into Photonic Devices," *Applied Sciences* 6(12), 426 (2016) | DOI 10.3390/app6120426 | [abstract] | ✅ Identity, full author list, venue, article number and DOI confirmed 2026-08-24 via Crossref (the packet's author field, "P. M. et al.", was wrong) | 2026-08-26 — re-resolved against the Crossref API (identity, full author list, venue, article number, DOI); no erratum/retraction | Article metadata | 7a |
| [Tan2023] | Tan, M., Xu, J., Liu, S., Feng, J., Zhang, H., Yao, C., Chen, S., et al., "Co-packaged optics (CPO): status, challenges, and solutions," *Frontiers of Optoelectronics* 16, 1 (2023) | DOI 10.1007/s12200-022-00055-y | [abstract] | ✅ Identity, authors, venue and abstract confirmed 2026-08-24 (Crossref + Semantic Scholar). The packet's *quantitative* claim that switch-die power greatly exceeds the CPO module's photonic power is **not** supported by anything read here — see correction log | 2026-08-26 — re-resolved via Crossref; the full 32-author list was retrieved and this row's truncated list matches its order exactly; no erratum/retraction | Abstract | 6 (serviceability row), 7a |
| [Yang2026] | Yang, Z., He, G., Li, Y., Sun, Y., Luo, W., Zhang, W., "Thermal management in copackaged optics: from device assembly to system operation," *Advanced Photonics Nexus* 5(3), 034001 (2026) | DOI 10.1117/1.APN.5.3.034001 | [abstract] | ✅ Identity/authors/venue confirmed via Crossref; abstract retrieved verbatim via Semantic Scholar. Full text blocked by the publisher's bot filter — body claims not read | 2026-08-26 (identity only) — authors/venue re-resolved via Crossref; the publisher's bot filter still blocks the body, so only the quoted abstract sentence is read. `review-when:` the full text becomes fetchable | Abstract ("extreme power density of ASICs, together with the temperature sensitivity of photonic components, makes thermal management a critical bottleneck for CPO performance and reliability") | 1 (constraint 3), 2.1 (laser, thermal path), 3, 6 (uniform-chamber row), 7a |
| [Kurata2025] | Kurata, K., Kobayashi, S., Nakamura, T., Yashiki, K., Muto, T., Kuwata, M., Okamoto, D., Hagihara, Y., Pitwon, R., "Achieving High Reliability in Silicon Photonics Optical Transceivers for Harsh Environments Over 100 °C in Excess of Ten-Year Operation," *IEEE Trans. Components, Packaging and Manufacturing Technology* **15**(8), 1592–1600 (2025) | DOI 10.1109/TCPMT.2025.3549758; IEEE Xplore doc. 10922121 | [abstract] | ✅ Title, venue and DOI confirmed 2026-08-24; co-author list not enumerated | 2026-08-26 — **upgraded**: the full 9-author list plus volume/issue/pages were resolved via Crossref (this row previously carried "et al." and no volume/issue/pages) | Title/abstract | 2.1 (thermal path), 5 (high-temperature capability) |
| [YangHung2025] | Yang, Y.-T., Hung, C.-M., "Heterogeneous Integration in Co-Packaged Optics," *IEEE J. Emerging and Selected Topics in Circuits and Systems* 15(3), 427–437 (2025) | IEEE Xplore doc. 11087222 | [abstract] | `~` Title, venue, volume/issue/pages confirmed via the Xplore listing; author initials taken from that listing and not independently re-checked | 2026-08-26 — **upgraded from `~`**: the full author names (Yu-Tao Yang, Chih-Ming Hung), title, venue and volume/issue/pages were independently corroborated this pass | Abstract (multi-physics electrical/optical/thermal/mechanical/material interactions) | 6 (serviceability row) |
| [Bender2024] | Bender, E., Bernstein, J.B., Boning, D.S., "Modern Trends in Microelectronics Packaging Reliability Testing," *Micromachines* 15(3), 398 (2024) | DOI 10.3390/mi15030398; PMC10972392 | [full] | ✅ Identity confirmed via Crossref; Table 1/Table 3 values and the §3.1/§3.2.2 activation energies retrieved from the PMC full text 2026-08-24. The stress conditions independently corroborate the JEDEC designations searched separately. **Title corrected**: the packet recorded "…Reliability: A Review" | 2026-08-26 — identity re-resolved via Crossref and the **full text re-read** via PMC: Table 1 (Peck n=3, Ea=0.9 eV; Arrhenius; Coffin–Manson ΔT-ratio form; Eyring) and Table 3 (TC −65→150 °C/1000 cyc; TS −55→125 °C/1000 cyc; HTS 150 °C) all reproduce verbatim — every number this profile quotes matches, with its conditions | Table 1 (AF models, Peck n=3, Ea=0.9 eV); Table 3 (TC/TS/THB/PCT/HAST/HTS conditions, 45 units/lot × 3 lots); §3.1 (wire-bond Ea 0.7–1.0 eV); §3.2.2 (EM Ea 0.8 eV/atom) | 1 (constraints 1–2), 2.2, 2.3, 4 (all AF rows), 5 (stress levels, Ea rows), 6, 7a |
| [Tian2024] | Tian, W., Chen, X., Zhang, G., Chen, Y., Luo, J., "Delamination of Plasticized Devices in Dynamic Service Environments," *Micromachines* 15(3), 376 (2024) | DOI 10.3390/mi15030376; PMC10972266 | [full] | ✅ Identity and the hygroscopic-vs-thermal strain statement retrieved from the PMC full text 2026-08-24, with conditions (EMC, 60 °C/60 % RH) | 2026-08-26 — identity re-resolved via Crossref and the **full text re-read** via PMC: §2.1.2's hygroscopic-vs-thermal strain equivalence statement reproduces verbatim | §2.1.2 | 1 (constraint 4), 5 (strain equivalence), 6 (humidity row) |
| [Lam2008] | Lam, K.W., Uddin, M.A., Chan, H.P., "Reliability of adhesive bonded optical fiber array for photonic packaging," *J. Optoelectron. Adv. Mater.* 10(10), 2539–2546 (2008) | joam.inoe.ro (JOAM 10(10):2539); CityU HK Scholars record | [abstract] | ✅ Identity, author group, venue and pagination confirmed 2026-08-24 (**the packet attributed this paper to "J. Tian et al." — wrong author group**). Qualitative conclusion (CTE mismatch + bonded-surface contamination as the two critical degradation causes; plasma cleaning improves adhesion) is abstract-level. ⚠ The packet's *test conditions* for this paper (GR-1221 thermal shock; "HAST 121 °C/100 % RH/2 atm, 8 h") could **not** be verified — the publisher PDF is password-protected | 2026-08-26 — identity, author group, venue and pagination re-confirmed through two independent channels (CityUHK Scholars and the journal's own site), separately from the 2026-08-24 pass; no DOI exists for this journal/volume | Abstract | 2.2 (adhesion row), 6 (adhesive-process row), 7a |
| [Uddin2006] | Uddin, M.A., Chan, H.P., Tsun, T.O., Chan, Y.C., "Uneven Curing Induced Interfacial Delamination of UV Adhesive-Bonded Fiber Array in V-Groove for Photonic Packaging," *J. Lightwave Technology* 24(3), 1342 (2006) | DOI 10.1109/JLT.2005.863329; IEEE Xplore doc. 1605336; opg.optica.org/jlt/abstract.cfm?uri=JLT-24-3-1342 | [abstract] | ✅ Identity, venue and the mechanism (index-contrast-driven uneven UV cure → interfacial delamination; index matching to the cladding minimizes it) confirmed 2026-08-24 at abstract level | 2026-08-26 — **upgraded**: DOI 10.1109/JLT.2005.863329 resolved via Crossref (matching the DOI the sibling profile `adhesives_polymer_reliability.md` had already resolved for the same paper — the two ledgers now agree), four-author identity re-confirmed | Abstract | 2.2 (cure/index row), 6 (adhesive-process row) |
| [Ptasinski2014] | Ptasinski, J., Khoo, I.-C., Fainman, Y., "Passive Temperature Stabilization of Silicon Photonic Devices Using Liquid Crystals," *Materials* 7(3), 2229–2241 (2014) | DOI 10.3390/ma7032229 | [abstract] | ✅ Identity, authors, venue and pagination confirmed via Crossref 2026-08-24. The packet cited this URL for "negative-TOC passive stabilization" without naming the material system — it is a **liquid-crystal** cladding study | 2026-08-26 — identity, authors, venue and pagination re-resolved via Crossref; no erratum/retraction | Article metadata | 5 (athermalization row) |
| [Komma2012] | Komma, J., Schwarz, C., Hofmann, G., Heinert, D., Nawrodt, R., "Thermo-optic coefficient of silicon at 1550 nm and cryogenic temperatures," *Applied Physics Letters* 101(4), 041905 (2012) | DOI 10.1063/1.4738989 | [abstract] | `~` Identity/authors/venue confirmed via Crossref; the quoted room-temperature value ($1.8\times10^{-4}\ \mathrm{K^{-1}}$ at 300 K, 1550 nm, FP-etalon interferometry) is corroborated by secondary summaries of this paper but was not read in the full text | 2026-08-26 (identity only) — authors/venue re-resolved via Crossref, no erratum/retraction; the quoted room-temperature value was **not** re-read in situ, so the `~` status stands | Abstract / room-temperature value | 1 (constraint 7), 2.1, 3, 5 (bulk TOC), 6 (bulk-vs-device row) |
| [Weituschat2020] | Weituschat, L.M., Dickmann, W., Guimbao, J., Ramos, D., Kroker, S., Postigo, P.A., "Photonic and Thermal Modelling of Microrings in Silicon, Diamond and GaN for Temperature Sensing," *Nanomaterials* 10(5), 934 (2020) | DOI 10.3390/nano10050934 | [abstract] | ⚠ Identity/authors/venue confirmed via Crossref, but the ≈68.2 pm/K figure was taken from a secondary summary of the paper's text, not read in situ. Treat as order-of-magnitude for a Si microring near 1550 nm until re-read | 2026-08-26 (identity only) — authors/venue re-resolved via Crossref, but the ≈68.2 pm/K figure was **again** not read in situ and still comes from a secondary summary; treat as order-of-magnitude. `review-when:` the article text becomes readable | Reported Si microring temperature sensitivity | 2.1 (spectral row), 5 (resonance drift) |
| [GR-468] | Telcordia GR-468-CORE, *Generic Reliability Assurance Requirements for Optoelectronic Devices Used in Telecommunications Equipment*, Issue 2 (Sept 2004) | Telcordia GR-468-CORE | [secondary] | ✅ Title, scope and Issue 2 date confirmed 2026-08-24 via Telcordia/distributor listings; the standard document itself was not read | 2026-08-26 — title, scope and the Issue 2 (2004) date re-confirmed; multiple independent listings agree **no Issue 3 exists**, so the 2004 issue remains current despite its age. `review-when:` GR-468-CORE Issue 3 is published, **or** JEDEC's JC-14.3 Silicon Photonics Qualification and Reliability standard (currently in draft) is published — either would change what this row means | Scope statement | 1 (constraint 6), 2.3, 5 (ΔIL), 6 (Telcordia rows), 7a |
| [GR-1221] | Telcordia GR-1221-CORE, *Generic Reliability Assurance Requirements for Passive Optical Components*, Issue 2 (Jan 1999) / Issue 3 | Telcordia GR-1221-CORE | [secondary] | Split status: **✅** title and scope ("passive optical components") confirmed 2026-08-24 via Telcordia/distributor listings — **corrects the packet's "fiber/cable components" scope claim**. **`~`** for the ±0.5 dB IL / ±0.2 dB PDL pass criteria: these are the widely-cited figures, not read from the standard document. Single verification history — the thresholds were first resolved in `v_groove_fabrication.md` §7b's 2026-08-24 pass and are **carried over here, not independently re-verified**; this profile is now their home (see Cross-Domain Links), so a future re-verification updates this row and the sibling pointers, not two parallel records | 2026-08-26 (scope + issue currency only) — **Issue 3 is current, not Issue 2**: two independent catalogue listings agree. Its exact issue *date* could not be pinned — two search summaries gave conflicting dates and both were rejected rather than picked. `review-when:` the GR-1221-CORE Issue 3 document, or a reliable description of it, becomes readable — then pin the date and re-check the threshold figures against that issue | Scope statement; commonly-cited threshold figures | 1 (constraint 6), 2.3, 5 (ΔIL, ΔPDL), 6 (GR-1221 scope row) |
| [JESD22-A101] | JEDEC JESD22-A101, *Steady-State Temperature Humidity Bias Life Test* | JESD22-A101 | [secondary] | ✅ Designation-to-test mapping confirmed 2026-08-24 (85 °C/85 % RH with bias) | ⚠ **not independently confirmed since authoring** — the 85 °C/85 % RH-with-bias mapping was re-confirmed 2026-08-26, but the **issue letter is still unpinned** and the pin attempt failed (jedec.org and every reseller mirror returned HTTP 403). `review-when:` an unblocked path to jedec.org or an authoritative catalogue becomes available | Standard title | 2.3, 4 (Eyring), 5 (THB) |
| [JESD22-A102] | JEDEC JESD22-A102, *Accelerated Moisture Resistance — Unbiased Autoclave* | JESD22-A102 | [secondary] | ✅ Designation-to-test mapping confirmed 2026-08-24 | ⚠ **not independently confirmed since authoring** — mapping re-confirmed 2026-08-26; **issue letter unpinned**, pin attempt blocked (403). A third-party listing suggests a later revision exists; that is circumstantial and is deliberately not written into this row | Standard title | 2.3, 5 (PCT), 6 (PCT-vs-HAST row) |
| [JESD22-A103] | JEDEC JESD22-A103, *High Temperature Storage Life* | JESD22-A103 (jedec.org 22a103D.pdf) | [secondary] | ✅ Confirmed 2026-08-24: A103 is the unpowered high-temperature storage method (150 °C/1000 h typical) | ⚠ **not independently confirmed since authoring** — re-confirmed 2026-08-26 that A103 is the *unpowered* high-temperature storage method (150 °C/1000 h typical), matching [Bender2024] Table 3 exactly; **issue letter unpinned**, pin attempt blocked (403) | Standard title/purpose | 2.3, 5 (HTS), 6 (designation row) |
| [JESD22-A104] | JEDEC JESD22-A104, *Temperature Cycling* | JESD22-A104 | [secondary] | ✅ Designation-to-test mapping confirmed 2026-08-24 | ⚠ **not independently confirmed since authoring** — mapping re-confirmed 2026-08-26 and matches [Bender2024] Table 3 exactly (−65→150 °C, 1000 cycles as one qualification example); **issue letter unpinned**, pin attempt blocked (403) | Standard title | 2.3, 5 (TC) |
| [JESD22-A106] | JEDEC JESD22-A106, *Thermal Shock* | JESD22-A106 (jedec.org 22a106b.pdf) | [secondary] | ✅ Designation-to-test mapping confirmed 2026-08-24 | 2026-08-26 (scope/mapping) — matches [Bender2024] Table 3 exactly (−55→125 °C, 1000 cycles). JEDEC's own currently-indexed page for this standard is titled at **revision B**; that page title was read, the document itself was not fetched, so the pin is indicative rather than primary | Standard title | 2.3, 5 (TS) |
| [JESD22-A108] | JEDEC JESD22-A108, *Temperature, Bias, and Operating Life* | JESD22-A108 (jedec.org 22A108D.pdf) | [secondary] | ✅ Confirmed 2026-08-24: A108 is the biased/operating-life (HTOL) method — **not** high-temperature storage | ⚠ **not independently confirmed since authoring** — re-confirmed 2026-08-26 that A108 is the biased/operating-life (HTOL) method and **not** a storage test, which is exactly what the Node 6 pitfall turns on; **issue letter unpinned**, pin attempt blocked (403) | Standard title/purpose | 2.3, 6 (designation row) |
| [JESD22-A110] | JEDEC JESD22-A110, *Highly-Accelerated Temperature and Humidity Stress Test (HAST)* | JESD22-A110 — ⚠ **issue letter still unpinned** (a filename `JESD22A110B.pdf` was seen, which is a filename, not a confirmed designation) | [partial] — **upgraded from [secondary] 2026-08-26**: an OCR excerpt of the standard's own body text (§3.0–§7.0) was supplied by the user and read directly. It is partial and lossy — the cover page, the full lettered-condition table, and the revision line are **not** in it | ✅ Conditions now read **from the document itself**, not from secondary description: §3.1 gives 130 ± 2 °C dry bulb / 85 ± 5 % RH / wet bulb 124.7 °C / 33.5 psia / 96 h (the duration tolerance reads as +2/−0 but is OCR-degraded). §3.1 notes 4–5, the §3.2 bias-decision table and the §4.5 readout window were also read and are now cited in Nodes 2/5/6. ⚠ Still **unpinned**: the excerpt carries no revision letter, so which issue these conditions belong to remains unknown — and the standard's own §7 requires a *condition letter* to be specified, while only one condition row survived the OCR. `review-when:` a cover page, revision line, or an unblocked jedec.org path becomes available | 2026-08-26 — conditions verified against the primary document (user-supplied OCR excerpt); **issue letter not verified** | §3.1 table + notes 4–5; §3.2 bias guidelines; §4.5 readout window | 2.3, 5 (HAST), 6 (PCT-vs-HAST row) |
| [JESD22-A118] | JEDEC JESD22-A118, *Accelerated Moisture Resistance — Unbiased HAST* | JESD22-A118 | [secondary] | ✅ Confirmed 2026-08-24 (110–130 °C/85 % RH/~2 atm, no bias) | ⚠ **not independently confirmed since authoring** — re-confirmed 2026-08-26 (110–130 °C/85 % RH/~2 atm, no bias), with the mechanistic reason recovered: bias is deliberately omitted so bias-independent mechanisms remain observable; **issue letter unpinned**, pin attempt blocked (403) | Standard title/conditions | 2.3 |
| [JESD22-B104] | JEDEC JESD22-B104, *Mechanical Shock* (superseded by JESD22-B110A for device and subassembly) | JESD22-B104C | [secondary] | ✅ Designation confirmed 2026-08-24, including the supersession note | 2026-08-26 — designation and supersession re-confirmed via JEDEC's own hosted page titles plus independent resellers. **New finding:** the superseding JESD22-B110 has itself been revised, so the chain now reads B104C → B110(A) — that second hop's exact current letter needs the same primary access this pass could not get. `review-when:` jedec.org becomes fetchable | Standard title | 2.3 |
| [JESD22-B103] | JEDEC **JESD22-B103B.01**, *Vibration, Variable Frequency* | JESD22-B103B.01 (issue pinned 2026-08-26) | [secondary] | ⚠ Designation-to-test mapping **not** independently confirmed in this pass (the search return was self-contradictory). Verify before citing the number in a deliverable | 2026-08-26 — **⚠ → ✅**: JEDEC's own hosted document page is titled "JESD22-B103B.01 — VIBRATION, VARIABLE FREQUENCY", corroborated by three independent resellers. This is the one standard row in this ledger whose issue **is** pinned | Standard title | 2.3 |
| [IEC60068] | IEC 60068 series, *Environmental testing* | IEC 60068 | [secondary] | `~` Series scope known at catalogue level; no specific part verified in this pass | 2026-08-26 (scope only) — series structure re-confirmed (‑1 general/guidance, ‑2 tests, ‑3 supporting documentation; environmental testing generally, not restricted to electrotechnical products). No part or edition is pinned, and none is cited for a numeric claim | Series scope | 2.3 |
| [IEC61300] | IEC 61300 series, *Fibre optic interconnecting devices and passive components — Basic test and measurement procedures* | IEC 61300 (‑1 current edition: **Ed. 5.1:2024**, pinned 2026-08-26) | [secondary] | `~` Series scope known at catalogue level; no specific part verified in this pass | 2026-08-26 (scope + current edition) — **new finding:** IEC 61300-1 **Ed. 5.1 (2024)** is current, superseding Ed. 5.0 (2022), which superseded the 4th edition (2016). This row previously pinned no edition at all. `review-when:` IEC issues a further amendment or edition | Series scope | 2.3 |
| [MIL-STD-883] | MIL-STD-883, *Test Method Standard: Microcircuits* | MIL-STD-883 | [secondary] | `~` Scope known at catalogue level; no specific method verified in this pass | ⚠ **not re-verified since authoring** — deliberately not attempted in the 2026-08-26 pass (lowest priority under that pass's budget; no numeric claim in this profile depends on this row). `review-when:` a Node 1–6 claim starts depending on a specific MIL-STD-883 method | Standard scope | 2.3 |

### Provenance & correction log (source packet → this profile, 2026-08-24)

The packet ("方向 2", a Perplexity research session output) carried opaque footnote indices with
URLs. Each load-bearing footnote was re-resolved to a primary record. Findings:

| Packet claim | Status | Correction |
|---|---|---|
| "D. Chen et al., *Advanced Photonics Nexus* (2026)" | ❌ wrong first author | The CPO thermal-management review is Yang, Z., He, G., Li, Y., Sun, Y., Luo, W., Zhang, W. → [Yang2026] |
| "J. Tian et al., Reliability of adhesive bonded optical fiber array…" | ❌ wrong author group | That paper is Lam, Uddin & Chan (CityU HK) → [Lam2008]. The surname "Tian" belongs to a *different* packet source, the polymer-delamination review → [Tian2024] |
| "E. Bender et al., Modern Trends in Microelectronics Packaging Reliability: **A Review**" | ❌ wrong title | Actual title: "Modern Trends in Microelectronics Packaging Reliability **Testing**" → [Bender2024] |
| "P. M. et al., Photonic Packaging…" | ❌ unusable author field | Carroll, L., et al. (2016) → [Carroll2016] |
| "JEDEC JESD22-A108 = 高溫儲存壽命 (high-temperature storage)" | ❌ wrong designation | A103 is High Temperature Storage Life; A108 is Temperature, Bias, and Operating Life. Kept as a Node 6 pitfall |
| "Telcordia GR-1221-CORE = 光纖／光纜元件通用可靠度保證要求" | ❌ wrong scope | GR-1221-CORE covers **passive optical components**. Kept as a Node 6 pitfall |
| "HAST 121 °C / 100 % RH / 2 atm, 8 h" (attributed to the fiber-array paper) | ⚠ unverified + terminology conflict | Those are autoclave/PCT conditions, not JESD22-A110 HAST conditions. The paper's actual conditions could not be checked (password-protected publisher PDF). Kept only as a Node 6 pitfall about the naming, never as a cited condition |
| "Switch die 功耗遠高於 CPO module 內的光子元件" (attributed to the CPO review) | ⚠ unverified | Not stated in anything read for [Tan2023]. The verified, citable form of the claim is [Yang2026]'s abstract: ASIC extreme power density + photonic temperature sensitivity ⇒ thermal management is a critical bottleneck. The quantitative ratio was dropped |
| Footnote list items [^10]–[^46] (hidden span in the packet) | not imported | These were never cited inline in the packet body. One of them — the UV-cured V-groove fiber delamination work — was independently located, verified and imported as [Uddin2006]; the rest were left out rather than imported unverified |

---

## Cross-Domain Links

### Closest Related Domain Profiles

| Profile name | Overlap dimensions | Typical use split |
|------|------|-------|
| `fiber_chip_passive_alignment.md` (Fiber-to-Chip Passive Alignment & Attachment) | first principles (CTE-mismatch thermo-mechanics, cure shrinkage), quality metrics (ΔIL, worst-channel IL), measurement tools (qualification chambers) | Use **that** profile for *where the core lands and why it moves* — datum chain, error budget, adhesive/cure process, single-interface drift. Use **this** profile for *the whole package under stress* — test-matrix design, acceleration models, standards selection, mechanism attribution, thermal architecture. That profile explicitly hands off to this one at the worst-channel and cost-per-channel metrics |
| `v_groove_fabrication.md` (V-Groove Fabrication) | application targets (fiber array), materials/interfaces (Si–adhesive–fiber) | Use **that** profile for *how the groove is cut*. Use **this** profile when the question is whether the groove-based attach *survives* TC/THB/HAST and what the failure mechanism is |
| `adiabatic_taper_ssc.md` (Adiabatic Taper & SSC) | quality metrics (coupling loss, alignment tolerance), application targets (edge coupling, packaging cost) | Use **that** profile for *mode expansion and time-zero coupling*. Use **this** profile for end-of-life coupling: a larger MFD relaxes the *thermally induced* misalignment sensitivity too, which is a reliability argument that profile does not make |
| `silicon_photonics_device_physics.md` (Silicon Photonics Device Physics) | measurement tools (L–I–V, I–V, dark current, ER/$V_\pi$, BER), first principles (carrier–photon–thermal coupling), application targets (CPO link budget) | Use **that** profile for *why a device behaves or degrades at the physics level* — laser threshold and gain, plasma dispersion, Ge dark-current mechanisms, link-budget accounting. Use **this** profile for *what the package does to it and what the evidence must look like* — the thermal/mechanical/moisture stress that drives the drift, the acceleration model, the qualification claim. A laser wavelength drift is that profile's physics and this profile's failure mode; both should be loaded when a question spans them |
| `gan_power_device.md` (Vertical GaN Power Devices) | first principles ($T_j$, $R_\theta$, thermal path), measurement tools (HTOL, thermal characterization) | Both care about junction temperature and thermal resistance. Use **that** profile when the observable is electrical device behaviour (dynamic $R_{ON}$, breakdown); use **this** one when $T_j$ matters because it moves a *wavelength*, a coupling position, or an interface stress |
| `adhesives_polymer_reliability.md` (Adhesives & Polymer Reliability) | first principles (hygrothermal/CTE-mismatch mechanics), measurement tools (HAST/PCT/thermal-shock chambers), quality metrics (ΔIL as an adhesive-fatigue sensor) | Use **that** profile for what the adhesive material *is* and why it degrades — degree of cure, Tg, moisture diffusion model, cohesive/interfacial failure mode. Use **this** profile for whether a stress condition and acceleration model actually match the adhesive's confirmed failure mechanism before an AF/lifetime number is reported |

### Boundary & ownership notes

- **Agreed split with `fiber_chip_passive_alignment.md` (settled 2026-08-24).** That profile's author
  raised the overlap (its Node 2 qualification-stress block, its Node 5 post-stress IL drift, and its
  Node 4 "IL step vs. monotonic ramp" rule) and proposed a split; it is accepted here as written,
  and both files now state it identically. **Route by observable + scope**: "how much did this
  coupling degrade, and why did the fiber move?" → that profile (one fiber–chip interface, the
  alignment/attach chain, per-channel and worst-channel array statistics). "What stress matrix
  qualifies this module, and what acceleration factor applies?" → this profile (module-level
  qualification planning, Arrhenius/Coffin–Manson/Peck/Weibull, failure-mechanism attribution across
  the whole package, thermal architecture). Neither profile absorbs the other's rows: the shared
  concepts appear in both only as a pointer, never as a second copy of a number.
- **Telcordia GR-1221 pass criteria (±0.5 dB IL, ±0.2 dB PDL) are homed here** as of 2026-08-24 —
  they are acceptance criteria, which is this profile's subject. Their single verification history
  originates in `v_groove_fabrication.md`'s 2026-08-24 citation pass and is recorded in this
  profile's §7b `[GR-1221]` row; `v_groove_fabrication.md` and `fiber_chip_passive_alignment.md` now
  point here for the criterion instead of carrying their own copies.
- The photonics-interface family now partitions one physical assembly into **cutting**
  (`v_groove_fabrication`) / **mode-matching** (`adiabatic_taper_ssc`) / **placing-and-holding**
  (`fiber_chip_passive_alignment`) / **surviving-and-proving** (this profile). When a question spans
  two of them, load both and say explicitly which one owns the governing constraint.
- Cross-profile numbers are referenced, not copied: MFD and 1-dB tolerance figures live in
  `adiabatic_taper_ssc.md`; the alignment error budget and fiber-geometry specs live in
  `fiber_chip_passive_alignment.md`; groove geometry lives in `v_groove_fabrication.md`. Re-quoting
  them here would create a second, un-versioned copy of a number whose verification status is
  recorded elsewhere.
- This profile deliberately holds **no** adhesive-material selection table. Material-level polymer
  questions (degree of cure, Tg selection, moisture-uptake modelling, adhesion/fracture chemistry)
  are now the registered home of `adhesives_polymer_reliability.md` (added 2026-08-25 as the
  cluster's fifth member); this profile only owns how such a material is *stressed and judged* at
  the module level.

---

## Cross-Domain Conflict Notes

| Issue / constraint | Other profile(s) involved | Potential conflict | AI confirmation question |
|------|------|-------|-------|
| Time-zero loss vs. end-of-life loss | `fiber_chip_passive_alignment.md`, `adiabatic_taper_ssc.md` | Those profiles optimize initial coupling loss and placement accuracy; this profile's acceptance criterion is loss *after* the full stress sequence. An adhesive or geometry that wins at t = 0 can lose after TC/THB | "Is the acceptance criterion initial IL or post-qualification IL? The adhesive, geometry and cure choices can invert between the two" |
| MFD enlargement: tolerance vs. density vs. thermal drift | `adiabatic_taper_ssc.md` | Enlarging the mode relaxes both placement *and* thermally induced misalignment sensitivity, but costs channel density — which is precisely CPO's scaling axis | "Are you optimizing a single low-loss channel, an array's density, or the array's drift under thermal cycling? Those three point in different directions and only one can be the primary" |
| Destructive-analysis ordering | `v_groove_fabrication.md`, `fiber_chip_passive_alignment.md` | Groove cross-sectioning and pull testing destroy exactly the samples whose post-stress optical drift this profile needs | "Do you need this unit after the destructive step? If post-stress optical data matter, allocate sacrificial units per readout point and put non-destructive metrology (optical → C-SAM → X-ray) first" |
| Which discipline owns "alignment stability" | `fiber_chip_passive_alignment.md` | Both profiles can claim a fiber-drift problem: as an assembly-process defect (cure, datum) or as a reliability failure mechanism (creep, CTE fatigue, moisture). Different fixes follow | "Did the offset appear at assembly/cure, or did it develop during stress? If there is no pre-stress baseline for this unit, the first task is establishing one, not choosing a fix" |
| Device degradation vs. package-induced drift | `silicon_photonics_device_physics.md` | The same observable (laser power/wavelength drift, PD dark-current rise) has a device-intrinsic explanation there and a package-induced one here; each profile will propose a different fix | "Was the device measured at a controlled, known junction temperature and mount condition? If the thermal boundary condition moved between readings, the drift is a packaging observation, not a device-degradation one" |
| Thermal design owner in a CPO package | `gan_power_device.md` (and any future ASIC/thermal profile) | An electrically optimal thermal design (minimize $T_j$ of the power device) may not be optically optimal (minimize *gradient* and drift at the photonics) | "Is the thermal target a maximum junction temperature, or a maximum gradient/drift at the temperature-sensitive photonic devices? Those two objectives can select different lid/TIM/cold-plate architectures" |
