## fMRI in development

### part 1: probe the functional data

1.	Load the *.nii.gz file for the functional data and find some info about the scan through the pop-up dialogs. 
    *	❓ What’s the voxel resolution of this scan? 
    *	❓ How many slices were used to acquire each volume?
    *	❓ What was the matrix size?
    *	❓ How long between each consecutive volume (i.e., sampling rate)?
    *	❓ How many volumes (i.e., timepoints) were collected? What is that duration in minutes and seconds?
    *	❓ How does the dim field compare to the structural scan from last week? 
    *	❓ What file contains the slice timing information about the scan? Why is this important?
2.	Modify your view of the functional data.
    * ❓ Upon opening the functional file, what is the layout of the data? How does this relate to the scan parameters? (8x8 reflecting 64 slices)
    * Go to `Options` > `Layout and Display Options` and change the layout to show only one slice. Use the right and left arrow keys to scrub through the slices. 
    * ❓ What does intensity correspond to in this scan?
    * Adjust the brightness by going to `Options` > `Contrast and Brightness`. 
    * Look at the scan as a movie by going to `Options` > `Time Course Movie` and hitting play. 
    * ❓ What happens when you click the `First <-> Last` button? What does that tell you about the scan?
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
    * Go to `Analysis` > `FMR Data Preprocessing`, then press GO. Record the start time, and we will let it run while we answer the following questions.
    * ❓ What do the checked off processing steps do to the data?
        * Slice scan time correction
        * Motion detection
        * Temporal high-pass filtering
    * ❓ Why do you think the default does not include temporal or spatial smoothing? 
    * ❓ Where is the preprocessed data saved? How do you know from the filename what processing steps were carried out?
    * ❓	What does the 3D Motion Correction Parameters plot mean?
    * Look at the processed scan as a movie by going to `Options` > `Time Course Movie` and hitting play. 
    * ❓ What happens when you click the `First <-> Last` button? What does that tell you about the scan in comparison to the raw functional data?
    * ❓ How long did the three preprocessing steps take?

### part 3: transforming from functional to MNI space

5. Coregister the functional and anatomical (native space) data. 
    * Open the skullstripped, processed T1 *.vmr file. 
    * Select the functional data to be aligned. 
         * `Volumes` > `3D Volume Tools` > `Full Dialog` > `Coregistration`. 
         * Select the functional data by clicking `Select FMR…`
         * Choose the processed *.fmr file. 
    * ❓ What do you observe from the images that are shown on screen after opening the functional data? 
    * Click the Align button in the FMR-VMR coregistration field (where you selected the *.fmr file). 
    * Press Go to run the initial and final alignment processes. The initial alignment (IA) uses header information to orient the scans, then the fine-tuning alignment (FA) optimizes an affine transform matrix to rotate/translate/scale. 
    * ❓ How do you differentiate between these two transformations in the output *.trf files?
 6. Evaluate the coregistration
    * In the 3D Volume Tools box, under Target display options, choose the `Blend: Transparent` visualization option to see the functional data overlaid on the structural data. 
    * ❓ How does the coregistration look?
 7. Transform the functional data to the anatomical native, then MNI space.
    * Open the warped MNI-space anatomical scan.
    * Click `Analysis` > `Create Normalized VTC from FMR data`. In BrainVoyager, VTC stands for volume time course, which is a special format of the functional data. 
    * Load:
         * Preprocessed functional data from step 4.
         * .trf files for the initial and fine-tuned alignment steps
         * After clicking the `To MNI` radio button at the top of the window, load the native anatomical to MNI *.trf file from last class.
    * ❓ Which files did you put into each field?
    * Change the target resolution by clicking `Options` > `2x2x2` in Target resolution. 
    * ❓ What is the chain of transformations that is carried out on the functional data?
    * ❓ Click Go to start the transformation process. This generates a *.vtc file in the derivatives-functional folder which is the functional data in the MNI template space. 

### part 4: statistical analysis via general linear model (GLM)

8. Open and link the functional and anatomical scans
      * Open the MNI-space skullstripped anatomical scan
      * Click `Analysis` > `Link Volume Time Course (VTC) file…` and `Browse…` for the VTC file you just generated, then click OK. 
      * Verify that the linking has worked by right-clicking somewhere in the anatomical scan and selecting `Show ROI Time Course`. The functional data should pop up! 
9. Set up the design matrix for the GLM.
      * With the processed data file active (check the tab name), navigate to Analysis > General Linear Model: Single Study. 
      * Right-click on the colour bar associated with your first condition to define the first predictor. Click HRF to apply the HRF function to the boxcar and account for HRF delay. Repeat for each of the 6 conditions.
      * Click “Show all” in the predictors box to show the whole protocol. 
      * Save the matrix as FacesHousesDesignMatrix.sdm by pressing the ‘Save…’ button in the Single Study General Linear Model button. 
      * Open the design matrix file you just saved in a text editor. 
      * ❓ What are the dimensions of the design matrix? How do they relate to the predictors and time?
10. Run the GLM on your functional data.
      * Select `Analysis` > `General Linear Model: Single Study`
      * Load the FacesHousesDesignMatrix.sdm design matrix file that we generated in step 5. 
      * Click GO to run the GLM. 
11. Investigate the results of your GLM
      * A window titled Voxel Beta Plot pops up. ❓ What’s the meaning of the y- and x-axes?
      * Blue and red blobs are now overlaid on the anatomical scan. ❓ What is this plot showing? What are the values of the red to blue coloured voxels? 
      * ❓ When hovering over a red or blue voxel, what other info is shown in addition to the coordinates and anatomical scan intensity value?
      * Inspect a time course for a “hot” voxel. ❓ What do you notice about the time course?
      * Save the computed GLM by going to `Analysis` > `Overlay General Linear Model` > `Save .GLM`, and save it as FacesHouses_VTC.glm. 
      * Look at different contrasts by clicking the boxes beside each predictor and setting them to `+` or `-`. How do you think the contrasts correspond to what you set as `+` and `-`? 

### part 5: look at faces vs houses contrast

12.	Investigate Faces vs. Houses and find the peak voxel of a cluster.
      * Set all Face conditions to `+` and all House conditions to `-`, then click GO. 
      * ❓ What is the meaning of the new blob configuration on the anatomical scan? 
      * Go to `Volumes` > `Convert Map to VOIs`, select `Create VOI for each cluster`.
      * In the resulting pop-up dialog, click `Options` and switch to the `VOI Functions` tab. 
      * Click `Table…` under `VOI map peak voxels` to pull up a table containing peak MNI coordinates, as well as t- and p-values associated with the peak voxel. 
      * Click one of the cluster entries, then the Show Voxel button to move your crosshair to its location on the anatomical scan. 
      * Using MRIcron, look up the AAL regions associated with the peak MNI coordinates of each cluster. 
      * Using NeuroSynth, look up study associations for the peak MNI coordinates of a cluster. 

### part 6: effects of spatial smoothing
13.	Look into the effects of spatial smoothing. 
      *  Go to `Analysis` > `VTC Data Preprocessing`. 
      *  Set the Gaussian filter FWHM (full width half max) to 4. 
      * Repeat the GLM process and describe the impact of spatial smoothing.
      * Repeat for a FWHM smoothing filter of 8. 

### part 7: Do some event-related averaging
14. Event-related averaging
      * Go to `Analysis` > `Event-Related Averaging Specification`. 
      * Select all conditions by clicking/highlighting the condition names in the left panel. 
      * ❓ What happens when you increase the Pre and Post field values?
      * Click `Create AVG` and save the resulting .avg file.  
      * Find one of the peak cluster voxels. 
      * Right-click and click Show Time Course. 
      * Click anywhere in the window and click Show/Hide Options. 
      * Under Event-related averaging, `Browse…` to find the *.avg file we created, then click Enable. 
      * ❓ What is the plot showing?
