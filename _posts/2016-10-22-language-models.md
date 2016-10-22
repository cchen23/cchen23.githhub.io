---
layout: post
title: "AI: Language Models"
date: 2016-10-22
sources: lecture; http://www.cs.columbia.edu/~mcollins/courses/nlp2011/notes/lm.pdf
type: summary
---

## Motivation: Estimate the Probabilities of Sentences
Language models contain probability distributions that can be used to estimate the probability that a given sentence occurs. This can be very useful for helping machines process human language.

## Challenge: Huge Number of Possible Sentences
There are a huge number of words, and a huge number of ways in which these words can be combined. Therefore keeping track of the probabilities of relatively long combinations of words would take a lot of space. In addition, training data comes from existing sentences, and the number of existing sentences is very small in comparison to the number of possible sentences. Therefore there is not enough data to train a model that keeps track of the probabilities of long strings of words.
### Solution: Use Low-Order Markov Models
To address this issue, low-order markov models can be used to approximate sentence probabilities. For example, a first order markov model approximates that the probabilitiy that a given word occurs in a sentence depends only on the word that came before it. This is called the bigram model. Another model, the trigram model, approximates that each word depends only on the two words that came before it in the sentence.

## Training Language Models
To train the probability distributions of language models, a corpus containing many sentences is used as training data. To train a bigram model, we would estimate the probability that a given word word follows another word. For example, to calculate the probability that the word "birthday" follows "happy", one would divide the number of times "happy birthday" occurs by the number of times "happy" occurs.
### Smoothing
A problem with this method is that pairs of words that are never seen in the corpus would be given a probability of zero. However, if a pair of words is not specifically used in a given corpus, they could still occur in other sentences. To account for this, we would pretend we saw each bigram one more time than we actually saw it, and compute probability distributions accordingly.

## Evaluating Language Models
One way to evaluate a language model involves using a set of test data that consists of a number of sentences. From each sentence, we could calculate an evaluation metric called a perplexity score. The perplexity score is calculated by taking the geometric average of the inverse probability of each bigram in a sentence -- a lower perplexity score means a better prediction.
