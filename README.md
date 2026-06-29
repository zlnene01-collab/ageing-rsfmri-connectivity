# Testing an fMRIPrep + Nilearn Workflow for PCC/DMN Resting-State Connectivity

## Project Overview

This repository contains my Brainhack School final project on testing a resting-state fMRI preprocessing and connectivity workflow using open neuroimaging data.

The original project goal was to compare age-related differences in resting-state brain networks between younger and older adults. Based on instructor and TA feedback, I narrowed the scope to make the project more feasible within the final project timeline.

The current focus is to test and document an fMRIPrep + Nilearn workflow using one subject first, with a planned downstream focus on the Default Mode Network (DMN) or posterior cingulate cortex (PCC) seed-based connectivity.

Because fMRIPrep did not fully complete successfully on my local machine, the final project focuses on the preprocessing setup, HTML visual report, quality-control outputs, crash logs, troubleshooting process, and planned Nilearn analysis.

## Research Question

Can I build and test a beginner-friendly workflow to preprocess resting-state fMRI data and prepare for PCC/DMN-based functional connectivity analysis?

## Dataset

This project uses OpenNeuro dataset ds003592, a neurocognitive ageing dataset with behavioral, structural, and multi-echo functional MRI measures.

Dataset link: https://openneuro.org/datasets/ds003592/versions/1.0.13

Initial test subject:

* Subject: `sub-25`
* Session: `ses-1`
* Age group: young adult
* Data used:

  * 1 T1-weighted anatomical image
  * 3 resting-state functional echo files

Large neuroimaging files are not uploaded to this repository. Raw BIDS data and large derivative files are stored locally.

## Project Motivation

Ageing is associated with changes in cognition and brain function. Resting-state fMRI can be used to study functional relationships between brain regions when participants are not performing a specific task.

Large-scale resting-state networks such as the Default Mode Network may show age-related differences. The PCC is a key hub of the Default Mode Network, so focusing on PCC/DMN connectivity provides a more specific and feasible direction for a beginner-level project.

## Narrowed Project Scope

The initial plan was to compare multiple resting-state networks across younger and older adults. However, fMRI preprocessing is computationally intensive, and fMRIPrep can take a long time or fail depending on the dataset and local environment.

Based on feedback from Prof. Joshua Goh and TAs, I narrowed the project to:

1. Start with one subject first.
2. Test the fMRIPrep workflow.
3. Inspect the HTML visual report.
4. Document preprocessing and crash-log troubleshooting.
5. Plan a Nilearn PCC/DMN connectivity workflow for future analysis.

Prof. Joshua Goh confirmed that the final presentation can focus on troubleshooting unresolved processing issues.

## Planned Workflow

```text
BIDS raw data
→ fMRIPrep preprocessing
→ HTML report / quality control
→ preprocessed BOLD + confounds
→ Nilearn ROI or atlas time series extraction
→ PCC or DMN connectivity analysis
```

## What I Completed

* Selected OpenNeuro dataset ds003592
* Selected `sub-25/ses-1` as the first test subject
* Prepared a small BIDS subset locally
* Set up Docker on a MacBook Pro
* Prepared the FreeSurfer license
* Ran fMRIPrep version 25.2.5 using Docker
* Generated an fMRIPrep HTML visual report
* Viewed the HTML report through a local Python HTTP server
* Inspected anatomical and functional quality-control figures
* Generated partial derivatives, including:

  * BOLD reference images
  * brain masks
  * motion correction transform files
* Inspected crash logs from failed fMRIPrep runs
* Reran fMRIPrep with `--fs-no-reconall` after a FreeSurfer/surface-related error
* Created a planned Nilearn PCC/DMN connectivity script

## fMRIPrep HTML Report

The fMRIPrep HTML report was successfully generated and viewed in the browser using a local Python server:

```bash
cd derivatives/fmriprep
python3 -m http.server 8080
```

The report was viewed at:

```text
http://localhost:8080/sub-25.html
```

The report includes:

* Subject summary
* Anatomical brain mask and tissue segmentation
* Spatial normalization to `MNI152NLin2009cAsym`
* Functional summary
* Functional-anatomical coregistration
* fMRIPrep command and version information
* Methods boilerplate

The report-level error section shows “No errors to report.” However, separate crash logs show that the full fMRIPrep workflow did not fully complete.

## Current fMRIPrep Status

The full fMRIPrep workflow did not complete successfully.

### Attempt 1: Full fMRIPrep run

The first run failed during a FreeSurfer/surface-related step.

The crash log showed a failure around:

```text
project_unproject
surface-sphere-project-unproject
```

This appears to be related to a FreeSurfer/surface workflow issue in the local Docker/Mac environment.

### Attempt 2: Rerun with `--fs-no-reconall`

After the first failure, I reran fMRIPrep with:

```bash
--fs-no-reconall
```

This skipped FreeSurfer reconstruction and allowed the workflow to progress further.

However, the second run failed later during the multi-echo T2SMap/S0map step. The crash log indicated that `S0map.nii.gz` was expected but not generated.

Because of this, the final files required for Nilearn connectivity analysis were not generated:

```text
desc-preproc_bold.nii.gz
desc-confounds_timeseries.tsv
```

## Key Outputs in This Repository

```text
docs/
├── data_sources.md
├── feedback_questions.md
├── preprocessing_log.md
├── project_plan.md
├── subject_selection_sub-02.md
└── subject_selection_sub-25.md

scripts/
├── 01_inspect_dataset.py
├── 02_extract_timeseries.py
├── 03_compute_connectivity.py
└── nilearn_pcc_connectivity_plan.py

results/
└── partial_derivatives_summary.md

figures/
└── selected fMRIPrep HTML report screenshots

reports/
├── sub-25_fmriprep_html-report.html
├── crashlog_01_full-fmriprep_freesurfer-project-unproject.txt
└── crashlog_02_fs-no-reconall_multiecho-t2smap-s0map.txt
```

## Planned Nilearn Analysis

The planned downstream analysis is documented in:

```text
scripts/nilearn_pcc_connectivity_plan.py
```

If fMRIPrep preprocessing is completed successfully later, the Nilearn workflow would:

1. Load the preprocessed BOLD image.
2. Load the confounds timeseries file.
3. Define one ROI or network, likely PCC or DMN.
4. Extract the ROI/network time series.
5. Compute seed-based or atlas-based functional connectivity.

The planned script is currently a workflow template because the required final fMRIPrep outputs were not generated.

## What I Learned

This project became a practical troubleshooting and workflow-building exercise. I learned that:

* fMRI preprocessing can be computationally intensive and difficult to run locally.
* Multi-echo fMRI data can introduce additional preprocessing complexity.
* Starting with one subject is important before scaling up.
* fMRIPrep HTML reports are useful for visual quality control.
* Crash logs are important for identifying where a workflow failed.
* The HTML report may show no report-level error even when separate crash logs indicate that the full workflow did not finish.
* A focused ROI/network question is more feasible than a broad multi-network comparison for a short beginner-level project.

## Limitations

This project does not currently include a completed young-vs-older connectivity comparison.

The main limitations are:

* Only one subject was tested.
* fMRIPrep did not fully complete.
* Final preprocessed BOLD and confounds files were not generated.
* Nilearn connectivity analysis remains a planned next step.
* Results should not be interpreted as evidence for age-related brain connectivity differences.

## Next Steps

Future work should:

1. Ask fMRIPrep-experienced TAs about the multi-echo T2SMap/S0map crash.
2. Try preprocessing on a stronger Linux/HPC system if available.
3. Consider simplifying the workflow or testing a single echo first.
4. Once final fMRIPrep outputs are generated, run the Nilearn PCC/DMN connectivity workflow.
5. Add an older comparison subject, such as `sub-02/ses-1`, after the workflow is stable.
6. Expand cautiously to a small balanced sample only if preprocessing succeeds.

## Project Status

Current status: preprocessing workflow tested, HTML visual report generated, crash logs documented, and downstream Nilearn PCC/DMN connectivity workflow planned.

The final presentation will focus on the fMRIPrep setup, quality-control report, unresolved processing issues, troubleshooting process, and planned next steps.

## Recent Progress: SPM Reorientation and Check Registration

After the initial fMRIPrep workflow did not fully complete, I continued the project using an SPM-based preprocessing approach, following feedback from the course instructors and TA.

To avoid carrying over earlier orientation issues, I returned to the raw unoriented T1w and fMRI files for `sub-25`. I manually adjusted only the T1w image in SPM, set the origin, and then applied the same reorientation to both the T1w image and the echo-2 fMRI image together. This followed the TA’s recommendation that the anatomical and functional images should be reoriented together using the same adjustment.

I then reran Check Registration using:

* `T1_raw_retry.nii,1`
* `func_echo2_raw_retry.nii,1`

The updated Check Registration result was reviewed by the TA and confirmed to look better. This represents a successful step forward in the manual SPM preprocessing workflow and provides a cleaner starting point for the next preprocessing steps.

### Updated SPM Progress

* Created clean retry copies from the raw unoriented files
* Displayed the raw T1w image in SPM
* Manually adjusted the T1w image orientation
* Applied the same reorientation to both T1w and fMRI images
* Reran Check Registration
* Received TA confirmation that the updated result looked improved

### Next Steps

The next step is to confirm the appropriate preprocessing order for this test workflow, especially whether to proceed with Realign first or Slice Timing first for the echo-2 fMRI image. After this, the workflow can continue toward a basic SPM preprocessing pipeline and later PCC / Default Mode Network connectivity analysis.
