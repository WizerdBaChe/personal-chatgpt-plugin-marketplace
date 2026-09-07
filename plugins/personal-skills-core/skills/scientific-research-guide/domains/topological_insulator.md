---
xi: 1
what: "Topological Insulator (拓撲絕緣體, topological insulator, TI) — Topological-insulator domain profile"
tags: [srg-domain, 領域框架, base]
aliases: ["topological insulator", "TI", "Z₂", "Bi2Se3", "quantum spin Hall", "Dirac surface state", "QAHE", "Majorana"]
date: 2026-08-26
status: live
profile_type: base
parent: "-"
---
# Domain Profile: Topological Insulator (拓撲絕緣體, topological insulator, TI)

> Scope of applicability:
> - Bulk-gapped, edge/surface-conducting quantum materials described as topological insulators(拓撲絕緣體, topological insulator, TI).
> - Includes both 2D quantum spin Hall insulators(量子自旋霍爾絕緣體, quantum spin Hall insulator) and 3D topological insulators(三維拓撲絕緣體, three-dimensional topological insulator, 3D TI).[HasanKane2010][QiZhang2011]
>
> Scientific nature:
> - Band topology (能帶拓撲, band topology) of time-reversal-symmetric(時間反轉對稱, time-reversal symmetry, TRS) electronic systems classified by Z₂ topological invariants(Z₂ 拓撲不變量, Z₂ topological invariants).[FuKaneMele2007]
> - Bulk–boundary correspondence(體積–邊界對應, bulk–boundary correspondence) guaranteeing protected gapless boundary states.[HasanKane2010][Ando2013_PedagogicalReview]
>
> Engineering nature:
> - Materials and heterostructures providing robust spin-polarized surface or edge channels for transport, spintronics, quantum metrology, and proximity-induced phases (e.g. quantum anomalous Hall effect(量子反常霍爾效應, quantum anomalous Hall effect, QAHE), Majorana zero modes(馬約拉納零能模, Majorana zero modes)).[QiZhang2011][GrapheneTI_ProximitySOC_PRB2023]
>
> Profile metadata:
> - Profile ID: TI.domain.v1
> - Profile version: 1.0 (2026-08-24: full Source Ledger completed, Nodes 3-8 authored — structurally complete, matching the other three base profiles; two [~ Approximate] ledger entries remain representative-rather-than-exact sources, see Node 7b)
> - Last updated: 2026-08-26 (§3.7 currency pass: 14/16 ledger rows re-resolved, 3 published DOIs added, 3 "representative paper" hedges dropped, 3 arXiv version pins left open)
> - Author(s) / Maintainer(s): Perplexity (research assistant profile)
>
> Primary source types:
> - Textbooks:
>   - Lecture notes and introductory materials on topological insulators and superconductors (e.g. Qi & Zhang 2011, Bernevig course notes).[QiZhang2011][BernevigHughes2013_Textbook]
> - Review articles:
>   - Hasan & Kane, “Colloquium: Topological insulators” (Rev. Mod. Phys. 2010).[HasanKane2010]
>   - Qi & Zhang, “Topological insulators and superconductors” (Rev. Mod. Phys. 2011).[QiZhang2011]
>   - Pedagogical review “Topological insulator materials”.[Ando2013_PedagogicalReview]
> - Methods / standards papers:
>   - First-principles predictions of Bi₂Se₃/Bi₂Te₃/Sb₂Te₃ topological phases.[Zhang2009_SingleDiracCone]
>   - Magnetotransport WAL/WL studies using Hikami–Larkin–Nagaoka equation(希神–拉金–納卡奧方程, Hikami–Larkin–Nagaoka equation, HLN equation).[HLN1980][Adroguer2015][Wang2014_WAL_WL_Crossover]
> - Other (e.g. datasheets, industry standards):
>   - Materials-chemistry studies of Bi₂Se₃/Bi₂Te₃ surface reactivity and acceptable preparation/handling conditions.[Bi2Se3_SurfaceOxidation_JVSTA2016]
>
> Notes for AI use:
> - Intended use:
>   - Provide first-principles and materials-level reasoning for queries about topological insulators(拓撲絕緣體), their classification, transport signatures, and heterostructure effects before jumping to device-level optimization.
> - Validation status / usage note:
>   - This profile is anchored to canonical RMP reviews and established materials papers; when user queries touch speculative TI candidates or non-electronic “topological” systems, the AI should explicitly flag evidence levels and stay within this profile’s validated scope.[HasanKane2010][QiZhang2011][Ando2013_PedagogicalReview]

---

## 1. Theoretical Framework Anchoring

### Core first principles

| Scale / problem type | Foundational theory | Core physical quantity |
|----------------------|---------------------|------------------------|
| Bulk band classification of insulators | Band theory + Z₂ topological invariant(Z₂ 拓撲不變量, Z₂ topological invariant) for TRS systems | Z₂ indices \((\nu_0;\nu_1,\nu_2,\nu_3)\) distinguishing trivial vs strong/weak TI phases.[FuKaneMele2007] |
| Boundary state existence and robustness | Bulk–boundary correspondence(體積–邊界對應, bulk–boundary correspondence) | Topologically protected gapless edge/surface modes and their symmetry protection.[HasanKane2010][Ando2013_PedagogicalReview] |
| 2D TI / quantum spin Hall physics | Quantum spin Hall theory(量子自旋霍爾理論, quantum spin Hall theory) for 2D TRS systems | Helical edge states(螺旋邊界態, helical edge states) and spin-resolved edge conductance.[HasanKane2010][BernevigHughesZhang2006] |
| 3D TI surface states | Effective Dirac Hamiltonian(Dirac 哈密頓量, effective Dirac Hamiltonian) for TI surfaces | Dirac cone(狄拉克錐, Dirac cone) dispersion, spin–momentum locking(自旋–動量鎖定, spin–momentum locking), Berry phase(貝里相位, Berry phase).[HasanKane2010][Xia2009_LargeGap] |
| Disorder and quantum corrections | Quantum interference theory for weak localization(弱局域化, weak localization, WL) and weak antilocalization(弱反局域化, weak antilocalization, WAL) | Phase coherence length(相干長度, phase coherence length), magnetoconductivity corrections, HLN equation parameters.[HLN1980][Adroguer2015][Wang2014_WAL_WL_Crossover] |
| Symmetry-breaking and proximity-induced phases | TRS breaking and superconducting proximity in TI | Surface gaps, quantum anomalous Hall effect(量子反常霍爾效應, QAHE), Majorana zero modes(馬約拉納零能模, Majorana zero modes).[QiZhang2011] |

### Inviolable physical constraints (the AI should warn the user here)

1. TI boundary states require a non-trivial bulk topology with appropriate protecting symmetries (typically TRS); boundary states cannot be arbitrarily added by “engineering” without changing bulk band topology.[HasanKane2010][QiZhang2011]
2. Z₂ classification applies only to band insulators with TRS; using Z₂ indices outside their applicability (e.g. strongly interacting, symmetry-broken systems) is physically invalid.[FuKaneMele2007]
3. In realistic Bi₂Se₃/Bi₂Te₃ samples, bulk conduction can be substantial; assuming “perfectly insulating bulk” for transport interpretation without checking carrier densities and defect chemistry is unsafe.[BiSe_BulkConduction_General][Bi2Se3_SurfaceOxidation_JVSTA2016]
4. WAL/WL analysis using HLN equation assumes quasi-2D transport, diffusive regime, and specific disorder/SOC regimes; blindly fitting 3D or strongly inhomogeneous systems to HLN without checking dimensionality, dephasing mechanisms, and multi-channel contributions leads to false conclusions.[HLN1980][Adroguer2015][Wang2014_WAL_WL_Crossover]
5. TI surface-state robustness applies to non-magnetic disorder; magnetic impurities or magnetic proximity can break TRS and open gaps, invalidating simple “protected transport” assumptions and requiring QAHE/topological magnetism frameworks instead.[HasanKane2010][QiZhang2011][HLN1980][Adroguer2015][Wang2014_WAL_WL_Crossover][Chang2013_QAHE]

> **Decision point (mandatory Tier 0 confirmation)**: when the user describes a “topological insulator device or experiment”,
> the AI must confirm:
> “Is your goal (A) to understand/classify the bulk band topology, (B) to interpret edge/surface transport signatures (e.g. WAL, ARPES), or (C) to design/assess a heterostructure or proximity-induced phase?”
> The three goals correspond to entirely different measurement, modeling, and analysis paths:
> - (A): focus on band-structure calculations, Z₂ indices, and canonical TI vs trivial materials.[FuKaneMele2007][Zhang2009_SingleDiracCone]
> - (B): focus on transport, magnetotransport, ARPES, and surface vs bulk conduction separation, including WAL/WL and multi-channel analysis.[HasanKane2010][HLN1980][Adroguer2015][Wang2014_WAL_WL_Crossover]
> - (C): focus on interface quality, materials matching, and proximity-effect theory (graphene/TI, magnetic/TI, superconducting/TI).[GrapheneTI_ProximitySOC_PRB2023][QiZhang2011][Bi2Se3_SurfaceOxidation_JVSTA2016]

---

## 2. Measurement Tool Inventory

### Electronic structure and boundary-state spectroscopy

| Measurement target | Tool | Output information | Applicable conditions | Common misuse | Source [Key] |
|--------------------|------|--------------------|-----------------------|---------------|---------------|
| Bulk band topology and surface Dirac cones | ARPES (angle-resolved photoemission spectroscopy, 角解析光電子能譜) | Direct band dispersion, Dirac cone presence, band inversion at Γ, surface vs bulk bands.[HasanKane2010][Zhang2009_SingleDiracCone][Xia2009_LargeGap] | High-quality single crystals or epitaxial films with clean surfaces; ultrahigh vacuum (UHV); controlled cleaving or *in situ* preparation; sufficient energy and momentum resolution.[Bi2Se3_SurfaceOxidation_JVSTA2016] | Interpreting every linear-looking feature as a TI Dirac cone without checking surface sensitivity, bulk gap, or spin texture.[HasanKane2010][Xia2009_LargeGap] | HasanKane2010, Zhang2009_SingleDiracCone; web:56/63 unresolved (see Node 7b) |
| Surface-state spin texture | Spin-resolved ARPES (自旋解析 ARPES) | Spin–momentum locking patterns, spin polarization of surface states.[HasanKane2010][Xia2009_LargeGap] | Same as ARPES plus spin detection capabilities, often lower count rates and stricter surface quality requirements.[Xia2009_LargeGap] | Assuming spin–momentum locking from band shape alone, without actual spin-resolved measurement. | HasanKane2010; web:68 ~ approximate (see Node 7b) |
| Band gap magnitude and band inversion | Optical spectroscopy, STM/STS | Bulk band gap size, local density of states near Dirac point.[QiZhang2011][BernevigHughes2013_Textbook] | Clean surfaces; well-characterized doping level; low temperatures for STS; careful distinction between surface and bulk features. | Treating local STS spectra as representative of entire bulk without regard to spatial inhomogeneity or defects. | QiZhang2011; web:51 unresolved (see Node 7b) |

### Transport and magnetotransport

| Measurement target | Tool | Output information | Applicable conditions | Common misuse | Source [Key] |
|--------------------|------|--------------------|-----------------------|---------------|---------------|
| Quantum corrections (WL/WAL) to conductivity | Low-temperature magnetotransport (四端或霍爾量測) | Magnetoconductivity curves, WAL/WL signatures, coherence length from HLN fits.[HLN1980][Adroguer2015][Wang2014_WAL_WL_Crossover] | Thin films or quasi-2D samples; temperatures low enough for phase coherence; diffusive transport regime; magnetic fields covering the WL/WAL regime but below strong quantum limit.[HLN1980][Adroguer2015][Wang2014_WAL_WL_Crossover][general-method] | Fitting HLN blindly to any magnetoresistance data (including 3D or ballistic regimes) without verifying dimensionality, SOC regime, dephasing mechanism, or multi-channel transport (bulk + surface).[HLN1980][Adroguer2015][Wang2014_WAL_WL_Crossover] | HLN1980, Adroguer2015, Wang2014_WAL_WL_Crossover; web:60 unresolved (see Node 7b) |
| Surface vs bulk conduction contributions | Temperature-dependent resistivity and Hall measurements | Carrier densities, mobilities, activation behaviour vs metallic conduction; separating bulk and surface dominance.[BiSe_BulkConduction_General] | Wide temperature range; careful geometry; possibly gate-tuning or thickness variation to modulate surface carriers vs bulk; complementary spectroscopy if available. | Assuming “surface-only” conduction in Bi₂Se₃ family without measuring carrier density, thickness dependence, or performing gating/geometry analysis.[BiSe_BulkConduction_General][Bi2Se3_SurfaceOxidation_JVSTA2016] | web:17/65 ~ approximate (general Se-vacancy bulk-conduction finding, see Node 7b); web:56 unresolved |
| Quantum anomalous Hall plateau | Low-temperature Hall measurements in magnetically doped TI films | Quantized Hall resistance, vanishing longitudinal resistance, evidence for QAHE.[QiZhang2011][BernevigHughes2013_Textbook] | Very low temperatures; carefully controlled magnetic doping or proximity; thin-film geometry; stable magnetization orientation. | Interpreting any anomalous Hall signal as QAHE without quantization, clear plateau behaviour, or TI surface origin. | QiZhang2011, Chang2013_QAHE; web:58 unresolved (see Node 7b) |

### Interface and proximity characterization

| Measurement target | Tool | Output information | Applicable conditions | Common misuse | Source [Key] |
|--------------------|------|--------------------|-----------------------|---------------|---------------|
| Graphene/TI proximity-induced SOC | ARPES, transport, spintronic measurements on graphene/TI stacks | SOC-induced band gaps in graphene, spin Hall signals, modified band structures.[GrapheneTI_ProximitySOC_PRB2023] | High-quality heterostructures with atomically clean interfaces; controlled graphene thickness and TI layer thickness; minimal contamination between layers.[GrapheneTI_ProximitySOC_PRB2023][Bi2Se3_SurfaceOxidation_JVSTA2016] | Attributing all changes in graphene transport to TI proximity without ruling out disorder, substrate effects, or charge transfer. | web:35/56 unresolved (see Node 7b) |
| Magnetic/TI interfaces and surface gaps | ARPES, magnetotransport, Kerr microscopy | Surface gap opening, magnetization orientation, QAHE signatures.[QiZhang2011][BernevigHughes2013_Textbook][Chang2013_QAHE] | Magnetic order well defined; TI film thickness tuned; low temperatures; control of light source and measurement geometry (gap signatures can depend on probe).[Chang2013_QAHE] | Assuming TRS is intact when magnetic signatures are clearly present; misusing TI “protected surface” language in magnetically ordered systems. | QiZhang2011, Chang2013_QAHE; web:58 unresolved |
| Superconducting/TI Majorana candidates | Tunneling spectroscopy, Josephson measurements | Zero-bias peaks, 4π-periodic Josephson signals indicative of Majorana modes.[QiZhang2011] | High-quality TI–superconductor interfaces; phase-coherent Josephson junctions; low-noise spectroscopy; control of trivial Andreev bound states. | Claiming Majorana modes from any zero-bias anomaly without systematic checks against trivial bound states, inhomogeneity, or measurement artifacts. | QiZhang2011 |

---

## 3. Standard Modeling Toolchain

```
First-principles / band-topology scale
→ Output: band structure, parity eigenvalues at TRIM points, Z₂ invariants, bulk gap size
    ↓
Effective k·p / tight-binding surface-state modeling
→ Input: DFT band parameters near the relevant TRIM point, symmetry constraints
→ Output: Dirac Hamiltonian parameters (velocity, mass term), surface-state dispersion, spin texture
    ↓
Transport / magnetotransport modeling (HLN, multi-channel conductivity)
→ Input: measured magnetoconductance, Hall data, channel assumptions
→ Output: phase-coherence length, channel decomposition (bulk/surface/2DEG), WAL/WL coefficients
    ↓
Device / heterostructure-scale modeling (proximity, QAHE, Majorana)
→ Input: interface geometry, magnetic or superconducting order parameters
→ Output: induced gaps, predicted quantized responses, junction behavior
```

### Toolchain interpretation rules

- Start with DFT/first-principles for material-identity questions ("is this compound topologically non-trivial").
- Use k·p/tight-binding for quantitative surface-state predictions once bulk topology is already established — not as a substitute for establishing it.
- Use transport modeling (HLN, multi-channel fits) only after Node 2 methods have established which channels (bulk/surface/2DEG) are plausible for the sample; see `topological_insulator/wal_hln_transport.md` for the full HLN toolchain.
- Device-scale modeling (QAHE, Majorana) requires validated material and interface characterization as an *input*, not as a starting assumption — a simulated prediction is not evidence that the effect has been realized in a given sample.

---

## 4. Domain-Specific Fitting Methods

| Method | Applicable conditions | Common error | Correct approach | Source [Key] |
|---|---|---|---|---|
| Z₂ invariant from parity eigenvalues (Fu-Kane-Mele shortcut) | Centrosymmetric band insulator with time-reversal symmetry; parity eigenvalues computable at all TRIM points | ⚠️ Applying the parity-eigenvalue shortcut to a non-centrosymmetric material where it is not valid | Use the general non-Abelian Berry-connection/Wilson-loop formula when inversion symmetry is absent; restrict the parity shortcut to centrosymmetric cases | FuKaneMele2007 |
| ARPES Dirac-cone linear-dispersion fit | Near the Dirac point, within the verified linear-dispersion window | ⚠️ Extending the fit window into the region where hexagonal warping or bulk-band hybridization bends the dispersion | Restrict the fit window to the confirmed linear regime and report the window bounds together with the extracted Dirac velocity | HasanKane2010 |
| k·p effective Dirac Hamiltonian fitting | A single, well-isolated surface-state band, with channel purity already confirmed | ⚠️ Fitting a k·p Hamiltonian to a mixed surface+bulk or surface+quantum-well dataset without first separating channels | Confirm channel purity via Node 2 methods before fitting; report the Hamiltonian parameters together with the channel-purity evidence | HasanKane2010, QiZhang2011 |
| HLN magnetoconductance fitting (parent-level pointer) | Quantum-interference transport is quasi-2D and diffusive over a justified low-field window | ⚠️ See `topological_insulator/wal_hln_transport.md` for the full applicability/error/correct-approach treatment — do not re-derive it inline here | Load the WAL/HLN sub-profile for any HLN fitting question | HLN1980 |

---

## 5. Domain-Specific Quality Metrics

| Metric | Abbreviation | Physical meaning | Typical value range | Conditions | Source [Key] |
|---|---|---|---|---|---|
| Bulk band gap | Eg | Energy gap between bulk valence and conduction bands | ~0.2–0.3 eV for Bi₂Se₃-family strong TIs; varies substantially by compound | Compound-specific; from ARPES or optical spectroscopy | Zhang2009_SingleDiracCone |
| Z₂ invariant set | (ν₀;ν₁ν₂ν₃) | Topological classification index | ν₀=1 → strong TI; ν₀=0 with any νᵢ=1 → weak TI; all zero → trivial insulator | Requires a centrosymmetric or Wilson-loop calculation | FuKaneMele2007 |
| Dirac-point offset from Fermi level | ED−EF | Chemical-potential position relative to the topological surface state's Dirac point | Highly sample-dependent; as-grown samples often show EF well above ED due to unintentional n-type doping | ARPES-measured; doping- and surface-preparation-dependent | HasanKane2010 |
| Surface-state spin polarization | P | Degree of spin-momentum locking measured by SARPES | Theoretical ideal ~100%; experimentally reduced (often to roughly 20–60%) by bulk-band overlap and instrumental resolution | SARPES-measured; resolution- and overlap-dependent | HasanKane2010 |
| Phase coherence length (parent-level pointer) | Lφ | See `topological_insulator/wal_hln_transport.md` Node 5 for the full metric treatment | Sample- and temperature-dependent | — | HLN1980 |

---

## 6. Common Assumption Pitfalls

| Pitfall | Trigger condition | How to recognize it | Correct approach | Source [Key] |
|---|---|---|---|---|
| Treating any linear band crossing as a topological Dirac cone | User reports "linear dispersion" as proof of a TI surface state | No symmetry/topology check (Z₂, parity, or bulk-boundary correspondence) accompanies the claim | Establish bulk band topology (Z₂ invariant) independently before calling a linear feature "topological" | FuKaneMele2007 |
| Applying Z₂ classification outside TRS-preserving band insulators | User applies Z₂ indices to a magnetically ordered or strongly interacting system | The system explicitly breaks time-reversal symmetry or is not a single-particle band insulator | Z₂ classification requires TRS and band-insulator behavior; use QAHE/Chern-number or many-body topological frameworks instead | FuKaneMele2007 |
| Assuming an ARPES surface state is automatically the dominant transport channel | User infers "surface-dominated transport" from ARPES alone | No transport measurement (Hall, magnetotransport) accompanies the spectroscopic claim | ARPES probes occupied electronic structure, not carrier transport; corroborate with Node 2 transport methods before claiming transport dominance | HasanKane2010 |
| Blind HLN fitting outside the diffusive quasi-2D regime | User fits HLN to wide-field or 3D/ballistic magnetoresistance data | See `wal_hln_transport.md` for the full symptom/recovery treatment — this row is a pointer | Load the WAL/HLN sub-profile before interpreting any HLN fit | HLN1980 |
| Assuming magnetic doping automatically produces QAHE | User reports magnetic doping plus an anomalous Hall signal as QAHE | No Hall-resistance quantization (h/e²) or vanishing longitudinal resistance is shown | Require a quantized plateau and vanishing Rxx, not just a nonzero anomalous Hall signal | Chang2013_QAHE |
| Confusing weak-TI robustness with strong-TI robustness | User assumes a weak-TI (ν₀=0) classification confers the same disorder-robust surface states as a strong TI | Weak-TI surface states are protected only under weak, layer-preserving disorder; strong bulk disorder can gap them, unlike a strong TI's protected surface | Distinguish weak (ν₀=0) from strong (ν₀=1) TI before claiming disorder robustness | FuKaneMele2007 |
| Extrapolating one TI compound's properties to "all TI materials" | User generalizes a Bi₂Se₃-specific finding to the whole TI materials class | Different TI compounds (Bi₂Se₃, Bi₂Te₃, Sb₂Te₃, HgTe quantum wells, ternary compounds) have very different gaps, Dirac velocities, and defect chemistry | Confirm which specific compound/branch a claim applies to; route to a material-specific sub-profile (e.g. `bi2se3_material.md`) when one exists | Ando2013_PedagogicalReview |

---

## 7a. Literature Anchors

| Type | Reference | Why it matters |
|---|---|---|
| Textbook | Bernevig, B.A. & Hughes, T.L., *Topological Insulators and Topological Superconductors*, Princeton University Press (2013) | The standard graduate-level synthesis of the field; self-contained derivations for Z₂ classification, k·p models, and topological superconductivity |
| Review | Hasan, M.Z. & Kane, C.L., "Colloquium: Topological insulators," Rev. Mod. Phys. 82, 3045 (2010) | The most-cited foundational colloquium; defines the standard terminology and experimental framing used throughout this profile |
| Review | Qi, X.-L. & Zhang, S.-C., "Topological insulators and superconductors," Rev. Mod. Phys. 83, 1057 (2011) | Companion review with a more field-theoretic/topological-response framing; the second most-used background source in this profile |
| Materials review | Ando, Y., "Topological Insulator Materials," J. Phys. Soc. Jpn. 82, 102001 (2013), arXiv:1304.5693 | Pedagogical, materials-focused review — which TI compounds exist, their gaps and growth methods, complementing the more theory-focused reviews above |
| Methods paper | Fu, L., Kane, C.L., Mele, E.J., "Topological Insulators in Three Dimensions," Phys. Rev. Lett. 98, 106803 (2007), arXiv:cond-mat/0607699 | Establishes the 3D Z₂ classification (4 invariants; strong vs. weak TI) that Node 4/5's Z₂ rows depend on |

## 7b. Source Ledger (completed 2026-08-24; supersedes the earlier partial-inventory version)

> **Inline rewrite completed 2026-08-24 (second pass).** The first pass added this ledger but left
> all 73 `[web:NN]` markers (23 distinct tags) in Nodes 1–6 — a half-migration, since a table that
> only resolves opaque indices still leaves every citation unreadable without a lookup. All 73
> markers have now been rewritten to the `[Key]` values below (31 citation runs; adjacent duplicates
> collapsed). Every tag resolved from this ledger's own "formerly web:NN" annotations — none was
> guessed, and no claim was added or removed in the rewrite. Four tags (`web:30/33/36/62`) had been
> resolved by the first pass to the same **three-source WAL/HLN cluster** rather than to individual
> papers; they are therefore rendered as all three keys together, which is what the evidence
> actually supports. `web:60` was recorded as needing no source; it is now the explicit
> `[general-method]` key rather than an opaque number. The verification statuses below are
> unchanged — several remain `~` Approximate ("representative paper", not confirmed as the exact
> source the original session intended), and rewriting the markers did not upgrade them.

> **Verified (date)** (`domain-expansion-guide.md` §3.7): when this row's claim was last checked
> against the primary source — not the source's own publication year.
>
> **2026-08-26 currency pass** (audit trail: `reports/2026-08-26-scientific-research-guide-source-currency-pass.md`).
> 14 of the 16 rows were re-resolved against Crossref and/or the arXiv API; **no erratum or retraction
> was found on any of them**, and — contrary to what this profile's `[web:NN]`-packet origin would
> predict — **no wrong-author or wrong-venue defect was found either**. The pass added three
> previously-missing published DOIs (`Bi2Se3_SurfaceOxidation_JVSTA2016`, `Ando2013_PedagogicalReview`,
> `GrapheneTI_ProximitySOC_PRB2023`), dropped the "representative paper" hedge on the three rows whose
> identity is now unambiguous (`BernevigHughesZhang2006`, `FuKaneMele2007`, `Chang2013_QAHE`), and
> upgraded two rows that had been carried over on another file's verification. Two rows were **not**
> attempted and say so: `BiSe_BulkConduction_General` (already disclosed as a multi-source claim with
> no single DOI) and `general-method` (no source by design). Three arXiv-sourced rows carry an open
> §3.7 **version pin**: which version the original packet read was never recorded, and this pass would
> have had to guess — an honest gap is left instead.

| Key | Full citation | Identifier | Access tag | Verification status | Verified (date) | Locator | Used in |
|---|---|---|---|---|---|---|---|
| HasanKane2010 | Hasan, M.Z. & Kane, C.L., "Colloquium: Topological insulators," Rev. Mod. Phys. 82, 3045–3067 (2010) | DOI: 10.1103/RevModPhys.82.3045 | [abstract] | ✅ Confirmed (Crossref 2026-08-26: title, both authors, vol. 82(4), pp. 3045–3067, issued 2010-11-08 — exact match; no erratum/retraction. Bibliographic identity only — the review itself was not re-read) | 2026-08-26 | Whole paper | Nodes 1, 2, 4, 5 (dominant background reference, formerly web:22/55) |
| QiZhang2011 | Qi, X.-L. & Zhang, S.-C., "Topological insulators and superconductors," Rev. Mod. Phys. 83, 1057–1110 (2011) | DOI: 10.1103/RevModPhys.83.1057 | [abstract] | ✅ Confirmed (Crossref 2026-08-26: title, both authors, vol. 83(4), pp. 1057–1110, issued 2011-10-14 — exact match; no erratum/retraction. Bibliographic identity only — the review itself was not re-read) | 2026-08-26 | Whole paper | Nodes 1, 2, 4 (formerly web:39/54) |
| FuKaneMele2007 | Fu, L., Kane, C.L., Mele, E.J., "Topological Insulators in Three Dimensions," Phys. Rev. Lett. 98, 106803 (2007) | DOI: 10.1103/PhysRevLett.98.106803; arXiv:cond-mat/0607699 (⚠ §3.7 version pin outstanding — the version originally consulted was never recorded, and this pass would have had to guess) | [abstract] | ✅ Confirmed (Crossref + arXiv 2026-08-26: the PRL record and the preprint's own journal-ref agree on title, all three authors, and PRL 98, 106803. The earlier "representative paper" hedge is **dropped** — this is the paper the Z₂-classification claim describes) | 2026-08-26 | Whole paper | Nodes 1, 4, 5, 6 (formerly web:45/48) |
| BernevigHughesZhang2006 | Bernevig, B.A., Hughes, T.L., Zhang, S.-C., "Quantum Spin Hall Effect and Topological Phase Transition in HgTe Quantum Wells," Science 314, 1757–1761 (2006) | DOI: 10.1126/science.1133734 | [abstract] | ✅ Confirmed (Crossref 2026-08-26: title, three authors in order, Science 314(5806), pp. 1757–1761 — exact match; no erratum/retraction. The "representative paper" hedge is **dropped**: the identity is unambiguous) | 2026-08-26 | Whole paper | Node 1 (formerly web:26) |
| Zhang2009_SingleDiracCone | Zhang, H. et al., "Topological insulators in Bi₂Se₃, Bi₂Te₃ and Sb₂Te₃ with a single Dirac cone on the surface," Nat. Phys. 5, 438–442 (2009) | DOI: 10.1038/nphys1270 | [abstract] | ✅ Confirmed (same paper independently verified for `bi2se3_material.md`; re-resolved here against Crossref 2026-08-26 — title, all six authors, Nat. Phys. 5(6), pp. 438–442 — exact match, no erratum/retraction) | 2026-08-26 | Whole paper | Nodes 1, 5 (formerly web:52/29) |
| HLN1980 | Hikami, S., Larkin, A.I., Nagaoka, Y., "Spin-Orbit Interaction and Magnetoresistance in the Two Dimensional Random System," Prog. Theor. Phys. 63(2), 707–710 (1980) | DOI: 10.1143/PTP.63.707 | [abstract] | ✅ Confirmed (same source independently verified for `wal_hln_transport.md`; re-resolved here against Crossref 2026-08-26 — title, three authors, Prog. Theor. Phys. 63(2), pp. 707–710 — exact match, no erratum/retraction) | 2026-08-26 | Whole paper | Nodes 1, 2, 4, 5, 6 (formerly web:33/30/36/62) |
| Adroguer2015 | Adroguer et al., "Conductivity corrections for topological insulators with spin-orbit impurities: Hikami–Larkin–Nagaoka formula revisited," Phys. Rev. B 92, 241402(R) (2015) | DOI: 10.1103/PhysRevB.92.241402 | [abstract] | ✅ Confirmed — **upgraded from `~ Approximate` 2026-08-26**: independently re-fetched here (Crossref: title, all four authors, PRB 92(24), article 241402, issued 2015-12-04), so the "not re-fetched separately" caveat no longer applies | 2026-08-26 | Whole paper | Node 2 (formerly part of web:33/30/36/62 cluster) |
| Wang2014_WAL_WL_Crossover | Wang et al., "Crossover between weak antilocalization and weak localization of bulk states in ultrathin Bi₂Se₃ films," Sci. Rep. 4, 5817 (2014) | DOI: 10.1038/srep05817 | [abstract] | ✅ Confirmed — **upgraded from `~ Approximate` 2026-08-26**: independently re-fetched here (Crossref: title, full 12-author list, Sci. Rep. 4, article 5817, issued 2014-07-24), so the "not re-fetched separately" caveat no longer applies | 2026-08-26 | Whole paper | Node 2 (formerly part of web:33/30/36/62 cluster) |
| Xia2009_LargeGap | Xia, Y. et al., "Observation of a large-gap topological-insulator class with a single Dirac cone on the surface," Nat. Phys. 5, 398–402 (2009) | DOI: 10.1038/nphys1274 | [abstract] | ~ Approximate (plausible candidate for the Dirac-cone/spin-momentum-locking ARPES claim; not confirmed as the exact originally-intended source — a dedicated spin-momentum-locking paper such as Hsieh et al. 2009 was not separately searched). Bibliographic identity re-confirmed 2026-08-26 (Crossref: title, all 11 authors, Nat. Phys. 5(6), pp. 398–402; no erratum/retraction) — the identity is settled, the **topical-fit** question is not, and this pass did not attempt to resolve it (it needs full-text reading or a comparative search against the named alternative) | 2026-08-26 (identity only; topical fit still open) | Whole paper | Nodes 1, 2 (formerly web:38/68) |
| Chang2013_QAHE | Chang, C.-Z. et al., "Experimental Observation of the Quantum Anomalous Hall Effect in a Magnetic Topological Insulator," Science 340, 167–170 (2013) | DOI: 10.1126/science.1234414 | [abstract] | ✅ Confirmed (Crossref 2026-08-26: title, full 23-author list, Science 340(6129), pp. 167–170 — exact match; no erratum/retraction. The "representative paper" hedge is **dropped**: this is the specific first-observation QAHE paper the row's claim describes) | 2026-08-26 | Whole paper | Nodes 1, 2, 6 (formerly web:66) |
| BiSe_BulkConduction_General | General finding: Se-vacancy-driven unintentional n-type bulk conduction in Bi₂Se₃/Bi₂Te₃ — corroborated across multiple native-point-defect studies found 2026-08-24, no single canonical source pinned down | (multiple sources; none individually resolved to a specific DOI in this pass) | [secondary] | ~ Approximate (well-established finding, same claim independently verified with its own sources in `bi2se3_material.md` Node 1 constraint 1) | ⚠ not re-verified in the 2026-08-26 pass — deliberately not attempted: pinning one canonical Se-vacancy defect-chemistry source is a literature search, not a re-resolution, and was out of that pass's bounded scope. `review-when:` this row is next cited for a *specific numeric* claim rather than a general one | — | Nodes 1, 2 (formerly web:17/65) |
| Ando2013_PedagogicalReview | Ando, Y., "Topological Insulator Materials," J. Phys. Soc. Jpn. 82, 102001 (2013) | DOI: 10.7566/jpsj.82.102001; arXiv:1304.5693 (v1 2013-04-21 … v3 2013-09-03 — ⚠ §3.7 version pin outstanding: which version was consulted was never recorded) | [abstract] | ✅ Confirmed 2026-08-24 (title matches the profile's original "Pedagogical review 'Topological insulator materials'" description exactly); re-resolved 2026-08-26 — sole author Yoichi Ando confirmed via arXiv, and the **published DOI was located and added** (it was missing: the row carried only the preprint id) | 2026-08-26 | Whole paper | Metadata; Node 6 (formerly web:40/41) |
| BernevigHughes2013_Textbook | Bernevig, B.A. & Hughes, T.L., *Topological Insulators and Topological Superconductors*, Princeton University Press (2013) | DOI: 10.1515/9781400846733 | [secondary] (canonical textbook, not individually re-fetched) | ~ Approximate (confirmed real textbook 2026-08-24; the profile's original "Bernevig course notes" description likely refers to material that became this book, not verified as byte-identical). **2026-08-26 finding:** Crossref's record for this book DOI lists **only B. A. Bernevig** as author — T. L. Hughes' co-authorship is corroborated at chapter-DOI level but not from the book's own front matter, because the publisher page returned HTTP 405 to automated fetch. The two-author byline above is retained (it is the widely-cited form) but is *not* confirmed from a primary record. `review-when:` the Princeton UP / De Gruyter listing becomes fetchable — then confirm the title-page byline | 2026-08-26 (identity partial — see the byline note) | Whole textbook | Metadata; Node 2 QAHE row (formerly web:51/58) |
| Bi2Se3_SurfaceOxidation_JVSTA2016 | "Surface Oxidation of the Topological Insulator Bi₂Se₃," J. Vac. Sci. Technol. A 34, 061403 (2016) | DOI: 10.1116/1.4964637; arXiv:1601.04057v1 (sole existing version, 2016-01-15) | [abstract] | ✅ Confirmed 2026-08-24 (real paper directly on-topic; representative of a small cluster of similar Bi₂Se₃/Bi₂Te₃ surface-oxidation studies found in the same search); re-resolved 2026-08-26 — seven-author list confirmed via arXiv (Green, Dey, An, O'Brien, O'Mullane, Thiel, Diebold), the **published DOI was located and added**, and the preprint has only v1, so the §3.7 pin is exact | 2026-08-26 | Whole paper | Metadata; Node 2 ARPES sample-prep row (formerly web:56/63) |
| GrapheneTI_ProximitySOC_PRB2023 | "Twist-angle dependent proximity induced spin-orbit coupling in graphene/topological insulator heterostructures," Phys. Rev. B 107, 195144 (2023) | DOI: 10.1103/PhysRevB.107.195144; arXiv:2302.03102 (⚠ §3.7 version pin outstanding — version consulted never recorded) | [abstract] | ~ Approximate — **identity now settled, topical fit still not**: re-resolved 2026-08-26 (arXiv: title, authors Thomas Naimer & Jaroslav Fabian, journal-ref PRB 107, 195144), and the published DOI was added. The remaining hedge is only about whether this is the *best* representative of graphene/TI proximity SOC — several candidates exist and this pass did not compare them | 2026-08-26 (identity only; representativeness still open) | Whole paper | Node 1 engineering-nature line; Node 2 graphene/TI proximity row (formerly web:35) |
| general-method | web:60 (Node 2 magnetotransport "applicable conditions" cell, phrase "below strong quantum limit") | none | none | No dedicated source needed — general methodological point about magnetotransport field-range selection, consistent with the treatment already in `wal_hln_transport.md` | — (no source to verify, by design) | — | Node 2 |

---

## Cross-Domain Links

### Closest Related Domain Profiles

| Profile name | Overlap dimensions | Typical use split |
|---|---|---|
| `gan_power_device.md` | fabrication vocabulary (RIE, ALD, XPS/EDS), some shared characterization tools | Use this profile for band-topology, transport, and TI-specific device physics; use the GaN profile for power-device blocking/conduction electrostatics — do not import TI surface-state assumptions into GaN MOS interfaces |
| `microled.md` | surface-state and optical characterization vocabulary, only in specialized experiments | A microLED sidewall state is not a topological surface state; use this profile only when band topology is actually the question |
| `plasmonic_waveguide.md` (+ `plasmonic_waveguide/active_modulation.md`, `topological_insulator/bi2se3_plasmonic_photoresponse.md`) | Bi₂Se₃-based plasmonic/photogalvanic devices sit at the boundary of both domains | Use `topological_insulator/bi2se3_plasmonic_photoresponse.md` for Bi₂Se₃-specific carrier/symmetry reasoning; use `plasmonic_waveguide.md` for generic SPP mode/geometry physics |

---

## Cross-Domain Conflict Notes

| Issue / constraint | Other profile(s) involved | Potential conflict | AI confirmation question |
|---|---|---|---|
| Surface-state terminology reused across power/optical devices | `gan_power_device.md`, `microled.md` | A GaN interface trap or a microLED sidewall defect is not a topological surface state, despite similar "surface state" language | "Is this claim about a topologically protected boundary state (requires bulk Z₂ topology), or a conventional semiconductor interface/defect state?" |
| Bi₂Se₃ material data reused without band-topology context | `plasmonic_waveguide.md`, `plasmonic_waveguide/active_modulation.md` | A plasmonic or optical-modulation result using Bi₂Se₃ does not by itself establish which channel (Dirac surface, bulk, or 2DEG) is responsible | "Does this photoresponse/plasmonic result identify the topological surface channel specifically, or could it be bulk/2DEG dominated?" |
