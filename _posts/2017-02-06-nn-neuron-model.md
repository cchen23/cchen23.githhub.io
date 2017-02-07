---
layout: post
title: "NN: Neuron Model"
date: 2017-02-06
sources: lecture
type: summary
---

## Neuron Structure

In a neural network, each neuron receives inputs from incoming edges. Each neuron has a threshold and an activation function, which determine how its inputs affect its output. To produce its output the neuron takes a weighted sum of its inputs, subtracts its threshold value, and performs the activation function on the difference. The neuron's output can serve as an input to another neuron, creating multiple layers of neurons in a neural network.

In comparison to standard electrical circuits, neurons in neural networks (in real life and in artificial networks) have much higher fan-in and fan-out. This means that they are more powerful but also more complex.

![alt text][logo]

[logo]: https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "Logo Title Text 2"
## Activation Function

Two common functions used in neural networks are the Heaviside Step Function and the RELU Function. The Heaviside Step Function produces an output of 1 for a non-negative value and produces a 0 otherwise, giving a binary decision. The RELU Function produces a value of 0 for a negative value and produces an output equal to the input for non-negative values. Above a certain threshold, this function acts linearly.

## Decision Boundary and Preferred Stimulus

A decision boundary for a binary classifier splits possible inputs into two sets: those that produce outputs of 1 and those that produce outputs of 0. Neurons that use Heaviside Step Functions as their activation function have a decision boundary that consists of a hyperplane. This hyperplane consists of the inputs for which the dot product of the input vector and the weight vector equals the threshold, since these inputs determine where the activation function changes behavior (from outputting 0 to outputting 1). All vectors on one side of the hyperplane (the side with the weight vector) produce outputs of 1, while all vectors on the other side of the hyperplane produce outputs of 0.

In this case, the neuron's preferred stimulus -- the minimum input that activates the neuron -- is in the direction of the weight vector, since this direction maximizes the dot product between the weight vector and the input.
