---
title: 'Why is Large Language Modeling not Enough?'
date: 2022-10-22
permalink: /posts/2022/10/llm_not_enough/
tags:
  - cool posts
  - category1
  - category2
---

### A Rather Long Intro

Like any tired, overworked, stressed fourth-year undergrad on a Thursday night before the midterm week, I was procrastinating by browsing Twitter and happened to run into [this paper](https://arxiv.org/pdf/2210.08340) about the so-called "NeuroAI" revolution [1]. I wasn’t surprised. In fact I got excited and downloaded the paper immediately on my iPad and started reading. 

This paper expresses the central idea that the formation of a fundamental NeuroAI research community and initiative is crucial for the development of next-generation intelligent systems. The classical Turing test based entirely on linguistic abilities / behavioral measures of performance metrics fails short in probing common sense, world models, and sensorimotor controls of artificial intelligent systems. This is something I felt strongly about while my friends were showing me gibberish, nonfactual, and “degenerate” text from the OpenAI GPT-3 Playground, albeit its impressive performances in language generations and the SuperGLUE benchmark [2].

As far as I know, current pre-trained large language models (LLMs) are almost entirely based on the idea of distributional semantics: the meaning of a word in a sequence is defined by all the words around it. This idea is directly built into the unsupervised learning objective of word2vec, masked language models (e.g. BERT), and causal language models (e.g. GPT-3) (see appendix). So if we consider the statistical model $(\Omega,\mathcal{P})$, where $\Omega$ is the space of all possible sequences and $\mathcal{P}:=\{\mathbb{P}_\theta:\theta\in\Theta\}$ is the set of probability measure on $\Omega$, then a language model is no more than an element of the set $\mathcal{P}$ parametrized by the learnt $\theta$ under the probabilistic interpretation. It already occurs to me that estimating the true underlying probability distribution over $\Omega$ is a bizarre idea. It seems to be philosophically questionable if such a distribution even exists out there in the world——but of course there is an empirical distribution if you consider the entire Internet.

Nevertheless, this probabilistic approach seems to be the most successful one so far, attracting enormous social attentions and concerns. I happen to have taken the class DS-GA 1011 Natural Language Processing with Representation Learning by Prof. Kyunghyun Cho at NYU about “a matrix factorization view of NLP models”. I thought it would be interesting to review it in light of the recent NeuroAI paper and to highlight what I think are some of the limitations of the SOTA and scaling law oriented developments in AI research:

### Notes from NYU DS-GA 1011 Natural Language Processing with Representation Learning: Lecture 9 - Matrix Factorization [3]

Consider a word $w_i$ from the set of vocabulary $V$. We would like to ask the question that which words does $w$ appear together with. 

Let $\phi(w_i)\in\mathbb{R}^{\vert V \vert \times 1}$ be a feature vector of $w_i$ and $\phi(w_i)_j$ be the count of the word $j$ appearing in the context of $w$, where the context in this case could be the same sentence, i.e. $\phi(w_i)_j$ is the co-occurence vector of $w_i$. 

We can then define the following large and sparse centered co-occurence count matrix $\tilde A\in\mathbb{R}^{\vert V\vert \times\vert V\vert }$:

$$
\tilde A=
\begin{bmatrix}
\phi^\top(w_0)-\mu^\top\\
\phi^\top(w_1)-\mu^\top\\
\vdots\\
\phi^\top(w_{\vert V\vert -1})-\mu^\top\\
\end{bmatrix},
$$

where $\mu=\frac{1}{\vert V\vert }\sum_{i=1}^{\vert V\vert }\phi(w_i)$ is the mean vector. For a word embedding matrix $U\in\mathbb{R}^{\vert V\vert \times d}$ and a context embedding matrix $V\in\mathbb{R}^{\vert V\vert \times d}$ with $d<<\vert V\vert ,$ we have the following PCA objective via the minimization of reconstruction error: 

$$
\min_{U,V}\vert \vert \tilde{A}-UV^\top\vert \vert _F^2
\\=\sum_{i=1}^{\vert V\vert }\sum_{j=1}^{\vert V\vert }\bigg[\tilde{\phi}(w_i)_j-u^\top_i v_j\bigg]^2
$$

where $\tilde{\phi}(w_i)_j$ is the count of the $j$-th word as contexts appear together with the $i$-th word after subtracting the mean. Essentially, we are using $u_i^\top v_j$ to approximate $\tilde{\phi}(w_i)_j$, i.e. using two low rank matrices to approximate the centered word-occurence matrix. 

To make the scenarios more applicable to the NLP task, consider the new matrix $A\in\mathbb{R}^{\vert V\vert \times \vert V\vert ^n}$.  $\vert V\vert $ is the possible number of vocabulary, and $\vert V\vert ^n$ is the possible number of n-gram co-occurence for the vocab $v_i\in V.$ The n-gram here is a sequence of n consecutive words, i.e. it can be thought of as a sentence. For $\tilde{A}=A-\mu$, we have again the following PCA objective. 

$$
\min_{U,V}\vert \vert \tilde{A}-UV^\top\vert \vert _F^2
$$

with $U\in\mathbb{R}^{\vert V\vert \times d}$, $V\in\mathbb{R}^{\vert V\vert ^n\times d}$. Notice that $V$ is extremely impractical to estimate. In fact, lots of the rows of $V$ are gonna be all zeros. We can then proceed to make a parametrization of $V$. The traditional continuous bag of word (CBOW) model gives

$$
V_{ij}=V'_{ij_1}+V'_{ij_2}+\cdots+V'_{ij_n},
$$

where $j=(j_1,...,j_n)$, $V'\in\mathbb{R}^{\vert V\vert \times d}$. Here $j$ refers to one particular n-gram. We have only one $V'$ matrix. Here the ordering information is ignored as addition doesn’t preserve the ordering information. Then we have

$$
\sum_{i=1}^{\vert V\vert }\sum_{j=1}^{\vert V\vert ^n}
\bigg[
\tilde\phi(w_i)_j-u_i^\top\bigg(\sum_{n'=1}^{n}V'_{jn'}\bigg)
\bigg]^2
$$

If we parametrize $V$ by a neural network, we have

$$
\sum_{i=1}^{\vert V\vert }\sum_{j=1}^{\vert V\vert ^n}
\bigg[
\tilde\phi(w_i)_j-u_i^\top F_\theta(j)
\bigg]^2
\\=\sum_{i=1}^{\vert V\vert }\sum_{j=1}^{\vert V\vert ^n}
\bigg[
\bigg(\phi(w_i)_j-\mu_j\bigg)-u_i^\top F_\theta(j)
\bigg]^2
\\=\sum_{i=1}^{\vert V\vert }\sum_{j=1}^{\vert V\vert ^n}
\bigg[
\phi(w_i)_j-\bigg(u_i^\top F_\theta(j)+\mu_j
\bigg)\bigg]^2
$$

Here $j$ is the n-gram. $F_\theta(\cdot)$ can be a neural network like BERT, LSTM etc. We take as input an n-gram, then the neural network $F_\theta(j)$ is gonna summarize the n-gram into a single vector, and the $u_i$ is now a class embedding.

### So What’s the Problem?

Consider the asymptotic scaling limit of the model $F_\theta(\cdot)$. It looks like, at least from the PCA point of view, we’re just approximating the asymptotic n-gram word-occurence matrix $A$ better and better over time. Needless to say, the resulting model will be a powerful intelligent system of its own, capable of impressive language generation, question answering, classification, code generation performance. Nevertheless, it seems to be limited if we do not accept the claim that distributional semantics is all that there is about the world. By the authors in the NeuroAI paper, we have

> “Many of the errors that current natural language processing systems make illustrate a fundamental lack of semantics, causal reasoning and common-sense. Words only have meaning for these models by virtue of their statistical co-occurrence, as opposed to their grounding in real-world experiences, so even the most advanced language models, despite their increasing power, continue to struggle with some basic aspects of physical common sense. Thus, the Turing test, as originally formulated, does not probe the ability, shared with animals, to make sense of the physical world in a flexible way “ [1].
>

### How does NeuroAI help?

The fact that our brains exist, and that it looks implausible our brains assign an objective probability measure on the space of sequences for speech production, implies the existence of a more efficient and powerful algorithm for natural languages. It’s hard to say how neuroscience and AI will come to a productive synergy for the advancement of both fields, but history has already shown us fruitful interchanges between disciplines will only bring more insights to both. 

It’s possible that all of my ramblings above looks absolutely erroneous ten years from now, but this paper at least inspire me to try to explore both side of the worlds. It’s hard to hold on to one’s ideal and intuition with other people’s discouragements. I felt like this particularly while getting a CS degree at NYU——people around me just say I shouldn’t do computational neuroscience and should take machine learning classes ASAP if I want to do machine learning. But here I am, excited by comp neuro and in general interesting research ideas. 

I would like to end this blog post by my scribbings on the NeuroAI paper, which I relate quite a lot.

![IMG_0903.jpg](https://yilunkuang.github.io/files/images_for_blogs/neuroai_paper_last_page.jpg)

**Reference** 

[1] [Toward Next-Generation Artificial Intelligence: Catalyzing the NeuroAI Revolution](https://arxiv.org/abs/2210.08340)

[2] [SuperGLUE Leaderboard](https://super.gluebenchmark.com/leaderboard)

[3] [DS-GA 1011 (Fall 2021) - Lecture 9 - Matrix factorization and language modeling](https://www.youtube.com/watch?v=buzWAgo_dKM&list=PLdH9u0f1XKW_s-c8EcgJpn_HJz5Jj1IRf&index=9)

**Appendix**
To be filled in.