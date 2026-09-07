---
xi: 1
what: "Sub-profile: WAL, HLN, and Hall Transport — under Topological Insulator — Phenomenon/method sub-profile: WAL/HLN applicability and Hall-channel traps"
tags: [srg-domain, 領域框架, sub-profile]
aliases: ["WAL", "weak antilocalization", "HLN", "HNL", "Hikami-Larkin-Nagaoka", "magnetoconductance", "Hall measurement", "phase coherence"]
date: 2026-09-02
status: live
profile_type: sub-profile
parent: "topological_insulator"
---
# Sub-profile: WAL, HLN, and Hall Transport — under Topological Insulator

> Parent domain: `topological_insulator.md`
> Branch axis: phenomenon / method
> Scope: weak antilocalization (WAL), Hikami–Larkin–Nagaoka (HLN) fitting, and
> supporting Hall measurements in topological-insulator films and flakes.
> Inherits from parent: available Nodes 1–2. The parent Node 3 is currently
> incomplete; use the method-specific rules below rather than assuming a toolchain.

## 4. Branch-Specific Fitting Methods

### HLN magnetoconductance fitting

**Applicable conditions**: quantum-interference transport is quasi-two-dimensional and
diffusive over a justified low-field window; the elastic, phase-coherence, magnetic, and
spin-orbit length scales are compatible with the selected HLN form.

**Common error**: ⚠️ fitting magnetoresistance directly, using an arbitrary wide field
range, and interpreting the prefactor as a literal count of topological surfaces.

**Correct approach**:

1. Define `Δσ(B)` and the exact HLN sign/prefactor convention.
2. Convert resistance to conductivity using the actual tensor and device geometry.
3. Symmetrize/antisymmetrize field sweeps as appropriate and document background removal.
4. Fit a low-field window justified by the diffusive length scales.
5. Repeat across several nested fit windows and temperatures.
6. Inspect residuals and parameter covariance; report window sensitivity.
7. Interpret the prefactor only after considering bulk, surface, 2DEG, and coupled
   coherent channels.

### Hall extraction

**Applicable conditions**: a single dominant carrier produces a linear Hall response and
the sample geometry/contact assumptions are satisfied.

**Common error**: ⚠️ applying `n = 1/(qR_H)` and `μ = σ/(qn)` to nonlinear or multiband
Hall data and then using that result as proof of surface-only transport.

**Correct approach**: inspect Hall linearity, field range, contact offsets, and
longitudinal admixture. Use an explicitly justified multicarrier model when needed, and
report whether density is sheet or bulk density.

## 5. Branch-Specific Quality Metrics

| Metric | Interpretation rule |
|---|---|
| Phase-coherence length `L_phi` | Must be positive, physically scaled, and stable enough across fit windows to interpret; temperature dependence is more informative than one value |
| HLN prefactor | Convention- and model-dependent; never compare values before aligning equations and channel assumptions |
| Fit-window sensitivity | Large parameter drift across reasonable low-field windows signals model/background inadequacy |
| Residual structure | Systematic curvature or field-odd residuals indicate missing background, tensor mixing, or an unsuitable model |
| Hall linearity | A prerequisite for simple one-carrier extraction, not proof of a topological surface channel |

## 6. Branch-Specific Assumption Pitfalls

| Pitfall | Trigger condition | How to recognize it | Correct approach |
|---|---|---|---|
| Treating a zero-field cusp as unique proof of TSS transport | User identifies WAL by shape alone | No thickness, angle, gate, or channel evidence | Treat WAL as quantum-interference evidence; use complementary channel discrimination |
| Reading the HLN prefactor as an exact channel count | User maps one fitted value directly to top/bottom surfaces | Equation convention and channel coupling are unstated | Align conventions and test multiple-channel interpretations |
| Fitting outside the diffusive regime | Elastic mean free path is comparable to the magnetic length in the fit window | Parameters depend strongly on the high-field endpoint | Use a model valid for the measured regime or restrict the window |
| Ignoring classical magnetoresistance | Wide-field data are fit with HLN alone | Residuals curve systematically at larger fields | Model or remove a justified background before low-field interpretation |
| Fitting resistance instead of magnetoconductance | Raw `Rxx(B)` is inserted into the HLN expression | Hall mixing and tensor inversion are absent | Convert the measured tensor to conductivity with geometry corrections |
| Claiming “surface only” from Hall plus WAL | A one-carrier Hall result and WAL cusp are treated as decisive | Bulk/2DEG channels remain plausible | Add gate, thickness, angle, spectroscopy, or multichannel evidence |
| Treating `WAL@2 K` as a method name | Temperature is attached to the acronym | No temperature sweep or dephasing test | Record 2 K as one condition and analyze temperature dependence |
| `HNL` read as a distinct model | User writes "HNL equation" or "HNL fit" | The described physics is Hikami–Larkin–Nagaoka but the acronym is transposed | Confirm the intended model is HLN before correcting the name; do not silently normalize (moved from the abolished trigger checklist 2026-08-25) |
| Only the best-fit curve reported | User presents one fitted trace as the whole HLN result | No residuals, no parameter covariance/uncertainty, no fit-window stability check | Require residual inspection, covariance, and nested-window stability per the Node 4 procedure before interpreting any parameter (moved from the abolished trigger checklist 2026-08-25) |

## Evidence Anchors

- Hikami, Larkin, and Nagaoka, *Progress of Theoretical Physics* 63, 707–710 (1980).
  DOI: https://doi.org/10.1143/PTP.63.707
- Adroguer et al., “Conductivity corrections for topological insulators with
  spin-orbit impurities: Hikami–Larkin–Nagaoka formula revisited,”
  *Physical Review B* 92, 241402(R) (2015).
  DOI: https://doi.org/10.1103/PhysRevB.92.241402
- Wang et al., “Crossover between weak antilocalization and weak localization of bulk
  states in ultrathin Bi₂Se₃ films,” *Scientific Reports* 4, 5817 (2014).
  DOI: https://doi.org/10.1038/srep05817
- NIST, “Hall Effect Measurements,” archived measurement guide:
  https://www.nist.gov/pml/nanoscale-device-characterization-division/popular-links/hall-effect

## Source Ledger (backfilled 2026-08-24 per `domain-expansion-guide.md` §3.2)

> **Verified (date)** (`domain-expansion-guide.md` §3.7): when this row's claim was last checked
> against the primary source. **2026-08-26 currency pass** (audit trail:
> `reports/2026-08-26-scientific-research-guide-source-currency-pass.md`): all four rows re-resolved,
> no errata. This pass also closed a **cross-ledger disagreement**: `Adroguer2015` and
> `Wang2014_WAL_WL_Crossover` were still marked `~ Approximate (not independently re-fetched)` here
> while the parent `topological_insulator.md` had already re-fetched and upgraded both the same day.
> An independent third re-fetch reproduced the parent's findings exactly, so both are now ✅ in both
> ledgers. Two files describing the same source differently is itself a defect, even when neither is
> wrong about the facts.

| Key | Full citation | Identifier | Access tag | Verification status | Verified (date) | Locator | Used in |
|---|---|---|---|---|---|---|---|
| HLN1980 | Hikami, S., Larkin, A.I., Nagaoka, Y., "Spin-Orbit Interaction and Magnetoresistance in the Two Dimensional Random System," Prog. Theor. Phys. 63(2), 707–710 (1980) | DOI: 10.1143/PTP.63.707 | [abstract] | ✅ Confirmed (2026-08-24: title, authors, journal, volume/pages/date verified via search) | 2026-08-26 — re-resolved against Crossref (title, three authors, vol./pages, date exact); no erratum. Upgrades the 2026-08-24 search-based check to a metadata-record one | Whole paper | Node 4 HLN fitting method — the namesake original derivation |
| Adroguer2015 | Adroguer et al., "Conductivity corrections for topological insulators with spin-orbit impurities: Hikami–Larkin–Nagaoka formula revisited," Phys. Rev. B 92, 241402(R) (2015) | DOI: 10.1103/PhysRevB.92.241402 | [abstract] | ✅ Confirmed — **upgraded from `~ Approximate` 2026-08-26**: independently re-fetched (Crossref: title, all four authors, PRB 92(24) article 241402, issued 2015-12-04; no erratum). This also resolves a cross-ledger disagreement with the parent profile, which had upgraded the same row earlier the same day | 2026-08-26 | Whole paper | Node 4 HLN applicability caveats |
| Wang2014_WAL_WL_Crossover | Wang et al., "Crossover between weak antilocalization and weak localization of bulk states in ultrathin Bi₂Se₃ films," Sci. Rep. 4, 5817 (2014) | DOI: 10.1038/srep05817 | [abstract] | ✅ Confirmed — **upgraded from `~ Approximate` 2026-08-26**: independently re-fetched (Crossref: title, full 12-author list, Sci. Rep. 4 article 5817, issued 2014-07-24; no erratum), matching the parent profile's same-day upgrade. Scope note from the re-read: this paper's result is a **parallel-field, Dugaev–Khmelnitskii** crossover for bulk states, not a perpendicular-field HLN fit — which is why it belongs to the channel-discrimination pitfall and not to the HLN-method section, as this file already has it | 2026-08-26 | Whole paper | Node 6 pitfall rows on channel discrimination |
| NIST_HallGuide | NIST, "Hall Effect Measurements," archived measurement guide | URL: nist.gov/pml/nanoscale-device-characterization-division/popular-links/hall-effect | [partial] (web guide, not a peer-reviewed paper) | ✅ Confirmed live 2026-08-26 — the page was fetched and its content matches the described scope. ⚠ **New finding:** it now carries NIST's own banner saying the page is no longer updated and remains online for reference only, so it is a frozen archive rather than current guidance. `review-when:` NIST publishes a replacement guide | 2026-08-26 | Whole guide | Node 4 Hall extraction method |
