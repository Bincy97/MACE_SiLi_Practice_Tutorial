# MACE Tutorial Notebooks

This folder contains two versions of the hands-on MACE tutorial for training and fine-tuning machine-learning interatomic potentials using Si–Li DFT data.

## 1. MACE_Tutorial_Practice.ipynb

**Hands-on Practice Notebook**

- Contains the complete tutorial code and Markdown explanations.
- Cell outputs have been cleared so participants can execute the calculations themselves.
- **Recommended for use during the hands-on session.**

## 2. MACE_Tutorial_(outputs).ipynb

**Reference Notebook with Results**

- Contains the same tutorial workflow with previously generated outputs.
- Includes training results, RMSE tables, and DFT–MACE comparison plots.
- Useful for checking expected results or reviewing the tutorial afterward.

## How to Use

1. Open `MACE_Tutorial_Practice.ipynb` in Google Colab.
2. Establish a Colab runtime connection.
3. Execute the notebook cells sequentially.
4. Refer to `MACE_Tutorial_(outputs).ipynb` to compare your results with the reference results.

**Note:** Training results and execution times may vary depending on the computing environment. The tutorial can run on a CPU, although execution may be slower than on a GPU.

All required Si–Li datasets and dataset-preparation details are available in the repository's `data/` folder.
