---
layout: default
title: Art generation with Neural Style Transfer
---

### Description:

In this project, we used Neural Style Transfer to generate novel artistic images resembling the work of an artist. This algorithm was created by [Gatys et al. (2015)](https://arxiv.org/abs/1508.06576).

Neural Style Transfer (NST) merges two images, namely, a "content" image (C) and a "style" image (S), to create a "generated" image (G). The generated image G combines the "content" of the image C with the "style" of image S.

<img src="/assets/img/louvre_generated.png" alt="Logo" />

In this example, we will generate an image of the Louvre museum in Paris (content image C), mixed with a painting by Claude Monet, a leader of the impressionist movement (style image S).

We will do this by using VGG-19, a 19-layer version of the VGG network. This model has already been trained on the very large ImageNet database, and thus has learned to recognize a variety of low level features (at the earlier layers) and high level features (at the deeper layers).

We will build the NST algorithm in three steps:

* Build the content cost function $J_{content}(C,G)$
* Build the style cost function $J_{style}(S,G)$
* Put it together to get $J(G) = \alpha J_{content}(C,G) + \beta J_{style}(S,G)$. 

