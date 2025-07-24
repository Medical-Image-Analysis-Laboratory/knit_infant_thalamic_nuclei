--------------------------------------------------------------------------------------------------------------------------
Thalamic clusters creation
--------------------------------------------------------------------------------------------------------------------------

1- A parcellation of the different brain ROIs and a thalamus mask must exist for each subject (i.e both in native subject space)

The parcellation in subject space can be created for e.g. with ITK-Snap by running a registration between the anatomical image (e.g. T2-w) and the corresponding average_bold

2- Run the script *run_fc.py* to get the functional connectivity (FC) between each thalamic voxel and the ROIs (40 cortical and sub-cortical regions in the case of our work) for all subjects that are present in the folder path root_dir

This step is the most time consuming and takes time (~100 min) per subject in a local computer (if a parcellation has less ROIs, it will of course take proportionally less time)

3- Create a population average of the thalamus (i.e. a “new” template) in which the FCs of each subject (output of step 2): 
(i) should be aligned with (use registration from ITK-Snap for example)
(ii) this new template creation can be performed by running the script *tasks.py* and putting avgFCtoGetPopulationFCtemplate to True, this will output both the average FC map (average_fc_map.nii.gz) and a corresponding thalamus mask (average_fc_map_mask.nii.gz) to be used in the next steps.

4- Run the script *tasks.py* by putting AvgSubjectsFC to True to get an average of the functional connectivity of the different subjects (put into average thalamus template from step 3) present in the path root_dir 

5- Run the script *generate_clusters.py* to create the thalamic clusters by choosing the number of clusters - Once they are generated, they can be visualized in ITK-Snap by loading them as a segmentation map (on top of the average average_fc_map.nii.gz generated in step 3 for example). 


--------------------------------------------------------------------------------------------------------------------------
Thalamic clusters analysis
--------------------------------------------------------------------------------------------------------------------------

6- To analyze the cluster profiles, run the script *cluster_analysis.py*. After providing the FC maps average generated in step 4, and the clusters generated in step 5. This script creates average connectivity profiles for each cluster across the different ROIs, including z-scored FCs.
