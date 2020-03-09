---
title: "Backpropagation"
draft: true
weight: "9"
katex: true
---

### Motivating Backpropagation
- One goal of backpropagation is understanding how changes in the weights and biases lead to changes in a cost function
- This process involves computing partial derivatives $\frac{\partial J(w,b)}{\partial w}$ and $\frac{\partial J(w,b)}{\partial b}$

### Defining Notation
- The output of some activation function of the $j^{th}$ neuron in the $l^{th}$ layer is directly related to the output of the activation function in the $(l-1)^{th}$ layer
- We'll refer to the output of an activation function as:

$$ a^{l} = f(w^{l}a^{l-1} + b^{l}) $$

- In other words, the output of an activation function is based on the output of an activation function from its previous layer, the current weights, and some bias tern
- We can also refer to the *weighted input* to the neurons in the $l^{th}$ layer as the following:

$$ z^{l} \equiv w^{l}a^{l-1} + b^{l} $$

- In other words, a $z^{l}$ term refers to the input going into our activation function of the $j^{th}$ neuron in the $l^{th}$ layer

---

### tldr

---

### References
- [How Backpropagation Works](http://neuralnetworksanddeeplearning.com/chap2.html)
- [6.2 Gradient-Based Learning](http://www.deeplearningbook.org/contents/mlp.html#pf6)
