---
layout: post
title: Locale Basics
tags:
  - locale-basics
---

This quarter I've been running a reading group for some undergraduates on
[pointless topology][1]. I want to take some time to write down a summary 
of the basics of locales (which are the object of study of pointless topology),
both so that my students can have a reference for what we've covered, and also
because I think there's still a space for a really elementary presentation of 
some of these topics, with a a focus on concrete examples.

So then, let's get to it ^_^

TODO: mention that this post is going to be about various ways of 
building locales from scratch. We'll write a follow up later where
we talk about how to build new locales from old.

---

Our first few weeks were a crash course on the kind of category theory
that I usually assume my readers know already. We focused on partial orders
and lattices -- this is particularly economical for a few reasons:

First, posets and lattices are simple combinatorial objects that you can 
understand without much background in abstract algebra or topology. We also
get two "levels" of categories out of this, since every poset is a category
in its own right, but we can also consider the category of posets, or any 
one of the zoo of categories of lattices.

In fact, the zoo of lattice categories is nice, because it forces you to 
acknowledge that it's the _arrows_ that matter. After all, frames 
(which we'll define soon) and complete heyting algebras are the same thing! 
We can only distinguish between the categories because the homomorphisms are different.

This means that we can see categorical constructions in multiple lights 
very quickly: Products in a poset are meets, while products in the _category_
of posets are given by a poset of tuples. Adjoint functors between posets
are [galois connections][2], while adjoint functors between the categories
of posets and meet semilattices might be a free/forgetful pair, etc.

After spending time getting to adjoint functors, we defined a topological 
space, and then observed that the lattice of open sets has a certain 
algebraic structure: 

 - Opens are closed under finite intersection
 - Opens are closed under arbitrary union

which we abstract into a definition[^1]:

<div class=boxed markdown=1>
  A <span class=defn>Frame</span> is a lattice $(F, 0, 1, \land, \lor)$ 
  which is closed under _arbitrary_ joins, which we write as $\bigvee a_\alpha$.

  Moreover, we have to explicitly require that 

  $$a \land \left ( \bigvee b_\alpha \right ) = \bigvee (a \land b_\alpha)$$

  (since lattices are not automatically distributive).

  A <span class=defn>Homomorphism of Frames</span> is a map $\varphi : F \to G$
  which preserves finite meets and arbitrary joins.
</div>

Now, since we know that a continuous maps of topological spaces 
$(X,\tau) \to (Y,\sigma)$ 
are in bijection with frame homomorphisms from $\sigma \to \tau$, we 
_define_ the category of <span class=defn>Locales</span> to be opposite
the category of Frames.

---

With these definitions in hand, it's high time for some examples! 

The first important class of examples are the "geometric" ones. 
Every topological space[^2] is specified in terms of either a [base][4]
or a [subbase][5], and we can imitate these constructions exactly in the
world of locales.

Let's do the real numbers to start. These have a basic open for each interval
$(a,b)$. Classically we can take all such intervals, but constructively it's
more hygienic to take only the intervals with rational endpoints. Obviously
these generate the same topology, so we're not losing anything by doing this.

Now, the intervals $(a,b)$ form a [meet semilattice][6] where we define

$$
(a,b) \wedge (a', b') = (\max(a,a'), \min(b,b'))
$$

with the convention that $(a,b) = \bot$ whenever $b \lt a$.

<div class=boxed markdown=1>
As an easy exercise, draw a picture of two intervals $(a,b)$ and $(a',b')$
and convince yourself that their intersection is really given by the meet
as defined above
</div>

This is telling us that our open intervals really are a _basis_ in the 
strong sense that the intersection of two basic opens is basic open. 

From here, we want to define a topology by declaring an open set to be an 
arbitrary union of the basic opens. In the locale-theoretic world, we 
take this meet-semilattice and (freely) close it under arbitrary joins! 

To do that, we recall the adjunction 

<p style="text-align:center;">
<img src="/assets/images/locale-basics/downset-adjunction.png" width="25%">
</p>

where (as usual) $U$ is the forgetful functor and $\mathcal{D}$ is the 
_downset functor_, which sends a poset $P$ to the lattice $\mathcal{D} P$ whose 
elements are the downwards-closed subsets of $P$[^3]. The unit of this adjunction
sends $p \in P$ to $$\downarrow p = \{ x \in P \mid x \leq p \}$$.

Then, at the end of the day, we can define the locale $\mathbb{R}$ to be 
generated by the basic opens $(a,b)$ with $a \lt b \in \mathbb{Q}$. These 
assemble into a meet-semilattice $P$, and the downset lattice 
$\mathcal{D} P$ is a frame.

<div class=boxed markdown=1>
  As a nice exercise, you should check that $\mathcal{D}P$ really is a 
  frame. Moreover, that the inclusion $P \hookrightarrow \mathcal{D}P$ 
  preserves $\land$.
</div>

Of course, there's nothing special about $\mathbb{R}$ here! 

Given any meet-semilattice of basic open sets[^4] $(M, \wedge)$,
the downsets $\mathcal{D}M$ form a locale where every open is the 
union of basic opens in $m$ (here, as usual, we identify $m \in M$ with
the principal downset $\downarrow m \in \mathcal{D}M$).

<div class=boxed markdown=1>
  Can you modify the construction of $\mathbb{R}$ to build a locale for 
  $\mathbb{R}^2$, or more generally $\mathbb{R}^n$?

  In the next blog post of the series, we'll talk about product locales, 
  and we'll show that $\mathbb{R} \times \mathbb{R} \cong \mathbb{R}^2$.
</div>

For another example of building locales from a geometric space, let's
build $S^1$ together! We have a few options for how to do this.

In practice, we use the fact that $S^1$ as a topological space is hausdorff,
thus [sober][10]. Then we appeal to an important theorem 
(which we'll discuss later) that the full subcategory of sober topological
spaces is equivalent to the full subcategory of spatial locales. 

In particular, the usual topology on $S^1$, viewed as a frame, gives a locale
for $S^1$ with no changes necessary.

If we need to, though, we can also build $S^1$ by hand. After all, we can 
describe the open arcs and their intersections as basic opens, then take 
downsets just as we did for $\mathbb{R}$.

However, it would be nice if we could somehow define $S^1$ to be 
$\mathbb{R} / \mathbb{Z}$. In all my reading, I've never actually seen
anybody talk about how to do this, so this blog post seems like a perfect place!

If $\mathbb{Z}$ is acting on $\mathbb{R}$ by translation, 
that means we have an action of $\mathbb{Z}$ on the frame of opens of 
$\mathbb{R}$, where a basic open $(p,q)$ pulls back to the basic open 
$(p-1,q-1)$.

Since locales are dual to frames, a _quotient locale_ (that is, an 
epimorphism) should correspond to a _subframe_ (that is, a monomorphism),
and a moment's meditation on the [quotient topology][11] shows that 
we want to consider the sublocale of open sets fixed by the $\mathbb{Z}$ action.
So a typical open in this sublocale looks like 

$$\bigvee_{n \in \mathbb{Z}} (p-n, q-n)$$

Intuitively, we're identifying an open set of $S^1$ with its preimage in $\mathbb{R}$,
which lets us identify the frame of opens of $S^1$ with a subframe of the 
opens of $\mathbb{R}$.

TODO: put a picture here? 
Take an open arc of the circle, and show its preimage in $\mathbb{R}$

TODO: talk about flat sites

---

Of course, locale theory (like most of my interests) has a dual nature 
as a geometirc subject and a logical subject. The previous section was 
about locales which arise from geometric objects, but what about locales
arising logically?

Let's start with the notion of a (propositional) [geometric theory][12].

<div class=boxed markdown=1>
  Fix a family of "primitive propositions" $P_\alpha$. Then 
  <span class=defn>geometric formulas</span> are described by the
  following grammar:

  $$
  \begin{align}
  \varphi 
  ::=& \ P_\alpha \\
  &|   \ \top \\
  &|   \ \bot \\
  &|   \ \varphi \land \psi \\
  &|   \ \varphi \lor  \psi \\
  &|   \ \bigvee \varphi_\alpha
  \end{align}
  $$

  Next, a <span class=defn> geometric sequent</span> is an object of the form

  $$\varphi_1, \ldots, \varphi_n \vdash \psi$$

  where $\varphi$ and $\psi$ are geometric formulas. We interpret this as 
  expressing "whenever all of the $\varphi_k$ are true, $\psi$ is true too".

  Finally, a <span class=defn>geometric theory</span> is a set $\mathbb{T}$ of
  geometric sequents, which we think of as _axioms_ for $\mathbb{T}$.
</div>

There is a [sequent calculus][13] for geometric logic, which, for those in the
know, is exactly what you expect[^6]. All that we need to know is that it lets
us _derive_ the truth of certain sequents in a way that formally mirrors the 
way we prove things as mathematicians. For instance, one can derive the sequent
$\varphi \land \psi \vdash \psi \land \varphi$, which tells us that $\land$ 
is commutative.

This is important because the language[^7]
$$L(\{ P_\alpha \})$$
is a preorder if we define $\varphi \leq \psi$ by $\varphi \vdash \psi$.
Intuitively, elements "higher up the poset" are "more true", with $\top$ and
$\bot$ as the top and bottom elements. 

If we then quotient by the equivalence relation of $x \leq y \leq x$ 
(so we consider two provably-equivalent formulas to be "the same") then we get a 
frame, where the lattice operations are given by the logical ones[^8]!
In fact, this construction gives the _free_ frame generated by the set
$\{ P_\alpha \}$ of primitive propositions.

Now, given a theory $\mathcal{T}$ with primitive propositions $\{ P_\alpha \}$,
we define the <span class=defn>Lindenbaum Algebra</span> $\mathcal{L}[\mathbb{T}]$
to be the frame of formulas in $\{ P_\alpha \}$ modulo the relations 

$$\varphi_1, \ldots, \varphi_n \leq \psi$$

for each $\big ( \varphi_1 \ldots, \varphi_n \vdash \psi \big ) \in \mathbb{T}$.

This is again a frame, which we should think of as the formulas in $$L(\{P_\alpha\})$$
up to provable equivalence, where now we may use the sequents in $\mathbb{T}$ 
as axioms in our proofs[^9]! 

This was all very abstract, so let's see some concrete examples:

Let $X$ be a set, and consider a theory $\mathbb{T}$ with one primitive proposition 
$\sigma_{x,y}$ for each $x,y \in X$, and axioms

$$
\begin{align}
\top                       &\vdash \bigvee_{y \in X} \sigma_{x,y} 
&&\text{(for each $x \in X$)} \\

\sigma_{x,y}, \sigma_{x,z} &\vdash \bot 
&& \text{(for $y \neq z \in X$)} \\

\sigma_{x,y}               &\vdash \sigma_{y,x}
\end{align}
$$

What's the use of this theory? Well recall a (classical) model of a 
(propositional) theory $\mathbb{T}$ is exactly a frame homomorphism
$$\mathcal{L}[\mathbb{T}] \to \{ 0, 1 \}$$.

Now, a model of this theory assigns each $\sigma_{x,y}$ to $0$ or $1$,
thus a model is really picking out a subset of $X \times X$ -- 
namely those pairs $(x,y)$ so that $\sigma_{x,y} = 1$.

Through this lens, the first two axioms express that for every $x$,
there is _exactly one_ $y$ with $\sigma_{x,y} = 1$, so that our model
is naming a _function_ (which I'll call $f_\sigma : X \to X$). The last
axiom is asserting that $f_\sigma(x) = y$ implies $f_\sigma(y) = x$. That is,
$f_\sigma$ should be an involution!

So (classical) models of $\mathbb{T}$ are exactly $\mathbb{Z}/2$ actions on $X$.

We can push this further, though! 

Consider a theory $\mathbb{T}$ with primitive propositions $\theta_{n,x}$
for $n \in \mathbb{N}$ and $x \in \mathbb{R}$, and the axioms

$$
\begin{align}
\top &\vdash \bigvee_{x \in \mathbb{R}} \theta_{n,x}
&& \text{(for each $n \in \mathbb{N}$)} \\

\theta_{n,x}, \theta_{n,y} &\vdash \bot
&& \text{(for $x \neq y \in \mathbb{R}$)} \\

\top &\vdash \bigvee_{n \in \mathbb{N}} \theta_{n,x}
&& \text{(for each $x \in \mathbb{R}$)}
\end{align}
$$

As before, the first two axiom schemas assert that for any (classical)
model of $\mathbb{T}$, the subset $$\{ (n,x) \mid \theta_{n,x} = 1 \}$$ 
defines a function $f_\theta : \mathbb{N} \to \mathbb{R}$. But the last axiom
asserts that $f_\theta$ should be surjective!

Thus, this theory has no (classical) models. But it is still an interesting
object of study, in part for reasons to be discussed in the next section. 

Lastly, though, we should show that _every_ locale arises in this way! We 
say that a locale $\mathcal{L}[\mathbb{T}]$ is the 
<span class=defn>classifying locale</span> for the theory $\mathbb{T}$, 
and now we'll show that every locale classifies a certain canonical theory[^10]


---

TODO: Points, geometrically, then as models

TODO: N --> R is pointless!

---

Exercises

<div class=boxed markdown=1>
  Show that every frame is also a [Heyting Algebra][8]. You can do this
  with abstract nonsense (use the [adjoint functor theorem][9]) or directly
  (give an explicit expression for the arrow $a \implies b$).

  You should do whichever comes less naturally to you 
  (or both, if neither comes naturally).

  As a part 2, you should show that _defining_ frames to be complete 
  heyting algebras is incorrect, since morphisms of heyting algebras 
  should preserve $\implies$, whereas frame homomorphisms don't need to[^5].
</div>

---

Sign off

---

[^1]:
    The definition given on the [nlab][3] is nice because it make the analogy
    with topoi incredibly clear. It's an easy exercise that our definitions
    are equivalent.

[^2]:
    That I can think of right now

[^3]:
    There's actually a _lot_ to say about this construction! It turns out that
    $\mathcal{D}P$ is the same thing as $[P^\text{op},2]$, the monotone maps from 
    $P^\text{op}$ to the two element poset $$\{0,1\}$$ with $0 \leq 1$.

    Then $\mathcal{D}P$ is nothing but the "presheaves on $P$" if we enrich 
    over $2$ instead of $\mathsf{Set}$. This makes it clear that it should be
    the free way of adding joins (colimits) to $P$, by analogy to the presheaves on a 
    category $\mathcal{C}$ being the "free cocompletion" of $\mathcal{C}$.

    There's a _lot_ to say here, since frames/locales are analogous in _many_
    was to grothendieck topoi, and this method of getting a locale by looking
    at "presheaf posets" is one instance of that analogy!

[^4]:
    Notice that we're assuming the intersection of two basic opens is itself
    basic open. The usual definition is that the intersection of two basic 
    opens merely _contains_ a basic open -- this seems like a property that
    should have a name, but I don't know of one. Hopefully someone can
    leave a comment clarifying this ^_^

    Either way, we'll relax this assumption later on in the post!

[^5]:
    You can see [this][7] mathoverflow question if you need a hint.

[^6]:
    We have the usual [structural rules][14], 
    and all the connectives work in the traditional way, with the rules for 
    infinite disjunction being the natural generalization of the usual disjunction
    rules. We won't need to know the intricacies of the system here, so I'll omit
    a full description, but the interested reader can find one in section D1.3 
    of the elephant.

[^7]:
    That is, the set of geometric formulas with the given primitive propositions

[^8]:
    So, for instance, given two equivalence classes of formulas
    $[\varphi]$ and $[\psi]$, their meet in the frame will be given by 
    the class of their conjunction $[\varphi \land \psi]$.

    Similarly, for (infinitary) joins and disjunction.

    This is why we need to quotient by provable equivalence, because 
    $\varphi \land (\psi \land \theta)$ and $(\varphi \land \psi) \land \theta$
    are _technically_ two different formulas. Though they're provably equivalent,
    which is all we need to claim that $\land$ is associative!

[^9]:
    You'll often hear logicians talk about formulas 
    "up to $\mathbb{T}$-provable equivalence". 

    This is what we're talking about!

[^10]:
    Though this sounds much more exciting than it is... Prepare to be underwhelmed :P

[1]: https://en.wikipedia.org/wiki/Pointless_topology
[2]: https://en.wikipedia.org/wiki/Galois_connection
[3]: https://ncatlab.org/nlab/show/frame
[4]: https://en.wikipedia.org/wiki/Base_(topology)
[5]: https://en.wikipedia.org/wiki/Subbase
[6]: https://en.wikipedia.org/wiki/Semilattice
[7]: https://mathoverflow.net/questions/248711/an-example-of-a-frame-homomorphism-which-does-not-preserve-heyting-implication
[8]: https://en.wikipedia.org/wiki/Heyting_algebra
[9]: https://ncatlab.org/nlab/show/adjoint+functor+theorem
[10]: https://en.wikipedia.org/wiki/Sober_space
[11]: https://en.wikipedia.org/wiki/Quotient_space_(topology)
[12]: https://ncatlab.org/nlab/show/geometric+theory
[13]: https://en.wikipedia.org/wiki/Sequent_calculus
[14]: https://en.wikipedia.org/wiki/Structural_rule