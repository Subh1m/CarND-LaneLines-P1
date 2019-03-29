# **Finding Lane Lines on the Road** 

### Running Instructions:
`P1_LaneLines.ipynb` contains the full workflow.

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

### Output videos:
`test_videos_output` folder
1. solidWhiteRight.mp4
2. solidYellowLeft.mp4
3. challenge.mp4

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

#### Architecture Pipeline:

1. Read the image.
2. Convert image to grayscale
3. Apply Gaussian Blur with Kernel
4. Apply Canny function to detect edges by identifying hifh change in gradient.
5. Mask edges using region of interest.(Experiment Space to work on)
6. Apply Hough Transform on the masked edges.
7. Extrapolate disjoint line segments within draw_line() to gain a single line segment (1 each for both sides of the lane).
8. Combine the new line with the original image to find the accuracy.

##### NOTE: I have commented the plt.imshow() later in the function image_lane_lines after running it over the test images for a clean notebook. (Video output would have created undesired outputs)

#### draw_line() explanation:
##### Initial Iteration
1. In the beginning, I replicated the demo lecture quiz code into this pipeline to obtain the following image.
2. Following this step, I tried joining the lines using the following steps:

Approach 1:
1. First, found out the line equation, slope and intercept. 
2. Found out the score for line based on points given (Score here is the distance of point from line)

Approach 2a:
1. Found the slope and intercept for all given points.
2. Took mean of slope and intercept. (Optional video sometimes gives only one point for some frames, so filter created)
3. Found the intersection point between the 2 lines using slope and intercept.
4. Directly plotted the line using the formula mentionaed alongside the code.
5. These result was good but it gave me a triangle shape rather than two separate lines.


Approach 2b:
1. Follow Steps 1-3 from Approach 2a.
2. After doing some reading online, I found that the best way to separate 2 line segments is to mention threshold for both.
3. Running multiple iterations on the region of interest and points I found 0.97 to satisfy the bottom as it is close to the axis and 0.61 to satisfy the top as it is near mid of the image. Another reason for this step is to prevent the lines from jumping between the video.
4. Thus, using an ensemble to the Approach 2a slope, intercept and the new points, plotted the new extended line segments.
5. All these new customizations were to satisfy the Optional Video.


#### Architecture Challenges:
1. Finding the coordinates for the perfect region of interest took multiple iterations.
2. Had to change the region of interest from hard-coded values to image size as the videos are of different sizes.
3. Had to switch from Approach 1 to 2 due to complications and efficiency issues with the Optional Video for Approach 1.
4. Had to set threshold (deviation < mean.std) for slope as all values caused it create fluctuating lines in the videos.
5. The Optional video enabled me to create a null filter for slope as it occurs for some frames.
6. Finding the perfect range for the line segments took most of my time to satisfy the Optional Video.


### 2. Identify potential shortcomings with your current pipeline


#### Shortcomings:
1. The lines in the Optional Video are still not perfectly arranged and gets problematic during the tree shadow.
2. This approach won't work if the camera angle is kept other than the fron or back of the car as region of interest has been placed in reference to the center bottom of the image.


### 3. Suggest possible improvements to your pipeline

#### Improvements:
1. Using gradient to identify the lines much better.
2. Enhancing the image to increase the contrast difference which will help increasing the efficiency of line identification.
3. Using learning algorithm to auto-identify the correct slope, intercept instead of using hard-coded slopd intercept thresholds.

## LICENSE:
This project has been open-sourced basedon on MIT License. All Developers are free to use my code or make pull requests without any issue.
