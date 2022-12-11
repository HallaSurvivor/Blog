---
layout: post
title: Externalizing Some Simple Topos Statements
tags:
  - 
---

Hey all! It's been a minute. I've been super busy with 
[the UC strike][1] and honestly I haven't done math in any
serious capacity for almost the past month. It's been a 
lot of hard work trying to get fair contracts out of the UC, 
but I had a lot of travel plans this December to see my friends,
so I've taken a step back from the picket line until January.

This means I have time to do math again, and it's been really good 
for me to get back into it! I've started working with [Peter Samuelson][2]
on some really cool work involving skein algebras, and I can't wait to
chat about it once I spend more time with it.

I also spent some time trying to understand manifolds in a topos of $G$-sets.
I gave a (fairly informal) talk in Dave Weisbart's seminar, where I tried to
pitch him topos theory as a method of studying $G$-invariant constructions[^1],
and I thought I remembered a result that we can get our hands on a 
[global quotient orbifold][3] $M // G$ by working with a manifold internal to 
$G$-set... but I couldn't find a reference for this, and it turns out it's 
false. So my last couple weeks, when I had the energy to do math after picketing,
looked eerily like Julia Robinson's famous description of her week:

<p style="text-align:center;">
<img src="/assets/images/internal-logic-examples/robinson.png" width="50%">
</p>

I learned a _ton_ while doing this, though, and I wanted to share some 
insights with everyone. I haven't been able to find many examples of 
people taking statements in the internal logic of a topos and externalizing
them to get "classical" statements, so I had to work out a bunch of small
examples myself.

I want to share some of them here, and hopefully explain how they work, so 
the next people interested in this have an easier time ^_^. 

Let's get started!

---

$$\lvert X \rvert = 3$$

Let's start small. What does it mean to say that $$\lvert X \rvert = 3$$? 
This is really an abbreviation saying "there's a bijection between $X$ and $3$",
which we expand out to

$$
\exists \alpha : 3^X . \exists \beta : X^3 . 
\alpha \beta = \text{id}_3 \land \beta \alpha = \text{id}_X
$$

Here, of course, we're writing $A^B$ for the [exponential object][4] of the
topos.

So we're saying that $$\mathcal{E} \models \lvert X \rvert = 3$$. If we switch over 
to the forcing language, we're saying that $$1 \Vdash \lvert X \rvert = 3$$, and from
here we can follow the instructions in section VI.6 of Mac Lane and Moerdijk's 
_Sheaves in Geometry and Logic_. In fact, since we'll be working exclusively
with grothendieck topoi in this post, we can work with the slightly simpler
sheaf semantics outlined in section VI.7.

First, let's look at the case $\mathcal{E} = G\text{-}\mathsf{Set}$.

We start with 

$$
1 \Vdash \exists \alpha : 3^X . \exists \beta : X^3 . 
\alpha \beta = \text{id}_3 \land \beta \alpha = \text{id}_X
$$

Next we cash out our existential quantifiers for honest (generalized) 
elements $f$ in $3^X$ and $g$ in $X^3$. The "local" nature of existential
quantification, though, means that our generalized elements no longer have
domain $1$ (which would make them _global_ elements). Instead, they have
domain $V$ for some epi $V \twoheadrightarrow 1$. 

Of course, in a topos of $G$-sets, every nonempty object admits a unique
epi to $1$, and every nonempty object is a disjoint union of $G$-orbits. 
So it's not hard to see we can restrict attention to the connected epis 
(transitive $G$-sets). But we _also_ know that truth is local. So we can pull
back some transitive $G$-set along a further epimorphism to assume that our
connected object is actually $G$ itself!

So we end up with elements $\alpha : G \to 3^X$ and $\beta : G \to X^3$
so that 

$$
G \Vdash \alpha \beta = \text{id}_3 \land \beta \alpha = \text{id}_X
$$

But what does this mean? Well, in $G$-set, the exponential $A^B$ is the set of
_all_ functions $\{\varphi : B \to A\}$ equipped with the conjugation action:

$$
(g \cdot_{A^B} \varphi)(x) = g \cdot_A \varphi (g^{-1} \cdot_B x)
$$

Notice that the _global_ elements of $A^B$ are the maps $1 \to A^B$, 
which are thus the fixed points of $A^B$. But to say $\varphi = g \cdot \varphi$
for all $g$ is to say that $\varphi$ is $G$-equivariant. However generalized
elements give us access to other maps. In particular:

<div class=boxed markdown=1>
Exercise: Show that the $G$-elements of $A^B$ (that is, the maps $G \to A^B$)
are in natural bijection with ordinary functions $B \to A$ that ignore the 
$G$-structure entirely.

Hint: Look at what happens to the identity element of the group
</div>

So then we have two ordinary functions $\alpha : X \to 3$ and $\beta : 3 \to X$ 
which are mutually inverse. This means exactly that the underlying set of $X$
has $3$ elements.

This brings us to an important observation about $G$-sets:

Something is "locally" true in $G\text{-}\mathsf{Set}$ exactly when it's 
true for the underlying sets. This is basically because each $G$-set $X$ 
is covered by $G \times X$, but this is isomorphic to $G \times UX$ where
$UX$ (the underlying set of $X$) is equipped with the trivial $G$-action!

So if we want a statement in $G\text{-}\mathsf{Set}$ to externalize to
something $G$-equivariant, we'll want to avoid existential quantifiers
and disjunctions (since these are only true up to a cover)[^3].

<div class=boxed markdown=1>
Can you find a formula $\psi(X)$ (which will use $G$ as a parameter) so that 
$G\text{-}\mathsf{Set} \models \psi(X)$ if and only if $X$ has finitely many
$G$-orbits[^2]?
</div>

<p style="text-align:center;">
<img src="/assets/images/internal-logic-examples/hand-raise.gif" width="50%">
</p>

Great question! I'm glad you asked!

Say that instead of $G$-sets, we work inside a topos $\mathcal{E} = \mathsf{Sh}(S)$
for some topological space $S$[^4].
What does it mean if $$\mathcal{E} \models \lvert X \rvert = 3$$?

Well again, we see that 

$$
1 \Vdash \exists \alpha : 3^X . \exists \beta : X^3 . 
\alpha \beta = \text{id}_3 \land \beta \alpha = \text{id}_X
$$

and we cash out our existential quantifiers for _local_ witnesses. That is,
there's an open cover $\{ U_i \}$ of $S$ with elements 
$\alpha_i : U_i \to 3^X$ and $\beta_i : U_i \to X^3$ so that, for each $U_i$,

$$
U_i \Vdash \alpha_i \beta_i = \text{id}_3 \land \beta_i \alpha_i = \text{id}_X
$$

Now, an element $U_i \to A^B$ is "just" a function $B \to A$ defined over $U_i$.
So altogether we see that $\lvert X \rvert = 3$ if and only if there's an open
cover $$\{U_i\}$$ of $S$ so that 
$$X \! \upharpoonright_{U_i} \cong 3 \! \upharpoonright_{U_i}$$
for each $i$.

This means $X$ is _locally isomorphic_ to $3$, the disjoint union of three 
copies of $S$. It's not hard to see that this means $X$ is a 3-sheeted 
covering space of $S$.

Notice that these local isomorphisms do _not_ have to glue into a global
isomorphism! The simplest thing to do is to give a picture. If $S = S^1$ 
is a circle, and $X$ is a triple cover as shown below:

<p style="text-align:center;">
<img src="/assets/images/internal-logic-examples/triple-cover.png" width="25%">
</p>

then $X$ is locally isomorphic to the trivial triple cover $3$:

<p style="text-align:center;">
<img src="/assets/images/internal-logic-examples/triple-cover-trivial.png" width="25%">
</p>

despite the fact that they _aren't_ globally isomorphic!

From the perspective of the internal logic, the issue is that the isomorphisms
over each $U_i$ are not compatible in the sense that 
$$\alpha_i \! \upharpoonright_{U_i \cap U_j} \neq \alpha_j \! \upharpoonright_{U_i \cap U_j}$$.

<div class=boxed markdown=1>
If you've never done it before, it's worth going through this in detail! 

Cover $S^1$ by open sets (so that each intersection is connected,
for simplicity) and show that the two triple covers are isomorphic on 
each open set, but these isomorphisms aren't compatible on intersections.
</div>

Note, as an aside, that we've been working with an explicit choice of 
finite cardinality: $\lvert X \rvert = 3$. Say instead we wanted the 
weaker "$\lvert X \rvert \text{ is finite}$". There's nothing to worry about 
in $G\text{-}\mathsf{Set}$ because this topos is boolean, satisfies AC, etc.
However for topoi without LEM, there are multiple inequivalent notions of 
finiteness. See [here][7] for a discussion[^5].

---

$a = a' \lor a \neq a'$ 

(decidable. Show the example of the topos $\mathsf{Set}^\to$ where $A_0 \to A_1$ 
is decidable iff it's a mono)

---

come up with exactly one more.


---

[^1]:
    In particular, we're planning to think about $G$-equivariant brownian 
    motion.

[^2]:
    Try 
    $\exists n : \mathbb{N} . \exists f : X^{G \times n} . 
    \ulcorner f \text{ is surjective} \urcorner$

[^3]:
    Something like this is probably true for more general [etendues][5],
    which (up to a cover) look like $\mathsf{Sh}(X)$. The case of $G$-sets
    is particularly easy, since locally they look like 
    $\mathsf{Set} = \mathsf{Sh}(\star)$.

[^4]:
    Nothing at all changes if we instead take $X$ to be a [locale][6]

[^5]:
    Also note that the existential quantifier really impacts things. Essentially
    we asked for 
    $\mathcal{E} \models \exists \alpha : X \cong 3 . \top$. 
    If we had instead asked for an actual (global) element, 
    $\mathcal{E} \models \alpha : X \cong 3$, we would have actual isomorphism
    instead of mere local isomorphism. This is what the previous nlab link 
    calls "(bishop) finite", and it's a stronger condition than what we've been
    working with.

    

[1]: https://www.fairucnow.org/
[2]: https://sites.google.com/view/petersamuelson/home?pli=1
[3]: https://ncatlab.org/nlab/show/global+quotient+orbifold
[4]: https://en.wikipedia.org/wiki/Exponential_object
[5]: https://ncatlab.org/nlab/show/%C3%A9tendue
[6]: https://ncatlab.org/nlab/show/locale
[7]: https://ncatlab.org/nlab/show/finite+set
