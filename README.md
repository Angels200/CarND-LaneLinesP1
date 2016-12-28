# CarND-LaneLinesP1
First Project SDC
Reflections
I've tryed two different ways to built two kind of pipelines : 1/RGB to Gray oriented pipeline 2/Color selection oriented pipeline.
Recall that each pipeline has to answer the following requirements : 1/annotate the raw lane lines (left and right). The result should be an output images or videos almost same as the line-segments-example.jpg 2/fully annotate the lane line (left and right). The result should be an output images or videos almost same as the P1_example
1/RGB to Gray oriented pipeline (findLaneLines_seglines.ipynb)
It contains the following steps : */load Imge or video */convert the loaded media from color space (RGB) to Gray. With 8-bits matrix, it makes the next steps easy to process the media */Apply ROI (region of interest) to keep only the region in front of driver which focuses only on the lane lines */Apply gaussian blur to smooth the pixels of the image */Apply canny edge detector */Apply hough transform to detect lines */Draw lines detected by hough transform */Add the drawn lines to the original image
Implementation details:
Need to tweak the bluring kernel, the canny edge thresholds and hough transform parameters (threshold, min line length ...)
Results :
Pros : Simple and easy to answer the first requirement (raw lane lines) Cons : */failed to answer the annotate the fully lane lines */failed to answer the challenge video with so many lines corresponding to trees, road horizontal lines sometimes, the guard rails ...
Enhancements : The dashed lines are rendred on video with a blinking effect.
2/Color selection oriented pipeline: (findLaneLines.ipynb)
It contains the following steps : */load Imge or video */Convert the color space from RGB to HSV */create a first image based on the white color selection from the original one */create a second image based on the yellow color selection from the original one */add white and yellow image */Apply ROI (region of interest) to keep only the region in front of driver which focuses only on the lane lines */Apply canny edge detector */Apply hough transform to detect lines */Draw lines detected by hough transform */Add the drawn lines to the original image with details focused mainly on the lines */Apply canny edge detector with better resolution */Apply hough transform to detect lines */Group left lane lines and right lane lines by slope or angle (negative are right and positive are left) */Average each group lines to obtain one line by group */Extrapolate each line by : */calculating its slope and intercept first. */calculating the intersection points with bottom and top of the ROI (region of interest) */Extend the line end points to intersection points */Draw the lane lines */Add the drawn lines to the original image
Implementation details:
Need to tweak the color selection interval, the bluring kernel, the canny edge thresholds and hough transform parameters (threshold, min line length ...), the ROI coordinates
Results :
Pros : Simple and easy to answer the first requirement (raw lane lines) and the second requirement Accurate when rendering the lines on the image Address the challenge video with accuracy
Enhancements : The dashed lines are rendred on video with a blinking effect.
