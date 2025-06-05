---
layout: post
title: An Empty Product of Nonempty Sets
tags:
  - topos-theory
---

A few days ago I saw a [cute question][1] on mse asking about a particularly 
non-intuitive failing of the axiom of choice. I remember when I was an 
undergrad talking to a friend of mine about various statements equivalent 
to choice, and being particularly hung up on the same statement that OP 
asks about -- The product of nonempty sets is nonempty. I understood that 
there were models where the axiom of choice fails, and so in those models 
we must have some family of nonempty sets whose product is, somehow, empty!
Now that I'm older and I've spent *much* more time thinking about these things, 
this is less surprising to me, but reading that question reminded me how badly
I once wanted a concrete example, and so I'll share one here!

This should be a pretty quick post, since I'll basically just be fleshing 
out my answer to that mse question. But I think it'll also be nice to have 
here, since these things can be hard to find when you're first getting into 
logic and topos theory! Let's get to it!

---

First, let's remember that for any group $G$ the category $G\text{-}\mathsf{Set}$
of sets equipped with a $G$-action is a topos. Indeed you can see it as a 
presheaf topos, since $G\text{-}\mathsf{Set}$ is equivalent to the category 
of functors from $G \to \mathsf{Set}$ (viewing $G$ as a one-object category).
We've talked about this topos [before][2], and it's wild to think how 
far I've come since writing that post!

The basic idea of $G\text{-}\mathsf{Set}$ as a topos is that any set theoretic 
construction we do to some $G$-sets again gives us $G$-sets! For instance, 
any (co)limits of $G$-sets will have a natural $G$-action. If $X$ is a $G$-set
then its powerset $\mathcal{P}(X)$ has a $G$-action where if 
$A \in \mathcal{P}(X)$ we define $$g \cdot A = \{g \cdot a \mid a \in A \}$$,
which is another element of $\mathcal{P}(X)$. If $X$ and $Y$ are $G$-sets 
then the set of functions $X \to Y$ is again a $G$-set where we say 
$(g \cdot_{X \to Y} f)(x) = g \cdot_Y f(g^{-1} \cdot_X x)$.

In particular, we can recover the "$G$-equivariant" constructions as the 
[global elements][3]! So even though $\mathcal{P}(X)$ contains *all* subsets 
of $X$ (not just the $G$-invariant subsets), if we look at the global elements
(that is the maps $1 \to \mathcal{P}(X)$) we do get exactly the 
$G$-invariant subsets. Similarly while the set of functions $X \to Y$ sees 
*all* functions, the global elements of this set will pick out exactly the 
$G$-equivariant functions. 

But $G\text{-}\mathsf{Set}$ has a [coreflective subcategory][4] given by those
$G$-sets all of whose orbits are finite. The coreflector takes a $G$-set 
and just deletes all the infinite orbits, so we have an adjunction

$$
(\iota : G\text{-}\mathsf{Set}_\text{finite orbits} \to G\text{-}\mathsf{Set})
\dashv
(R : G\text{-}\mathsf{Set} \to G\text{-}\mathsf{Set}_\text{finite orbits})
$$

which gives us a comonad $\iota R$ on $G\text{-}\mathsf{Set}$. This 
comonad is idempotent, and its category of coalgebras is equivalent to 
$$G\text{-}\mathsf{Set}_\text{finite orbits}$$. Then since $\iota$ is left 
exact (and so is $R$, since it's a right adjoint), we see that 
$$G\text{-}\mathsf{Set}_\text{finite orbits}$$ is the category of coalgebras 
for a lex comonad on a topos, thus is *itself* a topos!

<div class=boxed markdown=1>
As a cute exercise, check that $\iota$ really is left exact!
</div>

Now doing computations in this topos is pretty easy! Finite limits and 
arbitrary colimits are computed as in $G\text{-}\mathsf{Set}$ since 
$\iota$ preserves these. Arbitrary limits and exponentials $Y^X$ come from 
coreflecting -- that is $Y^X$ as computed in 
$$G\text{-}\mathsf{Set}_\text{finite orbits}$$ is just what we get by 
removing the infinite orbits from $Y^X$ as computed in $G\text{-}\mathsf{Set}$,
and similarly for limits. The subobject classifier is just the usual set 
of truth values $$\{ \top, \bot \}$$ with the trivial $G$-action[^1]. 
In particular this topos is boolean, so set theory inside it is *particularly*
close to the usual ZF set theory.

Now with this in mind, we can prove the main claim of this post:

<div class=boxed markdown=1>
In $\mathbb{Z}\text{-}\mathsf{Set}_\text{finite orbits}$, let $C_n$ be $\mathbb{Z}/n$ 
with its obvious $\mathbb{Z}$-action. Then each $C_n$ is inhabited[^3] in 
the sense that $\exists x . x \in C_n$, and yet $$\prod_n C_n = \emptyset$$!

So this topos shows explicitly how, in the absence of choice, you can have 
a family of nonempty sets[^2] whose product is somehow empty!
</div>

The computation is actually quite friendly! To compute $\prod_n C_n$ in 
this topos, we first compute the product in the category of *all* 
$\mathbb{Z}$-sets, then throw away any infinite orbits.

But it's easy to see that *every* orbit is infinite! Any element of the 
product will contain an element from every $C_n$, so that in any finite 
number of steps some large entry in this tuple won't be back where it started.

---

Ok, this one was *actually* quite quick, which I'm happy about! 
My parents are visiting soon, and I'm excited to take a few days 
to see them ^_^. I have another shorter post planned which another 
grad student asked me to write, and I've finally *actually* 
started the process of turning my [posts on the topological topos][9]
into a paper. I'm starting to understand [TQFTs][10] better, and it's 
been exciting to learn a bit more physics. Hopefully I'll find time 
to talk about all that soon too, once I take some time to really organize 
my thoughts about it.

Thanks for hanging out, all! Stay safe, and we'll talk soon.



---

[1]: https://math.stackexchange.com/q/5072206/655547
[2]: /2022/12/13/internal-logic-examples
[3]: https://ncatlab.org/nlab/show/global+element
[4]: https://ncatlab.org/nlab/show/coreflective+subcategory
[5]: https://ncatlab.org/nlab/show/profinite+completion+of+a+group
[6]: https://ncatlab.org/nlab/show/Grothendieck%27s+Galois+theory
[7]: https://en.wikipedia.org/wiki/Residually_finite_group
[8]: https://ncatlab.org/nlab/show/bracket+type
[9]: /2024/07/03/life-in-johnstones-topological-topos
[10]: https://en.wikipedia.org/wiki/Topological_quantum_field_theory

[^1]:
    In case $G = \mathbb{Z}$ then it's a kind of cute fact that this topos 
    is equivalent to the 
    topos of *continuous* (discrete) $\widehat{\mathbb{Z}}$-sets, where 
    $\widehat{\mathbb{Z}}$ is the [profinite completion][5] of $\mathbb{Z}$.
    See, for instance, Example A2.1.7 on page 72 of the elephant. This gives 
    another computationally effective way to work with this topos!

    I'm pretty sure I convinced myself that more generally the category 
    of $G$-sets all of whose orbits are finite should be equivalent to 
    the category of continuous discrete $\widehat{G}$-sets, but I haven't 
    thought hard enough about it to say for sure in a blog post.

[^2]:
    Since this topos is boolean, nonempty and inhabited are actually 
    synonyms here. Moreover, this "nonempty" is closer to how a lot of 
    working mathematicians speak, so it felt right to use this wording here.

[^3]:
    Of course, there's no global points for $n \neq 1$, since maps 
    $1 \to C_n$ correspond to fixed points. But existential quantification 
    is *local*, so that the topos models $\exists x \in C_n . \top$ if there's 
    some surjection $V \twoheadrightarrow 1$ and a map $V \to C_n$. ~~We 
    can take $V = \mathbb{Z}$ with its left multiplication action on itself, 
    and there *is* a map from $\mathbb{Z} \to C_n$.~~ **Edit, June 5**: 
    Thanks to Kevin Carlson for pointing out that $\mathbb{Z}$ with its 
    left multiplication action isn't in this topos, since its orbit is infinite! 
    We instead need, for each $n$, to look at the surjection from 
    $C_n \twoheadrightarrow 1$ and then you can use the identity map from 
    $C_n \to C_n$ to witness inhabited-ness.
    

    If you're more used to type theory, we don't have $\Sigma_{x : C_n} \top$,
    since that would imply a global element. But despite this, we *do* 
    have the [propositional truncation][8] 
    $\lVert \Sigma_{x : C_n} \top \rVert$, so that an element of $C_n$ 
    *merely* exists. 
