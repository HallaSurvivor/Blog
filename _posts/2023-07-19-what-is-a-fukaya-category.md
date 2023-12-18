---
layout: post
title: What the Hell is a Fukaya Category?
tags:
  - 
---

The [Fukaya Category][1] of a surface is a deep and interesting invariant 
with important applications to physics (in particular, to [Mirror Symmetry][2]).
They've recently shown up in my research, which is exciting and scary in 
equal measure. The definition is already pretty intimidating, and if you 
try to look up motivation and examples, you'll be met with a deluge of terms 
like "$A_\infty$ Structure", "Maslov Index", and "Novikov Field". Even just 
trying to understand the chain complex structure requires knowledge of 
(compactifications of) moduli spaces of pseudoholomorphic disks in your surface! 
It's unbelievable to me that anyone could have come up with this, or worse, 
that anyone could calculate anything to do with it! With this in mind, 
I wanted to find a different (more mathematical) motivation for the fukaya 
category, which made it feel more natural (at least to me). I'm only interested 
in the fukaya categories of surfaces 
(which I think are "toy examples" for the actual fukaya people), so it seems 
like there should be a better way to understand them.
Earlier this year I co-organized a reading group on symplectic geometry 
and fukaya categories with [Catherine Cannizzo][3], and I got to organize 
my thoughts into a talk. Now, _months_ later, I'm finally writing up a blog 
post about them. I hope this is as helpful for other people as it was for me!

---

So then, where should we start?

Let's say you're studying curves on a surface, and you have a very concrete 
question in mind:

Given two curves $\alpha$ and $\beta$, how many times do they intersect?

Of course, it's reasonable to ask for this to be homotopy invariant. You 
can always perterub to curves to make them intersect lots by wiggling

TODO: two wiggling curves intersecting a lot

So we define the <span class=defn>Geometric Intersection Number</span> 
$i(\alpha,\beta) \triangleq \min_{\alpha', \beta'} | \alpha' \cap \beta' |$
to be the _minimum_ number of intersections, taken over all curves 
$\alpha'$ and $\beta'$ (freely) homotopic to $\alpha$ and $\beta$.



TODO: say some words about the algebraic intersection number. 
I _think_ this is easier to compute? But I'm not totally sure, 
it would be nice to have a reference.

Mention that the algebraic intersection number is a symplectic form 
on $H^1$. This is really useful for the study of the mapping class group 
(cf. Farb and Margalit, ch 6)




In general, when you have a family of numbers that you want to understand, 
it's helpful to ~categorify~ the situation! Instead of working with numbers, 
try viewing those numbers as the dimensions of vector spaces. Then instead of 
working with the numbers you can work with all the extra structure of vector 
spaces.

TODO: Say some words about betti numbers, stanley's unimodal stuff, etc.

A common way to categorify a sum of numbers is as a chain complex. Then 
we can take the sum of the numbers as the rank of the chain complex, and 
we can take the _alternating_ sum of the numbers as the euler characteristic 
of the chain complex!

So we can categorify the goemetric and algebraic intersection numbers in 
one fell swoop by building a chain complex
$CF^\bullet(\alpha, \beta)$ where we have a generator for each intersection 
point. 

TODO: Say how we get the algebraic/geometric intersection numbers from 
this chain complex.


If we want to compare these, then the natural idea is to build a category 
whose objects are curves, and where we set 
$\text{Hom}(\alpha,\beta) \triangleq CF^\bullet(\alpha, \beta)$. 
Depending on your background this might look like a weird thing to do,
but categories "enriched in chain complexes" 
(that is, categories where $\text{Hom}(A,B)$ is a chain complex for each 
pair of objects) show up very naturally in many situations. In fact, 
this is one of the main ways that [$\infty$-categories][4] arise!

TODO: But what should composition be? (draw a picture)

TODO: is this associative? (no :/... but almost)

TODO: Interlude: $A_\infty$ stuff

---

[^1]: 
    Can we say we "undersatnd" curves on a surface if we can't even say 
    how often two curves intersect?

[1]: https://ncatlab.org/nlab/show/Fukaya+category
[2]: https://en.wikipedia.org/wiki/Mirror_symmetry_(string_theory)
[3]: https://sites.google.com/view/ccannizzo/
[4]: https://mathoverflow.net/questions/40075/chain-complexes-and-linear-infinity-categories
