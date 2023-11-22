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

An [essentially algebraic theory][3] is something like categories. It's a 
structure that can be defined as a set (or possibly multiple sets) with some 
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
so that $UH \cong (UG) \big / \theta$.

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

We've already touched on the relationship between 

- $$\{ \text{algebraic theories} \}
    \leftrightsquigarrow 
    \{ \text{finite product categories} \}$$
- $$\{ \text{essentially algebraic theories} \} 
    \leftrightsquigarrow 
    \{ \text{finite limit categories} \}$$

But it turns out the relationship goes _much_ deeper! Indeed, one can show 
that the "sets" in the above bullets actually represent $2$-categories, 
and that the correspondences are (contravariant) bi-equivalences!

Given a finite product (resp. finite limit) category $\mathcal{C}$, 
we treat it as an (essentially) algebraic theory, and say its 
<span class=defn>category of models</span> is the 
category of finite product (resp. finite limit) functors 
$\mathcal{C} \to \mathsf{Set}$.

In fact, we can go further! Given a finite product (resp. finite limit) categories 
$\mathcal{C}$ and $\mathcal{V}$, we say that the cateogry of 
<span class=defn>$\mathcal{C}$ models in $\mathcal{V}$</span> is the category 
of finite product (resp. finite limit) functors $\mathcal{C} \to \mathcal{V}$.

Conversely, given a category of models for some (essentially) algebraic theory, 
its category of ($\mathsf{Set}$-valued) finitely generated free algebras[^6] 
(resp. finitely presented algebras) has finite coproducts 
(resp. finite colimits). So if we take the opposite category of this, we get 
a category with finite products (resp. finite limits)!

It's then not _so_ hard to show that these operations are mutually inverse[^5]!


<br><br>

Now if we have an algebraic theory $\mathbb{A}$, that corresponds to a 
finite product category $\mathcal{A}$ where the category of 
$\mathbb{A}$-models is the functor category 
$\mathsf{FinProd}(\mathcal{A}, \mathsf{Set})$.

To view this as an essentially algebraic theory, we want to find a 
finite limit category $\mathcal{E}$ which has the same models. That is,
so that for every finite limit category $\mathcal{V}$:

$$
\mathsf{FinLim}(\mathcal{E}, \mathcal{V}) \cong 
\mathsf{FindProd}(\mathcal{A}, U \mathcal{V})
$$

where $U$ is the forgetful functor from finite limit categories to 
finite product categories.

This makes it clear that $\mathcal{E}$ should be the free finite 
limit completion of the finite product category $\mathcal{A}$ we 
started with! Since we already have products, all we have to do is 
freely add equalizers!

With this in mind, we see how to rephrase our problem of recognizing 
the algebraic theories among the essentially algebraic ones!

<div class=boxed markdown=1>
    Fix an essentially algebraic theory $\mathbb{E}$, with 
    (finite limit) classifying category $\mathcal{E}$.

    Then $\mathbb{E}$ is actually algebraic if and only if 
    $\mathcal{E}$ is equivalent to the 
    <span class=defn>free equalizer completion</span> of a 
    finite product category $\mathcal{A}$!

    This means if we want to recognize the algebraic theories, 
    we just need a way to recognize the essential image of 
    the equalizer completion functor!
</div>

Thankfully, there's a very heavy hammer we can use to understand 
the image of a left adjoint: [Comonadic Descent][10]!

---

I don't want to say too much about (co)monadic descent here, mainly because 
I'm going to a friend's concert tonight and I've already written quite a lot 
about it in my [recent preprint][11]. But here's the short story. We have a 
diagram of categories

<p style="text-align:center;">
<img src="/assets/images/ctoctoberfest2023/descent.png" width="50%">
</p>

where $\mathsf{FinLim}_{\mathsf{Eq} \ U}$ is the category of [coalgebras][12]
for the $\mathsf{Eq}\ U$ comonad, and the usual Barr-Beck yoga shows that 
everything in the image of $\mathsf{Eq}$ has a canonical coalgebra structure,
which is where the top map (which I'm abusively also calling $\mathsf{Eq}$)
comes from.

The adjunction $\mathsf{Eq} \dashv U$ is called 
<span class=defn>comonadic</span> exactly when this top map is an equivalence.
In particular, this means we can recognize the image of $\mathsf{Eq}$ 
in $\mathsf{FinLim}$ as those categories admitting an $\mathsf{Eq} \ U$ 
coalgebra structure!

It turns out to not be too hard to prove that this adjunction _is_ comonadic 
by using Beck's famed [(Co)monadicity Theorem][13]! This comes down to 
some combinatorics[^7] involving Pitt's explicit construction of the 
equalizer completion, first published in Bunge and Carboni's 
[_The Symmetric Topos_][14], which solves our problem!

Pedicchio and Wood, in their '99 paper 
[_A Simple Characterization of Theories of Varieties_][15], give a nice 
characterization of the image of $\mathsf{Eq}$ as those categories with 
enough "effective projectives"[^8]. 

---

Let me say a quick word about the "2-categorical" in the title. In the 
last section, to make use of the descent machinery, we had to work with 
1-categories $\mathsf{FinLim}$ and $\mathsf{FinProd}$. That is, with 
_stict_ such categories. Of course, this result should really be 
2-categorical in nature, working with _all_ such categories, and we should 
be using a 2-categorical version of comonadic descent to prove the theorem...
Unfortunately I don't know of one!

I was kind of hoping that someone would ask about this during the talk -- 
after all I put "2-categorical" in the title, but didn't mention 2-categories 
at all! But my talk was the first talk of the day[^9], so it makes sense 
that people would have been nice and not asked that.

Regardless, I'm pretty sure an australian would have a reference for this 
kind of descent
(and I might ask about it in the category theory zulip after posting this),
because there's no way I'm the first person to want to use it!

All in all, I'm happy with how the talk went. It was one of the shorter 
talks I've given, and I wanted to assume the audience didn't know a ton 
of logic. I think I did a good job giving the flavor of the theorem, 
and some reasons to care about it, without necessarily getting bogged 
down in the details of the proof. Hopefully I didn't come off as too 
upset that I was 24 years late to publish it myself!

As usual, here's a copy of the slides, abstract, and recording. 
I'll also encourage people to take a look at some of the other 
talks from the conference (which you can find [here][1]). There 
were a _ton_ of interesting ones[^10] and if you like category theory 
I'm sure you'll find something you enjoy!

Thanks again for reading. Stay warm, and try not to let the November 
darkness weigh on you too much! Talk soon ^_^

---

$2$-Categorical Descent and (Essentially) Algebraic Theories

An essentially algebraic theory is an algebraic theory that moreover allows 
certain partially defined operations. Since algebraic theories enjoy 
certain nice properties that essentially algebraic theories don’t, 
it’s natural to ask if we can recognize when an essentially algebraic theory 
is actually algebraic. In the language of functorial semantics, this amounts 
to recognizing when a finite limit category is the free completion of a 
finite product category, and the problem can be solved by considering a 
2-categorical descent theory. This was independent work, but writing it up 
I learned that the same result can already be found in a 1999 paper of 
Pedicchio and Wood. This seems to be less well known than it should be, 
and I hope this talk brings attention to this fascinating subject.

The slides are [here][16], and a recording is below:

<iframe width="560" height="315" src="https://www.youtube.com/embed/T-VVF30NiQA?si=OFGAvXfAe7U4eUtg" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>


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

[^5]:
    But they're only mutually inverse up to equivalence! If we start with a 
    finite limit category $\mathcal{C}$, and then look at the 
    opposite of the finitely presented objects in the functor category 
    $[\mathcal{C},\mathsf{Set}]$, then we merely get something _equivalent_ 
    to $\mathcal{C}$!

    In particular, we don't get something isomorphic to $\mathcal{C}$, 
    and we _definitely_ don't get something equal to $\mathcal{C}$!
    Some readers will likely say that concepts of "isomorphism" and 
    "equality" aren't even defined in a 2-category (they would say 
    bicategory, of course), but that's not a quibble I want to have right now.

    What matters is that there's something honestly 2-categorical happening 
    here, and we need that language to make this notion of "sameness" precise 
    in the same way we need 1-categories to make the notion of "isomorphism" 
    precise. I'm literally so close to finishing a blog post on 
    "2-categories and why you should care" that goes into this in more depth,
    but I wanted to say a word about it here. After all, rambling footnotes 
    are a feature of this blog!

[^6]:
    This is the _slightest_ of fibs. The situation for finite product 
    categories is actually slightly more sublte than I'm letting on,
    basically because a finite product category might not be 
    [cauchy complete][9]. If you know you know, if you don't, then trust 
    me that it doesn't really matter. If you're interested in the details, 
    you can find them in Adámek, Vitale, and Rosický's book
    _Algebraic Theories_.

[^7]:
    As many theorems do, at the end of the day. Thankfully our combinatorics 
    is also pretty polite.

[^8]:
    Though they work with the opposite of the categories we work with, 
    so for us they're more likely to be "effective injectives" after 
    dualizing.

[^9]:
    Which put it at 6am my time... Thankfully I've recently become a 
    morning person, so I only had to wake up an hour earlier than usual.

[^10]:
    And I haven't even had time to watch them all yet!

[1]: https://richardblute.ca/octoberfest-2023/
[2]: https://ncatlab.org/nlab/show/algebraic+theory
[3]: https://ncatlab.org/nlab/show/essentially+algebraic+theory
[4]: https://en.wikipedia.org/wiki/Congruence_relation
[5]: https://en.wikipedia.org/wiki/Universal_algebra
[6]: https://math.hawaii.edu/~ralph/Classes/619/univ-algebra.pdf
[7]: https://ncatlab.org/nlab/show/monadicity+theorem
[8]: https://en.wikipedia.org/wiki/Orbifold
[9]: https://ncatlab.org/nlab/show/Cauchy+complete+category
[10]: https://ncatlab.org/nlab/show/monadic+descent
[11]: /2023/10/05/descent-for-raags
[12]: https://ncatlab.org/nlab/show/coalgebra
[13]: https://ncatlab.org/nlab/show/monadicity+theorem
[14]: https://www.sciencedirect.com/science/article/pii/002240499400157X
[15]: https://www.sciencedirect.com/science/article/pii/S0021869300984473
[16]: /assets/docs/ctoctoberfest2023/talk.pdf
