---
layout: post
title: 
tags:
  - 
---

What do algebras look like in $\mathcal{T}$?

First of all, for any (essentially) algebraic theory $\mathbb{T}$, 
if we have a (sequential!) topological model (for example, a topological 
group whose underlying topology is sequential), that model is still a 
model in $\mathcal{T}$.

Indeed, the [funtorial semantics][17] perspective says that 
a topological $\mathbb{T}$-model $M$ corresponds to a finite product
functor[^2] from some classifying category $\mathcal{C}_\mathbb{T}$ to 
$\mathsf{Seq}$. Since the inclusion functor 
$\mathsf{Seq} \hookrightarrow \mathcal{T}$ is a right adjoint, it preserves 
products, and thus $M$ is still a $\mathbb{T}$-model when viewed as an 
object in $\mathcal{T}$! 

TODO: so if we constructively prove a theorem about groups, say, then 
that theorem is true inside $\mathcal{T}$. Thus, since (sequential) 
topological groups all live inside $\mathcal{T}$, we get a theorem about 
all topological groups!

And this works for basically _any_ kind of algebraic gadgets you want 
to consider!

<br>

Conversely, say we _have_ a $\mathbb{T}$-model in $\mathcal{T}$. 
That is, say we have a finite product functor 
$\mathcal{C}_\mathbb{T} \to \mathcal{T}$.
Then since the reflector $\mathcal{T} \to \mathsf{Seq}$ preserves 
finite products, the honest topological space associated to our 
object is itself a $\mathbb{T}$-model!

This tells us that if we ever want to reason about an algebraic 
object in $\mathcal{T}$, we can fruitfully pretend it's "just" a 
topological model! After all, its underlying topological space is 
still a model, and the only difference between an object in $\mathcal{T}$ 
and its underlying space is the potential for multiple proofs of convergence!

TODO: phrase that better, and tie it into your earlier discussion about 
what objects in $\mathcal{T}$ look like... In fact, maybe say something like 
this earlier in the post.

---
