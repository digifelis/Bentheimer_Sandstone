# Leakage-Controlled Resolution-Bias Correction for Pore-Scale Permeability

This repository contains the public computational records supporting the manuscript
"Leakage-Controlled Resolution-Bias Correction for Pore-Scale Permeability in
Micro-CT Bentheimer Sandstone."

## Scope

The archive provides the ROI registry, L1/4x and L2/2x voxel-CFD summaries,
matched native-resolution L3/1x pilot summaries, model metrics and predictions,
computational-cost records, analysis code, and the figures used in the manuscript.
The repository supports the reported resolution-bias correction analysis; it does
not claim that L2 is physical ground truth or that the three voxel tiers establish
monotonic grid convergence.

## Repository contents

- `results/operator_v1/roi_registry/`: all candidate and accepted ROI records,
  blockwise split assignments, and axis-conditioned case plans.
- `results/operator_v1/cfd_results/`: retained L1/4x and L2/2x CFD flow and
  permeability summaries, including acceptance diagnostics.
- `results/operator_v1/fidelity_comparison/`: matched L1-L2 permeability records
  and resolution-sensitivity summaries.
- `results/operator_v1/multifidelity_correction/`: correction metrics,
  predictions, training tables, and paired held-out error diagnostics.
- `results/operator_v1/operator_models/`: ridge and random-forest metrics and
  predictions for the single-fidelity baselines.
- `results/operator_v1/operator_voxel_cnn*/`: voxel-CNN metrics, histories,
  predictions, and five-seed robustness records.
- `results/operator_v1/operator_graph_gcn/`: regional pore-graph GCN metrics,
  predictions, and five-seed robustness records.
- `results/operator_v1/revision_support/`: native L3 pilot, REV/field-of-view,
  voxel-interface, augmentation, and stage-resolved cost summaries.
- `figures/paper/`: the 14 raster figures embedded in the revised manuscript.
- `src/`, `scripts/`, and `tests/`: implementation, analysis entry points, and tests.
- `PUBLICATION_MANIFEST.csv`: relative paths, byte sizes, and SHA-256 hashes for
  the public archive.

## Data provenance

The segmented Bentheimer sandstone source images are from the DRP-236 data set:

Digital Rocks Portal, "Bentheimer Sandstone for Analyzing Wetting Phenomena
(DRP-236)," https://digitalporousmedia.org/published-datasets/tapis/projects/
drp.project.published/drp.project.published.DRP-236

The large source NetCDF volumes and full OpenFOAM case directories are not
redistributed here. The public archive contains the derived ROI registry and the
retained numerical summaries needed to audit the manuscript results. Local case
paths in copied records are represented relative to `${PROJECT_ROOT}`.

## Environment

The retained Python requirements are listed in `requirements_locked.txt`, and
project metadata is in `pyproject.toml`. OpenFOAM workflows require a compatible
OpenFOAM installation in addition to the Python environment.

Typical setup:

```bash
python -m venv .venv
python -m pip install -r requirements_locked.txt
```

The analysis entry points added during revision are located directly under
`scripts/`, including `complete_revision_analyses.py`,
`run_operator_cnn_multiseed.py`, and `train_operator_graph_gcn.py`.

## Evidence boundaries

- The L3/1x evidence is a five-case x-flow pilot, including three test-block ROIs.
- The L1-L2-L3 sequence is non-monotonic and does not support a Grid Convergence
  Index or population-level native-resolution error bounds.
- The field-of-view study reports morphology through 320 voxels but does not
  establish a transport REV.
- The reported 12.5x ratio is a paired solver-stage L2/L1 timing ratio, not an
  end-to-end heterogeneous-hardware speedup.
- The retained data cover Bentheimer sandstone and single-phase permeability only.

## Integrity

Run the following command from the repository root to verify the copied archive:

```bash
python scripts/verify_publication_manifest.py
```

