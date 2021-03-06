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
    * ❓ In a T1-weighted scan, how do the intensities relate to tissue class?
2. Find out some info about the properties of this scan from the NIfTI Header pop-up window. 
    * ❓ What is a NIfTI header?
    * ❓ How many slices were used to acquire this scan? 
    * ❓ What was the matrix size (i.e., dimensions of each slice)?
    * ❓ What was the size of each voxel?  
3. Explore the impact of magnetic field inhomogeneities on a scan.
    * Use the shortcut Ctrl+T to enlarge the saggital view of the brain. Navigate through the scan until you're on slice x = 108.  
    * ❓ What are the intensity values at xyz = [108, 160, 102] and [108, 80, 70]? 
    * ❓ Why is it important to have similar intensity values within the same tissue class?
4. Correct the scan for field inhomogeneities. 
    * Navigate to `Volumes` > `Inhomogeneity Correction, V16 Tools...`
    * On the top right, click the `Go` button beside `Auto-IIHC` (IIHC: intensity inhomogeneity correction). This will do the following preprocessing steps:
        * Background cleaning (all intensities of voxels in the background are set to 0)
        * Brain extraction (brain segregated from head tissue)
        * White matter detection
        * Bias field estimation within white matter voxels
    * ❓ What are the intensity values at xyz = [108, 160, 102] and [108, 80, 70], and how do they compare to pre-correction values?
5. Look at other outputs from the Auto-IIHC in step 4.
    * ❓ Where are the processed files outputted/saved on your computer?
    * ❓ What is the *_BrainMask.vmr file? 
    * ❓ Which filename corresponds to the skullstripped inhomogeneity-corrected T1 scan?
6. Normalize the participant's brain to the MNI template space. 
    * Starting with the skullstripped scan, go to `Volumes` > `Normalize to MNI Template Space`
    * Hit `Go` to run the transformation from native to MNI space. 
    * ❓ Using a text editor (e.g., Notepad), open the output file `*_MNI_a12.trf`. What is the purpose of this file?
7. Check the alignment between the warped participant brain and the MNI template.
    * Go to `Volumes` > `3D Volume Tools` > `Full Dialog` (if you're in the minified window) > `Spatial Transf` and check off the `Show secondary VMR` option
    * ❓ Was the transformation to MNI space successful?

#### references
  
Scans for part 1 of the tutorial are from the following OpenNeuro datasets:
  * Trevor K. M. Day and Tara M. Madyastha and Peter Boord and Mary K. Askren and Thomas J. Montine and Thomas J. Grabowski (2019). ANT: Healthy aging and Parkinson's disease. OpenNeuro. [Dataset] 
  * Richardson, Hilary and Lisandrelli, Grace and Riobueno-Naylor, Alexa and Saxe, Rebecca (2019). MRI data of 3-12 year old children and adults during viewing of a short animated film. OpenNeuro. [Dataset] 
  * Aarthi Padmanabhana and Charles F. Geier and Sarah J. Ordaz and Theresa Teslovich and Beatriz Luna (2018). Developmental changes in brain function underlying the influence of reward processing on inhibitory control (Slot Reward). OpenNeuro. [Dataset]
  * Richardson, Hilary and Lisandrelli, Grace and Riobueno-Naylor, Alexa and Saxe, Rebecca (2019). MRI data of 3-12 year old children and adults during viewing of a short animated film. OpenNeuro. [Dataset] 
  * Thompson WH* and Nair R* and Oya H* and Esteban O and Shine JM and Petkov CI and Poldrack RA and Howard M and Adolphs Râ  and *equally contributing, â corresponding author (2021). Human es-fMRI Resource: Concurrent deep-brain stimulation and whole-brain functional MRI. OpenNeuro. [Dataset] doi: 10.18112/openneuro.ds002799.v1.0.4
