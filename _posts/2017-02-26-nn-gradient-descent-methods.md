---
layout: post
title: "NN: Gradient Descent Methods"
date: 2017-02-26
sources: lecture
type: summary
---

## Possible Issues with Gradient Learning

When [training neural networks](https://cchen23.github.io/blog/2017/02/09/nn-learning), we use gradient descent to minimize the errors in the network's predictions. However, certain aspects of the error function could cause issues during gradient learning. 

### Local Minima

The error function could have local minima. Because of this, gradient descent might converge to a local minimum instead of finding the global minimum of the function. To deal with this problem, we could use a convex approximation of the gradient function or we could try gradient descent from different initial values in the hopes that one of the initializations will find the global minimum, or something close to it.

### Ravines

For example, the error function might decrease very rapidly in one direction but more slowly in another direction, forming a ravine-like structure. In this case, gradient descent could oscillate back and forth across the ravine, converging slowly to the minimum. 

### Method: Momentum

One way to deal with ravines is to compute a moving average of the gradient computed on each iteration. In doing so, we hope to average out the oscillations across the ravine and move more quickly to the minimum of the error function.

### Method: Diagonal Rescaling

The problem of ravines occurs because the error function decreases more quickly in certain directions than others. To deal with this, we can use different learning rates for different directions. The direction of the update vector will not be exactly in the direction of steepest descent, but it will still be in a direction of descent.

### Method: Input Centering/Rescaling

Another way to deal with ravines is the re-scale input values to a reasonable range, to make sure that updates do not change the weights too quickly.

### Plateaus

Another potential problem with gradient learning is that certain sections of the area function are relatively flat, which means that their gradients are near zero. For example, the logistic function flattens out at large positive or negative input values. This means that if the initial weights of a network cause large inputs to a neuron's logistic activation function, then the neuron will change very little on each iteration of radient descent.

![logistic function](https://upload.wikimedia.org/wikipedia/commons/thumb/8/88/Logistic-curve.svg/320px-Logistic-curve.svg.png "Logistic Function")

To avoid this, we can initialize the weights so that the magnitude of inputs to each neuron's activation function is not too large. This involves setting the variance of the random weight initializations based on the fan-in and fan-out to each weight.

### Decreasing Learning Rate

As we get closer to the minimum of a function, we want to take smaller steps in each update. To do this, we can decrease the learning rate as training progresses. Certain methods adjust the learning rate according to the magnitudes of gradients computed at previous steps.

## Generalization

In training our network, we aim to construct a network that will be able to provide correct predictions for unseen data. This means that we want to avoid overfitting, which is when a network performs better for predicting the data it was trained on than for predicting unseen data. To train a network whose predictions generalize to unseen data, we can apply a number of strategies during gradient descent.
During training, we can split our data into a training set, which we use to train the model, and a test set, which we use to see how the model performs on previously unseen data.

### Method: Regularization

More complicated models might overfit the data because they end up modelling the noise in the training data. To avoid this problem, we can penalize large weights by adding a term that relies on the size of the model's weights to the error function. This imposes a soft constraint that pushes the network towards smaller weights. Another method involves a hard constraint in which we only consider weight settings that fulfill a certain condition, such as requiring that the sum of squared weights is less than a certain value.

### Method: Model Averaging

Different models tend to make different mistakes in prediction. Therefore another method involves training multiple models with various architectures and weight initializations, and using a combination of their outputs for the final prediction.

### Method: Dropout

Another method to improve generalization involves setting a certain number of neuron's outputs to zero during each iteration of training.
