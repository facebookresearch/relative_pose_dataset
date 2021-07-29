# Relative pose problem dataset
We release a dataset that we have generated from the publicly available TUM benchmark (Sturm et al. [1]) to evaluate relative pose estimators and therefore facilitate the comparison
against future solutions for the relative pose problem. To this purpose, we use six recordings from TUM benchmark – two from each different Freiburg Kinect
sensor. We run the publicly avaiable SLAM system ORB-Slam (Mur-Artal et al. [2]) in every recording and we store the keyframe-to-frame bearing correspondences that it produces into text files.
The corresponding ground-truth 6 DoF pose from keyframe-to-frame is also provided for quantitative evaluation. We also
generate the same feature correspondences but without noise to facilitate the debugging when first using this dataset. We produce the noiseless correspondences
by projecting the 3D map points associated to those correspondences into the keyframe and the frame. We subsample the dataset to have an affordable number of
keyframe-to-frame pairs per recording, resulting in around 300 pairs per recording on average. 

-----------------------------------------------------------------------------------------------------------------------------------------------------------

## The format for the dataset is as follows: 

 1. For each recording, we store the data in a different folder ("dataset_name/...").
 2. Every keyframe-to-frame pair receives an ID starting from 1 and in consecutive order.
 3. Feature correspondences are stored as normalized bearing vectors in "dataset_name/feature_ID.txt" files. See the format of this file below. 
 4. Similarly, noiseless feature correspondences are stored as normalized bearing vectors in "dataset_name/featureGT_ID.txt" files. See the format of this file below. 
 5. Ground-truth 6 DoF poses from keyframe-to-frame are stored as a 4x4 homogeneous matrix "T_Cam1_Cam2" in "dataset_name/gtPose_ID.txt" files.
 Where the pose is defined as follows pointInCam2 = T_Cam1_Cam2 * pointInCam1.
 
-----------------------------------------------------------------------------------------------------------------------------------------------------------
 
## The format of "dataset_name/feature_ID.txt" and "dataset_name/featureGT_ID.txt" files is as follows:
 
0.161141 0.195828 0.967308   // feature 1 cam 1

0.0830744 0.068574 0.994181  // feature 1 cam 2

0.0529926 0.206024 0.977111  // feature 2 cam 1

-0.02439  0.082315 0.996309  // feature 2 cam 2

0.419396  0.116196 0.900337  // feature 3 cam 1

0.339811 -0.01593 0.940359  // feature 3 cam 2
 
 
-----------------------------------------------------------------------------------------------------------------------------------------------------------

## How to use:
 
 1. Uncompress dataset from "relative_pose_dataset/relative_pose_dataset.zip".
 2. Read actual feature correspondences from a recording and a given ID (i.e., a keyframe-to-frame pair). For example for ID = 12: 
 "rgbd_dataset_freiburg1_desk2/feature_12.txt".
 3. Run your approach to compute "T_Cam1_Cam2_estimated" and compare this pose against the ground-truth keyframe-to-frame 6 DoF pose, which can be taken from  
 "rgbd_dataset_freiburg1_desk2/gtPose_12.txt". 
 4. You can double check that your script is correct by also using noiseless correspondences ("featureGT_12.txt"). In this case, you should expect an error
 close to 0 in step 3.
 
-----------------------------------------------------------------------------------------------------------------------------------------------------------
 
## If you use this dataset, please cite this paper: 
Instant Visual Odometry Initialization for Mobile AR (to do: add proper arxiv reference)

-----------------------------------------------------------------------------------------------------------------------------------------------------------

## License
Attribution-NonCommercial 4.0 International

-----------------------------------------------------------------------------------------------------------------------------------------------------------
## References:

[1] J. Sturm, N. Engelhard, F. Endres, W. Burgard, and D. Cremers. A benchmark for the evaluation of rgb-d slam systems. In 2012 IEEE/RSJ International 
Conference  on Intelligent Robots and Systems, pp. 573–580. IEEE, 2012.
[2] R.Mur-ArtalandJ.D.Tardos. Orb-slam2: An open-source slam system for monocular, stereo, and rgb-d cameras. IEEE Transactions on Robotics, 33(5):1255–1262, 
2017.


