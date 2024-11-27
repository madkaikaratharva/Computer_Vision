# Metric Rectification and Robust Homography

## Overview

This repository implements computer vision techniques, including metric rectification, homography estimation using the Random Sample Consensus (RANSAC) algorithm, image warping with the homography matrix, and panoramic view generation using the computed homography.


## Image Wraping:

The objective was to map the template image onto the original image using the computed homography matrix. The backward interpolation method was implemented for this transformation.

![template image](outputs/template.png)

**Figure 1:** Template Image


![wraped image](outputs/image_warping.png)

**Figure 2:** Output after image wraping


## Metric Rectification:

Metric rectification involves eliminating projective and affine distortions from an image. The goal was to implement two metric rectification methods: the Two-Step (Stratified) approach and the One-Step approach.


![source image](outputs/original_door_img.png)

**Figure 3:** Source Image


### 1. Two step approach:

In this approach, projective distortion is removed by identifying the line at infinity. Once the homography matrix Hp is computed, backward interpolation is applied to obtain the affinely rectified image.

The second step eliminates affine distortion by determining Ha, which is derived from the dual of the conic at infinity. To compute this conic, at least two pairs of orthogonal lines are required to determine Ha.


![affinely rectified image](outputs/affinely_rectified.png)

**Figure 4:** Removal of Projective distortion. Affinely rectified image


![metric rectification](outputs/metric_rectified_stratified.png)

**Figure 5:** Removal of Affine distortion. Metric rectification


### 2. One step approach:

In this approach, the dual of the conic at infinity is used to remove both projective and affine distortions. At least five pairs of orthogonal lines are required. Singular Value Decomposition (SVD) is performed to compute the conic's parameters, enabling the derivation of the homography matrix (HaHp)

![metric rectification](outputs/metric_rectified_stratified.png)

**Figure 6:** Metric rectification using one step approach


## Robust Homography Estimation using RANSAC :

This section implements homography estimation using the RANSAC algorithm to address the presence of outliers. Outliers can cause inaccuracies and lead to incorrect solutions when computing the homography between image pairs. RANSAC mitigates misalignment caused by these outliers.

The Direct Linear Transform (DLT) algorithm was implemented from scratch to compute the homography matrix. RANSAC was then applied to identify the best possible solution, minimizing the symmetric transfer error.

Once the homography was computed, the images were stitched together to get a panaromic view.


![input images](outputs/images_to_be_stitched.png)

**Figure 7:** Input Images


![panaromic image](outputs/panaromic_output.png)

**Figure 8:** Panaromic View stitched together using computed homography