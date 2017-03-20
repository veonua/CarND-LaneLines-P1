#**Finding Lane Lines on the Road** 

##Writeup Template

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

---

### Reflection

###1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of several steps. First, I converted the images to YUV to be able to detect color lines easily (as I saw there are yellow line examples too), then filter out a triangle, as we assume that car goes forward (and it was in lesson), 
then I run historgam on brightness channel (Y), in order to improve contrast for different filming conditions I've run histogram eq. (clahe).
as lesson involves canny filter, I had to apply gaussian bluring and canny. then hough lines, which gave pretty decent results (like 30+ lines) extracted from sample image, I've played with parameters (blur level, canny, hough) and the best I came with is 15 lines per image. 

In order to draw a single line on the left and right lanes, I modified the draw_lines() function to split lines to positive and negative (left and right) slopes. Mean slope in each category is supposed to be true slope of the lane. Then I found two lines that have slope nearest to calculated mean slopes, and applied linear extrapolation. see extrapolate_line(slope, point) 


###2. Identify potential shortcomings with your current pipeline


It's pretty naive to rely on lanes to drive the car autonomously. And classic CV algorithms require a lot of fine-tuning to make things work in different conditions. So there is a short-list of issues in this code. 

* assumumption car goes forward, and there is no large curve on the road 
* assumumption there is no obstacles on the road, white car on the lane will ruin this pipeline
* hough lines works pretty bad, with canny it catches either one side of road marking or another, so lines jitter

as I understand we need canny only to make hough lines algorithm work little bit better.

###3. Suggest possible improvements to your pipeline

possible improvements... 

maybe left this code as an assistant with the small weight. and implement on more robust algorithms that would take into consideration obstacles, extract and track other objects from the video flow, 
may be apply couple of filters and use more sensors so it would use some kind of memory.

also it would be nice at least to extract bird-eye-view to find true curve of the road. 

