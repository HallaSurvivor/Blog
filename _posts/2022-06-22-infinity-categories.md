---
layout: post
title: $\infty$-Categories and Model Categories
tags:
  - oo-categories
---

The title of this post is slightly misleading. It will be almost entirely
about $\infty$-categories, but it _will_ have a focus on how 
$\infty$-categories solve some of the formal problems with model categories
that we outlined in [part 1][1] of this trilogy.

That said, let's have a quick recap.

---

The setting we're interested in is a category $\mathcal{C}$ equipped with
some arrows $\mathcal{W}$ that morally _should_ be isomorphisms, but which
aren't (these are called _relative categories_).
The quintessential examples are the (weak) homotopy equivalences in 
$\mathsf{Top}$, and the quasi-isomorphisms of chain complexes.

We want to build a new category 
(called the <span class=defn>Homotopy Category</span> or <span class=defn>Localization</span>)
$\mathcal{C}[\mathcal{W}^{-1}]$ where we freely invert all the arrows in 
$\mathcal{W}$. The issue is that this category is quite badly behaved. 
For instance, even if $\mathcal{C}$ is (co)complete, 
$\mathcal{C}[\mathcal{W}^{-1}]$ almost never is. 

A [model structure][2] on a pair $(\mathcal{C}, \mathcal{W})$ is a choice of
two new families of arrows, called <span class=defn>fibrations</span> and
<span class=defn>cofibrations</span>, plus axioms saying how they relate to 
each other and to the weak equivalences $\mathcal{W}$.

A model structure on $(\mathcal{C}, \mathcal{W})$ solves many of the 
computational problems with $\mathcal{C}[\mathcal{W}^{-1}]$. For instance,
now the homotopy category is guaranteed to be locally small, and we have 
effective techniques for computing compute homotopy (co)limits, 
derived functors, and guaranteeing that two relative categories have
equivalent localizations. All of these techniques go through 
_bifibrant replacement_, which is a generalization of the familiar 
projective and injective resolutions from homological algebra. 

Unfortunately, as we noted at the end of the last post, model categories are
not without flaws. As soon as you want to talk about relationships _between_
model categories, you start running into trouble.

For instance, there's no good notion of a functor between model categories,
which is already annoying. But this spreads to cause issues even if one 
only cares about a single model category.
For instance, there's many constructions
that should be functorial, but aren't (the [mapping cone][3], for example).

What, then are we to do? The answer is to fully accept homotopy theory as 
part of our life, and to move to a notion of "category" which is better 
equipped to handle the geometry which is implicit in the machinery of 
model categories.

---

TODO: follow Lurie's AMS paper introducing $\infty$-categories
(mention there are _lots_ of definitions, we'll handle this in part 3)

TODO: define the hammock localization of a relative category

TODO: define the nerve localization of a model category

TODO: oo-functors, oo-(co)limits

TODO: in fact, we can redo all of CT!

TODO: what is the precise relationship between relative categories and 
oo-categories? do we lose anything when we make this upgrade?

TODO: notice that oo-functors, suitably truncated, define functors on the 
homotopy category [here][4]



[1]: part 1
[2]: model structure
[3]: https://math.stackexchange.com/questions/2219726/what-is-an-example-showing-the-failure-of-the-functoriality-of-the-cone-construc
[4]: https://kerodon.net/tag/005Z
