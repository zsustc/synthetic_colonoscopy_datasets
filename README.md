# synthetic_colonoscopy_datasets
this repository contains brief introdcution of simulated data for colon 3D reconstruction and the dataset download link

This dataset contains 4 cases of simulated colonoscopic images with ground truth of camera poses and images depths for the simulation experiemnts.
Also, this dataset also contains the 10 groups of synthetic colonoscopic images with ground truth of depth images for training and testing the depth estimation network.

In each folder named Case#, its subfolder "rgb" contains the images and the subfolder "depth_gt" constains the ground turth of depth images. 
And "groundTruth_pose" in mat file is the camera poses, the optical center of the first frame camera is used as the origin point of the global space.

The dataset was collectd when the camera was moved in a normal motion simillar to a normal colonosacopy procedure and the camera calibration parameters for this folder of images: fx = 1.550029785575049e+02; % unit in pixel fy = 1.550029785575049e+02; cx = 120.0; cy = 160.0;

datasetlink: https://studentutsedu-my.sharepoint.com/:f:/g/personal/shuai_zhang_alumni_uts_edu_au/EnbBHlnZNoZLkU__FfAGHSMBwUrqfP_N-vWNFPKk4kMO2A?e=biKv7y

If you use the developed simulator and datasets in your papers, please cite our paper named "3D Reconstruction of Deformable Colon Structures based on Preoperative Model and Deep Neural Network", thank you very much!


For the usgae of related parameters in the developed simulator:
The example to obtain camera intrinsic parameters, camera extrinsic parameters and point cloud of one frame:

focal_length = 4.969783; 

sensor_width = 10.26; 

sensor_height = 7.695;

cols = 320; % image width

rows = 240; % image height

fx = focal_length * cols / sensor_width; % unit in pixel

fy = focal_length * rows / sensor_height;

cx = cols/2.0;

cy = rows/2.0;

img_rgb = cell(1,num);

depth_exr = cell(1,num);

for i = 1:num

    img_rgb{i} = imread(['path\SUK_L',num2str(i,'%05d'),'.png']);
    
    depth_exr{i} = exrread(['path\SUK_L_depth',num2str(i,'%05d'),'.exr']);
    
end

scan_gt = cell(1,num);

**depth_scale = 5.0;**

for i = 1:num

    xyzPoints = zeros(rows, cols, 3);
    
    for v = 1:rows % rows
    
        for u = 1:cols % cols
        
            d = depth_exr{i}(v,u,1);
            
            if d == 0
            
                continue;
                
            end
            
            depth_pixel = depth_scale * double(d);
            
            xyzPoints(v,u,3) = depth_pixel;
            
            xyzPoints(v,u,1) = (u - cx)*depth_pixel/fx; % x coordinates
            
            xyzPoints(v,u,2) = (v - cy)*depth_pixel/fy; % y coordinates
            
        end
        
    end
    
    ptCloudOut = pointCloud(xyzPoints, 'Color', img_rgb{i});
    
    scan_gt{i} = ptCloudOut; 
    
end


**% transform quaternion from the unity left handed space to matlab right handed space**

% y direction is opposite 

% [q0, q1, q2, q3]-->[q0, -q1, q2, -q3] under y direction is opposite

unity:

quat = [q0, q1, q2, q3];

quat(2) = quat(2)*(-1);

quat(4) = quat(4)*(-1);

rotm = quat2rotm(quat);

**% tranform translation from unity left handed space to matlab right handed space**

% [x,-y,z]-->[x,y,z] under x direction is opposite

transt = [x,y,z]

transt(2) = transt(2) * (-1);

**% "rotm" is the camera's pose in the world space, so rotm's transpose can transform the camera's**

**% scan back to its original pose in the world space**

grdth = [**rotm'**, zeros(3,1); transt*10, 1]; % convert cm to mm, the colon model is in mm unit

pose = affine3d(grdth); %pose format in matlab, it transforms the local point cloud into the global colon model space

