# synthetic_colonoscopy_datasets
this repository contains brief introdcution of simulated data for colon 3D reconstruction and the dataset download link

This dataset contains 5 cases of simulated colonoscopic images with ground truth of camera poses and images depths.

In each folder named Case#, its subfolder "rgb" contains the images and the subfolder "depth_gt" constains the ground turth of depth images. 
And "groundTruth_pose" in mat file is the camera poses, the optical center of the first frame camera is used as the origin point of the global space.

In the folder named "dataset_with_normal_camera_motion", the dataset was collectd when the camera was moved in a normal motion simillar to a normal colonosacopy procedure and the camera calibration parameters for this folder of images: fx = 232.5044678; % unit in pixel fy = 232.5044678; cx = 240.0; cy = 320.0; baseline = 4.5; %unit in milimeter

datasetlink: https://studentutsedu-my.sharepoint.com/:f:/g/personal/13026366_student_uts_edu_au/EnbBHlnZNoZLkU__FfAGHSMB1kxXrwXhHdQUY2ZbaU0_xQ?e=GEaTle
