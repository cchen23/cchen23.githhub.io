---
layout: post
title: "NN: Convolutional Neural Nets"
date: 2017-03-05
sources: lecture
type: summary
---

## How do convolutional nets work?

In convolutional neural nets, a neuron in one layer is connected to a subset of the neurons in the next layer according to the distance between the two neurons. The weights between neurons in two layers are constrained so that each neuron in a single layer uses the same set of weights in their connections to the next layer.

For example, in a neural network with two layers, each neuron in the first layer might be connected to only three neurons in the next layer: the one directly above it, the one to the left, and the one to the right. Each neuron in the first layer would be connected to the three respective neurons in the second layer via the same weights.

![Convolutional Network Weights](https://swarbrickjones.files.wordpress.com/2015/04/convolution.png "Weights Example")

The shared sets of weights between each pair of layers act as filters that we slide across the signals, which are the outputs of neurons in the layers feeding into the weights. The outputs of these convolutions then serve as the inputs to the layers that the weights feed into.

![Convolutional Network Filter](http://colah.github.io/posts/2014-07-Understanding-Convolutions/img/RiverTrain-ImageConvDiagram.png "Filter Example")

In each layer, we can have multiple filters that each detect a certain feature of the input. Each filter produces its own output layer, and these outputs can in turn be used as inputs to subsequent layers, in which filters can detect combinations of features in the neural network's input.

## Why do we use convolution nets?

The constraints placed on weights in convolutional neural nets has similarities to how real neurons (in the brain) process images. In addition, limiting the number of connections between neurons means that training a convolutional neural net requires less computation.

## We do we use pooling?

We can add pooling layers into convolutional networks. In these layers, instead of an actual convolution, the outputs of the neurons in the layer are put into a function such as the maximum or average function. For instance, the pooling layer might output the maximum value of each set of four adjacent. This means that small changes in input, which might shift the output of a layer by a little bit, can get smoothed out by the pooling operation.

## How do we learn the weights for these networks?

### Gradient descent with shared weights

In a neural network, we find the gradient of the error function with respect to each connection and we use this gradient to learn the connections' weights. In convolutional networks, multiple connections share the same weight. Because multiple connections are constrained to have the same weight value, while learning the weights we use the sum of the gradients for each connection sharing a certain weight as the gradient for that weight value, and we update the weights accordingly.

### Gradient descent with pooling

During backpropagation, we send the gradient of the connections in each layer backwards to the previous layer, and we use each layer's gradients to compute the gradients in the previous layer. In layers that use functions such as max pooling, a neuron in a layer might be connected to multiple neurons in the previous layer but only receive input from one of them (the neuron with the maximum value). In these situations, we only send the receiving neuron's gradient back to the neuron whose input it actually receives.
