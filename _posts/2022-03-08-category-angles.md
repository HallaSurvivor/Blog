---
layout: post
title: What Are Categories, Anyway?
tags:
  - 
---

One obvious question is "what _is_ a category?", and the answer is 
surprisingly long. Categories have the flavor of algebraic objects,
geometric objects, and logical objects, and this cross-pollination 
is part of what makes category theory such a rich subject (and also
part of what makes it such a foreboding one). In this post I want to 
spend some time talking about all the ways I know of for thinking about
categories, and hopefully also explain what each viewpoint brings to the
table.

---

## Universes Of Discourse

This is the way that most sources introduce categories, and it's also
the way that I think a lot of mathematicians understand categories. 
This was definitely the original motivation for categories[^1], and it's
also a very useful perspective to keep in mind.

For instance, we know that we have categories of 

 - Sets and functions
 - Groups and homomorphisms
 - Topological spaces and continuous maps
 - R-modules and homomorphisms
 - (Smooth) Manifolds and smooth maps
 - Categories and functors
 - etc.

In general, most geometric or algebraic objects live inside some
ambient category with their structure preserving maps. 

This perspective is well known, so it feels a bit silly to talk about the
benefits this perspective offers, but in the interest of completeness I'll
say a few words anyways.

First, it lets us recognize similar constructions throughout mathematics,
and write them as special cases of a categorical construction applied to this
universe of discourse.

For instance, mathematicians have long had an intuitive understanding of what
a "product" of topological spaces, groups, etc. should be, and the 
_properties_ we expect a product to have. For instance, when considering the
product of two affine lines, $\mathbb{A}^1 \times \mathbb{A}^1$, we must
_not_ give this space the product topology if we want it to be the 
affine plane $\mathbb{A}^2$!

This intuition for what a "product" of objects should be was later made
precise by looking at universal properties, and a general idea of product
in a category. 

Similarly with coproducts, direct and inverse limits, etc. 

Of course, once we have universes of discourse, we have maps between them,
for instance the fundamental group functor $\pi_1$. 

Also, the language of categories lets us express when two classes of objects
are "really the same". The (anti)equivalence of categories between stone spaces
and boolean algebras is beautiful and useful. Similarly, the (anti)equivalence
of finitely generated reduced $k$-algebras with algebraic varieties led 
Grothendieck and others to define affine schemes to be opposite the category
of commutative rings. This, of course, revolutionized algebraic geometry.

---

## Algebraic Objects

Categories can also be seen as algebraic objects in their own right.

After all, one standard definition of a category _looks_ like 
a definition of an algebraic structure: 

We have

- A set[^2] of objects $O$
- A set of arrows $A$
- a map $s : A \to O$ assigning each arrow its source
- a map $t : A \to O$ assigning each arrow its target
- a map $i : O \to A$ assigning each object its identity arrow
- a (partially defined!) composition operation $\circ : A^2 \to A$ 
- a bunch of axioms saying how these operations should interact

Most simply, we can think of a group $G$ (or more generally a monoid $M$)
as a category with one object $\star$. Then all the algebraic data is
contained in the composition on $A$. Moreover, since there's only one object,
_every_ pair of arrows is composable, so $\circ$ becomes a total operation.


---

Algebraic
  - axioms (composition is an operation, subject to certain rules)
  - can be defined by generators and relations
  - groups/monoids
  - factorization systems
  - (open) petri nets?
  - braid categories? tensor products, etc
  - https://mathoverflow.net/a/43615/145247 ?

Geometric
  - objects are "points", arrows are "paths"
  - groupoids, posets
  - this is one of my first thoughts on categories
  - fibrations?

Logical
  - objects are "terms", arrows are "implications"
  - alternatively, objects are "types"
  - locales (model of a theory is a hom of locales, cf Vickers paper)
  - "classifying category"
  - functorial semantics

Invariant
  - usually a "categorified" version of a preexisting invariant
  - Rep(G), Rmod
  - can recover group/ring from the category: tanaka-krein (?), etc
  - morita equivalence
  - something about knot polynomials?
  - instead of betti numbers, we look at homology groups. Invariant categories are a higher-level version of this idea
  - At time of writing I don't feel like I fully understand this viewpoint
  - https://mathoverflow.net/a/9432/145247
  - https://www.youtube.com/watch?v=reTw27FYhlQ ?
  - category of covering spaces is equivalent to category of subgroups



---

[^1]:
    We need universes of discourse so that we can talk about transformations
    (functors) between them so that we can talk about _natural_ transformations
    between _those_.

[^2]:
    I'll be following the usual tradition of ignoring foundational issues here,
    much to the disappointment of my set theorist friends, I'm sure.
