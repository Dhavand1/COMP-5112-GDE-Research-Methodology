# COMP-5112-GDE-Research-Methodology

Detecting and Recognizing Vehicle Number Plate from a video in real time

# Table of Contents

1) [Dependencies](#Dependencies "Goto Dependencies1")
2) [Description](#Description "Goto Description")
3) [Approach](#Approach "Goto Approach")
4) [Methodology](#Methodology "Goto Methodology")
5) [Code](#Code "Goto Code")
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
a) Find all the contours in the image.

b) Find the bounding rectangle of every contour.

c) Compare and validate the sides ratio and area of every bounding rectangle with an average plate (plate recognition).

d) Apply image segmentation in the image inside validated contour to find characters in it.

e) Recognize characters using an OCR (character recognition).

# Methodology
1. To reduce the noise we need to blur the input Image with Gaussian Blur then convert the it to grayscale. 
![image](https://user-images.githubusercontent.com/79090426/129054772-03af6d70-a78d-424b-a1f4-da940f150087.png)

2. Find vertical edges in the image.

  ![image](https://user-images.githubusercontent.com/79090426/129055079-74a49172-5f27-4c2b-b87e-df05d02ecbf2.png)

3. To reveal the plate we have to binarize the image. For this apply Otsu’s Thresholding on the vertical edge image. Otsu’s Thresholding determines the value automatically, whereas in other thresholding methods we have to choose a threshold value to binarize the image.
![image](https://user-images.githubusercontent.com/79090426/129055947-463294b7-89b5-4d6f-aa1a-df2d1379bf9e.png)
4. Apply Closing Morphological Transformation on thresholded image. Closing is useful to fill small black regions between white regions in a thresholded image. It reveals the rectangular white box of the number plate present on the vehicle.
![image](https://user-images.githubusercontent.com/79090426/129056325-5a281b6c-b508-4758-872c-a811ec01b400.png)
5. To detect the plate on the vehicle we need to find contours in the image. Contour is an outline, especially one representing or bounding the shape or form of something. It is important to binarize and morph the image before finding contours so that it can find more relevant and less number of contours in the image. If you draw all the extracted contours on original image, it would look like this: 
![image](https://user-images.githubusercontent.com/79090426/129057654-c0fab284-e111-492d-b291-164f5e8b29a7.png)
6. Now find the minimum area rectangle enclosed by each of the contour and validate their side ratios and area. I have defined the minimum and maximum area of the plate as 4500 and 30000 respectively.
7. Now find the contours in the validated region and validate the side ratios and area of the bounding rectangle of the largest contour in that region. This is because the number plate will be having the largest area. After validating we will get a perfect contour of a license plate. Now extract that contour from the original image. We will get the image of the number plate somewhat like this:
![image](https://user-images.githubusercontent.com/79090426/129058410-ddef660a-08b3-4325-8899-1737a093a329.png)

# Code
i) The above step is performed by **clean_plate** and **ratioCheck** method of class **PlateFinder**.

ii) To recognize the characters on the plate precisely, we have to apply image segmentation. For that first step is to extract the value channel from the HSV format of the plate’s image.

iii) Now apply adaptive thresholding on the plate’s value channel image to binarize it and reveal the characters. It is an image processing method that creates a bitonal (aka binary) image based on setting a threshold value on the pixel intensity of the original image. The image of plate can have different lightning conditions in different areas, in that case adaptive thresholding can be more suitable to binarize because it uses different threshold values for different regions based on the brightness of the pixels in the region around it.

iv) After binarizing apply bitwise not operation on the image to find the connected components in the image so that we can extract character candidates.

v) Construct a mask to display all the character components and then find contours in mask. After extracting the contours take the largest one (that will be the number plate), find its bounding rectangle and validate side ratios.

vi) After validating the side ratios find the convex hull of the contour and draw it on the character candidate mask.

vii) Now find all the contours in the character candidate mask and extract those contour areas from the plate’s value thresholded image, you will get all the characters separately.

![image](https://user-images.githubusercontent.com/79090426/129067510-b879ad0a-d2c5-48e5-a5fd-fe8babcce4fc.png)

viii) The above steps are performed by **segment_chars** function that you can find in the source code. The driver code for the functions used is written in the method **check_plate** of class **PlateFinder**.

ix) Finally, use OCR to recognize the character one by one.

# Usage






