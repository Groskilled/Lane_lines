# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I added some blur using numpy.gaussian_blur to remove some lines that were found but did not interest us. Next step is using the cany edge detection to find the lines in the image and after that I put a mask of a region of interest on the image (it looks like a triangle formed by both corner at the bottom and the middle of the image). To find points in the lines I used a hough transformation and some parameter tuning. 

In order to draw a single line on the left and right lanes, I splitted the image. The down half is were we can find the lines and the left part is obviously for the left line. I then find every point which belongs to a lane and then I try to find the best line to fit it using numpy.polyfit. Now that I have the equation of both lines, I extrapolate that to find points with high = 340 and 540 (I used y = ax + b -> x = (y-b)/y with y being 340 or 540). And then, all I have to do is draw lines on the image.

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when I cant find a line (it happened in some video and I had to reduce the threshold in the hough_lines function).

Another shortcoming could be when lines are curves. Since I am looking for lines it goes crazy.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to use a 2nd degree polynomial so it can find curves.

Another potential improvement could be to find better parameters for the hough and cany functions or decrease the thresholds when not enough points are found for the lines.
