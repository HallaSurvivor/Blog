---
layout: post
title: An Overly Explicit Computation with Character Stacks
tags:
  - 
---

In the [main post][1] I go over a talk I gave today explaining how 
factorization homology relates to (quantum) character stacks. In this 
post I want to do a sample computation which gives some justification that 
the main theorem from that talk (which is *not* mine) actually does work!

Recall from that blog post that we can compute the category of sheaves on 
the character stack $\underline{\text{Ch}}(\Sigma,G)$ by integrating 
$\mathsf{B}G$ over $\Sigma$ in the sense of factorization homology:

$$
\text{QCoh}(\underline{\text{Ch}}(\Sigma,G)) \simeq \int_\Sigma \text{Rep}(G)
$$

Let's take a simple surface (like the annulus) and a simple group (like 
$GL_1 = \mathbb{C}^\times$) and just... check!

There's a lot of problems with what I'm doing here... For one, I'm not 
actually sure if I'm working $\infty$-categorically or $1$-categorically!
It's possible that when I say $\text{QCoh}$ and $\text{Vect}$ and what not 
I really mean the *derived* category of quasicoherent sheaves and 
*chain complexes*, etc... that seems likely to me since I'm using a lot of 
formal gluing and duality statements, which tend to work better in the 
derived world... I really need to sit down and learn enough algebraic 
geometry to appreciate the differences between the derived and underived 
stories, but unfortunately that will have to wait for another day. 

Another problem is that I'm only going to naively check that the objects 
of these categories seem to agree. It's almost certainly possible to work 
with the arrows by hand as well and check that they agree, but I don't have 
time to do that right now.
Plus, in case we *are* working in a derived setting, I *definitely* don't have 
time to check the infinitely many higher cells! 

So with these caveats,
I'll follow in the footsteps of Jim Dolan and just press on doing computations 
to see if something meaningful pops out.

---

Let's start with the left hand side. 

When $\Sigma$ is the annulus and $G$ is $\mathbb{C}^\times$ we see that 

$$
\begin{aligned}
\underline{\text{Ch}}(\Sigma,G) 
&\simeq \text{Hom}(\pi_1 \Sigma, G) \big / G \\
&\simeq \text{Hom}(\mathbb{Z}, \mathbb{C}^\times) \big / \mathbb{C}^\times \\
&\simeq \mathbb{C}^\times \big / \mathbb{C}^\times \\
&\simeq \mathbb{C}^\times \times \mathsf{B}\mathbb{C}^\times
\end{aligned}
$$

The last step is because here $\mathbb{C}^\times$ is acting on itself by 
conjugation -- which is the trivial action since $\mathbb{C}^\times$ is 
abelian. We know a point with the trivial action gives rise to a 
$\mathsf{B}\mathbb{C}^\times$ and how we have $\mathbb{C}^\times$ many 
such points, so that we get a $\mathbb{C}^\times \times \mathsf{B}\mathbb{C}^\times$
in total.

So now we want to compute quasicoherent sheaves on this space, but
products on the geometric side are coproducts (read: tensor products) 
on the algebraic side so we get

$$
\begin{aligned}
\text{QCoh}(\underline{\text{Ch}}(\Sigma,G))
&\simeq \text{QCoh}(\mathbb{C}^\times \times \mathsf{B}\mathbb{C}^\times) \\
&\simeq \text{QCoh}(\mathbb{C}^\times) \otimes \text{QCoh}(\mathsf{B}\mathbb{C}^\times) \\
&\simeq \text{QCoh}(\mathbb{C}^\times) \otimes \text{Rep}(\mathbb{C}^\times) \\
&\simeq \text{Rep}(\mathbb{Z}) \otimes \bigoplus_\mathbb{Z} \mathsf{Vect}
\end{aligned}
$$

In the last step we've used the fact that 
$\mathbb{C}^\times = \text{Spec}(\mathbb{C}[t^\pm])$ so that its
category of sheaves is just modules over $\mathbb{C}[t^\pm]$, which we 
recognize as the group algebra of $\mathbb{Z}$. So such a module is 
exactly a vector space with an action of $\mathbb{Z}$. In fact this is 
some kind of Fourier duality, where sheaves on $\mathbb{C}^\times$ 
(some kind of circle) are interchanged with representations of $\mathbb{Z}$
(the dual group). 

We've also used the fact that 
$\text{QCoh}(\mathsf{B}G)$ is $\text{Rep}(G)$, where for us 
$G = \mathbb{C}^\times$. Moreover, by Fourier duality again, 
$\text{Rep}(\mathbb{C}^\times)$ is the same as $\text{QCoh}(\mathbb{Z})$,
but a sheaf on a discrete set like $\mathbb{Z}$ is just a choice of vector 
space above each point, so that we get the category of 
$\mathbb{Z}$-graded vector spaces.

Now of course we would expect tensor products to distribute over sums, 
and we know that $\mathsf{Vect}$ is the monoidal unit, so that at the end of 
the day we've computed

$$
\text{QCoh}(\underline{\text{Ch}}(\Sigma,G))
\simeq
\bigoplus_\mathbb{Z} \text{Rep}(\mathbb{Z})
$$

the category of quasicoherent sheaves on the character stack is 
the category of $\mathbb{Z}$-graded $\mathbb{Z}$-modules! Which 
almost sounds like the kind of thing one can understand and compute with!

---

Next, the right hand side.

We compute factorization homology by excision -- by cutting a surface into 
disks glued along collared embeddings and using the fact that the factorization 
homology of a disk with coefficients in $\mathcal{A}$ is just $\mathcal{A}$ 
again.

So we decompose the annulus into disks glued along their collared boundary

<p style="text-align:center;">
<img src="/assets/images/computing-quantum-character-stacks/annulus-decomp.png" width="50%">
</p>

and then we can inductively compute the factorization homology by a 
Mayer-Vietoris style argument. Concretely, say you have an $E_2$-algebra 
$\mathcal{A}$ and you're interested in computing factorization homology over 
the annulus. We want to do this in an oriented sense, and out of laziness 
I'm going to draw the annulus as though it's a circle. Then we get 

<p style="text-align:center;">
<img src="/assets/images/computing-quantum-character-stacks/hochschild-computation.png" width="50%">
</p>

where as usual I'm writing $\mathcal{A}^\text{op}$ to mean $\mathcal{A}$ with the 
reversed algebra structure: $a \cdot^\text{op} b$ is defined to be $b \cdot a$.
This makes the computation look more like the Hochschild homology computation
it is, but could possibly be confusing since we're about to work in the case 
where $\mathcal{A} = \text{Rep}(\mathbb{C}^\times)$ is a monoidal category!
So just remember that in what follows $\text{Rep}(\mathbb{C}^\times)^\text{op}$
doesn't mean the opposite category! It means the same category with the 
definition of $\otimes$ flipped -- $M \otimes^\text{op} N$ is $N \otimes M$.

Then for us, we find ourselves wanting to compute

$$
\text{Rep}(\mathbb{C}^\times)^\text{op} 
\boxtimes_{\text{Rep}(\mathbb{C}^\times)^\text{op} \boxtimes \text{Rep}(\mathbb{C}^\times)}
\text{Rep}(\mathbb{C}^\times) 
$$

Here I'm switching over to $\boxtimes$ for the tensor product *of* categories
in order to keep it straight with the monoidal product $\otimes$ 
*inside a particular* category later.

Now again Fourier duality makes this look less scary, since we know that 
$\text{Rep}(\mathbb{C}^\times) \simeq \bigoplus_\mathbb{Z} \mathsf{Vect}$! 
We need to know the monoidal structure now, and it will come as no surprise 
that we swap the "pointwise" monoidal structure on 
$\text{Rep}(\mathbb{C}^\times)$ with the "convolution" monoidal structure 
on $\bigoplus_\mathbb{Z} \mathsf{Vect}$!

To see why, consider the one dimensional $\mathbb{C}^\times$ representation 
$V_n$ where $z \in \mathbb{C}^\times$ acts by scalar multiplication by $z^n$.
This is the generator for the grade $n$ copy of of $\mathsf{Vect}$. Now 
what is $V_n \otimes V_m$ supposed to be? Well $z$ acts diagonally so that 
$$
z \cdot (v_n \otimes v_m) = (z^n v_n) \otimes (z^m v_m) = z^{n+m} (v_n \otimes v_m)
$$
and $V_n \otimes V_m$ is $V_{n+m}$. 

So cashing out the $\text{Rep}(\mathbb{C}^\times)$ for 
$\bigoplus_\mathbb{Z} \mathsf{Vect}$ everywhere we get

$$
\left ( \bigoplus_\mathbb{Z} \mathsf{Vect} \right )^\text{op}
\boxtimes_{
\left ( \bigoplus_\mathbb{Z} \mathsf{Vect} \right )^\text{op}
\boxtimes
\left ( \bigoplus_\mathbb{Z} \mathsf{Vect} \right )
}
\left ( \bigoplus_\mathbb{Z} \mathsf{Vect} \right )
$$

Where the action (on objects) of 
$\left ( \bigoplus_\mathbb{Z} \mathsf{Vect} \right )^\text{op} 
\otimes \left ( \bigoplus_\mathbb{Z} \mathsf{Vect} \right )$
on 
$\left ( \bigoplus_\mathbb{Z} \mathsf{Vect} \right )$ is by 

$$(V_n \otimes V_m) \cdot V_i \simeq V_n \otimes V_i \otimes V_m$$

just like the bimodule action for the ordinary Hochschild homology! So,
using the presentation for the relative tensor product of categories, 
we see that our factorization homology is generated by objects of the form

$$V_i \boxtimes V_j$$

where we add in isomorphisms 

$$
(V_n \otimes V_i \otimes V_m) \boxtimes V_j 
\cong
V_i \boxtimes (V_m \otimes V_j \otimes V_n)
$$

From this description it's clear that, up to isomorphism, 
we can always make the $V_j$ into $V_0$ so that a normal form for objects 
of our category is 

$$V_i \boxtimes V_0$$

Of course, we have *more isomorphisms*! Indeed when $n = -m$, we get an 
isomorphism 

$$
(V_n \otimes V_i \otimes V_{-n}) \boxtimes V_0 
\cong 
V_i \boxtimes V_{-n} \otimes V_n
\cong
V_i \boxtimes V_0
$$

So we have integer many generating objects $V_i \boxtimes V_0$,
each of which carries integer many automorphisms given by conjugating 
by $V_n$ for $n \in \mathbb{Z}$... Moreover, these automorphisms are compatible
since $V_n \otimes V_m \cong V_{n+m}$ so that conjugating by $V_n$ and then 
$V_m$ is the same as conjugating by $V_{n+m}$. 

Thus we have $\mathbb{Z}$-many generating objects, each of which carries a 
$\mathbb{Z}$-action!

So, at least at the level of objects, it's believable that when $\Sigma$ 
is the annulus that 
$\int_\Sigma \text{Rep}(\mathbb{C}^\times)$ is $\mathbb{Z}$-graded 
$\mathbb{Z}$-modules!

Of course, this is exactly what we were expecting, 
since if you recall from the previous section we computed the same thing for 
$\text{QCoh}(\underline{\text{Ch}}(\Sigma,\mathbb{C}^\times))$!

---

Lastly, let's say what the "correct" way to do this is. [Tom Gannon][2]
showed me how to do this when I talked to him about this yesterday.

We compute

TODO: put Tom's proof here


[1]: /2026/02/19/talk-quantum-character-stacks.html
[2]: https://sites.google.com/view/tomgannon
