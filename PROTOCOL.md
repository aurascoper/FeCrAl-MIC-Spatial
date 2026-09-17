# PROTOCOL.md — Study M1: Spatially Explicit Coupled Bio-Electrochemical Model of Localized Pitting on FeCrAl ATF Cladding

**Status: DRAFT-PROPOSAL (v1.0). No model code is written, no laboratory work is
scheduled, and no endpoint number exists yet. This document pre-declares the
parameter space, the negative-control gates, and the endpoints before any of
them are computed or measured, under the same discipline as the PRRT-spatial-CPM
program (protocols v1.x, amendment history, verdicts committed with code).**

## 1. Goal

Verify, by construction, that an evolving, heterogeneous biofilm architecture
(cellular Potts model) can be coupled through a reaction-diffusion chemical
microenvironment to a spatially resolved moving-boundary depassivation model
of an FeCrAl accident-tolerant-fuel cladding surface, under a computed
radiolysis field appropriate to a spent-fuel-pool environment, and validated
against co-registered longitudinal measurements at the micrometer scale.

## 2. Declared inputs (literature verdicts, verified 2026-09-17)

Each design element below is fixed by a verified literature verdict, not a
convenience. The verdicts were produced by a pre-declared search procedure
(criteria before queries; near-hits characterized in full text).

- **V1 — Instrument transfer is unproven on this alloy.** Scanning
  electrochemical microscopy (SECM), scanning vibrating electrode technique
  (SVET), and localized electrochemical impedance spectroscopy (LEIS) have
  never been applied to FeCrAl/APMT. Precedent exists on stainless and carbon
  steel (Krawiec et al., microcell + SVET at MnS inclusions,
  doi:10.1016/s1388-2481(04)00109-2). Consequence: Arm A-prime (surrogate
  316L method development) is mandatory, and first spatially resolved
  electrochemical mapping on ATF cladding is itself a declared
  methodological contribution.
- **V2 — The chemical microenvironment has measured anchors.** Lee & de Beer
  (1995, doi:10.1080/08927019509378280) measured anodic-tubercle pH 5-7
  against cathodic-surface pH 9.45 under a biofilm, with oxygen depleted at
  anodes; differential aeration cells drove the corrosion. Consequence: the
  reaction-diffusion boundary conditions adopt this envelope; Arm B
  re-measures it on the FeCrAl system with modern dual DO+pH microsensors
  (Guimera et al. 2019, doi:10.3390/s19214747).
- **V3 — The radiolysis sign is an empirical question.** Dzaugis, Spivack &
  D'Hondt (2015, doi:10.1016/j.radphyschem.2015.06.011) provide the
  quantitative dose-rate-to-H2/H2O2 production model near radionuclide
  solids, applicable to spent-fuel-pool gamma fields. Motooka et al. (2014,
  doi:10.1080/00223131.2014.907550) found gamma radiolysis RAISED the pitting
  potential of Zircaloy-2 (H2O2-driven oxide thickening). Consequence: the
  radiolysis term in the coupled model may not be declared an accelerant a
  priori; Arm A is the sign-resolver and the model's ROS term is conditioned
  on its outcome.
- **V4 — The validation cadence is itself novel.** Correlative biofilm imaging
  exists (e.g., NMR + CLSM, McLean et al. 2007,
  doi:10.1038/ismej.2007.107), but daily co-registered CLSM and SECM/SVET
  rasters over identical coordinates on a corroding coupon have no published
  MIC precedent. Consequence: the measurement cadence is declared a
  methodological contribution of this study.
- **V5 — The three-way coupling is unclaimed.** Re-verified after adding the
  radiation facet: no published study couples (a) a spatially explicit,
  evolving cell lattice, to (b) spatially resolved electrochemistry / pitting
  algorithms, under (c) a computed radiation/ROS field. The nearest prior art
  is Kovacevic & Martinez-Paneda (arXiv:2606.22640), a phase-field MIC model
  that by its own admission does not model biofilm architecture or its
  evolution, and contains no radiation field.

## 3. The experimental matrix (five arms, factor-complete)

The biofilm x radiation factors require a complete 2x2 plus the
method-development arm; three arms alone would leave the radiation and
biofilm main effects confounded.

- **Arm A0 (FeCrAl, abiotic, no radiation):** passive-layer baseline;
  anchorage for every later contrast on the same alloy.
- **Arm A (FeCrAl, abiotic, + radiation):** the sign-resolver per V3. Does
  radiolysis passivate (Motooka pattern) or depassivate FeCrAl?
  Endpoint: pitting-potential shift and oxide characterization (XPS/EIS).
- **Arm A-prime (316L surrogate, method development):** validates the
  SECM/SVET/LEIS protocol on a steel with published precedent before it
  touches FeCrAl, per V1. Gate: current-density maps must reproduce the
  known 316L behavior before any FeCrAl scan is interpreted.
- **Arm B (FeCrAl, biofilm, no radiation):** the architecture and chemistry
  arm. Time-lapse CLSM canopy, SECM/micro-optode pH and O2 gradients per V2.
- **Arm C (FeCrAl, biofilm, + radiation):** the full loop. The coupled
  model's every term is exercised; selection under a radiation field is
  measured, not assumed.

## 4. The measurement cadence (declared contribution, per V4)

- T0: inoculation; bulk effluent sampling every 12 h (ICP-MS, HPLC) —
  global mass-balance bounds only, never local boundary conditions.
- T-dynamic: daily in-situ CLSM z-stacks of the live canopy AND daily
  SECM/SVET rasters over the same registered coordinates, in the same
  radiation-hardened flow cell on synthetic borated SFP water.
- T-final: coupon harvest, biofilm strip, white-light interferometry for
  the 3D crater map — the ground truth the model's final topography must
  match.

The bulk aliquots calibrate conservation (integral of modeled local
dissolution must not exceed total dissolved metal measured in bulk); the
spatial instruments calibrate the model. This division is the correction to
any protocol that would calibrate a localized 3D model with bulk fluid
chemistry.

## 5. Negative-control gates (pre-declared, must be able to fail)

- **G1 (Instrument):** Arm A-prime SECM/SVET maps on 316L must match the
  literature baseline before any FeCrAl interpretation. Fail = no FeCrAl
  electrochemistry is interpreted this campaign.
- **G2 (Sign):** Arm A must show a statistically resolved passivation or
  depassivation shift; an unresolved result sends the radiolysis term to a
  declared neutral default and is reported as a finding either way.
- **G3 (Null-selection):** a CPM canopy with uniform traits and no radiation
  must produce no spatially structured pit pattern beyond instrument noise;
  structured output would mean the coupling machinery fabricates structure.
- **G4 (Mass-balance):** at every time point, the model-integrated metal
  dissolution must not exceed the ICP-MS bulk bound. Exceedance = model
  defect, not a corrected bound.
- **G5 (Endpoint honesty):** the WLI crater map is compared to model output
  only after the model is frozen; no parameter may be fitted to the crater
  map (the framework is explicitly non-calibrating).

## 6. Endpoints (pre-declared)

1. Passivation-sign verdict for radiolysis on FeCrAl (Arm A vs A0).
2. Measured pH/O2 envelope under the canopy (Arm B), against the V2 ranges.
3. Spatial correlation between canopy thickness (CLSM), local current
   density (SVET), and local chemistry (SECM) in Arm C — the physical
   correlation the model must reproduce.
4. Model-vs-WLI topography agreement at T-final, scored only after G1-G4.
5. The 4D export: every arm writes the same PVD-of-VTI series established in
   the PRRT program (time-dependent state volumes; no flow field is computed
   or exported by the model unless the declared NS/IFP coupling exists).

## 7. Amendment rule

Any change to sections 3-6 after data collection begins requires a versioned
amendment recorded below, before the affected number is computed. No
retroactive parameter changes.

## Amendment history

- v1.0 (2026-09-17): initial declaration. Five literature verdicts embedded
  as declared inputs; five-arm factor-complete matrix (A0, A, A-prime, B, C);
  gates G1-G5; endpoints 1-5. Status: DRAFT-PROPOSAL, nothing executed.