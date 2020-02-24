---
title: "Feedforward Networks"
draft: true
weight: "4"
katex: true
---

### Introducing Feedforward Networks
- Up to now, we've been discussing neural networks where the output from one layer is used as input to the next layer
- These multilayer perceptrons are *feedforward* neural networks
- These models are called feedforward because information from $x$ flows through the intermediate computations defined by a function $f$ to produce the output $y$
- In other words, information is only fed forward and never fed back
- Networks that include feedback connections are called *recurrent* neural networks

### Motivating Feedforward Networks
- We assume that data is created by a data-generating process
- A data-generating process is the unknown, underlying phenomenon that creates the data
- This data-generating process is modeled by a true function
- We'll refer to this true function as $f^{*}$

### Defining Feedforward Networks
- The goal of a feedforward network is to approximate some unknown function $f^{*}$ with $f$
- In this case, $f^{*}$ is the unknown, optimal classifier that maps an input $x$ to a category $y$
- In this case, $f$ is a known, approximated classifier that maps an input $x$ to a category $y$
- In other words, we estimate $f^{*}(x)$ with $f(x;\theta)$
- A feedforward network defines a mapping $y=f(x;\theta)$ and learns the value of the parameters $\theta$ that result in the best function approximation

### Representing Feedforward Networks
- Feedforward networks are typically represented by composing together many different functions
- For example, the output values of our feedforward network may be defined as a chain of three functions:

$$ f(x) = f^{3}(f^{2}(f^{1}(x))) $$

- Where $f^{1}$ is called the first hidden layer
- Where $f^{2}$ is called the second hidden layer
- Where $f^{3}$ is called the output layer

### Training Feedforward Networks
- $f$ models the training data
- $f$ does not model the data-generating process
- $f^{*}$ models the data-generating process
- We want $f(x)$ to match $f^{*}(x)$
- The training data provides us with noisy, approximate examples of $f^{*}(x)$ evaluated at different training points
- Each example $x$ is accompanied by a label $y \approx f^{*}(x)$
- In other words, we hope that the training data $x$ produce training labels $y$ that are close to $f^{*}(x)$

### Training Layers of Feedforward Networks
- The training data directly specifies what the output layer must do at each point $x$
- The goal of the output layer is to produce a value that is close to $y$
- We don't want the output layer to produce a value that is always equal to $y$, since we would be overfitting the noise
- The behavior of the other layers (i.e. hidden layers) is not directly speciﬁed by the training data
- The goal of the hidden layers is not to produce a value that is close to $y$
- Instead, the goal of the hidden layers is to help the output layer produce a value that is close to $y$
- In other words, the learning algorithm must decide how to use these hidden layers to best implement an approximation of $f^{*}$
- These layers are called *hidden layers* because the training data does not show the desired output for each of these layers

### Representing Nonlinear Functions of X
1. SVM using kernel functions
2. Decision trees
3. Deep learning using activation functions

### References
- [Feedfoward and Multi-Layer Perceptron Networks](http://www.deeplearningbook.org/contents/mlp.html)
- [Architecture of Feedforward Networks](http://neuralnetworksanddeeplearning.com/chap1.html#the_architecture_of_neural_networks)
- [Lecture about Data-Generating Processes](https://cs230.stanford.edu/section/7/)
- [Blog Post about True Models](https://forecasting.svetunkov.ru/en/2016/06/25/true-model/)
