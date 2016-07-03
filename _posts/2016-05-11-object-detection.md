---
layout: post
title: "Object detection from an video input using Opencv2"
date: 2016-05-11
---

<h2>Introduction:</h2>
<p>
<br>
To track humans in a particular video input we need to first identify the objects in the video input.
<br><br>
The object_deteciton.py code does that for us, we feed camera usb id or location of the video to the code.
<br><br>
To run object detection : python object_detection.py
<br><br>
</p>
<h2>Basic Principle and working</h2>
<p>
<br><br>
We primarily perform background subraction and find suitable contours from the subtracted image.
<br><br>
The contours which we select are based on few thresholds and area conditions.
<br><br>
The data for the demo below was captured by me from my phone which is really shaky, so the thresholds I have fixed are for that particular video input.
<br><br>
You will have to estimate your values and feed it to the INI file.
<br>
</p>
<h2>Next step</h2>
<p>
<br><br>
We will train a model to classify the object detected. This will predict humans from the object detected.
<br><br>
I have saved all the conoturs detected in a folder named detection_data in the code. 
which will be be my training data for my model.
<br><br>
</p>

<h2>Important reference links</h2>
<p>
<a href="https://github.com/dvigneshwer/human_motion_detection">Github Repo</a>
<br><br>
<a href="https://youtu.be/SAVFV5eWIvk">Demo of object detection</a>
<br><br>
<a href="http://www.samontab.com/web/2014/06/installing-opencv-2-4-9-in-ubuntu-14-04-lts/">OpenCV2 Installation</a>
<br><br>
<a href ="http://www.pyimagesearch.com/2015/05/25/basic-motion-detection-and-tracking-with-python-and-opencv/">Reference</a>
</p>
