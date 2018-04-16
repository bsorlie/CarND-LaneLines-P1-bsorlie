# **Finding Lane Lines on the Road** 

## Ben Sorlie 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./image1.jpg "Grayscale"
[image2]: ./image2.jpg "Blur"
[image3]: ./image3.jpg "Edge"
[image4]: ./image4.jpg "Masked Edges"
[image5]: ./image5.jpg "Masked Image"
[image6]: ./image6.jpg "Lines Drawn"
[image7]: ./image7.png "Crack Example"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. 

1. Convert to grayscale

![alt text][image1]

2. Apply smoothing using Gaussian blur

![alt text][image2]

3. Perform the canny function to locate edges

![alt text][image3]

4. Apply Region mask to where lanes are expected (The Masked Unchanged Image is shown for reference on the right)

![alt text][image4]
![alt text][image5]

5. Perform a Hough Transform to extract the lines in the image and highlight them

![alt text][image6]

#### Details 

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by finding the average slope and intersection of all lines with slopes within an expected threshold. 

Negative Slopes between -0.8 and -0.3 were considered right lane boundaries while positive slopes between .3 and 0.8 were considered left lane boundaries.

To prevent noise in the middle of the road from being classified as a lane line. The region mask was modified to not include the center of the road.

### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when turning at sharp angles or if the camera pointing was skewed. In this case the region mask and slope thresholds used may no longer apply.

Another shortcoming is that high frequency noise in the images caused by cracks or tire tracks in the road can be detected as lane lines.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to add a moving average or other filter on the slopes between frames. This would help to prevent noise such as tire tracks or cracks in the road.

Another potential improvement could be to create a mask that is adaptive to curvature of the lanes and pointing/offset of the camera. This could be done using a longer moving average initialized to the preset mask.

Another improvement would be to track only thick lines. An example of where this is an issue is shown if the image below.

![alt text][image7]

This issue could be solved by detecting parallel gradient lines within a given separation threshold. This would detect where the image transitions from dark to light and back with a preset value. This would filter out thin lines or single transitions.

