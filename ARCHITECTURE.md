# ARCHITECTURE.md — Hybrid Model Architecture and 4D Data Exchange

This program is a **hybrid model**, not a single-method model. Declaring the
split up front is a design decision and a recruiting document: the biology,
the chemistry, and the metal degradation each live in the numerical method
built for them, coupled through declared interfaces.

## 1. The three layers

**The Canopy (CPM).** Biofilm growth, EPS secretion, cell death, and
stochastic architecture are modeled as a discrete Cellular Potts Model
(Metropolis copy attempts over a Hamiltonian). The CPM is chosen precisely
because the biology is porous, heterogeneous, and stochastic — properties a
continuum film assumption erases, and the exact property the nearest prior
art (Kovacevic & Martinez-Paneda, arXiv:2606.22640) declines to model.

**The Microenvironment (PDEs).** Chemical gradients — pH, O2, organic acids,
ROS — are continuous fields solved by finite-volume reaction-diffusion on
the same spatial grid. Boundary conditions are anchored to measured
microsensor envelopes (Lee & de Beer 1995; V2 of PROTOCOL.md), not bulk
aliquots.

**The Substrate (Phase-Field).** FeCrAl degradation is a phase-field moving
boundary: the metal-fluid interface is a continuous level-set function
driven by the local pH, chloride, and sulfide fields supplied by the PDE
layer. This is the Kovacevic/Martinez-Paneda class of formulation — coupled
to a living boundary condition instead of an assumed film.

**The coupling sentence:** the CPM acts as the dynamic, living boundary
condition for the phase-field pitting model. The biology sets where the
chemistry concentrates; the chemistry sets where the metal dissolves; the
dissolving surface feeds back through selection on the canopy. That loop is
the program.

## 2. The 4D spatiotemporal data exchange

The lack of a standardized exchange format between the discrete-CPM
community and the continuum (Navier-Stokes / phase-field) community is the
declared methodological gap this contract addresses (see the parent
program's manuscript, section "Data export architecture"). The spec below
is the contract every module writes and every downstream solver may read.

### 2.1 The spatial container: `cycle_{k}.vti` (VTK ImageData)

At the end of every simulation cycle k, the state is serialized to a VTI
file on a uniform rectilinear grid matching the CPM lattice pitch. Declared
spacing rides in the file's field data; an asymmetric orientation probe is
embedded to pin the axis convention (inherited from the Biofilms exchange
schema).

**PointData (continuum fields):**

- `pH_field` (Float64): local hydrogen ion activity.
- `O2_field` (Float64): local oxygen concentration.
- `Phase_Field_Metal` (Float64): the metal-to-fluid transition — the
  moving pitting boundary.

**CellData (discrete CPM fields):**

- `Cell_ID` (Int32): unique identifier for lineage tracking; 0 = void/fluid.
- `Tissue_Class` (Int8): 1 = viable SRB, 2 = EPS, 3 = necrotic,
  4 = FeCrAl substrate.
- `Dose_Accumulated` (Float64): voxel-level dosimetry. Present only when
  the Arm C loop is running — the export contains what the model computes,
  nothing else (the honest-label rule inherited from the parent program).

### 2.2 The temporal wrapper: `simulation_master.pvd`

One lightweight XML index binds the per-cycle VTI files into a streamable
4D sequence; consumers read the temporal evolution without loading the
whole dataset:

```xml
<?xml version="1.0"?>
<VTKFile type="Collection" version="0.1" byte_order="LittleEndian">
  <Collection>
    <DataSet timestep="0.0" group="" part="0" file="cycle_000.vti"/>
    <DataSet timestep="1.0" group="" part="0" file="cycle_001.vti"/>
    <DataSet timestep="2.0" group="" part="0" file="cycle_002.vti"/>
    <!-- Appended continuously during runtime -->
  </Collection>
</VTKFile>
```

### 2.3 Implementation constraint

The export module is strictly a serialization layer: decoupled from the CPM
dynamics, reading in-memory arrays and writing XML headers. It preserves
the ground-truth histology-chemistry-dose state for downstream continuum
coupling and never computes physics of its own.

## 3. Declared choices (to be pinned by protocol amendment before implementation)

- **Level-set range convention.** The membrane level-set form follows Shen
  et al. (arXiv:2205.07190), phi in [-1, 1]; Kovacevic's corrosion phase
  field uses phi in [0, 1]. The substrate convention is pinned by protocol
  amendment before the phase-field layer is implemented; the divergence is
  declared here rather than resolved silently.
- **Units in array names.** The parent program carries units in names
  (e.g. `dose_Gy`). If adopted here it happens by amendment; the names
  above are canonical until then.
- **No flow field is exported** unless the declared Navier-Stokes /
  interstitial-pressure coupling actually exists in the model. The honest
  label travels with the data: this export is a histology-chemistry-dose
  state.

## 4. Standing collaboration rule

The agent drafts and verifies; the human transmits. No autonomous posting
into the collaboration channel (Discord or otherwise): replies to
collaborators are pasted by the operator, preserving voice, pacing, and
ownership of the repositories.