---
title: "Linearity and Activation Functions"
draft: true
weight: "1"
katex: true
---

### Overview of Linearity
- A linear map refers to a function $f : V \to W$ that satisfies the following two conditions:
	1. $f(x+y) = f(x) + f(y); x,y \in V$
	2. $f(cx) = xf(x); c \in \R$
- This is a definition referred to in linear algebra often
- However, we can also think of linearity in terms of *linear separability*
- Linear separability means a line can be separate our data into two different classes
	- This line becomes a hyperplane if the space is greater than two dimensions
- This line represents a linear decision boundary
- Rarely do we find a physical world phenomenon that generates data that is linearly separable
- In these cases, we need to find a way to model nonlinear decision boundaries

### Linearity and Neural Networks
- To model our data using nonlinear decision boundaries, we can utilize a neural network that introduces nonlinearity
- Neural networks classify data that is not linearly separable by transforming data using some nonlinear function
- We refer to these nonlinear functions as *activation functions*
- After applying nonlinear functions to our data, our hope is that our transformed data points become linearly separable

### Brief Overview of Activation Functions
- Essentially, activation functions help introduce non-linearity in neural networks
- Different activation functions are used for different problem settings
- Here are a few examples of activation functions:
	- Tanh
	- Sigmoid
	- Re-Lu

### Decision Boundaries and Activation Functions
- The main purpose of an (nonlinear) activation function is to create a nonlinear decision boundary for a neural network
- Any decision boundary is a linear combination of polynomial combinations of the input features
- The decision boundary is not a property of the training set
- Instead, the decision boundary is a property of the hypothesis and parameters
- Specifically, the shape and position of a decision boundary is based on the weights and bias

---

### tldr
- Neural networks are good for nonlinear classification
- Neural networks use activation functions to find nonlinear decision boundaries
- Activation functions are nonlinear functions used to map our data to some space where the data becomes linearly separable
- In other words, we usually apply a linear model to a transformed input $\phi(x)$, instead of applying a linear model to $x$ itself

---

### References
- [Post about Linearity in Neural Networks](https://ai.stackexchange.com/a/5494)
- [Post about the Uses of Activation Functions](https://ai.stackexchange.com/a/5521)
- [Feedfoward and Multi-Layer Perceptron Networks](http://www.deeplearningbook.org/contents/mlp.html)
- [Activation Function Wiki](https://en.wikipedia.org/wiki/Activation_function)
- [Purpose of Activation Functions](https://stats.stackexchange.com/a/236386)
