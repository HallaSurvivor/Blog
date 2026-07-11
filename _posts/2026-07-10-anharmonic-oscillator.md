---
layout: post
title: The Quartic Oscillator is Provably Not Solvable!
tags:
  - 
---

First things first, I just passed my defense! I still have to format my 
thesis and officially hand it in, but the last majorly stressful part of 
my PhD is done! 🎉🎉🎉 I want to thank everybody who has loved me over these
last few years and kept me sane. Of course, now that I'm done with all this 
thesis writing, I obviously want to spend some time on... *different writing*?
Look, for some reason writing blog posts is "fun" and something I've had 
to put off for the last few months while writing my thesis was "work" and 
it was super draining to write... I'm not sure exactly what's wrong with me,
but it works pretty well for me so let's not question it, haha.

My thesis work is in Hall algebras and Fukaya categories, and I think I'm 
more well known online for my posts on topos theory and constructive math, 
but recently I've been having a *lot* of fun learning physics! Obviously 
part of this is just because it's extremely interesting -- years ago 
John Baez told me that I would love physics if I would only give it a chance,
and at the time I thought this was his bias as a physicist, but now I know 
that he was completely correct, haha. Part of this is because I've been really 
busy working on my thesis, and it's a lot easier to learn basic physics than
it is to learn the kind of math I want to learn. So counterintuitively,
learning physics has been a rather relaxing activity recently[^1]. Oh, and 
of course ideas from physics have been extremely influential in a lot of 
subjects that I've been drawn to in the last few years. [Mirror Symmetry][1],
of course, plus [Geometric Langlands][2], [Quantization][3], 
[(Topological) Quantum Computing][4], and lots of things that I don't 
currently know a ton about, but that I would love to better understand 
some day (like [Cluster Algebras][5]). 
Eventually I want to work my way up to supersymmetric quantum field 
theories, to try and understand TQFTs, mirror symmetry, etc. through 
that lens. But for now
I'm thinking a lot about differential equations, Fourier theory, and 
basic quantum mechanics.

Now, while reading about all this, I came across a lot of people saying that 
the "quartic oscillator" is not exactly solvable. This is interesting, 
since the [harmonic oscillator][6] is one of the most central examples in 
physics, and it's my impression that we understand it very very well. In 
the harmonic case, our potential looks like $V(x) = x^2$. In the quartic 
case, our potential looks like $V(x) = x^4$. But this makes all the difference!

Even though I'm *learning* a bunch of physics right now, I'm still a 
logician/algebraist at heart, and so I naturally asked maybe the least 
physics-y question possible when shown this example:

<div class=boxed markdown=1>
Can one make precise the statement that the quartic oscillator 
is not analytically solvable?
</div>

It seems like the answer is *yes*, and the proof goes through 
[Differential Galois Theory][7]! Just like (algebraic) Galois theory 
relates solvability of a (discrete) group of symmetries of roots to the ability 
to express those roots as iterated radicals, *differential* Galois theory
relates solvability of a (Lie) group of symmetries of solutions to a 
differential equation to the ability to express those solutions in terms of 
antiderivatives of functions we already know.

Apparently one can show that the differential Galois group for the quartic 
oscillator $y'' = (x^4 - E)y$ is $\text{SL}(2,\mathbb{C})$ -- a Lie group 
which is famously *not* solvable! This tells us that there is no way to 
express the solutions to this equation as "Liouvillian functions"... 
I spent a few hours while writing this post trying to find 
this example computed in a way that I can understand, but I didn't have 
much luck. Normally I would spend a few days/weeks/months trying to figure it 
out myself before writing this up, but I really want to have a post announcing 
my 

I thought a little bit about differential Galois theory when I was 
younger, and actually there have been *lots* of times I've thought about 
writing a blog post about it. This seems like as good an excuse as any, 
so let's get to it!

---

First, remember the story in "classical" Galois theory. We have a field $k$
and a polynomial $f \in k[X]$. We want to understand the roots of $f$ 
(that is, the solutions to the _algebraic equation_ $f(X)=0$), and oftentimes 
these roots live in an _extension_ $K$ of $k$. As a simple example, consider 
the polynomial $x^2 - 2 \in \mathbb{Q}[x]$. The solutions to this equation, 
$\pm \sqrt{2}$, live in a larger field $\mathbb{Q}(\sqrt{2})$.

Now, put yourself into the shoes of a similarly "classical" mathematician.
The explicit numbers that feel comfortable are things like 
$$\sqrt[3]{2 - \sqrt{\frac{3}{2}}}$$. For every quadratic, cubic, and quartic 
polynomial $f$, you can express the solutions to $f(X)=0$ in terms of 
these kinds of nested $n$th roots and the coefficients of $f$. At this point 
it's natural to ask if we can *always* write the solutions to a polynomial
in this form.

Well, Galois comes around[^2] in $1830$ (when he was only $18$!) 
and says *no*! Indeed, one can show that 
the roots of the polynomial $f(X) = X^5 - 4x + 2 \in \mathbb{Q}[X]$ cannot 
be written in terms of nested radicals! Moreover, the argument is fantastic!

Consider the splitting field $K \supset \mathbb{Q}$ we get by adjoining 
new elements $\theta_1, \ldots, \theta_5$ to $\mathbb{Q}$ (which should be 
thought of as formal symbols giving the different roots of $f$, just like 
$\pm\sqrt{2}$ is a formal symbol giving  roots of $X^2-2$). Then we can ask 
about *symmetries* among the roots. For instance, the roots of $X^n - a$
are radially symmetric about the origin in $\mathbb{C}$, and you can imagine 
"clicking" the roots one notch to the left -- 
$$\sqrt[n]{a}\zeta^i \mapsto \sqrt[n]{a}\zeta^{i+1}$$. 

<p style="text-align:center;">
<img src="/assets/images/anharmonic-oscillator/cyclic-roots.png" width="50%">
</p>

In fact, you can probably imagine *lots* of permutations of the roots
($n!$ many, if you have a good imagination), but we're only interested in 
those permutations $\sigma$ which 
"preserve the algebraic structure" in the sense that a polynomial 
$P(\theta_1, \ldots, \theta_n) = 0$ if and only if 
$P(\sigma \theta_1, \ldots, \sigma \theta_n) = 0$. 

Under mild conditions[^3], one can show that for the roots of $X^n - a$ 
the "click to the left" symmetry generates *all* of these special 
symmetries, and so we say that the *Galois Group* of $X^n - a$ is 
$\mathbb{Z}/n$.

So now consider a more complicated polynomial $g(X)$ whose solutions can be 
written in terms of nested radicals. Then we can build a field up in stages

$$\mathbb{Q} \subseteq K_1 \subseteq K_2 \cdots \subseteq K_n$$

where at each stage we add another "layer" of radicals necessary for building
the solutions to $g$. So, for example, if our earlier example 
$$\sqrt[3]{2 - \sqrt{\frac{3}{2}}}$$ is a root of $g$, then we would have 
extensions looking something like

$$
\mathbb{Q} 
\subseteq 
\mathbb{Q} \left (\sqrt{\frac{3}{2}} \right ) 
\subseteq
\mathbb{Q} \left ( \sqrt{\frac{3}{2}}, \sqrt[3]{2 - \sqrt{\frac{3}{2}}} \right)
$$

where getting to the first field involves adding roots of 
$$X^2 - \frac{3}{2} \in \mathbb{Q}[X]$$
and getting to the second field involves adding roots of 
$$X^2 - \left ( 2 - \sqrt{\frac{3}{2}} \right ) \in 
\mathbb{Q} \left (\sqrt{\frac{3}{2}} \right )[X]$$.

So in this way, the symmetry group of the roots of $g(X)$ can be understood 
in terms of the symmetry groups of each stage, which we just showed are 
all of the form $\mathbb{Z}/n$. Because of this connection to *solving*
polynomials, a group that can be built by repeatedly extending cyclic groups
is called [*Solvable*][10]. 

Conversely, if we can show that the symmetry group of the roots of $f$ is 
_not_ solvable, then we'll have shown that the roots of $f$ can *not* be 
expressed in terms of nested radicals! 

One then computes the Galois group of, say, $$X^5 - 4X + 2$$ to be 
the symmetric group $\mathfrak{S}_5$, by showing that it contains a $5$-cycle
rotating the roots as before, as well as a $2$-cycle given by complex 
conjugation. Next one shows that $\mathfrak{S}_5$ is not solvable, since one 
can just... compute all its quotients with a finite amount of work.
For more details see [here][11].

---

Now we want to play exactly the same game, but with *differential* equations,
rather than *algebraic* ones!

Instead of a structure with $(0,1,+,-,\times)$, which allows us to define 
polynomial equations (with constant parameters for coefficients), we now have 
a structure with $(0,1,+,-,\times,\partial)$ which is both a field for the 
first part of the stricture and satisfies the linearity and product rules we 
expect: 

- $\partial(x+y) = \partial(x) + \partial(y)$
- $\partial(xy) = \partial(x)y + x\partial(y)$

The only example we'll consider is $\mathbb{C}(x)$, the 
[rational function field][12] with its usual notion of 
differentiation... As well as extensions of this field by solutions to 
various differential equations. See also [here][13] for more examples.

Now instead of solutions to polynomials, our definable sets are solutions to 
differential equations:

$$\partial^2 y + a y^2 \partial y + b y = 0$$

This obviously makes the theory extremely difficult, but as usual, the 
situation improves for *linear* differential equations. This is the subject of 
[Picard-Vessiot Theory][14], which was developed in the $1880$s, a short 
$50$ years after Galois's work.

Before we thought about the kinds of numbers that "classical" 
mathematicians would be comfortable with. Now let's think about what kinds of 
_functions_ one might be comfortable with. Certainly all 
[algebraic functions][15] are fine. These are functions satisfying 
*algebraic* equations, as were studied in Galois's day. So for instance 
if you know that $f(x)$ satisfies the equation 

$$a_n(x) f^n(x) + a_{n-1}(x) f^{n-1}(x) + \cdots + a_1(x)f(x) + a_0(x)$$

for known functions $a_i(x)$, that's as good as solved nowadays. For instance,
functions like $f(x) = \sqrt{\frac{1 - \cos(x)}{e^x}}$, which satisfy the 
equation $e^x f^2 + \cos(x) - 1 = 0$ are as good as known, even if we might 
not be able to explicitly write down a closed form for $f$.

Next, antiderivatives should be considered acceptable. After all, we're 
happy to use the error function 
$\frac{2}{\sqrt{\pi}} \int_{-\infty}^x e^{-t^2} \mathrm{d}t$ whenever we want,
and of course [WKB Theory][16], which physicists love, is full of 
functions that look like $e^{\int_0^x \sqrt{Q(t)} \mathrm{d}t}$, so we should 
also be allowed to compose existing functions, which possibly came themselves 
from taking antiderivatives.

Just like solvability by radicals is all about the algebraic equations we 
can solve by repeatedly using $n$th roots, a [Liouvillian Function][17] is 
a solution to a *differential equation* which one can understand by repeatedly
taking roots of algebraic equations, antiderivatives, and composition.

Now, in the case of an order $n$ linear differential equation, we have 
$n$-many linearly independent solutions, and a _Picard-Vessiot Extension_ is 
the differential field you get by adding 
these $n$-many solutions $y_1, \ldots, y_n$ to your base field 
(and closing under the differential field operations, so something like 
$x^2 y_2 + \partial (y_1 y_2^2)$ is allowed). 

In the classical Galois case we had a symmetric group $\mathfrak{S}_n$ 
worth of ways to permute the roots. Now in the differential case we have a 
$\text{GL}(n,\mathbb{C})$ worth! Indeed, if $\vec{y}$ is a vector of linearly 
independent solutions and $M$ is an invertible matrix (with scalar entries) 
then $M\vec{y}$ is a new vector of linearly independent solutions!

So now instead of looking at the subgroup of $\mathfrak{S}_n$ preserving all
the algebraic structure, we look at the subgroup of $\text{GL}(n,\mathbb{C})$ 
preserving the differential structure in the sense that for every 
differential polynomial 
$Q(\vec{y}, \vec{y}', \vec{y}'', \ldots, \vec{y}^{(N)})$
we have $Q(\vec{y}, \vec{y}', \ldots, \vec{y}^{(N)}) = 0$ if and only if 
$Q(M \vec{y}, M \vec{y}', \ldots, M \vec{y}^{(N)}) = 0$.

We call this (Zariski closed) subgroup of $\text{GL}(n,\mathbb{C})$ the 
*Differential Galois Group* $\text{Gal}_\partial$.

As in classical Galois theory, given an intermediate differential extension 
$F \subseteq K \subseteq L$ we can look at the (Zariski closed) subgroup of 
$$\text{Gal}_\partial(L/F)$$ which fixes $K$ pointwise, and given a closed 
subgroup we can look at its fixed points. These maps give a bijection between 
intermediate differential extensions and closed subgroups of 
$$\text{Gal}_\partial$$. Again, as in the classical case, the *normal* 
closed subgroups $N$ of $$\text{Gal}_\partial$$ are in bijection with the 
intermediate differential fields that are themselves Picard-Vessiot, 
and as in the classical case the quotient $$\text{Gal}_\partial \big / N$$ is 
canonically isomorphic to the differential Galois group of this intermediate
extension.

With all these analogies in mind, the reader will not be surprised to see 

<div class=boxed markdown=1>
A Picard-Vessiot differential field extension 
$F \subseteq F(y_1, \ldots, y_n)$ is Liovillian, in the sense that each of the 
$y_i$s are Liouvillian, if and only if the identity component 
$$\text{Gal}_\delta(F(\vec{y}),F)^\circ$$ is [solvable][18] 
(in the sense that its Lie algebra is).
</div>

So now we know how to check that the solutions to a (linear) 
differential equation are "not expressible" in a simple way! All we have to 
do is check that the differential Galois group of the differential equation 
is not solvable!

Moreover, for second order homogeneous equations ODEs $y'' = r(x) y$ this is 
effective! Kovacic's algorithm will take $r(x)$ as an input and tell you 
whether the differential Galois group of $y'' = ry$ is solvable or not!

Normally I like to spend more time with references before suggesting them, but
today I'm really trying to get this out quickly, so I'll mention all of the 
books that I flipped through while writing this section. 
Beukers's [_Differential Galois Theory_][19] is a really good (short!) 
chapter in a book that I think I would enjoy reading. There's also 
Singer and Van der Put's 
[_Galois Theory of Linear Differential Equations_][20], which is much longer,
but covers much more ground. Lastly, while I didn't actually get a chance to 
look at it tonight, Sauloy's 
[_Differential Galois Theory through Riemann-Hilbert Correspondence: An Elementary Introduction_][21]
sounds *extremely* up my alley, both because it discusses all these ideas 
in the context of the [Riemann-Hilbert Correspondence][22] (which is central 
in a *lot* of subjects I'm growing interested in) but also because it promises
to be "an elementary introduction", which is great for dummies like me!

---

Ok, let's get to the quartic oscillator!
This is a fancy physics name for the differential equation

$$y'' = (x^4 - E)y$$

where $E$ is a number, representing the energy in the system.




---

[1]: https://en.wikipedia.org/wiki/Mirror_symmetry_(string_theory)
[2]: https://web.ma.utexas.edu/users/vandyke/notes/langlands_sp21/langlands.pdf
[3]: https://en.wikipedia.org/wiki/Quantization_(physics)
[4]: https://en.wikipedia.org/wiki/Topological_quantum_computer
[5]: https://en.wikipedia.org/wiki/Cluster_algebra
[6]: https://en.wikipedia.org/wiki/Quantum_harmonic_oscillator
[7]: https://en.wikipedia.org/wiki/Differential_Galois_theory
[8]: https://en.wikipedia.org/wiki/Galois_theory#History
[9]: https://jontallen.ece.illinois.edu/uploads/537.F18/Papers/MathematicsandItsHistory-johnStillwell.pdf
[10]: https://en.wikipedia.org/wiki/Solvable_group
[11]: https://math.stackexchange.com/questions/837948/proving-that-a-polynomial-is-not-solvable-by-radicals
[12]: https://en.wikipedia.org/wiki/Rational_function
[13]: https://en.wikipedia.org/wiki/Differential_algebra#Examples
[14]: https://en.wikipedia.org/wiki/Picard%E2%80%93Vessiot_theory
[15]: https://en.wikipedia.org/wiki/Algebraic_function
[16]: https://en.wikipedia.org/wiki/WKB_approximation
[17]: https://en.wikipedia.org/wiki/Liouvillian_function
[18]: https://en.wikipedia.org/wiki/Solvable_Lie_algebra
[19]: https://doi.org/10.1007/978-3-662-02838-4_8
[20]: https://doi.org/10.1007/978-3-642-55750-7
[21]: https://bookstore.ams.org/gsm-177
[22]: https://en.wikipedia.org/wiki/Riemann%E2%80%93Hilbert_correspondence




[^1]:
    Although that's because I'm focusing on things that I'm very well 
    prepared for. There's *lots* of interesting physics I want to learn that 
    I haven't had a chance to get to yet, and I'm sure it will be really 
    difficult once I get there. But we have to walk before we can run, and 
    right now I'm doing pretty well established stuff.

[^2]:
    Actually it's my impression that other people said "not always" first, 
    and Galois' main contribution was understanding when the answer is 
    yes or no. For a less impressionistic view of history, see 
    [the wikipedia page][8] or Chapter 19.3 in Stillwell's fantastic 
    [Mathematics and its History][9]

[^3]:
    I don't feel like getting out a book right now, since I want to publish
    this post today (to line up with the defense announcement in the 
    introduction), but I think it's enough to have your ground field be 
    characteristic $0$, contain all $n$th roots of unity, and obviously 
    $a$ should not already have an $n$th root in $K$... Oh and $f$ should
    probably be irreducible.
