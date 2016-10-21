---
layout: post
title: "AI: Neural Nets Overview"
date: 2016-10-21
sources: lecture; http://neuralnetworksanddeeplearning.com/chap1.html; http://neuralnetworksanddeeplearning.com/chap2.html
type: summary
---

## How Are Neural Nets Structured?
Neural nets consist of layers of nodes that are connected by edges. The first layer takes in inputs and the last layer produces outputs, and a number of intermediary layers are called "hidden layers" and affect the relationship between inputs and outputs. One particular type of neural net, a feed-forward network, only consists of edges that point in the direction from input to output layers -- in these networks, there are no connections between nodes in the same layer or to nodes in a previous layer.

## How are Neural Nets Used for Prediction?
A neural net's edges contain weights, its nodes contain biases, and a specified function is computed at each node. Using these specifications, input values are propagated throughout the neural network, resulting in values at the output layer of the neural network that serve to predict some output.
### Propagation
The first layer of the neural net takes in input values. Nodes in the next layer each receive a weighted sum of these inputs, depending on the weights of the edges connecting nodes in the two layers. These nodes then output some function of the values they received (which depends on the function of the neural net and the bias that the node contains). This process is repeated for each layer, until the neural network produces the final predictions in the output layer.

## How are Neural Nets Trained?
Neural nets are trained to find the proper weights and biases for its edges and nodes. It does so using [gradient descent](https://cchen23.github.io/blog/2016/10/09/gradient-descent). However, because there are so many parameters (all the weights and biases of the neural network) and possibly many layers, separately computing the gradient for each parameter ends up taking a long time. Therefore people use a method called backward propagation. 
### Backward Propagation
Gradient descent attempts to minimize the error of the neural network's outputs. The cost function measures the error of the neural net's prediction outputs. Each layer's outputs depend upon the outputs of the layer before, so the derivative of the cost function with respect to the parameters in layer k - 2 depends on the derivative of the cost function with respect to layer k - 1. So instead of separately computing the gradient of parameters in each layer, back propagation starts from the output layer and works backwards. By working backwards, it can re-use the gradients that it has already computed to compute gradients of earlier layers, making gradient descent a lot more efficient.
