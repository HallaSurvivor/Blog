---
layout: post
title: Talk -- 2-Categorical Descent and (Essentially) Algebraic Theories
tags:
  - my-talks
---

A few weeks ago I gave a talk at the [CT Octoberfest 2023][1] about some 
work I did over the summer that I'm really proud of. Unfortunately, while 
writing up the result I found a 1999 paper by Pedicchio and Wood that 
proves the same theorem (with roughly the same proof), so I wasn't able to 
publish. Thankfully, the work is still extremely interesting, and I was more 
than happy to talk about it at a little online conference for other 
category theorists ^_^.

---

Recall an [algebraic theory][2] is something like groups, rings, modules,
etc. It's a structure that can be defined as a set (or possibly multiple sets)
with some operations defined on it (allowing constants as $0$-ary operations) 
and equations specifying the behavior of those operations.

An [essentially algebraic theory][3] is something like a category. It's a 
structure that can be defined as a site (or possibly multiple sets) with some 
operations defined on it, etc. The main superpower we get in the _essentially_
algebraic world over the algebraic one is _partially defined functions_. 
Now our operations don't have to be defined everywhere, they are allowed 
to be defined on subsets of the sorts. As long as those subsets are definable 
by equations!

For instance, the theory of categories is essentially algebraic since we have 

- Sets $O$ and $A$ (the sets of objects and arrows)
- operations $\text{dom}, \text{cod} : A \to O$ taking an arrow to its domain/codomain
- an operation $\text{id} : O \to A$ taking an object to the identity arrow at that object 
- an operation $$\circ : \{ (f,g) \in A \times A \mid \text{dom}(f) = \text{cod}(g) \}$$
- satisfying certain equational axioms, like $\text{dom}(\text{id}(x)) = x = \text{cod}(\text{id}(x))$, 
    $(f \circ g) \circ h = f \circ (g \circ h)$, etc.

Notice that composition _isn't_ defined on the whole set $A \times A$. It's 
only _partially_ defined! But the set where it's defined is easy to understand 
-- it's defined by an equation in the other functions ($\text{dom}(f) = \text{cod}(g)$).

Contrast this with fields, which have a partially defined inverse operation 
$$(-)^{-1} : \{ x \in k \mid x \neq 0 \} \to k$$. There is no way to write 
the domain of inversion as an _equation_[^1].

<br>

Now, essentially algebraic theories are _extremely_ nice, for lots of reasons 
I outlined in my talk (and mentioned on the nlab page I linked earlier),
but they're not _quite_ as nice as honest algebraic theories. 

For instance, the underlying set of a quotient of groups is a quotient 
of the underlying set. If we have a surjection $G \twoheadrightarrow H$,
then there's an equivalence relation[^2] $\theta$ on $UG$ (the underlying set of $G$)
so that $UH \cong UG \big / \theta$.

This is no longer the case for models of an _essentially_ algebraic theory! 
That is, the underlying set of a quotient might not be a quotient of the underlying set[^3].

For example, consider the following category:

<p style="text-align:center;">
<img src="/assets/images/ctoctoberfest2023/cat-before-quotient.png" width="50%">
</p>

Notice its set of arrows (ignoring identities) is $\{ f, g \}$.

Now if we quotient to set $Y_1 = Y_2$, we get a new category

<p style="text-align:center;">
<img src="/assets/images/ctoctoberfest2023/category-after-quotient-partial.png" width="50%">
</p>

But now that $Y_1 = Y_2$, $f$ and $g$ are composable! So we had better add a 
composite!

<p style="text-align:center;">
<img src="/assets/images/ctoctoberfest2023/cat-after-quotienting-new-arrow.png" width="50%">
</p>

So after quotienting, our underlying set of arrows (again, ignoring identities) is 
$\{ f, g, gf \}$, which _isn't a quotient_ of the set we started with! Also, 
note the role that partial operations played in this. The reason we got 
~bonus elements~ in our underlying set is because after quotienting the 
domain for the partial operation got bigger, so we had to freely add stuff 
to make sure we were closed under composition.

Another reason to care about algebraic theories over essentially algebraic 
ones is that algebraic theories can be interpreted in any _finite product_ 
category, while essentailly algebraic theories make use of all finite _limts_!
This shows up even for "real mathematicians", since the category $\mathsf{Diff}$ 
of smooth manifolds doesn't have finite limits! So we can define a lie group 
as a group object in $\mathsf{Diff}$ (since the theory of groups is algebraic)
but we _can't_ define a lie groupoid as a groupoid object in $\mathsf{Diff}$
(since the theory of groupoids is merely _essentially_ algebraic)[^4]!

With this in mind, it's natural to ask when we can recognize an 
algebraic theory amongst the essentially algebraic ones. It turns out 
we _can_, and the process requires a fair amount of category theory!

---



---

[^1]:
    In fact, we can prove this with category theory! It's a theorem that 
    the category of all models for an essentially algebraic theory has 
    an initial object. But there isn't an initial object in the category 
    of fields! So no matter how clever we are, there won't be an 
    essentially algebraic axiomatization of fields.

[^2]:
    In fact there's much more to be said here. The equivalence relation 
    $\theta$ will be a [congruence][4] (meaning it's compatible with the 
    algebraic structure), and the study of such congruences is historically 
    one of the biggest topics in [universal algebra][5]. I won't say more 
    here, but trust me that there's _much_ more to say. If you're interested, 
    I recommend Burris and Sankappanavar's book, freely available 
    [here][6].

[^3]:
    This should be believable for a few reasons. Indeed, the "underlying set"
    functor is a _right_ adjoint, so we shouldn't expect it to play nicely 
    with any kind of colimit (like a quotient). 

    Moreover, $U$ playing nicely with congruences is 
    _one of the defining features_ of an _algebraic_ theory! 
    This is the key criterion for [monadicity][7]!

[^4]:
    If you haven't seen them before, it may come as a surprise that 
    "real mathematicians" care about lie groupoids, since they sound 
    quite abstract. But they're really not esoteric at all! They model 
    [orbifolds][8], which are manifolds with certain mild singularities.
    They arise incredibly naturally when studying, say, manifolds with 
    a group action.


[1]: https://richardblute.ca/octoberfest-2023/
[2]: https://ncatlab.org/nlab/show/algebraic+theory
[3]: https://ncatlab.org/nlab/show/essentially+algebraic+theory
[4]: https://en.wikipedia.org/wiki/Congruence_relation
[5]: https://en.wikipedia.org/wiki/Universal_algebra
[6]: https://math.hawaii.edu/~ralph/Classes/619/univ-algebra.pdf
[7]: https://ncatlab.org/nlab/show/monadicity+theorem
[8]: https://en.wikipedia.org/wiki/Orbifold
