# FeCrAl-MIC-Spatial

A spatially explicit, coupled bio-electrochemical model of microbiologically
influenced pitting on FeCrAl accident-tolerant-fuel cladding in a
spent-fuel-pool environment.

**Status: pre-registered proposal.** See [PROTOCOL.md](PROTOCOL.md) — the
experimental matrix, negative-control gates, and endpoints are declared
before any model code or laboratory work exists. Nothing here is executed
yet; that is the point.

## The verified gap

No published model resolves an evolving, heterogeneous biofilm architecture
(a cellular Potts model) and closes the loop to local chemistry, localized
depassivation, and an updated surface. No MIC model of any class is coupled
to a radiation field, and no spatial corrosion model of any class addresses
FeCrAl. The nearest prior art (Kovacevic & Martinez-Paneda,
arXiv:2606.22640) is a phase-field MIC model that, by its own admission,
does not model the biofilm; the radiolysis literature itself warns that
radiation may passivate rather than depassivate oxide-forming alloys
(Motooka et al. 2014), so the sign of the radiation term is treated as an
empirical endpoint, not an assumption.

## What is here

- `PROTOCOL.md` — the pre-declared protocol: five-arm factor-complete
  experimental matrix (abiotic controls, surrogate-alloy method development,
  biofilm, full loop), measurement cadence, negative-control gates G1-G5,
  and endpoints, each anchored to verified literature verdicts (V1-V5).
- The model layer (CPM canopy -> reaction-diffusion microenvironment ->
  moving-boundary depassivation -> computed radiolysis field) and the
  measurement pipeline (time-lapse CLSM, SECM/SVET/LEIS, white-light
  interferometry) will be added as they are built, with the same
  commit-with-verdict discipline as the parent program.

## Lineage

Methods, export architecture (PVD-of-VTI 4D series), and negative-control
discipline are inherited from
[PRRT-spatial-CPM](https://github.com/aurascoper/PRRT-spatial-CPM) and the
Biofilms one-way radiation-transport framework. This repository is
independent by design: localized electrochemistry and moving-boundary
corrosion need a clean environment, not the tumor CPM codebase.

## Collaborators sought

This program needs a corrosion electrochemist / metallurgy co-author —
specifically someone who has run SECM, SVET, or LEIS on passive-film alloys,
to co-lead the Arm A-prime method development (the technique has never been
applied to FeCrAl; that is the point and the contribution). If that is you,
open an issue or reach out.

## License

CC0-1.0 — see [LICENSE](LICENSE).