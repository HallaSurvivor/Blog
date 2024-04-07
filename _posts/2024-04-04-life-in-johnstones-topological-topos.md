---
layout: post
title: Life in Johnstone's Topological Topos
tags:
  - 
---

TODO: mention somewhere that if you want a detailed description of 
some pointset topological properties of sequential spaces, you can 
read Dan Ma's excellent [series of blog posts][16]

I've been thinking a lot about the internal logic of topoi again, and in 
order to feel like I understand things I want more examples of topoi 

TODO: finish this introduction. Talk about wanting examples of topoi 
we can use to externalize stuff. We're already pretty comfortable with 
sheaf topoi $\text{Sh}(X)$, but we want to throw some gros topoi into the 
mix. Let's start with Johnstone's topological topos, but eventually I want 
to learn about the effective topos[^1] (and other [realizability topoi][2]),
various [smooth topoi][3], .... any others?

The [topological topos][4] $\mathcal{T}$ is a world where every set is 
_intrinsically_ a space. 

And every function is continuous intrinscially

TODO: say more about that, and the difference between intrisic and structure

This is great for a couple reasons. First, it tells us that anything we 
construct using type theory can be thought of as being, automatically, 
some kind of "space". Understanding this relationship between types and 
topology has been a staple in many people's careers, but I want to single 
out [Martín Escardó][5] as someone whose papers I've been reading lately 
(and who I talk to fairly often on [mastodon][6]).

Second, this tells us that any theorem we're able to prove [constructively][7]
is automatically true "continuously", and gives us a theorem for 
_topological_ structures! Of course, in order to _use_ these theorems, we 
need to understand how objects inside the topological topos $\mathcal{T}$ 
externalize to give honest topological spaces in "the real world".

I wasn't able to find many people talking about this, so I worked out a bunch 
of it for myself, which I'm super excited to share ^_^.

So then, let's get started!

---

TODO: what _is_ the topological topos? Sheaves on $\mathbb{N}_\infty$ 
vs sheaves on $\{ \mathbb{N}_\infty, 1 \}$. These are the same 
because one is a [dense subsite][8] of the other (prove that)

A sheaf on $\{\mathbb{N}_\infty, 1\}$ is nice because we can think of $X(1)$ 
as the _set of points_ and $X(\mathbb{N}_\infty)$ as _proofs that sequences 
converge_. Indeed, $n : 1 \to \mathbb{N}_\infty$ gives a map on sheaves 
$n^* : X(\mathbb{N}_\infty) \to X(1)$ for all $X$. 
If $p \in X(\mathbb{N}_\infty)$, then we think of $n^*(p)$ as being 
$p_n$, the $n$th point in the sequence. We think of $\infty^*(p)$ as 
being the limit the sequence converges to. So $p$ is itself a proof that 
$p_n \to p_\infty$, and there might well be a second proof $q$ so that 
for all $n$, $q_n = p_n$ and $q_\infty = p_\infty$. This is a second proof 
that the same sequence converges.

Of course, every topological space $X$ gives an object 
$\overline{X}$ in the topos where we set $\overline{X}(1) = X$ 
and $\overline{X}(\mathbb{N}_\infty) = \{ f : \mathbb{N}_\infty \to X \}$. 
That is, underlying set of $\overline{X}$ is exactly the underlying set of $X$,
and for every convergent sequence in $X$ we add a unique proof that that 
sequence converges.

TODO: say that for [sequential spaces][9] this is a fully faithful 
embedding. 

More generally, say we have a [kuratowski limit space][10] 
(also called a subsequential space). This is a 

TODO: definition, and mention what the homs are

Every sequential space is automatically a limit space. And the argument from 
before gives a fully faithful embedding of limit spaces into $\mathcal{T}$.

Taken together, we have fully faithful embeddings 

$$
\mathsf{Seq} \hookrightarrow \mathsf{Kur} \hookrightarrow \mathcal{T}
$$

TODO: say something about "processes", a la lawvere?


<br>

TODO: talk about the left adjoints to each of these embeddings. Mention that
they both preserve finite products... While we're at it, mention that the 
inclusions preserve certain colimits (in particular, those involved in 
making CW complexes).

TODO: remember to describe the left adjoints explicitly. The reflector to 
Kur just forgets that there are multiple proofs, and only remembers 
_that_ a sequence converges, rather than _how_. The reflector to Seq 
then builds a topology based on these convergent sequences.

Mention that Kur is a [quasitopos][12]? This gives us some nice results 
for free. Cf.... somewhere in the elephant.

TODO: since products are preserved, these form an [exponential ideal][11],
and the inclusions preserve the cartesian closed structure too!
Note this also tells us that if $Y$ is a sequential space, and $X$ is 
_any_ object of $\mathcal{T}$, then the function space $Y^X$ is already 
a sequential space!

TODO: summarize this with the picture Martin always draws with Seq 
(with $\times,+,\to$) sitting inside Kur (with $\prod, \sum$) sitting 
inside $\mathcal{T}$ (with $\Omega$).

TODO: mention, probably in a footnote, that while MANY spaces are sequential 
(for instance, all first countable spaces, thus all metric spaces, 
CW complexes, etc), this doesn't cover EVERY space you might be interested in.
For instance, the [Stone–Čech Compactification][13] of the natural,
$\beta \mathbb{N}$, is equivalently the space of [ultrafilters][14] on 
$\mathbb{N}$. This space is extremely important in various subfields of 
logic and combinatorics. See, for instance, 
Hindman and Strauss's 
_Algebra in the Stone-Čech Compactification: Theory and Applications_. 
In particular, the applications to [Ramsey Theory][15].

If you can, maybe compute the sequential reflection of $\beta \mathbb{N}$?

TODO: if you want to read more about how to actually compute (co)limits 
and exponentials in $\mathsf{Seq}$ and $\mathsf{Kur}$, I highly recommend 
Menni and Simpson's 
_Topological and limit-space subcategories of countably-based equilogical spaces_

TODO: add a link to that, and summarize some important stuff in a footnote.
See pdf pg 10

---

So now we see how to get an honest topological space from an object in 
$\mathcal{T}$! 

Reflecting $X$ into $\mathsf{Kur}$ takes the underlying set $X(1)$ and 
just remembers which sequences converge. Then reflecting _this_ into 
$\text{Seq}$ builds an honest to goodness topological space by saying 
$U \subseteq X(1)$ is open iff .... 

TODO: something!

TODO: also maybe mention that under a mild separation condition 
(sequential hausdorffness?) $\mathsf{Seq} \simeq \mathsf{Kur}$?

TODO: put a few computations here. Define some simple types and figure out what 
the topology on them should be. 

For instance, $\prod_{n : \mathbb{N}} 2$. 
This is equivalent to $\mathbb{N} \to 2$, where everything in sight 
already lives in the CCC $\mathsf{Seq}$. So this space 

Maybe the type of decreasing binary sequences?

---

What do locales look like in $\mathcal{T}$?

Well, for any $T_1$ locale (footnote with the definition), then... 
something something this is homming into the version of that locale 
externally. See, for instance, the first section of 
Moerdijk and Reyes 
_Smooth spaces versus continuous spaces in models for synthetic differential geometry_

TODO: It's worth figuring out exactly what this means. 
We need to compare it to a locale object internal to $\mathcal{T}$...

---

What do algebras look like in $\mathcal{T}$?

First of all, for any (essentially) algebraic theory $\mathbb{T}$, 
if we have a (sequential!) topological model (for example, a topological 
group whose underlying topology is sequential), that model is still a 
model in $\mathcal{T}$.

Indeed, the [funtorial semantics][17] perspective says that 
a topological $\mathbb{T}$-model $M$ corresponds to a finite product
functor[^2] from some classifying category $\mathcal{C}_\mathbb{T}$ to 
$\mathsf{Seq}$. Since the inclusion functor 
$\mathsf{Seq} \hookrightarrow \mathcal{T}$ is a right adjoint, it preserves 
products, and thus $M$ is still a $\mathbb{T}$-model when viewed as an 
object in $\mathcal{T}$! 

TODO: so if we constructively prove a theorem about groups, say, then 
that theorem is true inside $\mathcal{T}$. Thus, since (sequential) 
topological groups all live inside $\mathcal{T}$, we get a theorem about 
all topological groups!

And this works for basically _any_ kind of algebraic gadgets you want 
to consider!

<br>

Conversely, say we _have_ a $\mathbb{T}$-model in $\mathcal{T}$. 
That is, say we have a finite product functor 
$\mathcal{C}_\mathbb{T} \to \mathcal{T}$.
Then since the reflector $\mathcal{T} \to \mathsf{Seq}$ preserves 
finite products, the honest topological space associated to our 
object is itself a $\mathbb{T}$-model!

This tells us that if we ever want to reason about an algebraic 
object in $\mathcal{T}$, we can fruitfully pretend it's "just" a 
topological model! After all, its underlying topological space is 
still a model, and the only difference between an object in $\mathcal{T}$ 
and its underlying space is the potential for multiple proofs of convergence!

TODO: phrase that better, and tie it into your earlier discussion about 
what objects in $\mathcal{T}$ look like... In fact, maybe say something like 
this earlier in the post.

---

Speaking of proving theorems in $\mathcal{T}$, we actually don't have to 
be _totally_ constructive! The topological topos satisfies certain nice 
~bonus axioms~ that make it a particularly nice place to work.

For instance, $\mathcal{T}$ models [Dependent Choice][20][^3]

TODO: say some words about what this means, for instance, the 
dedekind and cauchy reals agree, and many of the pathologies 
from constructive math go away!

Moreover, $\mathcal{T}$ models Brouwer's Continuity Principle that 
"Every function $f : \mathbb{R} \to \mathbb{R}$ is continuous".

TODO: find a proof. Maybe ML&M?

TODO: mention that this makes $\mathcal{T}$ a rather stronger version of 
[Solovay's Model][22] which models 
$$\mathsf{LEM}+\mathsf{DC}$+"every function $\mathbb{R} \to \mathbb{R}$ is measurable".

In order to get all functions to be _continuous_, we have to drop LEM.

---

TODO: don't forget to say something about universes

TODO: say something about $\Omega$

TODO: figure out how function spaces in $\mathcal{T}$ (really in $\mathsf{Seq}$)
relate to function spaces in $\mathsf{Top}$ (when they exist)

---

[1]: https://arxiv.org/abs/2404.01256
[2]: https://ncatlab.org/nlab/show/realizability+topos
[3]: https://ncatlab.org/nlab/show/Models+for+Smooth+Infinitesimal+Analysis
[4]: https://ncatlab.org/nlab/show/Johnstone%27s+topological+topos
[5]: https://www.cs.bham.ac.uk/~mhe/
[6]: https://mathstodon.xyz/@MartinEscardo
[7]: https://ncatlab.org/nlab/show/constructive+mathematics
[8]: https://ncatlab.org/nlab/show/dense+sub-site
[9]: https://en.wikipedia.org/wiki/Sequential_space
[10]: https://ncatlab.org/nlab/show/subsequential+space
[11]: https://ncatlab.org/nlab/show/exponential+ideal
[12]: https://ncatlab.org/nlab/show/quasitopos
[13]: https://en.wikipedia.org/wiki/Stone%E2%80%93%C4%8Cech_compactification
[14]: https://en.wikipedia.org/wiki/Ultrafilter_on_a_set
[15]: https://en.wikipedia.org/wiki/Ramsey_theory
[16]: https://dantopology.wordpress.com/2010/06/21/sequential-spaces-i/
[17]: https://ncatlab.org/nlab/show/Lawvere+theory
[18]: https://en.wikipedia.org/wiki/Regular_cardinal
[19]: https://ncatlab.org/nlab/show/essentially+algebraic+theory
[20]: https://en.wikipedia.org/wiki/Axiom_of_dependent_choice
[21]: https://ncatlab.org/nlab/files/DCTopTopos.pdf
[22]: https://en.wikipedia.org/wiki/Solovay_model

[^1]:
    I spent some time a few years ago (Feb of 2022, according to my Zotero)
    thinking hard about the effective topos. I think I was going 
    to write a blog post about it, but I never got around to it.

    I think I should be able to remind myself what was going on, and 
    in a perfect world I would understand it much better now that I know 
    more things, so hopefully I'll finally write that post. This is 
    particularly relevant now that Andrej Bauer and James Hanson have posted 
    their [preprint][1] constructing a realizability topos where the 
    reals are countable.

[^2]:
    Of course, if you need operations of infinite arity, we can play this game 
    with functors that preserve limits of size $\lt \lambda$ for any 
    [regular cardinal][18] $\lambda$.

    Similarly, if you want partial operations, that's totally ok! 
    [Essentially algebraic][19] theories are modelled by finite 
    limit functors (or, again, by $\lt \lambda$-continuous functors),
    and since right adjoints preserve all limits, again any model in 
    $\mathsf{Seq}$ is still a model when considered as an object in 
    $\mathcal{T}$.

[^3]:
    You can find a proof in Shulman and Simpson's note 
    [_Dependent Choice in Johnstone's Topological Topos_][21]
