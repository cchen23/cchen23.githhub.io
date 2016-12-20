---
layout: post
title: "AI/ML: Reinforcement Learning"
date: 2016-12-20
sources: lecture, misc reading
type: summary
---

# We Can Model Reinforcement Learning with Markov Decision Processes
In a Markov Decision Process, an actor's actions lead to transitions between different states. The actor receives a cumulative reward from the actions they take and the states to which they transition. We can model decision making with the goal of maximizing cumulative utility. Because people generally weight current rewards more heavily than future rewards, we can use a parameter to discount the weight of future rewards in our decision-making process. With this goal, we can try to learn the policy that maximizes expected total utility. The policy dictates which action an actor should choose at any given state of the Markov Decision Process.

# We Can Learn the Optimal Policy through Iterative Methods
Based on the MDP, we could write an equation and solve for the optimal policy. However, this could be very difficult or impossible, depending on the specifics of the MDP. So instead, we can use dynamic programming to iteratively find the optimal policy. One such method, policy iteration, starts with a random policy and keeps evaluating and greedily improving the policy until it coverges to the optimal policy. Another method, value iteration, starts with a random value assigned to each state and greedily improves the value at each state until it converges to the optimal value. Once value iteration determines the optimal value, it determines the policy that corresponds to the optimal value. We can prove that both methods converge to the optimal value eventually.

# Model-Free Reinforcement Learning
Sometimes, we don't know everything about the MDP or we have an MDP that is too large to work with. In that case, we can use methods such as Monte Carlo and function approximation to estimate values used in finding the optimal policy.
