---
layout: default
title: Car detection with YOLOv2
---

## **Description**

In this project we built a very deep convolutional networks, using Residual Networks (ResNets). In theory, very deep networks can represent very complex functions; but in practice, they are hard to train. Residual Networks, introduced by [He et al.](https://arxiv.org/pdf/1512.03385.pdf), allow you to train much deeper networks than were previously practically feasible.

In ResNets, a "shortcut" or a "skip connection" allows the gradient to be directly backpropagated to earlier layers:

<img src="/assets/img/skip_connection_kiank.png" alt="Logo" />

The identity block is the standard block used in ResNets, and corresponds to the case where the input activation (say a<sup>[l]</sup>) has the same dimension as the output activation (say a<sup>[l+2]</sup>). Here is an alternative diagram showing the individual steps:

<img src="/assets/img/idblock2_kiank.png" alt="Logo" />

Similarly, skip connections can also skip over 3 sets of layers.

The following figure describes in detail the architecture of this neural network. "ID BLOCK" in the diagram stands for "Identity block," and "ID BLOCK x3" means that 3 identity blocks are stacked together.

<img src="/assets/img/resnet_kiank.png" alt="Logo" />

We will test our model on the SIGNS dataset which contains integers in Sign language as images

<img src="/assets/img/signs_data_kiank.png" alt="Logo" />

The dataset contains 1200 examples of which 1080 examples are in train set and the other 120 are in the test set.

Training this model with 20 epochs provided a train and test accuracy of 94% and 86% respectively.


