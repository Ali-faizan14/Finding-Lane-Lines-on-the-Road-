# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on my work in a written report

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 6 steps. First, I converted the images to grayscale, then I used the Gaussian blur function to smooth out the gray image. Next, I applied the canny edges function from OpenCV to obtain pixels at every location where is a sufficent color gradient. Before moving forward with the edges image, I created a mask to focus in on a polygon region within the image so as to separate the lane lines from the rest of image. Now in order to connect the pixels and form red lines, I used the Hough lines function to find the lines of best fit, extrapolate them, and then draw them onto the masked image. The final step was to overlay the mask and orignal image.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by calculating the slope of each line and then classifying it by either left or right. After getting the slopes, I averaged all the the x and y points for each side and used that and the slope to find the y-intercepts. After getting the y-intercepts, I obtained the extrapolated lines by choosing the y-coordinate and solving for the x-coordinate using the slope and intercept. I choose the values of (3/5 * height of the image) as the top of line and the full (height of the image) to get the bottom point of each line.


### 2. Identify potential shortcomings with your current pipeline

The shortcomings of my pipeline are that the extrapolated high and low point of each line cannot vary. So images or videos where you can see the hood of the car or where the road is quickly turning will not give a fitted lane line. Another issue is that the parameters of canny edge detection and hough lines work very well for straight lane images but don't work so well for lanes that are changing direction. 

Finally the last issue I had was with lane lines that had small lane markers that produced zero slope lines. My pipeline was not able to take these into account, but if it had it would have produced better fitted lines.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to implement hough line parameters and constrictions of the slope so that if lane are changing direction, a lane detection could still take place for a short distance.
