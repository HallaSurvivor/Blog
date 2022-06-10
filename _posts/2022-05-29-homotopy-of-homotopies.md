---
layout: post
title: Why Care about the "Homotopy Theory of Homotopy Theories"?
tags:
  - 
---

I'm a TA at the [HoTTEST Summer 2022][1] summer school on homotopy type theory,
and while I feel quite comfortable with the basics of HoTT, there's a TON of 
things that I should really know better; so I've been reading a lot to prepare.
One of the things that I really didn't know _anything_ about was the theory of
[model categories][2]. I knew they had something to do with 
[$\infty$-categories][3] and homotopy theory... but I didn't really know
_what_ :P. Well, multiple papers later, I have a better idea of what's going on,
and I'll say a few words about it in this post. The focus, though, is going to
be on the "homotopy theory of homotopy theories" -- this was a groundbreaking 
development in the field... but one which seems _very_ abstract. I've been 
thinking about why we should care about this result, and in the process I 
discovered a _new reason_ to care about things! 

So then, let's get to it!

---

First of all, what even _is_ a "homotopy theory"? 
Let's look at the primordial example: 

<div class=boxed markdown=1>
Whatever a "Homotopy Theory" is, it should encompass the category $\mathsf{Top}$
of topological spaces where we identify spaces up to [(weak) homotopy equivalence][5]
</div>

But there's another motivating example, which we also call "homotopy":

<div class=boxed markdown=1>
Whatever a "Homotopy Theory" is, it should encompass the chains of modules,
where we identify two chains up to [homotopy equivalence][6]
</div>

Obviously these are related -- after all, from a topological space we can
get an associated chain of [(co)homology groups][7] with coefficients in our 
favorite abelian group. Then a homotopy of spaces induces a homotopy of chains.

More abstractly, what links these situations? Well, we have some objects that
we want to consider "the same up to homotopy", and we capture this 
(as the category inclined are liable to do) by picking out some special arrows.
These are the "homotopy equivalences" -- and they're maps that we want to 
think of as isomorphisms... but which might not _actually_ be.

So, in $\mathsf{Top}$, we have the class of weak homotopy equivalences[^1],
which we want to turn into isomorhpisms. And in $\mathsf{Ch}(R\text{-mod})$,
the category of chains of $R$-modules, we want to turn the [quasi-isomorphisms][8]
into isomorhpisms.

So then, with these examples in mind, what should a 
_homotopy theory_ be? First:

<div class=boxed markdown=1>
A <span class=defn>Relative Category</span> is a small[^8] category $\mathcal{C}$ 
equipped with a set of arrows
$\mathcal{W}$ (called the <span class=defn>Weak Equivalences</span>) 
that contains all the isomorphisms in $\mathcal{C}$[^7].
</div>

Following our examples, we want to think of the arrows in $\mathcal{W}$ as 
being _morally_ isomorphisms, even though they might not _actually_ be 
isomorphisms.

Now, a (small) category is an algebraic structure, so there's nothing stopping us from
just... adding in new arrrows, plus relations saying that they're inverses for
the arrows we wanted to be isomorphisms. By analogy with ring theory, 
we call this new category the <span class=defn>Localization</span> 
$\mathcal{C}[\mathcal{W}^{-1}]$. 

Finally, then:

<div class=boxed markdown=1>
A Homotopy Theory is a category of the form 
$\mathcal{C}[\mathcal{W}^{-1}]$ for some relative category.

⚠ The choice of $(\mathcal{C}, \mathcal{W})$ is far from unique. It's 
entirely possible[^11] for two relative categories to have the same homotopy category

$$\mathcal{C_1}[\mathcal{W_1}^{-1}] \simeq \mathcal{C_2}[\mathcal{W_2}^{-1}]$$
</div>

So, for instance, the classical homotopy category $\mathsf{hTop}$ and the 
derived category[^4] of $R$ modules $\mathcal{D}(R\text{-mod})$ are both
examples of homotopy theories.

---

This is great, but there's one hitch...
the localized category might be extremely complicated!
Indeed, it's possible that we end up with a _proper class_ of arrows between
two objects, even if $\mathcal{C}$ started out locally small. Moreover, since
arrows in the localized category are so hard to get our hands on,
it becomes unwieldy to do computations in this category 
(for instance, computing limits and colimits).


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
- $X$ is called <span class=defn>bifibrant</span> if it is both

Then we have axioms[^12] which imply that every object is weakly equivalent to a
bifibrant object. Since, after localizing, our 
weak equivalences become isomorphisms, this means we can restrict attention to
the bifibrant objects... But why bother?

It's a theorem that we have _excellent_ control over the maps between 
bifibrant objects in the localization! In fact, there's a notion of
"homotopy" between maps, which is entirely analogous to the notion of 
homotopy in topology, and maps $X \to Y$ in $\mathcal{C}[\mathcal{W}^{-1}]$
between bifibrant objects
are exactly homotopy classes of maps from $X \to Y$ in $\mathcal{C}$!

Thus, a very common way we use model structures to perform computations is by
first replacing the object we want to compute with by a weakly equivalent 
bifibrant one. For instance, we might replace a module by its injective 
resolution. Then maps in the homotopy category $\mathcal{C}[\mathcal{W}^{-1}]$ 
are just maps in $\mathcal{C}$ up to homotopy[^13]! 

This is made even more useful by the existence of _multiple_ model structures
on $(\mathcal{C}, \mathcal{W})$. Depending on the computation, we might choose
one model structure over another in order to make our lives as simple as possible.

Another reason is to help us understand when 
$\mathcal{C}_1[\mathcal{W}_1^{-1}] \simeq \mathcal{C}_2[\mathcal{W}_2^{-1}]$.
Indeed, there's a notion of [Quillen Equivalence][24], which is quite 
easy to work with, and guarantees that two quillen equivalent model categories
present the same homotopy theory[^14].

---

We should probably say a few words about the intuition for fibrations and
cofibrations.

A _fibration_ $f$ is an arrow that's easy to "lift" into:

<p style="text-align:center;">
<img src="/assets/images/homotopy-of-homotopies/fibration.png" width="30%">
</p>

For instance, covering spaces and bundles are examples of fibrations in 
topology. Algebraically, there's a model structure where a map of chains of 
$R$-modules $f : A_\bullet \to B_\bullet$ is a fibration if each $f_n$ is a surjection.

Dually, a _cofibration_ $i$ is an arrow that's easy to "extend" out of:

<p style="text-align:center;">
<img src="/assets/images/homotopy-of-homotopies/cofibration.png" width="30%">
</p>

We should think of a cofibration as being a subspace inclusion 
$A \hookrightarrow X$ where $A$ "sits nicely" inside of $X$.

For instance, the inclusion arrow of a "good pair" is a cofibration. Thus
inclusion maps of subcomplexes of a simplicial/CW/etc. complex are cofibrations. 
More generally, any subspace inclusion $A \hookrightarrow X$ where $A$ is a 
[nieghborhood deformation retract][23] in $X$.

Algebraically, the same model structure as before thinks that a map 
$f : A_\bullet \to B_\bullet$ is a cofibration exactly when each $f_n$ is an
injection whose cokernel is projective.

<br>

Precisely, these triangles are really special cases of squares. In the 
fibration case, the left side of the square is the unique map from the 
initial object to $A$. Dually, in the cofibration case the right 
hand side of the square should really be the unique map from $Y$ to the 
terminal object. 

This lets us unify these diagrams into a single axiom, which says that
a square of the form

<p style="text-align:center;">
<img src="/assets/images/homotopy-of-homotopies/full-square.png" width="30%">
</p>

has a lift whenever $i$ is a cofibration, $f$ is a fibration, and one of $i$
or $f$ is a weak equivalence. 

---

Now, back to the main storyline:

It turns out that localizing a model category forgets a _lot_ of information! 

This is to be expected somewhat, since we're intentionally adding extra 
isomorphisms to "forget" the distinction between certain objects. But it 
turns out to be a good idea to invert these arrows, yes, but to _remember_
how our arrows composed to give the new equivalence classes of arrows,
rather than identifying them outright[^9].

We can remember some of this by building an $\infty$-category,
called the <span class=defn>Simplicial Localization</span> instead.

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

but when we take connected components, these two points $f$ and $g$ are 
treated as the same arrow. 

<br>

Now, in the case of a relative category $(\mathcal{C},\mathcal{W})$, we build
an $\infty$ category by 

TODO: write this

Now _this_ is starting to feel more like Homotopy Type Theory[^5]!

---

This construction retains strictly more information, since we can easily 
recover the localization. Maps $f : A \to B$ in $\mathcal{C}[\mathcal{W}^{-1}]$
are the same thing as the connected components of the space of maps 
$A \to B$ in the simplicial localization! This should make intuitive sense,
as we connected two arrows exactly when they represented "the same map".

Moreover, (up to size issues) _every_ $\infty$-category arises from a 
pair $(\mathcal{C}, \mathcal{W})$[^10]. Since the $\infty$-categories inverted
$\mathcal{W}$, it's reasonable to think of $\infty$-categories as 
"homotopy theories" as well... But is there a way to make this precise?

---

TODO: mention quillen equivalences somewhere earlier?

Now we get to the point of this whole post. Why care about the 
"homotopy theory of homotopy theories"? What does that even _mean_?

To start, recall that we might want to consider two relative categories
"the same" if they present the same homotopy theory. That is, if

$$\mathcal{C_1}[\mathcal{W}_1^{-1}] \simeq \mathcal{C_2}[\mathcal{W}_2^{-1}]$$

but wait... $\mathsf{RelCat}$ has certain objects we would _like_ to 
consider equivalent? Are you thinking what I'm thinking?

It turns out that we can put a model structure on $\mathsf{RelCat}$,
where the weak equivalences are exactly those functors $f$ which 
become equivalences of $\infty$-categories! 
TODO: see "models for oo-cats part 2"

In this sense, $\mathsf{RelCat}$ becomes itself a homotopy theory! And the
homotopy classes of objects in $\mathsf{RelCat}$ are themselves (smaller)
homotopy theories! 

But what about $\infty$-categories, I hear you asking? Well, there's 
also a model structure on the category of simplicial categories! Impressively,
one can show that the homotopy category of $\mathsf{RelCat}$ is equivalent
to the homotopy category of $\mathsf{sCat}$, so that we might reasonably 
also say that $\mathsf{sCat}$ presents the homotopy theory of homotopy theories!

And _this_ is the new justification that I've found for high power or high 
abstraction theorems! 

Even though it's not clear to me how this high power construction helps us
compute things in practice, or lets us solve concrete problems, it still 
does something obviously useful! We have at least two competing notions of
what a homotopy theory _is_, which should intuitively be "the same". 

We could work with relative categories, or we could work with 
$\infty$-categories directly. It turns out that these have pros and cons
when we _do_ want to make explicit computations, and there's still _other_ models 
as well which also present the homotopy theory of homotopy theories!

Thankfully, since these categories all have the same homotopy category, 
we can use whichever is most convenient as our definition of a "homotopy theory".

The innovation of the "homotopy theory of homotopy theories", besides being 
objectively cool, allows us to make precise our intuition that these different
categories are "describing the same thing".


---


---

[^1]:
    It turns out there's _also_ a model category structure whose homotopy 
    category gives homotopy equivalence, rather than weak homotopy equivalence.

    But the model structure on $\mathsf{Top}$ which gives weak homotopy 
    equivalence is the "standard" one, so that's what I'm listing as the 
    motivating example.

[^3]:
    There's also intuition that the cofibrant objects are the ones which can
    be built by repeatedly gluing together "nice" objects. In $\mathsf{Top}$,
    for instance, the cofibrant objects are the CW-complexes, and in 
    $R$-mod, they're the injective resolutions.

[^4]:
    This was a pleasant surprise for me. I've heard a lot of talk about 
    derived categories, and they always seemed quite scary. It's been very
    exciting to feel like I'm getting a two-for-one deal every time I notice
    another concept in this subject start to make sense ^_^.

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

[^7]:
    Be careful, though, I've seen a handful of other definitions too!

[^8]:
    A better word would probably be "strict". Since we're going to be 
    treating $\mathcal{C}$ like an algebraic structure pretty soon, it 
    should have fixed _sets_ of objects and arrows, which we will manipulate
    like we might manipulate the underlying set of a group, ring, etc.

[^9]:
    If I'm being perfectly honest, I don't know why a homotopy theorist 
    would care about this. But I can _definitely_ speak to way a 
    logician might care!

    We can think about an arrow $A \to B$ as being a proof that $A$ implies $B$,
    or more properly, a function turning a proof of $A$ into a proof of $B$.
    Then the existence of multiple arrows is giving us multiple ways of 
    witnessing $A \to B$, which might have different _computational content_.

    Under the Curry-Howard correspondence, where proofs are programs, these 
    genuinely different proofs give different programs. Moreover, remembering 
    the simplicial structure (that is, remembering which weak equivalences composed
    in order to get a new arrow) is roughly the same as remembering the 
    _computation trace_ itself.

    For more information about this link, you should check out John Baez's 
    _Cohomology and Computation_ series [here][9]

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

[^11]:
    For example, $\mathsf{Top}$ with the weak homotopy equivalences gives 
    the same localization as the category of simplicial sets with the 
    [Quillen Model Structure][10].

    As an aside, as a topos theorist, this all feels a bit familiar. 

    Just like a model structure is some structure that presents a homotopy 
    theory in a way that lets us do concrete computation, a [site][11] is 
    a structure that presents a (grothendieck) topos and lets us do 
    concrete computations.

    Now, in the topos theory world, 
    Olivia Caramello's bridges program is based on the idea that we can 
    find nontrivial relationships between two sites presenting the same 
    topos... I wonder if there are any theorems that let us relate two 
    model categories presenting the same homotopy theory.

[^12]:
    I don't want to get into the precise details of a model structure here, 
    but you can (and should!) read more in Dwyer and Spalinski's excellent 
    introduction _Homotopy Theory and Model Categories_, available 
    [here][12], for instance. 

    There's also Mazel-Gee's _The Zen of $\infty$-Categories_, avaialable 
    [here][13], and Kantor's survey _Model Categories: Theory and Applications_,
    available [here][14].

    While we're at it, there's also Goerss and Schemmerhorn's 
    _Model Categories and Simplicial Methods_ ([here][15]), Hovey's book
    ([here][16]), and MO questions [here][17], [here][18], [here][19], and
    [here][20]. There's also Ponto and May's _More Concise Algebraic Topology_
    ([here][21]), but at some point I should stop. 

[^13]:
    For an example of this idea in action, see [this][22] answer of mine.

[^14]:
    In a stronger way than we currently have the language to describe.
    Not only are the localizations (read: homotopy categories) equivalent,
    but actually the presented $\infty$-categories are equivalent too!


[1]: https://uwo.ca/math/faculty/kapulkin/seminars/hottest_summer_school_2022.html
[2]: https://en.wikipedia.org/wiki/Model_category
[3]: https://ncatlab.org/nlab/show/%28infinity%2C1%29-category
[5]: https://en.wikipedia.org/wiki/Homotopy
[6]: https://en.wikipedia.org/wiki/Chain_complex#Chain_homotopy
[7]: https://en.wikipedia.org/wiki/Homology_(mathematics)
[8]: https://en.wikipedia.org/wiki/Quasi-isomorphism
[9]: https://math.ucr.edu/home/baez/qg-spring2007/qg-spring2007.html#computation
[10]: https://ncatlab.org/nlab/show/model+structure+on+simplicial+sets
[11]: https://ncatlab.org/nlab/show/site
[12]: https://math.jhu.edu/~eriehl/616-s16/DwyerSpalinski.pdf
[13]: https://etale.site/writing/zen-of-infty-cats.pdf
[14]: http://math.uchicago.edu/~may/REU2016/REUPapers/Kantor.pdf
[15]: https://sites.math.northwestern.edu/~pgoerss/papers/ucnotes.pdf
[16]: https://people.math.rochester.edu/faculty/doug/otherpapers/hovey-model-cats.pdf
[17]: https://mathoverflow.net/questions/361191/applications-of-model-categories
[18]: https://mathoverflow.net/questions/84381/computations-in-infty-categories
[19]: https://mathoverflow.net/questions/169187/what-non-categorical-applications-are-there-of-homotopical-algebra?noredirect=1&lq=1
[20]: https://mathoverflow.net/questions/78400/do-we-still-need-model-categories?noredirect=1&lq=1
[21]: http://www.math.uchicago.edu/~may/TEAK/KateBookFinal.pdf
[22]: https://math.stackexchange.com/questions/4461610/maps-in-the-homotopy-category-and-derived-category-to-and-from-concentrated-in/4461656#4461656
[23]: https://ncatlab.org/nlab/show/neighborhood+retract
[24]: https://ncatlab.org/nlab/show/Quillen+equivalence
