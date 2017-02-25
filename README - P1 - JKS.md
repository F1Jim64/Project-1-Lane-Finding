#**Finding Lane Lines on the Road** 
 


The goals / steps of this project are the following:

Make a pipeline that finds lane lines on the road
Reflect on your work in a written report
Reflection

1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 6 steps. 

1. Read the images into my pipeline from the test images folder, (and save processed images with an "output" prefix. back into that folder)
2. Converted the images from color to grayscale
3. Ran a gaussian blur on the images, 
4. Ran the Canny Function to find edges
5. Then created a target area that narrowed the region of interest to just the lane area using a function that defined only the 4 points of the region of interest
6. Ran a Hough Line function to locate lines inside the region of interest - based on parameter set in Hough - such as line pixel length and width
7. For video processing - the same pipeline was used in the "process image function" - and it produced the White.mpeg video.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by creating a loop inside draw lines to process the (x1, y1, x2, y2) line coordinates provided by Hough line. You can use this loop to sort the lines into positive and negative slopes - and determine which are left and right lane lines. For each lane line (left and right) I used python arrays to store calculated slopes and x & y line coordinates. I then averaged the slopes and the x & y points - and used these values to find an average y intercept value. Once I had y intercept - I could then calulate the Xmin, Xmax and Y min, Y max for each lane line (left and right). The lanes lines were then drawn on the image using the CV2.line function.


2. Identify potential shortcomings with your current pipeline

One potential shortcoming would be what would happen when... the Hough Function can only find straight lane lines - so curved lane lines would be a problem

Another shortcoming could be if other cars or car body parts with straight lines came into the region of interest - the HoughLine function might detect those as lane lines. Houghline also seems to have issues with shorter lines - it would start picking up too many other lines unless you set the line length to a greater value.

3. Suggest possible improvements to your pipeline

A possible improvement would be to use more cameras and feed images from other angles - and then compare the images to see if the lines detected were lane lines - or something else

Another potential improvement could be to somehow move the region of interest based on the steering wheel angle so that it stayed focused on a curved lane as the road bends.