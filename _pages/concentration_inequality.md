---
layout: archive
title: ""
permalink: /notes/concentration_inequality
author_profile: true
---

# Concentration Inequality

> Concentration inequalities give probability bounds for a random variable to be concentrated around its mean, or for it to deviate from its mean or some other value——Mehryar Mohri. *Foundations of Machine Learning*

## Jensen’s Inequality

For any random variable $X$ and a convex function $f:\mathbb{R}\to\mathbb{R}$, we have

$$
f(\mathbb{E}[X])\leq\mathbb{E}[f(X)]
$$

Notice that Jensen’s Inequality is not tight. 

(Reference: High-Dimensional Probability: An Introduction with Applications in Data Science, Chapter 2)


## Markov’s Inequality

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

(Reference: Foundations of Machine Learning, Appendix D)


## **Chernoff Bound**

The Chernoff Bound is a natural extension of Markov’s Inequality. Let $X$ be any random variable over $\mathbb{R}$. For all $t\geq0$ we have

$$
\mathbb{P}[X\geq\epsilon]\leq\inf_{t\geq 0}\frac{\mathbb{E}[e^{tX}]}{e^{t\epsilon}}
$$

**Proof:**

$$
\mathbb{P}[X\geq\epsilon]=\mathbb{P}[e^{tX}\geq e^{t\epsilon}]
\leq\frac{\mathbb{E}[e^{tX}]}{e^{t\epsilon}}\leq \inf_{t\geq 0}\frac{\mathbb{E}[e^{tX}]}{e^{t\epsilon}}.\space\square.
$$

(Reference: Wikipedia)

## **Hoeffding’s Lemma**

To provide an upper bound on $\mathbb{E}[e^{tX}]$ in the Chernoff Bound above, consider the Hoeffding’s Lemma. Let $X$ be a random variable with $\mathbb{E}[X]=0$, $a\leq x\leq b$, $a<b$. For all $t>0$, we have

$$
\mathbb{E}[e^{tX}]\leq e^{\frac{t^2(b-a)^2}{8}}
$$

**Proof:**

(Reference: Foundations of Machine Learning, Appendix D)

## Hoeffding’s inequality

## Hoeffding’s Inequality for Learning Theory

Fix $\epsilon>0$. Then, for any hypothesis $h:X\to\{0,1\}$, the following inequalities hold:

$$
\mathbb{P}_{S\sim\mathcal{D}^m}\bigg[\widehat{R}_S(h)-R(h)\geq\epsilon\bigg]\leq\exp(-2m\epsilon^2)\\
\mathbb{P}_{S\sim\mathcal{D}^m}\bigg[R(h)-\widehat{R}_S(h)\geq\epsilon\bigg]\leq\exp(-2m\epsilon^2)
$$

By the union bound, this implies the following two-sided inequality:

$$
\mathbb{P}_{S\sim\mathcal{D}^m}\bigg[\bigg\vert\widehat{R}_S(h)-R(h)\bigg\vert\geq\epsilon\bigg]\leq2\exp(-2m\epsilon^2)
$$

(Reference: Foundations of Machine Learning, Chapter 2)


## McDiarmid’s inequality

## Application: JL-Lemma

For any $\epsilon\in(0,0.5)$ and any integer $m>4$, let $k=\frac{20\log m}{\epsilon^2}$. Then for any set of $V$ of $m$ points in $\mathbb{R}^N$, there exists a map $f:\mathbb{R}^N\to\mathbb{R}^k$ such that for all $\boldsymbol{u},\boldsymbol{v}\in V$,

$$
(1-\epsilon)||\boldsymbol{u}-\boldsymbol{v}||^2\leq||f(\boldsymbol{u})-f(\boldsymbol{v})||^2\leq(1+\epsilon)||\boldsymbol{u}-\boldsymbol{v}||^2.
$$

**Proof:**