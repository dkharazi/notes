---
title: "Cost Function"
draft: true
weight: "8"
katex: true
---

### Motivating Cost Functions
- We sometimes use gradient descent to train models such as linear regression and support vector machines when the training set is extremely large
- In these cases, we've been using a quadratic cost function
- However, we can use other cost functions for other purposes
- For example, we could use a cross-entropy cost function for classification problems, rather than a quadratic cost function for regression problems
- Once we determine how to represent the output of our model, we'll be able to choose a cost function to learn our weights and biases

### Introducing the Cost Function
- At the heart of backpropagations is an expression for the partial derivative $\frac{\partial J(\theta)}{\partial \theta}$ of the cost function $J(\theta)$
- Typically, $\theta$ is any weight $w$ or bias $b$ in the network
- The goal of backpropagation is to compute the partial derivatives $\frac{\partial J(w,b)}{\partial w}$ and $\frac{\partial J(w,b)}{\partial b}$ of the cost function $J(w,b)$

### Assumptions of Cost Functions
- For backpropagation to work, we need to make two assumptions about the form of the cost function:
	1. A cost function can be written as an average
	2. A cost function can be written as a function of the outputs
- For example, the quadratic cost function satisfies both assumptions:

$$ J(w,b) = \frac{1}{2m} \sum_{i=1}^{m} (h(x) - y)^{2} $$

- In other words, our cost function is an average due to the $\frac{1}{2m}$ term
- We need this assumption because backpropagation involves computin
g the partial derivatives $\frac{\partial J(w,b)}{\partial w}$ and $\frac{\partial J(w,b)}{\partial b}$ for a single training example
- Therefore, we take an average over all of these partial derivatives so our cost function is effectively able to represent a measure of these partial derivatives
- The quadratic cost function satisfies the second assumption as well because it takes in the outputs of our activations functions
- In other words, our cost function satisfies this assumption since our predictions $h(x)$ are the output of our activation functions

### Describing Cost Functions
- Up until now, we've mostly used the quadratic cost function to learn $\theta_{0}$ and $\theta_{1}$ for regression problems
- However, we can use a different cost function for classification problems, and other cost functions for other applications
- For classification problems, we can use the cross-entropy cost function:

$$ Cost(h_{\theta}(x),y) = \begin{cases} - \log (h_{\theta}(x)) &\text{if } y=1 \cr - \log (1 - h_{\theta}(x)) &\text{if } y=0 \end{cases} $$

- This is also known as the *Bernoulli negative log-likelihood* and *Binary Cross-Entropy*
- This cost function has its own gradient with respect to the output of a neural network 

---

### tldr
- A cost function is a measure of *how good* a neural network did with respect to its given training sample and its expected output
- It uses parameters, such as weights and biases, to do this
- A cost function returns a single value (not a vector) because it rates how good the neural network performs as a whole
- Cost functions typically rely on two assumptions, which are hard to enforce and usually broken
- Therefore, the only real requirement for backpropagation is that we can define gradients on all the computation steps between:
	- Weights we want to backpropagate into
	- And the cost function we want to backpropagate from
- These gradients don't necessarily need to be mathematically well defined, or even correct and unbiased (e.g. straight-through gradient estimators)

---

### References
- [6.2 Gradient-Based Learning](http://www.deeplearningbook.org/contents/mlp.html#pf6)
- [List of Cost Functions](https://jmlb.github.io/flashcards/2018/04/21/list_cost_functions_fo_neuralnets/)
- [Uses of Cost Functions](https://stats.stackexchange.com/questions/154879/a-list-of-cost-functions-used-in-neural-networks-alongside-applications)
- [Cross-Entropy and Quadratic Loss Functions](https://machinelearningmastery.com/loss-and-loss-functions-for-training-deep-learning-neural-networks/)
