---
layout: post
title: "Memory: Learning in Neural Networks"
date: 2017-02-09
sources: lecture
type: summary
---

Neural networks learn by changing the weights of connections between neurons. Ideally, by changing these weights, neural networks can learn to represent various concepts in the world.

## Hebbian Learning
In hebbian learning, connections between neurons that fire in sync strengthen and connections between neurons that fire out of sync weaken. This strengthens connections between concepts that correlate with each other in the world.

This occurs in a competitive environment: not all neurons can be active at the same time, so neurons compete with each other to be active. This means that a set of input neurons fire in sync with the neuron that is mostly strongly activated, so the neurons activated in the input will have stronger connection to the most strongly activated neuron in the next layer (rather than any neuron that is at all activated).
With hebbian learning, neural networks can learn to represent general concepts. However, because learning only depends on whether neurons fire in or out of sync, hebbian learning makes neural networks represent similar concepts with the same neuron. This prevents the neural network from determining more fine-grained distinctions between similar concepts.

## Error-Driven Learning
Error-driven learning addresses this problem by modifying the learning algorithm. Instead of simply strengthening connections between in-sync neurons and weakening connections between out-of-sync neurons, this method adjusts weights based on prediction errors. When the neural network receives a set of input activations, it looks at the next layer for neuron(s) activated by the inputs. The connections of the neurons activated in the next layer correspond to a prediction of which input neurons *should* be activated based on the activations in the next layer. Error-driven learning compares the predicted inputs with the actual inputs and uses the difference to adjust the weights of the network. By doing so, error-driven learning allows the neural network to distinguish between similar concepts.
