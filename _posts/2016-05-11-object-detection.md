---
layout: post
title: "Object detection from an video input using Opencv2"
date: 2016-05-11
---

#Introduction:

To track humans in a particular video input we need to first identify the objects in the video input.

The object_deteciton.py code does that for us, we feed camera usb id or location of the video to the code.

To run object detection : python object_detection.py

#Basic Principle and working:

We primarily perform background subraction and find suitable contours from the subtracted image.

The contours which we select are based on few thresholds and conditions.

The demo below was captured by me from my phone which is really shaky, so the thresholds I have fixed are for that particular video input.

You will have to estimate your values and feed it to the INI file.

#Next step

We will train a model to classify the object detected and predict humans from the object detected.

I have saved the conoturs detected which will be be my training data for my model.

#Important reference links

Github Repo : https://github.com/dvigneshwer/human_motion_detection

Demo of object detection : https://youtu.be/SAVFV5eWIvk

OpenCV2 Installation :  http://www.samontab.com/web/2014/06/installing-opencv-2-4-9-in-ubuntu-14-04-lts/

Reference: http://www.pyimagesearch.com/2015/05/25/basic-motion-detection-and-tracking-with-python-and-opencv/