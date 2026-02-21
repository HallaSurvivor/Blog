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
\boxtimes \left ( \bigoplus_\mathbb{Z} \mathsf{Vect} \right )$
on 
$\left ( \bigoplus_\mathbb{Z} \mathsf{Vect} \right )$ is by 

$$(V_n \boxtimes V_m) \cdot V_i \simeq V_n \otimes V_i \otimes V_m$$

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

We can do this by choosing $n = -(m+j)$, which uses up one of our two 
degrees of freedom. Of course, we can still freely choose $m$, which gives us
*more isomorphisms*! When $j=0$ for simplicity (or, given the above discussion,
without loss of generality), we get isomorphisms

$$
(V_n \otimes V_i \otimes V_{-n}) \boxtimes V_0 
\cong 
V_i \boxtimes (V_{-n} \otimes V_0 \otimes V_n)
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
showed me how to do this when I talked to him about this yesterday. Obviously,
any mistakes come from my incorrectly remembering some details, or incorrectly
filling in others.

We compute the factorization homology side again... But this 
computation will work for any group $G$, and we'll write it in 
that level of generality.

As before, we define $\underline{\text{Ch}}(\text{Annulus}, G)$ to be 
$\text{Hom}(\mathbb{Z}, G) \big / G$, which is $G \big / G$ -- the quotient of 
$G$ by the conjugation action on itself. We want to compare the category of 
quasicoherent sheaves on this stack to the factorization homology 
$\int_{\text{Annulus}} \text{Rep}(G)$.


As before, excision tells us that we can compute 
$\int_{\text{Annulus}} \text{Rep}(G)$ by the relative tensor product

$$
\text{Rep}(G)^\text{op} 
\boxtimes_{\text{Rep}(G)^\text{op} \boxtimes \text{Rep}(G)}
\text{Rep}(G) 
$$

but recall that $\text{Rep}(G) \simeq \text{QCoh}(\mathsf{B}G)$, so we can 
rewrite this as 

$$
\begin{aligned}
\text{QCoh}(\mathsf{B}G) 
\boxtimes_{
\text{QCoh}(\mathsf{B}G) \boxtimes \text{QCoh}(\mathsf{B}G)^\text{op}}
\text{QCoh}(\mathsf{B}G)^\text{op}
&\overset{(1)}{\simeq}
\text{QCoh}(\mathsf{B}G \times_{\mathsf{B}G \times \mathsf{B}G^\text{op}} \mathsf{B}G^\text{op}) \\
&\overset{(2)}{\simeq}
\text{QCoh}(G \big \backslash (G \times G^\text{op}) \big / G) \\
&\overset{(3)}{\simeq}
\text{QCoh}(G \big / G)
\end{aligned}
$$

In step $1$ we use the fact that the (relative) tensor product of sheaves 
corresponds to sheaves on the pullback. In step $2$ we compute the pullback
of classifying spaces. Indeed, if we wanted the (homotopy) pullback 
$\star \times_{\mathsf{B}(G \times G^\text{op})} \star$ (remember that $\mathsf{B}$ 
preserves products) this would just be the loopspace of $\mathsf{B}(G \times G^\text{op})$,
which is $G \times G^\text{op}$. But we don't have $\star$, we actually have 
$\mathsf{B}G = \star \big / G$. So we have one left $G$ action 
(from the $\mathsf{B}G$) and one right $G$ action 
(from the $\mathsf{B}G^\text{op}$) and we end up with the double quotient space
$G \big \backslash (G \times G^\text{op}) \big / G$... Apparently if you work
through the details both of these $G$ actions are diagonal, by left/right 
multiplication respectively, but I haven't tried to understand why that is.
I also don't entirely know that I'm keeping track of the "op"s correctly, 
and while we're at it I'm fuzzy on the details of this "act like we're 
pulling back to a pair of points and then quotient by the $G$ actions after"
stuff too... I'm sure it's formal, and I just haven't gotten familiar with 
the rules for symbol pushing yet, so let't not worry about it. 

Regardless, we find ourselves with 
$G \big \backslash (G \times G^\text{op}) \big / G$ where the action is by 
$h \cdot (g_1, g_2) \cdot k = (h g_1 k, k g_2 h)$. Then we can use 
one degree of symmetry by taking $k = h^{-1} g_2^{-1}$. This tells us that 
in the quotient we should identify $(g_1,g_2)$ with $(h g_1 g_2^{-1} h^{-1}, e)$.
Note that the multiplication order is kind of funny because of all the "op"s 
floating around. Of course we have another degree of freedom to use by 
choosing $h$, and as before this gives us an action of $G$ on itself by 
conjugation! So altogether we see that 
$G \big \backslash (G \times G^\text{op} ) \big / G$ is equivalent to 
$G \big / G$, the quotient of $G$ by the conjugation action! But this is 
exactly what we expect $\underline{\text{Ch}}(\text{Annulus}, G)$ to be!

---

Ok, thanks for reading all! This was a very quick-and-dirty post, and 
I'm not sure I got the details right with the objectwise argument in the 
first half, or with the "op"s in the second half. I would normally spend 
a few days (or weeks) reading up on stacks, properties of $\text{QCoh}$, 
this Fourier/Cartier/Pontryagin/Whatever duality that I was using, and 
check that everything really does work the way I think it does. But I 
want to get this out at the same time as the main post. Plus
I've already had to put two posts on the backburner which 
are probably mostly right but need some details checked (one is about the 
stack semantics for the internal logic of (1-)topoi, and one is an explicit 
computation of the goldman bracket for character varieties), and I really don't 
want a third post in that limbo space. This could easily become one of many 
technical computations stuck in my drafts, but maybe it's nice to share some 
quick-and-dirty computations too, since I do a lot of those in the privacy 
of my own home, haha. A lot of math looks polished once it gets presented, but 
at least for me the early days of learning a subject often look like this.

Stay safe everyone, and stay warm! 


[1]: /2026/02/20/talk-quantum-character-stacks.html
[2]: https://sites.google.com/view/tomgannon

