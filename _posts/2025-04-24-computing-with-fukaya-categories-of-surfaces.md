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

Normally I would start by motivating fukaya categories and explaining 
what kinds of problems they solve and why you might care, but to keep 
this post short I'll link to a [sister post][8] where I go over what 
my thesis is about. In that post I spend plenty of time talking about 
why fukaya categories are interesting, and there's no sense repeating myself 
here!

Instead, let's jump right into the main theorem that tells us we can 
*really* compute with fukaya categories of surfaces!

<div class=boxed markdown=1>
Theorem ([Haiden--Katzarkov--Kontsevich][9], 
[Lekili--Polishchuk][10], [Opper--Plamondon--Schroll][11]):

There is a bijection of sets[^2]

$$
\left \{
    \begin{array}{c}
        \text{Surfaces with boundary with} \\
        \text{marked intervals and a line field} \\
        \text{up to homeomorphism of marked surfaces}
    \end{array}
\right \}
\longleftrightarrow
\left \{
    \begin{array}{c}
        \text{Gentle algebras up to derived} \\
        \text{morita equivalence}
    \end{array}
\right \}
$$

sending a marked surface $S$ to its (partially wrapped) 
fukaya category $\mathcal{F}(S)$ and sending a gentle 
algebra $A$ to its bounded derived category $D^b(A)$.

</div>

This theorem is fantastic since gentle algebras are *highly* studied 
objects, and almost any question you have about them has been answered 
in a nice combinatorial way. In this post I want to explain how to 
compute a description of the gentle algebra from the surface you're 
interested in -- this lets you do computations *inside* a particular fukaya 
category. For instance, it tells you what the indecomopsable objects are, 
what the homsets are between two indecomposables[^4],
how to compute cones (and thus (co)limits[^3]), and much more.

After this, I'll say some words about how to compute *with* multiple 
fukaya categories. For example, you can compute the fukaya category of 
a complicated surface as the global sections of a "cosheaf" of 
smaller fukaya categories[^1]. 

Let's get to it!

---

Fukaya categories of general symplectic manifolds are complicated, 
and even stating the definition relies on detailed analytic data 
(such as compactifications of moduli spaces of pseudoholomorphic disks)
as well as detailed algebraic data (such as the "higher $A_\infty$ operations").
Because of this, there's many variations of the fukaya category in the 
literature which either augment lagrangians with ~bonus data~ or restrict 
attention to particularly nice lagrangians (or both) in order to make 
the fukaya category easier to compute.
We're going to be interested in the <span class=defn>(Partially) Wrapped</span>
Fukaya Category of a *surface*. This is probably the easiest variant, and 
is certainly the most combinatorially concrete.

Here *wrapped* means that whenever we have a boundary component, our 
noncompact lagrangians are required to approach infinity in the 
simplest possible way -- the boundary looks like a cylinder 
$S^1 \times \mathbb{R}$, and our lagrangian must eventually look like $
\{\text{pt}\} \times \mathbb{R}$.

<div class=boxed markdown=1>
TODO: a lagrangian moving straight towards the puncture of a punctured torus
</div>

This is called the *wrapped* fukaya category because we compute the 
homspace between two such lagrangians by *wrapping* one around the 
cylinder and then counting intersections:

<div class=boxed markdown=1>
TODO: a picture of this
</div>

We can also put <span class=defn>Stops</span> in our boundary, which 
prevent our lagrangians from wrapping. This makes the behavior *even simpler*.

<div class=boxed markdown=1>
TODO: a picture of a punctured torus with two stops
</div>

In this case of surfaces, we can turn this into pure combinatorics! 
If you're interested in this stuff,
do yourself a favor and watch the excellent lectures 
[_A geometric model for the bounded derived category of a gentle algebra_][6] 
by Sibylle Schroll and 
[_Fukaya categories associated with graded surfaces and gentle algebras_][7] 
by Claire Amiot. These were extremely important for my understanding of the 
subject, and their influence will be obvious in the way I talk about it.


---

So, how do we combinatorialize the situation?

We draw our surface and mark some intervals on the boundary. 
These marked points will be the *allowable endpoints* for curves. 
For example, here are some of the doodles you might draw to 
actually compute with, and the surfaces they represent:

<div class=boxed markdown=1>
TODO: a disk with 3 punctures 
</div>

<div class=boxed markdown=1>
An annulus with two and one marked points
</div>

<div class=boxed markdown=1>
TODO: an annulus with one and zero marked points
</div>

<div class=boxed markdown=1>
TODO: a punctured torus with three marked points
</div>

<div class=boxed markdown=1>
TODO: a twice punctured torus with no marked points
</div>

Officially we should put a line field on each of these too, which lets us 
lift the $\mathbb{Z}/2$-graded fukaya category 
(where shift corresponds to reversing the orientation of the curve)
to a $\mathbb{Z}$-graded fukaya category (where shift corresponds to 
a change of grading). I haven't drawn them because I think it would clutter 
the pictures, but once we start doing computations we'll see how the choice 
of line field impacts the objects in the category.

The key tool we'll need to understand these fukaya categories is an
<span class=defn>Arc System</span>, especially 
<span class=defn>Full Arc Systems</span> and 
<span class=defn>Dissections</span>.

An *arc system* is exactly what it sounds like -- a collection of (graded) arcs 
in your surface, which are pairwise non-isotopic and non-intersecting. An 
arc system is *full* if it cuts your surface into disks and contains 
all the boundary arcs. An arc system is a *dissection* if it cuts 
$S$ into disks each of which contains exactly one boundary arc.

Here the *boundary arcs* are just the non marked intervals on the boundary 
-- this will become clearer with examples.

<br>

Let's start with a disk with marked intervals.

<div class=boxed markdown=1>
TODO: disk with 4 punctures
</div>



---




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
compute relationships *between* fukaya categories.

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
[8]: sister post on my thesis
[9]: HKK
[10]: LP "derived equivalences of gentle algebras"
[11]: OPS "geometric model"


[^1]:
    For a long time I've planning to write a blog post explaining the
    different "levels" at which you can do computations. In increasing order 
    of abstraction, or "category level":

    There's computations of the form "given an $A$-module $M$, compute the 
    element $a \cdot m$" (etc.). At this level you have questions about 
    relationships between elements in the module.

    There's computations of the form "given two $A$-modules $M$ and $N$, 
    compute their tensor product" (etc.). At this level you have questions 
    about relationships between objects in the category of modules.

    There's computations of the form "given two algebras $A$ and $B$, 
    compute all functors $A$-mod to $B$-mod". At this level we have 
    questions about relationships between module categories (living in 
    some 2-category).

    Of course, this doesn't stop here, but the point is that at each of 
    these levels you have interesting computations to be done, but it's 
    important to know which tools are good for computations at which level. 
    Knowing an explicit presentation of a quantum group might not help you 
    compute a tensor product of its modules for the same reason that knowing 
    every module in a functor category admits a projective resolution by 
    representable functors won't help you compute a PBW-basis for your quantum 
    group! 

    Ideally you should be fluent with computations at multiple levels. 
    Even though they're differen't kinds of computation, they still 
    *interact*, and sometimes lower abstraction computations will help you
    guess the right higher abstraction computation to try, or higher 
    abstraction computations will "compile down" in a way that lets you 
    avoid a lower level computation that might be too gritty to do by hand.

[^2]:
    If you're anything like me, you're curious whether this bijection 
    can be upgraded to an equivalence of groupoids.
    For instance, this would tell us that the marked mapping class group of 
    $S$ acts on $D^b(A)$... This is probably true, but I can't actually find it 
    written down anywhere, and I haven't had time to read some of these papers
    carefully enough to see for myself whether this is a consequence of the 
    existing proofs.

    An equivalence of categories would be even nicer, but something is 
    scratching at my brain that not every map of marked surfaces induces a 
    map of fukaya categories... I think the definition in HKK isn't closed 
    under composition, for instance. 

    These are both things I want to think more about at some point, since 
    there's definitely something more to say here. But it'll have to wait 
    until after this post goes up.

[^3]:
    Recall that finite (co)limits can be computed from (co)products and 
    (co)equalizers, but the (co)product of two objects is just their direct sum 
    (which we understand) and the equalizer of two arrows $f,g : A \to B$ is 
    (up to shift) the cone of $f-g$. Of course, the magic of 
    stable $\infty$-cateogires is that the coproduct of two objects is _also_
    just their direct sum, and the coequalizer of two arrows $f,g : A \to B$ is 
    _also_ (up to shift) the cone of $f-g$!

[^4]:
    And thus between *any* two objects, since we write both as a direct 
    sum of indecomposables, then write a map between them as a matrix 
    of maps between the indecomposables. 
