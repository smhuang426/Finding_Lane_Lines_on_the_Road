# **Finding Lane Lines on the Road** 

[//]: # (Image References)
[image1]: ./examples/gray.png "Grayscale"
[image2]: ./examples/blur.png "Blur"
[image3]: ./examples/canny.png "Canny"
[image4]: ./examples/ROI.png "ROI"
[image5]: ./examples/hough.png "Hough Transform"
[image6]: ./examples/result.png "Outcome"

## Writeup

### 1. Describe pipeline

* My pipeline consisted of 5 steps.

1. Transform color RGB to gray scale image:

![alt text][image1]

2. Blur gray scale image so that remove some noise:

![alt text][image2]

3. Use canny edge detection, and edge will left on the image:

![alt text][image3]

4. Choose ROI we want, remove other part we don't care:

![alt text][image4]

5. Use hough transformation to fine lines, and pick lines we want via its slope:

![alt text][image5]

After above 5 step, we can get this result as below image

![alt text][image6]



* In order to draw a single line on the left and right lanes, I modified the draw_lines() function.

1. I use np.polyfit( x_points, y_points, 1 ) to find polynomial with 1 order ( y = mx + b ) .
  m is slope and b is bias, so that I can get slope directly and divide those line into right and left.

2. After append those polynomials, I average them from right_lines and left_lines variables, so that there are two line left, right line and left line

3. I create filter_1D() method to make the line move smoother with x = beta * x + ( 1 - beta ) * current_value, and set beta as 0.875.
  Besides, I do bias correction with beta = beta * ( 1~100% ), so that beta will increase gradually by time.


### 2. The potential shortcomings with current pipeline


One potential shortcoming would be what would happen when I test challenge video, the line is still shaking but it is smoother. I believe if the front car is closer, it will be worse


### 3. The possible improvements to this pipeline

A possible improvement would be to do more adaptive function so that this pipeline can fit more case.
And maybe I can add color detection to avoid light disturbance.
