---
layout: post
title: "AI: Decision Trees"
date: 2016-09-21
sources: lecture, misc online sources
type: summary
---

## Why do people use decision trees?
People use decision trees because they can easily understand why decision trees make specific decisions -- the trees have explicit branches based on specific characteristics, and it's easy to see how the trees relate inputs to outputs.
People can use decision trees to predict an output given a certain set of inputs. For instance, someone might use a decision tree to predict whether a passenger on the Titanic survived, given their age, gender, class, and family size.

## How do decision trees work?
Decision trees contain levels of nodes, and at each level a node represents a certain characteristic. The branches coming out of the node represent the possible values of the characteristic. Each branch ends either in an outcome or another branching node that represents another characteristic. See [a decision tree](https://bigwhalelearning.files.wordpress.com/2014/11/titanic_heuristic.png) for predicting survival of passengers on the Titanic.

## How are decision trees constructed?
Decision trees are created by choosing characteristics to split on, and the order in which to split on these characteristics. A heuristic can be used to choose which features to split on -- starting from an empty tree, look for the best next node to split on. After choosing that characteristic, create branches for each possible value it can take. One way to define the next best feature to split on is to measure how much this characteristic matters to the output -- if knowing this characteristic about an input makes someone a lot more certain about the output, it's probably a good idea to split on this characteristic. Maybe divide each of the branches based on other input characteristics. However, don't make the decision tree so specific that it can't generalize to new situations.
