# mimic-iii-adversarial-attack-defenses

This repository contains the full pipeline for my MSc. thesis titled “Analyzing the Impact of Adversarial Attacks on AI in Medical Systems and the Effectiveness of Defense Mechanisms.”

The project uses the MIMIC-III v1.4 critical care database to build machine learning models that predict in-hospital mortality from the first 24 hours of an ICU stay.

NOTE: The 24-hour limit can be adjusted/increased if needed in the data extraction pipeline if necessary, by adjusting the INTIME_24H parameter.

The code is organised into five main notebooks:

1_Data_Extraction_Pipeline_Merge
Builds the ICU cohort from MIMIC-III (single ICU stay per patient), joins core tables and timestamped vitals/labs and produces the denormalised master_24h.csv.

2_EDA_Preprocess_Cleanup
Performs exploratory analysis, applies physiological and unit checks, handles missingness and winsorisation and creates the final train/test splits (train_clean.csv, test_clean.csv).

3_Models_Baselines
Trains baseline models (Logistic Regression, Random Forest, XGBoost) with sklearn pipelines, evaluates ROC AUC / PR AUC / F1 and evaluates calibration and feature importance.

4_Adversarial_Attacks
Implements a white-box FGSM-based attack on numeric features using quantile clipping and finite-difference gradients, evaluates how performance degrades and analyses which features are perturbed most.

5_Defences
Tests simple defenses, including inference-time clipping and FGSM-based adversarial training, and re-evaluates model robustness on clean and attacked data.

The repository does not include any MIMIC-III v1.4 data. Access requires separate approval via PhysioNet and paths in the notebooks assume that the user has already downloaded and locally prepared the database by extracting the zipped CSVs.

The MIMIC-III database is available here: https://physionet.org/content/mimiciii/1.4/

The unzipped CSVs are to be stored in a folder whose path is the value for the “base_dir” parameter. 
By default it is set to the following:
base_dir = r"D:\Path\to\the\directory\where\the\extracted_mimic_iii_data\is\stored"

An additional notebook titled “MIMIC_III_DataRead” is available to provide a glimpse into some of the MIMIC-III database files.
