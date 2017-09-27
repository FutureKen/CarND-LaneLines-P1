# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/noise.jpg "Unstable frame"

---

### Reflection

### 1. Pipeline description. 

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I blurred the greyscaled img with gaussian_blur function. Second, I applied the canny edge detection function to get all the edges in the images. Third, I setted the mask edges that I only need for the lane detection. Fourth, I defined the parameters of the Hough transform and transformed the image into lines. At last, I drew the transformed lines onto the original image.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by the following steps.
1. I separated the left segments and right segments based on their slopes, basically, if the slope is less than 0, it belongs to the left line, if the slope is larger than 0, it belongs to the right line.
2. Calculate the average position and slopes for both lines.
3. We know that we can represent a line with "y=mx+b", we already have the x, y and m, we can calculate the value of b, so that we can calculate at which two points the left and right line are intersecting with the top and bottom masked edges.
4. Draw the left and right line on the original image.

If you'd like to include images to show how the pipeline works, here is how to include an image: 

### 2. Potential shortcomings
There is some white horizontal mark on the left lane, it is the noise which affects the extrapolated result. Like the following frame shows.

![alt text][image1]

Another shortcoming is the masked edge I choose may not fit videos with different resolutions very well. 


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to combine process_image and process_image_challenge functions with one function, it requires some adjustments with some parameters.

Another potential improvement could be shrinking the slope value range which can discard some of the noisy marks on the road. Also some parameters for the canny edge detection and hough transform function can be further optimized.