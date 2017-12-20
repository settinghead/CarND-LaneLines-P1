# **Finding Lane Lines on the Road**

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

[//]: # (Image References)

[solidWhiteCurve]: ./test_images_output/solidWhiteCurve.jpg "solidWhiteCurve"
[solidYellowCurve]: ./test_images_output/solidYellowCurve.jpg "solidYellowCurve"

---
![solidWhiteCurve][solidWhiteCurve]

![solidYellowCurve][solidYellowCurve]

### Reflection

### 1. Pipeline


My pipeline consisted of 6 steps:

1. Convert image to grayscale
2. Apply Gaussian smoothing
3. Apply Canny transform
4. Compute two lane lines within the confines of a trapezoidal region and draw the line with Hough transform
5. Maks the trapezoidal region onto the two lane Lines
6. Superimpose the two masked lane lines onto the original iamge

In order to draw a single line on the left and right lanes, I modified the draw_lines() to perform the following steps:

1. For each line segment, compute the slope for the segement
2. Categorize each segment as either "left", "right" or neither depending on whether slope is positive or negative and whether the segment falls roughly to the corresponding area of the image
3. Compute left and right lane lines with a heuristic where it finds two "extreme" end points in both the left and right segment groups such that the line that connects the two extreme points has the longest length
4. Extend the two resulting lane lines so that they both span the entire trapezoidal region

### 2. Potential shortcoming

1. The extrapolation heuristic can be finicky at times and can occasionally deviate from the actual lane by a small angle
2. The two lines can deviate further if part of the lane is curved

### 3. Suggest possible improvements to your pipeline

One area of improvement could be to use a clustering algorithm to find segements that belogn to the left lane and right lane

An improvement for locating lane lines could be to use regression algorithm to fit a straight line to a set of points (for example end points of all line segments)
