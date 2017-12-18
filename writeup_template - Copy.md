## *Finding Lane Lines on the Road** 
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

[image1]: ./test_images_output/solidWhiteCurve.jpg_8_weighted_2.png

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image2]: ./test_images_output/solidWhiteCurve.jpg_1_original.png "Original"
[image3]: ./test_images_output/solidWhiteCurve.jpg_2_gray.png "Gray"
[image4]: ./test_images_output/solidWhiteCurve.jpg_3_gauss.png "Gaussian Blur"
[image5]: ./test_images_output/solidWhiteCurve.jpg_4_canny.png "Canny Edge Detection"
[image6]: ./test_images_output/solidWhiteCurve.jpg_4_roi.png "Region of interest"
[image7]: ./test_images_output/solidWhiteCurve.jpg_6_hough.png "Hough Lines"
[image8]: ./test_images_output/solidWhiteCurve.jpg_7_weighted.png "Hough Lines over Original"
[image9]: ./test_images_output/solidWhiteCurve.jpg_8_weighted2.png "Custom-drawn lines"






---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I .... 

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
