# Si–Li AIMD Dataset for MACE Training and Fine-Tuning

## 1. Dataset Overview

This directory contains a subset of density functional theory (DFT)-based *ab initio* molecular dynamics (AIMD) configurations of lithium-containing amorphous silicon (a-Si).

The dataset is prepared for a hands-on tutorial demonstrating three approaches to machine-learning interatomic potentials (MLIPs):

1. Training a MACE model from scratch.
2. Predicting energies and forces using a pretrained MACE foundation model.
3. Fine-tuning a pretrained MACE model using system-specific DFT data.

Each configuration contains atomic positions, simulation cell information, DFT total energy, and atomic forces.

## 2. Original AIMD Dataset

The original dataset consists of amorphous silicon systems containing 64 Si atoms and varying numbers of Li atoms.

| Parameter | Description |
|---|---|
| Material system | Li-containing amorphous silicon |
| Compositions | Si₆₄Li₁ to Si₆₄Li₈ |
| Si atoms | 64 |
| Li atoms | 1–8 |
| Initial structures | 3 per composition |
| Temperatures | 300, 500, and 1000 K |
| AIMD steps | 5,000 per trajectory |
| Number of trajectories | 72 |
| Total candidate configurations | 360,000 |
| DFT software | VASP |
| Exchange–correlation | PBE-based PAW setup |
| Plane-wave cutoff | 499 eV |
| K-point sampling | 1 k-point |
| Spin polarization | Enabled |

The original AIMD calculations were performed using VASP with a Nosé–Hoover-type thermostat setting (`MDALGO = 2`) and a 2 fs simulation timestep (`POTIM = 2`).

The reported temperature was held constant within each trajectory using `TEBEG = TEEND`.

## 3. Tutorial Dataset Preparation

To make the hands-on exercises computationally practical, a smaller dataset was extracted from the original AIMD trajectories.

The preparation consisted of two stages:

**Stage 1 — AIMD extraction**

Every tenth configuration was selected from the original trajectories, producing 36,000 configurations.

**Stage 2 — Tutorial subset selection**

A smaller collection of configurations was selected across all eight Li compositions and three temperatures.

The dataset was separated according to the original starting structures to reduce overlap between training, validation, and test trajectories.

| Dataset | Starting structure | Configurations |
|---|---|---:|
| Training | Str1 | 192 |
| Validation | Str2 | 96 |
| Testing | Str3 | 96 |
| **Total** | | **384** |

All three datasets cover the eight Li concentrations and three simulation temperatures.

Each subset is intended to support practical MACE exercises rather than serve as a fully optimized training dataset for production-scale molecular dynamics.

## 4. Dataset Files

The directory contains three files:

### `SiLi_train.xyz`

Contains 192 configurations for training a MACE model from scratch and for fine-tuning a pretrained MACE model.

### `SiLi_valid.xyz`

Contains 96 configurations used to monitor prediction errors and model generalization during training.

### `SiLi_test.xyz`

Contains 96 independent configurations reserved for evaluating the trained models.

All files use the extended XYZ (`extxyz`) format supported by ASE and MACE.

## 5. Information Stored in Each Configuration

Every configuration includes:

| Property | Key | Unit |
|---|---|---|
| Atomic species | Atomic numbers/symbols | — |
| Atomic positions | `positions` | Å |
| Periodic simulation cell | `Lattice` | Å |
| Periodic boundary conditions | `pbc` | — |
| DFT total energy | `DFT_energy` | eV |
| DFT atomic forces | `DFT_forces` | eV/Å |
| Li concentration | `Li_count` | Number of Li atoms |
| Simulation temperature | `temperature_K` | K |
| Initial structure identifier | `structure_id` | — |
| Source trajectory | `source_id` | — |
| Original frame index | `frame_index_0based` | — |

The DFT energies and forces are used as reference labels during MACE training.

The energy and force keys must be specified during training:

```bash
--energy_key="DFT_energy"
--forces_key="DFT_forces"
```

## 6. Important Scientific Considerations

- The tutorial dataset contains a limited number of configurations and is intended primarily for demonstrating MLIP training and fine-tuning.
- Frames from the same AIMD trajectory are temporally correlated, and the selected starting structures are not guaranteed to be statistically independent.
- Total energies depend on composition and DFT reference conventions. Energy comparisons across different Li concentrations require appropriate reference-energy handling.
- Prediction accuracy on this dataset does not automatically establish reliability for diffusion coefficients, migration barriers, or long-timescale molecular dynamics.
- The complete AIMD dataset and additional scientific validation would be required for more comprehensive research applications.

## 7. Intended Use

This dataset is provided for educational demonstrations of MACE training, foundation-model inference, fine-tuning, and energy/force prediction evaluation.

It is not presented as a validated production-quality interatomic potential dataset for quantitative Li diffusion studies in amorphous silicon.
