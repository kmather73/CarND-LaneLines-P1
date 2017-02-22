#**Finding Lane Lines on the Road** 


The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road


[//]: # (Image References)

[image1]: ./writeupImages/index1.png "Yellow and White"
[image2]: ./writeupImages/index2.png "Grayscale"
[image3]: ./writeupImages/index3.png "Blur"
[image4]: ./writeupImages/index4.png "Canny"
[image5]: ./writeupImages/index5.png "ROI"
[image6]: ./writeupImages/index6.png "Final lane lines"
---

### Reflection

###1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 4 steps. First, I segment the images only for the colours yellow and white. 

![][image1]

Then the segmented images is converted to grayscale and a gaussanin blur is applied.


![][image3]

Next canny edge detector is applied to find line segments in the image. 

![][image4]

Now we clip a the "main" center region of the image.

![][image5]

In order to draw a single line on the left and right lanes, we apply a hough transform on the image produced by the pipline which give a collection of points in hough space. Then we classify these point to either belong to the left line or the right line class. Once we have these two classes we then average each of the clusters to find approximate points in hough space which represent each of the left and right lane lines.

![][image6]



###2. Identify potential shortcomings with your current pipeline

One potential shortcoming would be that then we are tring to classify the points produced from the hough transform we only consider there to be two class's for each of the lines it might be better to use k-means with a (k > 2) to take into account bends in the road.

Another is that we just take a linear average of the hough space points where instead we should take a weighted average where each point in hough space has a weight proportional to its distance in images space from the bottom center of the image.

###3. Suggest possible improvements to your pipeline

A possible improvement would be to subdivate the image into horazontal segments find the left and right lanes in each of these semgment. Pick control points from each of the semgents then form a Bézier curve or a spline to get a better local approximation of the lane lines. This could be used to handle a curive in the road.
