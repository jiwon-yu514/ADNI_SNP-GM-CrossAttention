# SNP–GM Cross-Attention for ADNI Binary Classification

This project investigates multimodal Alzheimer’s disease stage classification using clinical, SNP, and gray matter ROI features derived from the ADNI dataset. The model focuses on learning relationships between genetic information and brain structural changes through SNP–GM cross-attention, with the goal of improving disease-stage classification performance.


## Model Architecture

![Model Architecture](figures/model_architecture.png)

The proposed model consists of three main stages: feature embedding, bidirectional SNP–GM cross-attention, and multimodal feature integration for classification.

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

## Results

The model was evaluated using 5-fold cross-validation across five binary classification tasks. The table below summarizes the performance of the proposed Cross-Attention model reported in the paper.

| Task | AUC | Accuracy | Macro-F1 | Sensitivity | Specificity |
|---|---:|---:|---:|---:|---:|
| CN vs AD | 0.9736 ± 0.0256 | 0.9506 ± 0.0188 | 0.9500 ± 0.0191 | 0.9362 ± 0.0434 | 0.9622 ± 0.0286 |
| CN vs eMCI | 0.8185 ± 0.0573 | 0.7828 ± 0.0494 | 0.7805 ± 0.0370 | 0.7377 ± 0.0955 | 0.8250 ± 0.0667 |
| CN vs MCI | 0.8589 ± 0.0383 | 0.8092 ± 0.0424 | 0.7972 ± 0.0425 | 0.8256 ± 0.0643 | 0.7823 ± 0.0707 |
| LMCI vs AD | 0.8601 ± 0.0660 | 0.7963 ± 0.0618 | 0.7961 ± 0.0618 | 0.7682 ± 0.0640 | 0.8274 ± 0.0756 |
| MCI vs AD | 0.8846 ± 0.0382 | 0.8258 ± 0.0525 | 0.8022 ± 0.0484 | 0.7225 ± 0.0737 | 0.8768 ± 0.1023 |

The proposed SNP–GM Cross-Attention model achieved strong performance across all binary classification tasks, with the highest AUC in the CN vs AD task. It also showed meaningful performance improvement in early-stage classification tasks such as CN vs eMCI and CN vs MCI, where disease-stage differences are more subtle.
