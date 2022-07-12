---
layout: post
title: Why Care about the "Homotopy Theory of Homotopy Theories"? (Homotopy Theories pt 4/4)
tags:
  - homotopy-theories
date: 2022-07-11 04:00
---

It's time for the last post of the series! Ironically, this is the post that
I meant to write from the start. But as I realized how much background
knowledge I needed to provide (and also internalize myself), various sections
got long enough to warrant their own posts. 
Well, three posts and around $8000$ words later, it's finally time!
The point of this post will be to explain what people mean when they 
talk about the "homotopy theory of homotopy theories", as well as to 
explain why we might care about such an object. 
After all -- it seems incredibly abstract! 

Let's get to it!

---

Let's take a second to recap what we've been talking about over the course
of these posts. 

We started with relative categories. These are categories $\mathcal{C}$ 
equipped with a set of arrows $\mathcal{W}$ (called _weak equivalences_) 
which we think of as morally being isomorphisms, even if they aren't 
_actually_ isos in $\mathcal{C}$. The classical examples are topological
spaces up to homotopy equivalence, and chains of $R$-modules up to 
quasiisomorphism.

In the first post, we defined the _localization_ (or the _homotopy category_)
$\mathcal{C}[\mathcal{W}^{-1}]$, which we get by freely inverting the arrows
in $\mathcal{W}$. We say that a _homotopy theory_ is a category of the form
$\mathcal{C}[\mathcal{W}^{-1}]$ up to equivalence.

Unfortunately, homotopy categories (to use a technical term)
suck. So we introduce [model structures][2] on $(\mathcal{C}, \mathcal{W})$,
which let us do computations in $\mathcal{C}[\mathcal{W}^{-1}]$ using the
data in $\mathcal{C}$. Model structures also give us a notion of 
[quillen equivalence][4], which allow us to quickly guarantee that two 
relative categories present the same homotopy theory (that is, they have
equivalent localizations)[^1].

Unfortunately again, model categories have problems of their own. While 
they're great tools for computation, they don't have the kinds of nice
"formal properties" that we would like. Most disturbingly, there's no good
notion of a functor between two model categories.

We tackled this problem by defining _simplicial categories_, which are 
categories that have a _space_ worth of arrows between any two objects,
rather than just a set. We call simplicial categories 
(up to equivalence) $\infty$-categories.

Now, we know how to associate to each relative category $(\mathcal{C}, \mathcal{W})$
an $\infty$-category via _hammock localization_.
Surprisingly, (up to size issues), _every_ $\infty$-category arises from a 
pair $(\mathcal{C}, \mathcal{W})$ in this way. 
With this in mind, and knowing how nice the world of $\infty$-categories is,
we might want to say a "homotopy theory" is an $\infty$-category rather than
a relative category.
Intuitively, the facts 
in the previous paragraph tell us that we shouldn't lose any information by
doing this... But the correspondence isn't _actually_ one-to-one.
Is there any way to remedy this, and put our intuition on solid ground?

Also, in the [previous post][7] we gave a second definition of 
$\infty$-category, based on [quasicategories][8]! 
These have some pros and some cons compared to the simplical category approach,
but we now have _three different definitions_ for "homotopy theory" 
floating around. Is there any way to get our way out of this situation?

---

To start, recall that we might want to consider two relative categories
"the same" if they present the same homotopy theory. With our new, 
more subtle tool, that's asking if

$$L^H(\mathcal{C}_1, \mathcal{W}_1) \simeq L^H(\mathcal{C}_2, \mathcal{W}_2)$$

but wait... There's an obvious category $\mathsf{RelCat}$ whose objects
are relative categories and arrows 
$$(\mathcal{C}_1, \mathcal{W}_1) \to (\mathcal{C}_2, \mathcal{W}_2)$$ are functors 
$$\mathcal{C}_1 \to \mathcal{C}_2$$ sending each arrow in $$\mathcal{W}_1$$ to
an arrow in $$\mathcal{W}_2$$.

Then this category has objects which are _morally_ isomorphic 
(since they have equivalent hammock localizations), but which are not
_actually_ isomorphic...

Are you thinking what I'm thinking!?

$\mathsf{RelCat}$ _itself_ forms a relative category, and
in this sense, $\mathsf{RelCat}$ becomes itself a homotopy theory whose 
objects are (smaller) homotopy theories! 

We can do the same thing with simplicial categories (resp. quasicategories) 
to get a relative category of $\infty$-categories. In fact, all three of 
these categories admit model structures, and are quillen equivalent!

This makes precise the idea that relative categories and $\infty$-categories
are really carrying the same information[^25]!

In fact, there's a _zoo_ of relative categories which all have the 
same homotopy category as $\mathsf{RelCat}$. We say that these are 
models of the "homotopy theory of homotopy theories", or equivalently,
that these are models of $\infty$-categories[^27].

<div class=boxed markdown=1>
If you remember earlier, we only gave a tentative definition of a 
homotopy theory. Well now we're in a place to give a proper definition!

A <span class=defn>Homotopy Theory</span> 
(equivalently, an <span class=defn>$\infty$-category</span>) is an object 
in any (thus every) of the localizations of the categories we've just discussed.
</div>

Perhaps unsurprisingly, we can do the same simplicial localization 
maneuver to one of these relative categories 
in order to get an $\infty$-category of $\infty$-categories!

But why care about all this?

It tells us that (in the abstract) we can make computations with either 
simplicial categories or quasicategories -- whichever is more convenient
for the task at hand. But are there any more concrete reasons to care?

---

Remember all those words ago in the [first post][12] of this series, 
I mentioned that hammock localization _works_, but feels somewhat 
unmotivated. Foreshadowing with about as much grace as a young 
fanfiction author, I asked if there were some more conceptual way to 
understand the hammock construction, which shows us "what's really going on".

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

With that last example, we're _finally_ done! This is easily the most 
involved (series of) posts I've ever written, so thanks for sticking through 
it!

I learned a _ton_ about model categories and $\infty$-categories while 
researching for this post, and I'm glad to finally have a decent idea of
what's going on. Hopefully this will be helpful for other people too ^_^.

Stay safe, all, and I'll see you soon!

---

[^1]:
    Note, however, that while most examples of two model categories with the
    same homotopy theory come from quillen equivalences, this does not have
    to be the case. See [here][6] for an example.

[^9]:
    This is a common theme, which shows up in logic as well!
    This is part of the deep connection between
    logic and homotopy theory that HoTT reveals!

    We can think about an arrow $A \to B$ as being a proof that $A$ implies $B$,
    or more properly, a function turning a proof of $A$ into a proof of $B$.
    Then the existence of multiple arrows is giving us multiple ways of 
    witnessing $A \to B$, which might have different _computational content_.

    Under the Curry-Howard correspondence, where proofs are programs, these 
    genuinely different proofs give different programs. Moreover, remembering 
    the simplicial structure (that is, remembering which weak equivalences composed
    in order to get a new arrow) is roughly the same as remembering the 
    _computation trace_ itself.

    For instance, there are two genuinely distinct ways of proving
    $p \land q \to p \lor q$:

    - $p \land q \to p \to p \lor q$
    - $p \land q \to q \to p \lor q$

    These compute different functions when viewed as programs, even though
    their types are the same.

    For more information about this link, you should check out John Baez's 
    _Cohomology and Computation_ series [here][9]. He also has a good discussion
    of this for computation in monoids [here][26]. I definitely went to a talk
    at CMU once where the speaker built a similar structure for the computation
    of $\lambda$-terms... But I can't find anything about that right now! 

    If someone happens to know a source, I would LOVE to hear about it ^_^

[^25]:
    When I was originally conceiving of this post, I wanted this to be the
    punchline. 

    The "homotopy theory of homotopy theories" is obviously _cool_, but it 
    wasn't clear to me what it actually _did_. I was initially writing up this 
    post in order to explain that I've found a new reason to care about heavy
    duty machinery: Even if it doesn't directly solve problems, it can allow
    us to make certain analogies precise, which we can maybe only see from a
    high-abstraction vantage point.

    Fortunately for me, but unfortunately for my original outline for this post,
    while writing this I've found _lots_ of other, more direct, reasons to care about
    this theory! So I've relegated this original plan to the 
    footnote you're reading... [right. now][38]. 

[^27]:
    See Juila Bergner's _A Survey of $(\infty,1)$-Categories_ 
    (available [here][9]) for more.

[1]: https://uwo.ca/math/faculty/kapulkin/seminars/hottest_summer_school_2022.html
[2]: https://en.wikipedia.org/wiki/Model_category
[3]: https://ncatlab.org/nlab/show/%28infinity%2C1%29-category
[4]: https://ncatlab.org/nlab/show/Quillen+equivalence
[5]: https://en.wikipedia.org/wiki/Homotopy
[6]: https://mathoverflow.net/questions/135717/examples-of-non-quillen-equivalent-model-categories-having-equivalent-homotopy-c
[7]: quasicategories
[8]: https://en.wikipedia.org/wiki/Quasi-category
[9]: https://arxiv.org/pdf/math/0610239.pdf
[10]: https://ncatlab.org/nlab/show/model+structure+on+simplicial+sets
[11]: https://ncatlab.org/nlab/show/site
[12]: model-categories
[26]: https://golem.ph.utexas.edu/category/2019/09/partial_evaluations_2.html#c056600

[28]: https://people.math.harvard.edu/~lurie/papers/highertopoi.pdf
[33]: https://ncatlab.org/nlab/show/model+structure+on+sSet-categories#ModelForInfinityCategories
[36]: https://en.wikipedia.org/wiki/Quasi-category
[37]: https://ncatlab.org/nlab/show/complete+Segal+space
[38]: https://youtu.be/YFX7SOLoi1Y?t=246
[39]: https://www.youtube.com/watch?v=3IjAy0gHRyY&list=PLsmqTkj4MGTDenpj574aSvIRBROwCugoB
