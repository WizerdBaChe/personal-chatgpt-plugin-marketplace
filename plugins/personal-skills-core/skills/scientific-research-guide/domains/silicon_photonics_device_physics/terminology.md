---
xi: 1
what: "Reference: Silicon Photonics Active-Device Terminology (English ↔ 中文對照與命名陷阱) — English↔中文 term map for SiPh active devices + naming traps where the Chinese rendering itself causes a physics error"
tags: [srg-domain, 領域框架, reference]
aliases: ["中文術語", "翻譯", "terminology", "電光 vs 電漿色散", "線寬 (linewidth vs CD)", "異質整合 vs 混合整合", "消光比 vs 偏振消光比", "量子效率", "T₀ vs T₀*", "響應度 vs 靈敏度"]
date: 2026-09-02
status: live
profile_type: reference
parent: "silicon_photonics_device_physics"
---
# Reference: Silicon Photonics Active-Device Terminology (English ↔ 中文對照與命名陷阱)

> Parent domain: `silicon_photonics_device_physics.md`
> Type: reference; load only for terminology, naming, or English↔Chinese rendering questions.
> Role: give one agreed rendering per term and record where a *Chinese* rendering itself
> causes a physics error. No standing triggers — the traps that must fire automatically live
> in the parent profile's Node 6.

Why this file is bilingual while the rest of the domain layer is English: the term map is the
one place where the Chinese wording is the payload, not the presentation. Several of the
collisions in §2 exist *only* in Chinese (「線寬」, 「電光」, 「異質/混合整合」) and are invisible in an
English-only glossary. The explanatory text stays English so this file reads the same way as
its sibling reference notes.

---

## 1. Term map

### 1.1 Material and optical-response terms

| English term | 中文 | Meaning in this domain | Do not infer |
|---|---|---|---|
| Active photonic device | 主動光子元件 | A device whose optical behaviour is changed by electrical injection, bias, gain, or external control. | "Contains metal contacts" does not make a device active; a heated passive filter is a tuned passive, not an active device. |
| Optical gain | 光學增益 | Amplification from stimulated emission that can exceed optical loss. | Do not use bare 「增益」 without saying whether it is *material* gain g or *modal* gain Γg — only Γg competes with cavity loss at threshold. |
| Optical absorption | 光吸收 | Photon energy taken up by the material, exciting carriers or heat. | Absorption is not automatically useful signal; free-carrier absorption produces heat, not photocurrent. |
| Direct bandgap | 直接能隙 | Conduction-band minimum and valence-band maximum at the same crystal momentum; efficient radiative recombination. | A direct gap enables efficient emission; it does not by itself guarantee lasing (threshold still needs Γg ≥ α_i + α_m). |
| Indirect bandgap | 間接能隙 | Recombination generally requires phonon assistance for momentum conservation; poor emission efficiency. | Indirect ≠ "cannot emit at all" — it means no *practical telecom* gain medium. |
| Carrier | 載子 | Electron or hole carrying charge in a semiconductor. | — |
| Carrier concentration | 載子濃度 | Number of electrons or holes per unit volume; sets the electrical and optical constants. | Injected (excess) carrier density is not the same quantity as doping concentration — state which. |
| Refractive index | 折射率 | Sets phase velocity, mode profile and resonance condition. | Distinguish material index n, effective index n_eff, and group index n_g — resonance shifts and delay use different ones. |
| Absorption coefficient | 吸收係數 | Power-absorption rate, usually cm⁻¹. | Bulk material α is not the modal α_eff that a waveguide-integrated absorber actually sees. |
| Plasma-dispersion effect | 電漿色散效應／自由載子色散效應（陸：等離子體色散） | Free-carrier density change alters both refractive index and absorption coefficient. | The "plasma" here is a solid-state free-carrier plasma; it has no relation to gas-discharge 電漿. **It is not an electro-optic effect** — see §2.1. |
| Free-carrier absorption (FCA) | 自由載子吸收 | Loss from free carriers absorbing light; the inseparable companion of plasma-dispersion phase shift. | FCA is not a fabrication defect to be engineered away — it is the physics-mandated cost of the index change. |

### 1.2 Modulation mechanisms

| English term | 中文 | Meaning in this domain | Do not infer |
|---|---|---|---|
| Electro-absorption (EA) | 電吸收 | Applied field changes the absorption edge or coefficient, modulating intensity directly. | EA and EO are different mechanisms; an EA device modulates \|E\|, an EO device modulates phase. |
| Electro-optic (EO) effect | 電光效應 | Field-induced *refractive-index* change — Pockels (χ⁽²⁾) or Kerr (χ⁽³⁾). | Reserve this term strictly; see §2.1 for the most common misuse in Chinese writing. |
| Pockels effect | 普克爾效應／線性電光效應 | χ⁽²⁾ index change linear in applied field; requires a non-centrosymmetric crystal. | Crystalline Si is centrosymmetric — a "silicon Pockels modulator" implies a heterogeneous material or strain-induced symmetry breaking. |
| Franz–Keldysh effect | 法蘭茲–凱爾迪什效應 | Field-induced broadening/shift of the bulk absorption edge. | A bulk-material effect — do not use it to describe a quantum-well device's response. |
| Quantum-confined Stark effect (QCSE) | 量子侷限史塔克效應 | Field shifts quantum-well levels and the excitonic absorption peak. | A quantum-well effect — do not use it for a bulk Ge or SiGe absorber. |
| Carrier injection | 載子注入 | Forward-biased junction floods the waveguide with carriers. | High phase efficiency, but speed is limited by carrier lifetime and both FCA and heating rise. |
| Carrier depletion | 載子耗盡 | Reverse bias moves the depletion boundary through the optical mode. | The mainstream high-speed, CMOS-driver-compatible route; the cost appears as the V_πL/insertion-loss trade. |
| Carrier accumulation | 載子累積 | A MOS capacitor accumulates carriers at an oxide interface. | Potentially low-energy, but carries oxide reliability, process-integration and variability risk. |

### 1.3 Device structures

| English term | 中文 | Meaning in this domain | Do not infer |
|---|---|---|---|
| Mach–Zehnder interferometer (MZI) | 馬赫–曾德干涉儀 | Two arms; phase difference becomes output intensity. Broadband, wavelength-tolerant, larger footprint. | Its wavelength robustness does not make it drift-free — arm imbalance and thermal gradients still require bias control. |
| Micro-ring resonator (MRR) | 微環共振器（陸：微環諧振器） | Closed-loop waveguide resonance; compact, low capacitance, WDM-friendly. | Small footprint does not mean low system power once wavelength locking and thermal tuning are counted. |
| Resonance wavelength | 共振波長（陸：諧振波長） | Wavelength satisfying m·λ_res = n_eff·L_ring. | A temperature-dependent quantity, not a device constant. |
| Heterogeneous integration | 異質整合 | Different material systems combined — e.g. III–V bonded at wafer/die level onto Si so the optical mode spans both materials. | See §2.3 — this is *not* interchangeable with 混合整合. |
| Hybrid laser | 混合式雷射 | Separately fabricated III–V gain chip assembled to a Si PIC by packaging/proximity coupling. | Uses known-good die, but needs active alignment and carries its own thermal-path and rework problems. |
| External laser source (ELS) | 外接雷射源 | Laser sits away from the PIC; light arrives by fiber. | Thermally isolated, but adds fiber routing, an extra coupling interface, and back-reflection management. |

### 1.4 Metrics

| English term | 中文 | Meaning in this domain | Do not infer |
|---|---|---|---|
| Extinction ratio (ER) | 消光比 | 10·log₁₀(P_on/P_off) for a modulated signal. | Collides with *polarization* extinction ratio (PER) in fiber components — see §2.4. |
| V_πL | 半波電壓—長度積 | Voltage × phase-shifter length for a π phase shift; lower ⇒ higher phase efficiency. | Not a standalone figure of merit — always pair with insertion loss, bias point, drive configuration and λ. |
| Responsivity R | 響應度 | Photocurrent per unit incident optical power (A/W). | Distinct from 靈敏度 — see §2.5. Capped at qλ/hc (≈1.25 A/W at 1550 nm) without internal gain. |
| Quantum efficiency η | 量子效率 | Photons/carriers converted per incident photon (detector) or per injected carrier (emitter). | Ambiguous alone — see §2.6 for the internal/external/differential split. |
| Dark current | 暗電流 | Reverse-bias current with no illumination. | Not merely a DC power number: it sets a shot-noise floor and therefore receiver sensitivity. |
| Avalanche multiplication | 雪崩倍增 | Impact-ionization current gain M under strong field. | Gain is never free — excess noise F(M) and the gain–bandwidth product bound the useful M. |
| Relative intensity noise (RIN) | 相對強度雜訊 | Laser output-power fluctuation relative to the mean. | Strongly degraded by uncontrolled optical feedback — a packaging problem that appears as a laser metric. |
| Linewidth | 線寬（雷射譜線寬度） | Laser spectral width; tied to phase noise and coherence. | Collides with lithographic 線寬 (critical dimension) — see §2.2. |
| Threshold current I_th | 閾值電流（陸：閾值電流／臨界電流） | Current at which modal gain equals total loss. | A junction-temperature quantity; meaningless without the stated temperature and CW/pulsed mode. |
| Slope efficiency | 斜率效率 | dP_out/dI above threshold. | Must be extracted from the linear region only, not through thermal roll-over. |
| Differential gain | 微分增益 | dg/dN — gain change per unit carrier density. | Governs modulation speed and threshold behaviour; not the same as the gain value g itself. |
| Characteristic temperature T₀* | 特徵溫度 | Exponential sensitivity of I_th to temperature. | Written **T₀\*** throughout this domain to avoid the reference-temperature collision — see §2.7. |

---

## 2. Naming traps (the reason this file exists)

### 2.1 「電光」 over-extension — the highest-frequency error

In Chinese writing, 「矽電光調變器」 is routinely used for any electrically driven silicon
modulator, including plain PN-junction depletion devices. This is wrong at the mechanism level:
those devices work by **free-carrier plasma dispersion**, which changes the complex index via
carrier *density*, not by a field-induced index change. Silicon is centrosymmetric and has no
usable native Pockels effect. Consequences of the sloppy label: it implies a linear,
low-loss, essentially lossless phase shift, and it hides the mandatory FCA/insertion-loss cost.
Correct renderings: 「載子色散型矽調變器」 or 「自由載子電漿色散調變器」. Reserve 「電光」 for genuine
χ⁽²⁾/χ⁽³⁾ materials — thin-film LiNbO₃, BaTiO₃, EO polymer.

### 2.2 「線寬」 collides with lithographic critical dimension

In a silicon-photonics conversation both meanings are live at once: laser spectral linewidth
(Hz or MHz) and lithographic linewidth / critical dimension (nm). A sentence like 「線寬控制不好」
is genuinely ambiguous between "the laser is noisy" and "the fab's CD uniformity is poor".
Disambiguate on first use: 「譜線寬度 (spectral linewidth)」 vs 「線寬/關鍵尺寸 (CD, critical dimension)」.

### 2.3 「異質整合」 vs 「混合整合」 are not synonyms

Both are often rendered loosely as "integration of III–V with Si", but they name different
processes with different failure modes:

| | 異質整合 (heterogeneous integration) | 混合整合 (hybrid integration) |
|---|---|---|
| What happens | III–V epitaxial layers bonded at wafer/die level; the optical mode spans both materials | Separately fabricated III–V die assembled to the Si PIC by packaging |
| Scaling | Wafer-scale parallel | Serial, per-die assembly |
| Dominant risks | Bond voids/defects, thermal expansion mismatch, process complexity | Active alignment cost, die-attach thermal resistance, rework |
| Known-good die | Not available before bonding | Available |

Collapsing the two makes a yield or reliability argument meaningless. When a source is
ambiguous, ask which one is meant before comparing numbers.

### 2.4 「消光比」 — modulation ER vs polarization ER

The same two characters serve modulation extinction ratio (on/off power ratio of a data signal)
and polarization extinction ratio (PER, the polarization purity of a fiber or component, also in
dB). In a packaging discussion involving polarization-maintaining fiber, both appear. Write
「調變消光比 (modulation ER)」 vs 「偏振消光比 (PER)」.

### 2.5 「響應度」 vs 「靈敏度」

Responsivity (響應度, A/W) is a device property: photocurrent per unit optical power. Receiver
sensitivity (靈敏度, dBm) is a system property: the minimum received power for a target BER, and
it depends on the TIA noise, the dark-current shot noise and the modulation format as well as on
R. Improving R does not improve sensitivity by the same factor. Never substitute one for the other.

### 2.6 「量子效率」 needs a qualifier

At least three distinct quantities share the Chinese term: internal quantum efficiency (內部量子
效率, η_i), external quantum efficiency (外部量子效率, η_ext — the one that enters R = η_ext·qλ/hc),
and differential quantum efficiency (微分量子效率, η_d — the one that enters the above-threshold
laser slope). Always attach the qualifier.

### 2.7 T₀ symbol collision

The standard threshold model I_th(T) = I_th(T₀)·exp[(T − T₀)/T₀] uses T₀ for both the *reference*
temperature and the *characteristic* temperature. This domain writes the characteristic
temperature as **T₀\*** throughout. When reading external sources, resolve which one a quoted T₀
means before comparing lasers — and check the fitted temperature range, since the exponential
form typically degrades at high temperature.

### 2.8 Regional variants worth recognizing but not adopting

The parent profile and this domain use Taiwan-standard renderings. Recognize the mainland
variants when reading sources, but do not mix them inside one document: 電漿 / 等離子體 (plasma),
共振 / 諧振 (resonance), 光偵測器 / 光電探測器 (photodetector), 雷射 / 激光 (laser),
半導體雷射 / 半導體激光器. These are pure orthography, not physics — a term-map mismatch is not a
finding, but a *silent* mid-document switch makes a source hard to audit.
