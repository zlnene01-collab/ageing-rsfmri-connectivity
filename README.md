# Age-related Differences in Resting-State Brain Networks Using Open fMRI Data

## Project Overview

This repository contains my Brainhack School final project on resting-state fMRI analysis and neurocognitive ageing.

The project aims to explore whether younger and older adults show differences in selected resting-state brain networks using open neuroimaging data. The main focus is to build a small, reproducible analysis workflow that directly works with fMRI data, including preprocessing documentation, feature extraction, visualization, and basic statistical comparison.

This is a learning-focused project. The goal is not to claim a novel finding about ageing, but to gain hands-on experience with open fMRI data, resting-state network analysis, and reproducible neuroimaging workflows.

## Research Question

Do younger and older adults show differences in selected resting-state brain networks, such as the Default Mode Network, Salience Network, and Executive Control Network?

## Dataset

The project will use **OpenNeuro ds003592**, a neurocognitive ageing dataset that includes younger and older healthy adults.

Dataset link: https://openneuro.org/datasets/ds003592/versions/1.0.13

The dataset includes:

* Structural MRI
* Multi-echo resting-state fMRI
* Behavioral measures
* Participant-level metadata

The initial plan is to start with a small number of participants to test the workflow. If the workflow is successful, the analysis may be expanded to a small balanced group, such as approximately 5 younger adults and 5 older adults.

Large neuroimaging files will not be uploaded to this GitHub repository. Raw data and derivatives will be stored locally.

## Project Motivation

Ageing is associated with changes in cognition and brain function. Resting-state fMRI provides a way to examine spontaneous brain activity and functional relationships between brain regions when participants are not performing a specific task.

Previous research suggests that large-scale resting-state networks, such as the Default Mode Network, Salience Network, and Executive Control Network, may show age-related differences. This project uses open fMRI data to learn how these network-level differences can be explored through a small-scale analysis workflow.

## Planned Analysis Workflow

The planned workflow includes the following steps:

1. Inspect the dataset metadata and BIDS organization.
2. Select one younger adult and one older adult as initial test cases.
3. Check whether usable preprocessed derivatives are available.
4. If needed and feasible, run or inspect fMRI preprocessing using fMRIPrep.
5. Document preprocessing decisions and quality-control concerns.
6. Extract resting-state network or ROI-level features.
7. Compute functional connectivity or network-level summary measures.
8. Compare younger and older adults using simple statistical analyses.
9. Visualize group-level results using connectivity heatmaps, network summary plots, or group comparison figures.
10. Document limitations and possible future directions.

## Possible Analysis Routes

I am currently considering two possible routes:

### Route 1: fMRIPrep + Nilearn Atlas-Based Functional Connectivity

This route would involve:

* Using fMRIPrep outputs or a simple preprocessing workflow
* Selecting an atlas, such as Schaefer or Harvard-Oxford
* Extracting ROI-level time series
* Computing ROI-to-ROI correlations
* Creating connectivity matrices
* Comparing network-level connectivity between younger and older adults

### Route 2: fMRIPrep + ICA-Based Resting-State Network Analysis

This route would involve:

* Using preprocessed resting-state fMRI data
* Running or learning an ICA-based analysis
* Identifying selected networks such as DMN, Salience Network, and ECN
* Comparing network measures between younger and older adults

The final route will depend on feasibility, available support, and feedback from the fMRI pod / TAs.

## Preprocessing Considerations

Preprocessing choices can affect resting-state fMRI results. This project will be careful with:

* Motion correction
* Confound regression
* Temporal filtering
* Spatial normalization
* Spatial smoothing
* Quality control
* Head motion differences between age groups

Spatial smoothing will be considered carefully because it may artificially increase correlations between nearby voxel time series and influence functional connectivity estimates.

## Statistical Plan

The statistical analysis will start simple and remain exploratory.

Possible analyses include:

* Comparing network-level connectivity measures between younger and older adults
* Two-sample t-tests if assumptions are reasonable
* Mann-Whitney U tests if the data are not normally distributed
* Linear regression models if covariates such as sex or mean motion need to be included
* Multiple-comparison correction if many connections or networks are tested

Because this is a small learning-focused project, the results will be interpreted cautiously.

## Expected Deliverables

The expected final deliverables include:

* A structured GitHub repository
* Jupyter notebooks and/or Python scripts
* Subject selection documentation
* Preprocessing and quality-control notes
* Functional connectivity matrices or network-level summaries
* Visualizations of selected resting-state networks
* Basic statistical comparison between younger and older adults
* A web-based final project page
* A final reflection on limitations and future directions

## Repository Structure

```text
.
├── README.md
├── docs/
│   ├── project_plan.md
│   ├── data_sources.md
│   ├── preprocessing_notes.md
│   └── feedback_questions.md
├── notebooks/
│   ├── 01_dataset_overview.ipynb
│   ├── 02_subject_selection.ipynb
│   ├── 03_preprocessing_qc.ipynb
│   ├── 04_network_analysis.ipynb
│   └── 05_group_statistics.ipynb
├── scripts/
│   ├── extract_confounds.py
│   ├── extract_timeseries.py
│   └── compute_connectivity.py
├── figures/
├── results/
├── requirements.txt
└── .gitignore
```

## Local Data Organization

Raw neuroimaging data and large derivative files will not be committed to this repository.

Suggested local paths:

```text
data/ds003592/              # OpenNeuro BIDS dataset, not committed
derivatives/fmriprep/       # fMRIPrep derivatives, not committed
derivatives/connectivity/   # extracted time series and connectivity outputs
results/                    # statistical outputs and tables
figures/                    # selected final figures
```

## Setup

A Python environment may be created with:

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Planned Python packages include:

```text
numpy
pandas
matplotlib
seaborn
nilearn
nibabel
scipy
scikit-learn
jupyter
```

Additional tools may include fMRIPrep, depending on preprocessing needs and computational feasibility.

## Current Questions for Feedback

I am currently seeking feedback on the following questions:

1. Is fMRIPrep + Nilearn a reasonable workflow for a beginner-level resting-state fMRI project?
2. Would ICA-based resting-state network analysis be more appropriate than atlas-based functional connectivity?
3. Which atlas or template would be suitable for examining DMN, Salience Network, and Executive Control Network?
4. How should spatial smoothing be handled in a correlation-based functional connectivity analysis?
5. What statistical approach would be reasonable for comparing younger and older adults in a small sample?
6. What preprocessing steps should be prioritized for a small individual final project?

## Project Status

This project is currently in the planning and setup stage.

The immediate goals are:

* Create the GitHub repository
* Post the project direction to the Brainhack School projects-2026 channel
* Receive feedback from the fMRI pod / TAs
* Inspect OpenNeuro ds003592 metadata
* Select initial test participants
* Decide on the most feasible analysis route

## Notes

This project is intended as a practical learning exercise in open fMRI data analysis. The analysis will be documented carefully, and limitations will be reported clearly.
