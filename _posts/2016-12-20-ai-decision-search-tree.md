---
layout: post
title: "AI/ML: Decision Making and Search Trees"
date: 2016-12-20
sources: lecture, misc reading
type: summary
---

# Utility and Search Trees
In some decision-making problems, we can assign utility scores to different outcomes. If we do this, we can model rational decision making as making the choices that maximize the total utility. In some scenarios/games, we can maximize utility by looking at all possible outcomes of all possible decisions. These form a tree of outcomes and corresponding utilities, and different decisions can lead to different outcomes and therefore different utilities. In that case, we can make a decision by searching the tree for the decisions that lead to the highest utility score.

# Heuristics
However, in more complicated games there are too many possibilities in the tree. Therefore people have come up with heuristics to deal with complicated search trees. One method involves looking a limited number of steps. Instead of exploring the entire tree to find the decision with the highest utility, we can use a heuristic to estimate the score of an intermediate point and choose decisions based on the intermediate point that we would reach after a couple of turns. Another method, called Alpha-Beta search, applies to two-player games in which the players alternate turns, one player wants to maximize a score, and the other player wants to minimize the same score. In this situation, we can use the assumption that both players always make decisions in their own best interest to prune the search tree. While exploring the search tree, we might realize that one player would never make a decision that leads to to a certain branch of the tree because it is definitely not their best option. In that case, we do not have to explore that branch of the tree any further because we know that the two players will never reach that part of the search tree.
