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

As an example, we might have two arrows $f,g : A \to B$,
which are connected by homotopies $H$ and $K$. In this case we have a 
"circle's worth" of arrows from $A \to B$:

<p style="text-align:center;">
<img src="/assets/images/homotopy-of-homotopies/circle.png" width="30%">
</p>

When we take connected components, these two maps $f$ and $g$ are 
identified, so we only see one arrow in the homotopy category.

<br>

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
<img src="/assets/images/homotopy-of-homotopies/1hammock.png" width="50%">
</p>

Similarly, a $k$-cell will be a hammock that is $k$ strands "wide".
Here's the picture from the original paper:

<p style="text-align:center;">
<img src="/assets/images/homotopy-of-homotopies/wide-hammock.png" width="50%">
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
<img src="/assets/images/homotopy-of-homotopies/hammock.gif" width="50%">
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
<img src="/assets/images/homotopy-of-homotopies/oo-pushout.png" width="33%">
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
