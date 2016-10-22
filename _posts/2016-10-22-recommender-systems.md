---
layout: post
title: "AI: Recommender Systems"
date: 2016-10-22
sources: Lecture
type: summary
---

## Motivation for a Learning-Based Approach
Recommender systems try to predict which items a user will like the most. Some systems might determine characteristics for each item and characteristics of each user, based on the things they've liked in the past. However, this has some problems -- for example, it doesn't provide a good way of dealing with new items or new users, and it might be difficult to choose which characteristics to track. A learning-based approach helps to address these problems.

## Method: Using a Learning-Based Approach
Mathematically, the goal of recommender systems is to predict the matrix in which each index corresponds to how much a given user likes a given item. A system with m users and n items could be represented by an m-by-n matrix, in which the value at row i, column j represents how much user i enjoys item j. To use the learning-based method, we assume that this matrix has low rank. That means that relatively few parameters can be used to approximately capture the values in the entire matrix. The learning-based approach can use gradient descent to learn the parameters needed to approximate the matrix. Since the number of parameters is small relative to the size of the matrix, this method can use relatively few training datapoints to learn the parameters and approximate the entire matrix. After learning parameters, this approach can use those parameters to predict how much a given user will like a given item, and create recommendations based on those predictions.
