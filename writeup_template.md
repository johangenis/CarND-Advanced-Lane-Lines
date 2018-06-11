## Project Read Me

### Advanced Lane Finding Project.

---

**The goals / steps of this project are the following:**

* Compute the camera calibration matrix and distortion coefficients given a set of chessboard images.
* Apply a distortion correction to raw images.
* Use color transforms, gradients, etc., to create a thresholded binary image.
* Apply a perspective transform to rectify binary image ("birds-eye view").
* Detect lane pixels and fit to find the lane boundary.
* Determine the curvature of the lane and vehicle position with respect to center.
* Warp the detected lane boundaries back onto the original image.
* Output visual display of the lane boundaries and numerical estimation of lane curvature and vehicle position.

[//]: # (Image References)

[image1]: ./distortedUndistorted.png "Distorted / Undistorted"
[image2]: ./test_images/test1.jpg "Road Transformed"
[image3]: ./binaryImages.png "Binary Examples"
[image4]: ./examples/warped_straight_lines.jpg "Warp Example"
[image5]: ./poliFit.png "Fit Visual"
[image6]: ./plottedBackOnOrig.png "Output"
[video1]: ./project_video_output.mp4 "Video"

## [Rubric](https://review.udacity.com/#!/rubrics/571/view) Points

### Here I will consider the rubric points individually and describe how I addressed each point in my implementation.  

---

### Writeup / README

#### 1. You're reading it!

### Camera Calibration

#### 1. Briefly state how you computed the camera matrix and distortion coefficients. Provide an example of a distortion corrected calibration image.

The code for this step is contained in the first code cell of the IPython notebook located in "./Advanced-Lane-Lines-P4.ipynb".  

I start by preparing "object points", which will be the (x, y, z) coordinates of the chessboard corners in the world. Here I am assuming the chessboard is fixed on the (x, y) plane at z=0, such that the object points are the same for each calibration image.  Thus, `objp` is just a replicated array of coordinates, and `objpoints` will be appended with a copy of it every time I successfully detect all chessboard corners in a test image.  `imgpoints` will be appended with the (x, y) pixel position of each of the corners in the image plane with each successful chessboard detection.  

I then used the output `objpoints` and `imgpoints` to compute the camera calibration and distortion coefficients using the `cv2.calibrateCamera()` function.  I applied this distortion correction to the test image using the `cv2.undistort()` function and obtained this result: 

![alt text][image1]

### Pipeline (single images)

#### 1. Provide an example of a distortion-corrected image.

To demonstrate this step, I will describe how I apply the distortion correction to one of the test images like this one:
![alt text][image2]

#### 2. I used a combination of color and gradient thresholds to generate a binary image (thresholding steps at heading 4. Detect lane pixels and fit to find the lane boundary).  Here's an example of my output for this step.  (note: this is not actually from one of the test images)

![alt text][image3]

#### 3. The code for my perspective transform includes a function called `unwarp()`, which appears at heading 3. Apply a perspective transform to rectify binary image ("birds-eye view"). of the IPython notebook).  The `unwarp()` function takes as inputs an image (`img`), as well as source (`src`) and destination (`dst`) points.  I chose the hardcode the source and destination points in the following manner:

I hardcoded the following source and destination points:

| Source        | Destination   | 
|:-------------:|:-------------:| 
| 585, 460      | 320, 0        | 
| 203, 720      | 320, 720      |
| 1127, 720     | 960, 720      |
| 695, 460      | 960, 0        |

I verified that my perspective transform was working as expected by drawing the `src` and `dst` points onto a test image and its warped counterpart to verify that the lines appear parallel in the warped image.

![alt text][image4]

#### 4. Then I defined a method to fit a polynomial to binary image with lines extracted, using sliding window. The code can be found at heading 5.3 Sliding Window Polyfit - defined and visualized of the accompanying Advanced-Lane-Lines-P4.ipynb notebook.

![alt text][image5]

#### 5. I calculated the radius of curvature of the lane and the position of the vehicle with respect to center at 6. Determine the curvature of the lane and vehicle position with respect to center.¶

#### 6. I plotted my result back down onto the road such that the lane area is identified clearly, and I implemented this step at heading 7.Warp the detected lane boundaries back onto the original image, in the Advanced-Lane-Lines-P4.ipynb notebook.  Here is an example of my result on a test image:

![alt text][image6]

---

### Pipeline (video)

#### 1. Here's a [link to my video result](./project_video_output.mp4)

---

### Discussion

#### 1. My pipeline fails in highly contrasting conditions, like heavy shadows (as in the two challenge videos). Should I have time and persue this project further, I will look into Canny Edge detection and refining Sobel.
