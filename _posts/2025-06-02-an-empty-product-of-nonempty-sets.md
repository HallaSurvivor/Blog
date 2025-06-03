---
layout: post
title: An Empty Product of Nonempty Sets
tags:
  - topos-theory
---

Earlier today I saw a [cute question][1] on mse asking about a particularly 
non-intuitive failing of the axiom of choice. I remember when I was an 
undergrad talking to a friend of mine about various statements equivalent 
to choice, and being particularly hung up on the same statement that OP 
asks about -- The product of nonempty sets is nonempty. I understood that 
there were models where the axiom of choice fails, and so in those models 
we must have some family of nonempty sets whose product is, somehow, empty!
Now that I'm older and I've spent *much* more time thinking about these things, 
this is less surprising to me, but reading that question reminded me how badly
I wanted a concrete example, and so I'll share one here!

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
$A \in \mathcal{P}(X)$ we define $g \cdot A = \{g \cdot a \mid a \in A \}$,
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
and just deletes all the infinite orbits! So we have an adjunction

$$
(\iota : G\text{-}\mathsf{Set}_\text{finite orbits} \to G\text{-}\mathsf{Set})
\dashv
(R : G\text{-}\mathsf{Set} \to G\text{-}\mathsf{Set}_\text{finite orbits})
$$

which gives us a comonad $\iota R$ on $G\text{-}\mathsf{Set}$. Indeed this 
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
and similarly for limits. The subobject classifier 

In fact, there's something really cute going on here which also lets you do 
these computations efficiently: It's "well known" that for any group $G$ 
the category of finite sets with a $G$ action is equivalent to the category of
finite discrete sets with a *continuous* $\widehat{G}$ action, where 
$\widehat{G}$ is the [profinite completion][5] of $G$ -- this is a central fact 
in [Grothendieck's Galois Theory][6]. I think there's nothing special about 
finite sets, though. What really matters is *finite orbits*. Indeed, it 
seems to me like 

<div class=boxed markdown=1>
$$
G\text{-}\mathsf{Set}_\text{finite orbits} 
\simeq
\widehat{G}\text{-}\mathsf{Sets}
$$
</div>

Recall $\widehat{G} = \varprojlim_{N \text{ finite index}} G \big / N$ is the 
limit (in the category of *topological* groups) of all the finite index quotients 
of $G$ (with the discrete topology). Then since $G$ (with the discrete topology)
has canonical maps to all the $G/N$, by the universal property we have a map 
from $G \to \widehat{G}$ (which is an injection exactly when $G$ is 
[residually finite][7]).

Now, say $X$ is a $G$-set with finite orbits. Then $X$ 





---

[1]: https://math.stackexchange.com/q/5072206/655547
[2]: /2022/12/13/internal-logic-examples
[3]: https://ncatlab.org/nlab/show/global+element
[4]: https://ncatlab.org/nlab/show/coreflective+subcategory
[5]: https://ncatlab.org/nlab/show/profinite+completion+of+a+group
[6]: https://ncatlab.org/nlab/show/Grothendieck%27s+Galois+theory
[7]: https://en.wikipedia.org/wiki/Residually_finite_group
