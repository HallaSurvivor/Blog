---
layout: post
title: Why Care about the "Homotopy Theory of Homotopy Theories"?
tags:
  - oo-categories
---

I'm a TA at the [HoTTEST Summer 2022][1] summer school on homotopy type theory,
and while I feel quite comfortable with the basics of HoTT, there's a TON of 
things that I should really know better, so I've been reading a lot to prepare.
One of the things that I really didn't know _anything_ about was the theory of
[model categories][2]. I knew they had something to do with 
[$\infty$-categories][3] and homotopy theory... but I didn't really know
_what_ :P. Well, multiple papers later, I have a better idea of what's going on,
and I'll say a few words about it in this post. The end goal will be the
"homotopy theory of homotopy theories" -- this abstract but groundbreaking
result seemed important, but it was tricky to find information about why
explicitly I should care about it. After some searching, I've found some reasons,
which I would love to share with you all ^_^.

So then, let's get to it!

---

---

It turns out this defect is because we're throwing out _too much information_
when we invert the arrows in $\mathcal{W}$. Rather than just inverting the 
arrows, we should keep track of how the arrows in $\mathcal{C}[\mathcal{W}^{-1}]$
are built from the old arrows and the new inverted arrows[^9]. This is a lot of
information, but we can conveniently think about it by using the language of
$\infty$-categories!

What's an $\infty$-category? I'm glad you asked!

<div class=boxed markdown=1>
  An <span class=defn>$\infty$-category</span> (properly an $(\infty,1)$-category)
  is a category "enriched in spaces"[^6]. Between any two objects we have a 
  homotopy-type worth of arrows. 

  There's a natural way of getting an ordinary category from an $\infty$-category,
  by keeping the same objects, but replacing the space of arrows $A \to B$ by
  its connected components. 
</div>





[^3]:
    There's also intuition that the cofibrant objects are the ones which can
    be built by repeatedly gluing together "nice" objects. In $\mathsf{Top}$,
    for instance, the cofibrant objects are the CW-complexes, and in 
    $R$-mod, they're the injective resolutions.

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
    I'm being intentionally vague here, but by "spaces" I mean the homotopy
    category of $\mathsf{Top}$. Or, equivalently,
    the homotopy category of $s\mathsf{Set}$!

    It turns out to be easier to work with simplicial objects, so that's what
    we'll be doing here.


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

[^10]:
    _Unfortunately_ not every 
    such system admits a compatible model structure. We say that an $\infty$-category
    is <span class=defn>Presentable</span> if it comes from a model structure --
    so the presentable $\infty$-categories are those in which we can do 
    computations. 

    This is analogous to a (finite) presentation of a group, say. Indeed, not every
    group has a finite presentation, and those that do don't have a _canonical_ 
    finite presentation. But if you _fix_ a presentation, it greatly expands the 
    kinds of (combinatorial and computational) tools for working with your group.

[^15]:
    You can read more in the (surprisingly readable!) paper 
    _Calculating Simplicial Localizations_ by Dwyer and Kan. 

    Another approach to simplicial localization is explained in another
    readable paper by the same authors: _Simplicial Localizations of Categories_.
    It's a perfectly good definition, and works well in the abstract, but 
    the "hammock" definition is more amenable to direct computation, since it's
    slightly more explicit.

    See [here][25] for more details.

[^16]:
    As before, we also allow the first map to face left instead of right,
    as long as our maps strictly alternate. What does this mean for our hammocks?
    The horizontal threads of our hammock must be oriented the same way!

    For instance, this is a valid hammock:

    <p style="text-align:center;">
    <img src="/assets/images/homotopy-of-homotopies/legal-hammock-1.png" width="30%">
    </p>

    This is a valid hammock:

    <p style="text-align:center;">
    <img src="/assets/images/homotopy-of-homotopies/legal-hammock-2.png" width="30%">
    </p>

    But this is _not_ a valid hammock:

    <p style="text-align:center;">
    <img src="/assets/images/homotopy-of-homotopies/illegal-hammock.png" width="30%">
    </p>



    Also, I can't express enough how much I love this naming idea! 
    It's quirky and apt in equal measure. 10/10.

[^17]:
    It's actually _slightly_ more general. The first arrow is also allowed to
    point left, as long as things still alternate. For instance, we allow 
    a zigzag of the form

    $$ A \overset{\sim}{\leftarrow} C_0 \to B $$

    as well.

    For the specifics of the construction, see 
    _Calculating Simplicial Localizations_ by Dwyer and Kan.

[^18]:
    And in case $(\mathcal{C}, \mathcal{W})$ admits a model structure
    (or even slightly less -- see _Calculating Simplicial Localizations_)
    we have ways of computing the homotopy type of $\text{Hom}(A,B)$ using
    only the data in $(\mathcal{C}, \mathcal{W})$! Again, see the paper.

[^19]:
    This is the plot of the first few chapters of Lurie's tome 
    [Higher Topos Theory][28]. 


[^21]:
    Though this post has been _particularly_ rambly because I've also been
    using it to get my thoughts about model categories and $\infty$-categories
    in order...

[^22]:
    By which I mean [Dwyer-Kan Equivalence][33], since $\infty$-categories are
    "really" objects in the homotopy category of homotopy categories, 
    equivalence comes from weak equivalences in one of the (many) model 
    categories presenting the homotopy theory of homotopy theories. 

    Throughout this post I'm implicitly working with Julie Bergner's 
    model structure on simplicial categories.

[^24]:
    I haven't forgotten that I said we can use $\infty$-categories to 
    solve the problems with localization. I'm going to put a discussion
    about the computational aspects of this theory in a follow up blog post,
    which was kind of a spin-off of some material I had to cut from this one.

    It'll (hopefully) be up on the same day I post this!

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

[^26]:
    It's actually not clear to me why we should care about _this_, but like...
    I know a lot about why we care about the ordinary category theoretic 
    analogues of these theorems. It doesn't take a ton of faith for me to 
    believe that they'll be useful in the $\infty$-category setting as well.

    That said, if anyone happens to know of any concrete applications of things
    like the adjoint functor theorem in the $\infty$-categorical setting, I
    would _love_ to hear about it!

[1]: https://uwo.ca/math/faculty/kapulkin/seminars/hottest_summer_school_2022.html
[2]: https://en.wikipedia.org/wiki/Model_category
[3]: https://ncatlab.org/nlab/show/%28infinity%2C1%29-category
[5]: https://en.wikipedia.org/wiki/Homotopy
[10]: https://ncatlab.org/nlab/show/model+structure+on+simplicial+sets
[11]: https://ncatlab.org/nlab/show/site
[25]: https://ncatlab.org/nlab/show/simplicial+localization
[26]: https://golem.ph.utexas.edu/category/2019/09/partial_evaluations_2.html#c056600
[27]: https://en.wikipedia.org/wiki/Simplicial_set#Face_and_degeneracy_maps_and_simplicial_identities
[28]: https://people.math.harvard.edu/~lurie/papers/highertopoi.pdf
[33]: https://ncatlab.org/nlab/show/model+structure+on+sSet-categories#ModelForInfinityCategories
[36]: https://en.wikipedia.org/wiki/Quasi-category
[37]: https://ncatlab.org/nlab/show/complete+Segal+space
[38]: https://youtu.be/YFX7SOLoi1Y?t=246
[39]: https://www.youtube.com/watch?v=3IjAy0gHRyY&list=PLsmqTkj4MGTDenpj574aSvIRBROwCugoB
