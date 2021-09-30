## fMRI in development

### part 1: probe the functional data

1.	Load the functional data and find out some info about the scan through the pop-up dialogs. 
    *	❓ What’s the voxel resolution of this scan? 
    *	❓ How many slices were used to acquire each volume?
    *	❓ What was the matrix size?
    *	❓ How long between each consecutive volume (i.e., sampling rate)?
    *	❓ How many volumes (i.e., timepoints) were collected? What is that duration in minutes and seconds?
    *	❓ How does the dim field compare to the structural scan from last week? 
    *	❓ What file contains the slice timing information about the scan? Why is this important?
2.	Modify your view of the functional data.
    * ❓ Upon opening the functional file, what is the layout of the data? How does this relate to the scan parameters? (8x8 reflecting 64 slices)
    * Go to Options > Layout and Display Options and change the layout to show only one slice. Use the right and left arrow keys to scrub through the slices. 
    * ❓ What does intensity correspond to in this scan?
    * Adjust the brightness by going to Options > Contrast and Brightness. 
    * Look at the scan as a movie by going to Options > Time Course Movie and hitting play. 
    * ❓ What happens when you click the “First <-> Last” button? What does that tell you about the scan?
3.	Examine the experiment protocol file and voxel timecourse.
    *	Using a text editor, open the *.tsv file in the func folder from the GSGData folder. 
    *	❓ What do you think this file is used for?
    *	In the FMR Properties dialog, under Reference protocol (PRT) file, click Edit to bring up a colour map of the experimental conditions. Next, click anywhere within the brain on a slice. You should see a voxel highlighted by your click, and a pop-up window containing a timecourse. 
    *	❓ What’s the relationship between these two windows? 
    *	❓ What are the units of each axis in the timecourse window pop-up?
    *	❓ Instead of clicking a single point on the brain slice, what happens if you click and drag an area of the slice? (It should highlight more than one voxel.)
    *	❓ Find an example of low temporal drift using the ROI Signal Time Course tool. 

### part 2: preprocessing fMRI data

4. Apply slice time correction, motion correction, and temporal high-pass filtering to the functional data.
    * Go to Analysis > FMR Data Preprocessing, then press GO. Record the start time, and we will let it run while we answer the following questions.
    * ❓ What do the checked off processing steps do to the data?
        * Slice scan time correction
        * Motion detection
        * Temporal high-pass filtering
    * ❓ Why do you think the default does not include temporal or spatial smoothing? 
    * ❓ Where is the preprocessed data saved? How do you know from the filename what processing steps were carried out?
    * ❓	What does the 3D Motion Correction Parameters plot mean?
    * Look at the processed scan as a movie by going to Options > Time Course Movie and hitting play. 
    * ❓ What happens when you click the “First <-> Last” button? What does that tell you about the scan in comparison to the raw functional data?
    * ❓ How long did the three preprocessing steps take?

