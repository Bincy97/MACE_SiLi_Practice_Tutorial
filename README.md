# MACE Hands-on Tutorial: Training and Fine-Tuning MLIPs

### A Beginner-Friendly Tutorial Using Si–Li DFT/AIMD Data

This repository contains the materials for a hands-on introductory tutorial on **Machine Learning Interatomic Potentials (MLIPs)** using [MACE](https://github.com/ACEsuit/mace).

The tutorial demonstrates how to prepare DFT reference data, train an MLIP from scratch, use a pretrained foundation model, and fine-tune it for a specific material system.

The examples use a small dataset of lithium-containing amorphous silicon (Si–Li) configurations obtained from DFT-based ab initio molecular dynamics (AIMD) simulations.

## 1. Tutorial Objectives

By completing the tutorial, participants will learn how to:

1. Understand the basic requirements for preparing DFT/AIMD datasets for MLIP training.
2. Train a MACE model from scratch using DFT energies and atomic forces.
3. Use a pretrained MACE-MP-0 foundation model for zero-shot predictions.
4. Fine-tune a pretrained model using material-specific DFT data.
5. Evaluate model performance using energy and force RMSE and parity plots.

Due to time limitations, the tutorial mainly focuses on **learning rate, training epochs, and RMSE** rather than detailed hyperparameter optimization.

## 2. Tutorial Notebooks

Two versions of the tutorial notebook are provided.

| Notebook | Description |
|---|---|
| [MACE_Tutorial_Practice.ipynb](notebook/MACE_Tutorial_Practice.ipynb) | Hands-on notebook without executed outputs. Recommended for participants. |
| [MACE_Tutorial_(outputs).ipynb](notebook/MACE_Tutorial_%28outputs%29.ipynb) | Reference notebook containing previously generated results, tables, and plots. |

### Run the Tutorial in Google Colab

**[Open Practice Notebook in Google Colab](https://colab.research.google.com/github/Bincy97/MACE_SiLi_Practice_Tutorial/blob/main/notebook/MACE_Tutorial_Practice.ipynb)**

No local MACE installation is required when using Google Colab.

1. Open the practice notebook using the link above.
2. Establish a Colab runtime connection.
3. Run the cells sequentially, following the Markdown explanations.
4. Compare your results with the reference notebook if needed.

A GPU is not required for this small tutorial dataset. The notebook has also been tested using a CPU, although execution times may vary.

## 3. Dataset

The tutorial uses 384 selected Si–Li AIMD configurations, divided into three independent subsets.

| Dataset | Configurations | Purpose |
|---|---:|---|
| `SiLi_train.xyz` | 192 | Training |
| `SiLi_valid.xyz` | 96 | Validation |
| `SiLi_test.xyz` | 96 | Independent testing |

Each configuration includes atomic species, atomic positions, simulation cell information, DFT total energy, and atomic forces.

**[Dataset and preparation details](data/README.md)**

The dataset is provided in the extended XYZ format compatible with ASE and MACE.

## 4. Repository Structure

```text
MACE_SiLi_Practice_Tutorial/
├── README.md
├── requirements.txt
│
├── data/
│   ├── README.md
│   ├── SiLi_train.xyz
│   ├── SiLi_valid.xyz
│   └── SiLi_test.xyz
│
└── notebook/
    ├── README.md
    ├── MACE_Tutorial_Practice.ipynb
    └── MACE_Tutorial_(outputs).ipynb
```

## 5. Tutorial Workflow

**DFT/AIMD data → Dataset preparation → Scratch training → Pretrained MACE → Fine-tuning → DFT comparison**

Throughout the tutorial, energy and force predictions are compared with DFT reference calculations to illustrate the differences between these approaches.

## 6. Important Notes

- The small dataset and short training runs are intended for educational purposes.
- The trained models are not validated for quantitative molecular dynamics, diffusion coefficients, or migration-barrier calculations.
- Model accuracy may vary depending on training settings, random initialization, and computing environment.
- For research applications, larger and more representative datasets and additional physical validation are required.

## 7. References and Resources

- [Official MACE GitHub Repository](https://github.com/ACEsuit/mace)
- [MACE Documentation](https://mace-docs.readthedocs.io/)
- [Atomic Simulation Environment (ASE)](https://ase-lib.org/)

---



