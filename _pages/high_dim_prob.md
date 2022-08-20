---
layout: archive
title: ""
permalink: /notes/high_dim_prob
author_profile: true
---

# High Dimensional Probability: An Introduction with Applications in Data Science - Notes

## Chapter 0 - Appetizer: Using Probability to Cover a Geometric Set

### Introduction

This section uses high dimensional probability as a tool to solve the covering problems for motivation of the later chapters. 

### Preparation

**Definition:** A convex combination of points $z_1,...,z+m\in\mathbb{R}^n$ is a linear combination with coefficients that are non-negative and sum to $1$, i.e. it is a sum of the form

$$
\sum_{i=1}^{m}\lambda_iz_i\text{ where } \lambda_i\geq0\text{ and }\sum_{i=1}^{m}\lambda_i=1
$$

**Definition:** The convex hull of a set $T\subset\mathbb{R}^n$ is the set of all convex combinations of all finite collections of points in $T$:

$$
\text{conv}(T):=\{\text{convex combinations of }z_1,...,z_m\in T\text{ for }m\in\mathbb{N}\}
$$

### Theorem 0.0.1  (Caratheodory’s Theorem)

Every point in the convex hull of a set $T\subset \mathbb{R}^n$ can be expressed as a convex combination of at most $n+1$ points from $T$.

**Proof:**

Assume there could be $k>n+1$ points and prove by contradiction. 

### Theorem 0.0.2  (Approximate Form of Caratheodory’s Theorem)

Consider a set $T\subset\mathbb{R}^n$ whose diameter is bounded by 1 $(\text{diam}(T):=\sup\{\|\|s-t\|\|_2:s,t\in T\})$. Then for every point $x\in\text{conv}(T)$ and every integer $k$, one can find points $x_1,...,x_k\in T$  such that

$$
\bigg|\bigg|x-\frac{1}{k}\sum_{j=1}^kx_j\bigg|\bigg|_2\leq\frac{1}{\sqrt{k}}
$$

**Proof:**

Expand and bound  $\mathbb{E}\Bigg[\bigg\|\bigg\|x-\frac{1}{k}\sum_{j=1}^kZ_j\bigg\|\bigg\|_2^2\Bigg]$where $Z_1,...,Z_k$ are samples from the random vector $Z$ such that $\mathbb{P}[Z=z_i]=\lambda_i$, where $\lambda_i$ is the coefficients in the convex combination. In other words, treat vectors $x_i$ in the convex combinations as samples from a probability distribution of a random vector $Z$. 

### Corollary 0.0.4 (Covering Polytopes by Balls)

Let $P$ be a polytope in $\mathbb{R}^n$ with $N$ vertices and whose diameter is bounded by 1. Then $P$ can be covered by at most $N^{\lceil 1/\epsilon^2\rceil}$ Euclidean balls of radius $\epsilon>0$. 

**Proof:** 

Apply Theorem 0.0.2