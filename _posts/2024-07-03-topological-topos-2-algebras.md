---
layout: post
title: Life in Johnstone's Topological Topos 2 -- Topological Algebras
tags:
  - life-in-the-topological-topos
---

In the [first post][5], we introduced Johnstone's topological topos $\mathcal{T}$ 
and talked about what its objects look like. We showed how the interpretation 
of type theory in $\mathcal{T}$ gives us an "intrinsic topology" on any 
type we construct. We also alluded to the fact that, by working in $\mathcal{T}$ 
as a universe of sets, we're able to interact with _topological_ gadgets 
by forgetting about the topology entirely and just manipulating them naively 
as we would sets!

In this post, we'll talk about how that works in the special case of 
algebraic gadgets, like groups, rings, etc., and use this to prove some 
interesting theorems about topological groups!

---

Recall Lawvere's notion of [Functorial Semantics][1]. 
An <span class=defn>Algebraic Theory</span> is presented by some 
function symbols and equational axioms 
(we allow constant symbols as 0-ary functions), and this is probably best 
given through a "definition by examples".

The usual presentation of the theory of groups is

<div class=boxed markdown=1>
A set $G$ equipped with function symbols 
- $e : G^0 \to G$
- $(-)^{-1} : G^1 \to G$
- $\cdot : G^2 \to G$

satisfying the equational axioms 

- $(x \cdot y) \cdot z = x \cdot (y \cdot z)$
- $x \cdot e = x = e \cdot x$
- $x \cdot x^{-1} = e = x^{-1} \cdot x$
</div>

Notice that the theory of posets is _not_ algebraic[^1] and indeed 
the usual presentation involves a _relation_ symbol $\leq$ (which is not allowed)
rather than only function symbols. Similarly, the theory of fields is not 
algebraic[^2] and the usual presentation requires an axiom that's _much_ 
more complicated than just an equation: $(x = 0) \lor \exists y . xy = 1$.

However, these presentations by functions and equational axioms should really 
be thought of as _presentations_. There are superficially quite different 
presentations which still present the same theory. For instance, here is 
another presentation of the theory of groups[^3]:

<div class=boxed markdown=1>
A set $G$ equipped with a function symbol 
- $/ : G^2 \to G$

satisfying the equational axiom

- $x / \big ( ((x/x)/y)/z) / ((x/x)/x)/z \big ) = y$
</div>

With this in mind it's natural to want an abstract characterization of 
an algebraic theory, that is _independent_ of the choice of presentation.
In his PhD thesis, Lawvere set this in motion by showing that for any 
algebraic theory $\mathbb{T}$, there's a Classifying Category 
$\mathcal{C}_\mathbb{T}$ so that 

$$
\{ \mathbb{T}\text{-algebras} \} 
\simeq
\{ \text{finite product functors } \mathcal{C}_\mathbb{T} \to \mathsf{Set} \}
$$

If we have a good understanding of $\mathbb{T}$, then we can get our 
hands on $\mathbb{C}_\mathbb{T}$ concretely since it's (opposite) 
the full subcategory of finitely generated free models!

Important for us is the related result that models of $\mathbb{T}$ in 
some other finite product category are given exactly by finite product 
functors from $\mathcal{C}_\mathbb{T}$ into that category!

So, for example, a topological group is the same data is a finite product 
functor $$\mathcal{C}_\mathsf{Grp} \to \mathsf{Top}$$, while a lie group is 
the data of a finite product functor $$\mathcal{C}_\mathsf{Grp} \to \mathsf{Diff}$$.

This is what's going to give us the ability to relate algebras
in $\mathcal{T}$ to topological algebras! Let's see how it works!

---

First, say we have a group object in $\mathcal{T}$. This is the data 
of a finite product preserving functor 
$\mathcal{C}_\mathsf{Grp} \to \mathcal{T}$. But we know from part 1 
that the reflector $r : \mathcal{T} \to \mathsf{Seq}$ preserves finite products 
too! So composing these gives a finite product functor 

$$
\mathcal{C}_\mathsf{Grp} \to \mathcal{T} \to \mathsf{Seq}
$$

which is a group object in $\mathsf{Seq}$. That is, a (sequential) 
topological group[^4]!

Conversely, say we have a sequential topological group. Then the 
embedding $e : \mathsf{Seq} \to \mathcal{T}$ is a right adjoint, 
and in particular preserves finite products. So again we get a 
group object in $\mathcal{T}$! 

In fact, the adjunction $r \dashv e$ gives us an adjunction 
$$r_* \dashv e_*$$ between the functor categories, and since 
$r \circ e \cong \text{id}_\mathsf{Seq}$, this is true at the 
level of functor categories too!

So the category of sequential topological groups is a reflective 
subcategory of the category of groups in $\mathcal{T}$, and the 
reflector is exactly what you expect: Just take the topological 
reflection of the underlying object of $G$!

There's nothing special about groups here, and so we learn that 
for _any_ algebraic theory, the category of sequential models 
is a reflective subcategory of the category of models in $\mathcal{T}$.
Thus, any question we have about (sequential) topological models can 
be answered in $\mathcal{T}$ without losing information, and anything 
we prove about models in $\mathcal{T}$ immediately gives us results about 
topological models by reflecting (though in this direction we possibly 
lose information about the proofs of convergence).

This is all kind of abstract right now, so let's do a very down-to-earth 
example:

In $\mathcal{T}$, a subset of $G$ is any monic $X \hookrightarrow G$
(that is, any continuous injection). In particular, $X$ does _not_ 
need to have the subspace topology!

With this in mind, a subgroup of $G$ is just a continuous injection 
$H \hookrightarrow G$ whose image is a subgroup in the usual sense.
Of course, this pulls back (by injectivity) to a unique 
group structure on $H$ rendering the inclusion a homomorphism.

Now here's a typical (very easy!) theorem/construction:

<div class=boxed markdown=1>
Let $X$ be any subset of $G$, a group. Then there's a smallest subgroup 
$\langle X \rangle \leq G$ containing $X$.
</div>

$\ulcorner$
If $X$ is any subset, we define 

$$\langle X \rangle = \bigcap \{ H \leq G \mid X \subseteq H \}.$$

This is a subgroup containing $X$, and any other subgroup containing $X$ 
is part of the intersection, rendering this the smallest such subgroup.
<span style="float:right">$\lrcorner$</span>

Notice that this proof is _constructive_ in the sense that it doesn't use 
LEM or Choice[^5]. In particular, this proof works in every topos, and 
thus in $\mathcal{T}$.

But what does this exceptionally simple proof tell us about 
topological groups? Well subsets and subgroups are continuous 
injections, so this tells us that[^6] 

<div class=boxed markdown=1>
Let $X \hookrightarrow G$ be any continuous injection into a 
topological group $G$. Then there's a topological group $\langle X \rangle$ 
with a continuous injection $\langle X \rangle \hookrightarrow G$ so that 

1. $X \hookrightarrow G$ factors through $\langle X \rangle$
2. $\langle X \rangle$ is initial with this property
</div>

We can actually build such an $H$ by externalizing the proof of this 
theorem too! Subsets are interpreted as general monics into $G$, and 
the "intersection" of two monics externalizes to their pullback.
So the desired $\langle X \rangle$ is exactly the pullback of the family 
of all continuous injections $H \hookrightarrow G$ factoring the 
inclusion from $X$[^7].

In case $G$ is sequentially hausdorff, this is on-the-nose correct. In 
case $G$ isn't, then $\langle X \rangle$ might live in $\mathsf{Kur}$ 
instead of $\mathsf{Seq}$. But that's ok! We can just hit it with the 
reflector to get an "honest" topological group with the same universal 
property (among the continuous injections whose domain is also "honest").

Now, it's entirely possible that you would have come up with such a theorem 
yourself. After all, a moment's thought shows that $\langle X \rangle$ is 
"just" the usual subgroup generated by $X$, equipped with the finest 
topology rendering $X \hookrightarrow \langle X \rangle$ continuous. 

The utility of the topos theoretic language is in doing more complicated 
constructions, where we're still allowed to manipulate everything as though 
they're sets, and we can be safe in the knowledge that, at the end of the 
day, we can cash out our theorem for one about topological spaces! 
It frees us from the burden of carrying around topologies all the time.

<br>

For a more complicated example, one can show that the category of 
abelian groups in a (grothendieck) topos is always AB5. In particular,
the category of abelian groups in $\mathcal{T}$ is abelian and has 
enough injectives, so we can do homological algebra to it! Contrast this 
with the category of abelian groups in $\mathsf{Top}$, which is famously 
_not_ abelian!

This is one of the big motivations for [Condensed Mathematics][4]. 
Indeed, in $\mathsf{Top}$, the continuous bijection of abelian groups
$(\mathbb{R},\text{discrete}) \to (\mathbb{R},\text{euclidean})$
is not an isomorphism. Yet the kernel and cokernel are both trivial!
In both condensed mathematics and the topological topos, this is 
remedied by a more complicated cokernel. Remember that 
the colimits preserved by the embedding $\mathsf{Seq} \to \mathcal{T}$ 
are only those that look like covers. 

In fact, we can compute the cokernel as the coequalizer of the inclusion 
map and the constant $0$ map. In the topos, this is the sheafififcation 
of the colimit of presheaves, which are computed pointwise. So 
the underlying set of the cokernel is the colimit of the underlying sets 
is $\{ 0 \}$. But the convergent sequences is the colimit of

$$
\{ 
\text{eventually constant sequences} \} 
\rightrightarrows 
\{ \text{convergent sequences} \}
$$

where one map is just the inclusion, and the other sends every eventually constant 
sequence to the constant $0$ sequence.

So the cokernel has a single point $\{ 0 \}$, but there's a proof that 
the constant $0$ sequence converges for every equivalence class of 
convergent sequences differing by an eventually constant sequence!

Keeping track of these proofs (which themselves form an abelian group) 
is exactly what we need to do to algebraically detect that 
$(\mathbb{R}, \text{discrete}) \to (\mathbb{R}, \text{euclidean})$ isn't 
an isomorphism!

As an aside, I don't understand condensed mathematics well enough to 
know how it differs from math in the topological topos. Just looking at 
definitions, I know it's based on test maps from all compact hausdorff spaces 
instead of test maps from only $$\mathbb{N}_\infty$$. This probably 
means it's closely related to compactly generated spaces in much the 
way that $\mathcal{T}$ is related to sequential spaces. 
I'm sure there's a reason to prefer this, but I don't know what it is[^8].
The moral to keep in mind is that the power of doing algebra in a topos 
that handles the topology for you is currently being used to great effect 
in applying homological algebra to analytic situations where it previously 
couldn't go!

---

Alright, I told you this one was going to be more leisurely than the last one!
Now that we've seen some applications of $\mathcal{T}$ to topological 
algebra, and we've seen some basic externalization, let's move on to [part 3][7] 
and _really_ get familiar with the internal logic and how it relates to 
the real world!

---

[1]: https://ncatlab.org/nlab/show/categorical+semantics
[2]: https://ncatlab.org/nlab/show/regular+category
[3]: https://ncatlab.org/nlab/show/predicative+mathematics
[4]: https://en.wikipedia.org/wiki/Condensed_mathematics
[5]: /2024/07/03/life-in-johnstones-topological-topos.html
[6]: https://mathoverflow.net/questions/441610/properties-of-pyknotic-sets
[7]: /2024/07/03/topological-topos-3-bonus-axioms.html


[^1]:
    You can show this with categorical techniques. For instance, 
    the category of models of any algebraic theory is always [regular][2],
    while the category of posets isn't

[^2]:
    The category of models for any algebraic theory always has an initial 
    object, yet the category of fields doesn't!

[^3]:
    See McCune's _Single Axioms for Groups and Abelian Groups with Various 
    Operations_.

    This operaetion is related to the "usual" operations by $x / y = x \cdot y^{-1}$.

[^4]:
    Remember, though, that the product on $\mathsf{Seq}$ is different 
    from the product on $\mathsf{Top}$. This never matters in practice, 
    and the $\mathsf{Seq}$ product agrees with the product in the 
    "convenient category" of compactly generated spaces, but if you want 
    an honest group object in $\mathsf{Top}$, you'll want $G$ to be 
    locally compact.

[^5]:
    It's not [predicative][3], but that's fine for a topos. And regardless, 
    if you know enough to complain about predicativity, you know enough to 
    give a predicative version of this proof :P.

[^6]:
    Indeed, it says something slightly stronger than this! In the case of 
    non (sequentially) hausdorff spaces, there might be extra subsets 
    that are merely kuratowski limit spaces! The theorem says we're actually 
    allowed to take $X$ to be such a subspace as well!

[^7]:
    The diligent reader will note there are a proper class of such arrows,
    so this pullback as written isn't defined. Of course, the domain 
    of any such arrow has at most $|G|$ many elements, and there's only a 
    set worth of topologies we can put on one of these domains. So up to 
    isomorphism there's only a set worth of arrows, and we're good to go!

[^8]:
    Peter Scholze actually says a few words about why condensed sets 
    are easier to work with than objects of $\mathcal{T}$ in a comment 
    to his answer to [this MO question][6]. I still don't _really_ see it,
    but that's probably because I haven't spent a lot of time (or any time)
    working with condensed sets.
