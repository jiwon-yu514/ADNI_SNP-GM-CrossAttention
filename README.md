# SNP–GM Cross-Attention for ADNI Binary Classification

This project investigates multimodal Alzheimer’s disease stage classification using clinical, SNP, and gray matter ROI features derived from the ADNI dataset. The model focuses on learning relationships between genetic information and brain structural changes through SNP–GM cross-attention, with the goal of improving disease-stage classification performance.


## Data Description and Preprocessing

This project uses preprocessed multimodal features derived from the ADNI dataset, including clinical information, SNP features, and gray matter ROI volume features. The cohort consists of 734 subjects from four diagnostic groups: CN, EMCI, LMCI, and AD.

To effectively integrate heterogeneous data with different characteristics, each modality is first mapped into a shared latent space with the same embedding dimension (`d = 64`). SNP and GM data are processed through independent token embedding-based encoders. The SNP features are transformed into a token-level representation of size `64 × 64`, while the GM features are transformed into a ROI-level representation of size `93 × 64`.

| File name | Description |
|---|---|
| `C_age.npy` | Age of each subject |
| `C_sex.npy` | Sex of each subject |
| `C_edu.npy` | Education years |
| `S_MMSE.npy` | MMSE cognitive assessment score |
| `X_SNP 1.npy` | GWAS-based SNP feature matrix with 2,098 SNP features |
| `X_GM.npy` | VBM-based gray matter ROI volume features extracted from T1-weighted MRI; 93 ROI features |
| `Y_dis.npy` | Diagnostic labels for CN, EMCI, LMCI, and AD |

Clinical information consists of age, sex, education, and MMSE. To reduce bias caused by scale differences across modalities, Z-score normalization is applied during preprocessing. In the notebook, the clinical variables are combined into a 4-dimensional clinical feature vector, and sex is label-encoded before model training.

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
