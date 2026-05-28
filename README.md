# SNP–GM Cross-Attention for ADNI Binary Classification

This project explores multimodal deep learning for Alzheimer’s disease stage classification using ADNI-derived clinical, genetic, and brain structure features. The main focus is to investigate whether SNP–GM cross-attention can capture meaningful relationships between genetic variation and gray matter structural changes, and whether these relationships can improve binary classification performance across different disease-stage comparison tasks.

## Data files

The notebook expects the following `.npy` files in `DATA_DIR`:

```text
C_age.npy
C_sex.npy
C_edu.npy
S_MMSE.npy
X_SNP 1.npy
X_GM.npy
Y_dis.npy
```

ADNI-derived data are not included in this repository. Do not upload private, restricted, or license-controlled data files to GitHub.

## How to run

1. Open `SNPXGM_github_clean.ipynb` in Google Colab.
2. Mount Google Drive if using Colab.
3. Set `DATA_DIR` to the folder containing the required `.npy` files.
4. Run the notebook from top to bottom.

## Experiments

The notebook evaluates the following binary tasks:

- CN vs EMCI
- CN vs MCI
- MCI vs AD
- LMCI vs AD
- CN vs AD

Metrics:

- Accuracy
- Macro-F1
- AUC
- Sensitivity
- Specificity

## Notes on reproducibility

The notebook uses random seeds, but GPU-based deep learning can still show small variations across repeated runs depending on CUDA, PyTorch, DataLoader shuffling, and nondeterministic operations. For strict reproducibility, fix the DataLoader generator and deterministic backend settings before final reporting.
