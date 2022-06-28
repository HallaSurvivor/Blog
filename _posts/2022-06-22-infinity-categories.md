---
layout: post
title: Infinity Categories and Model Categories
tags:
  - oo-categories
---

The title of this post is slightly misleading. It will be almost entirely
about $\infty$-categories, but it _will_ have a focus on how 
$\infty$-categories solve some of the formal problems with model categories
that we outlined in [part 1][1] of this trilogy.

With the intro out of the way, let's have a quick recap.

---

The setting we're interested in is a category $\mathcal{C}$ equipped with
some arrows $\mathcal{W}$ that morally _should_ be isomorphisms, but which
aren't (these are called _weak equivalences_, and a pair $(\mathcal{C}, \mathcal{W})$
is called a _relative category_).
The quintessential examples are the (weak) homotopy equivalences in 
$\mathsf{Top}$, and the quasi-isomorphisms of chain complexes.

We want to build a new category 
(called the <span class=defn>Homotopy Category</span> or <span class=defn>Localization</span>)
$\mathcal{C}[\mathcal{W}^{-1}]$ where we freely invert all the arrows in 
$\mathcal{W}$[^1]. The issue is that this category is quite badly behaved. 
For instance, even if $\mathcal{C}$ is (co)complete, 
$\mathcal{C}[\mathcal{W}^{-1}]$ almost never is. 

A [model structure][2] on a pair $(\mathcal{C}, \mathcal{W})$ is a choice of
two new families of arrows, called <span class=defn>fibrations</span> and
<span class=defn>cofibrations</span>, plus axioms saying how they relate to 
each other and to the weak equivalences $\mathcal{W}$.

A model structure on $(\mathcal{C}, \mathcal{W})$ solves many of the 
computational problems with $\mathcal{C}[\mathcal{W}^{-1}]$. For instance,
now the homotopy category is guaranteed to be locally small, and we have 
effective techniques for computing homotopy (co)limits, 
derived functors, and guaranteeing that two relative categories have
equivalent localizations. All of these techniques go through 
_bifibrant replacement_, which is a generalization of the familiar 
projective and injective resolutions from homological algebra. 

Unfortunately, as we noted at the end of the last post, model categories are
not without flaws. As soon as we want to talk about relationships _between_
model categories, we start running into trouble.

What, then are we to do? The answer is to fully accept homotopy theory as 
part of our life, and to move to a notion of "category" which is better 
equipped to handle the geometry which is implicit in the machinery of 
model categories.

---

To start, we need a model of "spaces" that's more convenient to work with
than topological spaces. 

<div class=boxed markdown=1>
A <span class=defn>Simplicial Set</span> is a functor 
$X : \Delta^{\text{op}} \to \mathsf{Set}$.

Here $\Delta$ (the _simplex category_) is the category whose objects are 
the nonemtpy finite totally ordered sets, with order preserving maps.
</div>

Every object in $\Delta$ is isomorphic to an object of the form

$$
0 \lt 1 \lt 2 \lt \ldots \lt n
$$

which we call $\Delta^n$. 

We should think of $\Delta^n$ as representing the [$n$-simplex][5],
where we've chosen a total order the $n+1$ vertices. This allows us
to orient all the edges in a consistent way[^2].

Now, to every topological space $X$ we can associate a simplicial set
$\text{Sing}_X$, where $\text{Sing}_X(\Delta^n)$ is the set of continuous
from the (topological) $n$-simplex into $X$. This construction is familiar
from, for instance, [singular homology][6].

It turns out that $$\text{Sing}_X$$ perfectly remembers the homotopy type of $X$,
in the sense that we can recover $X$ (up to homotopy equivalence) knowing
only the simplicial set $$\text{Sing}_X$$. This is some justification that 
simplicial sets really _can_ be used to model homotopy types. 

But there's a natural follow up question: Can we recognize when a 
simplicial set is $$\text{Sing}_X$$ for some space $X$? The answer,
of course, is _yes_, but we're not going to talk about that here. 
This topic deserves its own post, and indeed it [has one][12].

For now, though, we'll content ourselves with the knowledge that 
simplicial sets, up to homotopy equivalence, represent spaces 
in a convenient way. For those following along, this is the 
Quillen equivalence between $s\mathsf{Set}$ and $\mathsf{Top}$ that
we mentioned in the previous post!

We'll write $\mathcal{S}$ for the homotopy category of $s\mathsf{Set}$
(equivalently of $\mathsf{Top}$), and we'll call the objects of this 
category _spaces_.

---

<div class=boxed markdown=1>
An <span class=defn>$\infty$-category</span> is a category 
[enriched][13] in $\mathcal{S}$.

That is, given two objects $A$ and $B$ in our category, we have a
_space_ of morphisms $\text{Mor}(A,B)$.

Given an $\infty$-category, there's a natural way to get an 
ordinary category back from it. We keep the same objects, 
but replace the space of arrows $\text{Mor}(A,B)$ by its 
set of connected components.
</div>

As an example, we might have two arrows $f,g : A \to B$,
which are connected by homotopies $H$ and $K$. In this case we have a 
"circle's worth" of arrows from $A \to B$:

<p style="text-align:center;">
<img src="/assets/images/infinity-categories/circle.png" width="30%">
</p>

When we take connected components, these two maps $f$ and $g$ are 
identified, so we only see one arrow in the homotopy category.

---

Let's take a second to talk about how we actually build an 
$\infty$-category from a relative category $(\mathcal{C},\mathcal{W})$.
This is called the 
<span class=defn>Hammock Construction</span>[^15], and while we won't spend 
_too_ much time on this, it's worth at least a few words!

We want to build up a space of maps $A \to B$. 

The $0$-cells will be zigzags of the form:

 - $$ A \to B $$
 - $$ A \to C_0 \overset{\sim}{\leftarrow} B $$
 - $$ A \to C_0 \overset{\sim}{\leftarrow} C_1 \to B $$
 - $$ A \to C_0 \overset{\sim}{\leftarrow} C_1 \to C_2 \overset{\sim}{\leftarrow} B $$
 - etc.[^17]

where the left-pointing arrows are weak equivalences. Notice that, after we 
invert the weak equivalences, the left facing arrows will have inverses, 
which will compose with the other right facing arrows to give an 
honest-to-goodness arrow $A \to B$. That is, the $0$-cells really are 
maps $A \to B$ in $\mathcal{C}[\mathcal{W}^{-1}]$.

Now, a $1$-cell from $f$ to $g$ should be a "proof" that $f$ and $g$ are homotopic.
If $f$ and $g$ have the same length, then we can represent this with a 
"hammock"[^16]:

<p style="text-align:center;">
<img src="/assets/images/infinity-categories/1hammock.png" width="50%">
</p>

Similarly, a $k$-cell will be a hammock that is $k$ strands "wide".
Here's the picture from the original paper:

<p style="text-align:center;">
<img src="/assets/images/infinity-categories/wide-hammock.png" width="50%">
</p>

As before, the vertical arrows should all be weak equivalences, as should all
the backwards facing arrows in the zigzags.

Of course, we need the [face maps][27] between simplicies. We get the $i$th face map
by just omitting row $i$ from the hammock. We get the $i$th degeneracy map
by repeating the $i$th row, using the identity map in each column as the weak
equivalence.

<div class=boxed markdown=1>
The resulting $\infty$-category $L^H(\mathcal{C}, \mathcal{W})$ is called the 
(Hammock) Simplicial Localization of $(\mathcal{C}, \mathcal{W})$.
</div>

<p style="text-align:center;">
<img src="/assets/images/infinity-categories/hammock.gif" width="50%">
</p>

---



---

TODO: define the nerve localization of a model category

TODO: oo-functors, oo-(co)limits

TODO: in fact, we can redo all of CT!

TODO: what is the precise relationship between relative categories and 
oo-categories? do we lose anything when we make this upgrade?

TODO: notice that oo-functors, suitably truncated, define functors on the 
homotopy category [here][4]


---

[^1]:
    As one concrete reason to do this, in chain complexes with 

[^2]:
    Notice this is exactly what we do to make (co)homological computations
    with simplicial chains in topology.

[1]: part 1
[2]: https://en.wikipedia.org/wiki/Model_category
[3]: https://math.stackexchange.com/questions/2219726/what-is-an-example-showing-the-failure-of-the-functoriality-of-the-cone-construc
[4]: https://kerodon.net/tag/005Z
[5]: https://en.wikipedia.org/wiki/Simplex
[6]: https://en.wikipedia.org/wiki/Singular_homology
[12]: quasicategory post
[13]: https://en.wikipedia.org/wiki/Enriched_category
