---
layout: post
title: 
tags:
  - 
---

TODO: use the relationship between monos/epis in Seq and in T to show $\mathcal{T}$ is not 
de morgan. Indeed, from the [nlab page][56] deMorgan-ness is equivalent 
to $1+1$ being injective. But it _isn't_, since in Seq there's a map
$(0,1) + (2,3) \to 1+1$ which doesn't extend to a map $(0,3) \to 1+1$ 
(which has to be constant). Since monos in Seq are still monos in $\mathcal{T}$,
we're done. If you really want to be careful, we know a mono in Top reflects 
to a mono in Seq, which gives us a mono in $\mathcal{T}$.

TODO: Of course, another way to do this 
is to note that the double negation topos is $\mathsf{Set}$ with the 
indiscrete topology (maybe this is worth checking explicitly?) Then 
(also following that nlab page) we want to know if $1+1 \to \Omega_{\lnot \lnot}$ 
is an isomorphism, and it isn't. They're both supported on $\{0,1\}$, but 
the topologies are different!


## Bonus Axioms Validated by $\mathcal{T}$

Speaking of proving theorems in $\mathcal{T}$, we actually don't have to 
be _totally_ constructive! The topological topos satisfies certain nice 
~bonus axioms~ that make it a particularly nice place to work.

For instance, $\mathcal{T}$ models [Dependent Choice][20][^3]. 

Say you have a relation $R \subseteq X \times X$ which is 
<span class=defn>total</span> in the sense that 
$\forall x . \exists y . R(x,y)$.

Then DC says for each $x_0 : X$, there's a function 
$f : \mathbb{N} \to X$ so that $f(0) = x_0$ and for each $n$,
$R(f(n), f(n+1))$.

If we think of $$\{ y \mid R(x_n,y) \}$$ as being 
"allowable values for $x_{n+1}$", then totality of $R$ says that 
we can always take one more step. However, we might have to _choose_ 
the next step from inhabited set of allowable options, and these choices 
_depend_ on the choices that came before (since if we'd chosen a different 
$x_1$, we might have different allowable choices for $x_2$, and so on).

Thus, DC basically tells us that recursive definitions work, even if we 
don't have a canonical way to _choose_ one of many options at each 
recursive stage. Indeed, most recursive definitions work by first choosing 
an $x_0$, and then arguing that the set of "allowable" next steps is 
always inhabited[^16].

Here's an idiomatic example of dependent choice in action: The 
[Baire Category Theorem][45] for complete metric spaces.

<div class=boxed markdown=1>
Let $(X,d)$ be a (cauchy) complete metric space[^14] with inhabited 
(strongly[^15]) dense open sets $U_1, U_2, U_3, \ldots$.

Then the countable intersection $\bigcap_n U_n$ is still (strongly) dense.
</div>

The usual proof doesn't use LEM, so it goes through unchanged. 
We'll present it here, though, paying special attention to the 
use of DC.

TODO: are we using DC? or $\mathsf{DC}$? I think we should do the former

$\ulcorner$

Let $V$ be open in $X$. We need to show that $V \cap \bigcap_n U_n$ is 
inhabited. We proceed recursively:

Since $U_1$ is strongly dense, we know that $U_1 \cap V$ is inhabited, 
say by $x_1$. Now since $U_1 \cap V$ is open, we can find a neighborhood of 
$x_1$, say $B

<span style="float:right">$\lrcorner$</span>

TODO: ok so here's some facts you might want later:

$C \subseteq X$ is _weakly closed_ if it contains all its limit points. 
It's _strongly closed_ if it's the complement of an open set. 

Strongly closed always implies weakly closed, and I think we can use 
regularity of a metric space to show that $x \in C \subseteq U$ 
with $C$ strongly closed and $U$ any neighborhood of $x$ 
(which will be enough to make the BCT proof go through)

<br>

Dependent Choice implies [Countable Choice][41], which itself implies 
[Weak Countable Choice][42]. But WCC implies that the 
[dedekind reals][43] and the [cauchy reals][44] agree. And indeed one 
can show directly that in $\mathcal{T}$ both the dedekind and cauchy reals 
are given by $よ\mathbb{R}$.

<br>

Moreover, $\mathcal{T}$ models Brouwer's Continuity Principle that 
"Every function $f : \mathbb{R} \to \mathbb{R}$ is continuous"!

It's shockingly hard to find this written down anywhere, but it's 
cited in lots of places! It's definitely part of the folklore, 
but for completeness I'll include a proof in an "appendix" 
at the bottom of this post. If you know of a reference, or of a 
slicker proof than the one I found, I would REALLY love to hear 
about it[^13]!

Regardless, the truth of Brouwer's principle tells us that 
$\mathcal{T}$ is a rather stronger version of [Solovay's Model][22]. 
Solovay's model validates
$$\mathsf{LEM}+\mathsf{DC}+$$"every function $\mathbb{R} \to \mathbb{R}$ is measurable".

In $\mathcal{T}$, we have $\mathsf{DC}$ and the stronger 
"every function $\mathbb{R} \to \mathbb{R}$ is continuous". But the price 
we pay is LEM.

<br>


We can ask about other nonconstructive principles too. For instance, 
the [(Lesser) Limited Principle of Omniscience][49]!

LPO says that every sequence of bits is either $0^\omega$ or 
contains a $1$. That is:

$$\forall s : 2^\mathbb{N} . (\forall n . s(n) = 0) \lor (\exists n . s(n) = 1)$$

This is false in $\mathcal{T}$:

$\ulcorner$
If it were true, then we would know $1 \Vdash \text{LPO}$. Now 
cashing out the universal quantifier, we would know that 
for every $$s \in 2^\mathbb{N}(\mathbb{N}_\infty)$$

$$\mathbb{N}_\infty \Vdash (\forall n . s_k(n) = 0_k) \lor (\exists n . s_k(n) = 1_k)$$

Here $$s_k : \mathbb{N}_\infty \to 2^\mathbb{N}$$ is allowed to be any 
convergent sequence in cantor space, and we interpret $0_k$ and $1_k$ as 
constant sequences.

Let's take $s_k$ to be the sequence $0^k 1^\omega$.
That is, the $k$th element of this sequence, $s_k$, should be the point in 
cantor space with $k$ many $0$s followed by an infinite tail of $1$s.
Note this sequence converges to $0^\omega$.

Now what would it mean to have $(\forall n . s(n) = 0) \lor (\exists n . s(n) = 1)$?
We would have an open cover of $$\mathbb{N}_\infty$$ where each element of 
that cover thinks that one of these disjuncts is true. But every covering 
seive of $$\mathbb{N}_\infty$$ contains a function $f_U$ for $U$ an infinite 
subset of $\mathbb{N}$.

TODO: say what this means? 

Now restricting $s$ to this member of the cover amounts to restricting $s$ 
to a subsequence, $s_{r_k}$.

Is it possible that $$\mathbb{N}_\infty \Vdash \forall n . s_{r_k}(n) = 0_{r_k}$$?
This says for every convergent sequence 
$$n_k \in \mathbb{N}(\mathbb{N}_\infty)$$, we must have $$s_{r_k}(n_k) = 0_{r_k}$$
for all $k$. Of course, it's easy to find a convergent sequence where this 
is false! We can just choose $$n_1 \gt r_1$$ to make $$s_{r_1}(n_1) = 1 \neq 0$$.

Is it possible for $$\mathbb{N}_\infty \Vdash \exists n . s_{r_k}(n) = 1_{r_k}$$?
This says we can pass to a further subsequence $$s_{\ell_{r_k}}$$ so that 
for some convergent sequence $$n_k \in \mathbb{N}(\mathbb{N}_\infty)$$ we 
have $$s_{\ell_{r_k}}(n_k) = 1_k$$ for all $k$. But of course this is false too!
Every convergent sequence of naturals is eventually constant, say $n_k = N$ 
for $k \gg 1$. Then for $k$ large enough, we'll have both $n_k = N$ and 
$$\ell_{r_k} \gt N$$, in which case $$s_{\ell_{r_k}}(n_k) = 0 \neq 1$$.

So we see that LPO externalizes to a false claim, and thus is not validated 
by $\mathcal{T}$.
<span style="float:right">$\lrcorner$</span>

<br>

What about LLPO? This turns out to be true[^17]! In fact, we'll prove 
something a priori stronger: _Analytic_ LLPO. This is well known 
to imply LLPO, and the converse is true under weak countable choice.
Since $\mathcal{T}$ models DC, it certainly models WCC, so this is 
equivalent to checking LLPO directly.

Analytic LLPO says that $$\forall x : \mathbb{R} . (x \geq 0) \lor (x \leq 0)$$.

$\ulcorner$
Proposition 6.2 in Johnstone's original paper implies that $\mathbb{R}$ 
is the pushout of the closed cover 

<p style="text-align:center;">
<img src="/assets/images/life-in-johnstones-topological-topos/closed-pushout.png" width="25%">
</p>

Now showing $\forall x : \mathbb{R} . (x \geq 0) \lor (x \leq 0)$ amounts 
to building a section of the projection 
$\pi : \sum_{x : \mathbb{R}} \lVert (x \geq 0) + (x \leq 0) \rVert$.
Here I've also cashed out the $\lor$ for a [propositional truncation][53]
of a coproduct.

But by the universal property of the pushout, we get a map 
$s : \mathbb{R} \to \sum_{x : \mathbb{R}} \lVert (x \geq 0) + (x \leq 0) \rVert$
as below:

<p style="text-align:center;">
<img src="/assets/images/life-in-johnstones-topological-topos/llpo-universal-property.png" width="100%">
</p>

Moreover, since both $\pi s$ and $\text{id}_\mathbb{R}$ make the outer 
square commute, they must be equal by uniqueness in the universal property. 
So $s$ is the desired section of $\pi$, and $\mathcal{T}$ models LLPO.
<span style="float:right">$\lrcorner$</span>

<br><br>

Aaaand last but not least, let's check [Markov's Principle][54]:

We'll show that 
$\mathcal{T} \models \forall x : \mathbb{R} . (x \neq 0) \to (x \# 0)$.
Here $\#$ means that $x$ is [apart][55] from $0$. That is, 
$\exists q : \mathbb{Q} . (x \lt q \lt 0) \lor (0 \lt q \lt x)$.

This is actually a bit stronger than what we need. We leave it as a 
nice exercise to show that $(x \neq 0) \to (x \# 0)$ implies the 
usual statement of (analytic) MP: $\lnot (x \leq 0) \to (x \gt 0)$.

TODO: this proof

TODO: mention $\lnot (x \# 0) \to (x = 0)$.

TODO: does $\mathcal{T}$ model de morgan's laws?


---
---

## Appendix: A Proof that Johnstone's Topos Models Brouwer's Continuity Principle

If you're not super familiar with externalizing formulas, you 
might want to read my [old blog post][39] with a bunch of simpler 
examples before trying to tackle this one!

We'll be doing this computation using the site with two objects, 
$$\{1, \mathbb{N}_\infty\}$$.

$\ulcorner$
We want to show that

$$
\mathcal{T} \models 
\ulcorner 
\text{every function $f : \mathbb{R} \to \mathbb{R}$ is continuous}
\urcorner
$$

Which happens if and only if the terminal object $1$ _forces_ it. 
Switching to the forcing notation and writing down the definition 
of continuity explicitly[^11], we get

$$
1 \Vdash
\forall f : \mathbb{R}^\mathbb{R} . 
\forall \epsilon : \mathbb{R}_{\gt 0} .
\forall x : \mathbb{R} .
\exists \delta : \mathbb{R}_{\gt 0} .
\forall y : \mathbb{R} . 
|x-y| \lt \delta \to |fx - fy| \lt \epsilon 
$$

But now we can start cashing out what _this_ is equivalent to, 
until we're left with a statement purely about "the real world".
Then we'll check directly that this "real world" statement is true 
to prove the claim!

Well, to cash out some universal quantifiers, we need to know that 
for every arrow $U \to 1$ in the site and for every 

- $f \in \mathbb{R}^\mathbb{R}(U)$
- $\epsilon \in \mathbb{R}_{\gt 0}(U)$
- $x \in \mathbb{R}(U)$

that 


$$
U \Vdash 
\exists \delta : \mathbb{R}_{\gt 0} . 
\forall y : \mathbb{R} . 
|x-y| \lt \delta \to |fx - fy| \lt \epsilon 
$$

Thankfully, there's only two maps $U \to 1$ in our site! 
The unique maps $1 \to 1$ and $\mathbb{N}_\infty \to 1$.

<br>

Let's check $1 \to 1$ first, since that's easier. Remembering 
that $\mathbb{R}$ in $\mathcal{T}$ is represented by 
$よ\mathbb{R} = \text{Hom}_\mathsf{Top}(-,\mathbb{R})$, we see

$$
\begin{align}
\mathbb{R}^\mathbb{R}(1)
&= よ1 \to よ\mathbb{R}^{よ\mathbb{R}} \\
&= よ1 \times よ\mathbb{R} \to よ\mathbb{R} \\
&= よ(1 \times \mathbb{R}) \to よ\mathbb{R} \\
&= よ\mathbb{R} \to よ\mathbb{R} \\
&= \Big \{ \text{continuous functions $\mathbb{R} \to \mathbb{R}$} \Big \}
\end{align}
$$

Here the first step is yoneda, then the fact that product is left adjoint 
to exponential. Then the fact that yoneda preserves limits, and 
finally yoneda again.

This means that if $f \in \mathbb{R}^\mathbb{R}(1)$, then $f$ is just 
a continuous function $\mathbb{R} \to \mathbb{R}$ in "the real world",
and similar computations show that $\epsilon$ and $x$ are honest real 
numbers (with $\epsilon \gt 0$, of course).

Now to show that 

$$
1 \Vdash 
\exists \delta : \mathbb{R}_{\gt 0} . 
\forall y : \mathbb{R} . 
|x-y| \lt \delta \to |fx - fy| \lt \epsilon 
$$

we need to find a cover $V \twoheadrightarrow 1$ and a 
$\delta \in \mathbb{R}_{\gt 0}(V)$ so that 
$V \Vdash \forall y : \mathbb{R} . |x-y| \lt \delta \to |fx - fy| \lt \epsilon$.
Thankfully, this is surprisingly easy!

We'll choose the (rather silly) cover $1 \to 1$. Then we need a 
$\delta \in \mathbb{R}_{\gt 0}(1)$, which we'll take to be the 
$\delta$ (in the real world!) promised by the fact that $f$ is 
continuous at $x$.

For our last universal quantifier, we have to show that for any map 
$W \to 1$ in our site (again, there's only two options) and any 
$y \in \mathbb{R}(W)$ that

$$
|x-y| \lt \delta \to |fx - fy| \lt \epsilon 
$$

where this implication is in the real world!

In case $W = 1$, $y \in \mathbb{R}(1)$ is just a real number. 
So the claim is immediate from our choice of $\delta$ 
(the external witness to continuity of $f$).

In case $$W = \mathbb{N}_\infty$$, then $$y \in \mathbb{R}(\mathbb{N}_\infty)$$
is a convergent sequence $$y_n : \mathbb{N}_\infty \to \mathbb{R}$$. Then 
we need to show that whenever $|x - y_n| \lt \delta$ for all $n$ 
(including $n=\infty$) that $|fx - f y_n| \lt \epsilon$ for all $n$ 
as well. But, of course, this follows immediately from continuity on 
each $y_n$ separately.

<br>

Whew! Halfway done!
Unfortunately that was the easier case, haha.
Now let's see what happens when $U \to 1$ is $$\mathbb{N}_\infty \to 1$$.

Then a similar argument from before shows that 
$$f \in \mathbb{R}^\mathbb{R}(\mathbb{N}_\infty)$$ means exactly that 
(externally)
$$f : \mathbb{N}_\infty \times \mathbb{R} \to \mathbb{R}$$ is continuous.

Similarly, we get continuous functions (read: convergent sequences)
$$\epsilon : \mathbb{N}_\infty \to \mathbb{R}_{\gt 0}$$ and 
$$x : \mathbb{N}_\infty \to \mathbb{R}$$.

Now we need to find a cover $$V \twoheadrightarrow \mathbb{N}_\infty$$, 
which we'll again take to be the identity 
$$\mathbb{N}_\infty \to \mathbb{N}_\infty$$, and a choice of 
$$\delta \in \mathbb{R}_{\gt 0}(V) = \mathbb{R}_{\gt 0}(\mathbb{N}_\infty)$$
so that for every $$g : W \to \mathbb{N}_\infty$$ and every $y : \mathbb{R}(W)$, 
we have (pointwise)

$$
|x \circ g - y| \lt \delta \circ g \to |f \circ x \circ g - f \circ y| \lt \epsilon \circ g
$$


Now, what should $\delta$ be? Once we have that in hand, we can 
just check the above inequality and finally be done with this proof!

Morally, the question is this: If we treat 
$$f : \mathbb{N}_\infty \times \mathbb{R} \to \mathbb{R}$$ 
as a convergent sequence of functions $f_n : \mathbb{R} \to \mathbb{R}$,
and we're given a convergent sequence $\epsilon_n$, can we choose our 
witnesses $\delta_n$ to continuity of $f_n$ at $x_n$ so that the 
$\delta_n$ themselves are a convergent sequence?

This would probably be easy for an actual analyst, but I found the 
construction a bit delicate. I'm particularly happy to have it 
written down somewhere!

We'll first notice that 
$$\epsilon_* = \inf \{ \epsilon_1, \epsilon_2, \ldots, \epsilon_\infty \}$$
is bounded away from $0$. After all, for $n \gg 1$, 
$\epsilon_n \gt \frac{\epsilon_\infty}{2}$. So this infimum is taken over 
the first finitely many $\epsilon_n$s (which are all $\gt 0$) and an 
infinite tail of $\epsilon_n$s which are uniformly 
$\gt \frac{\epsilon_\infty}{2} \gt 0$.
Now, since $$f : \mathbb{N}_\infty \times \mathbb{R} \to \mathbb{R}$$ 
is continuous, it's _uniformly_ continuous on a compact subset. For instance, 
on the compact subset 
$$\mathbb{N}_\infty \times \left [x_\infty - \frac{1}{10}, x_\infty + \frac{1}{10} \right ].$$

Thus, we can find a $$\delta_* (\lt \frac{1}{10})$$ so that whenever two inputs 
$(n_1,x_1)$ and $(n_2,x_2)$ are are $$\delta_*$$-close to each other, 
(and $x_1,x_2$ are within $\pm \frac{1}{10}$ of $x_\infty$)
the outputs are $$\frac{\epsilon_*}{4}$$-close to each other!

We'll take $m$ large enough so that 
- $\frac{1}{m} \lt \delta_*$
- for all $n \gt m$ we have $$\lvert x_n - x_\infty \rvert \lt \delta_*$$

For $n \leq m$, we'll let $\delta_n$ be whatever reals we like so that 
whenever $|x_n - y| \lt \delta_n$, we know $|f(n,x_n) - f(n,y)| \lt \epsilon_n$.
There's no difficulty in doing this since each function $f(n,-)$ is 
continuous.

Of course, we want these $\delta_n$s to assemble into a convergent sequence, 
so we'll need to be more careful when $n \gt m$ is "large".
For these, we'll let $$\delta_n = \delta_* - |x_\infty - x_n|$$. 
Note that, as $n \to \infty$, the $\delta_n$s really do converge to 
$$\delta_\infty = \delta_*$$.

<br>

Now that we know what our $$\delta : \mathbb{N}_\infty \to \mathbb{R}_{\gt 0}$$ 
is, we need to verify those inequalities!

For every arrow $$g : W \to \mathbb{N}_\infty$$, we need to show that 
(pointwise in $W$)

$$
|x \circ g - y| \lt \delta \circ g \to |f \circ x \circ g - f \circ y| \lt \epsilon \circ g
$$

First let's let $W = 1$. Then $g$ is naming an element $n$ of $$\mathbb{N}_\infty$$
(we allow $n=\infty$).

Then $x \circ g : 1 \to \mathbb{R}$ is just $x_n$, and similarly for everything 
else in sight. So our inequality becomes 

$$
|x_n - y| \lt \delta_n \to |f(n,x_n) - f(n,y)| \lt \epsilon_n 
$$

In case $n \leq m$, we literally chose $\delta_n$ to make this true, so we're good!.
In case $n \gt m$, then we need a small computation[^12]:

$$
\begin{align}
|f(n,x_n) - f(n,y)| 
&\leq |f(n,x_n) - f(\infty,x_n)| \\
&+ |f(\infty,x_n) - f(\infty,x_\infty)| \\
&+ |f(\infty,x_\infty) - f(\infty,y)| \\
&+ |f(\infty,y) - f(n,y)|
\end{align}
$$

Since $$\frac{1}{n} \lt \delta_*$$, the first summand is 
$$\lt \frac{\epsilon_*}{4}$$. Since $$|x_n - x_\infty| \lt \delta_*$$,
the second summand is $$\lt \frac{\epsilon_*}{4}$$ too. 
Since $$|x_n - y| \lt \delta_n = \delta_* - |x_\infty - x_n|$$,
we learn that 

$$
|x_\infty - y| \leq |x_\infty - x_n| + |x_n - y| \lt \delta_*
$$

so that the third summand is $$\lt \frac{\epsilon_*}{4}$$. Lastly, 
since $$\frac{1}{n} \lt \delta_*$$, the final summand is also 
$$\lt \frac{\epsilon_*}{4}$$.

Thus (since $$\epsilon_*$$ is the infimum of the $\epsilon_n$s)
$$|f(n,x_n) - f(n,y)| \lt \epsilon_* \leq \epsilon_n$$,
as desired!

<br>

And to finish things off, what happens if $$W = \mathbb{N}_\infty$$? 

Then $$g : \mathbb{N}_\infty \to \mathbb{N}_\infty$$ is continuous, 
and our inequality amounts to verifying that 
for every $$y : \mathbb{N}_\infty \to \mathbb{R}$$ and 
for every $n$ (including possibly $n=\infty$),

$$
|x_{gn} - y_n| \lt \delta_{gn} \to |f(gn,x_{gn}) - f(gn,y_n)| \lt \epsilon_{gn}
$$

Of course, blessedly, we _just_ proved that if an input $y_n$ is $\delta_{gn}$ 
close to $x_{gn}$, then its output $f(gn,y_n)$ must be 
$\epsilon_{gn}$ close to $f(gn,x_n)$! 

So finally, we're done ^_^

<span style="float:right">$\lrcorner$</span>

<div class=boxed markdown=1>
TODO: put an image here of someone sighing with relief 
</div>


---

[1]: https://arxiv.org/abs/2404.01256
[2]: https://ncatlab.org/nlab/show/realizability+topos
[3]: https://ncatlab.org/nlab/show/Models+for+Smooth+Infinitesimal+Analysis
[4]: https://ncatlab.org/nlab/show/Johnstone%27s+topological+topos
[5]: https://www.cs.bham.ac.uk/~mhe/
[6]: https://mathstodon.xyz/@MartinEscardo
[7]: https://ncatlab.org/nlab/show/constructive+mathematics
[8]: https://ncatlab.org/nlab/show/dense+sub-site
[9]: https://en.wikipedia.org/wiki/Sequential_space
[10]: https://ncatlab.org/nlab/show/subsequential+space
[11]: https://ncatlab.org/nlab/show/exponential+ideal
[12]: https://ncatlab.org/nlab/show/quasitopos
[13]: https://en.wikipedia.org/wiki/Stone%E2%80%93%C4%8Cech_compactification
[14]: https://en.wikipedia.org/wiki/Ultrafilter_on_a_set
[15]: https://en.wikipedia.org/wiki/Ramsey_theory
[16]: https://dantopology.wordpress.com/2010/06/21/sequential-spaces-i/
[17]: https://ncatlab.org/nlab/show/Lawvere+theory
[18]: https://en.wikipedia.org/wiki/Regular_cardinal
[19]: https://ncatlab.org/nlab/show/essentially+algebraic+theory
[20]: https://en.wikipedia.org/wiki/Axiom_of_dependent_choice
[21]: https://ncatlab.org/nlab/files/DCTopTopos.pdf
[22]: https://en.wikipedia.org/wiki/Solovay_model
[23]: https://ncatlab.org/nlab/show/big+and+little+toposes
[24]: https://ncatlab.org/nlab/show/Johnstone%27s+topological+topos
[25]: /2021/12/16/topological-categories.html
[26]: https://en.wikipedia.org/wiki/Box_topology
[27]: https://math.stackexchange.com/questions/871610/why-are-box-topology-and-product-topology-different-on-infinite-products-of-topo
[28]: https://en.wikipedia.org/wiki/Compact-open_topology
[29]: /2024/03/25/continuous-max-function
[30]: https://ncatlab.org/nlab/show/frame
[31]: https://en.wikipedia.org/wiki/Scott_continuity
[32]: https://en.wikipedia.org/wiki/Alexandroff_extension
[33]: https://ncatlab.org/nlab/show/canonical+topology
[34]: https://en.wikipedia.org/wiki/Subobject_classifier
[35]: https://londmathsoc.onlinelibrary.wiley.com/doi/abs/10.1112/plms/s3-38.2.237
[36]: https://en.wikipedia.org/wiki/First-countable_space
[37]: https://en.wikipedia.org/wiki/CW_complex
[38]: https://en.wikipedia.org/wiki/Spectrum_of_a_ring
[39]: /2022/12/13/internal-logic-examples.html
[40]: https://en.wikipedia.org/wiki/Sierpi%C5%84ski_space
[41]: https://ncatlab.org/nlab/show/countable+choice
[42]: https://ncatlab.org/nlab/show/countable+choice#WCC
[43]: https://ncatlab.org/nlab/show/Dedekind+cut
[44]: https://ncatlab.org/nlab/show/Cauchy+real+number
[45]: https://en.wikipedia.org/wiki/Baire_category_theorem
[46]: https://en.wikipedia.org/wiki/Second-countable_space
[47]: https://en.wikipedia.org/wiki/Compactly_generated_space
[48]: https://en.wikipedia.org/wiki/Locally_compact_space
[49]: https://ncatlab.org/nlab/show/principle+of+omniscience
[50]: https://ncatlab.org/nlab/show/quotient+type
[51]: http://www.lfcs.inf.ed.ac.uk/reports/92/ECS-LFCS-92-208/
[52]: https://core.ac.uk/download/33573841.pdf
[53]: https://planetmath.org/37propositionaltruncation
[54]: https://en.wikipedia.org/wiki/Markov%27s_principle
[55]: https://en.wikipedia.org/wiki/Apartness_relation
[56]: https://ncatlab.org/nlab/show/De+Morgan+topos

[^1]:
    I spent some time a few years ago (Feb of 2022, according to my Zotero)
    thinking hard about the effective topos. I think I was going 
    to write a blog post about it, but I never got around to it.

    I think I should be able to remind myself what was going on, and 
    in a perfect world I would understand it much better now that I know 
    more things, so hopefully I'll finally write that post. This is 
    particularly relevant now that Andrej Bauer and James Hanson have posted 
    their [preprint][1] constructing a realizability topos where the 
    reals are countable.

[^2]:
    Of course, if you need operations of infinite arity, we can play this game 
    with functors that preserve limits of size $\lt \lambda$ for any 
    [regular cardinal][18] $\lambda$.

    Similarly, if you want partial operations, that's totally ok! 
    [Essentially algebraic][19] theories are modelled by finite 
    limit functors (or, again, by $\lt \lambda$-continuous functors),
    and since right adjoints preserve all limits, again any model in 
    $\mathsf{Seq}$ is still a model when considered as an object in 
    $\mathcal{T}$.

[^3]:
    You can find a proof in Shulman and Simpson's aptly named note 
    [_Dependent Choice in Johnstone's Topological Topos_][21]

[^4]:
    And even then, it might not be obvious when you're learning! I remember 
    when I first learned pointset topology the idea of a "cylinder set" 
    and the product topology made no sense to me! Honestly without the 
    framework of [topological categories][25] or something similar, I could 
    see people _still_ being surprised that the [box topology][26] isn't 
    the "right" topology on an infinite product space! See, for instance,
    this old and highly upvoted [mse question][27].

[^5]:
    Note that it's entirely possible for two different elements
    $$p \neq q \in X(\mathbb{N}_\infty)$$ to witness convergence of 
    the same sequence (so $p_n = q_n$ for all $n$ and $\infty$)!

    Indeed, this will be crucial later, for instance in our discussion 
    of the [subobject classifier][34] $\Omega$.

[^6]:
    After my [last post][29] on a constructive extreme value theorem, I wanted to 
    see how it externalizes in topoi other than $\mathsf{Sh}(B)$. I'm pretty sure 
    in the effective topos we'll get something that looks like an algorithm 
    eating a function on a compact space and returning its max... But it's 
    super unclear what we should get interpreting this in $\mathcal{T}$! 
    After all, a [frame][30] in $\mathcal{T}$ is a topological lattice $L$. So 
    a locale in $L$ is a space whose frame of opens is _itself_ a space...

    I still haven't totally figured out this story
    (though I'm much less weirded out by the idea since I remembered that 
    [scott topologies][31] exist as a natural topology on the frame of opens), 
    so I won't say anything 
    more in _this_ post, but trying to understand $\mathcal{T}$ well enough to 
    externalize the constructive extreme value theorem was the second big 
    motivator for this post. Of course, understanding $\mathcal{T}$ was so fun 
    and interesting that I got distracted from my original goal, but that's how 
    these things tend to go for me, haha.

[^7]:
    If you want a _super_ concrete description, it's equivalent to 

    $$
    \left \{ 
        1, \frac{1}{2}, \frac{1}{3}, \frac{1}{4}, \ldots, \frac{1}{n}, \ldots, 0 
    \right \}
    \subseteq \mathbb{R}
    $$

    with the subspace topology.

[^8]:
    This is spelled out quite clearly in Johnstone's original paper 
    [_On a Topological Topos_][35]. Indeed, Johnstone computes the 
    covering sieves _very_ explicitly, and I highly recommend reading 
    about it there.

    I don't want to mention the grothendieck topology explicitly because 
    I think it would take too much time for not much payoff. I'm happy to 
    mainly summarize facts that are useful for working with 
    $\mathcal{T}$, and point to the relevant references where necessary.

[^9]:
    Still with the canonical grothendieck topology.

    Some people like to describe this (one object) category as the 
    "monoid of continuous endomorphisms of $$\mathbb{N}_\infty$$", but 
    I'd rather not say that because I think it would confuse the 
    exposition that follows.

[^10]:
    It's not _immediately_ obvious that this presheaf is actually a sheaf,
    but it turns out to be. This is in Johnstone's [original paper][35].

[^11]:
    This is the first time I'm actually written down the definition of 
    (metric space) continuity in full! No wonder students struggle with 
    this, haha. I've forgotten what a mouthful it is!

[^12]:
    Which looks simple now, but coming up with it took me longer than 
    I'd care to admit.
    Making this computation work is the crux of the whole proof.

[^13]:
    I would _also_ be super interested in hearing if $\mathcal{T}$ validates
    something like "for any spaces $X$ and $Y$, every $f : Y^X$ is continuous".
    
    My guess is that this is also true, but it sounds kind of annoying to 
    prove, especially in the absence of the metric space structure that we 
    used on $\mathbb{R}$.

    Or, maybe it's easier to work topologically than metrically, 
    and we can do this synthetically by using the 
    set of opens $\Sigma^X$ 
    (where $\Sigma$, as usual, is the [sierpinski space][40]). I'm kind 
    of tempted to try, but this blog post is already super long and I've 
    _gotta_ finish it.

[^14]:
    I don't know if there are constructive subtleties with the notion of 
    cauchy completeness which might be relevant here, and since I really 
    want to get this blog post out I don't want to read a bunch of literature 
    on constructive metric spaces to try and figure it out... 

    If anyone happens to know some facts about constructive metric spaces, though,
    I would love to hear about them! But for now, treat this example as being 
    more to showcase how dependent choie works than to say anything profound 
    about the topological topos.

[^15]:
    A set $D \subseteq X$ is called <span class=defn>Strongly Dense</span>
    if for any open set $V$ we know that $D \cap V$ is inhabited.

[^16]:
    You might wonder why we need a "nonconstructive" axiom to do this. Why 
    can't we use induction on $\mathbb{N}$?

    After all, we can prove (constructively, in type theory) that

    $$
    \left (
        \prod_{x:X} \sum_{y:X} R(x,y)
    \right ) 
    \to 
    \left ( 
        \prod_{x_0 : X }
        \sum_{f : \mathbb{N} \to X}
        f(0) = x_0 \land \prod_{n:\mathbb{N}} R(f(n), f(n+1))
    \right )
    $$

    (and this makes a nice exercise!)

    The difference lies in $\sum$ vs $\exists$! To build a term
    of type $\prod_x \sum_y R(x,y)$ is to build a function that 
    eats an $x$ and returns a $y$ alongside a proof that $R(x,y)$.
    This gives us a _canonical_ choice in $$\{ y \mid R(x,y) \}$$ -- 
    just use the one this function gave us!

    Dependent choice works with something much weaker. It says we can build 
    such a function even when there _merely exists_ such a $y$, without 
    being handed a witness! (Of course, the function we're given only 
    merely exists too)

    Think about the semantics in $\mathsf{Sh}(B)$ for a moment. 
    Here, to say that $\exists y . R(x,y)$ is to say that there's an 
    open cover of $B$ and a local witness $y$ on each element of the 
    cover. But it's entirely possible for these witnesses to not glue 
    into a global witness!

[^17]:
    This realization has probably been made by many people, but it was 
    added to the nlab by Mike Shulman.
