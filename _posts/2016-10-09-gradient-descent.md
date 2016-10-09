---
layout: post
title: "AI/ML: Gradient Descent"
date: 2016-10-09
type: summary
---

## Motivation
Gradient descent is a method used to find the local minimum of a function. If the function is convex, then gradient descent can find the global minimum as well. 

## Application
When we try to train a predictor using sample data, we can use a cost function to tell us how wrong a prediction is. We can use gradient descent to find the prediction parameters that minimize the cost function, which helps create a more accurate predictor.

## Negative Gradient: Direction of Steepest Decrease
A gradient of a function is a vector of its partial derivatives with respect to each input parameter. Derivates show how a function changes, and the gradient of a function shows how a function's value changes in response to changes in input values. By calculating the gradient of a function at a certain point, we can see how the function's value changes in response to changing the function's inputs a little bit in each direction. (We can only change the inputs a little bit, because derivatives only tell us how the function changes *near* a certain point.) If we multiply the gradient vector by a vector of changes to the input, we see how the function's output value changes when we move a little bit in a certain direction. To maximize the decrease in the function output, we therefore want to move in the opposite direction of the gradient, since multiplying vectors in the opposite direction creates the most negative product.

## Method
We want to find the input vector that minimizes the output of a function. Gradient descent uses a greedy method -- it keeps moving in the direction that most quickly decreases the function's value. The negative gradient gives us the direction of steepest descent, so at each step we calculate the gradient and move a little bit in the opposite direction. We don't want to move too far, because the gradient only tells us how the function behaves near a point. But we also don't want to move too little, since that would require more steps to reach the minimum. We can prove that it does not take too many steps to reach the minimum, if we choose a reasonable (based on the constraints of function we want to minimize) amount to move at each step.

## Optimization: Stochastic Gradient Descent
Even though gradient descent does not take too many steps, each step could take a long time. When gradient descent is used to minize a cost function, the cost function is the average inaccuracy over each training datapoint. However, sometimes many datapoints are used to train predictors, which makes computing the gradient of the cost function take a long time. One way to cut down that time is to use stochastic gradient descent. Instead of finding the average cost of every single training datapoint, at each step we just randomly choose a sample of training datapoints (or even a single training datapoint) and compute the gradient with that sample. We can prove that this method is expected to still find something close to the minimum of the function, even though it performs a lot faster than the alternative.
