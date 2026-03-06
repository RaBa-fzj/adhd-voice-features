# Voice Feature and Speech Embedding Analyses in ADHD


Associated Publication: *to be added* 


## Reproducibility and ethics

Due to privacy and ethical restrictions related to clinical data, the original dataset cannot be shared. The notebooks document the full analysis workflow and can be executed with equivalent datasets containing the same variables and structure.

## Repository Description

This repository contains two Jupyter notebooks for linear mixed model (LMM) analyses:
1) Voice feature LMMs (baseline and interaction effects).
2) Speech-embedding LMMs based on PCA of WavLM/Whisper embeddings.


**Expected data**

The notebooks expect a tabular dataset (e.g., `.xlsx`) containing participant identifiers, timepoints, task labels, diagnostic group, demographic covariates, acoustic voice features, speech embeddings, and Conners ADHD symptom scores.

**How to run**

1. Install required Python packages listed in the requirements section.
2. Update the `DATA_PATH` variable in each notebook to point to your dataset.
3. Run the notebooks sequentially from top to bottom.

---

## Notebook 1: LMM_Baseline_Treatment_Conners_git.ipynb

### Overview of Analyses
1) Data setup: load dataset, define column names and feature lists.
2) Preprocessing: filtering, exclusion, QC, standardization, equipment-sensitive handling.
3) LMMs: baseline group differences and group × time interaction per task and feature.
4) Multiple testing correction: FDR per task for baseline and interaction.
5) Sensitivity checks:
    * Ranked-data LMMs for significant features.
    * Time-between-visits covariate (days).
6) Plots: baseline boxplots and interaction line plots for significant features.
7) Post-hoc tests (ADHD only):
    * Change-score t-tests.
    * OLS on change scores.
    * Baseline and interaction clinical correlations with Conners scales.

---

## Notebook 2: PCA_LMM_Embeddings_git.ipynb

### Overview of Analyses
1) Data setup: load dataset and define embedding features (WavLM or Whisper).
2) Preprocessing: exclusion, stable categorical encoding, standardization (per task for PCA), eGeMAPS covariates.
3) PCA: fit on baseline (t0) data per task, project both timepoints.
4) LMMs on PCA scores: baseline and interaction effects per task x PC.
5) Post-hoc LMMs: re-test significant PCs controlling for eGeMAPS covariates.

---

## Requirements

### Python and Packages
* Python 3.9+
* Packages: numpy, pandas, statsmodels, scipy, matplotlib, seaborn, tqdm, xlsxwriter, scikit-learn

### Data Requirements
Your dataset must include at least:

* Participant ID
* Timepoint
* Task
* Group 
* Age
* Sex
* Equipment: Voice_Equipment (Notebook 1)
* Conners scales: hi_hyperactivity_score, ua_inattention_score (Notebook 1)
* Voice features listed in Notebook 1
* Embedding features: wavlm_000..wavlm_767 or whisp_000..whisp_767 (Notebook 2)
* eGeMAPS covariates used in Notebook 2


## Running the Notebooks

* Open and run each notebook top-to-bottom.
* Outputs are saved as Excel and PDF files where specified in the notebooks.


## Notes

* Equipment-sensitive features are filtered to reduce device bias.
* Low-variance features are skipped automatically.
* FDR is applied within task for baseline and interaction effects.

## Contact

For questions regarding the analysis code or repository, please contact: Rachel Bamberger (r.bamberger@fz-juelich.de)
