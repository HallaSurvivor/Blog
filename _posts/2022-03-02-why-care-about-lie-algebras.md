---
layout: post
title: Talk -- Why Care about Lie Algebras?
tags:
  - my-talks
---

I gave my second (and last) presentation/talk in my lie algebras class today,
and it was on a topic that was and is really important to me. When learning
something new, I think it's worth asking yourself what it does for you. 
What problems does it solve? How do the structures we're learning about arise? 
There's a lot of people who enjoy abstraction for its own sake, but I ultimately
care about _solving problems_, and while I'm not going to shy away from high
abstraction mathematics to do so (I'm still a category theorist after all)
I think it's important to be aware of concrete examples that can ground your
theory in things that obviously matter.

Again, this talk was just under a half hour, and I don't have an abstract for
it (since it was informal), but I want it included with my other talks because
I'll be giving a debrief at the end.

---

First, I gave (what I think is) the original motivation for lie algebras: 

A [lie group][1] is a group which is also a manifold, and the group operations
should be smooth. Important examples are $(\mathbb{R}, +)$ and $(S^1, \times)$
(where we view $S^1$ as the unit circle in $\mathbb{C}$, say).

These are (in my mind) obviously interesting, with wide application. Anytime
you have a continuous family of symmetries, as you do in many situations in
geometry, physics, and differential equations[^1], you have a lie group describing
those symmetries. Then we can _exploit_ this symmetry in order to simplify
problems. As a great example of using lie groups to simplify calculations
and solve problems, see [this][2] 3Blue1Brown video.

Unsurprisingly, lie groups are _complicated_! But since they have smooth
structure we can hit our problems over the head with calculus, thus turning
our problems into linear algebra. This is exactly how lie algebras arise[^2]!

Now, since we're taking the first-order approximation of our lie group structure,
it's reasonable to worry that we're going to lose lots of information about
our lie group when we differentiate. Thankfully, this isn't the case! There's
a slew of correspondence theorems which let you translate back and forth between
the lie algebra and the lie group. Most notably:

<div class=boxed markdown=1>
  1. If $G$ is connected and simply connected, then lie group homs $G \to H$
  are in natural bijection with lie algebra homs $\mathfrak{g} \to \mathfrak{h}$

  2. If $\mathfrak{g}$ is a (real or complex) lie algebra, then there is a 
  unique connected and simply connected lie group $\tilde{G}$ whose lie algebra is $\mathfrak{g}$.
  Moreover, every connected lie group $G$ whose lie algebra in $\mathfrak{g}$ 
  is a quotient of $\tilde{G}$ by a discrete central subgroup.

  3. The (connected) subgroups (resp. normal subgroups, etc.) of a (connected)
  lie group $G$ are in natural correspondence with subalgebras (resp. ideals, etc.)
  of the lie algebra $\mathfrak{g}$.
</div>

So as long as we're interested in connected lie groups, we lose _remarkably_ 
little information in passage to the lie algebra[^3]. 

Next I gave a concrete example of a computation that is simplified by the 
use of lie algebras. Physicists care about finite dimensional irreducible representations
of $SU(2)$ because they tell us what kinds of "spin" a particle can have. 
Thankfully $SU(2)$ is simply connected, so irreducible representations of
$SU(2)$ are in natural bijection with (real) irreducible representations of 
$\mathfrak{su}(2)$. Then by [complexifying][10], these are in natural bijection
with (complex) irreducible representations of $\mathfrak{sl}(2, \mathbb{C})$.
But in this class we completely classified the irreducible 
$\mathfrak{sl}(2,\mathbb{C})$ representations[^4]! Unraveling this procedure
gives a complete classification of irreducible representations of $SU(2)$,
which seem (to me) almost impossible to get our hands on directly!

---

With this computation out of the way, the talk became much more of a survey.
I ended with three other examples of lie algebras arising "in the wild" as 
useful tools for solving (seemingly unrelated) problems.

First, the obvious one. Instead of working with lie groups, we can work with
[algebraic groups][11] (their algebro-geometric analogue). These too give
lie algebras when we look at the tangent space of the identity, and again
there's a correspondence between properties of the group and its lie algebra
(see [here][12] for more). These are important (so I'm told) to the 
[langlands program][13], which I think provides suitable motivation.

Next a more surprising application. Recall the [Burnside Problem][14], which asks

<div class=boxed markdown=1>
If $G$ is finitely generated, and every element is finite order, must $G$ be finite?
</div>

The answer (famously) is "no"[^5]. But it was an extremely hard problem, and in 
the process of studying it people came up with the 
<span class=defn>Restricted Burnside Problem</span>:

<div class=boxed markdown=1>
If $G$ is finitely generated (by $m$ elements) and every element is finite order
(at most $n$), _and_ we moreover assume $G$ is finite, can we bound the size
of $G$ in terms of $m$ and $n$?
</div>

If $n = p^k$ is a prime power, then $G$ is nilpotent (it's a finite $p$-group), 
and bounding its nilpotency class will also bound its order. Now for the magic.

From a "Zassenhaus Filtration"

$$
G = G_0 \vartriangleright G_1 \vartriangleright \cdots \vartriangleright G_\ell = 1
$$

we build a vector space

$$
\tilde{L}(G) \triangleq \bigoplus G_i / G_{i+1}
$$

(recall each $G_i / G_{i+1}$ is elementary abelian, thus a vector space over
$\mathbb{F}_p$)

equipped with the bracket 
$[a G_{i+1}, b G_{j+1}] \triangleq a^{-1}b^{-1}ab G_{i+j+1}$
this becomes a lie algebra, and the question of bounding the nilpotency class
of $G$ is translated into a purely lie algebra theoretic question about 
a subalgebra of $\tilde{L}(G)$. See the (excellent!) survey 
_On the Restricted Burnside Problem_ by Zelmanov for more details.

Lastly, a construction from [homotopy theory][16]. Here I spent another good
chunk of time talking about homotopy groups (which are hard to understand),
and the (comparatively simple) _rational_ homotopy groups. It's a (very)
famous theorem of Quillen that the rational homotopy groups of a space
assemble into a (differential, graded) lie algebra 
(with the [whitehead bracket][17]) which is effective 
(in the sense that we can actually compute with this lie algebra) and also
a perfect invariant (in the sense that two simply connected spaces $X$ and $Y$ 
have the same rational homotopy if and only if their associated lie algebras 
are [quasi-isomorphic][18]). 

Much of this was parroted from Jacob Lurie's talk 
_Lie Algebras and Homotopy Theory_, which you can find [here][19]. 
One day I would like to spend more time with this material, because I think
homotopy theory is super interesting, but for now I have to be quite sketchy
when talking about it, because I don't know anything at all.

---

And that was the talk! 

I think it was alright? Definitely not my best talk, but I also wanted to give
as many examples as possible in a fairly short time span. I liked the 
survey-esque nature of it, but wish I knew more about each of the topics I was
surveying :P.

If nothing else, I learned a _ton_ writing this talk, and am now entirely 
convinced on lie algebras as something I should be familiar with, which was
really the point of me looking into this at all. I also gained some ammunition
for caring about categories, since we actually get an _equivalence of categories_
between the category of $G$ reps to the category of $\mathfrak{g}$ reps
(when $G$ is simply connected, see [here][20]). This tells you, basically for
free, that irreducible $G$ representations are the same thing as irreducible
$\mathfrak{g}$ representations, since reducibility is expressible categorically.

Another thing I want to think more about is the relationship between the last
two examples... In both cases we had a family of related objects
(the $G_i / G_{i+1}$ and the rational homotopy groups) plus some kind of 
"derivation" (either group-theoretic commutators, or the whitehead bracket)
which gives us lie algebra structure.

This might be superficial, but I would like to think more about it, and see 
if I can't find other examples of this phenomenon. I remember reading somewhere
that we can study noncommutative algebras by using techniques from 
commutative algebra as long as the noncommutativity is "bounded" in some sense,
and this _also_ reminds me of that.

For instance, we can study the [Weyl Algebra][21] 

$$
k\langle x, y \rangle \big / xy - yx = 1
$$

which is "barely noncommutative[^6]" in the sense that while $x$ and $y$ 
don't commute, we're only off by a constant (that is, a term of smaller degree
than the terms we started with). Then we can run a similar construction, where
we look at the direct sum of the degree $n$ elements modulo the degree $n-1$ 
elements, and this forms a ring that _is_ commutative. 

Anyways, it's quite late now and I feel like I'm starting to ramble. 
All in all, the talk was _fine_, but I definitely learned a lot, and have
a lot of follow-up thinking to do, which is what I really wanted to get out
of it.

I'll see you all soon ^_^

---

[^1]:
    [Sophus Lie][3] was actually initially interested in lie groups because he 
    wanted a smooth analogue of [galois theory][4] that would let him understand
    when differential equations have "simple" solutions, in a way analogous to
    classical galois theory classifying when polynomial equations have "simple"
    (read: radical) solutions. 

    The resulting machinery, which can also be used to solve differential 
    equations (again, in a way analogous to using galois theory to solve polynomial
    equations, a topic I've talked about [before][5]) turned out to be a bit
    unweildy. It turns one "large" differential equation into many "small"
    differential equations, and by "many" I mean possibly hundreds. 

    This is difficult for a human to manage? But for a computer? This is ideal!

    You can read more about the idea in [this][6] set of notes, and about
    possible computer implementations in [this][7] paper. There's also apparently
    a whole book on the subject, Schwarz's _Algorithmic Lie Theory for
    Solving Ordinary Differential Equations_, though I've not read it.

[^2]:
    I didn't mention this in the talk, because I didn't have time, but I feel
    like I should say a quick word here for completeness.

    Given a lie group $G$, we define its lie algebra $\mathfrak{g}$ to be the
    [tangent space][8] at the identity element $e$. Then the bracket 
    $[-,-]$ on $\mathfrak{g}$ is defined in a somewhat roundabout way.

    First, let $\text{AD}_g : G \to G$ be $\text{AD}_g(h) = ghg^{-1}$. Then
    if we differentiate $\text{AD}_g(h)$ with respect to $h$ at the identity, 
    we get a map $\text{Ad}_g : \mathfrak{g} \to \mathfrak{g}$. 

    Next, we differentiate _this_ with respect to $g$! This gives us a map
    $\text{ad}_v : \mathfrak{g} \to \mathfrak{g}$ for each $v \in \mathfrak{g}$.

    Lastly, we define $[v,w] = \text{ad}_v(w)$.

    If you're interested in this, you can read more at John Baez's lecture
    notes [here][9] (which is where I learned most of this). In particular
    lectures $11$ to $16$. 

[^3]:
    There's a categorical remark here as well, which I didn't make in the
    talk. But the functor sending a lie group to its lie algebra and the 
    functor sending a lie algebra to its connected, simply connected lie group
    is a pair of adjoint functors!

    In this sense, sending a lie group to its lie algebra is "forgetful",
    and there's a unique "free" way to assign a lie group to a lie algebra!
    Moreover, we have $RL\mathfrak{g} \cong \mathfrak{g}$.

[^4]:
    They all look like the action of $\mathfrak{sl}(2)$ on $S^n\mathbb{C}^2$,
    the space of homogeneous degree $n$ polynomials in $2$ variables.

[^5]:
    It's at this point that I'm obligated to mention one solution to this
    problem (though not the first) comes via [automata groups][15], which I
    did research in as an undergraduate. 

    For more, you might look into "Gupta-Sidki Groups".

[^6]:
    Apparently "[almost commutative][22]" is a technical term!

[1]: https://en.wikipedia.org/wiki/Lie_group
[2]: https://www.youtube.com/watch?v=ltLUadnCyi0
[3]: https://en.wikipedia.org/wiki/Sophus_Lie
[4]: https://en.wikipedia.org/wiki/Galois_theory
[5]: /2021/08/06/cyclic-extensions.html
[6]: http://www.physics.drexel.edu/~bob/LieGroups/LG_16.pdf
[7]: https://www.heldermann-verlag.de/jlt/jlt01/CZICHPL.PDF
[8]: https://en.wikipedia.org/wiki/Tangent_space
[9]: https://math.ucr.edu/home/baez/lie_groups/
[10]: https://en.wikipedia.org/wiki/Complexification
[11]: https://en.wikipedia.org/wiki/Algebraic_group
[12]: https://www.jmilne.org/math/CourseNotes/LAG.pdf
[13]: https://en.wikipedia.org/wiki/Langlands_program
[14]: https://en.wikipedia.org/wiki/Burnside_problem
[15]: https://en.wikipedia.org/wiki/Mealy_machine
[16]: https://en.wikipedia.org/wiki/Homotopy_theory
[17]: https://en.wikipedia.org/wiki/Whitehead_product
[18]: https://en.wikipedia.org/wiki/Quasi-isomorphism
[19]: https://www.youtube.com/watch?v=LeaiPHAh0X0
[20]: https://math.stackexchange.com/q/641082/655547
[21]: https://en.wikipedia.org/wiki/Weyl_algebra
[22]: https://en.wikipedia.org/wiki/Almost_commutative_ring
