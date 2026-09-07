---
xi: 1
what: "Silicon Photonics Device Physics (矽光子主動元件物理) — Silicon photonics ACTIVE device physics: integrated light sources, modulators, Ge photodetectors, and the carrier-photon-thermal chain linking device metrics to a link budget"
tags: [srg-domain, 領域框架, base]
aliases: ["silicon photonics", "SiPh", "矽光子", "silicon modulator", "ring modulator", "MZI modulator", "plasma dispersion", "Soref-Bennett", "carrier depletion", "carrier injection", "electro-absorption", "Franz-Keldysh", "QCSE", "V_piL", "extinction ratio", "Ge photodetector", "Ge-on-Si", "germanium photodiode", "avalanche photodiode", "APD", "responsivity", "dark current", "heterogeneous laser", "III-V on Si", "hybrid laser", "quantum dot laser", "threshold current", "slope efficiency", "RIN", "linewidth", "link budget", "CPO", "co-packaged optics"]
date: 2026-08-26
status: live
profile_type: base
parent: "-"
---
# Domain Profile: Silicon Photonics Device Physics (矽光子主動元件物理)

> Scope of applicability: Active devices on silicon photonic platforms — integrated light sources (heterogeneous/hybrid III–V, quantum dot, Raman, Ge/GeSn), optical modulators (Si free-carrier, EA, Pockels-material), and photodetectors (Ge-on-Si PIN and APD) — plus the carrier–photon–thermal physics that links their device-level metrics to a system-level optical link budget.
> Scientific nature: Semiconductor band structure and radiative/non-radiative recombination, free-carrier plasma dispersion, electro-absorption, laser gain and threshold physics, carrier transport and collection under bias.
> Engineering nature: Heterogeneous material integration (Ge, III–V, EO materials on Si), electro-optic and opto-electronic device design, thermal and reliability co-design in co-packaged optics (CPO), link-budget and BER accounting.
>
> Profile metadata:
> - Profile ID: SIPH-ACTIVE-001
> - Profile version: v1.0 (first intake; citation-resolution pass completed at authoring time)
> - Last updated: 2026-08-26 (§3.7 currency pass: 16/16 identities re-resolved with zero mismatches, but two claim-level defects found — Kim2014's result was stated backwards in Node 5, and Liu2005 is a probable citation conflation, flagged not fixed; Soref–Bennett gained its missing version pin)
> - Author(s) / Maintainer(s): Compiled from a user-supplied Perplexity research packet ("方向 3: Silicon Photonics Device Physics"), rewritten to this SKILL's profile format by Claude; every citation re-resolved via `literature-search-extract` (Mode 2, source-provided route) before entering the profile
>
> Primary source types:
> - Textbooks: (not yet incorporated — recommend Coldren, Corzine & Mašanović "Diode Lasers and Photonic Integrated Circuits" for gain/threshold physics, and Chuang "Physics of Photonic Devices" for EA/QCSE derivations)
> - Review articles: [Reed2010], [Michel2010], [Liang2010], [Wang2018], [Shekhar2024], [Zhang2024a]
> - Methods / standards papers: [Soref1987] (plasma-dispersion coefficients), [Liu2005] (tensile-strained Ge band edge)
> - Other: Device-level experimental reports [Kim2014], [Liu2025], [Cao2024], [Koscica2023], [Park2008], [Guo2019]
>
> Notes for AI use:
> - Intended use: Cross-check claims about Si modulator / Ge photodetector / integrated-laser physics and metrics, and route device-level numbers into (or out of) a link-budget argument. Load alongside `adiabatic_taper_ssc.md` whenever the question also touches fiber–chip coupling.
> - Validation status / usage note: The source packet used opaque footnote indices (`[^1]`…`[^13]`) with no bibliography — exactly the citation form `domain-expansion-guide.md` §3.2 prohibits. All 13 were resolved to real works during intake, and **three source-packet errors were corrected in the process** (see Node 7b "Intake corrections"). Numeric claims carry the verification status recorded in Node 7b; a `~` status means the general claim is corroborated but the exact figure was not independently re-derived. This is a first-round profile — do not treat unmarked statements as multi-source consensus.

---

## Citation convention (read before editing Nodes 1–6)

Per `domain-expansion-guide.md` §3.2: every inline citation is a human-resolvable `[Author Year]`
key with a row in Node 7b, and every quantitative claim states its conditions (material system,
measurement method, wavelength/temperature/bias/optical power) in the same breath as the number.
This profile's own intake is the cautionary case: the packet it came from quoted `[^7]` — a
**Nature collection landing page, not a paper** — as the source for three different review
articles. All three are real and are now cited individually; the index that pointed at them was not.

---

## 1. Theoretical Framework Anchoring

### Core first principles

| Scale / problem type | Foundational theory | Core physical quantity |
|---|---|---|
| Whether the host material can emit at all | Semiconductor band theory; direct vs. indirect gap; momentum conservation via phonon assistance | E_g, k-space offset of conduction-band minimum vs. valence-band maximum, radiative recombination rate |
| Index/absorption change under bias in Si | Free-carrier plasma dispersion (Drude-like), Soref–Bennett empirical fit | ΔN, ΔP → Δn, Δα |
| Index change under field in a non-centrosymmetric medium | Second-order nonlinearity χ⁽²⁾ (Pockels), χ⁽³⁾ (Kerr) | Electro-optic coefficient r_ij, applied field E |
| Absorption change under field | Franz–Keldysh effect (bulk), quantum-confined Stark effect (quantum well) | α(V), exciton absorption-peak shift |
| Phase → intensity transduction | MZI two-arm interference; ring round-trip resonance | Δφ = (2π/λ)·Δn_eff·L; m·λ_res = n_eff·L_ring |
| Photon → carrier conversion | Interband absorption + drift/diffusion collection in a depleted region | α_eff; η_abs = 1 − e^(−α_eff·L); R = η_ext·qλ/(hc) |
| Carrier → photon conversion with net gain | Round-trip gain-equals-loss threshold condition | Γ·g(N_th) = α_i + α_m; I_th, η_d, differential gain |
| Device → system | Optical link power budget | P_Rx = P_laser − ΣL_i; requirement P_Rx ≥ P_sens + M_margin |

### Inviolable physical constraints (the AI should warn the user here)

1. **Silicon has no usable native telecom gain.** Si is an indirect-gap semiconductor: electron–hole radiative recombination generally requires phonon assistance to conserve momentum, so bulk Si cannot serve as a practical telecom laser gain medium the way InP-based compounds do [Liang2010][Wang2018]. Any claim of a "silicon laser" must name the actual gain mechanism — bonded/grown III–V, quantum dot, Raman nonlinearity, Ge/GeSn band engineering, or rare-earth doping. Without a named mechanism, the label is not describing the device.
2. **Si has no usable native Pockels effect.** Crystalline Si is centrosymmetric, so χ⁽²⁾ vanishes in the bulk dipole approximation. A "linear EO" or "Pockels" silicon modulator implies a heterogeneous EO material (thin-film LiNbO₃, BaTiO₃, EO polymer) or deliberate strain-induced symmetry breaking [Zhang2024a]. Free-carrier plasma dispersion is **not** an electro-optic effect and must not be described as one (see `silicon_photonics_device_physics/terminology.md`).
3. **Δn and Δα are not independently purchasable in Si free-carrier modulation.** The Soref–Bennett relations couple them: any carrier change that buys phase shift also buys free-carrier absorption [Soref1987][Reed2010]. A reported V_πL improvement without the accompanying insertion loss (and, for injection devices, the resulting power/heat) is an incomplete result, not a better device.
4. **A ring resonator's operating point is a moving target.** λ_res is set by n_eff, and n_eff is temperature-dependent through silicon's strong thermo-optic coefficient. Any ring ER / IL / energy-per-bit figure quoted without stating the detuning, the temperature, and whether tuning power is included is unusable for comparison [Shekhar2024][Margalit2021]. For the full thermal-control physics — passive athermalization, heater/feedback architectures, and WDM ring-to-ring crosstalk — see `silicon_photonics_device_physics/ring_resonator_thermal_control.md`.
5. **Ge's direct gap sits essentially at the C-band edge.** Unstrained Ge has a direct gap of ≈0.80 eV at 300 K — almost exactly the 1550 nm photon energy (hc/λ = 0.800 eV) — so responsivity rolls off through C-band into L-band. Reported extended cutoffs come from deliberate tensile strain: 0.20% strain lowers the direct gap from 0.80 to ≈0.77 eV, and ≈0.25% pushes the direct band edge from 1550 to ≈1623 nm [Liu2005]. ⚠ The 0.20 %/0.77 eV half of this may belong to a **second, uncited** 2005 Liu et al. paper (*Appl. Phys. Lett.* 87(10), 103501, DOI 10.1063/1.2037200) rather than the cited one (87(1), 011110) — unresolved as of 2026-08-26, both paywalled; see the Node 7b row before quoting either figure. A responsivity measured "at 1550 nm" cannot be extrapolated to L-band without knowing the strain state.
6. **Responsivity has a hard physical ceiling without internal gain.** R ≤ qλ/(hc), i.e. ≈1.25 A/W at 1550 nm and ≈1.06 A/W at 1310 nm, at unity external quantum efficiency. A reported R above that ceiling implies avalanche/internal gain, an optical-power calibration error, or a responsivity defined against coupled rather than incident power — confirm which before using the number.
7. **Laser threshold and slope efficiency are junction-temperature quantities.** I_th(T) and η_d degrade with T_j, not with the package label temperature. Quoting laser performance against ambient without a thermal-resistance path is not a device claim [Koscica2023].
8. **Dark current is a noise term, not only a DC power term.** It enters receiver shot noise as ⟨i²_shot⟩ = 2q·I_dark·B, so it degrades sensitivity independently of its (usually negligible) power draw [Michel2010].

> **Decision point (mandatory Tier 0 confirmation)**: when the user describes an active-device
> problem ("我的調變器…", "PD 的頻寬…", "雷射整合…"), the AI must confirm:
> "Is your goal (A) explaining or correcting the underlying device physics (band structure,
> carrier–photon interaction, gain/absorption mechanism), (B) optimizing a device-level metric
> under fabrication and thermal constraints, or (C) closing a system-level link budget / BER
> requirement?"
> The three goals correspond to entirely different analysis paths: (A) needs band-structure and
> rate-equation-level rigor; (B) needs process, RF-parasitic and thermal co-design literature;
> (C) needs link-budget accounting where a single device metric is only one term among many.

---

## 2. Measurement Tool Inventory

### Electro-optic / modulator characterization

| Measurement target | Tool | Output information | Applicable conditions | Common misuse | Device class | Source [Key] |
|---|---|---|---|---|---|---|
| Phase-shifter efficiency | DC bias sweep on an MZI + optical power meter; fit transfer curve | V_π, V_πL (V·cm) | Requires known arm length and a stated bias point (depletion devices are strongly bias-dependent) | Quoting V_πL without the bias point or arm length, making devices non-comparable | Modulator | Reed2010 |
| Insertion loss attributable to modulation | Reference waveguide de-embedding + cut-back | IL (dB) separated from coupler/waveguide loss | Reference structure must share the same couplers and routing | Reporting V_πL as a standalone figure of merit while omitting the FCA-induced IL it bought | Modulator | Soref1987 |
| EO bandwidth | Vector network analyzer, S21 (E/O response), calibrated photoreceiver | f_3dB, RF loss, impedance match | Must state termination, drive swing, and whether the receiver response was de-embedded | Treating a small-signal S21 f_3dB as a guarantee of large-signal PAM4 eye quality | Modulator | Margalit2021 |
| Ring resonance shape and drift | Tunable laser wavelength sweep + temperature-controlled stage | λ_res, Q, ER, FSR, thermal shift dλ/dT | Requires stage temperature logging; high input power perturbs the measurement itself | Sweeping at high optical power and reading the resonance as if it were the low-power linear resonance (thermal bistability, TPA-generated free carriers) | Modulator (ring) | Shekhar2024 |
| Large-signal link quality | BERT + eye/eye-mask analysis, PAM4 TDECQ-style metrics | BER, eye opening, chirp penalty | Needs the actual driver, TIA and DSP in the loop | Inferring BER from small-signal ER alone | Modulator | Margalit2021 |

### Photodetector characterization

| Measurement target | Tool | Output information | Applicable conditions | Common misuse | Device class | Source [Key] |
|---|---|---|---|---|---|---|
| Responsivity | Calibrated tunable source + reference power meter + source-measure unit | R (A/W) vs. λ and bias | Must state whether power is *incident on fiber*, *coupled into waveguide*, or *incident on the Ge* | Reporting waveguide-referred R against fiber-launched power (or vice versa), inflating or deflating R by the whole coupling loss | Photodetector | Liu2025 |
| Dark current | SMU I–V in the dark, temperature-controlled | I_dark vs. reverse bias and T | Bias and temperature must both be stated; I_dark is strongly T-activated | Comparing I_dark values taken at different reverse biases or temperatures | Photodetector | Liu2025 |
| Opto-electrical bandwidth | VNA S21 with calibrated optical modulation, or impulse response | f_3dB, transit- vs. RC-limited regime | Bandwidth is optical-power-dependent; must state the input power | Quoting a low-power f_3dB for a link that operates at high received power (space-charge screening reduces it) | Photodetector | Cao2024 |
| Saturation / high-power behavior | Power-swept responsivity and bandwidth at fixed bias | 1-dB compression power, R at high P_in | Requires a source able to reach the intended operating power | Extrapolating small-signal responsivity into the saturated regime | Photodetector | Cao2024 |
| Avalanche gain and noise | Bias sweep to near breakdown + noise spectral density | M(V), excess noise factor F(M), gain–bandwidth product | Needs breakdown-safe compliance and temperature control (V_br is T-dependent) | Reporting M without F(M), so the sensitivity gain looks free | Photodetector (APD) | Michel2010 |

### Light-source characterization

| Measurement target | Tool | Output information | Applicable conditions | Common misuse | Device class | Source [Key] |
|---|---|---|---|---|---|---|
| Threshold and efficiency | LIV measurement on a temperature-controlled stage | I_th, slope efficiency, η_d, roll-over point | Stage temperature ≠ junction temperature; state the thermal path | Quoting I_th without the stage temperature or duty cycle (CW vs. pulsed) | Laser | Koscica2023 |
| Temperature sensitivity | LIV over a temperature series, exponential fit | Characteristic temperature T₀ (written T₀* in this profile, see terminology note), max lasing temperature | The fitted T₀ is only valid over the fitted range | Quoting a single T₀ as if it were temperature-independent | Laser | Koscica2023 |
| Spectral quality | OSA (coarse), delayed self-heterodyne or heterodyne beat (linewidth) | Peak λ, SMSR, linewidth | OSA resolution bandwidth is far too coarse for linewidth — needs a heterodyne method | Reading "linewidth" off an OSA trace | Laser | Liang2010 |
| Intensity noise | RIN measurement: photodetector + ESA, with shot-noise and thermal-noise calibration | RIN (dB/Hz) vs. frequency and bias | Requires explicit noise-floor subtraction and stated bias | Reporting RIN without the noise floor, or without back-reflection isolation | Laser | Zhang2024b |
| Sensitivity to back-reflection | Variable optical isolator/reflector setup, monitor linewidth/RIN/mode stability | Feedback tolerance | Must state reflection level (dB) and phase condition | Characterizing a laser only under ideal isolation, then deploying it behind a real fiber interface | Laser | Zhang2024b |

### Material and heterogeneous-integration characterization

| Measurement target | Tool | Output information | Applicable conditions | Common misuse | Device class | Source [Key] |
|---|---|---|---|---|---|---|
| Threading dislocation density in III–V or Ge on Si | Cross-sectional TEM (destructive), etch-pit density, XRD rocking curve | TDD (cm⁻²), strain, layer quality | TEM samples a very small volume; EPD needs a calibrated etch | Reporting a TEM-derived TDD as a wafer-level figure | Laser / Photodetector | Guo2019 |
| Bond-interface integrity (III–V/Si) | Acoustic microscopy, cross-sectional SEM/TEM, IR transmission | Void fraction, bonded-area uniformity | Destructive methods end the sample's life — sequence them last | Treating a laser yield problem as purely epitaxial when the bond interface was never imaged | Laser | Park2008 |
| Ge epitaxial strain state | XRD reciprocal-space mapping, Raman shift | Tensile strain (%), relaxation degree | Raman peak shift also responds to temperature and doping | Quoting a Ge absorption cutoff without the measured strain state | Photodetector | Liu2005 |

---

## 3. Standard Modeling Toolchain

```
Band structure of the active material (k·p, tight-binding, DFT for new alloys e.g. GeSn)
→ Output: E_g and its direct/indirect ordering, effective masses, gain vs. carrier density g(N),
           absorption spectrum α(λ), electro-absorption response α(V)
    ↓
Material-response models (Soref–Bennett plasma dispersion; Franz–Keldysh / QCSE; Pockels r_ij)
→ Input: carrier concentrations ΔN, ΔP or applied field E
→ Output: Δn(λ), Δα(λ) — the complex index perturbation the optical solver consumes
    ↓
Carrier transport / device electrostatics (TCAD drift-diffusion: junction profile, depletion
width, MOS accumulation layer, transit time, dark-current generation paths)
→ Input: doping profile, bias, geometry, trap/defect models
→ Output: ΔN(x,y,V), depletion boundary, C(V), transit time, I_dark(V,T)
    ↓
Optical mode / circuit solvers (FEM, FDTD, EME for the cross-section; MZI/ring transfer-matrix
or coupled-mode circuit models for the device)
→ Input: perturbed complex index distribution
→ Output: Δn_eff, modal loss, V_πL, ring λ_res / Q / ER, η_abs along the absorber
    ↓
RF/electrical co-simulation (transmission-line and parasitic extraction, driver/TIA co-design)
→ Output: f_3dB decomposition (transit vs. RC), impedance match, energy per bit
    ↓
Thermal model (ASIC hotspot map → PIC temperature field → local Δn_eff, T_j at the laser)
→ Output: resonance drift, tuning power, I_th(T_j), aging acceleration
    ↓
Link-level budget and BER model
→ Output: P_Rx margin, sensitivity requirement, tolerance to drift and aging
```

Handoff caution: the thermal stage is not an optional afterthought in this domain — it feeds
back into both the optical solver (via Δn_eff) and the laser model (via T_j). A toolchain that
runs optics and electronics but stops before the thermal loop will produce device numbers that
are individually correct and jointly unachievable in a CPO package.

---

## 4. Domain-Specific Fitting Methods

| Method | Applicable question | Applicable conditions | Common error | Correct approach | Device class | Source [Key] |
|---|---|---|---|---|---|---|
| Soref–Bennett plasma-dispersion relations | What Δn and Δα follow from a carrier-density change in Si? | Crystalline Si, near 1.55 µm (a separate coefficient set exists for 1.3 µm); ΔN, ΔP in cm⁻³, Δα in cm⁻¹. At 1.55 µm: Δn = −[8.8×10⁻²²·ΔN_e + 8.5×10⁻¹⁸·(ΔN_h)^0.8], Δα = 8.5×10⁻¹⁸·ΔN_e + 6.0×10⁻¹⁸·ΔN_h — these are the **original Soref & Bennett (1987)** coefficients as reproduced in secondary reviews; a later revised/extended fit exists (Nedeljkovic, Soref & Mashanovich, "Free-Carrier Electrorefraction and Electroabsorption Modulation Predictions for Silicon Over the 1–14-μm Infrared Wavelength Range," *IEEE Photon. J.* 3(6), 1171–1180, 2011, DOI 10.1109/JPhot.2011.2171930). **Do not mix coefficient sets** — state which one a model uses | ⚠️ Applying the 1.55 µm coefficient set at 1.31 µm or in the mid-IR; or applying it to SiGe/strained Si as if the coefficients transferred unchanged | Use the coefficient set matching the wavelength; for SiGe or strained material, use a material-specific measurement — strain measurably changes the response (see next row) | Modulator | Soref1987, Reed2010 |
| Strain-corrected plasma dispersion in SiGe | Does compressive strain improve modulation efficiency? | Measured for Si₀.₈₆Ge₀.₁₄ at 85% of theoretical maximum strain (0.48% compressive), 1.55 µm | ⚠️ Quoting "SiGe gives ~1.3× Δn and ~1.7× Δα" as a general SiGe property, with no Ge fraction or strain value | State composition and strain with the enhancement factor; enhancement arises from effective-mass modification and does not extrapolate to arbitrary Ge fraction | Modulator | Kim2014 |
| MZI transfer-curve fit for V_π | How efficient is this phase shifter? | P_out = P_in·cos²(Δφ/2), Δφ = (2π/λ)·Δn_eff·L; needs a stated bias point and known L | ⚠️ Fitting a single-arm-drive curve and reporting it as if push–pull, halving the apparent V_π | State drive configuration (single-arm vs. push–pull), bias point, and λ alongside V_πL | Modulator | Reed2010 |
| Ring resonance (Lorentzian / all-pass transfer) fit | What are Q, ER, and the coupling regime? | Low enough optical power that thermal and free-carrier nonlinearity do not distort the lineshape | ⚠️ Fitting a thermally-broadened or bistable (triangular, hysteretic) resonance with a symmetric Lorentzian and reporting the resulting Q | Sweep at reduced power, or sweep in both directions to detect hysteresis, before extracting Q; report the sweep power | Modulator (ring) | Shekhar2024 |
| Waveguide-absorber responsivity model | How long must the Ge absorber be? | η_abs = 1 − e^(−α_eff·L); R = η_ext·qλ/(hc); α_eff is the *modal* absorption, not the bulk Ge α | ⚠️ Using bulk Ge α instead of the modal α_eff, over-predicting absorption for a weakly overlapping mode | Extract α_eff from the mode–absorber overlap; validate against a length series of detectors | Photodetector | Michel2010 |
| Transit/RC bandwidth decomposition | Is this detector transit-limited or RC-limited? | 1/f²_3dB ≈ 1/f²_transit + 1/f²_RC; valid for a lumped device below the distributed regime | ⚠️ Concluding "make the absorber shorter" when the device is actually RC-limited (or the reverse) | Separate the terms by measuring bandwidth vs. bias (transit) and vs. load/area (RC) before redesigning | Photodetector | Michel2010 |
| Avalanche gain and excess-noise fit | Does APD gain actually improve sensitivity here? | M = I_multiplied/I_primary; excess noise F(M) and the gain–bandwidth product must be fitted together | ⚠️ Optimizing M alone; beyond an optimum gain, F(M) growth overtakes the signal gain and sensitivity worsens | Fit M, F(M) and gain–bandwidth jointly and report the *optimum* M for the target bit rate, not the maximum M | Photodetector (APD) | Michel2010 |
| LIV threshold extraction | What is I_th and the slope efficiency? | Linear extrapolation of the above-threshold L–I segment back to L = 0; P_out ≈ η_d·(hν/q)·(I − I_th) | ⚠️ Extrapolating through a thermally rolled-over segment, understating η_d and overstating I_th | Fit only the linear region well below roll-over; report stage temperature and CW/pulsed mode | Laser | Koscica2023 |
| Characteristic-temperature (T₀*) fit | How temperature-sensitive is this laser? | I_th(T) = I_th(T₀)·exp[(T − T₀)/T₀*] over the fitted temperature range only | ⚠️ Quoting a T₀* fitted near room temperature as if it held up to the maximum operating temperature — the exponential form typically degrades at high T | State the fitted temperature range with every T₀* value; report the maximum lasing temperature separately | Laser | Koscica2023 |

---

## 5. Domain-Specific Quality Metrics

| Metric | Abbreviation | Physical meaning | Typical value range | Conditions (material/method/wavelength/temp…) | Device class | Source [Key] |
|---|---|---|---|---|---|---|
| Half-wave voltage–length product | V_πL | Voltage × phase-shifter length needed for π phase shift; lower ⇒ higher phase efficiency | No single universal target — depends strongly on mechanism (injection ≪ depletion) and bias point; always compare at a stated bias | Crystalline Si, stated λ (1.31 vs 1.55 µm), stated drive configuration (single-arm vs. push–pull) and bias point; must be reported together with the insertion loss it costs | Modulator | Reed2010, Soref1987 |
| Extinction ratio | ER | 10·log₁₀(P_on/P_off) | Design- and detuning-dependent; for rings, meaningless without the detuning and temperature | Detuning from λ_res, temperature, sweep optical power, and whether thermal tuning power is included | Modulator | Shekhar2024 |
| Plasma-dispersion enhancement from strain | — | Ratio of Δn (and Δα) in strained SiGe to unstrained Si at equal carrier change | ≈1.3× for Δn and ≈1.7× for Δα | Si₀.₈₆Ge₀.₁₄ at 85% of theoretical maximum strain (0.48% compressive), 1.55 µm; deduced from wavelength dependence, with a companion device requiring >2× **lower injection current density for the same 20 dB attenuation** (24 vs 55 mA/mm) than a Si control — i.e. >2× the modulation *efficiency*, not >2× the attenuation at equal current (corrected 2026-08-26 against the paper's full text; the earlier wording inverted the comparison and stated a quantity the source never measured) | Modulator | Kim2014 |
| Responsivity | R | Photocurrent per unit incident optical power (A/W) | 0.87 A/W measured on a Ge-on-Si waveguide PD; physical ceiling ≈1.25 A/W at 1550 nm without internal gain | 1550 nm, −3 V bias, room temperature, Ge-on-Si waveguide photodetector; the same study reports responsivity *declining* at 200 K as the epitaxial-Ge absorption coefficient falls | Photodetector | Liu2025 |
| Responsivity under high optical power | R(P_in) | Responsivity retained in the saturated regime | 0.68 A/W retained at 28 mW input optical power | Lateral Ge/Si waveguide PD with four-channel adiabatic side-coupling into two parallel Ge waveguides (a design intended to suppress the space-charge effect); >40 GHz bandwidth reported for *low* optical power | Photodetector | Cao2024 |
| Dark current | I_dark | Reverse-bias current with no illumination; sets a shot-noise floor ⟨i²⟩ = 2q·I_dark·B | 4.62 nA on the same Ge-on-Si waveguide PD; decreases substantially at 200 K | −3 V bias, room temperature, 1500–1600 nm study range; the low-temperature reduction comes with a responsivity penalty — the two do not improve together | Photodetector | Liu2025 |
| Avalanche gain / excess noise | M, F(M) | Internal current gain from impact ionization, and the noise penalty it carries | No universal target — the useful figure is the *optimum* M for a given bit rate, bounded by gain–bandwidth product | Reverse bias near breakdown, stated temperature (V_br is temperature-dependent); M without F(M) is not a sensitivity claim | Photodetector (APD) | Michel2010 |
| Characteristic temperature | T₀* | Exponential sensitivity of I_th to temperature; higher ⇒ more temperature-tolerant | ≈221 K reported near room temperature, with lasing sustained to 105 °C | III–V quantum-dot laser heterogeneously integrated on **silicon carbide** (chosen for high thermal conductivity) — not a Si-substrate figure; fitted near room temperature | Laser | Koscica2023 |
| Lattice mismatch to Si | — | Relative lattice-constant difference driving threading-dislocation formation in direct growth | InP/Si ≈8%, GaAs/Si ≈4% | Room-temperature lattice constants (a_Si = 5.431 Å, a_GaAs = 5.653 Å, a_InP = 5.869 Å); the consequence is threading dislocations that shorten carrier lifetime, raise non-radiative recombination, raise threshold and degrade reliability | Laser | Guo2019 |
| Link power budget closure | P_Rx, M_margin | P_Rx = P_laser − L_coupling − L_mod − L_waveguide − L_WDM − L_fiber/chip − L_other; requires P_Rx ≥ P_sens + M_margin | Application-specific; margin must cover aging, temperature drift, manufacturing variation, polarization and crosstalk | Every loss term must state whether it is per-facet or total, and at which temperature/wavelength; a device metric enters this budget only through its own term | System | Shekhar2024, Margalit2021 |

---

## 6. Common Assumption Pitfalls

| Pitfall | Trigger condition | How to recognize it | Correct approach | Device class | Source [Key] |
|---|---|---|---|---|---|
| Free-carrier modulation described as an "electro-optic" effect | User writes "silicon EO modulator" or 「矽電光調變器」 for a PN-junction device | The mechanism named is injection/depletion/accumulation, but the label implies χ⁽²⁾/χ⁽³⁾ | Plasma dispersion changes the *complex* index via carrier density; it is neither Pockels nor Kerr. Reserve "EO" for genuine field-induced index change (LiNbO₃, BTO, polymer) | Modulator | Soref1987, Zhang2024a |
| V_πL treated as a standalone figure of merit | User compares two modulators on V_πL alone | No insertion loss, bias point, drive configuration or λ quoted alongside | Demand the (V_πL, IL, bandwidth, bias) tuple; Soref–Bennett guarantees that phase efficiency was bought with absorption | Modulator | Reed2010, Soref1987 |
| Ring modulator metrics quoted without thermal context | User cites a ring ER, Q, or energy-per-bit figure | No detuning, temperature, or tuning-power accounting in the same breath | Ask for dλ_res/dT, the locking scheme, and whether heater power is counted in energy/bit — thermal tuning power can dominate the very energy advantage the ring was chosen for | Modulator (ring) | Shekhar2024, Margalit2021 |
| Ring resonance characterized at operating power and read as linear | User reports a Q or ER from a high-power sweep | Asymmetric/triangular lineshape, or different results sweeping up vs. down in wavelength | Two-photon absorption and the free carriers it generates cause thermal bistability; sweep at reduced power and in both directions before extracting Q | Modulator (ring) | Shekhar2024 |
| Small-signal bandwidth read as large-signal link performance | User cites an S21 f_3dB to argue a PAM4 rate is achievable | No eye/BER data, no driver in the loop, chirp not mentioned | f_3dB is necessary, not sufficient: chirp, linearity and driver swing decide PAM4 quality. Ask for eye or BER data with the intended driver | Modulator | Margalit2021 |
| Ge responsivity extrapolated across the C/L band | User applies a 1550 nm responsivity to 1600+ nm | No strain state reported for the Ge layer | Ge's direct gap ≈0.80 eV ≈ 1550 nm; only deliberate tensile strain extends the edge (0.20% → ≈0.77 eV; ≈0.25% → band edge 1550→1623 nm). Ask for the measured strain before extrapolating | Photodetector | Liu2005, Michel2010 |
| Low-power detector bandwidth assumed to hold at link power | User quotes ">40 GHz" for a receiver operating at tens of mW | The bandwidth figure and the operating optical power come from different measurement conditions | Space-charge screening and self-heating reduce bandwidth and responsivity at high power; demand a power-swept characterization. Note that even a design explicitly built for high power reports its >40 GHz bandwidth at *low* optical power | Photodetector | Cao2024 |
| Cooling assumed to improve the detector overall | User proposes low-temperature operation to cut dark current | Only the dark-current benefit is stated | Dark current falls at 200 K, but responsivity also falls because the epitaxial-Ge absorption coefficient drops (0.87 A/W at 300 K → 0.34 A/W at 200 K, alongside 4.62 nA → 93.69 pA dark current, on the same Ge-on-Si waveguide PD) — the trade is real and must be evaluated jointly, not assumed one-sided | Photodetector | Liu2025 |
| APD gain treated as free sensitivity | User proposes an APD to "get more signal" | M is quoted; F(M), gain–bandwidth product and breakdown control are not | Excess noise grows with M; past an optimum gain, sensitivity degrades. Also budget the high bias, the temperature dependence of V_br, and the added electro-thermal coupling | Photodetector (APD) | Michel2010 |
| "Silicon laser" used without naming the gain mechanism | User says a laser is "on silicon" or 「矽基雷射」 | No mention of III–V bonding/growth, quantum dots, Raman pumping, or Ge/GeSn band engineering | Si's indirect gap forbids practical telecom gain; ask which mechanism supplies gain, because the reliability, thermal and process consequences differ completely between them | Laser | Liang2010, Wang2018 |
| Integration strategies compared on optical performance alone | User ranks ELS vs. hybrid vs. heterogeneous vs. monolithic by loss or output power | Thermal isolation, known-good-die reuse, rework, bond-defect and lattice-mismatch consequences are absent from the comparison | Each strategy trades a different axis: ELS isolates heat but complicates fiber routing and reflection management; hybrid allows known-good die but needs active alignment; heterogeneous scales to wafer level but carries bond defects and thermal mismatch; monolithic growth faces threading dislocations from ≈4% (GaAs/Si) to ≈8% (InP/Si) lattice mismatch | Laser | Park2008, Guo2019 |
| T₀ ambiguity in the threshold model | User quotes "T₀ = 221 K" or similar | The same symbol denotes both the reference temperature and the characteristic temperature in I_th(T) = I_th(T₀)·exp[(T−T₀)/T₀*] | This profile writes the characteristic temperature as **T₀\*** to keep it distinct from the reference temperature T₀. Also confirm the substrate: the 221 K figure is for a QD laser on **SiC**, not on Si | Laser | Koscica2023 |
| Back-reflection ignored in the device model | User characterizes a laser under ideal isolation, then integrates it behind a fiber interface | Coupling design and laser characterization are discussed as separate problems | Uncontrolled reflection from the fiber/chip interface feeds back into the laser and degrades RIN, mode stability and linewidth — a packaging decision that shows up as a laser-physics symptom | Laser | Zhang2024b |
| Good device numbers assumed to compose into a good link | User presents best-in-class modulator, PD and laser figures as evidence the link closes | No power budget, no margin for aging/temperature/variation | Assemble P_Rx = P_laser − ΣL and check P_Rx ≥ P_sens + M_margin; several device metrics degrade *together* under a single cause (a hot ASIC raises T_j, which lowers laser power, drifts ring resonance, and raises PD dark current at the same time) | System | Shekhar2024 |

---

## 7a. Literature Anchors

Recommended reading order — build the mechanism vocabulary first, then the roadmap context.

| Type | Reference | Why it matters |
|---|---|---|
| Review (modulators) | Reed, Mashanovich, Gardes & Thomson, "Silicon optical modulators," *Nature Photonics* 4, 518–526 (2010) | The standard entry point for plasma dispersion, MZI vs. ring, and V_πL as a figure of merit. Note it carries a published erratum (Nat. Photon. 4, 660) — check it before quoting numbers |
| Review (detectors) | Michel, Liu & Kimerling, "High-performance Ge-on-Si photodetectors," *Nature Photonics* 4, 527–534 (2010) | Establishes Ge epitaxy, strain engineering, waveguide-integrated PDs and Ge-on-Si APDs as one connected design space |
| Review (sources) | Liang & Bowers, "Recent progress in lasers on silicon," *Nature Photonics* 4, 511–517 (2010) | The physics-first account of why Si cannot lase natively, and of the Raman / Ge-on-Si / hybrid III–V routes around it |
| Review (emerging) | Wang & Liu, "Emerging technologies in Si active photonics," *Journal of Semiconductors* 39, 061001 (2018) | Covers monolithic Ge/GeSn lasers, quantum-dot lasers, and novel modulator/detector materials beyond the 2010 reviews |
| Perspective (system) | Margalit, Xiang, Bowers, Bjorlin, Blum & Bowers, "Perspective on the future of silicon photonics and electronics," *Applied Physics Letters* 118, 220501 (2021) | Places device metrics inside large-scale integration, multi-wavelength sources and the foundry ecosystem |
| Roadmap | Shekhar, Bogaerts, Chrostowski, Bowers, Hochberg, Soref & Shastri, "Roadmapping the next generation of silicon photonics," *Nature Communications* 15, 751 (2024) | The current architectural framing for laser/modulator/PD/SiN/heterogeneous integration, including ring wavelength/thermal sensitivity as a system constraint |
| Material integration | Zhang, Guo, Ji, Shen, He & Su, "What can be integrated on the silicon photonics platform and how?" *APL Photonics* 9, 090902 (2024) | Organizes gain materials, EO materials, Ge detectors and low-loss waveguides as a materials-selection problem |

---

## 7b. Source Ledger (the resolution key for every `[Key]` used in Nodes 1–6)

> Legend — **Access tag**: `[full]` full text read · `[partial]` preview/excerpt only · `[abstract]`
> abstract/metadata only · `[secondary]` known via another source citing it.
> **Verification status**: ✅ Confirmed (checked directly against the source or its publisher
> metadata record) · `~` Approximate (general claim corroborated; exact figure not independently
> re-derived) · ⚠ Unconfirmed · ❌ Withdrawn.
>
> **Intake corrections (2026-08-24)** — three errors in the source packet were found and fixed
> while building this ledger. They are recorded here so a future editor does not reintroduce them:
> 1. `[^5]` was attributed to "Xiang et al." in *APL Photonics*. The work is **Margalit et al.** in
>    **Applied Physics Letters** 118, 220501 (2021) — both the first author and the journal were wrong.
> 2. `[^13]` was attributed to "Chen et al." The authors are **Wang & Liu**.
> 3. `[^7]` was a **Nature topical-collection landing page**, cited as the source for three
>    different review articles (Reed, Michel, Liang & Bowers). All three are real and are now
>    cited individually with their own DOIs; the index itself resolved to no specific work.

> **Verified (date)** (`domain-expansion-guide.md` §3.7): when this row's claim was last checked
> against the primary source — not the source's own publication year.
>
> **2026-08-26 currency pass** (audit trail: `reports/2026-08-26-scientific-research-guide-source-currency-pass.md`).
> All 16 rows had their bibliographic identity re-resolved against Crossref: **zero mismatches** — an
> unusually clean ledger, because an earlier intake pass had already caught this profile's author and
> venue errors. What the pass did find lives at the *claim* level, which identity checking never
> reaches: **Kim2014's result was stated backwards** in Node 5 (the paper reports >2× lower current
> for the same attenuation — an efficiency result — not >2× attenuation at equal current), and
> **Liu2005 is probably a citation conflation** (the 0.20 % → 0.77 eV figure appears to belong to a
> different, uncited 2005 Liu et al. paper). The second is flagged, not fixed: both papers are
> paywalled with no open route, and a search-snippet match is not evidence. Also added: the
> §3.7 **version pin** the Soref–Bennett relation was missing — the profile now names the later
> Nedeljkovic et al. (2011) revision as a distinct coefficient set that must not be mixed in.

| Key | Full citation | Identifier | Access tag | Verification status | Verified (date) | Locator | Used in (Node/row) |
|---|---|---|---|---|---|---|---|
| Soref1987 | R. A. Soref & B. R. Bennett, "Electrooptical effects in silicon," *IEEE J. Quantum Electron.* 23(1), 123–129 (1987) | DOI: 10.1109/JQE.1987.1073206 | [abstract] | ✅ Confirmed (publisher metadata verified 2026-08-24; the 1.55 µm coefficient set independently corroborated in secondary literature) | 2026-08-26 — identity re-confirmed via Crossref. ⚠ **Version-pinning gap found, not silently closed:** the profile states the 1.55 µm coefficients without saying whether they are the original 1987 values or the later revision; Node 4 row 1 now names Nedeljkovic, Soref & Mashanovich, *IEEE Photon. J.* 3(6), 1171–1180 (2011), DOI 10.1109/JPhot.2011.2171930 (citation independently re-checked against Crossref by the main session) as the distinct alternative set. Whether this profile's numbers *differ* from that revision was **not** determined — that needs Nedeljkovic's full text | The 1.55 µm empirical Δn/Δα fits | N1 constraint 3; N2 modulator IL row; N4 row 1; N5 V_πL row; N6 rows 1–2 |
| Reed2010 | G. T. Reed, G. Mashanovich, F. Y. Gardes & D. J. Thomson, "Silicon optical modulators," *Nature Photonics* 4(8), 518–526 (2010) — **erratum**: Nat. Photon. 4(9), 660 (2010), DOI: 10.1038/nphoton.2010.219 | DOI: 10.1038/nphoton.2010.179 | [abstract] | ✅ Confirmed (full citation and the existence of the erratum verified 2026-08-24) | 2026-08-26 — identity and the erratum both re-confirmed via Crossref | Plasma-dispersion / MZI / ring sections | N1 constraint 3; N2 V_π row; N4 rows 1, 3; N5 V_πL row; N6 row 2; N7a |
| Michel2010 | J. Michel, J. Liu & L. C. Kimerling, "High-performance Ge-on-Si photodetectors," *Nature Photonics* 4(8), 527–534 (2010) | DOI: 10.1038/nphoton.2010.157 | [abstract] | ✅ Confirmed (citation verified 2026-08-24); the APD and modal-absorption guidance drawn from it is `~` Approximate — general review content, not a pinned figure | 2026-08-26 — identity re-confirmed via Crossref (not re-read in full this pass) | Ge epitaxy / waveguide PD / APD sections | N1 constraint 8; N2 APD row; N4 rows 5–7; N5 APD row; N6 rows 6, 9; N7a |
| Liang2010 | D. Liang & J. E. Bowers, "Recent progress in lasers on silicon," *Nature Photonics* 4(8), 511–517 (2010) | DOI: 10.1038/nphoton.2010.167 | [abstract] | ✅ Confirmed (citation verified 2026-08-24) | 2026-08-26 — identity re-confirmed via Crossref (not re-read in full this pass) | Indirect-gap discussion; Raman / hybrid III–V routes | N1 constraint 1; N2 linewidth row; N6 row 10; N7a |
| Wang2018 | X. Wang & J. Liu, "Emerging technologies in Si active photonics," *J. Semicond.* 39(6), 061001 (2018) | DOI: 10.1088/1674-4926/39/6/061001 | [abstract] | ✅ Confirmed (authorship corrected from the source packet's "Chen et al.", 2026-08-24) | 2026-08-26 — identity re-confirmed via Crossref (not re-read in full this pass) | Ge/GeSn laser, QD laser, novel modulator sections | N1 constraint 1; N6 row 10; N7a |
| Margalit2021 | N. Margalit, C. Xiang, S. M. Bowers, A. Bjorlin, R. Blum & J. E. Bowers, "Perspective on the future of silicon photonics and electronics," *Appl. Phys. Lett.* 118(22), 220501 (2021) | DOI: 10.1063/5.0050117 | [abstract] | ✅ Confirmed (author list and journal corrected from the source packet, 2026-08-24) | 2026-08-26 — identity re-confirmed via Crossref (not re-read in full this pass) | Integration/roadmap perspective | N1 constraint 4; N2 EO-bandwidth and BER rows; N5 link-budget row; N6 rows 3, 5 |
| Shekhar2024 | S. Shekhar, W. Bogaerts, L. Chrostowski, J. E. Bowers, M. Hochberg, R. Soref & B. J. Shastri, "Roadmapping the next generation of silicon photonics," *Nature Communications* 15(1), 751 (2024) | DOI: 10.1038/s41467-024-44750-0 | [abstract] | ✅ Confirmed (full author list and article number verified 2026-08-24) | 2026-08-26 — identity re-confirmed via Crossref (not re-read in full this pass) | Ring modulator + multi-wavelength source architecture discussion | N1 constraint 4; N2 ring row; N4 row 4; N5 ER and link-budget rows; N6 rows 3, 4, 14 |
| Zhang2024a | Y. Zhang, X. Guo, X. Ji, J. Shen, A. He & Y. Su, "What can be integrated on the silicon photonics platform and how?" *APL Photonics* 9(9), 090902 (2024) | DOI: 10.1063/5.0220463 | [abstract] | ✅ Confirmed (citation verified 2026-08-24) | 2026-08-26 — identity re-confirmed via Crossref (not re-read in full this pass) | Material-integration survey (gain, EO, detector, waveguide) | N1 constraint 2; N6 row 1; N7a |
| Zhang2024b | J. Zhang, A. G. Shankar & X. Wang, "On-Chip Lasers for Silicon Photonics," *Photonics* 11(3), 212 (2024) | DOI: 10.3390/photonics11030212 | [abstract] | ~ Approximate (citation ✅ verified 2026-08-24; the RIN/feedback guidance attributed to it is general on-chip-laser review content, not a pinned figure) | 2026-08-26 — identity re-confirmed via Crossref (not re-read in full this pass) | On-chip laser review | N2 RIN and back-reflection rows; N6 row 13 |
| Kim2014 | Y. Kim, M. Takenaka, T. Osada, M. Hata & S. Takagi, "Strain-induced enhancement of plasma dispersion effect and free-carrier absorption in SiGe optical modulators," *Scientific Reports* 4, 4683 (2014) | DOI: 10.1038/srep04683 | [full] | ✅ Confirmed (1.3× Δn / 1.7× Δα, Si₀.₈₆Ge₀.₁₄, 0.48% compressive strain = 85% of maximum, 1.55 µm — all read from the open-access text 2026-08-24) | 2026-08-26 — **re-read in full** (open preprint, arXiv:1304.1229). Ge fraction, strain, wavelength and the 1.3×/1.7× factors all reproduce. ⚠ This re-read found that Node 5 **stated the paper's comparison backwards**: the source reports 24 vs 55 mA/mm to reach the *same* 20 dB attenuation — a >2× efficiency result — not >2× attenuation at equal current. Node 5 corrected the same day | Results: enhancement factors and device comparison | N4 row 2; N5 strain-enhancement row |
| Liu2005 | J. Liu, D. D. Cannon, K. Wada, Y. Ishikawa, S. Jongthammanurak, D. T. Danielson, J. Michel & L. C. Kimerling, "Tensile strained Ge p-i-n photodetectors on Si platform for C and L band telecommunications," *Appl. Phys. Lett.* 87(1), 011110 (2005) | DOI: 10.1063/1.1993749 | [abstract] | ~ Approximate (citation ✅ verified 2026-08-24; the 0.20% → 0.77 eV and 0.25% → 1623 nm figures are corroborated in the strained-Ge literature but were read from secondary summaries, not the primary full text) | 2026-08-26 — identity re-confirmed via Crossref; **claim-level check attempted and blocked** (publisher 403, no open route). ⚠ **Probable citation conflation, unresolved:** two independent searches converge on attributing the "0.20 % strain → 0.77 eV" figure to a *different* 2005 Liu et al. paper — *Appl. Phys. Lett.* **87**(10), 103501, DOI 10.1063/1.2037200 — while the paper cited here is 87(1), 011110. A search-snippet convergence is not evidence, so nothing was changed: the claim is flagged in N1 constraint 5 and stays attributed as-is until someone reads both papers. `review-when:` either paper's full text becomes accessible | Strain-induced direct-gap shrinkage and band-edge extension | N1 constraint 5; N2 Ge-strain row; N6 row 6 |
| Liu2025 | J. Liu, Z. Li, X. Liu, W. Yan, X. Zhao, S. Zheng, Y. Qiu, Q. Zhong, Y. Dong & T. Hu, "Low Temperature Characteristics of Ge-on-Si Waveguide Photodetectors: A Combined Simulation and Experimental Study," *Micromachines* 16(5), 542 (2025) | DOI: 10.3390/mi16050542 | [abstract] | ✅ Confirmed (abstract states: "Under a −3 V bias, the PD exhibits a room-temperature dark current of 4.62 nA and a responsivity of 0.87 A/W at 1550 nm"; 200–300 K, 1500–1600 nm study range) | 2026-08-26 — re-confirmed against the full abstract text in the Crossref record: 4.62 nA / 0.87 A/W at −3 V, room temperature, verbatim; the 200 K pair (0.34 A/W, 93.69 pA) was recovered in the same read and has now been added to N6 row 8, which previously described the trade-off only qualitatively | Abstract | N2 responsivity and dark-current rows; N5 responsivity and dark-current rows; N6 row 8 |
| Cao2024 | H. Cao, Y. Xiang, W. Sun, J. Xie, J. Guo, Z. Yu, L. Liu, Y. Shi & D. Dai, "High-Power Ge/Si Waveguide Photodetector," *ACS Photonics* 11(4), 1761–1770 (2024) | DOI: 10.1021/acsphotonics.4c00173 | [abstract] | ✅ Confirmed (0.68 A/W at 28 mW input optical power, and >40 GHz bandwidth stated for *low* optical power, both corroborated 2026-08-24) | 2026-08-26 — identity re-confirmed via Crossref; claim-level re-check **attempted and blocked** (publisher 403, no abstract on the fallback indexes), so the 2026-08-24 corroboration stands unrefreshed. `review-when:` the full text or a complete abstract record becomes reachable | Abstract | N2 bandwidth and saturation rows; N5 high-power responsivity row; N6 row 7 |
| Park2008 | H. Park, A. W. Fang, D. Liang, Y.-H. Kuo, H.-H. Chang, B. R. Koch, H.-W. Chen, M. N. Sysak, R. Jones & J. E. Bowers, "Photonic Integration on the Hybrid Silicon Evanescent Device Platform," *Advances in Optical Technologies* 2008, 682978 (2008) | DOI: 10.1155/2008/682978 | [abstract] | ✅ Confirmed (citation verified 2026-08-24) | 2026-08-26 — identity re-confirmed via Crossref (not re-read in full this pass) | Hybrid silicon evanescent platform: low-temperature wafer bonding of III–V onto Si waveguides | N2 bond-interface row; N6 row 11 |
| Guo2019 | X. Guo, A. He & Y. Su, "Recent advances of heterogeneously integrated III–V laser on Si," *J. Semicond.* 40(10), 101304 (2019) | DOI: 10.1088/1674-4926/40/10/101304 | [abstract] | ~ Approximate (citation ✅ verified 2026-08-24; the ≈8% InP/Si and ≈4% GaAs/Si mismatch figures follow directly from published room-temperature lattice constants and were not re-read from this paper's text) | 2026-08-26 — identity re-confirmed via Crossref (not re-read in full this pass); the ≈4 %/≈8 % mismatch figures follow from published lattice constants and are independent of this paper's own text, which was not re-read | Heterogeneous III–V-on-Si integration review | N2 TDD row; N5 lattice-mismatch row; N6 row 11 |
| Koscica2023 | R. Koscica, Y. Wan, W. He, M. J. Kennedy & J. E. Bowers, "Heterogeneous integration of a III–V quantum dot laser on high thermal conductivity silicon carbide," *Optics Letters* 48(10), 2539 (2023) | DOI: 10.1364/OL.486089 | [abstract] | ✅ Confirmed (T₀* ≈ 221 K near room temperature, lasing sustained to 105 °C, on a **SiC** substrate — corroborated 2026-08-24) | 2026-08-26 — re-confirmed against the full abstract text in the Crossref record, verbatim ("a large T₀ of 221 K near room temperature"), together with the SiC substrate and the 105 °C lasing limit — stronger evidence than this row previously carried | Abstract | N1 constraint 7; N2 LIV and T₀ rows; N4 rows 8–9; N5 T₀* row; N6 row 12 |

---

## Cross-Domain Links

### Closest Related Domain Profiles

| Profile name | Overlap dimensions | Typical use split |
|---|---|---|
| `adiabatic_taper_ssc.md` (Adiabatic Taper & Spot-Size Conversion) | first principles (mode solvers, FDTD/FEM), application targets (CPO transceivers) | Use this profile for what happens *inside* an active device (carrier–photon conversion, gain, absorption, bias); use the taper profile for how a mode is matched and transferred *between* waveguides or between fiber and chip. The two meet at the link budget: the taper profile owns the L_fiber/chip term, this profile owns P_laser, L_mod and P_sens |
| `v_groove_fabrication.md` (V-Groove Fabrication) | application targets (fiber-array packaging for CPO) | Use the V-groove profile for mechanical fiber fixturing precision; use this profile when the question is what a resulting coupling-loss change does to laser drive power, receiver margin or BER |
| `fiber_chip_passive_alignment.md` (Fiber-to-Chip Passive Alignment) | application targets (edge-coupled photonic packages), quality metrics (insertion-loss drift over temperature and aging) | Use the alignment profile for where the fiber core physically ends up and how that placement drifts; use this profile for what the resulting insertion-loss distribution does to the link's power margin and BER. An alignment-drift finding becomes a *device* problem only through the budget terms owned here |
| `microled.md` (Inorganic MicroLED Devices) | first principles (radiative/non-radiative recombination, LIV characterization, direct-gap III-V emission) | Both handle carrier recombination and calibrated optical measurement, but the metric sets do not transfer: microLED optimizes EQE/LEE/droop for display pixels; this profile optimizes threshold, slope efficiency, linewidth and RIN for a coherent single-mode source feeding a data link |
| `gan_power_device.md` (Vertical GaN Power Devices) | measurement tools (TCAD drift-diffusion, C-V, breakdown characterization), first principles (junction electrostatics) | Shared electrostatics and TCAD vocabulary only. Do not import power-device breakdown/R_ON criteria into an APD or modulator junction design — the optimization targets are unrelated |
| `siph_packaging_reliability.md` (Silicon Photonics Packaging & Reliability, 矽光子封裝與可靠度) | quality metrics (thermal budget, junction temperature, post-stress drift), application targets (CPO optical engines) | Use this profile for device-level physics under thermal stress — what the carrier/photon/thermal mechanism is. Use that profile for system-level I/O density, package thermal architecture, and qualification. **Same observable, two explanations**: a laser/ring drift or a dark-current rise is this profile's device physics and that profile's failure mode — if the thermal boundary condition moved between measurements, it is a packaging observation, not device degradation. See that profile's Cross-Domain Conflict Notes for the confirmation question |

### Boundary & ownership notes

- This profile is intentionally scoped to *active* devices. Passive routing, splitters and filters
  belong with the taper/coupling profile or a future passive-Si-photonics profile.
- The three device families (source, modulator, detector) are carried in one base profile because
  they share Node 1's first principles, Node 3's toolchain, and a single link-budget consumer. If
  any one family grows its own fitting methods and pitfalls beyond what a shared table can carry,
  promote it to a sub-profile under `domains/silicon_photonics_device_physics/` per the expansion
  guide's Gate 2 — done for the ring-modulator thermal-control branch on 2026-08-26, see
  `silicon_photonics_device_physics/ring_resonator_thermal_control.md`.

---

## Cross-Domain Conflict Notes

| Issue / constraint | Other profile(s) involved | Potential conflict | AI confirmation question |
|---|---|---|---|
| Where the loss budget is actually spent | `adiabatic_taper_ssc.md` | The taper profile optimizes a single coupling interface; this profile may recommend raising laser power or modulator ER to recover the same margin. Optimizing both independently double-counts the recovered budget | "Are we trying to close this link by reducing coupling loss, or by increasing source power / receiver sensitivity? Both change the same margin term and should not be credited twice" |
| MFD/tolerance target vs. device thermal budget | `adiabatic_taper_ssc.md`, `v_groove_fabrication.md` | A packaging change that improves alignment tolerance may move the laser closer to the ASIC hotspot, raising T_j and undoing the gain through I_th and wavelength drift | "Does the proposed fiber-attach or coupler change move the laser's thermal path? A tolerance win that raises T_j may be a net loss" |
| Recombination vocabulary shared with microLED | `microled.md` | SRH/Auger/surface recombination language is common to both, but a microLED EQE argument does not transfer to a laser threshold argument (below vs. above threshold, spontaneous vs. stimulated regime) | "Is the device operating below threshold (spontaneous emission, EQE-style bookkeeping) or above threshold (stimulated emission, I_th/slope-efficiency bookkeeping)?" |
| Junction design goals shared with power devices | `gan_power_device.md` | Both reason about depletion regions and breakdown, but an APD deliberately operates near breakdown while a power device is designed to avoid it | "Is breakdown here a failure mode to be avoided, or the operating mechanism (avalanche gain) to be controlled?" |
