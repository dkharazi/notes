---
title: "Causal Inference"
draft: true
weight: "12"
katex: true
---

### Describing Causal Inference
- Correlation is defined as the association (or dependence) between two variables (typically referring to a linear relationship)
- Causation is defined as the cause of one variable results in an effect in the other variable
- Correlation is not causation
- Not even statistical dependence is causation
- At best, both of these statements tell us that there's an association between two variable, but not necessarily causation

### Examples of Correlation but not Causation
- Confounding variables
	- This happens when a third variable causes our response and predictor variable
	- For example, ice cream sales and homicide rates are correlated, but the relationship is not causal (i.e. ice cream sales and homicides are most likely caused by weather)
- Reversed causality
	- This happens when our predictor variable actually causes our response variable
	- An example of this is saying autism causes vacciations, rather than vaccinations cause autism

### Testing Correlation and Causation
- Determining correlation between two variable involves simpler statistical testing, such as hypothesis testing
- Determining causation between two variables involves complicated statistical testing in a completely controlled environment using AB testing

### References
- [Probability, Statistics, and Stochastic Processes](http://bactra.org/prob-notes/srl.pdf)
- [Causality Wiki](https://en.wikipedia.org/wiki/Causality)
- [Correlation is not Causation](https://rationalwiki.org/wiki/Correlation_does_not_imply_causation)
