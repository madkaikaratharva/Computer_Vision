# Structure from Motion and Bundle Adjustment

## Overview :

This project involves 3D reconstruction using Structure from Motion (SfM), followed by bundle adjustment to minimize reprojection errors and enhance the quality of the reconstructed scene graph.

The reconstruction process includes three main steps:

### 1. Preprocessing and Setting up the graph scene

An initial image pair is selected, and 2D point correspondences between them are identified to construct the scene graph.


### 2. Incremental Structure from Motion

* Implement incremental Structure from Motion (SfM) by iteratively registering images.
* Select the image pair with the highest inlier correspondences from the scene graph to initialize SfM.
* Compute the essential matrix using the 5-point algorithm with RANSAC for robust estimation.
* Recover the relative pose of the second camera from the essential matrix and set its pose.
* Perform triangulation of inlier correspondences to reconstruct initial 3D scene points.
* Perform triangulation of inlier correspondences to reconstruct initial 3D scene points.


### 3. Bundle Adjustment

In bundle adjustment, the reprojection error is minimized with respect to the 3D scene points (X) and camera poses (R,t).
* It refines the estimated 3D structure and camera parameters to improve accuracy.
* The process ensures better alignment between projected 3D points and their corresponding 2D image features.
* Bundle adjustment enhances the consistency of the entire reconstruction pipeline.


## Setting Up :

If you are using Anaconda, you can run the following lines to setup:
```bash
conda create -n sfm python==3.7.6
conda activate sfm
pip  install -r requirements.txt
```

## Running Scripts
To run the scripts:
```bash
# performs preprocessing for temple dataset
python preprocess.py --dataset temple  

# performs preprocessing for mini-temple dataset
python preprocess.py --dataset mini-temple 

# performs structure from motion without bundle adjustment
python sfm.py --dataset temple 

# performs structure from motion with bundle adjustment on mini-temple dataset
python sfm.py --dataset mini-temple --ba

# performs structure from motion without bundle adjustment on mini-temple dataset
python sfm.py --dataset mini-temple 
```

To visualize, run:
```bash
# visualize 3d point cloud from reconstruction.
python visualize.py --dataset mini-temple
```

