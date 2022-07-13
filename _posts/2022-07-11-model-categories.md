---
layout: post
title: What are Model Categories? (Homotopy Theories pt 1/4)
tags:
  - homotopy-theories
date: 2022-07-11 01:00
---

I'm a TA at the [HoTTEST Summer 2022][1], a summer school about 
Homotopy Type Theory, and while I feel quite comfortable with the 
basics of HoTT, there's a _ton_ of things that I should really know
better, so I've been doing a lot of reading to prepare. One thing
that I didn't know anything about was [$\infty$-categories][2],
and the closely related [model categories][3]. I knew they had
something to do with homotopy theory, but I didn't really know how.
Well, after lots of reading, I've finally figured it out, and I 
would love to share with you ^_^.

This was originally going to be one post, but it ended up having
a lot of tangentially related stuff all mashed together, and it
felt very disorganized and unfocused[^1]. So I've decided to split it 
into ~~three~~ four posts, with each post introducing a new, more abstract
option, and hopefully saying how it solves problems present in 
the more concrete settings.

Let's get to it!

---

First of all, what even _is_ a "homotopy theory"? 
Let's look at the primordial example: 

<div class=boxed markdown=1>
Whatever a "Homotopy Theory" is, it should encompass the category $\mathsf{Top}$
of topological spaces where we identify spaces up to [(weak) homotopy equivalence][38]
</div>

But there's another motivating example, which we also call "homotopy":

<div class=boxed markdown=1>
Whatever a "Homotopy Theory" is, it should encompass the chains of modules,
where we identify two chains up to [quasi-isomorphism][5]
</div>

Obviously these are related -- after all, from a topological space we can
get an associated "singular cochain" of $R$-modules.
Then a homotopy of spaces induces a homotopy of cochains, and indeed the
[cohomology][6] of the cochain complex agrees with the cohomology of the space
we started with.

More abstractly, what links these situations? Well, we have some objects that
we want to consider "the same up to homotopy", and we capture this 
(as the category inclined are liable to do) by picking out some special arrows.
These are the "homotopy equivalences" -- and they're maps that we want to 
think of as isomorphisms... but which might not _actually_ be.

So, in $\mathsf{Top}$, we have the class of weak homotopy equivalences[^2],
which we want to turn into isomorphisms. And in $\mathsf{Ch}(R\text{-mod})$,
the category of chains of $R$-modules, we want to turn the [quasi-isomorphisms][7]
into isomorphisms.

With these examples in mind, what should a _homotopy theory_ be?

<div class=boxed markdown=1>
A <span class=defn>Relative Category</span> is a small[^3] category $\mathcal{C}$ 
equipped with a set of arrows
$\mathcal{W}$ (called the <span class=defn>Weak Equivalences</span>) 
that contains all the isomorphisms in $\mathcal{C}$[^4].
</div>

Following our examples, we want to think of the arrows in $\mathcal{W}$ as 
being _morally_ isomorphisms, even though they might not _actually_ be 
isomorphisms.

Now, a (small) category is an algebraic structure. It's just a set
with some operations defined on it, and axioms those operations satisfy.
So there's nothing stopping us from just... adding in new arrows, 
plus relations saying that they're inverses for
the arrows we wanted to be isomorphisms. By analogy with ring theory, 
we call this new category the <span class=defn>Localization</span> 
$\mathcal{C}[\mathcal{W}^{-1}]$. This is also called the 
<span class=defn>Homotopy Category</span> of $(\mathcal{C}, \mathcal{W})$.

For example, if we localize $\mathsf{Top}$ at the weak homotopy equivalences,
we get the classical homotopy category $\mathsf{hTop}$. If we invert the 
quasi-isomorphisms of chains of $R$ modules, we get the
derived category[^5] of $R$ modules $\mathcal{D}(R\text{-mod})$.

<div class=boxed markdown=1>
Tentatively, then, we'll say that a _homotopy theory_ is a category of the 
form $\mathcal{C}[\mathcal{W}^{-1}]$.

Notice that the choice of $(\mathcal{C}, \mathcal{W})$ is far from unique. It's 
entirely possible for two relative categories to have the same homotopy category[^6]

$$\mathcal{C_1}[\mathcal{W_1}^{-1}] \simeq \mathcal{C_2}[\mathcal{W_2}^{-1}]$$

In this situation we say that $$(\mathcal{C}_1, \mathcal{W}_1)$$ and 
$$(\mathcal{C}_2, \mathcal{W}_2)$$ _present the same homotopy theory_.
</div>

There are many important examples of two relative categories
presenting the same homotopy theory. To start, let's consider the 
category $s\mathsf{Set}$ of [simplical sets][8], equipped with a notion
of weak equivalence. It turns out that this presents the same homotopy 
theory as $\mathsf{Top}$ with weak homotopy equivalences!

This means that if we have a question about topological spaces up to homotopy,
we can study simplicial sets instead, with _no loss of information_! This is
fantastic, since simplicial sets are purely combinatorial objects, so 
(in addition to other benefits)
it's much easier to tell a computer how to work with them[^7]!

---

This is great, but there's one hitch...

The homotopy category $\mathcal{C}[\mathcal{W}^{-1}]$ might be 
_terribly behaved_. For instance, even if $\mathcal{C}$ is (co)complete, 
the homotopy category almost never is[^8]! 
Even worse, it's possible that we end up with a _proper class_ of arrows between
two objects, even if $\mathcal{C}$ started out locally small. Lastly, it's
difficult to tell when two relative categories present the same homotopy 
theory.

This is all basically because arrows in $\mathcal{C}[\mathcal{W}^{-1}]$ are
_really hard_ to understand! After all, a general arrow from $A$ to $B$ in
$\mathcal{C}[\mathcal{W}^{-1}]$ looks like this:

$$
A \overset{\sim}{\leftarrow} 
C_0 \to 
C_1 \overset{\sim}{\leftarrow} 
\cdots
C_k \to B
$$

where all the $\overset{\sim}{\leftarrow}$s are in $\mathcal{W}$. 
After we invert $\mathcal{W}$, these arrows all acquire right-facing
inverses, which we can compose in this chain to get an honest arrow
$A \to B$.

There's a _zoo_ of techniques for working with homotopy categories, but
they all come down to trying to tame this unwieldy definition of arrow[^9].
In this post, we'll be focusing on a very flexible approach by endowing
$(\mathcal{C}, \mathcal{W})$ with a <span class=defn>Model Structure</span>.

---

Roughly, to put a model structure on $(\mathcal{C}, \mathcal{W})$
(which we now assume to be complete and cocomplete) is to 
choose two new subfamilies of arrows: the 
<span class=defn>fibrations</span> and the <span class=defn>cofibrations</span>.

From these, we define some "nice" classes of objects:

- $X$ is called <span class=defn>fibrant</span> if the unique arrow to the 
    terminal object is a fibration
- $X$ is called <span class=defn>cofibrant</span> if the unique arrow from 
    the initial object is a cofibration
- $X$ is called <span class=defn>bifibrant</span> if it is both fibrant and cofibrant

Let's see some examples:

A _fibration_ $f$ is an arrow that's easy to "lift" into from cofibrant objects $A$:

<p style="text-align:center;">
<img src="/assets/images/model-categories/fibration.png" width="30%">
</p>

For instance, covering spaces and bundles are examples of fibrations in 
topology. If we restrict attention to the [CW-complexes][36] then every
object is cofibrant, and this statement is basically the 
[homotopy lifting property][37] for covering spaces.

Algebraically, there's a model structure where a map of chains of 
$R$-modules $f : A_\bullet \to B_\bullet$ is a fibration if each $f_n$ is a surjection.
The cofibrant objects in this model structure are exactly the levelwise
projective complexes, so this lifting property becomes the usual 
lifting property for projective modules.

Dually, a _cofibration_ $i$ is an arrow that's easy to "extend" out of
provided our target $Y$ is fibrant:

<p style="text-align:center;">
<img src="/assets/images/model-categories/cofibration.png" width="30%">
</p>

We should think of a cofibration as being a subspace inclusion 
$A \hookrightarrow X$ where $A$ "sits nicely" inside of $X$.

For instance, the inclusion arrow of a "good pair" is a cofibration. Thus
inclusion maps of subcomplexes of a simplicial/CW/etc. complex are cofibrations. 
More generally, any subspace inclusion $A \hookrightarrow X$ where $A$ is a 
[nieghborhood deformation retract][28] in $X$ will be a cofibration.

Algebraically, a map
$f : A_\bullet \to B_\bullet$ is a cofibration exactly when each $f_n$ is an
injection whose cokernel is projective[^17]. This is a somewhat subtle condition,
which basically says that each $B_n \cong A_n \oplus P_n$ where $P_n$ is 
projective. It should be intuitive that given a map $A_n \to Y_n$, it's 
easy to extend this to a map $B_n \to Y_n$ under these hypotheses.

<br>

Precisely, these triangles are really special cases of squares. In the 
fibration case, the left side of the square is the unique map from the 
initial object to $A$. Dually, in the cofibration case the right 
hand side of the square should really be the unique map from $Y$ to the 
terminal object. 

This lets us unify these diagrams into a single axiom, which says that
a square of the form

<p style="text-align:center;">
<img src="/assets/images/model-categories/full-square.png" width="30%">
</p>

has a lift (the dotted map $X \to E$) 
whenever $i$ is a cofibration, $f$ is a fibration, and one of $i$
or $f$ is a weak equivalence. 

---

The model category axioms[^10] imply that every object is weakly equivalent to a
bifibrant object. Since, after localizing, our 
weak equivalences become isomorphisms, this means we can restrict attention to
the bifibrant objects... But why bother?

Well in any model category we have a notion of "homotopy" between maps 
$f,g : A \to B$ which is entirely analogous to the topological notion.
Then by studying homotopy-classes of maps, we'll be able to get a great
handle on the arrows in $\mathcal{C}[\mathcal{W}^{-1}]$!

Precisely, each object $A$ is weakly equivalent to a [cylinder object][31]
$A \times I$ which acts like $A \times [0,1]$ in topology[^13]. In particular,
it has two inclusions 
$\iota_0 : A \to A \times I$ and $\iota_1 : A \to A \times I$.

<div class=boxed markdown=1>
⚠ This is _not_ in general an actual product with some element $I$. 
It's purely notational. Some authors use $A \wedge I$ instead, but 
I don't really like that either. 

The best notation is probably $\text{Cyl}(A)$ or something similar, but
in this post I want to emphasize the relationship with the classical
topological case, so I'll stick with $A \times I$.
</div>

Now if $f, g : A \to B$, then a homotopy between $f$ and $g$ is
a map $H : A \times I \to B$ so that the following triangle commutes:

<p style="text-align:center;">
<img src="/assets/images/model-categories/homotopy-triangle.png" width="33%">
</p>

If there is a homotopy between $f$ and $g$, we say that $f$ and $g$ are 
_homotopic_ or _homotopy equivalent_, often written $f \sim g$.

This brings us to the big punchline:

<div class=boxed markdown=1>

Let $(\mathcal{C}, \mathcal{W})$ be a model category. 

1. If $A$ and $B$ are bifibrant then homotopy equivalence really is
an equivalence relation on $\text{Hom}_\mathcal{C}(A,B)$. Moreover, 
composition is well defined on the equivalence classes.

2. $\mathcal{C}[\mathcal{W}^{-1}]$ is equivalent to the category whose
objects are bifibrant objects of $\mathcal{C}$, and whose arrows are 
homotopy equivalence classes of arrows in $\mathcal{C}$.
</div>

Thus, a very common way we use model structures to perform computations is by
first replacing the objects we want to compute with by weakly equivalent 
bifibrant ones. For instance, we might replace a module by a projective 
resolution[^15]. Then maps in the homotopy category $\mathcal{C}[\mathcal{W}^{-1}]$ 
are just maps in $\mathcal{C}$ up to homotopy[^11]! 

Notice this, off the bat, solves one of the problems with homotopy categories.
Maybe $\mathcal{C}[\mathcal{W}^{-1}]$ isn't locally small, but it's 
_equivalent_ to something locally small. 

Moreover, model structures give us a very flexible way to tell when two 
relative categories have the same homotopy theory. Indeed, say we we have
a pair of adjoint functors $L \dashv R$ between $\mathcal{C}_1$ and 
$\mathcal{C}_2$ that respect the weak equivalences in the sense that 
$f : c_1 \to R(c_2)$ is in $\mathcal{W}_1$ if and only if its adjoint 
$\tilde{f} : L(c_1) \to c_2$ is in $\mathcal{W}_2$. 
Then $\mathcal{C}_1[\mathcal{W}_1^{-1}] \simeq \mathcal{C}_2[\mathcal{W}_2^{-1}]$,
and moreover, this equivalence can be computed from the adjunction $L \dashv R$.

This is called a [Quillen Equivalence][26] between $$(\mathcal{C}_1, \mathcal{W}_1)$$
and $$(\mathcal{C}_2, \mathcal{W}_2)$$[^12].

Moreover again, even if $\mathcal{C}[\mathcal{W}^{-1}]$ doesn't have (co)limits,
we _can_ always construct [homotopy (co)limits][30], which we can compute
using the same cylinder objects from before. For instance, the homotopy pushout
of 

<p style="text-align:center;">
<img src="/assets/images/model-categories/homotopy-pushout.png" width="30%">
</p>

will be the colimit of the related diagram:

<p style="text-align:center;">
<img src="/assets/images/model-categories/homotopy-pushout-full.png" width="50%">
</p>

Geometrically, rather than gluing $X$ to $Y$ along $A$ directly, 
we're adding a _path_ from $f(a)$ to $g(a)$. This is the same up to 
homotopy, but is better behaved. 
We do this by taking disjoint copies of $X$ and $Y$, and then gluing 
one side of the cylinder $A \times I$ to $X$ along $f$, and gluing the 
other side of $A \times I$ to $Y$ along $g$.

Something like this will always work, but knowing how to modify our diagram
(and why) can be quite involved[^14]. Thus we've succeeded in 
computationally solving the (co)limit issue, but it would be nice to have a 
more conceptual framework, in which it's obvious why this is the 
"right thing to do"... 

---

We've seen that a model structure on a relative category helps to make 
computations in the localized category $\mathcal{C}[\mathcal{W}^{-1}]$
effective (or even possible). But model categories have a fair number 
of problems themselves.

For one, there's no _great_ notion of a 
functor between model categories. In the case that a functor
$F : (\mathcal{C}_1, \mathcal{W}_1) \to (\mathcal{C}_2, \mathcal{W}_2)$
comes from and adjoint pair, then we can [derive][34] it to get a 
functor on the homotopy categories, but this is too restrictive to 
be the general notion of functor between model categories.

Related to functors, if $\mathcal{C}$ has a model structure and $\mathcal{I}$
is an indexing category, then $\mathcal{C}^\mathcal{I}$, the category of
$\mathcal{I}$-diagrams in $\mathcal{C}$ (with the pointwise weak equivalences)
may not have a model structure. See [here][35], for instance[^18]. 

With this in mind, we would like to have a version of the theory of model 
categories which has better "formal properties". While working with a 
_single_ model category is often quite easy to do, as soon as one looks
for relationships _between_ model categories, we're frequently out of luck.
In fact, since (co)limits come from functors, as soon as we're interested in
(co)limits we already run into this problem! This is one philosophical reason
for the complexity of homotopy (co)limits.

The solution lies upwards, in the land of $\infty$-categories. These are categories
with homotopy theoretic structure (in the classical sense of topological spaces)
built in from the start. Miraculously, these will solve all the above problems
and more -- while the category of model categories is a terrible place to live
(if we can define it at all...) the category of $\infty$-categories[^16]
is extremely similar to the category of categories. Then, since every 
model category presents an $\infty$-category, we'll be able to use this
machinery to solve our formal problems with model categories! 

How exactly does this work? You'll have to read more in [part 2][4]!

---

[^1]:
    This is one of the biggest problems with trying to explain things you know.
    Especially while you're still trying to sort them out yourself! 

    All of this material was scattered in my head with messy interconnections,
    but of course words have to be linearly ordered on a page, and it took 
    a lot of work to figure out how to put these ideas into a fixed order. 
    Especially one which has a nice narrative.

    It's currently my fifth time restarting this post (now ~~trilogy~~ tetralogy), 
    but I think I'm finally happy with my outline.
    I don't know why I'm writing this footnote, to be honest. But it felt
    like something I wanted to say, so here we are. 

    On with the show!

[^2]:
    It turns out there's _also_ a model category structure whose homotopy 
    category gives homotopy equivalence, rather than weak homotopy equivalence.

    But the model structure on $\mathsf{Top}$ which gives weak homotopy 
    equivalence is the "standard" one, so that's what I'm listing as the 
    motivating example.

[^3]:
    A better word would probably be "strict". Since we're going to be 
    treating $\mathcal{C}$ like an algebraic structure pretty soon, it 
    should have fixed _sets_ of objects and arrows, which we will manipulate
    like we might manipulate the underlying set of a group, ring, etc.

[^4]:
    Be careful, though, I've seen a handful of other definitions too!

    I like this one because it means the obvious way to turn a 
    category into a relative category is to take just the isomorphisms. 
    Then localization from $\mathsf{RelCat} \to \mathsf{Cat}$ is 
    left adjoint to the functor sending $\mathcal{C}$ to 
    $(\mathcal{C}, \{\text{isos}\})$.

    I'm not sure if I should require that $\mathcal{W}$ be closed under 
    composition... This doesn't _feel_ like it should break anything,
    but I'm not 100% sure.

[^5]:
    This was a pleasant surprise for me. I've heard a lot of talk about 
    derived categories, and they always seemed quite scary. It's been very
    exciting to feel like I'm getting a two-for-one deal every time I notice
    another concept in this subject start to make sense -- after all, it 
    means I'm learning about both homotopy theories _and_ derived categories!
    ^_^

[^6]:
    As an aside, as a topos theorist, this all feels a bit familiar. 

    Just like a model structure (which we'll define later) is some 
    structure that presents a homotopy 
    theory in a way that lets us do concrete computation, a [site][11] is 
    a structure that presents a (grothendieck) topos and lets us do 
    concrete computations.

    Now, in the topos theory world, 
    Olivia Caramello's bridges program is based on the idea that we can 
    find nontrivial relationships between two sites presenting the same 
    topos... I wonder if there are any theorems that let us relate two 
    model categories presenting the same homotopy theory.

[^7]:
    See, for instance, the sage documentation [here][9] and [here][10].

[^8]:
    Even in the case of $\mathsf{hTop}$, we don't have all (co)limits! 
    See [here][11], for instance!

[^9]:
    For instance you can only look at families $\mathcal{W}$ satisfying
    the [Ore Conditions][12]. These say exactly that we can "commute"
    weak equivalences past other arrows. Then, up to homotopy, every 
    arrow in the localization is of the form

    $$A \overset{\sim}{\leftarrow} C \to B$$

    and these are quite easy to manipulate. 

    See Sasha Polishchuk's lectures on Derived Categories 
    [here][13], for a really nice treatment using this language.

[^10]:
    Which I still haven't _really_ told you, haha.

    I don't want to get into the precise details of a model structure here, 
    but you can (and should!) read more in Dwyer and Spalinski's excellent 
    introduction _Homotopy Theory and Model Categories_, available 
    [here][22], for instance. 

    There's a lot of good places to get intuition for model structures as well.

    For instance, Mazel-Gee's _The Zen of $\infty$-Categories_, avaialable 
    [here][23], Kantor's survey _Model Categories: Theory and Applications_,
    available [here][14], and of course, the [nlab][3].

    While we're at it, there's also Goerss and Schemmerhorn's 
    _Model Categories and Simplicial Methods_ ([here][15]), Hovey's book
    ([here][16]), and you can find a lot of good intuition in the 
    MO questions [here][17], [here][18], [here][19], and
    [here][20]. There's also Ponto and May's _More Concise Algebraic Topology_
    ([here][21])... I could keep going, but I should probably get back to
    writing the main body of the post.

[^11]:
    For an example of this idea in action, see [this][29] answer of mine.

[^12]:
    For example, the earlier example of $\mathsf{Top}$ and $s\mathsf{Set}$,
    which have the same homotopy theory, comes from a quillen equivalence.
    See [here][27], for instance.

    In fact, quillen equivalence is stronger
    tronger way than we currently have the language to describe.
    Not only are the localizations (read: homotopy categories) equivalent,
    but actually the presented $\infty$-categories are equivalent too!

[^13]:
    We build $A \times I$ by factoring the codiagonal 
    $A \coprod A \to A$ as 

    $$A \coprod A \to A \times I \overset{\sim}{\to} A$$

    where $A \coprod A \to A \times I$ is a cofibration and
    where $A \times I \overset{\sim}{\to} A$ is both a fibration and a 
    weak equivalence. 
    
[^14]:
    Even though it's complicated, this _is_ a solved problem. We understand 
    how to take a diagram and massage it into a new, "homotopy coherent" 
    diagram.
    The idea is again one of bifibrant replacement! 

    In many cases we can put a model structure on the category of 
    functors into a model category $\mathcal{C}$. Then instead of taking the
    (co)limit of a diagram $F$, we cake the (co)limit of its bifrant replacement.

    See either the notes by Dugger [here][32] or by Hirschhorn [here][33]
    for specifics.

    Also, after reading those, notice that already the best way to organize 
    this data is with some kind of simplicial object... and keep a pin in that.

[^15]:
    This is made even more useful by the existence of _multiple_ model structures
    on $(\mathcal{C}, \mathcal{W})$. Depending on the computation, we might choose
    one model structure over another in order to make our lives as simple as possible.
    For instance, we have two model structures on chain complexes, one based on 
    [projectives][24] and one based on [injectives][25]. Then computations 
    involving these model structures reduce to the classical projective or 
    injective resolutions which you may recognize from homological algebra!

[^16]:
    In fact, it eats its own tail, and we have an $\infty$-category of 
    $\infty$-categories. But more on that later.

[^17]:
    Really we're describing the _projective_ model structure here. 
    There's a dual model structure with the same weak equivalences
    where we work with injectives instead.

[^18]:
    Though, thankfully, most model categories that arise in practice are 
    (quillen equivalent to) a (simplicial) combinatorial model category. 

    In particular, this means that we can usually put a model structure on 
    the category of diagram in $\mathcal{C}$. In fact, this is one way to
    effectively compute homotopy (co)limits in practice. We replace our 
    functor $F : I \to \mathcal{C}$ by a weakly equivalent bifibrant 
    functor $\tilde{F} : I \to \mathcal{C}$ and then output the 
    (weak equivalence class of) the (co)limit of $\tilde{F}$. 

    This is basically the derived functor approach to homotopy (co)limits,
    and while it's effective, it requires us to _choose_ a bifibrant 
    replacement. Much like choosing coordinates or a basis makes some proofs 
    more annoying in the setting of differential geometry or linear algebra
    (since we then have to prove our results are independent of this choice),
    we would like to have a choice-free way of defining homotopy (co)limits.


[1]: https://uwo.ca/math/faculty/kapulkin/seminars/hottest_summer_school_2022.html
[2]: https://ncatlab.org/nlab/show/infinity-category
[3]: https://en.wikipedia.org/wiki/Model_category
[4]: infinity-categories
[5]: https://en.wikipedia.org/wiki/Chain_complex#Chain_homotopy
[6]: https://en.wikipedia.org/wiki/Cohomology
[7]: https://en.wikipedia.org/wiki/Quasi-isomorphism
[8]: https://en.wikipedia.org/wiki/Simplicial_set
[9]: https://doc.sagemath.org/html/en/reference/categories/sage/categories/simplicial_sets.html
[10]: https://doc.sagemath.org/html/en/reference/topology/sage/topology/simplicial_complex.html
[11]: https://mathoverflow.net/questions/10364/categorical-homotopy-colimits
[12]: https://ncatlab.org/nlab/show/Ore+condition
[13]: https://www.youtube.com/watch?v=qFlt1XBNf4k&list=PLCe-H2N8-ny5nIYCQevWaJsO3PP44uz03&index=29
[14]: http://math.uchicago.edu/~may/REU2016/REUPapers/Kantor.pdf
[15]: https://sites.math.northwestern.edu/~pgoerss/papers/ucnotes.pdf
[16]: https://people.math.rochester.edu/faculty/doug/otherpapers/hovey-model-cats.pdf
[17]: https://mathoverflow.net/questions/361191/applications-of-model-categories
[18]: https://mathoverflow.net/questions/84381/computations-in-infty-categories
[19]: https://mathoverflow.net/questions/169187/what-non-categorical-applications-are-there-of-homotopical-algebra?noredirect=1&lq=1
[20]: https://mathoverflow.net/questions/78400/do-we-still-need-model-categories?noredirect=1&lq=1
[21]: http://www.math.uchicago.edu/~may/TEAK/KateBookFinal.pdf
[22]: https://math.jhu.edu/~eriehl/616-s16/DwyerSpalinski.pdf
[23]: https://etale.site/writing/zen-of-infty-cats.pdf
[24]: https://en.wikipedia.org/wiki/Projective_module
[25]: https://en.wikipedia.org/wiki/Injective_module
[26]: https://ncatlab.org/nlab/show/Quillen+equivalence
[27]: https://ncatlab.org/nlab/show/classical+model+structure+on+simplicial+sets#quillen_equivalence_with_
[28]: https://ncatlab.org/nlab/show/neighborhood+retract
[29]: https://math.stackexchange.com/questions/4461610/maps-in-the-homotopy-category-and-derived-category-to-and-from-concentrated-in/4461656#4461656
[30]: https://en.wikipedia.org/wiki/Homotopy_colimit
[31]: https://ncatlab.org/nlab/show/cylinder+object
[32]: https://pages.uoregon.edu/ddugger/hocolim.pdf
[33]: https://math.mit.edu/~psh/notes/hocolim.pdf
[34]: https://ncatlab.org/nlab/show/derived+functor
[35]: https://ncatlab.org/nlab/show/model+structure+on+functors
[36]: https://en.wikipedia.org/wiki/CW_complex
[37]: https://ncatlab.org/nlab/show/homotopy+lifting+property
[38]: https://ncatlab.org/nlab/show/weak+homotopy+equivalence
