---
layout: post
title: Using Ultraproducts to Solve Problems
tags:
  - 
---

An <span class=defn>Ultraproduct</span> is a construction from mathematical
logic that lets us prove (first order) statements about some family of 
structures by studying a single object which somehow captures the behavior 
of the family. In this post we'll talk about ultraproducts -- what are they,
what do they do, and most importantly how can we actually _use_ them to solve
problems?

First, what _are_ ultraproducts anyways? 

Fix a sequence of groups (say) $$(G_n)_{n \in \mathbb{N}}$$. Then we can take 
their _product_ and get a new group $\prod G_n$ with coordinate-wise operations.
We would like to modify this construction in order to get a group 
$\prod_\mathcal{U} G_n$ (called the <span class="defn">Ultraproduct</span> of the $G_n$s)
which has better [model theoretic][1] properties. We'll go deeper into the
specifics of the construction later (TODO: that) but for now, it's enough to know
that the ultraproduct has the following properties[^1]:

 - Elements of $\prod_\mathcal{U} G_n$ are (equivalence classes of) tuples $(g_1, g_2, g_3, \ldots)$,
    where $g_n \in G_n$.
 - $\prod_\mathcal{U}$ thinks that some first-order property is true if and only if all
    but finitely many of the $G_n$s do. For example, if all but finitely many of the $G_n$
    are abelian, then the ultraproduct will be abelian too, since abelianness is 
    defined by the first order sentence $\forall x . \forall y. x^{-1}y^{-1}xy = 1$.

One special case of interest is where all the $G_n$ are actually the same! 
We call this the <span class=defn>Ultrapower</span> of $G$, written $G^\mathcal{U}$.

It might seem strange that this construction is useful. After all, by the 
bullet point above, we know that $G^\mathcal{U}$ thinks that something is true
if and only if $G$ does. So isn't it just $G$? What do we gain by moving to the
ultrpower?

The answer is caught up in the "first-order" qualifier! It turns out that there
can be _lots_ of differences between $G$ and $G^\mathcal{U}$. For instance,
$\mathbb{Z}^\mathcal{U}$ is uncountable, (in particular, it is not cyclic).

To know which properties we _can_ transfer back and forth between $G$ and $G^\mathcal{U}$,
then, we need to know what it means for a property to be "first order". 
I'm going to assume some familiarity with basic model theory, but I'll include
abbreviated definitions for completeness[^2].

<div class=boxed markdown=1>
  Let $\sigma$ be a collection of "primitive symbols" which are necessary for
  talking about a given object of study. For example:

  - If we're interested in groups, we might take $\sigma = \langle 1, \cdot, {}^{-1} \rangle$ 
  - for ordered rings we might take $\sigma = \langle \leq, 0, 1, +, -, \cdot \rangle$
  - If we're interested in graphs, we might take $\sigma = \langle E \rangle$ 
    (where $E(x,y)$ says that $x$ and $y$ are adjacent)

  Then the <span class=defn>First Order Language</span> associated to $\sigma$
  (often written $\mathcal{L}(\sigma)$ (sometimes $$\mathcal{L}_\mathsf{FO}(\sigma)$$ or 
  $$\mathcal{L}_{\omega, \omega}(\sigma)$$ if we're working with multiple different
  logics at once) is the collection of formulas we can build using

  1. primitive symbols from $\sigma$
  2. connectives: $\land$, $\lor$, $\lnot$, $\to$, $\leftrightarrow$, etc.
  3. variables like $x$, $y$, etc.
  4. $=$
  5. quantifiers: $\forall x$, $\exists x$

  ⚠ our quantifiers can only quantify over _elements_ of our structure! 
  This is the "first" in "first order". 
</div>

Now we see that there's no way to write down "$G$ is cyclic" in a first order way.
The obvious idea 

$$\exists g . \forall x . \exists n \in \mathbb{Z} . g^n = x$$

doesn't work because we're quantifying over $\mathbb{Z}$, which is _not_
our structure. Similarly, we can't write

$$ \exists g . \forall x . (x = 1) \lor (x = g) \lor (x = g^{-1}) \lor (x = g^2) \lor (x = g^{-2}) \lor \ldots $$

since that is an _infinite_ string of symbols. We only allow finite 
conjunctions or disjunctions.

Lastly, given a formula $\varphi \in \mathcal{L}(\sigma)$ and a 
<span class=defn>Model</span> $\mathfrak{M} 
(that is, a set $M$ equipped with constants, operations, and relations for each
)

<div class=boxed markdown=1>
  Here are some nice exercises you might try to get familiar with first order logic:

  1. For $\sigma = \langle E \rangle$ the language of graphs, write a formula
</div>

---

- define ultraproducts, and give some motivation
- Los's theorem
- example (ultraproduct of algebraically closed fields of char p)

How have ultraproducts been used to solve problems?

- Ramsey Theory
- Nonstandard analysis

Speculative example:

- Twin primes

---

[^1]:
    Technically this is only true of _nonprincipal_ ultraproducts. 
    TODO: say more about this?

[^2]:
    Pun intended

[1]: https://en.wikipedia.org/wiki/Model_theory

