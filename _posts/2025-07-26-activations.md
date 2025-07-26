---
layout: post
title: "The Effect of Different Activation Functions on Neural Network Performance"
date: 2025-07-26 00:00:00
categories: Math 
author: 'Nishanth Tharakan'
---

<script type="text/x-mathjax-config">
MathJax.Hub.Config({
tex2jax: {
inlineMath: [ ['$','$'], ["\$$","\$$"] ],
processEscapes: true
}});
</script> 

<script type="text/javascript" charset="utf-8"
src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML,
https://vincenttam.github.io/javascripts/MathJaxLocal.js"></script>


Activation functions are crucial components of neural networks, introducing non-linearity to enable the learning of complex patterns. The selection of an activation function significantly impacts a model's training dynamics and final performance. This study explores various popular activation functions and evaluates their effectiveness across different neural network architectures and datasets.

The activation functions examined include:
* `F.relu`: Rectified Linear Unit, commonly used and effective.
* `F.gelu`: Gaussian Error Linear Unit, a smoother approximation of ReLU.
* `F.elu`: Exponential Linear Unit, which helps mitigate vanishing gradients.
* `F.leaky_relu`: Leaky ReLU, addressing the "dying ReLU" problem.
* `F.selu`: Scaled Exponential Linear Unit, a self-normalizing function.
* `F.sigmoid`: Squashes values between 0 and 1, useful for binary classification.
* `F.tanh`: Hyperbolic Tangent, squashes values between -1 and 1 and is zero-centered.
* `F.softplus`: A smooth approximation of ReLU.
* `F.softsign`: A smoother, non-saturating alternative to tanh.
* `F.mish`: A smooth, non-monotonic, and self-regularizing function.
* `F.hardswish`: A computationally efficient approximation of Swish.
* `F.hardsigmoid`: A computationally efficient approximation of sigmoid.
* `F.logsigmoid`: The logarithm of the sigmoid function, useful for numerical stability.
* `F.softmax`: Converts a vector into a probability distribution, essential for multi-class classification.
* `F.log_softmax`: Applies softmax followed by a logarithm.
* `F.threshold`: Applies a simple thresholding operation.
* `F.relu6`: A bounded version of ReLU, often used in quantized networks.
* `F.celu`: Continual Exponential Linear Unit, another ELU variation.
* `F.glu`: Gated Linear Unit, a gating mechanism used in advanced architectures.

The study evaluated these functions on:
* A simple Graph Neural Network (GCN) on the Karate Club dataset (node classification).
* A simple Feedforward Neural Network on the MNIST dataset (image classification).
* A Graph Neural Network on the Cora dataset (semi-supervised node classification).
* A Graph Neural Network on the MUTAG TUDataset (graph classification).

The experiments aimed to visualize activation function characteristics, compare performance metrics, identify trends, and provide insights into appropriate selection for deep learning problems.

The python notebook with the code can be found [here](https://colab.research.google.com/drive/1PolZJUoEdWzS9RR1ecFMbrPCkKmos1f-?usp=sharing). Credit should be given to the [PyTorch Geometric website](https://pytorch-geometric.readthedocs.io/en/latest/index.html), for the GNN models, datasets, and example code that I used to help make this work.

As I find more useful datasets and models, I will add them to the notebook and you'll also be able to see the changing performance.