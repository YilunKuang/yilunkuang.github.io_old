---
layout: archive
title: ""
permalink: /notes/concentration_inequality
author_profile: true
---

## Concentration Inequality

### Markov’s Inequality

If $X$ is a non-negative random variable, then $\forall\space\epsilon>0$ we have

$$
\mathbb{P}[X\geq\epsilon]\leq\frac{\mathbb{E}[X]}{\epsilon}
$$

**Proof:**

Since $X$ is a non-negative random variable, the domain of $X$ is $[0,+\infty)$. Notice that the Markov’s Inequality is a tail bound, i.e. for arbitrarily large $\epsilon$, $\mathbb{P}[X\geq\epsilon]\leq\frac{\mathbb{E}[X]}{\epsilon}$, where $\frac{\mathbb{E}[X]}{\epsilon}$ is going to be arbitrarily small for bounded $\mathbb{E}[X]$. The intuition is then to partition the probability space into two components to isolate the tail. 

$$
\mathbb{E}[X]=\int_{0}^{+\infty}xf(x)dx
=\int_{0}^{\epsilon}xf(x)dx+\int_{\epsilon}^{+\infty}xf(x)dx
\\\geq\int_{\epsilon}^{+\infty}xf(x)dx\geq\epsilon\int_{\epsilon}^{+\infty}f(x)dx=\epsilon\space\mathbb{P}(X\geq\epsilon).\space\square.
$$

### **Chernoff Bound**

The Chernoff Bound is a natural extension of Markov’s Inequality. 

### Chebyshev's inequality

### Hoeffding’s inequality

### McDiarmid’s inequality
