# lane-detection-using-hough-transform
Lane Detection Project, using Hough Transform

<img src="laneLines_thirdPass.jpg" width="480" alt="Combined Image" />


# Finding Lane Lines on the Road 

When we drive, we use our eyes to decide where to go.  The lines on the road that show us where the lanes are act as our constant reference for where to steer the vehicle.  Naturally, one of the first things we would like to do in developing a self-driving car is to automatically detect lane lines using an algorithm.

In this project I detected lane lines in images using Python and OpenCV.  





## Pipeline

* I am first converting the color image (or a frame from a video) to a grayscale image. This enables us to work on a single channel of the image, instead of working on all 3 channels (BGR). So this is computationally less intensive
* Then I am applying Gaussian Blur to the image. I also tried Bilateral Filtering, since this filtering preserves edges better, compared to Gaussian Filter. However, I did not see a big advantage in this project, so I kept the Gaussian Filtering in my code to be consistent with given specifications.
* Then I applied Canny Edge detection on this smoothed image.
* To make this process more efficent, I used a small GUI tool. 
  Here's the demo of the tool: 
          https://youtu.be/xdiekchp-Uc
* On this Edge image, I filtered region of interest by applying a mask. Since we are primarily interested in edges in the region where we expect our road to be, I removed the edges in other areas of the image.
* Then I applied Hough Lines algorithm on this masked edge image. This gives us line segments where we have edges near the lane lines. 
* Once I get the lane line segments, I extrapolated the left lane line and right lane line, based on the angle.
* Since we are using Polar coordinates in Hough Transform, our left line will have negative slope and the right line will have positive slope. Based on this, I classify each line segment to be either a left line segment or a right line segment. Then I take average of all left line segments and draw an extrapolated left line. I apply same method for extrapolating the right line segment as well. To make the extrapolated lines more stable and less wobbly, I applied weighted sum of previous slope and current slope of each line. This allows smooth transitioning of the slope, so the outcome looks more stable.


## Video Output

#### Project Video:
Detecting White Lane Lines:  https://youtu.be/VXccUjr322A
<br />
Detecting Yellow Lane Lines:  https://youtu.be/t38wJ3V3Mi8
<br />
Challenge Video:  https://youtu.be/6eJAxwa-qDY
<br />: still pending to get a robust solution for it.


## Blog Post taken as reference:
https://blog.paperspace.com/understanding-hough-transform-lane-detection/
https://medium.com/@maunesh/finding-the-right-parameters-for-your-computer-vision-algorithm-d55643b6f954


