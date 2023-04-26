---
layout: post
title: What _Are_ Categories Anyways?
tags:
  - 
---

TODO: Intro

---

# Universes of Discourse

This is probably the most common example of a category, so I won't spend
too much time on it. For completion sake, though, I need to mention it.

A category can be viewed as a universe in which other, related, objects live.
In this universe, all of our functions automatically preserve the structure
of the objects inside it!

For instance, we can collect all of the groups together into a category of 
groups, and our arrows are precisely the group homomorphisms. So if we build
an arrow in this category, we know _automatically_ that it plays nice with
the group structure! Similarly there are categories of monoids, vector spaces,
etc.

Indeed for _any_ set of symbols $\sigma$[^1] and for _any_ set of axioms using
those symbols, we get a category whose objects are [models][2] of those axioms!
That is, sets equipped with operations and relations allowing us to interpret
the symbols in $\sigma$, and which make the axioms true!

<div class=boxed markdown=1>
For instance, we might choose $\sigma = \{+, -, 0, \leq\}$. Then we might 
choose for axioms

- $\forall x . x+0 = x = 0+x$
- $\forall x . x + (-x) = 0 = (-x) + x$
- $\forall x,y,z . (x+y)+z = x+(y+z)$
<br>
- $\forall x . x \leq x$
- $\forall x,y . x \leq y \land y \leq x \to x = y$
- $\forall x,y,z . x \leq y \land y \leq z \to x \leq z$
- $\forall x,y,z . x \leq y \to x+z \leq y+z$
<br>
- For every $n \in \mathbb{N}$, add an axiom saying 
  $\forall x . \exists y . \underbrace{y + y + \cdots + y}_{n \text{ times}} = x$

If we collect together the category of models of this theory, we get exactly
the category of ordered divisble groups with monotone group homomorphisms.

It's clear that no matter which symbols we want, and which axioms we ask for
as part of our theory, the collection of models always assembles into a category, 
which is the "universe of discourse" for that theory.
</div>

For instance, in this way we also get the category of topological spaces,
the category of partial orders, and many more.

## Functors Between Universes

When viewing categories as univeres of discourse, a [functor][3] is a 
method for _translating_ one type of object into another type of object.
That is, translating from one universe into another. This is useful because
we can often take a hard problem, translate it into a problem in another 
universe, and solve it there where it's easier.

One fruitful example of this comes from [Algebraic Topology][4][^2]. How
can we show that there is no continuous map from $D^2 \to S^1$? Or, more 
generally, from $D^n \to S^{n-1}$?

TODO: picture

Topology is "squishy" in the sense that there are LOTS of continuous functions!
This makes it hard to argue that there is _no_ continuous map $D^2 \to S^1$
since continuous maps can be extremely complicated and hard to visualize!
So we solve our problem by first _translating_ it into a more rigid world,
where maps are easier to understand: the world of groups.

Indeed, there's a functor $\pi_1$, called the [fundamental group][5]
which assigns to each topological space a group. Then if we had a map 
$D^2 \to S^1$, by functoriality it would give us maps

$$\pi_1 S^1 \to \pi_1 D^2 \to \pi_1 S^1$$

which compose to the identity.

But you can compute that this sequence is

$$\mathbb{Z} \to \{ e \} \to \mathbb{Z}$$

and clearly this composite _must_ be the $0$ map (in particular, it can't 
be the identity on $\mathbb{Z}$). So no such retraction exists!

By moving from a "squishy" world (like $\mathsf{Top}$) to a "rigid" world 
(like $\mathsf{Grp}$) we were able to show that something can't exist!
There are many many more examples like this, and much of the field of 
algebraic topology is about constructing these functors which toe the line 
between _remembering_ a lot about the space we started with, while still 
outputting something rigid that we can make computations with.

## Products and Coproducts



## Language Coming from the Universe Perspective

Since the view of categories as "universes of discourse" was _so_ foundational,
there's LOTS of terminology that comes from this. Indeed, the very notion of
"product" comes from this perspective, since it generalizes the product of 
models of some theory. The name "object" also arguably comes from this 
perspective, as does the word "category" itself (which informally means a certain 
type of object!).

TODO: say something about $\mathbb{A}^1$ in algebraic geometry, and 
products "doing the right thing"

---

# Algebraic Gadgets

A (small) category is also a model of some theory! Indeed, to talk about 
categories we use the symbols 
$\sigma = \{ \text{cod}, \text{dom}, \circ, \text{id} \}$, satisfying the axioms

TODO: write down the axioms

So a category also exists on the same level as groups, etc.

This is a fruitful viewpoint, but one which I think confuses many people!
For instance, it's quite uncommon to learn how to do computations with 
groupoids in the way we learn how to do computations with groups. But really
there's not much change!

TODO: move the discussion about monoids and matrices from the old version 
of this post to here

I have plans of writing up a post about how to build groupoids by generators
and relations, and then on making computations with this machinery. I have
no idea when I'll get around to it, though, and in the meantime you should 
read the excellent books TODO: what are the books? There's Higmann, and 
Brown, and probably another too?

TODO: say something about rings as monoids in Ab, etc.

TODO: say something about category actions, and the category of 
$\mathcal{C}$-sets is a topos! But this also lets us do functor 
homology on a standard footing.

## Functors

When we view a category as a model of some theory, a functor becomes 
exactly a homomorphism of models! Indeed, a functor is a function on
the underlying sets that respects the category structure!

It should come as no surprise that we can build a (big) category
(which acts as a universe) whose objects are (small) categories 
(viewed as algebraic gadgets). Then the arrows in this big category 
are the functors[^3].

## Products

When viewing a category as an algebraic theory, the existence of 
products/coproducts/etc. is some extra structure that we might ask for!

In the same way we might ask for a group to be abelian, and we restrict 
attention to the subcategory $\mathsf{Ab}$ of $\mathsf{Grp}$, we might
ask for our categories to have finite products, and restrict to the 
subcategory of categories with this structure. 

TODO: say something about doctrines here, and (2-)monads over Cat.

## Language Coming from the Algebraic Perspective

There's a TON of language coming from this perspective as well! Recall that 
a one object category is an algebraic object, and the arrows 
$\text{Hom}(\star, \star)$ are the elements. Then just like we can ask for 
the ability to _factor_ elements (read: arrows) in a ring
(into a product of irreducibles, say), we can ask for the ability to factor
elements (read: arrows) of a category! Some common options are the 
[epi-mono factorization][6] or the TODO: another?

This viewpoint also gives us many natural constructions _between_ categories,
like product categories, slice categories, etc. Basically any way of building
a new category from old amounts to viewing the old categories as models of 
some axioms, which we can then abstractly push around to get a new model of
those axioms.

One particualrly important special case is that of [localization][7],
whose language also [comes from rings][8]. Here we freely add inverses to 
certain arrows, just like we might freely add inverses to elements of 
a ring. This turns out to be an extremely useful thing to do, for instance 
in the construction of the [derived category][9], a central object of 
study in algebraic geometry.

We can also build "free" categories subject to certain data, or give a 
presentation of categories by generators and relations. I alluded to this 
earlier in the special case of groupoids, but this is useful in other settings 
too. For instance, the existence of "free" cartesian closed categories plays 
a crucial role in one proof of strong normalization for the 
simply typed lambda calculus. TODO: cite Jon's paper, probably?

---

# Geometric Objects

TODO: should this go _after_ the "invariants" perspective?

There are many ways to view a category as a geometric object, but we'll focus
on two here. Both take some time to get used to, but there are too many 
analogies to resist adding this viewpoint to your intuition!

The first perspective is that a category is "geometric" in some discrete sense.
In the same way that we can view a poset or a graph as a certain kind of 
"discrete geometric object"[^4], we can view a category as a discrete geometric 
object in the same way!

In this viewpoint, an object of the category is like a "point", and an arrow 
in the category is like an "oriented path" (some 1-dimensional data) connecting
the points of the space[^5]. You'll notice that, in the case of a groupoid, this 
lets us view _every_ groupoid as the fundamental groupoid of some space!



The second perspective comes from algebraic geometry, where we identify 
certain categories of invariants for a geometric space with the space itself!
Then the name of the game is to do as much geometry as possible working 
only with the category of invariants. After doing this, if we come across any
category that looks like such a category of invariants, we can fruitfully 
think about the category itself as being the underlying geometric object 
(even if no such object _actually_ exists!).

TODO: reread the intro to Alper's notes on stacks

For instance, TODO: talk about stacks, topoi, and noncommutative geometry 
(probably the dg perspective? but maybe the triangulated one)

## Functors

## Products and Coproducts

## Language Coming From the Geometric Perspective

Just like in topology we can think of certain "nice" maps $\pi : E \to B$
as a "bundle" over $B$ (that is, a family of fibres parametrized by 
points in $B$), we can view nice functors $\pi : \mathcal{E} \to \mathcal{B}$ 
as bundles!
This brings us to the notion of a [fibration][12] of categories, as well as 
the closely related notion of [displayed category][13]. 

The second geometric perspective is where we really start seeing the geometric
terminology, though. We can define open and closed [immersions][14], 
(locally) connected maps, etale maps, 

---

# Logical Gadgets

Categories are closely linked with logic in two related ways: 
They are natural _domains_ where theories live, and they also provide natural
worlds in which to _interpret_ those theories. These two viewpoints correspond 
to the _syntax_ and the _semantics_ of logic, respectively,
and it should come as no surprise that category theory is the right 
language to make precise the way in which syntax and semantics are "dual"
to each other!

TODO: say some words about functorial semantics, interpreted in Set. 

TODO: but why stop at Set? What about functors valued in some other category?
We need finite products, but that's it!

TODO: mention lawvere and gabriel-ulmer dualities

## Functors

TODO: these becomes the vehicle for _interpreting_ theories inside each other!

e.g. every ring is an abelian group. 

Then general theory tells us that our interpretations all have left adjoints,
which is a super useful fact!

## Products

TODO: eh, idk.

## Language 


----

[^1]: With specified [arity][1]

[^2]:
    This and examples like it were actually the birth of the whole 
    subject of category theory!

[^3]:
    In this category of categories, the right notion of "sameness" is 
    isomorphism! This comes as a surprise to a lot of people who have 
    been indoctrinated into thinking that weaker is always better, 
    and that we should _always_ use equivalence. 

    If we want to keep track of the data necessary to describe categories
    up to equivalence instead of up to isomorphism, then we need a big
    2-category, which keeeps the natural transformations (integral to the 
    definition of equivalence!) as part of the data.

    I actually also have a blog post on 2-categories in the pipeline,
    so hopefully we'll chat more about this soon ^_^.

[^4]:
    For instance, preorders and graphs both assemble into 
    [topological categories][10] in the sense that the "universe"
    containing all graphs (or all preorders) looks enough like the 
    universe of topological spaces to let us do a certain amount of 
    topology inside it!

    Since the universe of graphs (say) behaves like a universe of spaces,
    this justifies the idea that a single graph might behave like a 
    geometric space. In fact, with experience, this becomes a fruitful way
    to think about these things!

[^5]:
    If you're familiar with 2-categories, this extends in exactly the way you
    might expect. In fact, in 2-category theory it's fairly common to refer 
    to the objects/arrows/2-arrows as 0-cells/1-cells/2-cells (respectively),
    which mirrors the language we use for CW-complexes.
    For higher n-categories the geometric language becomes _even more_ 
    essential! 

    Eventually, at the level of $\infty$-categories, the very definition is 
    a kind of weak [kan complex][11], which is _extremely_ geometric!

[1]: arity
[2]: models like model theory
[3]: functor
[4]: algebraic topology
[5]: fundamental group
[6]: epi mono factorization
[7]: localize a cateogry
[8]: localize a ring
[9]: derived category
[10]: topologically concrete category
[11]: kan complex
[12]: fibration of categories
[13]: displayed category
[14]: immersion of categories (topoi?)
