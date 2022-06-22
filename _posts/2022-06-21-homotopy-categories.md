---
layout: post
title: What Are Homotopy Theories, and Why Should We Care?
tags:
  - oo-categories
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
felt very disorganized and unfocused[^1]. So I decided to split it 
into three posts, with each post introducing a new, more abstract
option, and hopefully saying how it solves problems present in 
the more concrete settings.

Let's get to it!

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
where we identify two chains up to [homotopy equivalence][5]
</div>

Obviously these are related -- after all, from a topological space we can
get an associated chain of [(co)homology groups][6] with coefficients in our 
favorite abelian group. Then a homotopy of spaces induces a homotopy of chains.

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
$\mathcal{C}[\mathcal{W}^{-1}]$. 

For example, if we localize $\mathsf{Top}$ at the weak homotopy equivalences,
we get the classical homotopy category $\mathsf{hTop}$. If we invert the 
quasi-isomorphisms of chains of $R$ modules, we get the
derived category[^5] of $R$ modules $\mathcal{D}(R\text{-mod})$.

<div class=boxed markdown=1>
⚠ The choice of $(\mathcal{C}, \mathcal{W})$ is far from unique. It's 
entirely possible for two relative categories to have the same homotopy category[^6]

$$\mathcal{C_1}[\mathcal{W_1}^{-1}] \simeq \mathcal{C_2}[\mathcal{W_2}^{-1}]$$

Tentatively, we'll say that a homotopy theory is a relative category. 
But we'll say that two relative categories _present the same homotopy theory_
exactly when their localizations agree.
</div>

This "warning" that two relative categories can have the 
same homotopy theory should be viewed as a _feature_, not a bug! 
For instance, there's a notion of weak equivalence in $s\mathsf{Set}$, the 
category of [simplicial sets][8], and this has the same homotopy theory
as $\mathsf{Top}$ with its weak homotopy equivalences!

This means that if we have a question about topological spaces up to homotopy,
we can study simplicial sets instead, with _no loss of information_! This is
fantastic, since simplicial sets are purely combinatorial objects, so 
(in addition to other benefits)
it's much easier to tell a computer how to work with them[^7]!

---

This is great, but there's one hitch...

The homotopy category $\mathcal{C}[\mathcal{W}^{-1}]$ might be 
_terribly behaved_. For instance, even if $\mathcal{C}$ is (co)complete, 
the homotopy category might not be[^23]! 
Even worse, it's possible that we end up with a _proper class_ of arrows between
two objects, even if $\mathcal{C}$ started out locally small. 

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

There's a _zoo_ of techniques[^9] for working with homotopy categories, but
they all come down to trying to tame this unwieldy definition of arrow.
In this post, we'll be focusing on a very flexible approach where we endow
$(\mathcal{C}, \mathcal{W})$ with a <span class=defn>Model Structure</span>.

---

Roughly, to put a model structure on $(\mathcal{C}, \mathcal{W})$
(which we now assume to be complete and cocomplete) is to 
choose two new subfamilies of arrows: the 
<span class=defn>fibrations</span> and the <span class=defn>cofibrations</span>.
We then define the "nice" subclasses of objects: 

- $X$ is called <span class=defn>fibrant</span> if the unique arrow to the 
    terminal object is a fibration
- $X$ is called <span class=defn>cofibrant</span> if the unique arrow from 
    the initial object is a cofibration
- $X$ is called <span class=defn>bifibrant</span> if it is both fibrant and cofibrant

Then there are axioms[^10] which imply that every object is weakly equivalent to a
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
are just maps in $\mathcal{C}$ up to homotopy[^11]! 

This is made even more useful by the existence of _multiple_ model structures
on $(\mathcal{C}, \mathcal{W})$. Depending on the computation, we might choose
one model structure over another in order to make our lives as simple as possible.
For instance, we have two model structures on chain complexes, one based on 
[projectives][24] and one based on [injectives][25]. Then computations 
involving these model structures reduce to the classical projective or 
injective resolutions which you may recognize from homological algebra!

Another reason is to help us understand when 
$\mathcal{C}_1[\mathcal{W}_1^{-1}] \simeq \mathcal{C}_2[\mathcal{W}_2^{-1}]$.
Indeed this is solved by [Quillen Equivalence][26], which is quite 
easy to work with, and which guarantees that two model categories have the
same homotopy theory[^12].

For example, the earlier example of $\mathsf{Top}$ and $s\mathsf{Set}$,
which have the same homotopy theory, comes from a quillen equivalence.
See [here][27], for instance.

---

[^1]:
    This is one of the biggest problems with trying to explain things you know.
    Especially while you're still trying to sort them out yourself! 

    All of this material was scattered in my head with messy interconnections,
    but of course words have to be linearly ordered on a page. So any expositor
    has to figure out how to put these ideas into a fixed order. Ideally one
    that has a narrative that's easy to follow, and which motivates all of 
    the ideas involved.

    It's currently my fifth time restarting this post (now trilogy), but I 
    finally feel like I _really_ understand how things fit together and how 
    to put them all into a satisfying narrative. 

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
    another concept in this subject start to make sense ^_^.

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
    Even in the case of $\mathsf{hTop}$, we might not have (co)limits! 
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
    I don't want to get into the precise details of a model structure here, 
    but you can (and should!) read more in Dwyer and Spalinski's excellent 
    introduction _Homotopy Theory and Model Categories_, available 
    [here][22], for instance. 

    There's also Mazel-Gee's _The Zen of $\infty$-Categories_, avaialable 
    [here][23], Kantor's survey _Model Categories: Theory and Applications_,
    available [here][14], and of course, the [nlab][3].

    While we're at it, there's also Goerss and Schemmerhorn's 
    _Model Categories and Simplicial Methods_ ([here][15]), Hovey's book
    ([here][16]), and you can find a lot of good intuition in the 
    MO questions [here][17], [here][18], [here][19], and
    [here][20]. There's also Ponto and May's _More Concise Algebraic Topology_
    ([here][21]), but at some point I should stop. 

[^11]:
    For an example of this idea in action, see [this][22] answer of mine.

    For more about the precise definition of "homotopy" here, I'll again
    point you to Dwyer and Spalinski's [excellent introduction][22].

[^12]:
    In fact, this is true 
    in a stronger way than we currently have the language to describe.
    Not only are the localizations (read: homotopy categories) equivalent,
    but actually the presented $\infty$-categories are equivalent too!



[1]: HoTTEST Summer
[2]: oo-cats
[3]: model cats
[4]: sceond post on oo-cats
[5]: https://en.wikipedia.org/wiki/Chain_complex#Chain_homotopy
[6]: https://en.wikipedia.org/wiki/Homology_(mathematics)
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
[24]: projective modules
[25]: injective modules
[26]: quillen equivalence
[27]: https://ncatlab.org/nlab/show/classical+model+structure+on+simplicial+sets#quillen_equivalence_with_
