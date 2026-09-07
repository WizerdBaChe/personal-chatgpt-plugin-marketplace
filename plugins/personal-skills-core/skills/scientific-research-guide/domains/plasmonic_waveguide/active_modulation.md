---
xi: 1
what: "Sub-profile: Active Plasmonic Modulation — under Plasmonic Waveguide — Active-material and bias-to-spectrum validation traps"
tags: [srg-domain, 領域框架, sub-profile]
aliases: ["plasmonic modulator", "graphene modulator", "ITO", "ENZ", "epsilon-near-zero", "depletion", "accumulation", "bias-induced spectral shift", "topological modulator"]
date: 2026-09-02
status: live
profile_type: sub-profile
parent: "plasmonic_waveguide"
---
# Sub-profile: Active Plasmonic Modulation — under Plasmonic Waveguide

> Parent domain: `plasmonic_waveguide.md`
> Branch axis: method / material platform
> Scope: electrically or optically tunable graphene, conducting-oxide/ENZ, and
> topological-insulator plasmonic waveguides or resonators.
> Inherits from parent: Nodes 1–3 unless overridden below.

> **Decision point**: when the user compares graphene, ITO/ENZ, and TI modulator platforms,
> confirm the governing wavelength, the drive mechanism, and whether the priority is loss,
> footprint, bandwidth, or switching energy — the platforms do not rank the same way under
> different priorities.

## 4. Branch-Specific Modeling and Fitting

### Bias-to-spectrum chain

**Applicable conditions**: a device reports voltage-dependent effective index, loss,
resonance position, or transmission.

**Common error**: ⚠️ fitting spectral displacement directly against voltage and naming
one microscopic mechanism without validating the intermediate material response.

**Correct approach**: validate the chain in order:

```
electrical/optical drive
→ carrier and temperature distribution
→ complex material response versus frequency
→ complex modal index and overlap
→ finite-device spectrum
```

Report which links were measured, which were simulated, and which were assumed. Fit the
complex response, not only the resonance wavelength.

## 5. Branch-Specific Quality Metrics

| Metric | Physical meaning | Required context |
|---|---|---|
| Extinction ratio | On/off transmission contrast | Device length, wavelength, polarization, and drive condition |
| Insertion loss | Loss in the transmitting state | Coupler de-embedding and reference device |
| Modulation efficiency | Optical change per drive or length | Exact definition and electrical boundary conditions |
| Energy per bit / capacitance | Electrical switching cost | Drive waveform, device capacitance, resistance, and bandwidth |
| Spectral shift | Drive-induced resonance displacement | Thermal drift, hysteresis, linewidth, and uncertainty |
| Complex effective-index change | Phase and attenuation response | Material model, mode normalization, and overlap |

Do not provide a universal “typical range” for these metrics: platform, wavelength,
device length, resonance quality factor, and drive convention change the comparison.

## 6. Branch-Specific Assumption Pitfalls

| Pitfall | Trigger condition | How to recognize it | Correct approach |
|---|---|---|---|
| Treating ENZ as loss-free index enhancement | User says only that `Re(ε) ≈ 0` | Imaginary permittivity and field overlap are omitted | Use measured complex permittivity and report the absorption/confinement trade-off |
| Assuming accumulation, depletion, and injection are interchangeable | Bias changes an ITO or semiconductor device | No electrostatic stack or carrier profile is given | Confirm polarity, contacts, oxide, equilibrium carrier density, and the solved carrier distribution |
| Assigning every spectral shift to free carriers | Resonance moves with bias or pump | Temperature, charging, trapping, and hysteresis were not checked | Use controls or time/voltage sweeps that separate thermal, electrostatic, and trap-mediated effects |
| Reusing bulk ITO data for a fabricated film | ENZ wavelength is taken from a generic table | Deposition, anneal, and carrier density are unreported | Measure the actual film or use a process-matched optical/electrical dataset |
| Ignoring active-layer overlap | Large material-index change is claimed to guarantee large device modulation | Mode overlap is absent | Compute the complex modal response with the actual layer thickness and geometry |
| Attributing Bi₂Se₃ response solely to topological surface states | A TI device is called a “topological modulator” | Bulk carriers, 2DEG states, and optical phonons are omitted | Fit or constrain all plausible carrier and phonon contributions with transport/spectroscopy |
| Treating graphene gating as a scalar refractive-index change | Graphene is inserted into a 3D bulk-material solver | Surface conductivity and Fermi-level dependence are absent | Use an appropriate sheet-conductivity model and verify the scattering rate and gating regime |
| Ignoring electrical parasitics | Optical simulation alone is used to claim speed or energy | RC parameters and contacts are absent | Separate optical modulation depth from electrical bandwidth and switching-energy evidence |

## Evidence Anchors

- Oulton et al., *Nature Photonics* (2008), hybrid plasmonic geometry.
  DOI: https://doi.org/10.1038/nphoton.2008.131
- Ansell et al., “Hybrid graphene–plasmonic waveguide modulators,”
  *Nature Communications* 6, 8846 (2015). DOI: https://doi.org/10.1038/ncomms9846
- Swillam et al., “On chip optical modulator using epsilon-near-zero hybrid plasmonic
  platform,” *Scientific Reports* 9, 6669 (2019).
  DOI: https://doi.org/10.1038/s41598-019-42675-z
- Chen et al., “Real-space nanoimaging of THz polaritons in the topological insulator
  Bi₂Se₃,” *Nature Communications* 13, 1374 (2022).
  DOI: https://doi.org/10.1038/s41467-022-28791-x

## Source Ledger (backfilled 2026-08-24 per `domain-expansion-guide.md` §3.2)

> **Verified (date)** (`domain-expansion-guide.md` §3.7): when this row's claim was last checked
> against the primary source. **2026-08-26 currency pass**: all four rows re-resolved against
> Crossref — no dead DOI here (unlike the parent profile), no erratum. Three access tags were
> **upgraded to open access** (CC-BY confirmed), and `Chen2022_THz`'s full text was read directly and
> supports its pitfall-row attribution. `Oulton2008`'s citation paraphrased the title instead of
> quoting it; now quoted.

| Key | Full citation | Identifier | Access tag | Verification status | Verified (date) | Locator | Used in |
|---|---|---|---|---|---|---|---|
| Oulton2008 | Oulton et al., hybrid plasmonic waveguide geometry, Nature Photonics 2, 496–500 (2008) | DOI: 10.1038/nphoton.2008.131 | [abstract] | ~ Approximate (well-formed DOI, not independently re-fetched in this pass; also cited in `terminology_and_geometry.md`) | 2026-08-26 — Crossref identity match (title, full author list, volume/issue/pages, date); no erratum; the DOI actually resolves | Whole paper | Evidence anchor for hybrid-geometry background |
| Ansell2015 | Ansell et al., "Hybrid graphene–plasmonic waveguide modulators," Nat. Commun. 6, 8846 (2015) | DOI: 10.1038/ncomms9846 | [abstract] | ~ Approximate (well-formed DOI, not independently re-fetched in this pass) | 2026-08-26 — Crossref identity match; **access upgraded to open (CC-BY 4.0)** and the abstract read directly | Whole paper | §Graphene modulation background |
| Swillam2019 | Swillam et al., "On chip optical modulator using epsilon-near-zero hybrid plasmonic platform," Sci. Rep. 9, 6669 (2019) | DOI: 10.1038/s41598-019-42675-z | [abstract] | ~ Approximate (well-formed DOI, not independently re-fetched in this pass) | 2026-08-26 — Crossref identity match; **access upgraded to open (CC-BY 4.0)**, abstract read directly and it strengthens the pitfall-row attribution | Whole paper | §ENZ modulator pitfall row |
| Chen2022_THz | Chen et al., "Real-space nanoimaging of THz polaritons in the topological insulator Bi₂Se₃," Nat. Commun. 13, 1374 (2022) | DOI: 10.1038/s41467-022-28791-x | [abstract] | ~ Approximate (well-formed DOI, not independently re-fetched in this pass) | 2026-08-26 — Crossref identity match; **access upgraded to open (CC-BY 4.0)** and the **full text read directly**, which explicitly supports what this file attributes to it | Whole paper | §Bi₂Se₃ topological-modulator pitfall row |
