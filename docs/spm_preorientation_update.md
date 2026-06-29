# SPM Reorientation and Check Registration Update

## Context

The original project aimed to compare age-related differences in resting-state brain networks using open fMRI data. The first preprocessing attempt used fMRIPrep, but the workflow did not fully complete due to technical issues related to FreeSurfer / surface processing and later multi-echo T2SMap / S0map generation.

Following instructor and TA feedback, I continued the project using an SPM-based preprocessing approach.

## Files Used

For this retry step, I returned to the raw unoriented files and created clean working copies:

```text
spm_work/sub-25/anat/T1_raw_retry.nii
spm_work/sub-25/func/func_echo2_raw_retry.nii
```

The echo-2 fMRI image was used as a test functional image for the SPM workflow.

## Procedure

1. Opened `T1_raw_retry.nii` in SPM Display.
2. Manually adjusted the T1w image orientation.
3. Used the T1w image as the reference for AC-PC style reorientation.
4. Pressed **Set Origin** after manual adjustment.
5. Applied the same reorientation to both:

   * `T1_raw_retry.nii,1`
   * `func_echo2_raw_retry.nii,1`
6. Reran Check Registration using the reoriented T1w and fMRI images.
7. Sent the updated Check Registration screenshot to the TA for feedback.

## Result

The TA confirmed that the updated Check Registration result looked better. This suggests that reorienting the raw T1w and fMRI files together using the same adjustment was more appropriate than trying to manually adjust the functional image separately.

## Reflection

This step was important because it showed that preprocessing is not only about running automated pipelines. Manual quality control, careful file handling, and feedback-based correction are also essential parts of neuroimaging research. Returning to the raw files and retrying the reorientation step helped create a cleaner and more reliable starting point for future preprocessing.

## Next Steps

The next step is to confirm the correct preprocessing order in SPM, especially whether to proceed with Realign first or Slice Timing first for the echo-2 fMRI test image. After this, the project can continue toward a basic preprocessing workflow and future PCC / Default Mode Network connectivity analysis.
