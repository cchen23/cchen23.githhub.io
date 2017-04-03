---
layout: post
title: "NN: Parallel and Distributed Algorithms"
date: 2017-04-02
type: summary
---

For efficiency, we can parallelize computations and use distributed algorithms when training the neural network.

## Training in Convolutional Neural Networks

### Kernel as a Matrix

One method involves representing the kernel of a CNN as a vector and performing convolution using matrix multiplication. This wastes memory, since pixels in the image are repeated in the matrix representation of the input image, but it allows us to take advantage of BLAS' fast matrix operations.

### Manual Optimization

Another method involves optimizing the convolution computation to take advantage of things such as vectorization and localization. This requires more work, but allows us to design faster computations.

### Fast Fourier Transform

By using FFT to perform convolution, we can increase the efficiency of convolution by reusing computations. This provides a bigger advantage for larger kernels, so it is generally used with convolutions involving large kernels.

## Distributed Computation

Sometimes, neural networks are too large to fit in the RAM of a GPU, so we use distributed nodes to train the network. We can divide each minibatch across multiple nodes, each of which computes the gradients based on its examples. A central node receives these gradients. In synchronous update methods, the central node computes the gradient based on the gradients it receives and each node updates its neural network at the same time -- on every node, the neural network is the same. In methods with asynchronous updates, each node periodically synchronizes with the central node, but not necessarily at the same time as all the other nodes -- each node might have a slightly different network, but this allows for more efficient computation.
