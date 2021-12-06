---
layout: post
title: Talk - The Univalence Axiom
tags:
  - my-talks
---

Today I gave my first proper _invited_ talk, which was really exciting! 
I spoke at CMU after I graduated, but I knew the organizers so it didn't really
feel like an invitation. [Jake Park][3] at the University of Florida, though,
invited me to give a talk about HoTT type theory in their department. I was
and am super grateful for the opportunity, and I think the talk itself
turned out fairly well too!

I wasn't sure what kind of background to expect, so I wanted to make sure
the talk was fairly beginner friendly. This was also convenient because it
kept me in waters that I feel comfortable talking about. Jake requested I
talk about what HoTT (particularly univalence) is used for, so I tried to 
emphasize what is (to me) the salient aspect of the theory: Namely the
constant interplay between the logical and the geometric interpretations 
of the operations[^1].

We started with a "quick" review of dependent types, and their dual life
as propositions with a free variable and covering spaces. Then $\Pi$ and 
$\Sigma$ types are (proof relevant) universal and existential quantifiers
(respectively) or global sections and the total space (respectively). 

Next up was identity types (or path types), which logically correspond to
propositions of the form $a \overset{?}{=} b$, and geometrically correspond
to the space of paths from $a$ to $b$. Considering paths between paths,
paths between (paths between paths), and so on, leads us naturally to the
$\infty$-groupoid structure on a type $A$. I first really understood this
after watching a (characteristically excellent) talk of Emily Riehl 
[here][4][^2], which I'm sure will help other people too ^_^.

Then, in order to talk about univalence, we need to talk about equivalences,
so we spent some time going over equivalences and why we care, culminating in
the univalence axiom:

<div class=boxed markdown=1>
  $$(A = B) \simeq (A \simeq B)$$
</div>

In fact, we know slightly more than that: We know _what_ the equivalence is,
as well as the computational content associated to it. If $e : A \simeq B$,
then $\mathtt{ua}(e)$ is a path from $A$ to $B$, and _transporting_ along
that path just applies $e$!

We first talked about some logical applications of univalence. For instance,
if $G$ and $H$ are isomorphic as groups, then they _must_ agree on all 
properties! Because they're actually _equal_! There was a really great question
here about some "group theoretic" properties that can distinguish isomorphic
groups. For instance, two isomorphic groups acting on different objects. 

The way we resolve this is by noticing that, to talk about these "bonus properties",
we need to fix some bonus data about $G$. Maybe it's the data of a group 
homomorphism into a symmetric group, or into a general linear group, etc. but
whatever it is, we _need_ this extra data in order to express the question.
So if we look at, say $(G,X,\alpha)$ and $(G,Y,\beta)$ as objects in the type of
"groups equipped with an action[^4]" 

$$
\sum_{G : \text{Group}} 
\sum_{X : \text{Set}} 
\sum_{\alpha : G \times X \to X}
\text{isGroupAction($\alpha$)}
$$

we'll find that even if $G$ and $H$ are equivalent, 
$(G,X,\alpha)$ and $(H,Y,\beta)$ might _not_ be!

Next we _wanted_ to talk about geometric applications of univalence, but to
do that we needed to spend more time building up geometric types. So we had
a brief diversion into the world of [HITs][6] (Higher Inductive Types),
before using univalence to construct some covering spaces of the circle
$S^1$. I ended with some resources that people might be interested in,
including

 - [this][7] talk of André Joyal on HoTT as foundations[^3], as well as everything
  from [this][8] workshop.
 - I've already linked some of Emily Riehl's talks on HoTT as applied to Homotopy Theory,
     but I'll also shamelessly plug some work of [Wes Caldwell][9], which you
     can read about [here][10], and you can even implement 
     [Eilenberg-Maclane Spaces][12] in HoTT! See [here][13]
 - There's a lot of _great_ work going on in trying to actually compute with
     HoTT efficiently. You can hear Dan Licata talk about it [here][11],
     or read about some developments on Andrej Bauer's blog [here][14].

---

After the talk someone asked a question about differential equations, in 
particular about the [Lotka-Volterra Equations][1]. It sounded like they 
wanted a specific theorem to do with these equations, but I never quite 
understood what they were looking for. I'll assume they
wanted a proof that these equations are always solvable. 

The question, then, is what does a proof of solvability do when we run it as 
code? And the answer, perhaps unsurprisingly, is that it solves the equations!

So if you have a proof (in LEAN, say) that 

$$
\begin{aligned}
\forall \alpha, \beta, \gamma, \delta &: \mathbb{R}_{\gt 0} . \\
\forall x_0, y_0 &: \mathbb{R}_{\gt 0} . \\
\exists x, y &: \mathbb{R}_{\gt 0} \to \mathbb{R}_{\gt 0} . \\
x(0) = x_0 \land \frac{dx}{dt} = \alpha x - \beta xy \quad &\land \quad y(0) = y_0 \land \frac{dy}{dt} = \delta xy - \gamma y
\end{aligned}
$$

the proof would be a piece of code that takes as input
positive constants $\alpha, \beta, \gamma, \delta, x_0, y_0$,
and gives as output two positive functions $x$ and $y$, plus proofs that
they satisfy the desired differential equations and initial conditions.

<div class=boxed markdown=1>
That is, _the proof solves the problem_!
</div>

In general, if you have a theorem that says 
"a solution to an equation of a certain form exists", then the proof of that
theorem should tell you how to _find_ the solution! So running the proof as
code actually _does_ find it! 

The person who asked this question wanted to see actual code, so here is 
one option:

<div class=boxed markdown=1>
  In LEAN, [here][2] is a proof that every equation $x' = v(x,t)$ with $v$ continuous in $t$
  and lipschitz in $x$ has a local solution. If you run this code, you'll get a local solution
  $x(t)$ with a proof that $x$ really satisfies $x' = v(x,t)$ inside the interval
  $(t_\text{min}, t_\max)$.
</div>

It _does_ seem like most of the people pushing for formalization are 
algebraists and logicians. This is not a limitation of the method, though! 
We need more people who know things about differential equations, etc. to 
contribute code to these projects, and flesh out the analytic parts of the
standard libraries. I'm sure there are plenty of easy theorems whose proofs
could be formalized if someone who knew how to do it were willing to put the
time in. Anyways -- I'll get off my soapbox now :P.

---

I actually never sent Jake a talk title or an abstract... So I don't have
one to put here, haha. But I do have slides [here][15]. The talk was also
recorded, and I asked for a copy, so as soon as I have it I'll post a link here ^_^.

---

[^1]: 
    Obviously this is not unique to HoTT! In some vague sense, this is a 
    reflection of the fact that HoTT is the internal language of an 
    "$(\infty,1)$-topos" (whatever that means), and topos theory more generally 
    has this dual logical/geometric flavor.

[^2]: 
    In case this gets taken down for some reason, it's a ~30m talk given
    at the LGBTQ+ math day called "Contractibility as Uniqueness". While I'm here,
    I should probably mention [this][5] video as well 
    ("$\infty$-Category Theory for Undergraduate"), which is longer, but also
    _super_ cool.

[^3]: 
    Again, to future proof, this is "HoTT is a Polyvalent Foundation of Mathematics",
    given at the IAS in 2013.

[^4]:
    As a cute little exercise, can you explicitly write down the rest of this
    type? What should $\text{isGroupAction}(\alpha)$ be?


[1]: https://en.wikipedia.org/wiki/Lotka%E2%80%93Volterra_equations
[2]: https://leanprover-community.github.io/mathlib_docs/analysis/ODE/picard_lindelof.html#top
[3]: https://people.clas.ufl.edu/j-park1/
[4]: https://www.youtube.com/watch?v=X2kNt0ARVeI
[5]: https://www.youtube.com/watch?v=A6hXn6QCu0k
[6]: https://ncatlab.org/nlab/show/higher+inductive+type
[7]: https://www.youtube.com/watch?v=TI-v4QoiEl0
[8]: https://hott-uf.github.io/2021/
[9]: https://www.andrew.cmu.edu/user/wcaldwel/
[10]: https://cmu-hott.github.io/grad-workshop-2021-files/slides-caldwell.pdf
[11]: https://www.youtube.com/watch?v=j5RIZAzooAg
[12]: https://en.wikipedia.org/wiki/Eilenberg%E2%80%93MacLane_spaceh
[13]: https://homotopytypetheory.org/2014/04/15/eilenberg-maclane-spaces-in-hott/
[14]: http://math.andrej.com/
[15]: /assets/docs/univalence-talk/univalence.pdf
