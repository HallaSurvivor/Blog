---
layout: post
title: Life in Johnstone's Topological Topos
tags:
  - 
---

TODO: mention somewhere that if you want a detailed description of 
some pointset topological properties of sequential spaces, you can 
read Dan Ma's excellent [series of blog posts][16]

TODO: Mention the stuff in section 9 of Johnstone's paper relating 
$\mathsf{Sh}(X)$ to $\mathcal{T} / X$.

TODO: say somewhere that it's also interesting to ask how Johnstone's 
topos relates to the gros topoi described in ML&M... Maybe try to 
work this out?


I've been thinking a lot about the internal logic of topoi again, and I 
want to have more examples of topoi that I understand well enough to 
externalize some statements. There's more to life than just a localic 
$\mathsf{Sh}(B)$, and since I'm starting to feel like I understand 
that example pretty well, it's time to push myself to understand 
other important examples too!

In particular, it would be nice to throw some [gros topoi][23] into 
the mix, and where better to start than Johnstone's [topological topos][24]?
This topos is fairly small (which makes explicit computation easy) and is 
very well studied (which makes finding references and examples merely annoying 
instead of totally impossible). 
Eventually I'll want to learn about the effective topos[^1] (and other 
[realizability topoi][2] more generally), various [smooth topoi][3], etc. 
but let's take them on one-at-a-time!

The topological topos $\mathcal{T}$ is a world where every set is 
_intrinsically_ a space. What does this mean?

Well, if we're working in $\mathsf{Set}$, then a space 
is a set $X$ equipped with some ~bonus structure~. This structure can take a 
lot of forms, but one ubiquitous example is that of a _topology_ 
$\tau \subseteq \mathcal{P}(X)$.

Then if you want to work with spaces, you have to constantly say explicitly 
what topology you're working with. After all, there's _lots_ of topologies 
you can put on $X \times Y$, and we need to make sure we choose the 
_right one_ to act like the product of the _spaces_ $(X,\tau)$ and $(Y,\sigma)$.

Nowadays the "right" topology is usually obvious[^4], but this is only because 
we're able to stand on the shoulders of countless 20th century mathematicians!
I think most people would be hard-pressed to come up with, say, the 
[compact-open topology][28] if they hadn't seen it before!

Of course, carrying around this ~bonus structure~ becomes most pronounced 
when working with continuous maps! Now, instead of just defining a function 
and moving on with your life, we're constantly burdened to check that our 
function $X \to Y$ actually respects the topologies involved to be a 
_continuous_ function $(X,\tau) \to (Y, \sigma)$! There are some friends 
of mine who are constantly complaining that algebraic topologists never check 
that things are continuous, and honestly I'm sympathetic. But it can be 
a real hassle to check these things all the time... 

Of course... There's a better way!

As we said before, objects in $\mathcal{T}$ are _intrinsically_ spaces! 
There's no need to choose the "right" topology, or to check that your 
function is "continuous". Inside $\mathcal{T}$, it's _literally impossible_ 
to write down a function that isn't continuous, because there's no 
~bonus structure~ to respect! 

<div class=boxed markdown=1>
TODO: put a picture here of someone saying like "it's impossible" 
or something. I think that'll help break up the wall of text
</div>

This is great for a couple reasons. First, it tells us that anything we 
construct using type theory can be thought of as being, automatically, 
some kind of "space". Understanding this relationship between types and 
topology has been a staple in many people's careers, but I want to single 
out [Martín Escardó][5] as someone whose papers I've been reading lately 
(and who I talk to fairly often on [mastodon][6]). These conversations were 
part of the reason I decided to spend some time trying to understand $\mathcal{T}$.

Second, this tells us that any theorem we're able to prove [constructively][7]
is automatically true "continuously", and gives us a theorem for 
_topological_ structures! Of course, in order to _use_ these theorems, we 
need to understand how objects inside the topological topos $\mathcal{T}$ 
externalize to give honest topological spaces in "the real world"[^6]. 

Of course, in the process of trying to understand $\mathcal{T}$, I had to 
work out a bunch of examples, which I'd love to share! Even though all of this 
is probably "well known to experts", I found a lot of it pretty hard to find, 
so hopefully this blog post is still useful for people ^_^.

Let's get started!

---

## What Is $\mathcal{T}$?
<br>

First, what even _is_ the topological topos? It's sheaves on some site, 
of course, but which one?

<div class=boxed markdown=1>
Write $$\mathbb{N}_\infty$$ for the [one point compactification][32] of 
$\mathbb{N}$. This is the space $$\{0,1,2,3,\ldots,\infty\}$$ topologized 
so that a convergent sequence $(x_n) \to x_\infty$ in $X$ is exactly a 
continuous map $\mathbb{N}_\infty \to X$[^7].

Then let's look at the full subcategory of $\mathsf{Top}$ spanned by 
$$\{1, \mathbb{N}_\infty \}$$. This becomes a site if we give it the 
[canonical topology][33] $J$, and we define the topological topos 
$\mathcal{T}$ to be sheaves on this site.
</div>

We'll motivate this definition in a 
minute, but first let's see how we can picture objects of $\mathcal{T}$.

A presheaf on this site is a pair of sets $X(1)$ and $X(\mathbb{N}_\infty)$ 
with a bunch of maps connecting them:

- There's a map $$n^* : X(\mathbb{N}_\infty) \to X(1)$$ for each $n$, plus a map 
    $$\infty^* : X(\mathbb{N}_\infty) \to X(1)$$
- There's a unique map $$!^* : X(1) \to X(\mathbb{N}_\infty)$$
- For every continuous function $$f : \mathbb{N}_\infty \to \mathbb{N}_\infty$$
    there's a map $$f^* : X(\mathbb{N}_\infty) \to X(\mathbb{N}_\infty)$$.

You should think of elements of $X(1)$ as the _points_ of $X$, and 
the elements of $$X(\mathbb{N}_\infty)$$ as (witnesses to) convergent 
sequences in $X(1)$.
Indeed, if $$p \in X(\mathbb{N}_\infty)$$, then we'll write 
$p_n$ for $$n^*(p)$$ (resp. $p_\infty$ for $$\infty^* p$$) and $p$ 
should be thought of as a _witness_ or _proof_ that the sequence 
$p_n$ converges to $p_\infty$ in $X(1)$[^5]. 

The unique map $$!^*$$ sends a point $x \in X(1)$ to a distinguished proof 
that the constant $x$ sequence converges to $x$, and the functions $$f^*$$ 
"reindex" a convergent sequence. So if $p$ is a proof that $x_n \to x_\infty$,
then $f^* p$ is a proof that $x_{fn} \to x_{f \infty}$ too.

The sheaf condition for the canonical topology guarantees that 
if every subsequence of $x_n$ converges to $x_\infty$, 
the whole sequence $x_n$ converges to $x_\infty$ too[^8].

<div class=boxed markdown=1>
Can you prove that this is reasonable? 

If $$x_n \to x$$ in some topological space $$X$$, and 
$$f : \mathbb{N}_\infty \to \mathbb{N}_\infty$$ is continuous,
why must $$x_{fn} \to x_{f \infty}$$?

You might find it helpful to case on whether $$f(\infty) = \infty$$ or not.
</div>

<div class=boxed markdown=1>
As a cute exercise can you find a simple description of the 
arrows in $\mathcal{T}$? That is, for a natural transformation between 
two sheaves?
</div>

<details>
    <summary>solution</summary>
    A natural transformation between $X$ and $Y$ is a pair of functions 

    $$f_1 : X(1) \to Y(1)$$ 

    $$f_{\mathbb{N}_\infty} : X(\mathbb{N}_\infty) \to Y(\mathbb{N}_\infty)$$

    So that whenever $p$ is a proof that $x_n \to x_\infty$,
    $f_{\mathbb{N}_\infty}(p)$ is a proof that 
    $f_1(x_n) \to f_1(x_\infty)$.

    Moreover, $f_{\mathbb{N}_\infty}$ should respect the distinguished proofs 
    that constant sequences converge 
    (so $f_{\mathbb{N}_\infty}(!^* x) = !^* f_1(x)$) as well as reindexing
    (so $f_{\mathbb{N}_\infty}(g^* p) = g^* (f_{\mathbb{N}_\infty} p)$)
</details>

<br>

Of course, every topological space $X$ gives an object 
$よX = \mathsf{Top}(-,X)$ in the topos[^10], where of course 
$よX(1) = X$ and 
$$よX(\mathbb{N}_\infty) = 
\{ \text{continuous functions } f : \mathbb{N}_\infty \to X \}$$. 
That is, underlying set of $よX$ is exactly the underlying set of $X$,
and for every convergent sequence in $X$ we add a unique proof that that 
sequence converges (represented by the sequence itself).

If we restrict attention to the full subcategory of [sequential spaces][9],
then $よ$ is a fully faithful embedding into $\mathcal{T}$. This shouldn't be 
too surprising, since the sequential spaces are exactly those spaces whose 
topologies are determined by a knowledge of which sequences converge!

You should think of this is a _super_ mild condition, since lots of 
natural spaces of interest are sequential. Just to name a few:

- all metric spaces 
- more generally, all [first countable][36] spaces
- every [CW-complex][37]
- every [ring spectrum][38]

We'll say more about this later, but for now just know that for a _huge_
class of spaces, we can work with them in $\mathcal{T}$ just as well as 
in $\mathsf{Top}$.

<br><br>

There's another definition of $\mathcal{T}$ which you're also likely to see. 

Having $X(1)$ around explicitly as a set of points is helpful for 
exposition and intuition, but it turns out to not change the topos if we 
work without it! Intuitively, we can recover the points from the constant maps 
$$n : \mathbb{N}_\infty \to \mathbb{N}_\infty$$. 

With this in mind, some authors define $\mathcal{T}$ to be the sheaves[^9]
on _just_ the full subcategory of $\mathsf{Top}$ spanned by 
$$\{ \mathbb{N}_\infty \}$$.

This gives some informal justification for the close connection between 
$\mathcal{T}$ and sequential spaces.

Indeed, objects of a sheaf topos can be thought of as being glued together 
from objects of the underlying site. In case you're working with a presheaf 
topos, we take _all_ the ways to glue things together, but in general a 
grothendieck topology forces us to restrict attention to those gluings 
which are "nice" in some sense.

So, with this smaller site in hand, one way to think about objects in 
$\mathcal{T}$ is as copies of $$\mathbb{N}_\infty$$ that are 
"glued together nicely". And one can show that the sequential spaces 
are _exactly_ the quotients of disjoint unions of copies of $$\mathbb{N}_\infty$$!

This tells us that, in some sense, the other objects of $\mathcal{T}$ are 
just copies of $$\mathbb{N}_\infty$$ glued together in more exotic ways,
for instance by gluing two copies of $$\mathbb{N}_\infty$$ literally on 
top of each other to get multiple witnesses to the convergence of the 
same sequence!

<br>

Of course, how do we _know_ that these two definitions agree? I wasn't 
able to find this written down anywhere, but it's not so hard to check 
for ourselves!

The key observation is that $$\{ \mathbb{N}_\infty \}$$ is a 
[dense subsite][8] of $$\{ \mathbb{N}_\infty, 1 \}$$. Here, of course, 
I'm writing a set to mean a full subcategory of $\mathsf{Top}$ equipped 
with the canonical topology.

$\ulcorner$
Indeed, to check this, we only need to show that 

TODO: check this.


<span style="float:right">$\lrcorner$</span>

Now we learn that the two definitions really _do_ agree since, in general,
the topos of sheaves on a dense subsite is equivalent to the topos of sheaves 
on the whole site.

---

## How Does $\mathcal{T}$ Relate to $\mathsf{Top}$?
<br>

More generally, say we have a [kuratowski limit space][10] 
(also called a subsequential space). This is a 

TODO: definition, and mention what the homs are

Every sequential space is automatically a limit space. And the argument from 
before gives a fully faithful embedding of limit spaces into $\mathcal{T}$.

Taken together, we have fully faithful embeddings 

$$
\mathsf{Seq} \hookrightarrow \mathsf{Kur} \hookrightarrow \mathcal{T}
$$

TODO: say something about "processes", a la lawvere?


<br>

TODO: talk about the left adjoints to each of these embeddings. Mention that
they both preserve finite products... While we're at it, mention that the 
inclusions preserve certain colimits (in particular, those involved in 
making CW complexes).

TODO: remember to describe the left adjoints explicitly. The reflector to 
Kur just forgets that there are multiple proofs, and only remembers 
_that_ a sequence converges, rather than _how_. The reflector to Seq 
then builds a topology based on these convergent sequences.

Mention that Kur is a [quasitopos][12]? This gives us some nice results 
for free. Cf.... somewhere in the elephant.

TODO: since products are preserved, these form an [exponential ideal][11],
and the inclusions preserve the cartesian closed structure too!
Note this also tells us that if $Y$ is a sequential space, and $X$ is 
_any_ object of $\mathcal{T}$, then the function space $Y^X$ is already 
a sequential space!

TODO: summarize this with the picture Martin always draws with Seq 
(with $\times,+,\to$) sitting inside Kur (with $\prod, \sum$) sitting 
inside $\mathcal{T}$ (with $\Omega$).

TODO: mention, probably in a footnote, that while MANY spaces are sequential 
(for instance, all first countable spaces, thus all metric spaces, 
CW complexes, etc), this doesn't cover EVERY space you might be interested in.
For instance, the [Stone–Čech Compactification][13] of the natural,
$\beta \mathbb{N}$, is equivalently the space of [ultrafilters][14] on 
$\mathbb{N}$. This space is extremely important in various subfields of 
logic and combinatorics. See, for instance, 
Hindman and Strauss's 
_Algebra in the Stone-Čech Compactification: Theory and Applications_. 
In particular, the applications to [Ramsey Theory][15].

If you can, maybe compute the sequential reflection of $\beta \mathbb{N}$?

TODO: if you want to read more about how to actually compute (co)limits 
and exponentials in $\mathsf{Seq}$ and $\mathsf{Kur}$, I highly recommend 
Menni and Simpson's 
_Topological and limit-space subcategories of countably-based equilogical spaces_

TODO: add a link to that, and summarize some important stuff in a footnote.
See pdf pg 10

---

So now we see how to get an honest topological space from an object in 
$\mathcal{T}$! 

Reflecting $X$ into $\mathsf{Kur}$ takes the underlying set $X(1)$ and 
just remembers which sequences converge. Then reflecting _this_ into 
$\text{Seq}$ builds an honest to goodness topological space by saying 
$U \subseteq X(1)$ is open iff .... 

TODO: something!

TODO: also maybe mention that under a mild separation condition 
(sequential hausdorffness?) $\mathsf{Seq} \simeq \mathsf{Kur}$?

TODO: put a few computations here. Define some simple types and figure out what 
the topology on them should be. 

For instance, $\prod_{n : \mathbb{N}} 2$. 
This is equivalent to $\mathbb{N} \to 2$, where everything in sight 
already lives in the CCC $\mathsf{Seq}$. So this space 

Maybe the type of decreasing binary sequences?

---

What do locales look like in $\mathcal{T}$?

Well, for any $T_1$ locale (footnote with the definition), then... 
something something this is homming into the version of that locale 
externally. See, for instance, the first section of 
Moerdijk and Reyes 
_Smooth spaces versus continuous spaces in models for synthetic differential geometry_

TODO: It's worth figuring out exactly what this means. 
We need to compare it to a locale object internal to $\mathcal{T}$...

---

What do algebras look like in $\mathcal{T}$?

First of all, for any (essentially) algebraic theory $\mathbb{T}$, 
if we have a (sequential!) topological model (for example, a topological 
group whose underlying topology is sequential), that model is still a 
model in $\mathcal{T}$.

Indeed, the [funtorial semantics][17] perspective says that 
a topological $\mathbb{T}$-model $M$ corresponds to a finite product
functor[^2] from some classifying category $\mathcal{C}_\mathbb{T}$ to 
$\mathsf{Seq}$. Since the inclusion functor 
$\mathsf{Seq} \hookrightarrow \mathcal{T}$ is a right adjoint, it preserves 
products, and thus $M$ is still a $\mathbb{T}$-model when viewed as an 
object in $\mathcal{T}$! 

TODO: so if we constructively prove a theorem about groups, say, then 
that theorem is true inside $\mathcal{T}$. Thus, since (sequential) 
topological groups all live inside $\mathcal{T}$, we get a theorem about 
all topological groups!

And this works for basically _any_ kind of algebraic gadgets you want 
to consider!

<br>

Conversely, say we _have_ a $\mathbb{T}$-model in $\mathcal{T}$. 
That is, say we have a finite product functor 
$\mathcal{C}_\mathbb{T} \to \mathcal{T}$.
Then since the reflector $\mathcal{T} \to \mathsf{Seq}$ preserves 
finite products, the honest topological space associated to our 
object is itself a $\mathbb{T}$-model!

This tells us that if we ever want to reason about an algebraic 
object in $\mathcal{T}$, we can fruitfully pretend it's "just" a 
topological model! After all, its underlying topological space is 
still a model, and the only difference between an object in $\mathcal{T}$ 
and its underlying space is the potential for multiple proofs of convergence!

TODO: phrase that better, and tie it into your earlier discussion about 
what objects in $\mathcal{T}$ look like... In fact, maybe say something like 
this earlier in the post.

---

## Bonus Axioms Validated by $\mathcal{T}$

TODO: mention LLPO too

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

---

TODO: don't forget to say something about universes

TODO: say something about $\Omega$

TODO: figure out how function spaces in $\mathcal{T}$ (really in $\mathsf{Seq}$)
relate to function spaces in $\mathsf{Top}$ (when they exist)


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
