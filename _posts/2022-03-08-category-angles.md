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

This post has actually been in my drafts for almost a year now[^3]
which is pretty wild to think about... I got in a discussion on 
mastodon recently that inspired me to come back and finish this up. 

I have a long train ride ahead of me anyways (I'm coming into New York City
from upstate where I spent new years eve with some friends) so let's do it ^_^.

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
in a category. There's a similar story for coproducts, direct and inverse limits, etc. 

Of course, the reason people were interested in developing universes of
discourse is so that they can develop _transformations_ that eat one kind
of object and output a new kind of object! Through this lens, these _functors_, 
like the fundamamental group $\pi_1$, essentially let us travel between 
universes in order to translate our problem into a new domain where it's 
(hopefully) easier to solve!

Lastly, the language of categories lets us express when two types of objects
are "really the same". The (anti)equivalence of categories between stone spaces
and boolean algebras is beautiful and useful. Similarly, the (anti)equivalence
of finitely generated reduced $k$-algebras with algebraic varieties led 
Grothendieck and others to define affine schemes to be opposite the category
of commutative rings. This, of course, revolutionized algebraic geometry.

---

## Algebraic Objects

Categories can also be seen as algebraic objects in their own right.

After all, a category with one object $\star$ is "just" a monoid. Our 
elements are the arrows $\text{Hom}(\star, \star)$ and multiplication is 
composition.

Through this lens, a category is a generalization where multiplication isn't
always defined. Instead we have a set of "labels" (the objects of our category)
and we can only multiply two eleemnts whose labels agree. 

To make this extremely concrete, consider the category which has natural
numbers as objects. Then the arrows $\text{Hom}(m,n)$ are exactly the 
matrices with $m$ rows and $n$ columns. 

TODO: picture

We know how to multiply matrices, but we are only allowed to do this when
the labels match up

TODO: another picture of the composite

So a category is a kind of algebraic gadget that allows us to keep track
of _which_ elements we're allowed to multiply! 

Now a functor between two categories is just a homomorphism. It's a 
structure preserving map between two algebras. Indeed, in case our 
categories both have a single object, a functor is _literally_ a 
monoid homomorphism.

For instance, a groupoid is a category where every arrow is invertible. 


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

This analogy can be pushed quite far, for instance, a ring can be viewed as
a one object category [enriched][1] in abelian groups.

More generally, it's common to _define_ a category by giving some generators
and some relations. This is entirely analogous to giving a presentation of a 
group. TODO: examples

Then there are lots of operations which we do to algebraic gadgets which we
can rephrase categorically. Oftentimes these operations end up being interesting
and useful in the broader setting!

Take, for instance, the monoid $\mathbb{N}^\times$, which has
one object $\star$, and an arrow $\star \to \star$ for each $n > 0$ so that
$m \circ n = mn$. Then there's a distinguished class of arrows (the primes)
so that every arrow _factors_ as a composite of primes.

More typically, we'll have two types of arrow, say $\mathcal{M}$ and $\mathcal{E}$,
and we want to know that every $f : A \to B$ factors as $f = m \circ e$ 
for $m \in \mathcal{M}$ and $e \in \mathcal{E}$. If every $f$ factors in this
way, we say our category has an $(\mathcal{M}, \mathcal{E})$-factorization system.


---


Algebraic
  - can be defined by generators and relations
  - factorization systems
  - (open) petri nets?
  - braid categories? (Universal web category)
  - representation, cohomology, etc
  - https://mathoverflow.net/a/43615/145247 ?
  - localization

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



"proof relevant preorder", which has algebraic, geometric, and logical content.

---

[^1]:
    We need universes of discourse so that we can talk about transformations
    (functors) between them so that we can talk about _natural_ transformations
    between _those_.

[^2]:
    I'll be following the usual tradition of ignoring foundational issues here,
    much to the disappointment of my set theorist friends, I'm sure.

[^3]:
    since March of 2022


[1]: https://en.wikipedia.org/wiki/Enriched_category
