---
layout: default
title: Car detection with YOLOv2
---

## **Description**

This project involved object detection using the very powerful YOLO model. Many of the ideas in this project are described in the two YOLO papers: Redmon et al., 2016 (https://arxiv.org/abs/1506.02640) and Redmon and Farhadi, 2016 (https://arxiv.org/abs/1612.08242).

The popularity of the YOLO algorithm comes from the high-accuracy that it can achieve while being able to process images in real-time. This is due to the fact that it only needs to process each image through the model once to detect all objects in the image. 

For this model:
1. The input is a batch of images of shape (m, 608, 608, 3)
2. The output is a list of bounding boxes along with the recognized classes. Each bounding box is represented by 6 numbers  (pc,bx,by,bh,bw,c).

<img src="/assets/img/box_label.png" alt="Logo" />

Anchor boxes are the bounding boxes that are used to search for objects. Here, we use 5 anchor boxes. So the YOLO architecture is somewhat like:

<img src="/assets/img/yolo_architecture.png" alt="Logo" />

The model tries to detect objects in each of the segments in the 19X19 grid and the segment which holds the center of the object is responsible for detecting the image.

The anchor boxes are of different size so that we can detect both overlapping objects and objects of varying orientation and size.

One of the issues with such a model is multiple detections of each object. This issue is mitigated by first rejecting any detection with a low score and then using Non-Max suppression to get a unique detection for each object. In Non-Max suppression we reject any detection which has a higher IoU than a threshold with the detection having highest score.

Since the model takes a lot of time to train we have used pretrained weights from the YOLOv2 model and further trained it using our data. An example of output bounding boxes after filtering is given below:
<img src="/assets/img/download.png" alt="Logo" />
