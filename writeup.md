# **Finding Lane Lines on the Road**
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images_output/whiteCarLaneSwitch.jpg_1_original.png
[image2]: ./test_images_output/whiteCarLaneSwitch.jpg_2_gray.png
[image3]: ./test_images_output/whiteCarLaneSwitch.jpg_3_gauss.png
[image4]: ./test_images_output/whiteCarLaneSwitch.jpg_4_canny.png
[image5]: ./test_images_output/whiteCarLaneSwitch.jpg_5_roi.png
[image6]: ./test_images_output/whiteCarLaneSwitch.jpg_6_hough.png
[image7]: ./test_images_output/whiteCarLaneSwitch.jpg_7_weighted.png
[image8]: ./test_images_output/whiteCarLaneSwitch.jpg_8_weighted2.png

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

**Pipeline**

My pipeline consisted of 7 steps in total, including the final step of modifying the draw_lines function

![original][image1]

1.) Convert to grayscale
![grayscale][image2]

2.) Add a Gaussian blur with a kernel size of 5
![Gaussblur][image3]

3.) Use Canny's edge detection algorithm in OpenCV to give an image of traced-out objects (lane lines included!)
    The "low" and "high" parameters were 250 and 350, respectively
    These two values were high enough that extra "artifacts" in the road surfaces would be ignored, 
    but not so high that the lane lines would not be detected
![Canny][image4]

4.) Apply a region of interest mask to ignore everything but the lane lines
    Through some trial and error, I found that the vertices 
    
    (100,540)
    
    (450,325)
    
    (550,325) 
    
    (960,540)
    
gave the best view of the lane, ignoring cars and other peripheral objects
![roi][image5]

5.) Apply the Hough line transform with the following parameters
    
    rho = 2
    
    theta = pi/180
    
    threshold = 15
    
    min_line_length = 10
    
    max_line_gap = 10
    
   These parameters, like the region-of-interest vertices and the Canny parameters, were found through trial and error
    
![Hough][image6]

6.) Combine the Hough Lines with the original image to trace the lane lines
![Hough_traced][image7]

7.) Using my customized version of the draw_lines function to draw two solid lane lines
    To be explained in detail below
![Solid_lines][image8]

**Customizing the draw_lines function**

At the recommendation of the project documentation, I collected the slopes and average positions of the lines,
and used those values in extrapolating a lane line from the "midpoint" to the top and bottom of my region of interest

1.) Collecting positions and slopes
With the x and y values having been collected from the Hough lines helper function, it was simply a matter of doing some algebra to find the slope of each line.

With knowledge of the images in hand (i.e., that pixel values increased down and to the right), I grouped my lines by slope - with left lines having negative slope, and right lines having positive slope. I also took the liberty of excluding slope values that had an absolute value higher than 1 or lower than 1/2. Having looked at the various slope values of the Hough lines during debugging, it appeared that most of the line slopes had absolute values between 0.6 and 0.8. I also used the slope values to group my line positions either to the left or to the right.

2.) Using slopes and midpoints to extrapolate
I took the average slope and average position of the Hough lines on the left and right side, and used these values to extrapolate to the top and bottom of my region of interest. Again, I took advantage of some previous information (the pixel values of my ROI vertices) to aid the function in drawing the lane lines from top to bottom (since the ROI had y values ranging from 325 to 540, I knew to calculate the necessary x values using these y values and the slopes). 

### 2. Identify potential shortcomings with your current pipeline

- One shortcoming, having reflected upon the project, may come in that I used a lot of trial-and-error in coming up with parameters, and in customizing the draw_lines function. Now, while trial-and-error is not always bad, it may lead to difficulty in standardizing the pipeline for many different types of video input (a potentially hilarious example of this comes in my attempt on the challenge video)

- Not a shortcoming, but a slight imperfection to my execution comes in drawing the solid lines over the video "solidYellowLeft" - Though the lane lines do hover over the lane markings on the road for the most part, the drawn lines do show some "jitter" since the lines are drawn using positions and average slopes calculated for every frame of the video.

### 3. Suggest possible improvements to your pipeline

Possible improvements come in answering to the two potential shortcomings described above. If possible, to use more computation to optimize the input parameters in the pipeline. Of course, human intuition is a powerful tool, but it isn't always ideal to rely on intuition alone. And in regards to the "jitter" of the drawn lines, it may be useful to find better parameters for finding our Hough lines  so to reduce the amount of "noise" in our line_drawing calculations (possibly a smaller ROI, since most of the jitter seems to occur at the top of the line).
