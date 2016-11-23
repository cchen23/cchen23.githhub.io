---
layout: post
title: "AI/ML: Word Embeddings"
date: 2016-10-22
sources: Lecture
type: summary
---

## Motivation: How Can We Use Word Embeddings?
Word embeddings use numerical vectors to represent words. We can then use these vectors to measure things such as the similarities between two different words or to measure ways in which different words relate to each other.

## Method: How to Compute Word Embeddings
One way to compute word embeddings involves looking word co-occurences -- for each word, its corresponding vector captures information about the distribution of words that occur near it (for example, the words that occur within three words of this word in a sentence). One way to implement this involves using a vector that holds the number of times a given word occurred with every other word.

### Problem: Some Words Don't Add Much Information
Some words occur very frequently with other words, but this co-occurence might not give a lot of information -- for example, "the" occurs with a lot of other words, but doesn't tell us much about the meanings of the words it occurs with. Therefore, just looking at how frequently words co-occur might not be the best way to compute vectors from words.

#### Solution: Look at How Much Information Co-Occurences Give
To solve this problem, we can use a metric called pointwise mutual information, which involves the probability that two words co-occur as well as the probabilities that each word appears on its own. By using the probabilities of each individual word occurring, this method captures the information gained from knowing that these two words occurred together.

### Problem: Word Vectors are Too Big and Sparse
Using vectors that correspond to every single word that a given word might occur with means that word embeddings consist of very long and sparse vectors -- there are lots of possible words, and each word occurs with a relatively small number of them.

#### Solution: Use Dense Embeddings
To address this problem, we can use vectors with fewer dimensions to represent each word. We can use gradient descent to learn new vector representations of words -- these new representations try to capture as much information about the word co-occurrences as possible while taking up much less space than the alternative.
