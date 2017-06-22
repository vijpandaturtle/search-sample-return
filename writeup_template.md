## Project: Search and Sample Return

**The goals / steps of this project are the following:**  

**Training / Calibration**  

* Download the simulator and take data in "Training Mode"
* Test out the functions in the Jupyter Notebook provided
* Add functions to detect obstacles and samples of interest (golden rocks)
* Fill in the `process_image()` function with the appropriate image processing steps (perspective transform, color threshold etc.) to get from raw images to a map.  The `output_image` you create in this step should demonstrate that your mapping pipeline works.
* Use `moviepy` to process the images in your saved dataset with the `process_image()` function.  Include the video you produce as part of your submission.

**Autonomous Navigation / Mapping**

* Fill in the `perception_step()` function within the `perception.py` script with the appropriate image processing functions to create a map and update `Rover()` data (similar to what you did with `process_image()` in the notebook).
* Fill in the `decision_step()` function within the `decision.py` script with conditional statements that take into consideration the outputs of the `perception_step()` in deciding how to issue throttle, brake and steering commands.
* Iterate on your perception and decision function until your rover does a reasonable (need to define metric) job of navigating and mapping.  

[//]: # (Image References)

[image1]: ./misc/rover_image.jpg
[image2]: ./calibration_images/example_grid1.jpg
[image3]: ./calibration_images/example_rock1.jpg

## [Rubric](https://review.udacity.com/#!/rubrics/916/view) Points
### Here I will consider the rubric points individually and describe how I addressed each point in my implementation.  

---
### Writeup / README

#### 1. Provide a Writeup / README that includes all the rubric points and how you addressed each one.  You can submit your writeup as markdown or pdf.  

You're reading it!

### Notebook Analysis

#### 1. Run the functions provided in the notebook on test images (first with the test data provided, next on data you have recorded). Add/modify functions to allow for color selection of obstacles and rock samples.
I addressed the point as per the instructions given for the notebook. As far as the color modification functions are concerned, in addition to the existing color thresholding function I created a custom function using openCV for detecting the rock samples and obstacles as it is a better alternative when you have upper and lower thresholds for specific colors.

![alt text][image1]

#### 1. Populate the `process_image()` function with the appropriate analysis steps to map pixels identifying navigable terrain, obstacles and rock samples into a worldmap.  Run `process_image()` on your test data using the `moviepy` functions provided to create video output of your result.
I followed the steps given in the notebook to complete the process_image() function. I also used the existing and new functions I implemented for color thresholding. Finally I ran the same function on new testing data.

![alt text][image2]
### Autonomous Navigation and Mapping

#### 1. Fill in the `perception_step()` (at the bottom of the `perception.py` script) and `decision_step()` (in `decision.py`) functions in the autonomous mapping scripts and an explanation is provided in the writeup of how and why these functions were modified as they were.
The code used in perception_step() is not very different from the code I implemented in process_image() in the jupyter notebook, with the exception of the rover update step. In the jupyter notebook I simply updated the state of data stored in a csv file, whereas here I updated the variable states of the class Rover that maintains all states and parameters that are essential for the rover to function.
Also, the perception_step() function, I changed the following commands to

```python
 Rover.worldmap[obstacle_y_world, obstacle_x_world, 0] = 255
 Rover.worldmap[rock_y_world, rock_x_world, 1] = 255
 Rover.worldmap[terrain_y_world, terrain_x_world, 2] = 255
 ```
 from
 ```python
  Rover.worldmap[obstacle_y_world, obstacle_x_world, 0] += 1
  Rover.worldmap[rock_y_world, rock_x_world, 1] += 1
  Rover.worldmap[terrain_y_world, terrain_x_world, 2] += 1
 ```
for visiblity purposes.

That's all for perception_step(). In the decision_step() function, I introduced a new instance variable of the Rover class called stop_time. This variable
was introduced to prevent the rover from turning continously, which means it will decide the actuation of the rover when it is in go_forward mode.


#### 2. Launching in autonomous mode your rover can navigate and map autonomously.  Explain your results and how you might improve them in your writeup.  

**Note: running the simulator with different choices of resolution and graphics quality may produce different results, particularly on different machines!  Make a note of your simulator settings (resolution and graphics quality set on launch) and frames per second (FPS output to terminal by `drive_rover.py`) in your writeup when you submit the project so your reviewer can reproduce your results.**




![alt text][image3]
