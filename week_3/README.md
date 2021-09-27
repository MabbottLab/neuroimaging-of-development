## Why and how do we use MRI to study cognitive development?

Before class, be sure to:
* Download (and extract) the following files from the OneDrive folder link (part1_dataset.zip and GSGData.zip). 
*	MRIcron and BrainVoyager EDU are installed on your machine. (Shoot Julie an email if you can’t get these working.)

Today's tutorial has two parts:
* Part 1: Finding clues from structural scans
* Part 2: Structural MRI preprocessing

### part 1: finding clues from structural scans

This segment of the tutorial assumes you have already downloaded and extracted the dataset from the OneDrive folder sent out and have installed MRIcron. 

| Scan(s) | Question(s) | 
| --------|-------------|
| `subj01_T1w.nii.gz` | <ul><li> What do you notice about the scan?</li><li> What do you think is the age of the participant?</li> |
| `subj02a_T1w.nii.gz`<br>`subj02b_T1w.nii.gz` | <ul><li> Both scans come from the same participant. What's the difference?</li> |
| `subj02a_T1w.nii.gz`<br>`subj03_T1w.nii.gz`<br>`subj04_T1w.nii.gz` | <ul><li> Order these participants by age. |
| `subj03_T1w.nii.gz`<br>`subj04_T1w.nii.gz` | <ul><li> Compare the quality of these two scans.</li>
| `subj05_T1w.nii.gz`<br>`subj05_T2w.nii.gz` | <ul><li> What's the difference between a T1w and a T2w scan?</li><li> What do you notice about this participant? Identify any relevant anatomical structures to your observations.</li> |

### part 2: structural MRI preprocessing

This segment of the tutorial assumes you have the BrainVoyager EDU tutorial dataset and have installed BrainVoyager EDU. 
  
1. Load the T1-weighted anatomical scan of the sample participant.
    * Open the program BrainVoyager EDU
    * Click `File` > `Open NIfTI`
    * Under the `GSGData` folder that you downloaded/extracted, open `GSGData/sub-01/ses-04/anat/sub-01_ses-04_acq-nondistorted_T1w.nii.gz`
2. Find out some info about the properties of this scan from the pop-up windows (NIfTI Header, sub-01_ses-04_acq-nondistorted_T1w.json windows). 
    * What is a NIfTI header and what is a JSON file?
    * How many slices were used to acquire this scan? Find two ways to identify this.  
    * What was the size of each voxel? 
    * What were the dimensions of each slice in voxels? 
 
