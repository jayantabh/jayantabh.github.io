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

* Build the content cost function <img src="https://latex.codecogs.com/gif.latex?$J_{content}(C,G)$" title="$J_{content}(C,G)$" />
* Build the style cost function <img src="https://latex.codecogs.com/gif.latex?$J_{style}(S,G)$" title="$J_{style}(S,G)$" />
* Put it together to get <img src="https://latex.codecogs.com/gif.latex?$J(G)&space;=&space;\alpha&space;J_{content}(C,G)&space;&plus;&space;\beta&space;J_{style}(S,G)$" title="$J(G) = \alpha J_{content}(C,G) + \beta J_{style}(S,G)$" />. 

We would like the "generated" image G to have similar content as the input image C. We choose a layer in the middle of the network-neither too shallow nor too deep-as the reference layer. 

We run both the images C and G through the network and calculate the content cost as,
<img src="https://latex.codecogs.com/gif.latex?$$J_{content}(C,G)&space;=&space;\frac{1}{4&space;\times&space;n_H&space;\times&space;n_W&space;\times&space;n_C}\sum&space;_{&space;\text{all&space;entries}}&space;(a^{(C)}&space;-&space;a^{(G)})^2$$" title="$$J_{content}(C,G) = \frac{1}{4 \times n_H \times n_W \times n_C}\sum _{ \text{all entries}} (a^{(C)} - a^{(G)})^2$$" />

Here, n<sub>H</sub>, n<sub>W</sub> and n<sub>C</sub>  are the height, width and number of channels of the hidden layer you have chosen, and appear in a normalization term in the cost. For clarity, note that a<sup>(C)</sup> and  a<sup>(G)</sup> are the volumes corresponding to a hidden layer's activations. 

<img src="/assets/img/NST_LOSS.png" alt="Logo" />

For the style cost we first calculate the Style Matrix which is also known as the "Gram Matrix" in Linear Algebra.

In NST, you can compute the Style matrix by multiplying the "unrolled" filter matrix with their transpose:

<img src="/assets/img/NST_GM.png" alt="Logo" />

The result is a matrix of dimension (n<sub>C</sub>,n<sub>C</sub>) where n<sub>C</sub> is the number of filters. The value G<sub>ij</sub> measures how similar the activations of filter i are to the activations of filter j.

After generating the Style matrix (Gram matrix), we will minimize the distance between the Gram matrix of the "style" image S and that of the "generated" image G. For now, we are using only a single hidden layer a<sup>[l]</sup>, and the corresponding style cost for this layer is defined as:

<img src="https://latex.codecogs.com/gif.latex?$$J_{style}^{[l]}(S,G)&space;=&space;\frac{1}{4&space;\times&space;{n_C}^2&space;\times&space;(n_H&space;\times&space;n_W)^2}&space;\sum&space;_{i=1}^{n_C}\sum_{j=1}^{n_C}(G^{(S)}_{ij}&space;-&space;G^{(G)}_{ij})^2$$" title="$$J_{style}^{[l]}(S,G) = \frac{1}{4 \times {n_C}^2 \times (n_H \times n_W)^2} \sum _{i=1}^{n_C}\sum_{j=1}^{n_C}(G^{(S)}_{ij} - G^{(G)}_{ij})^2$$" />

where G<sup>(S)</sup> and G<sup>(G)</sup> are respectively the Gram matrices of the "style" image and the "generated" image, computed using the hidden layer activations for a particular hidden layer in the network.

You can combine the style costs for different layers as follows:

<img src="https://latex.codecogs.com/gif.latex?$$J_{style}(S,G)&space;=&space;\sum_{l}&space;\lambda^{[l]}&space;J^{[l]}_{style}(S,G)$$" title="$$J_{style}(S,G) = \sum_{l} \lambda^{[l]} J^{[l]}_{style}(S,G)$$" />

where the values for λ<sup>[l]</sup> can be defined as per importance of each layer.

Finally, we create a cost function that minimizes both the style and the content cost. The formula is:

<img src="https://latex.codecogs.com/gif.latex?$$J(G)&space;=&space;\alpha&space;J_{content}(C,G)&space;&plus;&space;\beta&space;J_{style}(S,G)$$" title="$$J(G) = \alpha J_{content}(C,G) + \beta J_{style}(S,G)$$" />

Now, we initialize the "generated" image as a noisy image created from the content_image. By initializing the pixels of the generated image to be mostly noise but still slightly correlated with the content image, this will help the content of the "generated" image more rapidly match the content of the "content" image. 

<img src="/assets/img/generated_noise.png" alt="Logo" />

Now we can run these images through the network for multiple iterations till we get desired results.

After around 200 iterations we get the results as shown below:

<img src="/assets/img/louvre_generated.png" alt="Logo" />

Some other combinations which have been generated using similar approaches are given below:

<img src="/assets/img/perspolis_vangogh.png" alt="Logo" />

<img src="/assets/img/pasargad_kashi.png" alt="Logo" />

<img src="/assets/img/circle_abstract.png" alt="Logo" />

