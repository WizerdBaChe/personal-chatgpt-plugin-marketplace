---
xi: 1
what: "Boundary Note: Split-Ring Resonators and Plasmonic Waveguides — Boundary to electromagnetic metamaterials; corrects unsupported SRR equivalences"
tags: [srg-domain, 領域框架, boundary]
aliases: ["SRR", "split-ring resonator", "LSRR", "negative index", "metamaterial", "metasurface"]
date: 2026-09-02
status: live
profile_type: boundary
parent: "plasmonic_waveguide"
---
# Boundary Note: Split-Ring Resonators and Plasmonic Waveguides

> Parent domain: `plasmonic_waveguide.md`
> Type: boundary; load only when SRR, split-ring, LSRR, negative-index, or
> metamaterial terminology is explicit.
> Boundary: standalone SRR arrays are electromagnetic metamaterials or metasurfaces,
> not plasmonic waveguides merely because they contain metal.

## What can be retained from the supplied notes

- A split-ring resonator (SRR) is a subwavelength resonant element whose lowest-order
  behavior is often interpreted with an effective inductive-capacitive model.
- Geometry, material dispersion, loss, substrate, polarization, incidence angle, and
  coupling to neighboring resonators all affect the observed resonance.
- At optical and near-infrared frequencies, metallic SRRs support plasmonic current and
  charge modes. The circuit analogy becomes approximate because kinetic inductance,
  retardation, multipoles, bianisotropy, and material dispersion become important.
- SRRs can be placed in or near a guiding structure, but this does not make an SRR array
  equivalent to an IMI, MIM, or hybrid plasmonic waveguide.

## Corrections and boundary rules

1. **Do not expand `LSRR` without provenance.** It can denote different geometries or
   handedness conventions in different sources. Require the source's caption, diagram,
   or explicit definition.
2. **Do not equate an optical SRR resonance with generic LSPR.** Plasmonic language can
   be appropriate, but magnetic, electric, multipolar, and magnetoelectric responses
   must be identified from currents, charges, fields, symmetry, or parameter retrieval.
3. **Do not infer a negative refractive index from a transmission peak.** Verify phase
   dispersion or perform a causal effective-parameter retrieval; anisotropy and
   bianisotropy can invalidate a scalar `ε`/`μ` interpretation.
4. **Do not state that one SRR always supplies only negative permeability.** The
   electric and magnetic responses depend on geometry, orientation, coupling, and
   homogenization regime.
5. **Do not transfer microwave LC scaling unchanged to optical dimensions.** Use the
   actual dispersive material model and test whether homogenization remains valid.
6. **Do not use `n = -1` or “perfect lens” language as a device conclusion without**
   loss, bandwidth, impedance, spatial-dispersion, and finite-size evidence.

## Where to route the research question

- Route modal propagation, coupling loss, or IMI/MIM/HPW design back to
  `plasmonic_waveguide.md`.
- Route an SRR array's effective constitutive response, negative refraction, or
  metasurface retrieval to a future electromagnetic-metamaterial base profile.
- Route an optical SRR used only as a finite plasmonic resonator to a future
  plasmonic-resonator profile if that branch develops its own metrics and fitting rules.

## Evidence anchors

- Pendry et al., “Magnetism from conductors and enhanced nonlinear phenomena,”
  *IEEE Transactions on Microwave Theory and Techniques* 47, 2075–2084 (1999).
  DOI: https://doi.org/10.1109/22.798002
- Smith et al., “Composite medium with simultaneously negative permeability and
  permittivity,” *Physical Review Letters* 84, 4184–4187 (2000).
  DOI: https://doi.org/10.1103/PhysRevLett.84.4184
- Woodley et al., “Left-handed and right-handed metamaterials composed of split ring
  resonators and strip wires,” *Physical Review E* 71, 066605 (2005).
  DOI: https://doi.org/10.1103/PhysRevE.71.066605
- Seetharaman et al., “Electromagnetic interactions in a pair of coupled split-ring
  resonators,” *Physical Review B* 96, 085426 (2017).
  DOI: https://doi.org/10.1103/PhysRevB.96.085426

## Source Ledger (backfilled 2026-08-24 per `domain-expansion-guide.md` §3.2)

> **Verified (date)** (`domain-expansion-guide.md` §3.7): when this row's claim was last checked
> against the primary source. **2026-08-26 currency pass**: all four rows re-resolved against
> Crossref — no dead DOI, no erratum, no access upgrade available (all four remain paywalled and
> full-text reads were blocked). One open question was raised and **not** resolved: this file's
> `Smith2000` row credits that paper with the "perfect lens" caution, but that concept traces to a
> different, uncited Pendry paper. The full text could not be read to rule it out, so it is flagged
> rather than asserted.

| Key | Full citation | Identifier | Access tag | Verification status | Verified (date) | Locator | Used in |
|---|---|---|---|---|---|---|---|
| Pendry1999 | Pendry et al., "Magnetism from conductors and enhanced nonlinear phenomena," IEEE Trans. Microw. Theory Tech. 47, 2075–2084 (1999) | DOI: 10.1109/22.798002 | [abstract] | ~ Approximate (well-formed DOI, canonical foundational SRR paper, not independently re-fetched in this pass) | 2026-08-26 — Crossref identity match (full author list, volume/issue/pages, date); no erratum | Whole paper | Foundational SRR theory background |
| Smith2000 | Smith et al., "Composite medium with simultaneously negative permeability and permittivity," Phys. Rev. Lett. 84, 4184–4187 (2000) | DOI: 10.1103/PhysRevLett.84.4184 | [abstract] | ~ Approximate (well-formed DOI, canonical negative-index paper, not independently re-fetched in this pass) | 2026-08-26 (identity only) — Crossref identity match; no erratum. ⚠ **Open attribution question:** this row's "Used in" credits it with both the negative-index result *and* the "perfect lens" caution, but the perfect-lens concept traces to a **different, uncited Pendry paper**. The full text was paywalled, so this is flagged, not corrected. `review-when:` the full text becomes readable, or the perfect-lens claim is cited for anything load-bearing | Whole paper | "Perfect lens" / negative-index caution rules |
| Woodley2005 | Woodley et al., "Left-handed and right-handed metamaterials composed of split ring resonators and strip wires," Phys. Rev. E 71, 066605 (2005) | DOI: 10.1103/PhysRevE.71.066605 | [abstract] | ~ Approximate (well-formed DOI, not independently re-fetched in this pass) | 2026-08-26 — Crossref identity match (full author list, volume/issue, article number, date); no erratum | Whole paper | Background on SRR + strip-wire composites |
| Seetharaman2017 | Seetharaman et al., "Electromagnetic interactions in a pair of coupled split-ring resonators," Phys. Rev. B 96, 085426 (2017) | DOI: 10.1103/PhysRevB.96.085426 | [abstract] | ~ Approximate (well-formed DOI, not independently re-fetched in this pass) | 2026-08-26 — Crossref identity match (full author list, volume/issue, article number, date); no erratum | Whole paper | SRR coupling background |
