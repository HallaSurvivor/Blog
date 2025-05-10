---
layout: post
title: Explicitly Computing with Fukaya Categories of Surfaces
tags:
  - my-thesis
---

The [Fukaya Category][1] of a symplectic manifold is a subtle and 
interesting invariant that contains information about 
[lagrangian submanifolds][2] and how they intersect. This is of 
interest for many reasons (TODO: list some), but perhaps the most 
famous reason is Kontsevich's famous [Homological Mirror Symmetry][3] 
conjecture. These categories are famously difficult to compute in general, 
but in case our manifold is a surface we can make things *very* explicit!
In this post, we'll talk about how to compute *with* multiple 
fukaya categories of surfaces, as well as *in* a particular fukaya category.

This is related to my thesis work with [Peter Samuelson][4], which I'll 
want to talk more about soon.

TOOD: the rest of the intro

---

Let's start with a quick answer to a very reasonable question: 
What are Fukaya Categories, and why might you care?

TODO: a cute, anachronistic, reason -- arithmetic/geometric intersection 
numbers of curves

TODO: lagrange multipliers? This is in your zotero somewhere...
maybe from a pascaleff talk?

TODO: the big one -- mirror symmetry

TODO: emphasize you're **not** an expert in fukaya categories

---

This is great and all, but how do you *compute* with these?

Fukaya categories in general are complicated, since their 
definition relies on detailed analytic data 

TODO: say more about what that data is.

Because of this, there's many variants of the fukaya category that 
put restrictions on what kinds of lagrangians one considers. Most 
importantly for us will be the <span class=defn>(Partially) Wrapped</span>
Fukaya Category. 

Here *wrapped* means that whenever we have a boundary component, our 
lagrangians are required to "wrap around it", as shown in the following 
picture:

TODO: a lagrangian wrapping around the puncture in a punctured torus

TODO: say that wrapping makes things easier... for some reason

We can also put <span class=defn>Stops</span> in our boundary, which 
prevent our lagrangians from wrapping. This makes the behavior *even simpler*.

TODO: picture of stops

In this case of surfaces, we can turn this into pure combinatorics! We can 
describe our surface in terms of a [ribbon graph][5], and work entirely 
in terms of the data available there. 

This is going to be heavily based on the excellent lectures 
[TODO: lecture title][6] by Sybille Schroll (TODO: spelling) and 
[TODO: another leccture title][7] by Claire Amiot, which are what made 
a lot of this stuff start to make sense for me.


TODO: rewatch those lectures and explain what's happening

---

Now that we've seen this, let's do some example computations in 
some actual fukaya categories!

TODO: disk with n+1 marked points
            D^b(A_n)
            indecomposables
            homs/exts
            show this agrees with a classical reference on D^b(A_n)
                (which you'll probably have to find)

TODO: annulus with marked points
            indecomposables
            homs/exts

TODO: punctured torus
            indecomposables
            homs/exts

Mention that you can find an arc system/ribbon graph for your surface by 
using morse theory.

---

There's another kind of computation you might want to do, though: 
Rather than computing *inside* a fukaya category, we might want to 
compute relationships *between* fukaya categories[^1]

TODO: functors between fukaya categories

TODO: gluing fukaya categories by homotopy pullback

---

TODO: epilogue

---

[1]: fukaya category
[2]: lagrangian submanifold
[3]: HMS
[4]: peter's website
[5]: ribbon graph
[6]: Sybille's lectures
[7]: Claire's lectures


[^1]:
    For a long time I've been considering writing a blog post on these 
    different "levels" at which you can do computations. 
    TODO: say more about this

