# **Finding Lane Lines on the Road** 


---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"
[gray_image]: ./test_images_output/gray_challenge.jpg "Grayscale"
[canny_image]: ./test_images_output/canny_challenge.jpg "Canny"
[reg_image]: ./test_images_output/reg_challenge.jpg "Region"
[final_image]: ./test_images_output/challenge.jpg "Final"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I ....

My pipeline consisted of the following five steps:

1. Grayscale
2. Gaussian Blur
3. Canny Edge Detection
4. Region Selection
5. Hough Transform

The grayscale process begins by applying a threshold filter to the image frame that prioritizes red and green brightness. The following grayscale conversion creates a black base image with white edges along the road lines as can be seen below.

![Grayscale lane image.][gray_image]

The canny edge detection then checks for large gradients across pixels to find the most distinct edges within the grayscale image as seen below.

![Canny edge lane image.][canny_image]

Region selection then removes most of the extraneous data from the image and focuses upon the current lane. It was necissary to use proportional values rather than exact to account for diferent sized frames. The new result can be seen below.

![Applicable image region.][reg_image]

Finally, a Hough tranform is applied to the image. These lines are then passed through the draw_lines() function in order to generate a single prediction line. In order to accomplish this the average slopes of the Hough lines are then calculated such that left and right lane lines can be diferentiated. An average slope and average point are then calculated for each side allowing a new final prediction to be created. Once this prediction is overlayed upon the original image the following is produced:

![Hough lined overlay image.][final_image]


### Potential Shortcomings.


As seen in the challenge test video the current algorithm has issues in very high contrast segments of the road. During large changes in light levels it is difficult for the edge detector to differentiate between lane lines and general lighting shifts.

Second, while viewing the video files it is easy to see the constantly shifting nature of the prediction lines, this could be somewhat problematic in a steering algorithm and would need to be filtered.

Finally, were another car to shift lanes in front of the camera the algorithm could have a great deal of trouble diferntiating it from the lane lines.


### 3. Possible Improvements

A straigtforward fix for the first issue would be to create separate filters for the white and yellow lines. This would allow for far more selective edge detection and possibly fix the contrast issue all together by looking for color rather than attempting to select out other colors.

The second could be solved by taking a running average of the previous set of hough lines. This would allow the system to have continuity between each frame.

Finally, either considering only the closest area of the current lane or separating the lane into segments may allow the algorithm to detect and account for cars blocking the camera view.
