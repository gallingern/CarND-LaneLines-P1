# **Finding Lane Lines on the Road** 

## Writeup

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of the following steps:
* Grayscale
* Gaussian Blur
* Canny Edge Detection
* Vertex Assignment
* Region of Interest Masking
* Dilate Edges
* Hough Lines Detection
* Lines Extrapolation
* Drawing Region of interest bounding box
* Combining the Lines image with the original image

---

In order to draw a single line on the left and right lanes, I modified the draw_lines() function:
* y = mx + b
* m = (y2-y1)/(x2-x1)
* Filter line segments by slope above and below a tuned threshold
    * Right lines, slope > 0.5
    * Left lines, slope < -0.5
* Average all of the slopes (m)
* Assume upper and lower y value based on region of interest:
    * Calculate and average intercept (b)
    * Calculate x value using average slope and intercept
    
---

Challenge video:

* The challenge video initially didn't work because the video resolution was different
* I had defined my region of interest with hard coded pixel coordinates
* I solved this by defining the region of interest with dynamic percentages so it works for multiple resolutions

---

In the test image section of the notebook file, I broke each section of the pipeline into its own block and displayed the resulting image.  This made it much easier to debug errors and tune individual parameters.  See notebook file for more details on each step.


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be that the region of interest is limited to the cone in the middle of the screen.  For instance if the car changes lanes or there is a sharp turn, the lane lines won't be detected.

Another shortcoming could be that I didn't focus on making the code very efficient, this could cause the algorithms to be too slow to be useful.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to use a more sophisticated algorithm that can detect curving lines.  Also it might be possible to save the line from the last frame and compare it to the current result, they should only vary by a small margin.  The speed of the vehicle and frames/second could also be used to extrapolate this margin.

Another potential improvement could be to use C instead of python and really focus on algorithm efficiency to speed up computation.
