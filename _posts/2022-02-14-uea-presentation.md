---
layout: post
title: Talk (?) -- Universal Enveloping Algebras
tags:
  - my-talks
---

This barely counts as a talk, but I want it catalogued with the rest of the
talks I've given, because this is going to have a retrospective aspect to it
like all of my post-talk posts do. A while ago now, I gave a 30 minute 
presentation in my Lie Algebras class where I answered two questions that I'd
brought up over the course of the class, with the unifying thread being this:
both questions are naturally answered by the [Universal Enveloping Algebra][1].

As a brief aside, I gave a talk last week about a concrete application of 
topos theory. I want to write up a post about it, but unfortunately I 
screwed up the last ten minutes... I'll say more about it when I get around
to posting it, but the moral of the story is that I don't want to write that
post until I really understand what the last ten minutes _should_ have been if
I'd done it correctly.

---

So: what did I talk about in the presentation? Well, a lie algebra is a vector
space with bonus structure, and we talk about short exact sequences of 
lie algebras. So it's reasonable to wonder if the category of lie algebras
is [abelian][6].

In hindsight the answer is obviously "no", and I briefly mentioned why. It
comes down to the existence of monos which aren't [normal][2]. In the category
of abelian groups (the prototypical abelian category) every subgroup is normal.
Rephrased categorically, this says that every monomorphism is the kernel of 
some morphism. In an abelian category this condition (and its dual) must be 
satisfied, but we know there is a distinction between ideals 
(which we can quotient by) and subalgebras (which, in general, we can't) of 
a given lie algebra. So not every mono is normal, and the category of lie algebras
cannot be abelian.

This leads us to a related question: Is the category of $\mathfrak{g}$-reps
abelian for a lie algebra $\mathfrak{g}$? I was fairly sure the answer would be "yes"
asked this, but I wanted to bring it up in class because the class has been
entirely devoid of category theory, despite representation theory having a 
fairly categorical reputation in my mind.

The answer, of course _is_ yes, and the easiest way to see this (imo) is via
the universal enveloping algebra $U(\mathfrak{g})$. Before we go into that,
though, let's briefly say what the other question I wanted to answer was.

We know that $\mathfrak{g}$ naturally acts on itself by "left multiplication",
by which I mean $[g,-] : \mathfrak{g} \to \mathfrak{g}$. However this action 
need not be faithful! 

<div class=boxed markdown=1>
  If it's not obvious, it's a cute exercise to work out why this action need
  not be faithful!
</div>

With this in mind, it's natural to ask if there _is_ an space which admits
a natural, faithful $\mathfrak{g}$ action. The answer, again, is yes, and the 
vector space in question is the universal enveloping algebra[^1]!

So then, at this point you should be sold on $U\mathfrak{g}$ being an interesting
object... but what exactly _is_ it? I'll start with a motivating categorical
approach, then (for people whole aren't as well versed in the way of adjoint
functors), we'll go over how one might build it by hand. 
This follows the talk fairly closely[^2], but it should go better here since
I expect a bit more categorical maturity from readers of my blog[^3].

---

So then, what's the goal of the universal enveloping algebra? We know that 
matrix algebras are automatically lie algebras, when we interpret $[A,B]$
as $AB - BA$. More generally we can do this with the ring of endomorphisms
of your favorite vector space $\text{End}(V)$. More generally _still_, we
can do this for your favorite algebra over a field.

This is obviously functorial, and sends the ring $\text{End}(V)$ to the lie
algebra $\mathfrak{gl}(V)$, but I'm going to call this 
$\mathsf{Lie} \left ( \text{End}(V) \right )$ instead, to emphasize the fact
that $\mathsf{Lie}$ is a functor from $\mathbb{F}\text{-alg}$ to $\mathbb{F}\text{-lie-alg}$.

Here, as usual, $\mathbb{F}$ is either $\mathbb{R}$ or $\mathbb{C}$. I'm not 
sure what happens in positive characteristic (it seems to be subtle. See [here][5])
so I'm restricting attention to particularly nice fields, haha.

Now, recall a <span class=defn>Representation</span> of a lie algebra
$\mathfrak{g}$ is a homomorphism 
$$\alpha : \mathfrak{g} \to \mathsf{Lie} \left ( \text{End}(V) \right )$$. 
These obviously assemble into a category whose objects are pairs $(V,\alpha)$
and whose morphisms are linear maps $V \to W$ which commute with the 
$\mathfrak{g}$-action.

If this sounds like a category of modules, you're right! That's some good
justification for this being an abelian category, and it's not super hard to
verify the axioms by hand... But wouldn't it be nice if we didn't have to?

Let's say we had a left adjoint $U \dashv \mathsf{Lie}$. Then we would have

$$
\begin{prooftree}
\AxiomC{$\mathfrak{g}\text{-reps}$}
\UnaryInfC{$\alpha : \mathfrak{g} \to \mathsf{Lie} \left ( \text{End}(V) \right )$}
\UnaryInfC{$\tilde{\alpha} : U \mathfrak{g} \to \text{End}(V)$}
\UnaryInfC{$U \mathfrak{g}\text{-modules}$}
\end{prooftree}
$$

so, if we can find a left adjoint $U$ for $\mathsf{Lie}$,
the category of $\mathfrak{g}$-representations will be equivalent to the 
category of $U\mathfrak{g}$-modules.

Now, let's get all the abstract nonsense out of our system right now. Since
it's clear that $\mathsf{Lie}$ preserves limits (indeed, it's basically not
_doing_ anything at all), we can apply the 
[Special Adjoint Functor Theorem][7] to quickly see that $\mathsf{Lie}$ 
has a left adjoint. Unfortunately this tells us _nothing_ about what $U$ 
looks like, so while _true_, this proof is not as useful as it could be.

There's an art to finding left adjoints, where we try to figure out what
the "freest" way to build an object should be. Usually to introduce free 
structure, you just add the syntax, and declare it _has_ to satisfy all the
rules you want. 

So for us, we want to add multiplication, to turn our lie algebra into a 
traditional algebra. Following the hint I gave in the last paragraph, we might
look at the space of all sums of formal strings $x_1 x_2 \cdots x_n$, where
we multiply by concatenation. This construction already has a name, if we
recognize $x_1 x_2 \cdots x_n$ as an element of the $n$th tensor power of $\mathfrak{g}$.

That is, we look at 

$$
\mathfrak{g}^{\otimes n} \triangleq 
\underbrace{\mathfrak{g} \otimes \mathfrak{g} \otimes \cdots \otimes \mathfrak{g}}_{n \text{ times}}
$$

and we think of the element $x_1 \otimes x_2 \otimes x_3 \cdots \otimes x_n$ as
the product of the $x_i$. 

So $\mathfrak{g}^{\otimes n}$ consists of the free $n$-fold products of elements
of $\mathfrak{g}$, and we want to allow _arbitrary_ products. What's the obvious
thing to do? We look at the [tensor algebra][8]

$$
\bigoplus_{n \geq 0} \mathfrak{g}^{\otimes n}
$$

Now elements of this are exactly sums of products of elements of $\mathfrak{g}$!

There's one piece of data we're missing, though. We want $\mathsf{Lie}$ of this
algebra to be related to $\mathfrak{g}$ somehow. 
We know $\mathfrak{g} \hookrightarrow \bigoplus_{n \geq 0} \mathfrak{g}^{\otimes n}$
since $\mathfrak{g} = \mathfrak{g}^{\otimes 1}$, so it's reasonable to want
$[x_1, x_2]$ as computed in the tensor algebra to be the same as $[x_1, x_2]$
as computed in $\mathfrak{g}$.

How do we do that? Well, we just _force_ it to be true! For every $x_1, x_2 \in \mathfrak{g}$
we add a rule telling us how to evaluate the syntax 
$[x_1, x_2] = x_1 \otimes x_2 - x_2 \otimes x_1$. It should be $[x_1, x_2]_\mathfrak{g}$,
and so we define

$$
U \mathfrak{g} \triangleq 
\frac{\bigoplus_{n \geq 0} \mathfrak{g}^{\otimes n}}{ x_1 \otimes x_2 - x_2 \otimes x_1 = [x_1, x_2]_\mathfrak{g}}
$$

<div class=boxed markdown=1>
Check (using existing universal properties of quotients, sums, and tensor products)
that algebra homs out of $U \mathfrak{g}$ are in bijection with lie algebra homs 
out of $\mathfrak{g}$.

That is, show that $U \dashv \mathsf{Lie}$.
</div>

Remember at the start of all this, we had two questions that $U \mathfrak{g}$ 
is supposed to help us answer.

We've already spent some time showing that the category of 
$\mathfrak{g}$-reps is abelian. This is because the category of 
$\mathfrak{g}$-reps is equivalent to the category of $U \mathfrak{g}$-modules,
and we know that module categories are always abelian.

But how does this provide us with a canonical faithful $\mathfrak{g}$-rep? 
Well, I'll leave it to you to check that the obvious map
$\mathfrak{g} \hookrightarrow \mathsf{Lie} U \mathfrak{g}$ 
(if you like, the [unit][9] of the adjunction) really is an embedding. So
$\mathfrak{g}$ acts faithfully on $U \mathfrak{g}$. 

For extra concreteness, what _is_ this action? It's exactly the left-multiplication
action! So 

$$
g \cdot (x_1 \otimes x_2 \otimes \cdots \otimes x_n) \triangleq 
g \otimes x_1 \otimes x_2 \otimes \cdots \otimes x_n
$$

---

Let's work this out the only example in lie theory I know, $\mathfrak{sl}_2(\mathbb{C})$[^4].

This lie algebra is three dimensional, with a basis

$$
x = \begin{pmatrix} 0 & 1 \\ 0 & 0 \end{pmatrix}
\quad
y = \begin{pmatrix} 0 & 0 \\ 1 & 0 \end{pmatrix}
\quad
h = \begin{pmatrix} 1 & 0 \\ 0 & -1 \end{pmatrix}
$$

Moreover, the lie structure is generated by the equations

- $[x,y] = h$
- $[h,x] = 2x$
- $[h,y] = -2y$

Now the tensor algebra is going to be all the formal products of $x$, $y$,
and $h$. That is, we get $\mathbb{C} \langle x,y,h \rangle$, the space of
(noncommutative!) polynomials in $x$, $y$, and $h$. The subspace of degree $1$
polynomials can be identified with $\mathfrak{sl}_2$, since the degree $1$ 
polynomials are linear combinations $x$, $y$, and $h$. 

Now we have to _quotient_ the tensor algebra by the generating equations for
the lie bracket. So we end up with

$$
U \mathfrak{sl}_2(\mathbb{C}) \triangleq 
\frac{\mathbb{C}\langle x, y, h \rangle}{xy-yx = h \quad \quad hx-xh = 2x \quad \quad hy-yh = -2y}
$$

A fairly concrete object!

---

[^1]:
    NB: $U\mathfrak{g}$ is _huge_ in general, and if $\mathfrak{g}$ is finite 
    dimensional, one can also ask if there's a natural, finite dimensional
    faithful $\mathfrak{g}$-representation. Now it seems like the answer is 
    "no". 

    A finite dimensional faithful $\mathfrak{g}$-representation always exists,
    _but_ it's not natural (in the sense of category theory). This is called
    [Ado's Theorem][3], and Terry Tao has a great blog post about it
    [here][4].

[^2]:
    In hindsight, this was a
    mistake. I knew my audience wasn't particularly experienced with categorical
    lingo, but I gave a talk that would have been good for me, were I an audience
    member, rather than a talk that would be good for the audience I knew I had.

    The particularly disappointing thing is that, if I'm being completely
    honest with myself, I knew as I was writing the talk that I was probably
    not writing the best talk for my audience, and I did it anyways. I know I 
    have high standards for my talks, and am liable to think a quite average 
    talk was a trainwreck, but at the very least I should have done the 
    concrete construction first... Oh well.

[^3]:
    There's a part of me that likes to think I'm writing these posts for
    "myself, roughly 2 years ago", and by that metric the mention of 
    adjoint functors will be more clarifying than confusing. Unfortunately I 
    think the opposite was true in my presentation...

[^4]:
    I'm joking, obviously... But not by much.



[1]: https://en.wikipedia.org/wiki/Universal_enveloping_algebra
[2]: http://nlab-pages.s3.us-east-2.amazonaws.com/nlab/show/normal+monomorphism
[3]: https://en.wikipedia.org/wiki/Ado%27s_theorem
[4]: https://terrytao.wordpress.com/2011/05/10/ados-theorem/
[5]: https://mathoverflow.net/questions/7112/which-is-the-correct-universal-enveloping-algebra-in-positive-characteristic
[6]: https://en.wikipedia.org/wiki/Abelian_category
[7]: https://ncatlab.org/nlab/show/adjoint+functor+theorem#statement
[8]: https://en.wikipedia.org/wiki/Tensor_algebra
[9]: https://ncatlab.org/nlab/show/unit+of+an+adjunction
