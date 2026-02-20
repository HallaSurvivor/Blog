---
layout: post
title: An Overly Explicit Computation with Character Stacks
tags:
  - 
---

In the [main post][1] I go over a talk I gave today explaining how 
factorization homology relates to (quantum) character stacks. In this 
post I want to do a sample computation which gives some justification that 
the main theorem from that talk (which is *not* mine) actually does work!

Recall from that blog post that we can compute the category of sheaves on 
the character stack $\underline{\text{Ch}}(\Sigma,G)$ by integrating 
$\mathsf{B}G$ over $\Sigma$ in the sense of factorization homology:

$$
\text{QCoh}(\underline{\text{Ch}(\Sigma,G)) \simeq \int_\Sigma \text{Rep}(G)
$$

Let's take a simple surface (like the annulus) and a simple group (like 
$GL_1 = \mathbb{C}^\times$) and just... check!


[1]: /2026/02/19/talk-quantum-character-stacks.html
