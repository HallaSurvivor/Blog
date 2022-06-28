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
and talk about how they're related to the $s\mathsf{Set}$-enriched
categories we've come to know and love.

---

First, then, a reminder:

TODO: recap what a simplicial set is, and mention we can build
$$\text{Sing}_X$$ from a space $X$ in a way that doesn't lose 
homotopy information.

In the previous post, we were interested in recognizing when a 
simplicial set is of the form $$\text{Sing}_X$$. Let's see how
we can do that!

---

<div class=boxed markdown=1>
The <span class=defn>$i$th Horn</span> of $\Delta^n$ is (geometrically) 
the space we get by removing the interior of $\Delta^n$, along with the 
face opposite the $i$th vertex. We denote it $\Lambda^n_i$
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
given by the "paths" of arrows in $\mathcal{C}$ of length $n$. That is

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

---

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
</div>

Notice, though, that _every kan complex is a quasicategory_! This tells us
that quasicategories allow us to treat spaces and categories on equal footing[^5]!

In particular, quasicategories give us a setting where we can 
"do homotopy theory" to categories, and if you remember a hundred 
years ago at the start of this post, we were looking for 
_precisely_ such a generalization!

<div class=boxed markdown=1>
Here's another tentative definition. If this reminds you of the tentative
definition of a "homotopy theory" from the last post, you have good instincts.

An <span class=defn>$\infty$-category</span> is a quasicategory, where we 
say two quasicategories _present the same $\infty$-category_ if they are
weakly equivalent in a [certain model structure][10] on 
simplicial sets.
</div>


---

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
[7]: https://math.stackexchange.com/questions/4475159/conceptualizing-presheaves-as-generalized-spaces/4475219#4475219
[8]: http://arxiv.org/abs/0809.4221
[9]: https://ncatlab.org/nlab/show/geometric+realization
[10]: https://ncatlab.org/nlab/show/model+structure+on+simplicial+sets#joyals_model_structure
[11]: https://ncatlab.org/nlab/show/simplicial+set
