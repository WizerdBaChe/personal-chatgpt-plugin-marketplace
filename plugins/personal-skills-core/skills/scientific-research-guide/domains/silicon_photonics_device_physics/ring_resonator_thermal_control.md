---
xi: 1
what: "Sub-profile: Ring Resonator Thermal Control (環形諧振腔熱控制) — under Silicon Photonics Device Physics — Ring-resonator thermal control: local thermo-optic drift, passive athermalization, heater tuning/feedback locking, WDM ring-to-ring thermal crosstalk, detuning-to-link-impairment chain"
tags: [srg-domain, 領域框架, sub-profile]
aliases: ["ring thermal drift", "環形諧振腔熱控制", "熱致波長漂移", "athermal ring", "無熱化環形", "TiO2 cladding", "titanium oxide cladding", "liquid crystal cladding", "LC cladding", "ring heater", "heater tuning efficiency", "wavelength locking", "thermal dithering", "TDWS", "mW/FSR", "ring-to-ring thermal crosstalk", "microring thermal crosstalk", "Kij crosstalk matrix", "thermal RC model ring"]
date: 2026-09-02
status: live
profile_type: sub-profile
parent: "silicon_photonics_device_physics"
---
# Sub-profile: Ring Resonator Thermal Control (環形諧振腔熱控制) — under Silicon Photonics Device Physics

> Parent domain: `silicon_photonics_device_physics.md`
> Branch axis: phenomenon / method
> Scope: local thermo-optic coupling in Si-MRRs, passive athermalization (negative-TOC
> cladding, MZI phase balancing), heater-based tuning and feedback locking, ring-to-ring
> thermal crosstalk in WDM banks, and the chain from resonance detuning to link-level
> impairment (ER/IL/BER). This branch extends the parent's Node 1 constraint 4 ("A ring
> resonator's operating point is a moving target") with the full thermal-control physics,
> control architectures, and pitfalls that a shared table cannot carry.
> Inherits from parent: Nodes 1–3's device-physics core (resonance condition, carrier–photon
> chain, link-budget accounting) and Node 2's general spectral characterization tools. This
> file adds the thermal-specific theory, tools, toolchain, fitting methods, metrics, and
> pitfalls below rather than duplicating the parent's generic ring-modulator content.
>
> Bulk silicon dn/dT and carrier electro-optic mechanisms are owned by the parent profile;
> package-/ASIC-scale thermal-field simulation is owned by `siph_packaging_reliability.md`
> (see Cross-Domain Links). This branch owns the ring-specific local thermal response and
> its control.
>
> Primary source types:
> - Review: Padmaraju & Bergman (2014)
> - Primary device studies: Ptasinski et al. (2014); Guha et al. (2013); Dahlem et al. (2011);
>   DeRose et al. (2014); Grillanda et al. (2017); Qiu et al. (2015)
>
> Intake note: this branch was compiled from a user-supplied AI-research-tool packet.
> Per `domain-expansion-guide.md` §9's intake stance ("assume the packet is defective until
> each anchor is resolved"), every Node 7b key was independently re-resolved against
> publisher/Crossref metadata before this file was registered — see the Provenance &
> correction log in the Source Ledger below. **5 of 8 sources carried at least one
> bibliographic-identity defect** (wrong DOI, fabricated co-authors, wrong volume/issue/pages,
> or wrong venue name), consistent with every other AI-packet intake this SKILL has processed.

## Citation convention

Same rule as the parent (`domain-expansion-guide.md` §3.2/§3.7): every inline citation is a
human-resolvable `[Author Year]` key with a Source Ledger row, every quantitative claim states
its material system/method/wavelength/temperature/geometry in the same breath as the number,
and every ledger row carries a `Verified (date)` cell. `full` means full text directly read;
`abstract` means only abstract/metadata directly read; `partial` means an excerpt/preview only.

---

## 1. Theoretical Framework Anchoring (branch-specific)

For a ring at a fixed longitudinal order, the resonance condition is

\[
m\lambda_{res}=n_{eff}(\lambda,T)L(T).
\]

A first-order, dispersive form used in the microring thermal-control review is

\[
\frac{d\lambda_{res}}{dT}
=
\frac{\lambda_0}{n_g}
\left(
\frac{\partial n_{eff}}{\partial T}+n_{eff}\alpha_{sub}
\right).
\]

Padmaraju & Bergman explicitly note that the terms have wavelength dependence; for the usual
strongly Si-confined SOI mode, they reduce the expression by neglecting SiO₂'s much smaller TOC
and the Si substrate expansion term relative to Si's thermo-optic coefficient. This reduced form
is valid only under the stated modal-confinement and first-order assumptions; it is not a
replacement for a full multi-material eigenmode calculation for LC/TiO₂/slot
geometries.[PadmarajuBergman2014, §2, Eqs. (1)–(2)]

Near an isolated resonance, a Lorentzian transmission approximation can be written as

\[
T(\Delta\omega)\propto \frac{1}{1+\left(2\Delta\omega/\kappa\right)^2},
\qquad
Q=\frac{\omega_0}{\kappa}=\frac{\lambda_0}{\Delta\lambda_{FWHM}}.
\]

Thus a thermal perturbation maps into normalized detuning \(\Delta\lambda/\Delta\lambda_{FWHM}\),
not merely an absolute pm shift. High \(Q\) narrows the linewidth and hence can reduce allowable
temperature motion at a fixed wavelength-tracking requirement.[PadmarajuBergman2014, §2]

### Inviolable physical constraints (branch-specific additions to parent constraint 4)

1. **Athermal means reduced, not generically zero, thermal drift.** Effective TOC cancellation
   requires both a negative-TOC material and a geometry-specific modal overlap; higher-order
   wavelength dependence and fabrication variations obstruct broadband, perfectly flat
   cancellation.[PadmarajuBergman2014, §3.1]
2. **A heater provides practical heating, not efficient local cooling.** Control architectures
   commonly initialize the ring "hot" so later ambient changes can be corrected by increasing or
   decreasing heater power; relying on a heater to correct an already-too-hot local hotspot by
   active cooling is not the same control problem.[PadmarajuBergman2014, §4]
3. **Center-wavelength lock does not guarantee unchanged ER or insertion loss.** Tuning may alter
   loss/coupling or cause feedback dither to broaden the effective resonance; the control endpoint
   must include spectral shape and/or data-link performance, not only \(\lambda_{res}\).
   [PadmarajuBergman2014, §§4.1–4.2; Padmaraju2013]
4. **A diagonal heater calibration is invalid in a dense WDM ring bank once crosstalk is
   measurable.** Each ring's shift must be represented by its own heater contribution plus
   off-diagonal thermal terms, and the matrix must be re-identified after layout/metal-stack
   changes.[DeRose2014, pp. 125–126]

> **Decision point (mandatory Tier 0 confirmation):** Is the device primarily **(A) a ring
> modulator**, **(B) a passive WDM filter/MUX/DEMUX**, or **(C) a weight bank/switch fabric**?
> Also state: target wavelength/band, loaded \(Q\) or linewidth, expected local temperature
> excursion, channel spacing, number/pitch of nearby heated rings, and whether the allowed
> solution contains non-CMOS claddings or only foundry-compatible layers. These choices change
> the acceptable \(d\lambda/dT\), tuning range, sensing method, and crosstalk budget.

---

## 2. Measurement Tool Inventory (branch-specific)

### Spectral and thermal characterization

| Measurement target | Tool | Output information | Applicable conditions | Common misuse | Source [Key] |
|---|---|---|---|---|---|
| Resonance wavelength and loaded \(Q\) | Tunable telecom laser sweep + power-meter transmission | \(\lambda_{res}(T)\), FSR, \(\Delta\lambda_{FWHM}\), loaded \(Q\), ER | State laser range/resolution, polarization, port, sweep direction/rate, temperature stabilization | Quoting \(Q\) without defining loaded/intrinsic or fit method; comparing scans with thermal self-heating ignored | [Ptasinski2014] |
| Temperature coefficient of resonance | Temperature-controlled stage/TEC + repeated spectral sweeps | \(d\lambda_{res}/dT\) and linearity interval | Temperature sensor should be mechanically/thermally tied to sample; report range and precision | Calling a stage temperature the ring-core temperature without thermal calibration | [Ptasinski2014] |
| LC-cladding TOC inference | Measured ring shift + calibrated finite-element/eigenmode model | cladding \(dn/dT\), \(\Delta n_{eff}\) | Requires known waveguide cross section, cladding state, polarization and wavelength | Treating random/unknown LC director alignment as a scalar isotropic material constant | [Ptasinski2014] |
| Heater efficiency and dynamics | DC electrical sweep plus time-resolved optical transmission / lock-in | pm/mW, GHz/mW, mW/FSR, \(\tau_{th}\), rise/fall | Report heater material, oxide separation, ring geometry, ambient, power definition | Comparing mW/nm across ring radii without accounting for FSR; ignore resistance drift | [PadmarajuBergman2014] |
| Thermal-crosstalk transfer matrix | Drive one heater at a time; track all ring resonances / infrared thermography only as auxiliary | \(K_{ij}=\partial\lambda_i/\partial P_j\), spatial decay, asymmetry | Need full electrical/metal stack and same boundary condition as use case | Infer crosstalk only from physical spacing; omit metal heat paths | [DeRose2014] |
| Feedback-lock quality | Integrated photodetector / transparent detector / drop-port monitor + controller logging | lock error, settling, capture range, wavelength stability, actuator duty/power | Must distinguish laser drift, ring drift and photodetector amplitude drift | Quote wavelength stability without measurement bandwidth or response time | [Grillanda2017] |
| Link-level consequence | PRBS eye, BER, TDECQ or system-specific error metric with controlled detuning | ER/IL penalty, eye closure, BER/error floor vs detuning | Need stated data rate, modulation, receiver, wavelength, temperature/crosstalk condition | Translate a passive filter depth directly into BER without a transmitter/receiver experiment or model | [PadmarajuBergman2014] |

Ptasinski et al. used an Agilent 8163B tunable laser covering **1470–1570 nm**, a polarization
scrambler, free-space imaging to a Newport 2931-C power meter, and a thermocouple fastened to
the sample stage with stated **0.1°C** precision. Their direct spectral measurements were on
SOI rings of **9.9 μm radius**, **500 nm width**, **250 nm height**, and **100 nm ring–bus
gap**; this apparatus supports temperature-dependent resonance extraction, not a direct map of
on-chip spatial temperature gradients.[Ptasinski2014, §3.1–3.2 — re-verified against the full
text 2026-08-26]

### Thermal-control and local-temperature tools

| Measurement target | Tool | Output information | Applicable conditions | Common misuse | Source [Key] |
|---|---|---|---|---|---|
| Indirect resonance-drift monitor | Drop-port / in-situ photodiode with optical-power monitor | low-speed error signal | Must state whether signal is passive or data-modulated, and laser-power sensitivity | Treat signal power as unique wavelength error when laser amplitude changes | [PadmarajuBergman2014, §4.2] |
| Anti-symmetric lock error | Thermal/electrical dither + synchronous demodulation | sign of detuning about resonance | Dither amplitude/frequency must be compared with thermal bandwidth and allowable ER penalty | Use a dither amplitude chosen only for SNR without testing spectral broadening/ER | [Padmaraju2013] |
| Spatial temperature field | IR microscopy / thermoreflectance / calibrated Raman / embedded temperature sensing | hotspot profile, thermal gradient, thermal time response | Requires emissivity/calibration or optical-temperature calibration at device scale | Using macroscopic IR temperature as the ring-waveguide core temperature | [PadmarajuBergman2014, §4.2] |

---

## 3. Standard Modeling Toolchain (branch-specific)

```text
Waveguide cross-section + material dispersion + cladding state
→ eigenmode / FEM mode solver
→ Output: neff(λ,T), ng(λ,T), modal overlap Γi, dλres/dT
    ↓
Heater geometry + oxide/metal/substrate stack + boundary conditions
→ 3D electro-thermal FEM or experimentally identified thermal RC model
→ Input: Pj(t), ambient / package local temperature
→ Output: Ti(t), Kij = ∂λi/∂Pj, τth,i, thermal crosstalk matrix
    ↓
Coupled ring spectral model + control-loop model
→ Input: λlaser(t), λres,i(t), Q/κ, coupling/loss, sensor noise, actuator range
→ Output: IL/ER vs detuning, lock error, settling, power, spectral ghost response
    ↓
WDM link / receiver model or experiment
→ Output: eye metric / BER-related penalty versus thermal excursion and cross-channel actuation
```

For passive cladding, the first-order effective TOC must be formed from the modal overlaps:

\[
\frac{dn_{eff}}{dT}
\approx
\Gamma_{core}\frac{dn_{core}}{dT}
+
\Gamma_{clad}\frac{dn_{clad}}{dT}
+
\Gamma_{sub}\frac{dn_{sub}}{dT}.
\]

Padmaraju & Bergman emphasize that this linear overlap form omits higher-order wavelength
dependence; it should therefore be fitted/validated at the intended wavelength and over the
intended temperature span, rather than used as a universal athermal
guarantee.[PadmarajuBergman2014, §3.1, Eq. (3)]

For a ring array, a minimal linearized thermal model is

\[
\Delta\lambda_i(t)=\sum_j K_{ij}P_j(t)+S_i\Delta T_{amb}(t),
\]

where \(K_{ii}\) is self-tuning response, \(K_{ij}\) for \(i\ne j\) is thermal crosstalk, and
\(S_i=d\lambda_i/dT\) is residual ambient sensitivity. The linear model is a local
approximation: it must be re-identified if heater resistance, temperature-dependent material
properties, or operation point changes appreciably.

---

## 4. Domain-Specific Fitting Methods

| Method | Applicable question | Applicable conditions | Common error | Correct approach | Source [Key] |
|---|---|---|---|---|---|
| Linear \(\lambda_{res}(T)\) regression | What is local thermal sensitivity in a defined range? | No observable phase transition, mode hop, hysteresis or appreciable self-heating in selected range | Fit one slope across LC clearing transition or a resonance-shape change | State temperature interval, heating/cooling direction, wavelength, polarization and fit residual | [Ptasinski2014] |
| Lorentzian / coupled-mode spectral fit | How do \(Q\), linewidth, ER and detuning evolve? | Isolated resonance and stated port/coupling model | Equate a dip depth change with a center-wavelength shift only | Fit \(\lambda_0\), linewidth, depth/coupling and baseline jointly; inspect residuals for Fano/thermal-bistable shape | [PadmarajuBergman2014, §2] |
| Modal-overlap TOC fit | Which cladding width/thickness gives targeted \(d\lambda/dT\)? | Validated cross section and material dispersion/TOC at target \(\lambda,T\) | Use bulk TOC without mode-overlap or assume SiO₂ has negative TOC | Compute \(\Gamma_i\), use measured/material-specific \(dn_i/dT\), then verify ring slope experimentally | [Ptasinski2014; PadmarajuBergman2014, §3.1] |
| Heater transfer-function fit | How much power/speed/crosstalk does a heater produce? | Small-signal modulation around relevant DC operating power | Use a steady-state pm/mW slope to predict transient lock bandwidth | Fit static self/cross responses and dynamic \(K_{ij}(s)\) or RC poles; retain DC bias and ambient conditions | [PadmarajuBergman2014, §4.1] |
| Crosstalk-matrix identification | Can a multi-ring controller independently place channels? | Actuate each heater, observe every ring under same thermal boundary condition | Calibrate rings independently / treat \(K_{ij}=0\) | Measure and invert/regularize full \(\mathbf K\); update after metal routing/package change | [DeRose2014] |
| Dither lock-in estimation | Is resonance to laser on the blue or red side? | Dither remains small relative to spectral linewidth and control bandwidth | Increase dither only to improve SNR, ignoring ER cost | Optimize amplitude/frequency for error slope, sensor noise, ring thermal response and permitted ER reduction | [Padmaraju2013] |
| End-to-end detuning penalty curve | What detuning is allowed by a link budget? | Fixed modulation format, data rate, receiver, optical power, temperature and adjacent-channel condition | Declare a generic "ER threshold" without link definition | Sweep controlled detuning and report IL/ER/eye/BER or a specified validated proxy | [PadmarajuBergman2014, §§4.2–5] |

A direct dither-cost example: in a silicon microring of reported \(Q\approx14{,}000\),
Padmaraju et al.'s SRC TechCon paper reports ER reductions of **1.9 dB** and **4.8 dB** for
square-wave thermal dithers of **0.1 K** and **0.2 K**, respectively. The measurement is ring-
and dither-waveform-specific; it establishes that a stabilizing dither itself can consume ER
margin and must be included in the control budget. ⚠ This figure was corroborated in the
2026-08-26 authoring pass via the author's own publication listing and the paper's Best-in-
Session recognition, but the primary PDF's Fig. 4 could not be independently re-parsed this
pass (tool-format limitation, not a source-access block) — treat as `~ Approximate` until a
future pass re-extracts it directly.[Padmaraju2013, "Initialization and Stabilization…", Fig. 4
discussion]

---

## 5. Domain-Specific Quality Metrics

| Metric | Abbreviation | Physical meaning | Typical value range | Conditions (material/method/wavelength/temp…) | Source [Key] |
|---|---|---|---|---|---|
| Resonance thermal drift | TDWS / \(d\lambda_{res}/dT\) | Wavelength shift per temperature | Not a universal range | Air-clad SOI ring, radius 9.9 μm, 500×250 nm cross section, 100 nm gap: 87.5 pm/°C; measured with 1470–1570 nm tunable laser and TEC stage | [Ptasinski2014, §2.2; §3.2] |
| LC-reduced thermal drift | TDWS | Residual shift after negative-TOC cladding | Not a universal range | Same SOI geometry: 5CB cladding 40 pm/°C from 24–32°C; E7 56.3 pm/°C from 24–56°C; Lixon 52.3 pm/°C from 24–46°C; MDA-05-2968 58 pm/°C from 24–74°C | [Ptasinski2014, Table 2] |
| LC bulk average TOC | \(d\langle n\rangle/dT\) | Negative cladding material TOC inferred at 1550 nm | Material/state-specific | 5CB: \(-8.7\times10^{-4}\)/°C; E7: \(-6.7\times10^{-4}\)/°C; Lixon: \(-7.2\times10^{-4}\)/°C; MDA-05-2968: \(-6.5\times10^{-4}\)/°C. Derived using measured ring shifts plus COMSOL model over a 30°C rise | [Ptasinski2014, Table 3] |
| Cladding-mode overlap | \(\Gamma_{clad}\) | Fraction of modal power interacting with cladding | Geometry-specific | FEM calculation for 500×250 nm Si waveguide with \(n=1.53\) cladding: 26%; for 300 nm width: 58% | [Ptasinski2014, §2.2, Fig. 5] |
| Heater tuning efficiency | \(\eta_P\) | Electrical power per spectral shift or per FSR | Structure-specific | For a 20-channel Si counter-propagating filterbank, effective thermo-optic tuning efficiency reported as 27 μW/GHz/ring; report uses its own filterbank geometry and heater implementation | [Dahlem2011, abstract] |
| Normalized heater tuning power | mW/FSR (mW/\(2\pi\)) | Power to tune one FSR; useful across ring radius | Review-reported demonstrations | Conventional separated heater results around ~100 mW/FSR; review's best cited separated-heater example ~42 mW/FSR at 14 μs; substrate-isolated examples 2.4–4.9 mW/FSR | [PadmarajuBergman2014, §4.1] |
| Thermal time constant | \(\tau_{th}\) | Thermal actuator/sensor response time | Structure-specific | Review reports undercut/isolation example as high as ~170 μs; air-trench example <10 μs; interior-heater example ~1 μs | [PadmarajuBergman2014, §4.1] |
| Lock stability | \(\sigma_{\lambda}\), \(\sigma_f\) | Residual wavelength/frequency error after feedback | Architecture-specific | Silicon-photonics multiplexer feedback: about 4 pm (0.5 GHz) wavelength stability, 60 ms response; abstract reports BER measurement confirmation | [Grillanda2017, abstract] |
| Thermal-crosstalk coefficient | \(K_{ij}\) | Neighbor ring wavelength shift per driven-heater power | Layout/stack-specific | DeRose et al. report at approximately 10 μm device separation that passive-device shift was several percent of driven-device shift; >15 μm separation yielded passive temperature increase of only several percent in their simulated/experimental study | [DeRose2014, pp. 125–126] |
| Spectral quality factor | \(Q\) | Resonance frequency divided by linewidth | Device/coupling-specific | TiO₂–Si₃N₄ hybrid ring: \(Q=1.55\times10^5\), 0.4 dB/cm propagation loss, 0.14 pm/°C from 25–60°C; this is Si₃N₄/TiO₂ (not a Si-core CPO ring); numbers re-confirmed against the publisher abstract 2026-08-26 | [Qiu2015, abstract] |

> **Metric discipline:** Do not report \(dn_{eff}/dT\), pm/mW, GHz/mW, \(\tau_{th}\), ER, IL, or
> \(Q\) without reporting (i) waveguide cross section/ring radius, (ii) cladding and heater
> stack, (iii) target wavelength/polarization, (iv) temperature/ambient condition, and (v)
> whether power is electrical DC, AC amplitude, or dissipated heater power.

---

## 6. Common Assumption Pitfalls

| Pitfall | Trigger condition | How to recognize it | Correct approach | Source [Key] |
|---|---|---|---|---|
| "Use the silicon \(dn/dT\) only; cladding is negligible." | 「只要用 silicon 1.8e-4/K 算 ring drift」 | LC/TiO₂/polymer/slot geometry or narrow waveguide is present | Solve the actual mode and include \(\Gamma_i dn_i/dT\); validate with \(\lambda_{res}(T)\) | [Ptasinski2014; PadmarajuBergman2014] |
| "SiO₂ is a negative-TOC compensation layer." | 「石英包層可以用負 TOC 抵消矽」 | Claim supplies no material dispersion/source | In the reviewed SOI context SiO₂ is stated as \(+1\times10^{-5}\) K⁻¹, much smaller than Si, not negative; only call a layer negative-TOC with its measured source and wavelength | [PadmarajuBergman2014, §2] |
| "A passive athermal ring requires no thermal budget." | 「做了 TiO₂/LC 就不需要 heater 或 laser control」 | Fabrication offset, laser drift, finite residual TDWS or range is unreported | Budget residual drift, fabrication trim, LC/material operating range and laser stability; hybrid passive+trim heater is often the testable architecture | [PadmarajuBergman2014, §§2–5] |
| "Higher \(Q\) always improves thermal robustness." | 「Q 做高就能提升可靠性」 | Only \(Q\) is optimized without linewidth/detuning budget | Convert all temperature and crosstalk excursions to \(\Delta\lambda/\Delta\lambda_{FWHM}\); check ER/IL and control noise | [PadmarajuBergman2014, §2] |
| "Heater power per nm compares designs fairly." | 「這顆 ring 的 mW/nm 較低，所以 heater 更好」 | Ring radii / FSR differ | Report mW/FSR (mW/\(2\pi\)) in addition to pm/mW or GHz/mW | [PadmarajuBergman2014, §4.1] |
| "Thermal isolation has no dynamic penalty." | 「挖空 substrate 一定是最好」 | Static tuning efficiency only is reported | Measure \(\tau_{th}\), control stability, optical bistability and mechanical/process compatibility; review reports isolated devices with \(\tau_{th}\) up to ~170 μs | [PadmarajuBergman2014, §4.1] |
| "Independent heater calibration scales to a WDM bank." | 「每個 ring 各自 tune 到波長就好」 | Neighbor resonance shifts when one heater changes; metal routes differ | Identify full \(K_{ij}\), jointly solve/compensate, then revalidate under concurrent actuation | [DeRose2014] |
| "Locking the resonance has no ER cost." | 「只要 feedback lock，ER 不會受影響」 | Dither-based error generation or loss-changing actuator is used | Measure ER/IL/Q at locked state; for the cited Q≈14,000 ring, 0.1/0.2 K thermal dithers reduced ER 1.9/4.8 dB | [Padmaraju2013] |
| "A temperature sensor measures the optical mode temperature." | 「stage/IR 溫度就是 ring core 溫度」 | Sensor is distant or thermal boundary changes during operation | Calibrate local optical \(\lambda_{res}\) against sensor reading; use heater transfer dynamics and spatial thermal evidence | [Ptasinski2014; PadmarajuBergman2014] |
| "A fixed PM/°C number proves link BER compliance." | 「drift 小於某個 pm/°C 就一定 BER 合格」 | Modulation format, laser linewidth, channel plan, receiver and detuning curve are absent | Measure/model the actual ER/IL/eye/BER vs detuning and multi-ring actuation | [PadmarajuBergman2014, §§4.2–5] |

---

## Evidence Anchors

- Padmaraju, K.; Bergman, K. (2014). "Resolving the Thermal Challenges for Silicon Microring
  Resonator Devices." *Nanophotonics* 3(4–5), 269–281. DOI: 10.1515/nanoph-2013-0013. Canonical
  synthesis of resonance drift, negative-TOC claddings, MZI compensation, heater topologies,
  tuning-power normalization, and feedback-lock methods.
- Ptasinski, J.; Khoo, I.-C.; Fainman, Y. (2014). "Passive Temperature Stabilization of Silicon
  Photonic Devices Using Liquid Crystals." *Materials* 7(3), 2229–2241. DOI: 10.3390/ma7032229.
  Direct SOI-ring experiment measuring LC-cladding thermal-drift reduction, LC TOC inference,
  geometry/mode-overlap limits, and experimental setup — every quantitative claim used above was
  re-verified against the open full text 2026-08-26.
- Guha, B.; Cardenas, J.; Lipson, M. (2013). "Athermal Silicon Microring Resonators with
  Titanium Oxide Cladding." *Optics Express* 21(22), 26557–26563. DOI: 10.1364/OE.21.026557.
  Core TiO₂ athermal-ring reference; this branch has abstract-level access only — extract full
  geometry/loss/temperature data before setting a TiO₂ design rule.
- DeRose, C. T.; Martinez, N. J.; Kekatpure, R. D.; Zortman, W. A.; Starbuck, A. L.; Pomerene,
  A.; Lentine, A. L. (2014). "Thermal Crosstalk Limits for Silicon Photonic DWDM Interconnects."
  *2014 Optical Interconnects Conference*, 125–126. DOI: 10.1109/OIC.2014.6886111. Direct
  array-layout/thermal-path study establishing that distance and metal routing affect
  neighboring devices.
- Grillanda, S.; Ji, R.; Morichetti, F.; Carminati, M.; et al. (2017). "Wavelength Locking of
  Silicon Photonics Multiplexer for DML-Based WDM Transmitter." *Journal of Lightwave
  Technology* 35(4), 607–614. DOI: 10.1109/JLT.2016.2641163. Direct locking stability,
  response-time and BER-confirmed demonstration.

---

## Source Ledger

> **Provenance & correction log (added 2026-08-26, `domain-expansion-guide.md` §9 step 2).**
> This branch was compiled from a user-supplied AI-research-tool packet. Per the SKILL's
> standing intake stance, every key below was independently re-resolved against Crossref /
> publisher metadata before the file was registered. **5 of 8 keys (63%) carried at least one
> bibliographic-identity defect** — consistent with every prior AI-packet intake this SKILL has
> processed (`silicon_photonics_device_physics.md`'s own intake note; `domain-expansion-guide.md`
> §3.2's `v_groove_fabrication.md` incident). Dispositions:
> - **PadmarajuBergman2014** — ❌ **wrong DOI**. The packet's DOI (`10.1515/nanoph-2013-0020`)
>   resolves to an *unrelated* paper (Zhang, Agarwal, Kimerling & Michel, "Nonlinear Group IV
>   photonics based on silicon and germanium," same journal/volume/issue by coincidence). Title,
>   authors, venue, and pages were correct. Corrected DOI: `10.1515/nanoph-2013-0013` (confirmed
>   via Wiley Online Library page title/author match).
> - **Ptasinski2014** — ✅ fully correct as submitted; independently re-verified against the open
>   PMC full text, including six numeric claims (TDWS values, TOC values, Γ_clad, apparatus
>   specs) — all reproduce exactly.
> - **Guha2013** — ✅ correct as submitted (abstract-level check only).
> - **Dahlem2011** — ❌ **fabricated co-authors**. The packet listed "Tanguy, Quentin A." and
>   "Tennant, Aaron" as co-authors; neither appears in the actual author list (Crossref: Dahlem,
>   M. S.; Holzwarth, C. W.; Khilo, A.; Kärtner, F. X.; Smith, H. I.; Ippen, E. P.). The packet's
>   title ("Reconfigurable Multi-Channel Second-Order Silicon Photonic Filters") was also a
>   paraphrase, not the real title ("...silicon microring-resonator filterbanks for on-chip WDM
>   systems"). DOI, volume, and pages were correct.
> - **DeRose2014** — ✅ fully correct as submitted.
> - **Grillanda2017** — ❌ **wrong DOI, wrong volume/issue/pages, wrong title tail**. The
>   packet's DOI (`10.1109/JLT.2017.2701817`) does not resolve (404 at doi.org). Correct DOI:
>   `10.1109/JLT.2016.2641163`. The packet's volume/issue/pages ("35(16), 3274–3281") do not
>   match the real record (**35(4), 607–614**). Title tail "...DML-Based Transceivers" should
>   read "...DML-Based WDM Transmitter." The cited numeric claim (4 pm / 0.5 GHz stability, 60 ms
>   response) is correct and reproduces against the right paper's abstract — only the
>   bibliographic identity was wrong.
> - **Padmaraju2013** — ⚠ **wrong venue name, incomplete author list, incomplete title**. The
>   packet's venue "TechConnect Briefs, 2013" is a different, unrelated small-tech publisher; the
>   real venue is **SRC TechCon 2013** (Austin, TX; the paper won a Best-in-Session award there).
>   The packet listed only "Padmaraju, K.; Bergman, K." — the real author list has five names
>   (Padmaraju, K.; Logan, D. F.; Ackert, J. J.; Knights, A. P.; Bergman, K.). Title corrected to
>   "...for Next-Generation **Silicon Photonic** Interconnects" (packet dropped "Silicon
>   Photonic"). The Fig. 4 numeric claim (1.9/4.8 dB ER reduction) is corroborated by the paper's
>   scope and award record but was **not** independently re-extracted from the primary PDF this
>   pass (a tool-format limitation, not a source-access block) — left `~ Approximate`.
> - **Armani2015 → renamed Qiu2015** — ❌ **entirely wrong author attribution**. The packet
>   attributed this paper to "Armani, A. M.," who has no connection to it. The real authors are
>   Qiu, F.; Spring, A. M.; Miura, H.; Maeda, D.; Ozawa, M.; Odoi, K.; Yokoyama, S. (Kyushu
>   University group). DOI, journal, volume, pages, and every numeric claim (Q=1.55×10⁵, 0.4
>   dB/cm, 0.14 pm/°C 25–60°C) were correct — only the author identity was fabricated. The
>   profile's own original `⚠ Unconfirmed` flag on this row was the right call; this pass
>   resolves it.
>
> **Verified (date)** cells below record 2026-08-26, the date of this resolution pass
> (`domain-expansion-guide.md` §3.7). No versioned-source pinning applies — all eight sources are
> fixed-issue journal/conference publications, not standards or preprints.

| Key | Full citation | Identifier | Access tag | Verification status | Verified (date) | Locator | Used in (Node/row) |
|---|---|---|---|---|---|---|---|
| PadmarajuBergman2014 | Padmaraju, Kishore; Bergman, Keren. 2014. "Resolving the Thermal Challenges for Silicon Microring Resonator Devices." *Nanophotonics* 3(4–5): 269–281. | DOI: https://doi.org/10.1515/nanoph-2013-0013 ; author PDF: https://www.ee.columbia.edu/~kishore/publications/NP_2013.pdf | [full] | ✅ Confirmed — **DOI corrected 2026-08-26** (packet's `-0020` resolved to an unrelated paper; see Provenance log) | 2026-08-26 | §2, Eqs. (1)–(2); §3.1 Eq. (3); §§3.1–3.2; §4.1; §4.2; conclusion | §§1–6, Evidence Anchors |
| Ptasinski2014 | Ptasinski, Joanna; Khoo, Iam-Choon; Fainman, Yeshaiahu. 2014. "Passive Temperature Stabilization of Silicon Photonic Devices Using Liquid Crystals." *Materials* 7(3): 2229–2241. | DOI: https://doi.org/10.3390/ma7032229 ; URL: https://pmc.ncbi.nlm.nih.gov/articles/PMC5453267/ | [full] | ✅ Confirmed — identity via Crossref and six numeric claims re-read from the open full text, all exact | 2026-08-26 | Abstract; §1; §2.1 Tables 1–3; §2.2 Fig. 5; §3.1–3.2; §4 | §§1–6, Evidence Anchors |
| Guha2013 | Guha, Biswajeet; Cardenas, Jaime; Lipson, Michal. 2013. "Athermal Silicon Microring Resonators with Titanium Oxide Cladding." *Optics Express* 21(22): 26557–26563. | DOI: https://doi.org/10.1364/OE.21.026557 ; URL: https://opg.optica.org/oe/abstract.cfm?uri=oe-21-22-26557 | [abstract] | ✅ Metadata/abstract confirmed via Crossref 2026-08-26; ⚠ numeric detail not independently extracted (full text unread) | 2026-08-26 | Abstract only | §§3, Evidence Anchors |
| Dahlem2011 | Dahlem, Marcus S.; Holzwarth, Charles W.; Khilo, Anatol; Kärtner, Franz X.; Smith, Henry I.; Ippen, Erich P. 2011. "Reconfigurable multi-channel second-order silicon microring-resonator filterbanks for on-chip WDM systems." *Optics Express* 19(1): 306–316. | DOI: https://doi.org/10.1364/OE.19.000306 ; URL: https://opg.optica.org/fulltext.cfm?uri=oe-19-1-306 | [abstract] | ✅ Corrected 2026-08-26 — **author list and title corrected** (packet fabricated two co-authors and paraphrased the title; see Provenance log); DOI/volume/pages were already correct | 2026-08-26 | Abstract | §5 metric row |
| DeRose2014 | DeRose, Christopher T.; Martinez, Nicholas J.; Kekatpure, Rohan D.; Zortman, William A.; Starbuck, Andrew L.; Pomerene, Andrew; Lentine, Anthony L. 2014. "Thermal Crosstalk Limits for Silicon Photonic DWDM Interconnects." In *2014 Optical Interconnects Conference (OIC)*, 125–126. | DOI: https://doi.org/10.1109/OIC.2014.6886111 ; full PDF: https://www.osti.gov/servlets/purl/1140533 | [full] | ✅ Confirmed via Crossref 2026-08-26 (identity only — the OSTI full-text PDF could not be re-fetched this pass, connection refused; the 10 μm / 15 μm crosstalk figures stand as previously recorded, not re-derived this pass) | 2026-08-26 | pp. 125–126; simulation/measurement discussion | §§1–6, Evidence Anchors |
| Grillanda2017 | Grillanda, Stefano; Ji, Ruiqiang; Morichetti, Francesco; Carminati, Marco; Ferrari, Giorgio; Guglielmi, Emanuele; Peserico, Nicola; Annoni, Andrea; Dedè, Alberto; Nicolato, Danilo; Vannucci, Antonello; Klitis, Charalambos; Holmes, Barry; Sorel, Marc; Fu, Shengmeng; Man, Jiangwei; Zeng, Li; Sampietro, Marco; Melloni, Andrea. 2017. "Wavelength Locking of Silicon Photonics Multiplexer for DML-Based WDM Transmitter." *Journal of Lightwave Technology* 35(4): 607–614. | DOI: https://doi.org/10.1109/JLT.2016.2641163 ; repository PDF: https://re.public.polimi.it/bitstream/11311/1037077/2/11311-1037077_Sampietro.pdf | [abstract] | ✅ Corrected 2026-08-26 — **DOI, volume/issue/pages, title tail, and full author list corrected** (packet's DOI 404s; see Provenance log). The 4 pm/0.5 GHz/60 ms claim reproduces against the corrected paper's abstract | 2026-08-26 | Abstract only | §§3, 5, Evidence Anchors |
| Padmaraju2013 | Padmaraju, Kishore; Logan, David F.; Ackert, Jonathan J.; Knights, Andrew P.; Bergman, Keren. 2013. "Initialization and Stabilization of Microring Resonators for Next-Generation Silicon Photonic Interconnects." *SRC TechCon 2013* (Austin, TX). Best-in-Session award. | URL: http://www.ee.columbia.edu/~kishore/publications/TECHCON_2013.pdf | [partial] | ⚠ Corrected 2026-08-26 — **venue name, author list, and title corrected** (packet named a different, unrelated publisher and dropped 3 of 5 authors; see Provenance log). Fig. 4 numeric values (1.9/4.8 dB) corroborated by scope/award record but not re-extracted from the primary PDF this pass (tool could not parse the PDF text) — `review-when:` a future pass can parse the PDF or find an open HTML mirror | 2026-08-26 | Fig. 4 discussion; dither paragraph | §§4, 6 |
| Qiu2015 | Qiu, Feng; Spring, Andrew M.; Miura, Hiroki; Maeda, Daisuke; Ozawa, Masa-aki; Odoi, Keisuke; Yokoyama, Shiyoshi. 2015. "Athermal and High-Q Hybrid TiO₂–Si₃N₄ Ring Resonator via an Etching-Free Fabrication Technique." *ACS Photonics* 2(3): 405–409. | DOI: https://doi.org/10.1021/ph500450n | [abstract] | ✅ Corrected 2026-08-26 — **renamed from the packet's fabricated "Armani2015"; full author list restored** (see Provenance log). Q, loss, and TDWS numbers all reproduce against the publisher abstract | 2026-08-26 | Abstract snippet | §5 metric row only, explicitly Si₃N₄/TiO₂ context |

---

## Cross-Domain Links

### Closest Related Domain Profiles

| Profile name | Overlap dimensions | Typical use split |
|---|---|---|
| `silicon_photonics_device_physics.md` (parent) | material TOC; carrier electro-optics; resonator physics; link-budget accounting | Use the parent for bulk Si \(dn/dT\), plasma-dispersion modulation, and generic optical mode physics; use this branch for ring-specific thermal control, locking and WDM crosstalk. |
| `siph_packaging_reliability.md` | thermal field; package reliability; CPO context | Use the package profile to calculate ASIC/package boundary temperature fields; use this branch to translate local ring temperatures and heater operation into resonance and link metrics. |
| `adhesives_polymer_reliability.md` | polymer/LC claddings; moisture/thermal ageing | Use the adhesive/polymer profile for material ageing, absorption, chemical stability and cure; use this branch for optical modal overlap and thermal-resonance consequences. |

### Cross-Domain Conflict Notes

| Issue / constraint | Other profile(s) involved | Potential conflict | AI confirmation question |
|---|---|---|---|
| Passive LC/polymer athermal cladding | `adhesives_polymer_reliability.md`, `siph_packaging_reliability.md` | A large negative TOC may reduce drift but introduce LC alignment, phase-transition, moisture/sealing or high-temperature integration constraints outside ring-only analysis | "What are the required operating/storage temperature and humidity ranges, and is the cladding allowed to be a sealed non-CMOS material?" |
| Heater thermal isolation | `siph_packaging_reliability.md` | An undercut may minimize mW/FSR yet increase \(\tau_{th}\), hotspot sensitivity and mechanical/process complexity | "Is your dominant requirement minimum static power, fastest lock response, or compatibility with a fixed foundry/package flow?" |
| Ring detuning versus link failure | `silicon_photonics_device_physics.md` (parent); a system/link model | A spectral pm tolerance cannot be assigned without modulation format, linewidth, data rate, receiver and WDM plan | "What modulation format/data rate, laser linewidth, channel spacing and allowed IL/ER/BER penalty define success?" |
