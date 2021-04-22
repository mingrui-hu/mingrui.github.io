---
layout: post
title:  "Varational Inference High Level Explanation"
categories: varational methods
---

[OriginalLink](https://www.cs.jhu.edu/~jason/tutorials/variational.html)

# VI Intuition:

- ignore variable interactions or handle them as efficient as much

# Example:
- Speech IR, VI intuition: 

- - bag of word assumption 

  - calculate relevance of the expectation instead of the expected relevance.
    i.e. $P(y|\mathbb{E}(p(X))$ rather than $\mathbb{E}(P(y|X))$

> This is essentially a variational approximation, because it pretends that the count of "pen" is independent of the count of other word types. 

> Formally, we're approximating the lattice using a simple family Q of distributions over bags of words: in these distributions, p("pen") at one position is independent of p("sill") at the next position. What the forward-backward algorithm is doing is to find the best approximation q in this family (for some sense of "best").

> In short, once we throw away the interactions between different terms
>
> 