# SNP–GM Cross-Attention for ADNI Binary Classification

This repository contains a Colab/Jupyter notebook for multimodal binary classification using ADNI-derived features:

- Clinical features: age, sex, education, MMSE
- SNP features
- Gray matter ROI volume features
- Attention-based fusion models: self-attention, cross-attention, and self+cross attention

## Repository files

```text
SNPXGM_github_clean.ipynb
README.md
requirements.txt
.gitignore
```

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
