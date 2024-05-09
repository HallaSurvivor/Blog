---
layout: post
title: Life in Johnstone's Topological Topos
tags:
  - life-in-the-topological-topos
---

TODO: define "internally sequentially hausdorff" by 

$$
\forall f,g : \mathbb{N}_\infty \to X . 
(\forall n : \mathbb{N} . fn = gn) \to (f \infty = g \infty)
$$

and show that "internally sequentially hausdorff" iff
"externally sequentially hausdorff".

Then mention that "$\lnot \lnot$-separated" is the same thing as 
"in $\mathsf{Kur}$" externally.

So we can characterize the "nice spaces" internally as those sets 
satisfying these two axioms!

<br>

TODO: Mention the stuff in section 9 of Johnstone's paper relating 
$\mathsf{Sh}(X)$ to $\mathcal{T} / X$.

TODO: What do "mere existentials" look like in $\mathcal{T}$? In a 
sheaf topos it means something exists on each section of an open cover,
but these might not glue into a _global_ section. Is there a similar 
interpretation (maybe involving subsequences?) for $\mathcal{T}$?

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
- every noetherian [ring spectrum][38]

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
$$\{ \mathbb{N}_\infty \}$$. That is, they define it to be sheaves on the 
monoid of continuous endomorphisms of $$\mathbb{N}_\infty$$. See, for instance,
The Elephant (A2.1.11(j)).

This gives a different informal justification for the close connection between 
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
able to find this written down anywhere, but it's easy to check
for ourselves!

The key observation is that $$\{ \mathbb{N}_\infty \}$$ is a 
[dense subsite][8] of $$\{ \mathbb{N}_\infty, 1 \}$$. Here, of course, 
I'm using set-builder notation to mean a full subcategory of $\mathsf{Top}$ equipped 
with the canonical topology.

$\ulcorner$
Indeed, to check this, we only need to show that every object in 
$$\{ \mathbb{N}_\infty, 1 \}$$ is covered by maps with domain in 
$$\{ \mathbb{N}_\infty \}$$. But, of course, the identity function 
$$\mathbb{N}_\infty \to \mathbb{N}_\infty$$ covers, and the unique map 
$$\mathbb{N}_\infty \to 1$$ covers too. 

Since $$\{ \mathbb{N}_\infty \}$$ is a _full_ subcategory of 
$$\{ \mathbb{N}_\infty, 1 \}$$, the second condition of the 
[comparison lemma][8] is trivial, and we learn that the geometric map 
induced by the inclusion is an equivalence.

In particular, the two common definitions really _do_ agree!
<span style="float:right">$\lrcorner$</span>

---

## How Does $\mathcal{T}$ Relate to $\mathsf{Top}$?
<br>

<div class=boxed markdown=1>

Here's the tl;dr for this section, for ease of reference. 

We have a sequence of fully-faithful embeddings of cartesian closed categories, 
each of which admits a left adjoint, as shown below:

<p style="text-align:center;">
<img src="/assets/images/life-in-johnstones-topological-topos/relationship-adjoints.png" width="75%">
</p>

The embeddings preserve all limits (as right adjoints) but moreover preserve 
the cartesian closed structure, as well 
as certain "nice" colimits (in particular, all colimits involved in the 
creation of CW-complexes). The exact definition of "nice" here is 
explained below, but includes the coproduct. Additionally, the 
image of a map $X \to Y$ of sequential spaces (with $Y$ sequentially hausdorff)
as computed in $\mathcal{T}$ is just the set theoretic image equipped with 
the quotient topology.

The left adjoints preserve all colimits, and moreover preserve finite products 
(and thus, in particular, models of algebraic theories).

Lastly, in case we restrict to the full subcategory of 
"sequentially hausdorff spaces", in the sense that every convergent sequence 
has a unique limit, then the adjunction 
$\text{Seq} \leftrightarrows \text{Kur}$ is an adjoint equivalence!

<br>

Here $\text{Seq}$ is bicartesian closed, 
$\text{Kur}$ is locally cartesian closed,
$\mathcal{T}$ is a topos, and the embeddings preserve all of 
this structure. Thus one can say that at each level we add new
"type constructors", as shown in the following diagram 
(stolen from Martín Escardó):

<p style="text-align:center;">
<img src="/assets/images/life-in-johnstones-topological-topos/venn-diagram.png" width="50%">
</p>

Colimits in $\text{Seq}$ are computed as in $\mathsf{Top}$, so 
in particular the "nice colimits" that get preserved between 
$\text{Seq}$ and $\mathcal{T}$ agree with colimits in $\mathsf{Top}$.

The relationship of limits in $\text{Seq}$ to limits in 
$\mathsf{Top}$ is more subtle. If you only care about (quotients of)
[second countable][46] spaces, then the bicartesian closed structure 
on $\text{Seq}$ (and thus in $\mathcal{T}$) agrees with the usual 
bicartesian closed structure on the "convenient category" of 
[compactly generated spaces][47]. In particular, function spaces 
get the [compact-open topology][28].

If your spaces are [locally compact][48], then the (finite) 
product in $\text{Seq}$ (and thus in $\mathcal{T}$) agrees with 
the product in $\mathsf{Top}$.
</div>

---

TODO: do these embeddings preserve/reflect monos/epis/isos? Say explicitly 
that if $\mathcal{T}$ proves two spaces are isomorphic, then reflecting 
isos (fully faithfulness) means that $\text{Seq}$ thinks they're isomorphic, 
which means $\mathsf{Top}$ thinks they're homeomorphic 
(since all functors preserve isomorphisms). I think fully faithful functors 
_reflect_ monos/epis, so if we show something is mono/epi in $\mathcal{T}$ 
that tells us that it's mono/epi in $\text{Seq}$... Does this mean it's 
mono/epi in $\mathsf{Top}$? Conversely, if we have something that's 
mono/epi/iso in $\mathsf{Top}$, does that mean it's mono/epi/iso in 
$\mathsf{Seq}$/$\mathcal{T}$? This should be related to continuous functors 
preserving monos?

TODO: Actually, I bet Seq is topologically concrete. Or at least it has 
discrete/codiscrete functors from $\mathsf{Set}$! This tells us that we 
can check mono/epi-ness in Seq by checking injectivity/surjectivity of the 
map on points.

That's a _lot_, so let's go more in depth into what all of this means, haha.

We'll start with the definition of a [Kuratowski Limit Space][10] 
(also called a subsequential space): 

<div class=boxed markdown=1>
A <span class=defn>Kuratowski Limit Space</span> is a set $X$ 
equipped with a set of <span class=defn>Convergent Sequences</span> in $X$ 
subject to the following axioms:

1. For every $x \in X$, the constant sequence $(x)$ converges to $x$
2. If $(x_n)$ converges to $x$, then every subsequence of $(x_n)$ converges to 
$x$ too
3. If, for some $x$, every subsequence of $(x_n)$ contains a further subsequence 
converging to $x$, then the whole sequence $(x_n)$ already converges to $x$.

We moreover call $X$ <span class=defn>Sequentially Hausdorff</span> if it 
satisfies the bonus axiom

{:start="4"}
4. If $(x_n)$ converges to $x$ and $(x_n)$ converges to $y$, then $x=y$.

<br>

A function $f : X \to Y$ between limit spaces is called 
<span class=defn>continuous</span> if whenever $x_n \to x$, 
we have $fx_n \to fx$.
</div>

Every sequential topological space is automatically a limit space, where we 
just let the convergent sequences be the (topologically) convergent sequences.
Moreover, there's a fully faithful embedding of limit spaces into $\mathcal{T}$ 
where we let $X(1) = X$ and $$X(\mathbb{N}_\infty)$$ be the set of converget 
sequences in $X$. 

TODO: decide if you want to include the definition of the coverings, 
and verify (or leave as an exercise) that this embedding really gives us 
a _sheaf_... Cf also footnote[^8].

Taken together, we have fully faithful embeddings 

$$
\mathsf{Seq} \hookrightarrow \mathsf{Kur} \hookrightarrow \mathcal{T}
$$

In fact, Johnstone's original paper shows that $\mathsf{Kur}$ is the 
quasitopos of $\lnot \lnot$-separated sheaves in $\mathcal{T}$! Thus 
the embedding $\mathsf{Kur} \hookrightarrow \mathcal{T}$ admits a 
finite product preserving left adjoint, and the locally cartesian closed 
structure of $\mathsf{Kur}$ agrees with that of $\mathcal{T}$. 

Concretely, this left adjoint takes an object of $\mathcal{T}$ and 
fogets _how_ a sequence converges, only remembering _which_ sequences 
converge! Said another way, it identifies any proofs $p$ and $q$ with 
$p_n = q_n$ for all $$n \in \mathbb{N}_\infty$$.

Moreover, one can show that the embedding 
$\mathsf{Seq} \hookrightarrow \mathsf{Kur}$ _also_ admits a finite product 
preserving left adjoint! This takes a limit space $X$ and gives it a 
topology whose open sets are sets $U$ so that every sequence converging to 
a point in $U$ is eventually in $U$. It's not obvious that this reflector 
preserves finite products, but you can find a proof as proposition 3.1 in 
Menni and Simpson's 
[_Topological and limit-space subcategories of countably-based equilogical spaces_][57][^18].

Thus, given any object $X \in \mathcal{T}$, we get an honest-to-goodness 
topological space by reflecting it into $\mathsf{Seq}$! This space has 
$X(1)$ as its set of points, and a subset of $X(1)$ is open exactly when 
it's "sequentially open" (as in the last paragraph).

The fact that the reflectors preserve finite products tells us that the 
$\mathsf{Seq}$ and $\mathsf{Kur}$ are [exponential ideals][58] in $\mathcal{T}$.
Thus they're both cartesian closed, and the embeddings preserve the cartesian 
closed structure!
It's not hard to see the embeddings $\mathsf{Seq} \hookrightarrow \mathsf{Kur}$ 
and $\mathsf{Kur} \hookrightarrow \mathcal{T}$ preserve coproducts, so that 
we get the promised embeddings of bicartesian closed categories.

---

This is great and all, but the only way to _really_ get some intuition for 
how computations in $\mathcal{T}$ relate to computations in $\mathsf{Top}$ 
is to actually _do some computation and check_! So let's do that!

## $\mathbb{R}$

More generally, can we see (spatial) locales as being represented by 
yoneda in $\mathcal{T}$?

<br>
## $2^\mathbb{N}$

Since $2$ and $\mathbb{N}$ are both sequential, their exponential in 
$\mathcal{T}$ agrees with their exponential in $\mathsf{Seq}$. Since 
$2$ and $\mathbb{N}$ are moreover second countable, $2^\mathbb{N}$ gets 
the compact open topology. 

Now, in the realm of classical topology, since $\mathbb{N}$ is discrete 
the compact open topology on $2^\mathbb{N}$ is just the product topology, 
so we get cantor space (as expected!)

<br>
## $$\mathbb{R} \cong (-\infty,0] +_{\{0\}} [0,\infty)$$

This is proposition 6.2 in Johnstone's paper. In $\mathsf{Seq}$ we know 
we can write $\mathbb{R}$ as a union of the (finite family of) closed 
subsets $(-\infty,0]$ and $[0,\infty)$. Then Proposition 6.2 says this 
colimit is preserved in $\mathcal{T}$.

This is interesting, because it tells us that LLPO holds in $\mathcal{T}$:

$$\forall x : \mathbb{R} . (x \leq 0) \lor (x \geq 0)$$


<br>
## $$\sum_{\alpha : 2^\mathbb{N}} \prod_{n : \mathbb{N}} \alpha(n+1) \leq \alpha(n)$$

<br>
##  $\Omega$

<br>
## $\mathcal{U}$

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
[57]: https://doi.org/10.1017/S0960129502003699
[58]: https://ncatlab.org/nlab/show/exponential+ideal
[59]: /2021/12/16/topological-categories.html

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

[^18]:
    If you want to understand how to compute (co)limits in $\mathsf{Seq}$ 
    or $\mathsf{Kur}$, I highly recommend reading Section 3 of this paper.
    It's really great, and has a lot of information!

    Particularly helpful is the observation that $\mathsf{Kur}$ is 
    <span class=defn>Topologically Concrete</span>. See my old blog 
    post [here][59], and especially Adámek, Herrlich, and Strecker's 
    _The Joy of Cats_. This book writes $\mathbf{Conv}$ where we write 
    $\mathsf{Kur}$, and shows that it's topologically concrete and 
    concretely cartesian closed! This tells us very explicitly how 
    we can compute (co)limits and exponentials in $\mathsf{Kur}$, 
    on top of the great description in Section 3 of Menni and Simpson.
