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

Now, back to the main storyline[^24]!

We know how to associate to each relative category $(\mathcal{C}, \mathcal{W})$
an $\infty$-category.
Surprisingly, (up to size issues), _every_ $\infty$-category arises from a 
pair $(\mathcal{C}, \mathcal{W})$ in this way. 

With this in mind, we might want to think of $\infty$-categories as 
"homotopy theories" rather than relative categories. Intuitively, the facts 
in the previous paragraph tell us that we shouldn't lose any information by
doing this... But the correspondence isn't _actually_ one-to-one.
Is there any way to remedy this, and put our intuition on solid ground?

Now we get to the point of this whole post. Why care about the 
"homotopy theory of homotopy theories"? What does that even _mean_?

To start, recall that we might want to consider two relative categories
"the same" if they present the same homotopy theory. With our new, 
more subtle tool, that's asking if

$$L^H(\mathcal{C}_1, \mathcal{W}_1) \simeq L^H(\mathcal{C}_2, \mathcal{W}_2)$$

but wait... There's an obvious category $\mathsf{RelCat}$ whose objects
are relative categories and arrows 
$$(\mathcal{C}_1, \mathcal{W}_1) \to (\mathcal{C}_2, \mathcal{W}_2)$$ are functors 
$$\mathcal{C}_1 \to \mathcal{C}_2$$ sending each arrow in $$\mathcal{W}_1$$ to
an arrow in $$\mathcal{W}_2$$.
What's more, this category has some objects that are _morally_ equivalent,
but which aren't actually isomorphic! Are you thinking what I'm thinking!?

$\mathsf{RelCat}$ _itself_ forms a relative category, and
in this sense, $\mathsf{RelCat}$ becomes itself a homotopy theory whose 
objects are (smaller) homotopy theories! 

We can do the same thing with simplicial categories to get a relative 
category of $\infty$-categories. If we do this, we find that these two 
relative categories have equivalent localizaitons! 

This makes precise the idea that relative categories and $\infty$-categories
are really carrying the same information[^25]!

In fact, there's a _zoo_ of relative categories which all have the 
same homotopy category as $\mathsf{RelCat}$. We say that these are 
models of the "homotopy theory of homotopy theories", or equivalently,
that these are models of $\infty$-categories.

One of the most popular models right now are the [quasicategories][36],
but there's also [complete segal spaces][37], and more.

<div class=boxed markdown=1>
If you remember earlier, we only gave a tentative definition of a 
homotopy theory. Well now we're in a place to give a proper definition!

A <span class=defn>Homotopy Theory</span> 
(equivalently, an <span class=defn>$\infty$-category</span>) is an object 
in any (thus every) of the localizations of the categories we've just discussed.
</div>

Perhaps unsurprisingly, we can do the same simplicial localization 
maneuver to one of these relative categories 
in order to get an $\infty$-category of $\infty$-categories. 

But why care about all this?

---

Well, for one, the language of $\infty$-categories lets us compute 
(co)limits inside the homotopy categories! Precisely, it lets us 
compute homotopy (co)limits in a way that feels more like computing 
classical (co)limits. 
In fact, we can do almost everything we can do
in ordinary category theory in the $\infty$-category setting[^26].

But what about the homotopy theory of homotopy theories? Is there a
reason to care about thij? Of course!

Here's the example that sold me. If you remember, we built the 
hammock localization $L^H(\mathcal{C}, \mathcal{W})$ by hand,
and while it's a useful construction it's conceptually not as clean
as one might like. It would be nice if there were a parallel approach,
which makes it clear "what's really going on".

Well what's the simplest example of a localization? Think of the category
$\Delta^1$ with two objects and one arrow:

$$
0 \longrightarrow 1
$$

Inverting this arrow gives us a category with two objects and an isomorphism
between them, but of course this is equivalent to the terminal category
$\Delta^0$ (which has one object and only the identity arrow).

So then how should we invert all of the arrows in $\mathcal{W}$? It's not
hard to see that this pushout, intuitively, does the job:

<p style="text-align:center;">
<img src="/assets/images/infinity-categories/oo-pushout.png" width="33%">
</p>

Here the top functor sends each copy of $\Delta^1$ to its corresponding 
arrow in $\mathcal{W}$, and the left functor sends each copy of $\Delta^1$
to a copy of $\Delta^0$. Then the pushout should be $\mathcal{C}$, only we've
identified all the arrows in $\mathcal{W}$ with the points $\Delta^0$.
This is exactly what we expect the (simplicial) localization to be, and
it turns out that in the $\infty$-category of $\infty$-categories, this 
pushout really does the job! 

For more about this, I really can't recommend the youtube series 
[_Higher Algebra_][39] by Homotopy Theory Münster highly enough. 
Their goal is to give the viewer an idea of how we _compute_ with
$\infty$-categories, and what problems they solve, without getting
bogged down in the foundational details justifying exactly why these
computational tools work.

Personally, that's _exactly_ what I'm looking for when I'm first learning
a topic, and I really appreciated their clarity and insight! 

---

Speaking of computation, $L^H(\mathcal{C}, \mathcal{W})$ is better behaved
than $\mathcal{C}[\mathcal{W}^{-1}]$, but it's still hard to compute with.
It would be nice if there were some ~bonus structure~ that we could put on
a relative category that would give us a handle on 
$L^H(\mathcal{C}, \mathcal{W})$. Something similar to a presentation of a group,
a basis for a vector space, or a chart on a manifold. 

Like all of the cases I just listed, fixing such a structure should let us 
make concrete computations, often by making some noncanonical choices. Of 
course, we prove that these computations work 
(and are independent of the choices) by giving a more conceptual proof, which
is choice-free, in the $\infty$-category of $\infty$-categories. 

Such a thing exists, and we call it a [Model Structure][2] on a 
relative category. I'm publishing a sister blog post [here] TODO: link. 
where I talk about about model structures, what they do, and how to use them.

I'll see you there ^_^

---


---

Ok, so now we know (roughly) what an $\infty$-category is. How does this 
help us solve our problems with model categories?

First, to every relative category $(\mathcal{C}, \mathcal{W})$ we can 
build an $\infty$-category called the 

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
