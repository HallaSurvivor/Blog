---
layout: post
title: An Interlude -- quasicategories
tags:
  - oo-categories
---

In the [other posts][1], we defined $\infty$-categories as being 
categories "enriched in simplicial sets". These are nice, and 
fairly quick to introduce, but if you start reading the 
$\infty$-category theoretic literature, you'll quickly run into
another definition: <span class=defn>Quasicategories</span>.
In this post, we'll give a quick introduction to quasicategories,
and talk about how they're related to the $\mathcal{S}$-enriched
categories we've come to know and love.

---

First, then, a reminder:

A <span class=defn>Simplicial Set</span> is a (contravariant) 
functor from the [simplex category][3] to $\mathsf{Set}$. 

This seems strange at first, but it turns out that we can model
many different kinds of behavior using simplicial sets. 

Most notably, simpicial sets are a common generalization of both 
topological spaces (up to homotopy) and categories! 

We've already seen how simplicial sets can represent topological spaces up to
homotopy (this is given by a quillen equivalence of model structures on
$\mathsf{Top}$ and $s\mathsf{Set}$). To a simplicial set, we associate its
[geometric realization][4], and to a topological space we associate its 
(singular) simplicial set $\text{Sing}_X$ where $\text{Sing}_X(\Delta^n)$ 
is the set of continuous maps from the topological $n$-simplex into $X$.

We know that $X$ is determined up to (weak) homotopy equivalence by 
$\text{Sing}_X$, so we previously defined a 
<span class=defn>Simplicial Category</span> to be a category enriched in 
simplicial sets. We wanted to intuitively view this as a category with a
geometric space of arrows between any two objects, as this came up in our 
study of $\infty$-categories. This turns out to be 
a great definition for intuition, but it can be a bit difficult to work with.

I mentioned earlier that simplicial sets can _directly_ generalize categories...
Maybe there's some way to define $\infty$-categories directly as simplicial
sets as well?

The answer will be "yes", but let's start small. Is there a way for us to
recognize when a simplicial set is $\text{Sing}_X$ for some topological
space $X$?

---

<div class=boxed markdown=1>
The <span class=defn>$i$th Horn</span> of $\Delta^n$ is (geometrically) 
the space we get by removing the interior of $\Delta^n$, along with the 
face opposite the $i$th vertex[^1]. We denote it $\Lambda^n_i$
</div>

For instance, let's look at $\Delta^2$. This is a solid triangle, and it 
has three horns -- one for each vertex.

Concretely, $\Delta^2$ is given by

<p style="text-align:center;">
<img src="/assets/images/quasicategories/delta2.png" width="50%">
</p>

Then the $0$th horn of $\Delta^2$, denoted $\Lambda^2_0$, is what we get by 
removing the interior 2-cell, along with the 1-cell opposite $0$:

<p style="text-align:center;">
<img src="/assets/images/quasicategories/horn-2-0.png" width="50%">
</p>

Analogously, we get $\Lambda^2_1$ by removing the interior 2-cell and the 
1-cell opposite $1$:

<p style="text-align:center;">
<img src="/assets/images/quasicategories/horn-2-1.png" width="50%">
</p>

and we get $\Lambda^2_2$ by removing the interior 2-cell and the 1-cell
opposite $2$:

<p style="text-align:center;">
<img src="/assets/images/quasicategories/horn-2-2.png" width="50%">
</p>

What about the horns of $\Delta^3$? Well now, we remove the interior 3-cell
(the "volume" of the simplex) as well as the 2-cell opposite your favorite
vertex. Concretely, we see $\Lambda^3_0$ is given by[^3]

<p style="text-align:center;">
<img src="/assets/images/quasicategories/horn-3-0.png" width="50%">
</p>

Similarly, $\Lambda^3_1$ is

<p style="text-align:center;">
<img src="/assets/images/quasicategories/horn-3-1.png" width="50%">
</p>

$\Lambda^3_2$ is

<p style="text-align:center;">
<img src="/assets/images/quasicategories/horn-3-2.png" width="50%">
</p>

and $\Lambda^3_3$ is

<p style="text-align:center;">
<img src="/assets/images/quasicategories/horn-3-3.png" width="50%">
</p>

<div class=boxed markdown=1>
As a (quick?) exercise, you should try to write down a definition of
$\Lambda^n_i$ as a simplicial set. 

Remember that, by the yoneda lemma, it suffices to say what the
$k$-cells are for each $k$[^4].
</div>

---

Now then, we come to an important definition

<div class=boxed markdown=1>
A simplicial set $X$ is called a 
<span class=defn>Kan Complex</span>
if every horn $\Lambda^n_i$ in $X$ can be
"filled" by a $\Delta^n$.
</div>

In a commutative diagram, we ask that the following dotted 
morphism should always exist:

<p style="text-align:center;">
<img src="/assets/images/quasicategories/filling-horns.png" width="33%">
</p>

Why care about this? Because of the following major theorem:

<div class=boxed markdown=1>
For every topological space $X$, $\text{Sing}_X$ is a kan complex.

Moreover, (up to weak equivalence), every kan complex arises in this way.
</div>

So we see that we can completely recover the notion of topological space 
(up to homotopy) by looking at special simplicial sets... But wasn't this 
all supposed to have something to do with category theory?

---

Just like every topological space $X$ defines a simplicial set 
$$\text{Sing}_X$$, every category _also_ defines a simplicial set,
called the <span class=defn>Nerve</span> of the category $\mathcal{C}$.

In general, the $n$-cells in the nerve $\mathcal{N}(\mathcal{C})$ will be
given by the "paths" of length $n$ made of arrows in $\mathcal{C}$. That is

 - The 0-cells will be objects of $\mathcal{C}$
 - The 1-cells will be the arrows, $C_0 \to C_1$
 - The 2-cells will be the paths of length 2, $C_0 \to C_1 \to C_2$
 - The 3-cells will be the paths of length 3, $C_0 \to C_1 \to C_2 \to C_3$
 - etc.

Concretely, let's look at the following category (where $k = hf = hg$):

<p style="text-align:center;">
<img src="/assets/images/quasicategories/cat.png" width="50%">
</p>

Then its nerve should have three 0-cells ($A$, $B$, and $C$),
plus 1-cells for $f$, $g$, $h$, and the composite $k$
(notice this is only _one_ 1-cell, since it's a single arrow in $\mathcal{C}$).
However, we add _two_ 2-cells: 

$$
A \overset{f}{\to} B \overset{h}{\to} C
$$

$$
A \overset{g}{\to} B \overset{h}{\to} C
$$

since $k$ arises as a composite in _two_ ways: $hf$ and $hg$.

Thus, the nerve of $\mathcal{C}$ is a _cone_ 

<p style="text-align:center;">
<img src="/assets/images/quasicategories/nerve.png" width="50%">
</p>

Perhaps a better way to visualize this is as a _disk_ instead:

<p style="text-align:center;">
<img src="/assets/images/quasicategories/nerve2.png" width="50%">
</p>

Of course, it's easy to guess the next question. Can we tell 
_which_ simplicial complexes arise as the nerve of some category?

Again, the answer is _yes_, and the answer will look shockingly similar
to the case of topological spaces!

<div class=boxed markdown=1>
A simplicial complex is called a 
<span class=defn>Quasicategory</span>
if every "inner horn" has a fill.

That is, every horn $\Lambda^n_i$ should have a fill, except 
when $i=0$ or $i=n$.
</div>

This should make sense as a definition, since in a category _composition_
tells us that we can fill inner horns! 

Indeed, consider the inner horn $\Lambda^2_1$:

<p style="text-align:center;">
<img src="/assets/images/quasicategories/inner-horn.png" width="50%">
</p>

If this diagram lives inside the nerve of a category $\mathcal{N}(\mathcal{C})$,
then we can always fill the horn! Indeed, we have a 1-cell from $0 \to 2$
given by $gf$. We also have a 2-cell filling this triangle given by
the path $0 \overset{f}{\to} 1 \overset{g}{\to} 2$.

<p style="text-align:center;">
<img src="/assets/images/quasicategories/filled-inner-horn.png" width="50%">
</p>

<div class=boxed markdown=1>
As a cute exercise, you should check that the two inner horns 
$\Lambda^3_1$ and $\Lambda^3_2$ have fills in the nerve of a category.
</div>

---

This all brings us to another major theorem:

<div class=boxed markdown=1>
For every category, the nerve $\mathcal{N}(\mathcal{C})$ is a 
quasicategory.

Moreover, if $X$ is a quasicategory where each inner horn has a 
_unique_ fill, then $X$ is isomorphic to the nerve of some category.

Moreover again, the nerve construction embeds the category of categories
fully and faithfully into the category of quasicategories.
</div>

Importantly, this means that _every kan complex is a quasicategory_! This tells us
that quasicategories allow us to treat spaces and categories on equal footing[^5]!

In particular, quasicategories give us a setting where we can 
"do homotopy theory" to categories, and if you remember back to 
the main post about $\infty$-categories, and how they solve the
formal issues with model categories, that's exactly what we were looking for!

<div class=boxed markdown=1>
Here's another tentative definition. If this reminds you of the tentative
definition of a "homotopy theory" from the last post, you have good instincts.

An <span class=defn>$\infty$-category</span> is a quasicategory, where we 
say two quasicategories _present the same $\infty$-category_ if they are
[homotopy equivalent][10] as simplicial sets.
</div>

This is great because it gives us a super concrete way of working with 
$\infty$ categories. 

In this framework, our categories literally are geometric objects! The 
category of simplicial sets is a topos, so it has as many nice constructions
as we could want, and many of these preserve kan complexes and quasicategories.

For instance, now functors are just continuous maps, limits and colimits 
of quasicategories can be computed as with geometric objects, exponentials 
give us functor quasicategories, and all of these work as well as we could hope.

Because of this concreteness, 
Jacob Lurie's tomes on $\infty$-categories are primarily based on the 
language of quasicategories. But in the main post, we defined an 
$\infty$-category to be a category enriched in spaces...

How can we reconcile these viewpoints? Is there a way for us to apply
the machinery proven in Lurie's books to the hammock localization of
a model category?  Is there some way for us to
use these nice geometric definitions for computations involving quasicategories,
and leverage them to understand the simplicial categories we've been talking
about? Why have we given two seemingly unrelated definitions of an 
$\infty$-category in the first place?

For answers to these questions and more, read on to the [last post][5] in this
series[^2]!

---

[^1]:
    Super concretely, given $n+1$ vertices 

    $$0 \lt 1 \lt \ldots \lt n-1 \lt n$$

    the $i$th horn $\Lambda^n_i$ is $\Delta^n$ minus two cells:

    - the unique $n$-cell
    - the unique $n-1$ cell which doesn't contain $i$

[^2]:
    Thank goodness! I have been working on these for _so_ long.
    I really didn't realize how big a project I was in for when I decided
    to make a post clarifying the relationship between model categories
    and $\infty$-categories...

    I love how it's turning out, but I'm so ready for these posts to be 
    behind me, haha. I also didn't want to post any of them until they
    were all done. In part because I spent a lot of time moving various 
    bits back and forth between posts, and once one is public I would want
    to consider it (mostly) set in stone. But also because I wanted to make
    sure I actually finished them all.

    I have a bad habit of starting a series and leaving things unfinished
    (rest in peace [cohomology part 1][2]), 
    but it was important that I not do that to these posts.

[^3]:
    Sorry if these are hard to understand. Drawing 3d pictures is hard, haha.
    Each image is made up of 1-cells (colored in black) as well as 2-cells
    (shaeded in blue). Moreover, in each pictrue we've omitted exactly one
    2-cell from the boundary of the tetrahedron.

[^4]:
    If it's not clear what role yoneda plays in this situation, see 
    my answer [here][7]. 

    It's also definitely worth reading Friedman's 
    _An Elementary Illustrated Introduction to Simplicial Sets_
    (avaialable [here][8]).

[^5]:
    I originally put this in the main body, but I ended up deciding it
    ruined the flow of the post too much. That said, I still think it's 
    a fun (and enlightening) example, so I wanted to include it as a 
    ~bonus exercise~ here:

    <div class=boxed markdown=1>
    Show that two isomorphic categories give rise to homeomorphic nerves
    (after taking [geometric realizations][9], of course).

    Then, show that two _equivalent_ categories give rise to homotopy equivalent
    nerves.
    </div>



[1]: post 2
[2]: cohomology part 1
[3]: https://en.wikipedia.org/wiki/Simplex_category
[4]: https://ncatlab.org/nlab/show/geometric+realization#OfSimplicialSets
[5]: post 4
[7]: https://math.stackexchange.com/questions/4475159/conceptualizing-presheaves-as-generalized-spaces/4475219#4475219
[8]: http://arxiv.org/abs/0809.4221
[9]: https://ncatlab.org/nlab/show/geometric+realization
[10]: https://ncatlab.org/nlab/show/model+structure+on+simplicial+sets#joyals_model_structure
[11]: https://ncatlab.org/nlab/show/simplicial+set

