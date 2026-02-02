---
layout: post
title: Computing with the Atiyah-Bott-Goldman Bracket on the Character Variety
tags:
  - 
---

The ($G$-)<span class=defn>Character Variety</span> of a surface $\Sigma$ 
is the space of representations $\pi_1 \Sigma \to G$. This variety admits 
a symplectic structure (due to Atiyah-Bott in differential geometric terms 
and Goldman in more algebraic terms) which is extremely interesting from 
many perspectives. For instance, my thesis is in skein theory (though you 
might not know it from my blog posts) and by *quantizing* this symplectic 
structure we recover the skein algebra of our surface. In this post we'll 
go through this construction and do a simple example to show that this 
symplectic structure really is quite explicit! Though alomst everything here 
is already in [Goldman's original paper][6], which is an *extremely* pleasant
read!

My friend [Shane][1] and I are organizing a conference on NonAbelian Hodge
(NAH) Theory, and in the process of drafting all the talks we've been doing a lot 
of small computations and examples which we'll ask our speakers to include. 
This has been *great* for me, since I love doing computations, and I've 
learned a ton just by working through easy examples with Shane. One of my 
favorite professors, [Brian Collier][2] also gave a talk recently where he 
explained a lot of this extremely well, with an eye towards NAH. I probably
won't be able to resist including a few of the things he mentioned in this 
post, even though I don't fully understand them, and they're not strictly 
on topic. Hopefully this blog post will be similarly helpful for future 
students! 

Also, it's a double header of blog posts today, since it took me forever to 
finally stop looking for a counterexample in my Zorn's Lemma post. I've 
been writing these in parallel, but I foolishly put my Zorn's Lemma post in 
my master branch and I didn't feel like rebasing things to be able to 
publish this first. I also spent too much time thinking about stacks for that 
post to mention character *stacks* in this one, but maybe I'll try to do 
some analogous derived computations with character stacks someday.

Let's get to it!

---

First, let's recall the simplest version of the character variety: 
Given a nice Lie group $G$ and a surface $\Sigma$ we can build 

$$\mathsf{Ch}(\Sigma,G) = \text{Hom}(\pi_1 \Sigma, G) \big / G$$

where $G$ acts on $\text{Hom}(\pi_1 \Sigma, G)$ by conjugation.

Writing 
$\pi_1 \Sigma = 
\langle a_1, b_1, \ldots, a_g, b_g \mid [a_1,b_1] \cdots [a_g,b_g] = 1 \rangle$ 
for a genus $g$ surface, we see that $\text{Hom}(\pi_1 \Sigma, G)$ is 
a closed subspace of $G^{2g}$. Of course, you can add punctures and boundaries
and whatnot too! It changes the presentation of the fundamental group, but 
you'll still get a subspace of some power of $G$.

For instance, if $\Sigma = S^1 \times S^1$ and $G = SL_2(\mathbb{C})$ 
then $\pi_1 \Sigma = \langle a,b \mid [a,b]=1 \rangle$ so that 

$$
\text{Hom}(\pi_1 \Sigma, G) = 
\{ (A, B) \in SL_2(\mathbb{C})^2 \mid A^{-1} B^{-1} A B = 1 \}
$$

and $\mathsf{Ch}(\Sigma, G)$ is the quotient of this by the action of $G$ 
with $M \cdot (A,B) = (M^{-1} A M, M^{-1} B M)$. Precisely we look at the 
ring of functions $$\mathcal{O}_{\text{Hom}(\pi_1, \Sigma)}$$
on $$\text{Hom}(\pi_1 \Sigma, G)$$, then look at the subring
$$\mathcal{O}_{\text{Hom}(\pi_1, \Sigma)}^G$$ of functions which is invariant 
under this $G$ action. Then we define $\mathsf{Ch}(\Sigma, G)$ to be 
$$\text{Spec}(\mathcal{O}^G_{\text{Hom}(\pi_1 \Sigma, G)})$$.

Of course, if we want to put a symplectic structure on this then we need to 
understand it's tangent space. If $\rho : \pi_1 \Sigma \to G$ is a 
representation then the tangent space at $\rho$ controls first order 
deformations of this homomorphism. If this sounds like [group cohomology][5] 
to you then you're completely right!

Indeed to deform $\rho : \pi_1 \Sigma \to G$, we need to deform the output
to $\rho_\epsilon$ in such a way that these are all still homomorphisms. 
Deforming an element of a Lie group $G$ means multiplying by 
$\exp(\epsilon u)$ for some $u \in \mathfrak{g}$ so that 
$\rho_\epsilon = \exp(\epsilon u) \rho$ for some function 
$u : \pi_1 \Sigma \to \mathfrak{g}$. For this to stay a homomorphism we need
$\rho_\epsilon(xy) = \rho_\epsilon(x) \rho_\epsilon(y)$ so that 

$$
\exp(\epsilon u(xy)) \rho(xy) \overset{?}{=}
\exp(\epsilon u(x)) \rho(x) \exp(\epsilon u(y)) \rho(y)
$$

But we can commute the $\rho(x)$ and the $\exp(\epsilon u(y))$ across 
each other at the cost of a conjugation:

$$
\exp(\epsilon u(xy)) \rho(xy) \overset{?}{=}
\exp(\epsilon u(x)) 
\left ( \rho(x) \exp( \epsilon u(y)) \rho(x)^{-1} \right )
\rho(x) \rho(y)
$$

But since we know 

- $\rho(xy) = \rho(x) \rho(y)$ 
- the conjugation action at the level of the Lie group 
becomes the adjoint action at the level of the Lie algebra 
- $\exp(-)$ sends addition in the Lie algebra to multiplication in the 
Lie group

this equality is the same as

$$
\exp(\epsilon u(xy)) \overset{?}{=}
\exp(\epsilon (u(x) + \text{Ad}_{\rho(x)} u(y)))
$$

So we find $\rho_\epsilon$ is a homomorphism if and only if 
$u(xy) = u(x) + \text{Ad}_{\rho(x)} u(y)$ so that 
$u : \pi_1 \Sigma \to \mathfrak{g}$ is a group 1-cocycle valued
in $\mathfrak{g}$ with the action coming from composing 
$\rho : \pi_1 \Sigma \to G$ with the 
adjoint action of $G$ on $\mathfrak{g}$!

Of course, we're supposed to identify points in $\text{Hom}(\pi_1 \Sigma, G)$ 
under the action of $G$ by conjugation. In general if $G$ acts nicely on a 
manifold $M$ then the tangent space 
$T_{[p]} (M \big / G)$ can be compuated as the quotient 
of the tangent space at $p \in M$ by the tangent space in the orbit 
$p \in G \cdot p$: $T_{[p]} (M \big / G) \cong T_p M \big / T_p (G \cdot p)$.

For us, $G \cdot \rho = \{ g^{-1} \rho g \mid g \in G \}$ and the tangent 
space to $\rho$ comes from taking $g = \exp(\epsilon u_0)$ to be an 
infinitesimaly small change, with $u_0 \in \mathfrak{g}$. Then writing this as 
a cocycle means writing $\exp(-\epsilon u_0) \rho \exp(\epsilon u_0)$ as 
$\exp(\epsilon u) \rho$. So we move the $\rho$ to the right, again at the 
cost of a conjugation, to get 

$$
\exp(-\epsilon u_0) \rho \exp(\epsilon u_0) =
\exp(-\epsilon u_0 \exp(\epsilon \text{Ad}_\rho u_0) \rho =
\exp(\epsilon (\text{Ad}_\rho u_0 - u_0)) \rho
$$

so that our cocycle is $\text{Ad}_\rho u_0 - u_0$, which we recognize as the 
coboundary of $u_0$!

So then when $M = \text{Hom}(\pi_1 \Sigma, G)$ this means the tangent space 
to $\rho$ in $\text{Ch}(\Sigma,G)$ is given by the tangent space in
$\text{Hom}(\pi_1 \Sigma, G)$ mod the tangent space in $G \cdot \rho$. That is,
cocycles mod coboundaries, and $T_\rho \text{Ch}(\Sigma, G)$ is exactly the 
group cohomology $H^1(\pi_1 \Sigma, \mathfrak{g})$ where $\mathfrak{g}$ is a 
$\pi_1 \Sigma$-module by composing $\rho : \pi_1 \Sigma \to G$ with the adjoint 
action of $G$ on $\mathfrak{g}$!

<br>

So now we want to define a sympelctic form. This is supposed to eat two 
tangent vectors at a point $\rho$ and spit out a number. So using our 
identification of $T_\rho \mathsf{Ch}(\Sigma, G)$ with 
$H^1(\pi_1 \Sigma, \mathfrak{g}^{\text{Ad} \rho})$ we want a way to eat 
two cohomology classes and get a number. Of course, $\mathfrak{g}$ has its
[Killing form][3] $\kappa : \mathfrak{g} \otimes \mathfrak{g} \to \mathbb{R}$.
This is equivariant if we put the adjoint action on $\mathfrak{g}$ and the 
trivial action on $\mathbb{R}$ since the killing form is invariant under 
automorphisms of $\mathfrak{g}$ (such as $\text{Ad}(\rho(-))$), so we get 
a map on cohomology

$$
H^1(\pi_1 \Sigma, \mathfrak{g}) \otimes H^1(\pi_1 \Sigma, \mathfrak{g})
\to
H^2(\pi_1 \Sigma, \mathbb{R}) \cong \mathbb{R}
$$

(where $H^2(\pi_1 \Sigma, \mathbb{R})$ has the trivial action on $\mathbb{R}$)
by sending 1-cocycle representatives 
$\phi, \psi : \pi_1 \Sigma \to \mathfrak{g}$
to the 2-cocycle 
$(\phi \smile_\kappa \psi)(g,h) = \kappa(\phi(g), g \cdot \psi(h))$,
though we won't be computing with the bar resolution so this is not actually 
that useful for us.

For those who prefer differential geometry, $\Sigma$ is a classifying space for 
$\pi_1 \Sigma$ (since its universal cover is contractible by [uniformization][4])
so from a $\pi_1 \Sigma$-module $M$ we can build a local system $\widetilde{M}$
on $\Sigma$ for which group cohomology $H^\bullet (\pi_1 \Sigma, M)$ agrees 
with sheaf cohomology $H^\bullet (\Sigma, \widetilde{M})$. From this 
perspective the above pairing (with the equivalence 
$H^2(\pi_1 \Sigma, \mathbb{R}) \cong \mathbb{R}$) can be written in terms
of $\widetilde{\mathfrak{g}}$-valued differential forms

$$
H^1(\Sigma, \widetilde{\mathfrak{g}}) 
\otimes 
H^1(\Sigma, \widetilde{\mathfrak{g}})
\overset{\land_\kappa}{\to}
H^2(\Sigma, \mathbb{R})
\overset{\int}{\to}
\mathbb{R}
$$

where the "wedge product" $\land_\kappa$ is defined using the 
killing form to get a real 2-form which we can integrate over our 
surface to get a real number.

Since the Killing form is nondegenerate for nice (reductive) Lie groups, 
we see this 2-form is nondegerate. Closedness is more subtle, and I'd rather 
this blog post be quick, so I won't take the time to figure out exactly how 
that works right now. See Section 1.8 of [Goldman's paper][6] for more 
discussion.

Together, though, nondegeneracy and closedness mean that this 2-form 
$\omega$ on $\text{Ch}(\Sigma,G)$ is a [symplectic form][7]! This is often 
called the (Atiyah-Bott-)Goldman Sympelctic structure.

---

Ok, so let's get to the main point of the post! Can we actually compute the 
value of this sympelctic form on two tangent vectors for a simple case of 
the character variety construction?

Let's look at $\text{Ch}(S^1 \times S^1, SL_2(\mathbb{C}))$. Then 
we're looking at homs from $\pi_1 (S^1 \times S^1) = \mathbb{Z}^2$ into 
$SL_2(\mathbb{C})$. So let's pick a representation $\rho$, and two 
vectors in the tangent space 
$T_\rho \text{Ch}(S^1 \times S^1, SL_2(\mathbb{C}))$ and... compute!

A choice of $\rho$ is a choice of two commuting matrices in $SL_2$, 
let's call them $A$ and $B$.

Then a tangent vector at $\rho = (A,B)$ is an element of 
$H^1(\mathbb{Z}^2, \mathfrak{sl}_2)$ where $\mathbb{Z}^2$ 
acts on $\mathfrak{sl}_2$ by the adjoint action. Of course, for 
$\mathfrak{sl}_2$ we know what this looks like very concretely! 
For a matrix $M \in \mathfrak{sl}_2$ we have 
$(1,0) \cdot M = A^{-1} M A$ and $(0,1) \cdot M = B^{-1} M B$.







[1]: https://sites.google.com/view/shane-rankin
[2]: https://sites.google.com/view/brian-collier/home
[3]: https://en.wikipedia.org/wiki/Killing_form
[4]: https://en.wikipedia.org/wiki/Uniformization_theorem
[5]: https://en.wikipedia.org/wiki/Group_cohomology
[6]: https://doi.org/10.1016/0001-8708(84)90040-9
[7]: https://en.wikipedia.org/wiki/Symplectic_manifold
