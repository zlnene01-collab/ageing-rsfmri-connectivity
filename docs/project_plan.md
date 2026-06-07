# Project Plan

## Main Goal

The main goal of this project is to learn and implement a small-scale resting-state fMRI analysis workflow using open neuroimaging data.

## Dataset

The project will use OpenNeuro ds003592, a neurocognitive ageing dataset with younger and older adults, structural MRI, multi-echo resting-state fMRI, and behavioral measures.

## Research Question

Do younger and older adults show differences in selected resting-state brain networks, such as the Default Mode Network, Salience Network, and Executive Control Network?

## Initial Scope

Start with:

- 1 younger adult
- 1 older adult

The first goal is to test whether the workflow is feasible.

## Initial Test Subjects

The first workflow test will use:

| Participant | Group | Age | Sex | Site | Session |
|---|---|---:|---|---|---|
| sub-25 | Young adult | 23 | F | 1 | ses-1 |
| sub-02 | Older adult | 73 | F | 1 | ses-1 |

Both participants appear to have T1w anatomical MRI and multi-echo resting-state fMRI files.

## Expanded Scope

If the initial workflow works, expand to approximately:

- 5 younger adults
- 5 older adults

## Possible Analysis Routes

### Route 1: fMRIPrep + Nilearn Atlas-Based Functional Connectivity

This route will use atlas-based ROI time series extraction and compute ROI-to-ROI functional connectivity matrices.

### Route 2: fMRIPrep + ICA-Based Resting-State Network Analysis

This route will use ICA to identify resting-state network components such as DMN, Salience Network, and Executive Control Network.

## Current Preferred Route

The current preferred route is fMRIPrep + Nilearn atlas-based functional connectivity because it may be more beginner-friendly and easier to document in Python.

## Preprocessing Notes

Important preprocessing considerations include:

- Motion correction
- Confound regression
- Temporal filtering
- Spatial normalization
- Spatial smoothing
- Quality control
- Head motion differences between younger and older adults

Spatial smoothing will be handled carefully because it may affect correlation-based functional connectivity estimates.

## Statistical Plan

Possible statistical approaches include:

- Two-sample t-test
- Mann-Whitney U test
- Linear regression including covariates such as sex or mean motion

The statistical analysis will be exploratory because the sample size may be small.

## Expected Outputs

Expected outputs include:

- Subject selection table
- Preprocessing notes
- QC summary
- Connectivity matrices
- Network-level summary measures
- Group comparison plots
- Basic statistical test results
- Web-based final project page
