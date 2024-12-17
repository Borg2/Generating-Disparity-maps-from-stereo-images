# Disparity Map Calculation using Block Matching and Dynamic Programming

## Overview
This project implements **stereo disparity estimation** using block matching techniques and dynamic programming in Python. Given a pair of stereo images (left and right), the code computes a disparity map, which represents pixel shifts between corresponding points in the two images.

The implementation supports two cost functions for block matching:
- **SAD (Sum of Absolute Differences)**
- **SSD (Sum of Squared Differences)**

The disparity map helps determine depth information in stereo vision systems.

---
## How It Works

### Disparity Computation Pipeline (Block Matching)
1. **Convert Images to Grayscale**:
   Both input images (left and right) are converted to grayscale for processing.

2. **Block Matching**:
   For each block (window) in the left image:
   - A search is performed in the corresponding region of the right image.
   - Matching is determined using SAD or SSD cost functions.

3. **Disparity Calculation**:
   The horizontal shift (disparity) between matching blocks is recorded for each pixel.

4. **Normalization**:
   The disparity map is normalized to the range [0, 255] for visualization.

### Dynamic Programming Approach
Dynamic programming is used to align rows of pixels from the left and right images and compute the disparity efficiently. The **cost matrix** is constructed row by row:

- **Recurrence Relation**:
   C(i, j) = min [C(i-1, j-1) +match_cost , C(i-1, j) + 1.0 , C(i, j-1) + 1.0 ]

   where:
   - \( C(i, j) \) is the cost at position \( (i, j) \) in the cost matrix.
   - \( \text{match\_cost} \) is the squared difference between pixel intensities: \( \frac{(I_{left}[i] - I_{right}[j])^2}{4} \).
   - Penalties \(+1.0\) are added for skips or mismatches.

5. **Backtracking**:
   The optimal alignment path is backtracked through the cost matrix to determine the disparity for each row.

6. **Normalization**:
   The disparity map is normalized for visualization.

---

## Equations Used

### Block Matching
- **Sum of Absolute Differences (SAD):**
   $\[
   SAD = \sum_{i,j} | I_{left}(i,j) - I_{right}(i,j) |
   \]$
- **Sum of Squared Differences (SSD):**
   $\[
   SSD = \sum_{i,j} ( I_{left}(i,j) - I_{right}(i,j) )^2
   \]$

### Dynamic Programming
- **Cost Matrix Recurrence**:

 C(i, j) =min ( C(i-1, j-1) + match_cost , C(i-1, j) + 1.0 ,  C(i, j-1) + 1.0)


- **Match Cost**:

   match_cost = (I_left[i] - I_right[j])^2 )/ 4

---

## Inputs
- **Stereo Images**: Two images (left and right) of the same scene, taken from slightly different viewpoints.
- **Block Size**: Size of the window (block) used for matching pixels.
- **Search Block Size**: Range for searching matching blocks in the right image.
- **Cost Function**: Choose between SAD or SSD.

---

## Outputs
- **Disparity Map**: A grayscale image representing horizontal pixel shifts.

---

### Libraries Used
- `OpenCV`: For image processing.
- `NumPy`: For matrix operations.
- `Matplotlib`: For visualization.


