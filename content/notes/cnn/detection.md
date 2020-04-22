---
title: "Object Detection"
draft: true
weight: "12"
katex: true
---

### Introducing Object Detection
- Suppose we want to detect cars in images and videos
- This process involves object detection
- Object detection is a type of supervised classification
- Therefore, we need to train a network on a large number of input images of cars
- Having more images will lead to more accurate predictions of whether an image has a car or not
- This network would return a binary output of whether there is a car or not
- This network would also return the coordinates representing a bounding box around the car
- The following are the general steps for object detection:
	1. Train a convolutional network on images of cars
	2. Perform sliding windows detection on live video or new images
	3. Output a list of bounding boxes around any cars if they exist

![convolutiondetection](/convolution_detection.svg)

### Introducing Sliding Windows Detection

---

### tldr

---

### References
- [Object Detection](https://www.youtube.com/watch?v=5e5pjeojznk&list=PLkDaE6sCZn6Gl29AoE31iwdVwSG-KnDzF&index=25)
- [Convolutional Implementation Sliding Windows](https://www.youtube.com/watch?v=XdsmlBGOK-k&list=PLkDaE6sCZn6Gl29AoE31iwdVwSG-KnDzF&index=26)
- [Bounding Box Predictions](https://www.youtube.com/watch?v=gKreZOUi-O0)
