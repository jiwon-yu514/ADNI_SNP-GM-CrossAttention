# SNP–GM Cross-Attention for ADNI Binary Classification

This project investigates multimodal Alzheimer’s disease stage classification using clinical, SNP, and gray matter ROI features derived from the ADNI dataset. The model focuses on learning relationships between genetic information and brain structural changes through SNP–GM cross-attention, with the goal of improving disease-stage classification performance.


## Data Description

This project uses preprocessed multimodal features derived from the ADNI dataset.  
The original cohort consists of 734 subjects across four diagnostic groups: CN, EMCI, LMCI, and AD.  
The model uses three types of input features: clinical variables, SNP features, and gray matter ROI volume features.

The data files used in this notebook are listed below.

| File name | Description | Shape / Content |
|---|---|---|
| `C_age.npy` | Age information for each subject | Clinical variable |
| `C_sex.npy` | Sex information for each subject | Clinical variable |
| `C_edu.npy` | Education years for each subject | Clinical variable |
| `S_MMSE.npy` | Mini-Mental State Examination score | Clinical cognitive score |
| `X_SNP 1.npy` | SNP feature matrix extracted from GWAS-based genetic data | 2,098 SNP features |
| `X_GM.npy` | Gray matter ROI volume feature matrix extracted from T1-weighted MRI using VBM | 93 GM ROI features |
| `Y_dis.npy` | Diagnostic labels for disease-stage classification | CN, EMCI, LMCI, AD |

Clinical features are constructed by combining age, sex, education, and MMSE.  
Sex is label-encoded, and continuous clinical variables are standardized before model training.  
Gray matter ROI features are also standardized to reduce scale differences across modalities.  
SNP features are used as high-dimensional genetic input features.

The dataset is not included in this repository due to data usage restrictions.  
Users should prepare the required `.npy` files separately and place them in the appropriate data directory before running the notebook.



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
