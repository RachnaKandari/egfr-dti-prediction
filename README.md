# egfr-dti-prediction
# EGFR Inhibitor Prediction — Drug–Target Interaction (DTI) Modeling

Machine learning pipeline to predict binding strength (pIC50) between small-molecule compounds and the EGFR (Epidermal Growth Factor Receptor) protein, a well-established oncology drug target. This project is a working example of ML-based drug–target interaction prediction, a core method in computational drug discovery.

## Data

- Source: [ChEMBL](https://www.ebi.ac.uk/chembl/) database, target **CHEMBL203** (human EGFR)
- 607 unique compounds with experimentally measured IC50 values
- IC50 (nM) converted to pIC50 (`-log10(IC50 in M)`) for regression

## Method

- **Molecular representation:** Morgan (ECFP-style) fingerprints, radius 2, 1024 bits, generated with RDKit
- **Models:** Random Forest and XGBoost regressors
- **Evaluation:** 80/20 train/test split, R² and MAE

## Results

| Model | Representation | R² | MAE |
|---|---|---|---|
| Random Forest (initial version) | Physicochemical descriptors | 0.724 | 0.780 |
| Random Forest (updated) | Morgan fingerprints | 0.792 | 0.505 |
| XGBoost (updated) | Morgan fingerprints | **0.797** | **0.500** |

Switching from basic physicochemical descriptors to Morgan fingerprints was the primary driver of improvement, with XGBoost adding a smaller additional gain over Random Forest.

## Files

- `egfr_clean.csv` — cleaned dataset (SMILES, pIC50)
- `egfr_dti_model.ipynb` — full pipeline: data loading, fingerprint generation, model training, evaluation

## Motivation & Future Direction

This project is preliminary work toward a PhD research direction in ML-based drug–target interaction prediction for computational drug discovery, with a focus on oncology targets. Planned extensions include graph-based molecular representations (GNNs), additional oncology-relevant targets beyond EGFR, and a translational layer evaluating predicted candidates on drug-likeness and development feasibility.
