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
and I'll say a few words about it in this post. The end goal, though, is going to
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

With these examples in mind, what should a _homotopy theory_ be? First:

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
A <span class=defn>Homotopy Theory</span> is a category of the form 
$\mathcal{C}[\mathcal{W}^{-1}]$ for some relative category.

⚠ The choice of $(\mathcal{C}, \mathcal{W})$ is far from unique. It's 
entirely possible for two relative categories to have the same homotopy category[^11]

$$\mathcal{C_1}[\mathcal{W_1}^{-1}] \simeq \mathcal{C_2}[\mathcal{W_2}^{-1}]$$
</div>

So, for instance, the classical homotopy category $\mathsf{hTop}$ and the 
derived category[^4] of $R$ modules $\mathcal{D}(R\text{-mod})$ are both
examples of homotopy theories.

As an aside, this "warning" that two relative categories can have the 
same homotopy theory should be viewed as a _feature_, not a bug! 
For instance, there's a notion of weak equivalence in $s\mathsf{Set}$, the 
category of [simplicial sets][30], and this has the same homotopy theory
as $\mathsf{Top}$ with its weak homotopy equivalences!

This means that if we have a question about topological spaces up to homotopy,
we can study simplicial sets instead, with _no loss of information_! This is
fantastic, since simplicial sets are purely combinatorial objects, so 
(in addition to other benefits)
it's much easier to tell a computer how to work with them[^20]!

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
We then define the "nice" subclasses of objects: 

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
first replacing the objects we want to compute with by weakly equivalent 
bifibrant ones. For instance, we might replace a module by its injective 
resolution. Then maps in the homotopy category $\mathcal{C}[\mathcal{W}^{-1}]$ 
are just maps in $\mathcal{C}$ up to homotopy[^13]! 

This is made even more useful by the existence of _multiple_ model structures
on $(\mathcal{C}, \mathcal{W})$. Depending on the computation, we might choose
one model structure over another in order to make our lives as simple as possible.

Another reason is to help us understand when 
$\mathcal{C}_1[\mathcal{W}_1^{-1}] \simeq \mathcal{C}_2[\mathcal{W}_2^{-1}]$.
Indeed, there's a notion of [Quillen Equivalence][24], which is quite 
easy to work with, and which guarantees that two model categories have the
same homotopy theory[^14].

For example, the earlier example of $\mathsf{Top}$ and $s\mathsf{Set}$,
which have the same homotopy theory, comes from a quillen equivalence.
See [here][29], for instance.

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
[nieghborhood deformation retract][23] in $X$ will be a cofibration.

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

<p style="text-align:center;">
<img src="/assets/images/homotopy-of-homotopies/hammock.gif" width="50%">
</p>

It turns out that localizing a model category forgets a _lot_ of information! 

This is to be expected somewhat, since we're intentionally adding extra 
isomorphisms to "forget" the distinction between certain objects. It 
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

but when we take connected components, these two maps $f$ and $g$ are 
identified.

<br>

This blog post is already plenty rambly, so I don't mind taking some
time to tell you how we can build an $\infty$-category from a 
relative category $(\mathcal{C},\mathcal{W})$.
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

---

So we see how to associate to each relative category $(\mathcal{C}, \mathcal{W})$
an $\infty$-category[^18].
Surprisingly, (up to size issues), _every_ $\infty$-category arises from a 
pair $(\mathcal{C}, \mathcal{W})$ in this way[^10]. Moreover, 
$\infty$-categories have much nicer formal properties than relative or model
categories. There's a huge body of literature[^19] showing how $\infty$-categories
behave analogously to $1$-categories (which is what we call "ordinary"
categories in this context). 

With this in mind, we might want to think of $\infty$-categories as 
"homotopy theories" rather than relative categories. Intuitively, the facts 
in the previous paragraph tell us that we shouldn't lose any information by
doing this... But the correspondence isn't _actually_ one-to-one.

Is there any way to remedy this, and put our intuition on solid ground?

---

Now we get to the point of this whole post[^21]. Why care about the 
"homotopy theory of homotopy theories"? What does that even _mean_?

To start, recall that we might want to consider two relative categories
"the same" if they present the same homotopy theory. With our new, 
more subtle tool, that's asking if

$$L^H(\mathcal{C}_1, \mathcal{W}_1) \simeq L^H(\mathcal{C}_2, \mathcal{W}_2)$$

but wait... There's an obvious category $\mathsf{RelCat}$ whose objects
are relative categories and arrows 
$(\mathcal{C}_1, \mathcal{W}_1) \to (\mathcal{C}_2, \mathcal{W}_2)$ are functors 
$\mathcal{C}_1 \to \mathcal{C}_2$ sending each arrow in $\mathcal{W}_1$ to
an arrow in $\mathcal{W}_2$.

So $\mathsf{RelCat}$ has some objects that are _morally_ equivalent,
but which aren't actually isomorphic? Are you thinking what I'm thinking!?

It turns out that we can put a model structure on $\mathsf{RelCat}$,
where the weak equivalences are exactly those functors $f$ for which
$L^H(f)$ is an equivalence[^22] of $\infty$-categories! Notice, by taking
components in each homset, this means they'll have the same localization too.

In this sense, $\mathsf{RelCat}$ becomes itself a homotopy theory! And the
homotopy classes of objects in $\mathsf{RelCat}$ are themselves (smaller)
homotopy theories! 

But what about $\infty$-categories, I hear you asking? Well, there's 
also a model structure on the category of simplicial categories! Impressively,
one can show that the homotopy category of $\mathsf{RelCat}$ is equivalent
to the homotopy category of $\mathsf{sCat}$, so that we might reasonably 
also say that $\mathsf{sCat}$ presents the homotopy theory of homotopy theories!

---

Let's slow down for a second, and say what we just said again.

<div class=boxed markdown=1>
We have a category $\mathsf{RelCat}$ whose objects are
(up to some notion of equivalence) homotopy theories.

We also have a category $\mathsf{sCat}$ whose objects are
(up to some notion of equivalence) $\infty$-categories.

Moreover, there is a quillen equivalence between $\mathsf{RelCat}$ and 
$\mathsf{sCat}$ (equipped with some natural model structures), so that 
we get an equivalence of homotopy theories

$$\mathsf{RelCat}[\mathcal{W}^{-1}] \simeq \mathsf{sCat}[\mathcal{W}^{-1}]$$

Now, the _objects_ of this homotopy theory are _themselves_ 
homotopy theories (objects of $\mathsf{RelCat}$), or equivalently, 
$\infty$-categories (objects of $\mathsf{sCat}$).
</div>

And _this_ is the new justification that I've found for high power or high 
abstraction theorems! 

---

Even though this construction of the homotopy theory of homotopy theories 
doesn't let us perform computations, or solve concrete problems 
(as far as I know), it's still an extremely useful construction!

Why care?

Well to start, it lets us firmly define "homotopy theory" and "$\infty$-category".
These should actually be seen as objects in this localized category,
a fact I've been hiding for most of this post.

This is good, because there are _lots_ of competing definitions for
$\infty$-category, all of which have pros and cons. By showing that they
all present the same homotopy category, this means that we can use 
whichever definition is most convenient for us! 

The situation is perfectly analogous to getting to work with topological
spaces or simplicial sets -- as long as we're only asking questions 
up to homotopy equivalence, they're interchangeable! Similarly, as long as
we're only asking questions about $\infty$-categories 
(equivalently homotopy theories) up to equivalence, we can use whichever
definition we want!

The innovation of the "homotopy theory of homotopy theories", besides being 
objectively cool, allows us to make precise our intuition that these different
categories are "describing the same thing", and that by itself is a reason to care.

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
    I'm being intentionally vague here, but by "spaces" I mean the homotopy
    category of $\mathsf{Top}$. Or, equivalently,
    the homotopy category of $s\mathsf{Set}$!

    It turns out to be easier to work with simplicial objects, so that's what
    we'll be doing here.

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

[^11]:
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
    In fact, this is true 
    in a stronger way than we currently have the language to describe.
    Not only are the localizations (read: homotopy categories) equivalent,
    but actually the presented $\infty$-categories are equivalent too!

[^15]:
    You can read more in the (surprisingly readable!) paper 
    _Calculating Simplicial Localizations_ by Dwyer and Kan. 

    The other approach to simplicial localization is explained in another
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

[^20]:
    See, for instance, the sage documentation [here][32].

    (Yes, I know about the subtle distinction between simplical complexes and
    simplicial sets. If you want to be a pedant, see the documentation 
    for the category structure [here][31])

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
[25]: https://ncatlab.org/nlab/show/simplicial+localization
[26]: https://golem.ph.utexas.edu/category/2019/09/partial_evaluations_2.html#c056600
[27]: https://en.wikipedia.org/wiki/Simplicial_set#Face_and_degeneracy_maps_and_simplicial_identities
[28]: https://people.math.harvard.edu/~lurie/papers/highertopoi.pdf
[29]: https://ncatlab.org/nlab/show/classical+model+structure+on+simplicial+sets#quillen_equivalence_with_
[30]: https://en.wikipedia.org/wiki/Simplicial_set
[31]: https://doc.sagemath.org/html/en/reference/categories/sage/categories/simplicial_sets.html
[32]: https://doc.sagemath.org/html/en/reference/topology/sage/topology/simplicial_complex.html
[33]: https://ncatlab.org/nlab/show/model+structure+on+sSet-categories#ModelForInfinityCategories
