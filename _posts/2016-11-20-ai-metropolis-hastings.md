---
layout: post
title: "AI: Metropolis Hastings"
date: 2016-11-20
sources: lecture, misc online sources
type: summary
---

## Using Bayesian Nets for Marginal Distributions
[Bayesian networks](https://cchen23.github.io/blog/2016/11/20/ai-bayesian-nets) give a compact representation of probability distributions. We can use this information to find marginal distributions. For example, in the following Bayesian network we can find the marginal probability that the grass is wet.

![example Bayesian network](https://upload.wikimedia.org/wikipedia/commons/thumb/0/0e/SimpleBayesNet.svg/400px-SimpleBayesNet.svg.png) 

To compute this marginal probability, we could find the probability that the grass is wet given each possible combination of whether it is raining and whether the sprinkler is on, and then sum those probabilities to find the marginal probability that the grass is wet. This doesn't take too long, since the state of the grass depends only on two other variables. However, in a more complicated Bayesian network, we might want to find the marginal probability of a variable that depends on a huge number of other variables. In that case, summing over the probabilities for all possible combinations of those variables' states could take a long time. More specifically, if a variable depends on k other variables, and each of those variables can take two possible states, then we need to compute the sum of 2<sup>k</sup> probabilities to find the marginal distribution. Therefore we want to find other ways of computing marginal probabilities.

## Special Case: Polytrees
If the Bayesian network is a polytree (meaning that the undirected version of the network graph has no cycles), then we can use dynamic programming to compute the marginal probability more quickly. In the following Bayes net, I depends upon A, B, D, G, and H. But if we wanted to find the marginal probability of I, we would not have to separately compute the probability distribution of I for each of the possible combinations of states of A, B, D, and G.

[Polytree](https://upload.wikimedia.org/wikipedia/commons/thumb/6/61/Polytree.svg/200px-Polytree.svg.png)

Instead, starting with the probability distributions of A and B, we could then compute the probability distribution of D. Using the probability distribution of D, we can compute the probability distribution of G, and using the probability distribution of G and H, we can compute the probability distribution of I. By computing each intermediate probability distribution, we can avoid computing and summing 2<sup>5<\sup> probabilities to find the marginal distribution of I.

## Approximating Marginal Distributions
However, many Bayesian networks are not polytrees. In that case, using the algorithm we used with polytrees does not work efficiently. However, we can approximate a marginal distribution by using the Metropolis Hastings algorithm.

Using this algorithm, we can sample from a marginal distribution without having to compute the exact probabilities of the distribution. Instead, we only need the ratio of the probabilities of different values of the marginal distribution, and we use these ratios to sample from the distribution.

For example, we might have a Bayes net with 5 different variables (A, B, C, D, E), and we might want to estimate the marginal probability P[A|B=b, C=c].
We could imagine a Markov chain with a state for each possible assignment of A, B, C, D, and E. We would arbitrarily pick a state for which B=b and C=c. From that state, we would randomly pick a new state for which one variable (other than B and C) had a different value, and we would move to that state with a probability equal to the ratio of probabilities between the new state and the current state. For example, if we start from state (a1, b, c, d1, e1) and choose to consider state (a1, b, c, d1, e2), we would move to the new state with probability P[A=a1, B=b, C=c, D=d1, E=e2]/P[A=a1, B=b, C=c, D=d1, E=e1]. We would repeat this process for a certain number of times, and after that number of times we would use the current state's value of A as our sample.

This algorithm approximates the marginal distribution of P[A|B=b, C=c] because the Markov chain we used has a stationary distribution equal to the marginal distribution of P[A|B=b, C=c]. In practice, the Markov models constructed in this algorithm reach their stationary distribution relatively quickly, so if we perform enough iterations within the algorithm, the Markov chain will reach its stationary distribution. Therefore when we choose our sample at the end of the iterations, we will be sampling from the stationary distribution, and we constructed the Markov model so that the stationary distribution of the Markov chain would be equal to the marginal distribution that we sought.
