# synthetic_colonoscopy_datasets
this repository contains brief introdcution of simulated data for colon 3D reconstruction and the dataset download link

This dataset contains 4 cases of simulated colonoscopic images with ground truth of camera poses and images depths for the simulation experiemnts.
Also, this dataset also contains the 10 groups of synthetic colonoscopic images with ground truth of depth images for training and testing the depth estimation network.

In each folder named Case#, its subfolder "rgb" contains the images and the subfolder "depth_gt" constains the ground turth of depth images. 
And "groundTruth_pose" in mat file is the camera poses, the optical center of the first frame camera is used as the origin point of the global space.

The dataset was collectd when the camera was moved in a normal motion simillar to a normal colonosacopy procedure and the camera calibration parameters for this folder of images: fx = 1.550029785575049e+02; % unit in pixel fy = 1.550029785575049e+02; cx = 120.0; cy = 160.0;

datasetlink: https://studentutsedu-my.sharepoint.com/:f:/g/personal/shuai_zhang_student_uts_edu_au/EnbBHlnZNoZLkU__FfAGHSMBwUrqfP_N-vWNFPKk4kMO2A?e=RwTrrW

If you use the developed simulator and datasets in your papers, please cite our paper named "3D Reconstruction of Deformable Colon Structures based on Preoperative Model and Deep Neural Network", thank you very much!
