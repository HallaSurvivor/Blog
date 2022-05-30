---
layout: post
title: Why Care about the "Homotopy Theory of Homotopy Theories"?
tags:
  - 
---

I'm a TA at the [HoTTEST Summer 2022][1] summer school on homotopy type theory,
and while I feel quite comfortable with the basics of HoTT, there's a TON of 
things that I should really know better: so I've been reading a lot to prepare.
One of the things that I really didn't know _anything_ about was the theory of
[model categories][2]. I knew they had something to do with 
[$\infty$-categories][3] and [homotopy theory][4]... but I really didn't know
_what_ :P. Well, multiple papers later, I have a better idea of what's going on,
and I'll say a few words about it in this post. THe focus, though, is going to
be on the "homotopy theory of homotopy theories" -- a groundbreaking 
development in the field... but one which seems _very_ abstract. I've been 
thinking about why we should care about this result, and in the process I 
discovered a _new reason_ to care about things! 

So then, let's get to it!

---

First of all, what even _is_ a "homotopy theory"? And what does it have to do
with model categories?

Say we have a (complete and cocomplete) category $\mathcal{C}$, which has some 
arrows (called <span class=defn>weak equivalences</span>) that we _want_ to 
consider as isomorphisms... but which aren't. The two motivating examples are 

- topological spaces with weak homotopy equivalences[^1]
- chains of $R$-modules with quasi-isomorphisms

Now, a category is an algebraic structure, so there's nothing stopping us from
just... adding in new arrrows, plus relations saying that they're inverses for
the arrows we wanted to be isomorphisms. By analogy with ring theory, if 
$\mathcal{W}$ is the family of arrows to invert[^2] then we call this new 
category the <span class=defn>Localization</span> $\mathcal{C}[\mathcal{W}^{-1}]$.

There's just one hitch... the new notion of isomorhpism might be very complicated!
Indeed, it's possible that we end up with a _proper class_ of arrows between
two objects, even if $\mathcal{C}$ started out locally small. Moreover, since
the new isomorphism relation is so complicated, it becomes unwieldy to do 
computations in this category (for instance, computing limits and colimits).

It would be really nice if we had some way to reign in this localization 
process so that we end up with a category of roughly the same size as the
one we started with. While we're at it, it would be nice if we had a 
convenient way of doing computations in $\mathcal{C}[\mathcal{W}^{-1}]$.

Remarkably, a <span class=defn>Model Structure</span> on 
$(\mathcal{C}, \mathcal{W})$ solves both of these problems simultaneously!

The idea is to choose two new subfamilies of arrows: the 
<span class=defn>fibrations</span> and the <span class=defn>cofibrations</span>.
We then define two "nice" subclasses of objects: 

- $X$ is called <span class=defn>fibrant</span> if the unique arrow to the 
    terminal object is a fibration
- $X$ is called <span class=defn>cofibrant</span> if the unique arrow from 
    the initial object is a cofibration

Then we have axioms which imply that every object is weakly equivalent to an 
object which is both fibrant and cofibrant. Since, after localizing, our 
weak equivalences become isomorphisms, this means we can restrict attention to
the fibrant/cofibrant objects.

But it's a theorem that we have _excellent_ control over the maps between 
fibrant/cofibrant objects in the localization! In fact, there's a notion of
"homotopy" between maps, which is entirely analogous to the notion of 
homotopy in topology, and maps $X \to Y$ in $\mathcal{C}[\mathcal{W}^{-1}]$
are exactly homotopy classes of maps from $X \to Y$ \in $\mathcal{C}$
(provided $X$ and $Y$ are fibrant/cofibrant)!

---

We should probably say a few words about the intuition for fibrations and
cofibrations, as well as fibrant and cofibrant objects.

A _fibration_ is an arrow that's easy to "lift" into:

TODO: a picture of a lifting diagram

For instance, covering spaces and bundles are examples of fibrations in 
topology. Algebraically, a map of chains of $R$-modules 
$f : A_\bullet \to B_\bullet$ is fibrant if each $f_n$ is a surjection.

Dually, a _cofibration_ is an arrow that's easy to "extend" out of:

TODO: a picture of an extension diagram

For instance, the inclusion arrow of a "good pair" is a cofibration 
(TODO: double check this). So we should think of a cofibration as being
a subspace inclusion $A \hookrightarrow B$ where $A$ "sits nicely" inside $B$.
Algebraically, a map $f : A_\bullet \to B_\bullet$ is a cofibration if it's
(TODO: figure this out).

Then a _fibrant_ object is one which is particularly easy to map into
(since we can lift the unique map to the terminal object), and a 
_cofibrant_ object is one which is particularly easy to map out of
(since we can extend the unique map from the initial object)[^3].

TODO: fact check that footnote!

---

Notice that the model structure is primarily a computational tool for 
working with the localization $\mathcal{C}[\mathcal{W}^{-1}]$. If you're
a topologist you call this the <span class=defn>Homotopy Category</span> of
$\mathcal{C}$, and if you're an algebraist you call it the 
<span class=defn>Derived Category</span> instead[^4]. 

There might also be multiple model structures on $(\mathcal{C}, \mathcal{W})$,
and we can use whichever one makes our computation easier. For instance,
when working with chains of $R$-modules up to quasi-isomorphism, we have 
compatible model structures based on injective _and_ projective resolutions!
When computing right derived functors, we use the injective model structure,
and when computing left derived functors, we use the projective model structure.

TODO: fact check this.

---

Now, for something seemingly unrelated.

An <span class=defn>$\infty$-category</span> (properly an $(\infty,1)$-category)
is a category "enriched in spaces"[^6]. Between any two objects we have a 
homotopy-type worth of arrows. So we might have two arrows $f,g : A \to B$,
which are connected by homotopies $H$ and $K$. In this case we have a 
"circle's worth" of arrows from $A \to B$:

TODO: a picture of $f$, $g$, $H$, and $K$.

Now _this_ is starting to feel more like Homotopy Type Theory[^5]!

---

It turns out that localizing a model category forgets a _lot_ of information! 

We can remember some of this by building an $\infty$-category instead. It's 
still not entirely clear to me how to build it from the model structure, 
but that information is in a paper TODO: cite that paper

We can recover the localization, though, since maps $f : A \to B$ in the
localization are the same thing as the connected components of the space 
of maps from $A$ to $B$ in the $\infty$-category!

Moreover, (up to size issues) _every_ $\infty$-category arises from a 
pair $(\mathcal{C}, \mathcal{W})$, so that it's reasonable to identify
$\infty$-categories with homotopy theories. _Unfortunately_ not every 
such system admits a compatible model structure. We say that an $\infty$-category
is <span class=defn>Presentable</span> if it comes from a model structure --
so the presentable $\infty$-categories are those in which we can do 
computations. 

This is analogous to a (finite) presentation of a group, say. Indeed, not every
group has a finite presentation, and those that do don't have a _canonical_ 
finite presentation. But if you _fix_ a presentation, it greatly expands the 
kinds of (combinatorial and computational) tools for working with your group.

TODO: restructure this, and make sure you introduce the name "homotopy theory"
earlier on in the post.

---

[^1]:
    It turns out there's _also_ a model category structure whose homotopy 
    category gives homotopy equivalence, rather than weak homotopy equivalence.

    But the model structure on $\mathsf{Top}$ which gives weak homotopy 
    equivalence is the "standard" one, so that's what I'm listing as the 
    motivating example.

[^2]:
    $\mathcal{W}$ is short for "Weak Equivalence"

[^3]:
    There's also intuition that the cofibrant objects are the ones which can
    be built by repeatedly gluing together "nice" objects. In $\mathsf{Top}$,
    for instance, the cofibrant objects are the CW-complexes, and in 
    $R$-mod, they're the injective resolutions.

[^4]:
    This was a pleasant surprise for me. I've heard a lot of talk about 
    derived categories, and they always seemed quite scary. It's been very
    exciting to feel like I'm getting a two-for-one deal every time I feel
    another concept start to make sense ^_^.

[^5]:
    I don't want to say more about this, since I really want the focus of
    this article to be on model structures and the homotopy theory of 
    homotopy theories. But basically this method of building a "space" by 
    specifying its $0$-cells ($f$ and $g$), its $1$-cells ($H$ and $K$),
    and possibly higher dimensional cells too, is (basically) the 
    "$\infty$-groupoid" perspective on spaces. The reason HoTT "works" is
    because each type (equipped with its (higher) identity types) also forms
    an $\infty$-groupoid!

[^6]:
    Experts should wait _slightly_ longer before leaving angry comments!


[1]: HoTTEST Summer 2022 website
[2]: model categories
[3]: oo-cats
[4]: homotopy theory
