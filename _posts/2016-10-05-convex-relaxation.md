---
layout: post
title: "AI/ML: Convex Relaxation"
date: 2016-10-05
type: summary
---
* Continuation of Statistical Learning Theory [post](https://cchen23.github.io/blog/2016/10/04/statistical-learning-theory).
## Motivation
If we find a mapping that classifies sample data well, then we can prove that the mapping generalizes to all data reasonably well most of the time, if there is enough sample data.
However, it's not always easy to find a mapping that classifies sample data well.

To find a hypothesis that accurately predicts labels for sample data, we try to minimize the inaccuracy of the classification. In doing so, we have a function (called a loss function) that tells us how inaccurate a hypothesis is, and we try to minimize this function. Part of the trouble comes from minimizing this function. Sometimes the functions are complicated, and it's not easy to tell whether a certain value is a minimum. It's possible that we find a value that is less than values near it, but this could just be a local minimum instead of the actual value that minimizes the function over all possible values.

## Convex Relaxation
To avoid confusing a local optimum with a global optimum, we use convex relaxation. With a convex function, any local optimum is also a global optimum. So if our loss function is a convex function, then we can just try to find a minimum, and once we've found it we know that we've minimized the entire function. So we use a method called convex relaxation: we approximate the original loss function with a convex function, and find the hypothesis that minimizes the convex function.

## Method: Minimizing a convex function
To minimize a convex function, we can use an algorithm called gradient descent. In this algorithm, we start from a certain point and find the direction in which the function we're trying to minimize decreases the fastest (the gradient tells us this direction). We move a bit in that direction, and repeat the process starting at the point we move to. We repeat this until we find the minimum of the function. We can prove that this method doesn't take too long to find something that's close to the minimum of the function.
