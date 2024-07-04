---
layout: post
title: Topological Topos 3 -- Bonus Axioms
tags:
  - life-in-the-topological-topos
---

In the first post of the series, we talked about what the topological 
topos is, and how we can think about its objects (and, importantly, 
how we can relate computations in the topos $\mathcal{T}$ to 
computations with topological spaces in "the real world"). In part two, 
we talked about algebraic structures, and how (for example) 
groups in $\mathcal{T}$ are related to topological groups!

In that post we alluded to the presence of ~bonus axioms~ that allow us 
to reason in $\mathcal{T}$ more freely than in many other topoi. For instance, 
we have access to a certain amount of choice. We also have access to a 
powerful principle saying that every function between metric spaces is 
$\delta$-$\epsilon$ continuous!

In this post we'll spend some time talking about these bonus axioms, and 
proving that they're true (since a lot of these facts are basically folklore).

Let's get to it!

---

First, let's take a second to recall the definition of the grothendieck 
topology $J$ for $\mathcal{T}$. We're going to be externalizing a lot 
of theorems, and it'll be good to have the open cover condition on hand.
Here's what we wrote back in [the first post][64], but you can of course 
read more in Section 3 of Johnstone's original paper.

> For the site with two objects, $$\{1, \mathbb{N}_\infty\}$$, 
> every (nonempty) family of arrows $$\{X_\alpha \to 1 \}$$ is covering. 
> So the interesting question is what a covering family of $$\mathbb{N}_\infty$$ 
> looks like.
> 
> If $S$ is an infinite subset of $\mathbb{N}$, we write $f_S$ for the unique 
> monotone map $$\mathbb{N}_\infty \to \mathbb{N}_\infty$$ whose image is 
> $$S \cup \{ \infty \}$$.
> 
> <div class=boxed markdown=1>
> A family $$\{X_\alpha \to \mathbb{N}_\infty\}$$ is covering if and only if 
> both
> 
> 1. It contains every constant map $$1 \to \mathbb{N}_\infty$$
> 2. For every infinite $T \subseteq \mathbb{N}$, there is a further 
> infinite subset $S \subseteq T$ with 
> $$f_S : \mathbb{N}_\infty \to \mathbb{N}_\infty$$ in the family
> 
> In particular, if a family contains every constant map 
> $$1 \to \mathbb{N}_\infty$$ and a "tail of an infinite sequence" 
> $$f_{\{x \geq N\}}$$ for some $N$, then that family is covering.
> </div>
> 
> So, roughly, to prove that something "merely exists" in $\mathcal{T}$, we 
> have to provide a witness for every finite $n$, and these witnesses should 
> converge to the witness for $\infty$.
> 
> <br><br>
> 
> If we want to use the site with one object $$\{ \mathbb{N}_\infty \}$$, 
> the condition is almost exactly the same. A family of maps is covering 
> if and only if both
> 
> 1. every constant map $$\mathbb{N}_\infty \to \mathbb{N}_\infty$$ is in the family
> 2. For each infinite $T \subseteq \mathbb{N}$, there's a further infinite 
> $S \subseteq T$ so that $f_S$ is in the family.
> 
> This, unsurprisingly, doesn't make too much difference.

---

## Dependent Choice

To start, $\mathcal{T}$ models [Dependent Choice][20][^3]. 

Say you have a relation $R \subseteq X \times X$ which is 
<span class=defn>total</span> in the sense that 
$\forall x . \exists y . R(x,y)$.

Then DC says for each $x_0 : X$, there's a function 
$f : \mathbb{N} \to X$ so that $f(0) = x_0$ and for each $n$,
$R(f(n), f(n+1))$.

This is intuitively obvious. After all, we start with $x_0$, then 
by totality the set $$\{ y \mid R(x_0,y) \}$$ is inhabited. So we 
can choose an element $x_1$ from this set. Similarly we can choose 
an $x_2$ from $$\{y \mid R(x_1,y) \}$$, and so on. Notice that the 
_choices_ we make are allowed to _depend_ on the choices that came before. 
After all, it's possible that for two different choices 
$$x_1,x_1' \in \{ y \mid R(x_0,y) \}$$ the sets $$\{ y \mid R(x_1,y) \}$$ and 
$$\{ y \mid R(x_1',y) \}$$ might be different, leading to different 
allowable choices of $x_2$!

Thus, DC basically tells us that recursive definitions work, even if we 
don't have a canonical way to choose one of many options at each 
recursive stage. Indeed, most recursive definitions work by first choosing 
an $x_0$, and then arguing that the set of "allowable" next steps is 
always inhabited[^16]. For more information about DC and how to think 
about it, I recommend Karagila's excellent [paper][57] on the subject.

<div class=boxed markdown=1>
For those who like type theory, 
DC says that for every binary relation $R$ on a type $X$,

$$
\displaystyle
\mathtt{dc} : 
\left ( 
    \prod_{x:X} \left \lVert \sum_{y:X} R(x,y) \right \rVert
\right )
\to
\prod_{x_0 : X}
\left \lVert 
\sum_{f : \mathbb{N} \to X} (f(0) = x_0) \times \left ( \prod_{n:\mathbb{N}} R(f(n), f(n+1)) \right )
\right \rVert
$$

or, cashing out these $$\lVert \Sigma \rVert$$s for $$\exists$$s, 

$$
\left ( \forall (x:X) . \exists (y:X) . R(x,y) \right ) 
\to 
\forall (x_0 : X) . \exists (f : \mathbb{N} \to X) . f(0) = x_0 \land \forall n . R(f(n), f(n+1))
$$
</div>

Here's an idiomatic example of dependent choice in action: The 
[Baire Category Theorem][45] for complete metric spaces.

<div class=boxed markdown=1>
Let $(X,d)$ be a (cauchy) complete metric space[^14] with inhabited 
(strongly[^15]) dense open sets $U_1, U_2, U_3, \ldots$.

Then the countable intersection $\bigcap_n U_n$ is still (strongly) dense.
</div>

The usual proof (say, from Karagila's notes) doesn't use LEM, 
so it goes through unchanged. 
We'll present it here paying special attention to the 
use of DC.

$\ulcorner$
Let $V$ be open in $X$. We need to show that $V \cap \bigcap_n U_n$ is 
inhabited. 

Since $U_1$ is strongly dense, we know that $V \cap U_1$ is inhabited, 
say by $x_1$. Now since $U_1 \cap V$ is open, we can find a radius 
$r_1$ so that 

1. $0 \lt r_1 \lt 2^{-1}$
2. the (strongly closed) ball 
$$\overline{B(x_1,r_1)} = \{ y \mid d(x_1,y) \leq r_1 \}$$ is contained in $V \cap U_1$

By dependent choice (and strong density of each $U_k$), 
we may recursively build a sequence of pairs $(x_n,r_n)$ so that 

1. $0 \lt r_{n+1} \lt 2^{-(n+1)}$
2. the (strongly closed) ball $\overline{B(x_{n+1},r_{n+1})}$ 
is contained in $B(x_n,r_n) \cap U_{n+1}$.

By construction, then, the $x_n$s assemble into a cauchy sequence whose 
limit $x_\infty$ lies in each $B(x_n,r_n)$. Therefore 
$x_\infty \in \bigcap_n B(x_n,r_n) \subseteq V \cap \bigcap_n U_n$, 
so that $\bigcap_n U_n$ is dense, as desired.
<span style="float:right">$\lrcorner$</span>

<div class=boxed markdown=1>
Can you build a relation $R$ on 
$(X \times \mathbb{R}_{\gt 0} \times \mathbb{N})$ so that 
$R \big ( (x,r,n), \ (y,s,m) \big )$ holds exactly when 
$m=n+1$ and $(y,s)$ satisfy the above conditions compared to $(x,r)$?

This will let you see _precisely_ how dependent choice is used above.
</div>

Dependent Choice implies [Countable Choice][41], which itself implies 
[Weak Countable Choice][42]. But WCC implies that the 
[dedekind reals][43] and the [cauchy reals][44] agree. And indeed one 
can show directly that in $\mathcal{T}$ both the dedekind and cauchy reals 
are given by $よ\mathbb{R}$.

<br>

## Brouwer's Principle

The next ~bonus axiom~ we'll talk about is 
Brouwer's Continuity Principle that 
"Every function $f : \mathbb{R} \to \mathbb{R}$ is continuous"!

Precisely[^11]:

<div class=boxed markdown=1>
$$
\mathcal{T} \vDash
\forall f : \mathbb{R}^\mathbb{R} . \ 
\forall \epsilon : \mathbb{R}_{\gt 0} . \ 
\forall a : \mathbb{R} . \ 
\exists \delta : \mathbb{R}_{\gt 0} . \ 
\forall b : \mathbb{R} . \ 
d(a,b) \lt \delta \to d(fa,fb) \lt \epsilon
$$
</div>

In fact, this is true for any (external) metric spaces $X$ and $Y$ 
where $X$ is (externally) locally compact! In particular, it's also 
true that every function $\mathbb{N}^\mathbb{N} \to \mathbb{N}$ is 
$\epsilon$-$\delta$ continuous. 

Note that it's crucial here that we use the truncated $\exists$ 
rather than the untruncated $\Sigma$ in the statement of this theorem.
Martín Escardó and Chuangjie Xu have [shown][59] that the untruncated 
version of this theorem isn't just false in $\mathcal{T}$, it's 
_provably false_ in every topos!

Regardless, it's shockingly hard to find this continuity principle 
written down anywhere, but it's 
cited in lots of places! It's definitely part of the folklore, 
and I'm happy to share a full proof! It's a bit long, though, so I'm leaving 
it as an "appendix" at 
the bottom of this post. If you know of a reference, or of a 
slicker proof than the one I found, I would REALLY love to hear 
about it[^13]!

Regardless, the truth of Brouwer's principle tells us that 
$\mathcal{T}$ is a rather stronger version of [Solovay's Model][22]. 
Solovay's model validates
$$\mathsf{LEM}+\mathsf{DC}+$$"every function $\mathbb{R} \to \mathbb{R}$ is measurable".

In $\mathcal{T}$, we have $\mathsf{DC}$ and the stronger 
"every function $\mathbb{R} \to \mathbb{R}$ is continuous". But the price 
we pay is LEM.

<br>
## Omniscience Principles

We can ask about other nonconstructive principles too. For instance, 
Bishop's [Principles of Omniscience][49]!

First, let's look at the Limited Principle of Omniscience (LPO):

<div class=boxed markdown=1>
The <span class=defn>Limited Principle of Omniscience</span>:
says that every sequence of bits is either $0^\omega$ or 
contains a $1$. That is:

$$\forall s : 2^\mathbb{N} . (\forall n . s(n) = 0) \lor (\exists n . s(n) = 1)$$

In the presence of countable choice (which we have in $\mathcal{T}$), 
this is equivalent to the _analytic_ LPO, which says:

$$\forall x : \mathbb{R} . (x \lt 0) \lor (x = 0) \lor (x \gt 0)$$

and is further equivalent to the type-theoretic condition that 
the obvious embedding

$$\mathbb{N} + \{ \infty \} \hookrightarrow \mathbb{N}_\infty$$

is an isomorphism.
</div>

It's clear from the last condition that LPO is false in $\mathcal{T}$. 
Since both $$\mathbb{N} + \{ \infty \}$$ and $$\mathbb{N}_\infty$$ are 
sequential, these internal types correspond to the expected spaces externally,
where this is obviously not an isomorphism. After all, one space is 
discrete and the other isn't.

That said, it can be hard to find example computations of people 
statements internal to a topos to statements in the real world, 
so just for fun let's prove this again in a more complicated way:

$\ulcorner$
If it were true, then we would know $1 \Vdash \text{LPO}$. Now 
cashing out the universal quantifier, we would know that 
for every $$s \in 2^\mathbb{N}(\mathbb{N}_\infty)$$

$$\mathbb{N}_\infty \Vdash (\forall n . s_k(n) = 0_k) \lor (\exists n . s_k(n) = 1_k)$$

Here $$s_k : \mathbb{N}_\infty \to 2^\mathbb{N}$$ is allowed to be any 
convergent sequence in cantor space, and we interpret $0_k$ and $1_k$ as 
constant sequences.

Let's take $s_k$ to be the sequence $0^k 1^\omega$.
That is, the $k$th element of this sequence, $s_k$, should be the point in 
cantor space with $k$ many $0$s followed by an infinite tail of $1$s.
Note this sequence converges to $0^\omega$.

Now what would it mean to have $(\forall n . s(n) = 0) \lor (\exists n . s(n) = 1)$?
We would have an open cover of $$\mathbb{N}_\infty$$ where each element of 
that cover thinks that one of these disjuncts is true. But every covering 
seive of $$\mathbb{N}_\infty$$ contains a function $f_U$ for $U$ an infinite 
subset of $\mathbb{N}$.

Now restricting $s$ to this member of the cover amounts to restricting $s$ 
to a subsequence, $s_{r_k}$.

Is it possible that $$\mathbb{N}_\infty \Vdash \forall n . s_{r_k}(n) = 0_{r_k}$$?
This says for every convergent sequence 
$$n_k \in \mathbb{N}(\mathbb{N}_\infty)$$, we must have $$s_{r_k}(n_k) = 0_{r_k}$$
for all $k$. Of course, it's easy to find a convergent sequence where this 
is false! We can just choose $$n_1 \gt r_1$$ to make $$s_{r_1}(n_1) = 1 \neq 0$$.

Is it possible for $$\mathbb{N}_\infty \Vdash \exists n . s_{r_k}(n) = 1_{r_k}$$?
This says we can pass to a further subsequence $$s_{\ell_{r_k}}$$ so that 
for some convergent sequence $$n_k \in \mathbb{N}(\mathbb{N}_\infty)$$ we 
have $$s_{\ell_{r_k}}(n_k) = 1_k$$ for all $k$. But of course this is false too!
Every convergent sequence of naturals is eventually constant, say $n_k = N$ 
for $k \gg 1$. Then for $k$ large enough, we'll have both $n_k = N$ and 
$$\ell_{r_k} \gt N$$, in which case $$s_{\ell_{r_k}}(n_k) = 0 \neq 1$$.

So we see that LPO externalizes to a false claim, and thus is not validated 
by $\mathcal{T}$.
<span style="float:right">$\lrcorner$</span>

<div class=boxed markdown=1>
As an easy exercise, can you use LPO to build a function 
$\mathbb{R} \to \mathbb{R}$ which is _not_ $\epsilon$-$\delta$ 
continuous? This provides _another_ proof that $\mathcal{T} \not \models \text{LPO}$,
since it contradicts Brouwer's principle. 

In fact, we don't even need Bouwer's principle to contradict! By yoneda, 
$\text{Hom}(\mathbb{R}, \mathbb{R})$ is the set of continuous functions 
on $\mathbb{R}$, but if you build a function in $\mathcal{T}$ you know what 
that function does externally on points! In particular, you can contradict 
with continuity "in the real world".
</div>

<br>

Next, let's look at the _Lesser_ Limited Principle of Omniscience (LLPO):

<div class=boxed markdown=1>
The <span class=defn>Lesser Limited Principle of Omniscience</span> 
says that 

$$
\forall s : 2^\mathbb{N} . \exists ! n . s(n) = 1 . 
(\forall k . s(2k) = 0) \lor (\forall k . s(2k+1) = 0)
$$

This is equivalent to a kind of de Morgan's law

$$
\forall s, t : 2^\mathbb{N} . 
\lnot (\exists n . s(n) = 1 \land \exists m . t(m) = 1) \to 
(\forall n . s(n) = 0 \lor \forall m . t(m) = 0)
$$

and, as before, under countable choice this is equivalent to the _analytic_ LLPO,

$$
\forall x : \mathbb{R}. (x \geq 0) \lor (x \leq 0)
$$
</div>

This turns out to be true[^17]! Just to show more ways to reason about the 
internal logic of topoi, we'll prove this one by working with the category 
$\mathcal{T}$ directly. Since type theoretic functions externalize to 
arrows in $\mathcal{T}$, though, we'll use type theory to label our arrows. 

$\ulcorner$
Proposition 6.2 in Johnstone's original paper implies that $\mathbb{R}$ 
is the pushout of the closed cover 

<p style="text-align:center;">
<img src="/assets/images/life-in-johnstones-topological-topos/closed-pushout.png" width="25%">
</p>

Now showing $\forall x : \mathbb{R} . (x \geq 0) \lor (x \leq 0)$ amounts 
to building a section of the projection 
$\pi : \sum_{x : \mathbb{R}} \lVert (x \geq 0) + (x \leq 0) \rVert$.
Here I've also cashed out the $\lor$ for a [propositional truncation][53]
of a coproduct.

But by the universal property of the pushout, we get a map 
$s : \mathbb{R} \to \sum_{x : \mathbb{R}} \lVert (x \geq 0) + (x \leq 0) \rVert$
as below. Note the truncation $$\lVert (x \geq 0) + (x \leq 0) \rVert$$ 
is _crucial_ for making the middle square commute!

<p style="text-align:center;">
<img src="/assets/images/life-in-johnstones-topological-topos/llpo-universal-property.png" width="100%">
</p>

Moreover, since both $\pi s$ and $\text{id}_\mathbb{R}$ make the outer 
square commute, they must be equal by uniqueness in the universal property. 
So $s$ is the desired section of $\pi$, and $\mathcal{T}$ models LLPO.
<span style="float:right">$\lrcorner$</span>

<div class=boxed markdown=1>
As a nice exercise, check that internal to $\mathcal{T}$ the type 
$\mathbb{R}$ is equivalent to the quotient type[^19]

$$
\mathbb{R}_{\geq 0} + \mathbb{R}_{\leq 0} \big / \mathtt{inl}(0) \sim \mathtt{inr}(0)
$$

and use this fact to give a purely type theoretic proof of that LLPO 
holds in $\mathcal{T}$.

<br>

As another nice (but quite tricky!) exercise, try externalizing 
the statement of LLPO and proving it "directly" by seeing that it 
externalizes to something true!
</div>

<br><br>

Next on this list is Markov's Principle (MP):

<div class=boxed markdown=1>
<span class=defn>Markov's Principle</span> says that 

$$
\forall s : 2^\mathbb{N} . 
(\lnot \forall n . s(n) = 0) \to (\exists n . s(n) = 1)
$$

Again this is equivalent (under CC) to an _analytic_ version[^20]

$$
\forall x : \mathbb{R}. \lnot (x=0) \to x \# 0 
$$

Here $$\#$$ means that $x$ is [apart][55] from $0$. That is, 
$\exists q : \mathbb{Q} . (x \lt q \lt 0) \lor (0 \lt q \lt x)$.
</div>

MP is true in $\mathcal{T}$, and this is not so hard to show. 
We'll write this proof in a slightly more conversational style, but we 
encourage the reader interested in learning topos theory to check all 
the details with the forcing language.

$\ulcorner$
We want to show 

$$
1 \Vdash 
\forall s : 2^\mathbb{N} . 
(\lnot \forall n . s(n) = 0) \to (\exists n . s(n) = 1)
$$

so we fix a convergent sequence $$s_k : \mathbb{N}_\infty \to 2^\mathbb{N}$$.
We want to show that if, for all 
$$f : \mathbb{N}_\infty \to \mathbb{N}_\infty$$

$$
\mathbb{N}_\infty \not \Vdash \forall n . s_{fk}(n) = 0 \quad \quad (\star)
$$

then we must have 

$$
\mathbb{N}_\infty \Vdash \exists n . s_k(n) = 1.
$$

To show this existential claim, we need to provide a conergent sequence 
$n_k$ so that each $s_k(n_k) = 1$. But taking $f$ to be a constant function 
in $(\star)$, we learn that such an $n_k$ exists for each $k$. Moreover, 
since $$s_k \to s_\infty$$, there is a $k \gg 1$ so that $s_k$ and 
$s_\infty$ agree on the first $n_\infty + 1$ many bits, so that we may take 
$n_k = n_\infty$ when $k$ is large enough. Thus the sequence converges, 
as desired.
<span style="float:right">$\lrcorner$</span>

<br><br>

Now WLPO is easy:

<div class=boxed markdown=1>
The <span class=defn>Weak Limited Principle of Omniscience</span> says that 

$$
\forall s : 2^\mathbb{N}. (\forall n . s(n) = 0) \lor (\lnot \forall n . s(n) = 0)
$$

This is equivalent to a kind of excluded middle, and as expected there's an 
analytic version (equivalent in the presence of CC):

$$
\forall x : \mathbb{R} . (x = 0) \lor \lnot (x=0)
$$
</div>

Now, it's easy to see that MP + WLPO $\implies$ LPO 
(look at the analytic versions). So we learn indirectly that 
$\mathcal{T}$ cannot satisfy WLPO. Of course, here's a more direct proof 
that the analytic version can't work:

$\ulcorner$
Consider the sequence $x_n = \frac{1}{n}$, converging to $0$, as an 
element of $$\mathbb{R}(\mathbb{N}_\infty)$$.

If $\mathcal{T}$ were to model WLPO, it would mean (among other things) 
that some subsequence of $x_n$ would be either everywhere $0$ or everywhere 
nonzero. But no subsequence has this property, since $x_n$ is nonzero 
for each finite $n$, but zero at $n=\infty$.

So $\mathcal{T}$ does not model WLPO.
<span style="float:right">$\lrcorner$</span>

<br><br>

As an aside, in all of these statements we're using the "truncated" 
$\lor$ and $\exists$, and it's natural to ask what happens if we change 
these to their "untruncated" versions $+$ and $\Sigma$. 

It's a theorem of Martín Escardó that 

- truncated and untruncated LPO are equivalent
- truncated and untruncated WLPO are equivalent, and are equivalent to untruncated LLPO 
- truncated LLPO is weaker than untruncated LLPO 

In fact, in his [agda files][58], Martín wonders if there's a place in the 
literature where untruncated LLPO and WLPO are shown to be inequivalent. 

He mentions that $\mathcal{T}$ should be an example, and here 
we've shown that in fact it is! After all, $\mathcal{T} \models \text{LLPO}$
but $\mathcal{T} \lnot \models \text{WLPO}$!


---

## Bar and Fan Theorems

The Bar and Fan theorems are closely related to the nice properties of 
baire space and cantor space (respectively) as _spaces_ rather than as 
locales. The locales are always well behaved, but in some topoi these 
locales fail to have enough points, so that the baire space and cantor space 
as sets of points may be lacking.

Since we showed in Part 1 that spatial sequential $T_1$ locales always have 
enough points in $\mathcal{T}$, we see that baire space and cantor space 
both have enough points! By Propositions 3.12 and 3.13 in van den Berg and 
Moerdijk's 
[_Derived rules for predicative set theory: An application of sheaves_][63] 
we see that the Monotone Bar Theorem and the Full Fan Theorem hold in 
$\mathcal{T}$.

This is also the _best we can do_. Since the Full Bar Theorem is known to 
imply LPO, and $\mathcal{T} \not \models \mathsf{LPO}$ we know that 
we can't improve the monotone bar theorem to the full bar theorem in $\mathcal{T}$.

<div class=boxed markdown=1>
As a not-so-hard exercise, verify the _decidable_ fan theorem by hand!
That is, prove 

$$
\mathcal{T} \models 
\forall (B : 2^{\lt \mathbb{N}} \to 2) . 
\ulcorner B \text{ is a monotone bar} \urcorner 
\to 
\ulcorner B \text{ is uniform} \urcorner
$$

Or, entirely in symbols, prove

$$ 
\mathcal{T} \models 
\forall (B : 2^{\lt \mathbb{N}} \to 2) . 
\left ( 
    \begin{array}{c}
        \underbrace
        {
            \forall s : 2^{\lt \mathbb{N}} . s \in B \to (s0 \in B \land s1 \in B)
        }_{\text{$B$ is monotone}} \\
        \land \quad
        \underbrace
        {
            \forall \alpha : 2^\mathbb{N} . \exists n : \mathbb{N} . 
            \alpha \! \upharpoonright_n \in B
        }_{\text{$B$ is a bar}}
    \end{array}
\right )
\to
\Big (
    \underbrace
    {
        \exists N : \mathbb{N} . \forall \alpha : 2^\mathbb{N} . 
        \alpha \! \upharpoonright_N \in B
    }_{\text{$B$ is a uniform bar}}
\Big )
$$

Note that $B : 2^{\lt \mathbb{N}} \to 2$ is a _decidable_ subset of 
$2^{\lt \mathbb{N}}$. To prove the _full_ bar theorem you would want to 
prove the same theorem for all subsets of $2^{\lt \mathbb{N}}$. That is, 
for $B : 2^{\lt \mathbb{N}} \to \Omega$.

As a ~bonus exercise~, use what you know about 
discrete topological spaces and subobjects in $\mathcal{T}$ to argue that a 
semantic proof of this theorem is easily modified to give a proof of 
the full bar theorem.
</div>

<details>
<summary>discussion of the ~bonus exercise~</summary>

The idea here is that a general subobject of a sequential space X is a 
subset of the points of X equipped with some topology making the inclusion 
continuous.

A decidable subobject is a clopen subset of the points of $X$ equipped with the 
induced topology (do you see why?).

Of course, since $2^{\lt \mathbb{N}}$ is discrete, it's not hard to see that
_every_ subobject is decidable! This means in proving the theorem for 
decidable subobjects you've actually proven the theorem for _all_ subobjects!
</details>

---

## De Morgan and LEM

Obviously LEM fails, since $\Omega \not \cong 1+1$. But what about 
De Morgan's Laws?

It turns out that $\mathcal{T}$ is not de Morgan. In another paper 
(the aptly named _Conditions Related to de Morgan's Law_) Johnstone gives a 
slew of conditions equivalent to a topos being de Morgan. In particular, 
de Morgan-ness is equivalent to 

1. $[\top,\bot] : 1+1 \to \Omega_{\lnot \lnot}$ being an isomorphism
2. $1+1$ being [injective][62]

But we can show both of these are false 
(thus giving two proofs that $\mathcal{T}$ is not de Morgan).

For $1$, we can compute that $$\mathcal{T}_{\lnot \lnot}$$ is equivalent to 
$\mathsf{Set}$, where the equivalence sends a set $X$ the space $X$ equipped 
with the indiscrete topology. This is stated at the end of Section 3 of 
Johnstone's original paper. In particular, $1+1$, which has the discrete 
topology, is _not_ isomorphic to $$\Omega_{\lnot \lnot}$$ (which is indiscrete).

For $2$, we know that in $\mathsf{Seq}$ there's a map 
$(0,1) + (2,3) \to 1+1$ which doesn't extend to a map $(0,3) \to 1+1$. 
Since monos in $\mathsf{Seq}$ are still monos in $\mathcal{T}$ 
(since the inclusion is a right adjoint), we're done. 

---
---

## Appendix: A Proof that Johnstone's Topos Models Brouwer's Continuity Principle

If you're not super familiar with externalizing formulas, you 
might want to read my [old blog post][39] with a bunch of simpler 
examples before trying to tackle this one!

We'll be doing this computation using the site with one object $$\mathbb{N}_\infty$$.

<div class=boxed markdown=1>
We'll prove a kind of "theorem schema". Every metric space is sequential, 
so for any metric spaces $X$ and $Y$ in "the real world" we can think of 
$X$ and $Y$ as objects of $\mathcal{T}$. Now if $X$ is moreover locally 
compact, we'll prove that $\mathcal{T}$ models

$$
\ulcorner
\text{every function $X \to Y$ is $\epsilon$-$\delta$ continuous}
\urcorner
$$

Precisely:

$$
\mathcal{T} \vDash
\forall f : Y^X . \ 
\forall \epsilon : \mathbb{R}_{\gt 0} . \ 
\forall a : X . \ 
\exists \delta : \mathbb{R}_{\gt 0} . \ 
\forall b : X . \ 
d(a,b) \lt \delta \to d(fa,fb) \lt \epsilon
$$
</div>

$\ulcorner$
We want to show that 

$$
\mathbb{N}_\infty \Vdash 
\ulcorner
\text{every function $X \to Y$ is $\epsilon$-$\delta$ continuous}
\urcorner
$$

Cashing out the universal quantifiers, we want to show that 
for any continuous functions 
$$f : \mathbb{N}_\infty \times X \to Y$$, 
$$\epsilon : \mathbb{N}_\infty \to \mathbb{R}_{\gt 0}$$, 
and 
$$a : \mathbb{N}_\infty \to X$$ in "the real world" we have 

$$
\mathbb{N}_\infty \Vdash
\exists \delta : \mathbb{R}_{\gt 0} . \ 
\forall b : X . \ 
d(a,b) \lt \delta \to d(fa,fb) \lt \epsilon
$$

To witness the existential quantifier, we need to find a cover 
of $$\mathbb{N}_\infty$$, and produce a real-world $\delta$ defined on 
each member of the cover.

Finding a cover basically amounts to finding a cofinite subset of 
$\mathbb{N}$, and passing to a tail of all the sequences in sight.
With this in mind, we choose a compact neighborhood $K$ of $a_\infty$ 
(using local compactness of $X$), and choose $$\delta^*$$ so that 
$$B(a_\infty, \delta^*)$$ is contained in $K$ and for every 
$x \in B(a_\infty, \delta^*)$ we have 
$d(f_\infty a_\infty, f_\infty x) \lt \frac{\epsilon_\infty}{6}$
(using continuity of $f_\infty$).

Then, let $N$ be large enough that for all $n \gt N$:

1. $\epsilon_n \gt \frac{\epsilon_\infty}{2}$
2. $d(f_n a_n, f_\infty a_\infty) \lt \frac{\epsilon_\infty}{6}$
3. For all $x \in K$, we have $d(f_\infty x, f_n x) \lt \frac{\epsilon_\infty}{6}$
4. $d(a_n, a_\infty) \lt \delta^*$

In condition (3) we've used the fact that $f_n$ converges to $f_\infty$ 
_uniformly_ on the compact set $K$.

Now we take as our covering familiy 

- the constant functions $$k : \mathbb{N}_\infty \to \mathbb{N}_\infty$$
- $$i_S : \mathbb{N}_\infty \to \mathbb{N}_\infty$$ for any infinite subset 
$$S \subseteq \{ n \gt N \} \subseteq \mathbb{N}$$.

As a reminder, the function $i_S$ is the unique monotone function 
$$\mathbb{N}_\infty \to \mathbb{N}_\infty$$ whose image is $$S \cup \{\infty\}$$.


Now on each member $g$ of this family, we need to produce a function
$$\delta : \mathbb{N}_\infty \to \mathbb{R}_{\gt 0}$$ which witnesses 

$$
\mathbb{N}_\infty \Vdash 
\forall b : X . \ 
d(a_{g(-)}, b) \lt \delta \to d(f_{g(-)}(a_{g(-)}), f_{g(-)}(b)) \lt \epsilon_{g(-)}
$$

Cashing out the last universal quantifier, we need to know that for all 
$$h : \mathbb{N}_\infty \to \mathbb{N}_\infty$$ and for all 
continuous $$b : \mathbb{N}_\infty \to X$$, 

If $$\mathbb{N}_\infty \Vdash d(a_{gh(-)},b) \lt \delta_{h(-)}$$
then we must have 
$$\mathbb{N}_\infty \Vdash d(f_{gh(-)}(a_{gh(-)}), f_{gh(-)}(b)) \lt \epsilon_{gh(-)}.$$

So let's build such a $\delta$ for the two cases in our cover!

<br>

First, if $g$ is the constant $k$ function. Then we need a convergent sequence 
$\delta_n$ so that for any function $$h : \mathbb{N}_\infty \to \mathbb{N}_\infty$$
and any convergent sequence $b_n$ in $X$, 

If $d(a_k,b_n) \lt \delta_{hn}$ for all $n$, 
then $d(f_k(a_k), f_k(b_n)) \lt \epsilon_k$ for all $n$ too.

Of course, this is easy to arrange by taking $\delta_n$ to be the 
constant sequence witnessing continuity of $f_k$ at $a_k$.

<br>

Second, if $g = i_S$ is the unique monotone function whose image is 
$$S \cup \{ \infty \}$$. Recall also that every member of $S$ is at least $N$.

Then we define $\delta_n$ to be $$\delta^* - d(a_{i_S n}, a_\infty)$$. 
Note this _is_ convergent, with limit $$\delta^*$$. Now we must show
for any function $$h : \mathbb{N}_\infty \to \mathbb{N}_\infty$$ and 
for any convergent sequence $$b_n$$ in $X$ that

If $d(a_{i_S h n}, b_n) \lt \delta_{hn}$ for all $n$,
then $d(f_{i_S h n}(a_{i_S h n}), f_{i_S h n}(b_n)) \lt \epsilon_{i_S h n}$.

But since $i_S h n \gt N$ and 
$$d(b_n, a_\infty) \leq d(b_n, a_{i_S h n}) + d(a_{i_S h n}, a_\infty) \lt \delta^*$$
we see that 

1. $\epsilon_{i_S h n} \gt \frac{\epsilon_\infty}{2}$
2. $d(f_{i_S h n}(a_{i_S h n}), f_{\infty}(a_\infty)) \lt \frac{\epsilon_\infty}{6}$
3. $d(f_\infty b_n, f_{i_S h n} b_n) \lt \frac{\epsilon_\infty}{6}$

so that we can compute 

$$
\begin{aligned}
d(f_{i_S h n}(a_{i_S h n}), f_{i_S h n}(b(n))) 
&\leq 
d(f_{i_S h n}(a_{i_S h n}), f_\infty(a_\infty)) +
d(f_\infty(a_\infty), f_\infty(b_n)) +
d(f_\infty(b_n), f_{i_S h n}(b_n)) \\
&\leq 
\frac{\epsilon_\infty}{6} + 
\frac{\epsilon_\infty}{6} + 
\frac{\epsilon_\infty}{6} \\
&=
\frac{\epsilon_\infty}{2} \\
&\lt 
\epsilon_{i_S h n}
\end{aligned}
$$

As desired.
<span style="float:right">$\lrcorner$</span>

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
[23]: https://ncatlab.org/nlab/show/big+and+little+toposes
[24]: https://ncatlab.org/nlab/show/Johnstone%27s+topological+topos
[25]: /2021/12/16/topological-categories.html
[26]: https://en.wikipedia.org/wiki/Box_topology
[27]: https://math.stackexchange.com/questions/871610/why-are-box-topology-and-product-topology-different-on-infinite-products-of-topo
[28]: https://en.wikipedia.org/wiki/Compact-open_topology
[29]: /2024/03/25/continuous-max-function
[30]: https://ncatlab.org/nlab/show/frame
[31]: https://en.wikipedia.org/wiki/Scott_continuity
[32]: https://en.wikipedia.org/wiki/Alexandroff_extension
[33]: https://ncatlab.org/nlab/show/canonical+topology
[34]: https://en.wikipedia.org/wiki/Subobject_classifier
[35]: https://londmathsoc.onlinelibrary.wiley.com/doi/abs/10.1112/plms/s3-38.2.237
[36]: https://en.wikipedia.org/wiki/First-countable_space
[37]: https://en.wikipedia.org/wiki/CW_complex
[38]: https://en.wikipedia.org/wiki/Spectrum_of_a_ring
[39]: /2022/12/13/internal-logic-examples.html
[40]: https://en.wikipedia.org/wiki/Sierpi%C5%84ski_space
[41]: https://ncatlab.org/nlab/show/countable+choice
[42]: https://ncatlab.org/nlab/show/countable+choice#WCC
[43]: https://ncatlab.org/nlab/show/Dedekind+cut
[44]: https://ncatlab.org/nlab/show/Cauchy+real+number
[45]: https://en.wikipedia.org/wiki/Baire_category_theorem
[46]: https://en.wikipedia.org/wiki/Second-countable_space
[47]: https://en.wikipedia.org/wiki/Compactly_generated_space
[48]: https://en.wikipedia.org/wiki/Locally_compact_space
[49]: https://ncatlab.org/nlab/show/principle+of+omniscience
[50]: https://ncatlab.org/nlab/show/quotient+type
[51]: http://www.lfcs.inf.ed.ac.uk/reports/92/ECS-LFCS-92-208/
[52]: https://core.ac.uk/download/33573841.pdf
[53]: https://planetmath.org/37propositionaltruncation
[54]: https://en.wikipedia.org/wiki/Markov%27s_principle
[55]: https://en.wikipedia.org/wiki/Apartness_relation
[56]: https://ncatlab.org/nlab/show/De+Morgan+topos
[57]: https://arxiv.org/pdf/2010.15632
[58]: https://www.cs.bham.ac.uk/~mhe/agda/Taboos.LLPO.html
[59]: https://doi.org/10.4230/LIPIcs.TLCA.2015.153
[60]: http://arxiv.org/abs/2104.10399
[61]: https://en.wikipedia.org/wiki/Bar_induction
[62]: https://ncatlab.org/nlab/show/injective+object
[63]: https://www.sciencedirect.com/science/article/pii/S0168007212000292
[64]: /2024/04/04/life-in-johnstones-topological-topos.html
[65]: https://core.ac.uk/download/33573841.pdf

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
    You can find a proof in Shulman and Simpson's aptly named note 
    [_Dependent Choice in Johnstone's Topological Topos_][21]

[^4]:
    And even then, it might not be obvious when you're learning! I remember 
    when I first learned pointset topology the idea of a "cylinder set" 
    and the product topology made no sense to me! Honestly without the 
    framework of [topological categories][25] or something similar, I could 
    see people _still_ being surprised that the [box topology][26] isn't 
    the "right" topology on an infinite product space! See, for instance,
    this old and highly upvoted [mse question][27].

[^5]:
    Note that it's entirely possible for two different elements
    $$p \neq q \in X(\mathbb{N}_\infty)$$ to witness convergence of 
    the same sequence (so $p_n = q_n$ for all $n$ and $\infty$)!

    Indeed, this will be crucial later, for instance in our discussion 
    of the [subobject classifier][34] $\Omega$.

[^6]:
    After my [last post][29] on a constructive extreme value theorem, I wanted to 
    see how it externalizes in topoi other than $\mathsf{Sh}(B)$. I'm pretty sure 
    in the effective topos we'll get something that looks like an algorithm 
    eating a function on a compact space and returning its max... But it's 
    super unclear what we should get interpreting this in $\mathcal{T}$! 
    After all, a [frame][30] in $\mathcal{T}$ is a topological lattice $L$. So 
    a locale in $L$ is a space whose frame of opens is _itself_ a space...

    I still haven't totally figured out this story
    (though I'm much less weirded out by the idea since I remembered that 
    [scott topologies][31] exist as a natural topology on the frame of opens), 
    so I won't say anything 
    more in _this_ post, but trying to understand $\mathcal{T}$ well enough to 
    externalize the constructive extreme value theorem was the second big 
    motivator for this post. Of course, understanding $\mathcal{T}$ was so fun 
    and interesting that I got distracted from my original goal, but that's how 
    these things tend to go for me, haha.

[^7]:
    If you want a _super_ concrete description, it's equivalent to 

    $$
    \left \{ 
        1, \frac{1}{2}, \frac{1}{3}, \frac{1}{4}, \ldots, \frac{1}{n}, \ldots, 0 
    \right \}
    \subseteq \mathbb{R}
    $$

    with the subspace topology.

[^8]:
    This is spelled out quite clearly in Johnstone's original paper 
    [_On a Topological Topos_][35]. Indeed, Johnstone computes the 
    covering sieves _very_ explicitly, and I highly recommend reading 
    about it there.

    I don't want to mention the grothendieck topology explicitly because 
    I think it would take too much time for not much payoff. I'm happy to 
    mainly summarize facts that are useful for working with 
    $\mathcal{T}$, and point to the relevant references where necessary.

[^9]:
    Still with the canonical grothendieck topology.

    Some people like to describe this (one object) category as the 
    "monoid of continuous endomorphisms of $$\mathbb{N}_\infty$$", but 
    I'd rather not say that because I think it would confuse the 
    exposition that follows.

[^10]:
    It's not _immediately_ obvious that this presheaf is actually a sheaf,
    but it turns out to be. This is in Johnstone's [original paper][35].

[^11]:
    This is the first time I'm actually written down the definition of 
    (metric space) continuity in full! No wonder students struggle with 
    this, haha. I've forgotten what a mouthful it is!

[^12]:
    Which looks simple now, but coming up with it took me longer than 
    I'd care to admit.
    Making this computation work is the crux of the whole proof.

[^13]:
    Here we have to refer to external metric spaces, and we prove a 
    kind of "theorem schema". I suspect something like this is true 
    purely internally, if we can find the right definition of a 
    "metric space" in $\mathcal{T}$. Obviously we want a distance 
    function $d : X \times X \to \mathbb{R}_{\geq 0}$ satsifying the 
    usual axioms. But we also need to know that the topology $d$ 
    puts in $X$ agrees with the _intrinsic_ topology on $X$!

    Since $d$ is externally continuous we know that metric-open balls will 
    always be open in $X$, so I think the condition is something like 
    "every open of $X$ contains an open ball" or maybe 
    "every open of $X$ is the union of the open balls inside it".

    This should be expressible in the internal logic since the opens of 
    $X$ are exactly the inhabitants of $\Sigma^X$ where $\Sigma$ is the 
    sierpinski space.

    I know that Davorin Lešnik has [thought about this][60], but 
    I really want to get this post out (and ideally turn it into a paper)
    so unfortunately I won't be pursuing this any further... for now!

[^14]:
    I don't know if there are constructive subtleties with the notion of 
    cauchy completeness which might be relevant here, and since I really 
    want to get this blog post out I don't want to read a bunch of literature 
    on constructive metric spaces to try and figure it out... 

    If anyone happens to know some facts about constructive metric spaces, though,
    I would love to hear about them! But for now, treat this example as being 
    more to showcase how dependent choie works than to say anything profound 
    about the topological topos.

[^15]:
    A set $D \subseteq X$ is called <span class=defn>Strongly Dense</span>
    if for any open set $V$ we know that $D \cap V$ is inhabited.

[^16]:
    You might wonder why we need a "nonconstructive" axiom to do this. Why 
    can't we use induction on $\mathbb{N}$?

    After all, we can prove (constructively, in type theory) that

    $$
    \left (
        \prod_{x:X} \sum_{y:X} R(x,y)
    \right ) 
    \to 
    \left ( 
        \prod_{x_0 : X }
        \sum_{f : \mathbb{N} \to X}
        f(0) = x_0 \land \prod_{n:\mathbb{N}} R(f(n), f(n+1))
    \right )
    $$

    (and this makes a nice exercise!)

    The difference lies in $\sum$ vs $\exists$! To build a term
    of type $\prod_x \sum_y R(x,y)$ is to build a function that 
    eats an $x$ and returns a $y$ alongside a proof that $R(x,y)$.
    This gives us a _canonical_ choice in $$\{ y \mid R(x,y) \}$$ -- 
    just use the one this function gave us!

    Dependent choice works with something much weaker. It says we can build 
    such a function even when there _merely exists_ such a $y$, without 
    being handed a witness! (Of course, the function we're given only 
    merely exists too)

    Think about the semantics in $\mathsf{Sh}(B)$ for a moment. 
    Here, to say that $\exists y . R(x,y)$ is to say that there's an 
    open cover of $B$ and a local witness $y$ on each element of the 
    cover. But it's entirely possible for these witnesses to not glue 
    into a global witness!

[^17]:
    This realization has probably been made by many people, but it was 
    added to the nlab by Mike Shulman.

[^18]:
    Notably Moerdijk and Reyes, in 
    _Smooth spaces versus continuous spaces in models 
    for synthetic differential geometry_, for instance.

[^19]:
    This is the quotient type in the sense of Li's [PhD thesis][65], 
    _not_ the (higher!) quotient type in the sense of HoTT... 
    Though the quotient type I mean is almost certainly the $0$-truncation 
    of the higher inductive quotient type.

    I've been meaning to spend some time thinking about how you can prove 
    theorems about a 1-topos by working in HoTT and truncating everything 
    at the end, but I haven't had the time.

[^20]:
    Actually, I think I remember reading somewhere that the analytic 
    omniscience principles are always statements about the cauchy reals. 
    The reason countable choice makes them properties of the dedekind reals 
    is because under CC the dedekind and cauchy reals agree.

    If an expert sees this and happens to know offhand if that's true, 
    I would love to know for sure!
