---
layout: default
title: Car detection with YOLOv2
---

## **Description**

This project involved object detection using the very powerful YOLO model. Many of the ideas in this project are described in the two YOLO papers: Redmon et al., 2016 (https://arxiv.org/abs/1506.02640) and Redmon and Farhadi, 2016 (https://arxiv.org/abs/1612.08242).

The popularity of the YOLO algorithm comes from the high-accuracy that it can achieve while being able to process images in real-time. This is due to the fact that it only needs to process each image through the model once to detect all objects in the image. 

For this model:
1. The input is a batch of images of shape (m, 608, 608, 3)
2. The output is a list of bounding boxes along with the recognized classes. Each bounding box is represented by 6 numbers  (pc,bx,by,bh,bw,c) as explained above. If you expand c into an 80-dimensional vector, each bounding box is then represented by 85 numbers.

Here, we use 5 anchor boxes. So the YOLO architecture is somewhat like: 

IMAGE (m, 608, 608, 3) -> DEEP CNN -> ENCODING (m, 19, 19, 5, 85).

<img src="/assets/img/yolo_architecture.png" alt="Logo" />
      
