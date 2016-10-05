---
layout: post
title: "AI/ML: Statistical Learning Theory"
date: 2016-10-04
type: summary
---

## Statistical Learning
Statistical learning theory applies generally to learning from examples. Learning from examples means that an algorithm is given a set of inputs and outputs, and the algorithm returns a way of mapping inputs to outputs. This mapping is also called a hypothesis. The goal of statistical learning is to create a hypothesis, using a set of samples datapoints chosen independently at random, that generalizes to datapoints that were drawn from the same distribution that the sample datapoints came from. We want the hypothesis to reflect the actual mapping of inputs and outputs that the sample datapoints came from, which is called the concept.

## How to Evaluate a Hypothesis
A hypothesis is evaluated based on how accurately it classifies datapoints. For any given datapoint, the loss function measures how inaccurately the hypothesis classifies the datapoint. For example, the loss function could have a value of 1 for incorrect classifications, and a value of 0 for correct classifications. The loss function is used to calculate the generalization error, which is the expected value of the loss function. A good hypothesis has low generalization error -- it is expected to have a low inaccuracy.

## How to Find a Hypothesis
One way of learning a hypothesis is to find a hypothesis that has high accuracy on the sample data. However, this creates a problem because our ultimate goal is not to just be really good at predicting outputs for sample data -- we want to accurately predict outputs for any data. This poses a problem, because if we just try to minimize the error on the sample data, we might end up with a hypothesis that is really good at classifying sample data, but isn't very useful for anything else. That would mean that it overfits the data.
In order to avoid ending up with a super specific function that just classifies sample data, we can restrict the learning hypothesis to a specific set of hypotheses that we think might do a good job at describing all the data. These hypotheses form a hypothesis class. By limiting the possible hypotheses, we can decrease the probability of overfitting.

## Guarantees
We can prove that if there is a hypothesis that accurately represents the concept, then we can find a hypothesis that usually has a relatively high accuracy (also referred to as "Probably Approximately Correct") if we are given enough samples.
