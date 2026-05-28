# SNP–GM Cross-Attention for ADNI Binary Classification

This project investigates multimodal Alzheimer’s disease stage classification using clinical, SNP, and gray matter ROI features derived from the ADNI dataset. The model focuses on learning relationships between genetic information and brain structural changes through SNP–GM cross-attention, with the goal of improving disease-stage classification performance.


## Data Description

This project uses preprocessed multimodal features derived from the ADNI dataset, including GWAS-based SNP features, VBM-based gray matter ROI volume features extracted from T1-weighted MRI, and clinical variables such as age, sex, education, and MMSE. The cohort consists of 734 subjects from four diagnostic groups: CN, EMCI, LMCI, and AD.

| File name | Description |
|---|---|
| `C_age.npy` | Age of each subject |
| `C_sex.npy` | Sex of each subject |
| `C_edu.npy` | Education years |
| `S_MMSE.npy` | MMSE cognitive assessment score |
| `X_SNP 1.npy` | GWAS-based SNP feature matrix with 2,098 SNP features |
| `X_GM.npy` | VBM-based gray matter ROI volume features extracted from T1-weighted MRI; 93 ROI features |
| `Y_dis.npy` | Diagnostic labels for CN, EMCI, LMCI, and AD |

Clinical variables consist of age, sex, education, and MMSE. To reduce scale differences across modalities, Z-score normalization is applied to the clinical variables and GM ROI volume features before model training.

The data files are not included in this repository due to ADNI data usage restrictions.



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
