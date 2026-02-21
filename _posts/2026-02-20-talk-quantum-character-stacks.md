---
layout: post
title: Talk -- Factorization Homology and Quantum Character Stacks
tags:
  - my-talks
---

~~Today~~ Yesterday in the Representation Theory Seminar at UCR I gave a talk about 
Factorization Homology and how it lets us compute a "Quantum Character Stack".
This is all based on a great paper,
[_Integrating Quantum Groups Over Surfaces_][1] by Ben-Zvi, Brochier, and 
Jordan, which I've been reading and rereading for the last few years.
It's been a while since I've written up my thoughts after a talk, so I figured
I'd do that here to take a break from thesis writing.

I have an [old post][2] going through a talk I gave on factorization homology 
almost exactly 2 years ago back in March 2024, which might give a longer 
perspective on these ideas. I'm going to be fairly terse here because I want 
to get to the fun computation (which I'll put in a [sister post][3]), 
and I also want to write this in just a few hours.

The talk was kind of a whirlwild, haha. Especially for my audience, I needed 
to explain some basics about stacks and the rough idea of factorization 
homology before I could even *hope* to get to the actual definition of the 
quantum character stack! That's a big ask for an hour long talk, but I think 
I did alright. I asked my friend [Shane][6] how he thought it went, and he 
very graciously said that I did a good job telling a story and showing that
some could, in the abstract, compute things like this... but I didn't actually
show the audience how *they* can compute with it. I think that's a fair 
review, and is pretty consistent with my experience writing and giving the 
talk. Every professor that I talked to said that it was really good, though, 
which made me happy. Thankfully that's also pretty consistent with my experience
giving the talk, haha.

I've given other *really* dense talks before, and I remember coming off a 
bit... energetic, lol. I was pleased that I think I managed to fit a lot of 
material into this talk while still appearing somewhat collected at the 
white board. If nothing else, I didn't end the talk out of breath, haha.

Anyways, enough about my thoughts, let's get to the talk itself!

---

The beginning of the talk was meant to motivate stacks to the audience -- 
particularly some younger grad students who have asked me about them before. 
I actually have a looooong post about stacks in the works, 
where I talk about how to think of them, how to 
compute with them, and why you might care. I've had to put it on the back burner
while I work on my thesis, but hopefully some day I'll finish it up, since I 
have a lot of Thoughts™.

Given a surface $\Sigma$ and a reductive group $G$, we would like to have a 
space whose points are representations of $\pi_1 \Sigma$ valued in $G$. To 
do this we can look at $\text{Hom}(\pi_1 \Sigma, G)$ and then quotient out by 
"change of basis" given by conjugation in $G$. This has the extra benefit of 
removing the reliance of $\pi_1 \Sigma$ on a choice of base point, since 
a change of base point leads to a conjugate representation. 

There are a few things you could mean by the quotient 
$\text{Hom}(\pi_1 \Sigma, G) \big / G$. The first and most naive is to 
literally take the space and quotient out by the orbit equivalence relation.
This gives a space that isn't even Hausdorff (and it makes a nice exercise to 
see why!) so this isn't great. The more subtle approaches are 
both based on the observation that 
a function on $X \big / G$ should be the same thing as a $G$-equivariant 
function on $X$. If you haven't seen this before it's worth taking a second 
to think about why this should be true!

If you're a 20th century algebraic geometer you would define the 
<span class=defn>Character Variety</span> $\text{Ch}(\Sigma,G)$ as 
$$\text{Spec} \big (\mathcal{O}(\text{Hom}(\pi_1 \Sigma, G))^G \big )$$.
This literally means "the space whose ring of functions is $G$-equivariant 
functions on $\text{Hom}(\pi_1 \Sigma,G)$".

If you're a 21st century geometer, you're likely to de-emphasize 
$\mathbb{C}$-valued functions on $X$ (like $\mathcal{O}(X)$) for 
$\mathsf{Vect}\_\mathbb{C}$-valued functions. These assign a vector space 
to every point in a way that "varies smoothly", and the way to make this 
precise is via sheaves! So you find yourself interested in something like 
$\text{QCoh}(X)$. In this case, you might want to define the 
<span class=defn>Character Stack</span> $\underline{\text{Ch}}(\Sigma,G)$ 
to be "the space whose category of quasicoherent sheaves is $G$-equivariant 
sheaves on $\text{Hom}(\pi_1 \Sigma, G)$".

It turns out that these two spaces are generally not the same! Let's look 
at the simplest case where $\Sigma$ is just a disk. Then $\pi_1 \Sigma$ 
is the trivial group, so $\text{Hom}(\pi_1 \Sigma, G)$ is a point, with 
ring of functions given by $\mathbb{C}$. Then the $G$-action on this space 
(and this on the ring of functions) is trivial, so that the $G$-equivariant 
functions are still $\mathbb{C}$ and $\text{Ch}(\text{Disk},G) = \star$ 
is a point. In particular, its category of quasicoherent sheaves is just 
$\mathsf{Vect}$.

But what about the character *stack* $\underline{\text{Ch}}(\text{Disk},G)$?
Well now we define its category of quasicoherent sheaves to be $G$-equivariant
sheaves on $\text{Hom}(\pi_1 \Sigma, G) = \star$. So this is $\mathsf{Vect}^G$,
which is *not* $\mathsf{Vect}$! Indeed, when we say that a vector space is 
$G$-equivariant, what do we mean? We mean that $g \cdot V$ should be 
"the same as $V$" for every $g \in G$, but the notion of sameness for vector 
spaces is isomorphism! So saying that $g \cdot V$ is "the same as $V$" is 
saying we have isomorphisms $\varphi_g : g \cdot V \cong V$. Of course, 
$G$ is still acting trivially on $\text{Hom}(\pi_1 \Sigma, G) = \star$, so 
$g \cdot V = V$ and so $\varphi_g$ is an isomorphism of $V$ with itself! 
These isomorphisms are supposed to be compatible, so we find that 
$\mathsf{Vect}^G$, the category of $G$-equivariant vector spaces, is 
actually the category $\text{Rep}(G)$ of vector spaces equipped with a 
$G$-action! The space whose category of sheaves in $\text{Rep}(G)$ is 
usually called $\mathsf{B}G$, and we'll do this too[^1].

The character stack is better behaved in certain ways. It's smooth 
(in a stacky sense) while the character variety usually isn't[^2]
(this is why it's common to restrict to a "smooth locus" containing 
most representations). Moreover, the character stack for $\Sigma$ can be 
computed by gluing together the character stacks on an open cover for 
$\Sigma$, while the character variety has no such nice local-to-global 
property. The character variety also relies crucially on $G$ being 
reductive, while the character *stack* works for all groups $G$. 

It's a famous result of Goldman that the smooth locus of the character 
variety admits a symplectic structure, which quantizes to the ($G$-)skein 
algebra for $\Sigma$! It turns out the character stack also admits a 
symplectic structure (in a stacky sense) and it's natural to want to 
quantize this too. It should have something to do with skein theory... 
But what?

<br>

Let's change topic for a moment and talk about 
<span class=defn>Factorization Homology</span>. Again, we'll be much more 
terse here than we probably should be.

The notion of an $E_n$-algebra in a monoidal $k$-category $\mathcal{C}$ 
interpolates between noncommutative algebras ($E_1$) and commutative algebras 
($E_\infty$). When $n \gt k$ these stabilize so that $E_{k+1}$ algebras are 
already "fully commutative". Since we spend a lot of time working in 
$1$-categories (like $\mathsf{Set}$ and $\mathsf{Vect}$) we only really see 
the distinction between $E_1$ (noncommutative algebras) and $E_2 = E_\infty$
(commutative algebras).

However, if we work in a familiar $2$-category like $\mathsf{Cat}$ then 
we can see a bit further! Now an $E_1$-algebra is a monoidal category, 
an $E_2$-algebra is a *braided* monoidal category, and an 
$E_3 = E_\infty$-algebra is a *symmetric* monoidal category. 

At this point in the talk I said some words introducing braided monoidal 
categories and why they might be called that, but it's starting to get late so 
I think I won't say those words now. You can read all about this somewhere 
like [here][5].

Precisely, let $\mathsf{Disk}^n$ be the ($\infty$-)category whose objects 
are disjoint unions of $n$-disks and whose morphisms are (spaces of) 
smooth embeddings. Then a functor from $\mathsf{Disk}^n \to \mathcal{C}$ 
which sends disjoint union to the tensor product in $\mathcal{C}$ is 
*exactly* an $E_n$-algebra in $\mathcal{C}$!

Since $\text{Disk}^n$ is a full subcategory of the category of *all* 
$n$-manifolds with smooth embeddings, we can try to extend a functor
$\text{Disk}^n \to \mathcal{C}$ (read: an $E_n$-algebra $A$) to a functor 
$\text{Man}^n \to \mathcal{C}$. The free way to do this is via 
left Kan extension, and this is how we define factorization homology!

The "factorization homology of $M$ with coefficients in $A$", denoted by 
$\int_M A$, is defined to be the value of the left Kan extension 
$\text{Lan}(A)$ on $M$. This admits a "pointwise" formula to compute it, 
but it's much much better to use excision! Like any good homology theory, 
factorization homology has a notion of Mayer-Vietoris for computation.

At this point I included a computation of $\int_{S^1} A$ for an algebra 
$A$ in $\mathsf{Vect}$ and showed that it recovers the Hochschild homology 
$HH_0(A)$. Even though I was starting to run out of time, I couldn't help 
but mention one of my favorite facts about this too! If you view $A$ as an 
algebra in chain complexes which happens to be concentrated in degree $0$ 
then $\int_{S^1} A$ instead computes a derived enhancement, which happens to be
$CHH_\bullet(A)$ -- the entire complex of Hochschild chains! Since 
factorization homology is functorial and $S^1$ acts on itself, we get an 
induced $S^1$-action on $CHH_\bullet(A)$. An $S^1$-action on a chain complex 
is the data of a new differential on that complex, and it's natural to ask 
what differential we get on Hochschild homology from this game! Well the 
HKR theorem says that $HH_\bullet(A)$ is the algebraic de Rham complex on 
$\text{Spec}(A)$ (when $A$ is commutative), and the differential coming 
from this $S^1$-action is exactly the de Rham differential!

Again, I think I want to finish this post up quickly, so I won't include a 
copy of this computation here... I feel bad about it, though, so I'll 
say that this is done in Hiro Tanaka's fantastic series of talks starting 
[here][4].

<br>

At this point we're finally ready to bring the threads together! 

One of the main ideas in the _Integrating Quantum Groups Over Surfaces_
paper is that

$$
\text{QCoh}(\underline{\text{Ch}}(\Sigma,G)) = \int_\Sigma \text{Rep}(G)
$$

The computation I'm including in the [sister post][3] is a very explicit 
very special case of this computation where you can really get your 
hands on everything. Well... I at least sketch it, haha. You can see if you 
read that post. I originally planned to include this computation in the 
talk, but at this point I only had about 5 minutes left and I wanted to make 
sure I said something about the *quantum* character stacks in the title of 
the talk!

The point is that $\text{Rep}(G)$ is symmetric monoidal, so is an 
$E_\infty$ algebra, but we're only integrating it over the measly $2$-manifold
$\Sigma$! So we could get by with an $E_2$-algebra, which is less commutative!
Working in $\mathsf{Cat}$ this means we want a braided monoidal category,
and my favorite example is the category $\text{Rep}_q(G)$ of 
representations of a quantum group!

So now we see what to do:

Generalizing the above formula, we want to say that 

$$
\text{QCoh}(\underline{\text{Ch}}_q(\Sigma,G) = \int_\Sigma \text{Rep}_q(G)
$$

But what does this really mean?

Remember earlier when I said that the 21st century approach to geometry 
is to focus on the (derived) category of sheaves? Well just like 
Grothendieck said that every (commutative) ring should count as 
functions on a space, we might bravely hope that every dg-category 
should be sheaves on a space! It turns out that one can push this idea 
*very* far, and this is one of the modern approaches to 
<span class=defn>Noncommutative Geometry</span>. See, for example, 
Kontsevich's fantastic article [_Geometry in dg-Categories_][7] 
from the equally fantastic book _New Spaces in Mathematics_ -- 
every chapter is a banger.

This "noncommutative" perspective on geometry is what will let us make 
sense of the quantum character stack as a geometric object, even though
we really only have access to what its category of sheaves should be.

<br>

At this point I basically had to stop the talk, but I rushed to say a few 
last minute things that I hoped would convince the audience that this is 
something that you *can* get your hands on.

Obviously I mentioned Juliet Cooke's [thesis][8], where she shows that 
there's a concrete <span class=defn>skein category</span> defined in terms 
of tangles in the thickened $\Sigma \times I$ modulo local relations coming 
from the quantum group $G_q$. This should be compared to the classical skein 
*algebra* which is defined in terms of links in $\Sigma \times I$ modulo 
those same local relations. It turns out that this skein category presents 
the quantum character stack in the sense that the factorization homology 
$\int_\Sigma \text{Rep}_q(G)$ is the cocompletion of the skein category.

Also, the Barr-Beck yoga says that any category which looks like a category 
of algebras should be one, and indeed there's an algebra object[^3] 
$$A_\Sigma$$ in $$\text{Rep}_q(G)$$ so that $$\int_\Sigma \text{Rep}_q(G)$$
is "just" a category of modules over $$A_\Sigma$$ 
(internal to $$\text{Rep}_q(G)$$, of course) and from a combinatorial 
presentation of $\Sigma$ Ben-Zvi, Brochier, and Jordan are able to compute 
explicit presentations of this internal algebra!

---

Alright, it's a quick epilogue today. I would normally put the 
title, abstract, and slides here, but because it was an internal seminar 
and I gave a chalk talk I actually have none of those things, haha[^4]. 

Thanks for hanging out, everyone! It feels good to write about something 
that's not my thesis, and I'm excited to go and write the sister post 
with this computation! That will have to wait a bit, though, since now 
it's dinner time (I succeeded in writing this post in about three hours)
and then I'm going climbing with some friends.

Stay safe, and we'll chat soon ^_^.

---

[1]: https://www.doi.org/10.1112/topo.12072
[2]: /2024/03/27/ams-sectional-talk-fh
[3]: /2026/02/20/computing-quantum-character-stacks
[4]: https://www.youtube.com/watch?v=yeTngpqaAmk
[5]: https://ncatlab.org/nlab/show/braided+monoidal+category
[6]: https://sites.google.com/view/shane-rankin
[7]: https://doi.org/10.1017/9781108854429.014
[8]: https://julietcooke.net/CookeThesis.pdf

[^1]:
    You might be familiar with a different notion of $\mathsf{B}G$ from 
    homotopy theory. In that world you take a contractible space with a 
    free $G$-action and then quotient by it to get a "classifying space"
    where maps from $X$ to $\mathsf{B}G$ are principal $G$-bundles on $X$.

    Up to homotopy a contractible space is a point, so this homotopy-theoretic 
    $\mathsf{B}G$ is also "a point quotiented by $G$" just like our 
    algebro-geometric example. Much of the same intuition goes into thinking 
    about these two notions of $\mathsf{B}G$, but you have to remember that 
    their implementations are different!

    Since a lot of my readers are familiar with topos theory, I'll say here 
    that the category $G\text{-}\mathsf{Set}$ is a topos, and we often 
    denote it by $\mathsf{B}G$ for this same reason. Indeed, the topos
    $\mathsf{B}G$ thinks its category of vector spaces is $\text{Rep}(G)$
    so this is secretly the algebro-geometric example again.

[^2]:
    It's a fun (but possibly tricky) exercise to compute the dimension of 
    the tangent space at a generic point, then at the trivial representation.
    Remember that the tangent space to $\text{Ch}(\Sigma,G)$ at a 
    representation $\rho : \pi_1 \Sigma \to G$ is given by the group 
    cohomology 

    $$T_\rho \text{Ch}(\Sigma,G) = H^1(\pi_1 \Sigma, \mathfrak{g})$$ 

    where $\mathfrak{g}$ is a $\pi_1 \Sigma$-module by composing 
    $\rho$ with the adjoint action of $G$ on $\mathfrak{g}$. 

    For example let's take $\Sigma$ to be a punctured torus, whose fundamental 
    group is free on two generators $a$ and $b$, and let's take $G$ to be 
    $SL_2(\mathbb{C})$. Then a point in $\text{Ch}(\Sigma,G)$ is a 
    representation $\rho$ up to conjugation, is a pair of matrices 
    $A,B \in SL_2$ up to simultaneous conjugation (these are the images of 
    $a$ and $b$ under $\rho$).

    Now $\mathfrak{g} = \mathfrak{sl}_2(\mathbb{C})$ is the space of 
    $2 \times 2$ trace $0$ matrices, and the adjoint action of $G$ on 
    $\mathfrak{g}$ is conjugation! So $\mathfrak{sl}_2$ becomes a $F_2$-module
    (read: a $\pi_1 \Sigma$-module) by $a \cdot M = A^{-1} M A$ and 
    $b \cdot M = B^{-1} M B$. From here you can compute the group cohomology 
    $H^1(F_2, \mathfrak{sl}_2)$ explicitly, and you'll see that the generic 
    dimension is not the dimension when $A = B = \text{Id}$.

[^3]:
    In fact this algebra comes as a kind of $\text{Rep}_q(G)$-valued 
    endomorphism object of the quantum structure sheaf... But I didn't 
    have time to say any of that at the end of the talk. See the 
    _Integrating Quantum Groups Over Surfaces_ paper for more.

[^4]:
    Actually, writing this has reminded me that I never wrote a talk debrief 
    for my JMM talk about Fukaya categories and my thesis work... Maybe I'll 
    write a *very* belated post about that, especially since it *does* have a 
    title, an abstract, and slides!
    
    We'll see, though. I've been ridiculously busy lately.
