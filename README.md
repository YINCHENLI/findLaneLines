# **Finding Lane Lines on the Road** 

### This is the first project of udacity self-driving nano degree

---

**Finding Lane Lines on the Road**

[//]: # (Image References)

[image1]: ./test_images_output/out_solidWhiteCurve.jpg "test image output"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I use caussian blur to blur the gray image. 
Third, I apply canny to image and cropped the part that should be draw. Fourth, I draw the hough lines. Lastly, I use weighted image function to make it semi-transparent.
```
def find_lanes_pipeline(image):

    gray_image = grayscale(image)
    
    kernel_size = 5
    blur_gray = cv2.GaussianBlur(gray_image,(kernel_size, kernel_size),0)

    cannyed_image = canny(gray_image, 100, 200)

    shape = image.shape

    vertices = [(0, shape[0]),(450, 325),(500, 325),[shape[1], shape[0]]]

    cropped_image = region_of_interest(cannyed_image, np.array([vertices], np.int32))
    
    line_image = hough_lines(cropped_image, 1, np.pi / 180, 20, 20, 150)

    weighted_image = weighted_img(line_image, image)

    return weighted_image
```

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by finding the slope and intercept, and draw a straight line between the two points to the bottom and the 60% upper part of the picture.


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
