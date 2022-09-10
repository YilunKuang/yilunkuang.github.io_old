---
title: 'Debugging as a Scientific Endeavour'
date: 2022-09-10
permalink: /posts/2022/09/debug/
tags:
  - cool posts
  - category1
  - category2
---

Debugging with access to limited error log (e.g. error traceback) is exactly like a scientific problem. With a fixed set of parameter configurations and a finite sample of error logs, you are required to figure out the causal mechanism underlying the error.

In the beginning you will be fooled by the details and correlations presented to you just like the patches of similarity in the *Ditz Double Cat-spread* Jigsaw puzzle. You will propose hypotheses, chase red herrings here and there, only to be defeated again and again and gradually humble yourself in front of the bigger picture. You are an inference machine, constantly and iteratively updating your posterior measures in your hypotheses facing new evidences, as you explored more uncharted areas of the puzzle map.

Fortunately in the case of debugging, you can (sometimes) cheat by having full access to the program and gather more and more causal observations by logging everything you need to know. Most of the time in natural and social sciences, however, full causal access is simply impossible, and we propose a varieties of approaches and technicalities to tackle the problem we're interested in solving. Neuroscientist might struggle to understand a microprocessor if not carefully minded [1], just like foxes and hedgehogs can fail to differentiate between signals and noises in the market [2]. Another day of me cannot stop philosophizing:

> "There is no such thing as philosophy-free science; there is only science whose philosophical baggage is taken on board without examination" [3]. 


### Reference

[1] Jonas, E., & Kording, K. P. (2017). Could a neuroscientist understand a microprocessor?. PLoS computational biology, 13(1), e1005268.

[2] Silver, N. (2012). The signal and the noise: Why so many predictions fail-but some don't. Penguin.

[3] Dennett, D. C., & Mittwoch, U. (1996). Darwin's dangerous idea: Evolution and the meanings of life. Annals of Human Genetics, 60(3), 267-267.

<!-- This post will show up by default. To disable scheduling of future posts, edit `config.yml` and set `future: false`.  -->
