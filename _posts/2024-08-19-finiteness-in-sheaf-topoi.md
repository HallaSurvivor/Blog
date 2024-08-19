---
layout: post
title: Finiteness in Sheaf Topoi
tags:
  - topos-theory
---

The notion of "finiteness" is constructively subtle in ways that can be 
tricky for people new to the subject to understand. For a while now I've 
wanted to figure out what's going on with the different versions of "finite" 
in a way that felt concrete and obvious (I mentioned this in a few older 
blog posts [here][1] and [here][2]), and for me that means I want to 
understand them inside a sheaf topos $\mathsf{Sh}(X)$. I've thought about this 
a few times, but I wasn't able to really _see_ what was happening until a few 
days ago when I realized I had a serious misconception about picturing 
bundles and etale spaces! In this post, we'll talk about that misconception, 
and spend some time discussing constructive finiteness in its most important 
forms.

As a short life update before we get started, I'm currently in Denmark with 
[my advisor][7] to hang out with [Fabian Haiden][3]. We're going to be talking 
about all sorts of fun things related to my thesis work, mainly about 
[Fukaya Categories][4]. These can be _really_ scary when 
you first start reading about them, but in the special case of surfaces 
they're really not that bad! In the process of prepping for meeting Fabian, 
I've been writing a blog post that explicitly details what fukaya categories 
are, why you should care, and (for surfaces) how to compute them. I know I 
would have loved an article like this, and I'm excited to share one soon!
I'm also _finally_ going to finish my [qual prep series][5] from 
_three years ago_! Way back then I promised a post on fourier theory
that I never got around to, but I recently found a draft of that post! 
So it might not be 100% true to what I was studying back then, but it'll be 
as true to that as I can make it[^1].

With all that out of the way, let's get to it!

---

First, let's just recall the notions of finiteness you're likely to 
find in the literature[^2]. Keep in mind that, depending on the reference 
you're reading, each of these is liable to be called just "finite" 
without disambiguation. Sometimes you even get more confusing conventions, 
(such as writing "subfinite" to mean what we call "kuratowski finite"!)
so make sure you read carefully to know exactly what each particular 
author means! For this post, though, we'll write:

If $n : \mathbb{N}$, the <span class=defn>Finite Cardinal</span> of size $n$ 
is the set $$[n] = \{ x : \mathbb{N} \mid x \lt n \}$$. 

A set $X$ is called <span class=defn>Bishop Finite</span> if it's (locally)
isomorphic to a cardinal. That is, if 
$$\exists n : \mathbb{N} . \exists f : X \cong [n]$$

A set $X$ is called <span class=defn>Kuratowski Finite</span> if it's 
(locally) the image of a cardinal. That is, if 
$$\exists n : \mathbb{N} . \exists f : [n] \twoheadrightarrow X$$.

A set $X$ is called <span class=defn>Subfinite</span> if it's (locally) a 
subobject of a cardinal. That is, if 
$$\exists n : \mathbb{N} . \exists f : X \hookrightarrow [n]$$.

A set $X$ is called <span class=defn>Dedekind Finite</span> if every 
mono $X \hookrightarrow X$ is actually an iso. That is, if we can prove 
$$\forall f : X \hookrightarrow X . \exists g : X \to X . fg = 1_X \land gf = 1_X$$.

It's pretty obvious from these definitions that dedekind finiteness is 
a bit different from the others. This comes with pros and cons, but in my 
experience it's rarely the thing to consider. I'm including its definition 
more for cultural growth than anything, and I won't say anything more about 
it in this post[^3].

Also, notice we're putting an existential quantifier in front of everything. 
Externally, this means that we're allowed to pass to an open cover 
of our base space and use a different $f$ (or indeed, a different $n$!) 
on each open. If you prefer type theory[^4], you can replace every instance of 
$\exists$ by the [propositional truncation][9] of a $\Sigma$-type.

It's interesting to ask what the "untruncated" versions of these will be. 
I think that untruncated bishop finite types are exactly the cardinals, 
untruncated subfinite types are disjoint unions of finitely many propositions... 
But it's not clear to me what the untruncated kuratowski finite types should be.
Something like "finitely many copies of $B$, glued together along open 
sets"... But I don't see a snappy characterization of these[^5].

---

## Introducing Finiteness

Now, how should we go about _visualizing_ these things? Every sheaf on $B$ 
is also an [etale space][10] over $B$ 
(that is, a local homeomorphism[^6] $E \to B$).
And by thinking of our favorite sheaf as some space over $B$
we can draw pictures of it!

<br>

Let's start simple and let $B = [-1,1]$ be an interval. Then a cardinal[^12] 
is a sheaf $$[n] = \{x : \mathbb{N} \mid x \lt n \}$$. In every sheaf 
topos $\mathsf{Sh}(B)$ the natural number object is (the sheaf of sections of) 
$B \times \mathbb{N}$ where $\mathbb{N}$ gets the discrete topology. 

<p style="text-align:center;">
<img src="/assets/images/finiteness-in-sheaf-topoi/N-covering-interval.png" width="50%">
</p>

So if $n$ is a global section, it must be $$B \times \{ n \}$$ for some fixed $n$ 
in "the real world". This also tells us that 
$$[n] = \{ x : \mathbb{N} \mid x \lt n \}$$ is given by 

<p style="text-align:center;">
<img src="/assets/images/finiteness-in-sheaf-topoi/interval-n.png" width="50%">
</p>

The situation is only slightly more complicated if $B$ has multiple 
components[^7] (say $B = [-1,1] \sqcup S^1$). In this case, $\mathbb{N}$ 
is still $B \times \mathbb{N}$, but now global sections can choose a different 
natural over each component:

<p style="text-align:center;">
<img src="/assets/images/finiteness-in-sheaf-topoi/2-3-interval-and-circle.png" width="50%">
</p>

Because of this, we end up with more sets $[n]$! Indeed, now a global section 
$n$ might be something like $(2,3)$ (shown in pink above) 
so that we get a cardinal $[(2,3)]$, shown below:

<p style="text-align:center;">
<img src="/assets/images/finiteness-in-sheaf-topoi/cardinal-2-3.png" width="50%">
</p>

So cardinals are _really really_ easy to work with! This is what we 
would expect, since they're subsheaves of a particularly simple sheaf ($\mathbb{N}$). 
For instance, we can _see_ the fact that cardinals always have 
[decidable equality][12] by noticing that any two sections over $U$ are 
either equal on all of $U$, or none of $U$! Contrast this with a doodle 
of what other sheaves might look like, where the pink and blue sections are 
different, but nonetheless intersect. Then the truth value of 
$(\text{pink} = \text{blue}) \lor (\text{pink} \neq \text{blue})$ 
as computed in $\mathsf{Sh}([-1,1]) \big / U$ will not be all of $U$[^19]!

<p style="text-align:center;">
<img src="/assets/images/finiteness-in-sheaf-topoi/intersecting-or-not-intersecting-over-interval.png" width="75%">
</p>

We also _see_ why a cardinal is either empty or inhabited! As soon as you 
have a _piece_ of a section over $U$, it must extend to a section on all 
of $U$.

<br>

Next up are the bishop finite sets[^20]! These satisfy $\exists f : X \cong [n]$,
so that we can find an open cover $$\{U_\alpha \}$$ of $B$ and functions 
$$f_\alpha : X \! \upharpoonright_\alpha \cong [n] \! \upharpoonright_\alpha$$.

Since $[n]$ is a _constant_ family over $B$, this means we want $X$ to be 
_locally constant_. So bishop finite sets have to basically 
look like cardinals, but now we're allowed to "twist" the fibres around.
See how on each element of our cover we have something that looks like $\[2]$,
but globally we get something that is _not_ isomorphic to $\[2]$!

<p style="text-align:center;">
<img src="/assets/images/finiteness-in-sheaf-topoi/double-cover-locally-constant.png" width="50%">
</p>

In fact, the bishop finite sets are exactly the [covering spaces][13] with 
finite fibres. These inherit lots of nice properties from the cardinals, 
since as far as the internal logic is concerned they're isomorphic to 
cardinals!

For instance, here's an internal proof that bishop finite sets have 
decidable equality:

$\ulcorner$
We know $\exists f : X \cong [n]$. Fix such an $f$, and let $x,y : X$. 
Since $f$ is an isomorphism we know $x=y$ if and only if $fx = fy$, 
but we can decide this using decidable equality on $[n]$ 
(which comes from decidable equality on $\mathbb{N}$, which we prove by 
induction).
<span style="float:right">$\lrcorner$</span>

We can also _see_ this externally. As before, this is saying that two
sections over $U$ either agree everywhere or nowhere 
(and it's a cute exercise to see this for yourself).
But we can even see this in a _third way_! It says that the subsheaf 
$$\{(x,y) : X \times X \mid x=y \}$$ is a clopen subset of $X \times X$!
But we can compute $X \times X$ (the pullback of $X \to B$ along $X \to B$)
and check this. 

<p style="text-align:center;">
<img src="/assets/images/finiteness-in-sheaf-topoi/double-cover-double-pullback.png" width="75%">
</p>

Note that the subsheaf (really sub-etale space) where the fibres are the same 
really is a clopen subset (read: a connected component) of the whole space 
$X \times X$ over $B$. If it's not obvious that this really _is_ the 
pullback, it makes a fun exercise! Actually, it's a fun exercise to check 
this is true in general! 

As a last remark, let's also notice that bishop finite sets can be 
_inhabited_ without being _pointed_. That is, a bishop finite set $X$ can 
satisfy $\exists x : X$ ($X$ is inhabited[^14]) without actually having $x:X$ for any $x$
($X$ is not pointed)! This is because of the locality of the existential 
quantifier again! If we pass to an open cover of $B$, we can find a local 
section over each open. Unfortunately, these might not be compatible, so 
won't glue to a _global_ section (a point $x:X$)!

<p style="text-align:center;">
<img src="/assets/images/finiteness-in-sheaf-topoi/double-cover-not-pointed.png" width="50%">
</p>

<br>

Ok, now let's get to the example that led me to write this post!
How should we visualize kuratowski finite sets? These are (locally) 
_quotients_ of cardinals, so we start with a cardinal 
(which we know how to visualize) and then we want to start gluing stuff 
together.

Let's start with a trivial double cover of $B = [-1,1]$ 
(that is, with two copies of $B$), and glue them together along their 
common open subset $[-1,0) \cup (0,1]$. This space is the 
[line with two origins][14], and it's famously 
_nonhausdorff_!

<p style="text-align:center;">
<img src="/assets/images/finiteness-in-sheaf-topoi/two-origins.png" width="75%">
</p>

You can see that this space still deserves to be called "finite" 
over $B$ (for instance, all the fibres are finite), but it's more 
complicated than the bishop case. For instance, it doesn't have a 
well defined "cardinality". In some places it has one element in the fibre, 
and in others it has two. However, it's still possible to _list_ or 
_enumerate_ all the sections. In the above picture, there's the gold 
section and the blue section. It just happens that sometimes this list
has duplicates, since away from $0$ they're the same section!

The failure of hausdorffness and the failure of decidable equality are 
closely related. For example, consider the two sections from the previous 
picture. Decidable equality says that they should be either everywhere 
equal or everywhere unequal[^21]. But of course they aren't! They're 
equal in some places (over $1$, say) but unequal in others (over $0$)!

Following [Richard Borcherds][15], hausdorffness is 
also closely related to a kind of "analytic continuation". Indeed, say your 
etale space $X$ is hausdorff and you pick a point $x_b$ over $b \in B$ 
(in this context we think of $x_b$ as the germ of a function at $b$).
Then for any small enough open $U \ni b$, there is a _unique_ extension of 
$x_b$ to a function on the whole neighborhood $U$! We are able to 
_analytically continue_ $x_b$ from data at just a point to data defined in 
some neighborhood! 

<div class=boxed markdown=1>
Here's an easy exercise to see this for yourself and check your knowledge 
of the topology on the etale space of a sheaf:

Let $\mathcal{F}$ be a sheaf on $B$ whose etale space $X$ is hausdorff,
and let $U$ be a connected open of $X$.
Let $f,g \in \mathcal{F}(U)$ be local sections with $f(b_0) = g(b_0)$ 
for some $b_0 \in U$. Then show $f=g$ identically on $U$.

As a hint, consider the set $$\{ b \in U \mid f(b) = g(b) \}$$.
Why is it open? Why is it closed?

In fact, if $B$ is locally connected and hausdorff, then 
the converse is also true, and our sheaf of sections $\mathcal{F}$
has this analytic continuation property if and only if its etale 
space is hausdorff[^9]! This also makes a nice exercise 
(though it's less easy), and I'll include a solution below a fold.
</div>

<details>
    <summary>solution</summary>
    $\ulcorner$
    <p>
    First assume $\mathcal{F}$ has a hausdorff etale space $X$. 
    Then for sections $f,g : U \to X$ we see that the set 
    $\{b \in U \mid f(b) = g(b) \}$ is closed, as the preimage 
    of the closed diagonal in $X$. This set is also open since if 
    $f(b) = g(b)$ is the stalk at $b$, the 
    <a href="https://stacks.math.columbia.edu/tag/0078">definition of stalk</a>
    says 
    that $f=g$ on a neighborhood of $b$. Since $U$ is connected, we 
    learn this subset is the whole of $U$ and $\mathcal{F}$ has 
    analytic continuation.
    </p>

    <p>
    Conversely, assume $\mathcal{F}$ has analytic continuation, and 
    let $x,y \in X$ be two points. If $x$ and $y$ are in different fibres 
    (say $x$ is over $b_x$ and $y$ is over $b_y$) then we can separate 
    $b_x$ and $b_y$ using hausdorfness of $B$, and any representatives
    of $x$ and $y$ defined on these separating sets will separate $x$ and $y$ 
    in $X$. So we're left with the case of $x$ and $y$ both living in the same
    fibre over $b$.
    </p>

    <p>
    Say that every neighborhood of $x$ intersects every neighborhood of $y$.
    Using local connectedness of $B$, we can find a connected neighborhood $U$ 
    of $b$, and representatives $(f,U)$ and $(g,U)$ of $x$ and $y$. These 
    define open sets in the topology of $X$, and since neighborhoods of $x$ 
    and $y$ always intersect, we know there's a $b' \in U$ with $f(b') = g(b')$.
    Then analytic continuation says $f=g$ on $U$ so that $x = f(b) = g(b) = y$,
    and $X$ is hausdorff, as desired.
    </p>
    <span style="float:right">$\lrcorner$</span>
</details>

<br>

When I was trying to picture kuratowski finite objects inside $\mathsf{Sh}(B)$,
I'd somehow convinced myself that a local homeomorphism over a hausdorff 
space has to itself be hausdorff. This is, obviously, not true! So I was 
trying to picture kuratowski finite sets and struggling, because I was only 
ever picturing hausdorff covering spaces. And we'll see later that all 
hausdorff kuratowski finite sheaves (over spaces I was picturing) are 
actually bishop finite! So it's no wonder I was confused! I didn't realize 
the complexity (especially the nonhausdorff complexity) that etale spaces 
are allowed to have, even though in hindsight I'd been warned about this 
before[^17].

Going back to examples, we should ask if we recognize the sheaf of 
sections for our favorite "line with two origins" picture from earlier.
Away from $0$, we know there's exactly one section, but in any neighbordhood 
of $0$ there's two sections. So we see this is the etale space for the 
[skyscraper sheaf][17] with two points over $0$!

Since our epi $[n] \twoheadrightarrow X$ only has to exist locally, 
kuratowski finite objects in $\mathsf{Sh}(B)$ can have the same twisting 
behavior as bishop finite sets too!

<p style="text-align:center;">
<img src="/assets/images/finiteness-in-sheaf-topoi/twisted-cover-with-skyscrapers.png" width="50%">
</p>

If you look up an example of a kuratowski finite set that isn't 
bishop finite (for example, in Section 2.2.2 of Graham Manuell's 
excellent [note][18]), you're likely to find the example 
$$\{ \top, p \}$$ where $p$ is some truth value other than 
$\top$ or $\bot$. That is, where $p$ is some open set of the base 
space $B$.

Away from $p$, this set has two elements, $\top$ and $p$ 
(since away from $p$ we know $p = \bot$). But inside of $p$, this 
set has a single element (since in $p$ we know $p = \top$). We find its 
etale space is nonhausdorff as before, but now the nonhausdorffness is 
"spread out" over a larger set. It's a good exercise to figure out what's 
happening at the boundary of $p$. What are the basic opens of this space? 
Does the fibre at $p$ have one point, or two?

<p style="text-align:center;">
<img src="/assets/images/finiteness-in-sheaf-topoi/true-and-p.png" width="75%">
</p>


Kuratwoski finite sets can be shockingly complicated! 
Especially in contrast to the relatively tame 
bishop finite sets. For example, consider $B = \mathbb{R}$ with a skyscraper 
sheaf at every integer[^11]:

<p style="text-align:center;">
<img src="/assets/images/finiteness-in-sheaf-topoi/skyscrapers-at-integers.png" width="75%">
</p>

This space is kuratowski finite in $\mathsf{Sh}(\mathbb{R})$ 
(since it's locally a quotient of $\mathbb{R} \sqcup \mathbb{R}$), 
but it has continuum many global sections! Indeed, we can choose either the 
top or the bottom point at every integer.

Since even the choice of $[n]$ is local, we can change the size of the 
fibres as long as they're all finite!

<p style="text-align:center;">
<img src="/assets/images/finiteness-in-sheaf-topoi/increasing-skyscrapers.png" width="75%">
</p>

In fact, on mastodon ([here][21] and [here][22]), Antoine Chambert-Loir and 
Oscar Cunningham pointed out that you can do even weirder things. For instance,
the set $$\{\frac{1}{n} \mid n \in \mathbb{N} \} \cup \{ 0 \}$$ is closed 
in $[0,1]$. So its complement is open, and we can glue two copies of $[0,1]$ 
together along it! This gives us a kuratowski finite object which nonetheless 
has infinitely many sections in _every neighborhood of $0$_[^18]!

<p style="text-align:center;">
<img src="/assets/images/finiteness-in-sheaf-topoi/convergent-seq-of-skyscrapers.png" width="75%">
</p>

<br>

Finally, let's talk about subfinite sets. These are locally subobjects of 
cardinals, so are much easier to visualize again!

A subobject of a cardinal is just a disjoint union of open subsets of $B$:

<p style="text-align:center;">
<img src="/assets/images/finiteness-in-sheaf-topoi/subfinite-simple.png" width="75%">
</p>

So a subfinite set has to locally look like these. Keep in mind, though,
that like kuratowski finite sets, the choice of $[n]$ is made locally. So 
we can have something like this:

<p style="text-align:center;">
<img src="/assets/images/finiteness-in-sheaf-topoi/increasing-subfinite.png" width="75%">
</p>

In particular, we see that the fibres of a subfinite set don't need to be 
globally bounded! So, perhaps surprisingly, a subfinite set does _not_ need to be 
a subobject of a bishop finite set! 

As we've come to expect, the existential quantifier gives us the ability 
to twist.

<p style="text-align:center;">
<img src="/assets/images/finiteness-in-sheaf-topoi/twisted-subfinite.png" width="50%">
</p>

As subobjects of decidable objects, we see these inherit decidable 
equality. However, while bishop and kuratowski finite objects are all either 
empty or inhabited, subfinite sets don't need to be! For an easy example, 
consider 

<p style="text-align:center;">
<img src="/assets/images/finiteness-in-sheaf-topoi/undecidable-inhabitance.png" width="50%">
</p>

Here the truth value of $\exists x : X$ is $U \cup V$, and the truth value 
of $X = \emptyset$ is $\text{int}(U^c \cap V^c)$. (Do you see why?)

---


## An aside on decidable equality

This isn't _technically_ about visualizing etale spaces, but I was thinking 
about it while writing this post, and I think it fits well enough to 
include. If nothing else, it's _deifnitely_ interesting enough to include!

If you're really paying attention, you'll notice the "easy exercise" 
about analytic continuation didn't actually use any aspects of finiteness. 
Indeed, we can prove the following (very general) theorem:

<div class=boxed markdown=1>
Let $B$ be locally connected and hausdorff. Then the following 
are equivalent for a sheaf $\mathcal{F}$ on $B$:

1. The etale space of $\mathcal{F}$ is hausdorff 
2. Sections of $\mathcal{F}$ satisfy "analytic continuation", in the 
sense that two sections agreeing on a stalk[^10] must agree everywhere 
they're defined 
3. $\mathcal{F}$ has decidable equality in the internal logic of $\mathsf{Sh}(B)$

This comes from a [mathoverflow answer][16] by Elías Guisado Villalgordo
</div>

$\ulcorner$
The equivalence of $1$ and $2$ was the earlier exercise, and you can find 
a proof below it under a fold/

To check the equivalence of $2$ and $3$, we look at "decidable equality",
that $\forall f,g : \mathcal{F} . (f=g) \lor (f \neq g)$.

Externally, this says that for every $U$, for every pair of local sections 
$f,g \in \mathcal{F}(U)$, there's an open cover $$\{U_\alpha\}$$ so that 
on each member of the cover 
$$f \! \upharpoonright_{U_\alpha}$$ and $$g \! \upharpoonright_{U_\alpha}$$ 
are either everywhere equal or everywhere unequal.

Clearly if $\mathcal{F}$ has analytic continuation then $\mathcal{F}$ has 
decidable equality. Indeed using local connectedness of $B$ we can cover 
$U$ by connected opens. By analytic continuation we know that on each 
connected piece either $f=g$ everywhere or nowhere, as desired.

Conversely, say $\mathcal{F}$ has decidable equality. Fix a connected $U$ 
and sections $f,g \in \mathcal{F}(U)$ which have the same stalk at some point 
$b \in U$. By decidable equality, there's an open cover $$\{ U_\alpha \}$$ 
of $U$ where on each member of the cover $f=g$ holds everywhere or nowhere.
[Recall][20] that since $U$ is connected, for any two opens in the cover 
$U_\alpha$ and $U_\beta$ we can find a finite chain 
$U_\alpha = U_0, U_1, U_2, \ldots, U_n = U_\beta$ of opens in our cover where 
each $U_i$ intersects $U_{i+1}$.

Then for any $U_\beta$ in the cover, fix such a chain from $U_0 \ni b$ to 
$U_\beta$. By decidable equality we know $f=g$ on $U_0$. So for the point 
in $U_0 \cap U_1$ we know $f=g$, and by decidable equality again we learn 
$f=g$ on $U_1$. Proceeding in this way we learn $f=g$ on the whole of $U_\beta$.

Thus $f=g$ on every member of the cover, so on the whole of $U$, and so 
$\mathcal{F}$ satisfies analytic continuation.
<span style="float:right">$\lrcorner$</span>

<br>

If you've internalized this, it makes it geometrically believable that a 
decidable kuratowski finite set is actually bishop finite! 
I think it's fun to see this fact both _syntactically_ 
(reasoning in the internal logic) and _semantically_ 
(reasoning about bundles), so let's see two proofs!

First, a <span class=defn>syntactic proof</span>:

$\ulcorner$
Say $f : [n] \twoheadrightarrow X$. Then we note for each $x:X$ the 
predicate $\varphi(k) \triangleq f(k) = x$ on $[n]$ is decidable 
since $X$ has decidable equality. Thus it gives an inhabited decidable subset 
of $[n]$, which has a least element (Lemma D5.2.9(iii) in the elephant).
Call such an element $g(x)$.

Note the image of $g$ is a [complemented subset][25] of $[n]$, since we can decide 
$k \in \text{im}(g)$ by checking if $k = g(f(k))$ using decidability of $[n]$.
Then $\text{im}(g)$ is isomorphic to a cardinal (D5.2.3), $[m]$, and it's easy 
to see that composing $g$ and $f$ with this isomorphism gives a bijection 
between $X$ and $[m]$.
<span style="float:right">$\lrcorner$</span>


And now a <span class=defn>semantic proof</span>:

$\ulcorner$
Say $\pi : E \twoheadrightarrow B$ is the etale space of a kuratowski finite 
object in $\mathsf{Sh}(B)$. So, locally, $E$ is the quotient of some 
$\coprod_n B$. Say also that $E$ is has decidable equality so that, locally, 
two sections of $E$ that agree somewhere must agree everywhere. 

By refining our covers, then, we may fix an open cover $$\{U_\alpha\}$$ of $B$
and epimorphisms 
$$\coprod_{n_\alpha} U_\alpha \to E \! \upharpoonright_{U_\alpha}$$ so that 
two local sections on $U_\alpha$ either agree everywhere or nowhere. 
In particular, the $n_\alpha$ many components 
$f_i : U_\alpha \overset{i\text{th inclusion}}{\longrightarrow} \coprod_{n_\alpha} \to E$ 
are pairwise either have the same image or disjoint images. Choosing exactly 
one $f_i$ for each possible image (the least $i$ that works, say) we see that actually 
$\pi^{-1}(U_\alpha)$ is homeomorphic to the disjoint union of copies of 
$U_\alpha$ so that $E$ is actually a covering space, and thus represents a 
bishop finite object.
<span style="float:right">$\lrcorner$</span>

<div class=boxed markdown=1>
It's worth meditating on why these are actually the same proof! 
In both cases we use decidability to "remove duplicates" from our 
enumeration.
</div>

---

## Which Finite to Use?

Constructively, bishop and kuratowski finiteness encode two aspects of 
finiteness which are conflated in the classical finite world. Bishop finite 
sets are those which admit a cardinality. They're in bijection with some 
$[n]$, and so have a well defined notion of _size_. Kuratowski finite sets, 
in contrast, are those equipped with an _enumeration_. You can list 
all the elements of a kuratowski finite set.

Of course, knowing how to biject a set $X$ with a set $[n]$ always tells 
you how to enumerate $X$. But constructively knowing how to enumerate $X$ 
doesn't tell you how to biject it with some $[n]$! As we saw earlier,
the problem lies with removing duplicates. It's worth taking a second 
to visualize a kuratowski finite set that isn't bishop finite, and convince 
yourself that the question "is this a duplicate element" can have more 
subtle answers than just "yes" or "no". This makes it impossible to remove 
the duplicates.

This bifurcation might feel strange at first, but in some squishy sense it 
happens classically too once you start working with _infinite_ sets. 
Indeed in set theory the notion of finiteness bifurcates into 
[cardinals][23], which have a defined notion of "size", and 
[ordinals][24], which have a defined notion of "order" 
(kind of like an enumeration... if you squint).

So when you're working constructively, ask why you're using finiteness. 
Do you _really_ need to know that something literally has $n$ elements 
for some $n$? Or is it enough to know that you can put the elements 
in a finite list? Does it matter if your list has duplicates? 
These questions will tell you whether bishop finiteness or kuratowski 
finiteness is right for your purposes.

Subfiniteness, which amounts to being contained in some $[n]$, I find 
to be less useful "in its own right". Instead, if you're able to prove 
a result for bishop finite objects, it's worth asking if you can strengthen 
that to a proof for subfinite ones!

In any case, as long as we work with _decidable_ things, these notions 
all coincide. As we saw earlier, a decidable quotient of a bishop finite 
set (that is, a decidable kuratowski finite set) is again bishop finite.
Similarly, a complemented subset of a bishop finite set is finite 
(this is lemma D5.2.3 in the elephant, but it's not hard to see yourself).
So if you're working in a context where everything is decidable, finite sets 
work exactly as you would expect! This is part of why constructive math 
doesn't have much to say about combinatorics and algebra. Most arguments 
are _already_ constructive for decidable finite sets (which is what you're 
picturing when you picture a finite set and do combinatorics to it). 
Sometimes you can push things a bit farther though, and this can be interesting. 
See, for instance, Andreas Blass's paper on the 
[Constructive Pigeonhole Principle][19]. 

---

Another blog post done! I'm writing this on a train to Odense right now, 
and once I get to my room I'll draw all the pictures and post it.

Hopefully this helps demystify the ways in which constructive math might 
look strange at first. Once again the seemingly bizarre behavior is explained 
by its _vastly_ greater generality! When you 
first learn that a subset of a (bishop) finite set need not be (bishop) finite, 
it sounds so strange as to be unusable! But once you learn that this is an 
aspect of "everywhere definedness" in a space of parameters 
(read: the base space) it becomes much more palatable.

Thanks, as always, for hanging out. Try to keep cool during this summer 
heat (though it's actually _really_ pleasant in Denmark right now), 
and I'll see you all soon ^_^.

Here's a picture of me and Peter right after we got off the train:

<p style="text-align:center;">
<img src="/assets/images/finiteness-in-sheaf-topoi/me-and-peter.jpg" width="75%">
</p>

---

[1]: /2024/03/25/continuous-max-function.html
[2]: /2022/12/13/internal-logic-examples
[3]: https://semistability.wordpress.com/
[4]: https://ncatlab.org/nlab/show/Fukaya+category
[5]: /tags/analysis-qual-prep/
[6]: /tags/life-in-the-topological-topos/
[7]: https://sites.google.com/view/petersamuelson/home
[8]: https://doi.org/10.1016/0022-4049(87)90130-7
[9]: https://ncatlab.org/nlab/show/bracket+type
[10]: https://ncatlab.org/nlab/show/%C3%A9tale+space
[11]: https://en.wikipedia.org/wiki/Locally_connected_space
[12]: https://ncatlab.org/nlab/show/decidable+equality
[13]: https://en.wikipedia.org/wiki/Covering_space
[14]: https://ncatlab.org/nlab/show/line+with+two+origins
[15]: https://www.youtube.com/watch?v=aYzQJvIchjg
[16]: https://mathoverflow.net/a/440985/145247
[17]: https://ncatlab.org/nlab/show/skyscraper+sheaf
[18]: http://arxiv.org/abs/2304.06000
[19]: https://doi.org/10.2307/2275881
[20]: https://math.stackexchange.com/questions/1480639/connected-space-and-open-coverings
[21]: https://sunny.garden/@hallasurvivor/112961631080132543
[22]: https://sunny.garden/@hallasurvivor/112972328466131542
[23]: https://en.wikipedia.org/wiki/Cardinal_number
[24]: https://en.wikipedia.org/wiki/Ordinal_number
[25]: https://ncatlab.org/nlab/show/complemented+subobject
[26]: https://www.youtube.com/watch?v=vmcbm5FxRJE

[^1]:
    And, of course, I still really want to finish the blog post on 
    2-categories and why you should care... There's just _so_ many 
    other things to think about and to write! It also feels like a 
    big topic because I have a lot to say, and that makes me a bit 
    scared to actually start. Especially since I've been writing a 
    lot of longer form posts lately (like the three part series on 
    the [topological topos][6], and I can tell the fukaya post is 
    going to be long too...)

[^2]:
    Here we're using the expected abbreviations. 

    We write $f : X \cong Y$ to mean $f : X \to Y$ and 
    $\exists g : Y \to X . gf = 1_X \land fg = 1_Y$.

    We write $f : X \hookrightarrow Y$ to mean $f : X \to Y$ and 
    $\forall x_1, x_2 : X . fx_1 = fx_2 \to x_1 = x_2$

    We write $f : X \twoheadrightarrow Y$ to mean $f : X \to Y$ and 
    $\forall y : Y . \exists x : X . fx = y$.

[^3]:
    If you want to learn more about it, I highly recommend 
    Stout's [_Dedekind Finiteness in Topoi_][8]. I don't know of a 
    good way to visualize the dedekind finite objects in $\mathsf{Sh}(X)$
    (though I haven't tried at all -- I want this to be a quick post) which 
    was another reason to exclude them.

[^4]:
    Which I often do, but not today.

[^5]:
    And I want this to be a quick post, finished within a day or two 
    of starting. So I don't have time to think if there's something 
    slicker (and intuitively I don't expeect there to be).

    **Edit:** I got about as close to "within a day or two" 
    as is possible for me, haha.
    I started writing this on August 12, and it looks like I'll 
    get it posted on August 18. Given I went a few days without 
    working on it, that's not too bad!

[^6]:
    That is, a space built by gluing together opens of $B$ along common 
    intersections

[^7]:
    We'll still assume that $B$ is [locally connected][11], though, 
    since that makes them much easier to draw.

    It's important to remember that our geometric intuition is likely to 
    fail us if we start considering, say, sheaves on the cantor space!

[^9]:
    I stole this whole exercise from [this mathoverflow answer][16] by 
    Elías Guisado Villalgordo

[^10]:
    Saying that $f$ and $g$ agree on the stalk at $b$ is saying that 
    there's an open neighborhood of $b$ where $f=g$ on that neighborhood.

    So this is another way of saying that as soon as two sections agree 
    on an arbitrarily small neighborhood, they must agree on their whole 
    (connected) domain!

[^11]:
    Concretely you can build this space by gluing two copies of $\mathbb{R}$ 
    together along their common open subset $\mathbb{R} \setminus \mathbb{Z}$.

[^12]:
    Johnstone's Elephant defines a cardinal to be a pullback of the 
    "universal cardinal". In $\mathsf{Sh}(B)$ this is an object in 
    $\mathsf{Sh}(B) \big / \mathbb{N} \simeq \mathsf{Sh}(B \times \mathbb{N})$ 
    and is shown in the following picture:

    <p style="text-align:center;">
    <img src="/assets/images/finiteness-in-sheaf-topoi/generic-cardinal.png" width="60%">
    </p>

[^14]:
    Here we use the common abuse of notation of abbreviating 
    "$\exists x:X . \top$" by just "$\exists x:X$". It measures 
    "to what extent" there exists an element of $X$. That is, 
    its truth value is the _support_ of $X$ over $B$ -- 
    $$\text{int} \big ( \{b \in B \mid \exists x \in X_b \} \big )$$

[^15]:
    To make this easier on people new to this stuff, note the equalizer 
    of $f,g : [m] \rightrightarrows [n]$ is given by 
    $$\{x : [m] \mid f(x) = g(x) \}$$. Since equality in $[n]$ is decidable, 
    $f(x) = g(x)$ is a decidable proposition on $[m]$, so the subset it 
    classifies is complemented.

[^16]:
    Either in the sense that the quotient object itself is decidable, or that 
    the defining equivalence relation is decidable as a subset of $[n] \times [n]$.

[^17]:
    In that same [Richard Borcherds video][15], for instance, which I 
    know I watched when it came out. In fact, lots of references on etale 
    spaces, in hindsight, emphasize the fact that etale spaces can be 
    highly nonhausdorff. My guess is that I'm not the first person
    to have made this mistake, haha, and I know that when I teach etale 
    spaces going forwards I'm going to be sure to emphasize this too!

    In his talk [_Nonetheless One Should Learn the Language of Topos_][26],
    Colin McLarty compares etale spaces to a piece of mica 
    (around the 1h04m mark), and I think I'm starting to see what he means.

[^18]:
    This is a fun example to think about. Why does it have only _countably_ 
    many sections at $0$, rather than _uncountably_ many? Can you picture 
    its topology at all? See the linked mastodon posts for more discussion.

[^19]:
    Remember truth values are open sets in the base space, so the truth 
    value of $(\text{pink} = \text{blue}) \lor (\text{pink} \neq \text{blue})$ 
    will be $$\text{int}(\{ \text{pink} = \text{blue} \}) \cup 
    \text{int}( \{ \text{pink} \neq \text{blue} \} )$$

[^20]:
    I'm like... at least 90% sure it's an accident these are both named 
    after positions of authority in catholicism.

[^21]:
    Well, it says this should be true locally. But it's easy to see 
    we'll have a problem in any neighborhood of $0$.
