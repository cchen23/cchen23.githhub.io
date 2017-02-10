---
layout: post
title: "NN: Learning in Neural Networks"
date: 2017-02-09
sources: lecture
type: summary
---

## Neural Networks Learn to Minimize Errors

Neural networks learn by adjusting the synaptic weights between neurons. When learning, the network receives inputs and expected outputs, and it compares the outputs given by the network to the expected outputs. A loss function quantifies the number of erros: if the neural network has many inconsistencies between actual and desired output, then the loss function has a higher value. When learning, the neural network adjusts its weights to minimize the loss function.

### Minimizing the Loss Function

The gradient of a function points in the direction of steepest ascent. To minimize the loss function, learning therefore adjusts weights in the opposite direction: it subtracts some multiple of the gradient of the loss function from the current weight setting. This is called the delta rule. The specific constant that the gradient is multiplied by before being subtracted from the weights is a parameter that controls how quickly the neural network changes its weights: smaller constants correspond to slower learning, but larger constants could cause the network's weights to change too much too quickly.

There are a few possible variations in the weight update method. In batch updates, the weight adjustment is computed by looking at the average loss over all the datapoints (the batch loss). This produces a more accurate update, but could take a lot of time because it uses each datapoint. Learning could also use an online update, in which the weight adjustment is computed using the loss of a randomly chosen datapoint. This requires less computation, but it produces a noisier estimate. As a tradeoff between online and batch update, the minibatch update method looks at a few randomly chosen datapoints at a time when computing the weight adjustment.

### Loss Functions

Various loss functions can be used for computing weight adjustments, and these loss functions try to capture how incorrect the neural network's predictions are. For example, a loss function might be the squared difference between the desired and the actual output.

One reason that weight updates are computed using these loss functions, rather than simply the difference between the expected and desired value, is because the difference might not be a continuous function. In addition, many of the loss functions that are used for learning are convex functions, which makes sure that gradient descent finds the weight that achieves the global (not just a local) minimum of the loss function.
