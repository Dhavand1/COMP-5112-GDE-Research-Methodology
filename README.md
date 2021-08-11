# COMP-5112-GDE-Research-Methodology

Detecting and Recognizing Vehicle Number Plate from a video in real time

# Table of Contents

1) [Dependencies](#Dependencies "Goto Dependencies1")
2) [Description](#Description "Goto Description")
3) [Approach](#Approach "Goto Approach")
4) [Methodology](#Methodology "Goto Methodology")
5) [Example](#Example "Goto Example")
6) [Usage](#Usage "Goto Usage")
7) [Model](#Model "Goto Model")
8) [Video](#Video "Goto Video")
9) [mainfile.py](#mainfile.py "Goto mainfile.py")
10) [Results](#Results "Goto Results")
11) [Advantages](#Advantages "Goto Advantages")
12) [Future-Scope](#Future-Scope "Goto Future-Scope")
13) [License](#License "Goto License")
14) [Support](#Support "Goto Support")
15) [References](#Referencese "Goto References")


# Dependencies
opencv-python 3.4.2

numpy 1.17.2

skimage 0.16.2

tensorflow 1.15.0

imutils 0.5.3

# Description
Detecting and Recognizing Vehicle Number Plate is a very important task for a camera surveillance-based security system. We can extract the number plate from an image using some computer vision techniques and then we can use Optical Character Recognition to recognize the number written on the plate. Below, I will guide you through the whole procedure of the task and the project.

# Approach
1. Find all the contours in the image.
2. Find the bounding rectangle of every contour.
3. Compare and validate the sides ratio and area of every bounding rectangle with an average plate (plate recognition).
4. Apply image segmentation in the image inside validated contour to find characters in it.
5. Recognize characters using an OCR (character recognition).



