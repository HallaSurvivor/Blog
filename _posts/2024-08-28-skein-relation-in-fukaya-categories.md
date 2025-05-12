---
layout: post
title: The Skein Relation in the Hall Algebra of a Fukaya Category
tags:
  - my-thesis
---

Based on my usual blog posts, people might think that my thesis work 
is on constructive math, topos theory, and related ideas. But in fact 
I'm writing my thesis on a circle of ideas in [Quantum Algebra][2], 
relating [Skein Algebras][1], [Fukaya Categories][3], and 
[Hall Algebras][4]! I haven't blogged much about it since these topics 
can be pretty intimidating, and I wanted to wait until I felt like I 
understood them well before trying to explain them to others. I'm happy 
to say that I'm finally feeling confident enough to do that, and I'm planning
to write some blog posts on all of these topics! I want this post to be 
a sort of appetizer for my thesis work, where I'll explain _very_ roughly 
what's going on with all the ideas, and the surprising connection that my 
advisor and I are interested in.

I'm writing this on a plane ride from London back to New York after 
spending some time with [Fabian Haiden][5] at the Center for Quantum 
Mathematics in Odense. I had a great time, and I _loved_ Denmark. 
I've been traveling for a while now, though, so I'm very exited to be 
headed back to my own bed!

Let's get started!

---

First, let me say a few words about Skein Algebras.

Say you have a 3-manifold $M$. Then a <span class=defn>Link</span> in $M$ 
is a smooth function from a bunch of $S^1$s into $M$. You should think of 
this as a bunch of knots which you've _linked_ together.

<div class=boxed markdown=1>
TODO: a picture of a link in $\mathbb{R}^3$
</div>

In case $M = \mathbb{R}^3$ (which is just about the only $3$-fold I can visualize),
then there's a famous invariant of a link called its [Jones Polynomial][6], 
and an equally famous method for computing the invariant from a knot diagram
(which I believe is due to John Conway):

Start with a diagram of your link and every time you see a crossing, 
you're allowed to pass one strand through the other as long as you add a 
new term to your polynomial coming from the "resolution" of the intersection. 
This is best shown by an example[^1], so let's do one together!

<div class=boxed markdown=1>
TODO: a worked out example computing the jones polynomial for the trefoil knot
</div>

This can be pretty fun to work out, actually, and I encourage you to compute 
the jones polynomial of a hopf link (shown below). You should get 

TODO: compute this, lol

<div class=boxed markdown=1>
TODO: a hopf link
</div>

We want a way to make this work for more general $3$-folds $M$, and the 
standard approach is to look at the free $k[q^\pm]$-module spanned by links in 
$M$ up to isotopy. Then you quotient by all local instances of Conway's relation 

TODO: this "conway relation" is the "kauffman relation", right?

<div class=boxed markdown=1>
TODO: The Skein Relation
</div>

TODO: revise footnote 4

This gives the ($SL_2$-)[^4]<span class=defn>Skein Module</span> $\text{Sk}(M)$. 
In case $M = \mathbb{R}^3$ then $\text{Sk}(M)$ is one dimensional, spanned by the 
unknot $\bigcirc$. Then if $L$ is a link in $\mathbb{R}^3$ its class in 
$\text{Sk}(\mathbb{R}^3)$ is just the jones polynomial times $\bigcirc$.

In this way, a link in $M$ gets sent to some class in $\text{Sk}(M)$ 
and this vector (read: the coefficients in some nice basis) are generalizations 
of the jones polynomial to links in a general $3$-fold $M$!

<br>

But the attentive reader might be wondering what happened to the skein 
_algebra_. Well, if you have a surface $S$ and you compute 
$\text{Sk}(S \times \mathbb{R})$ you get a module, of course, but now 
we have a way to multiply! We can "stack" links (really classes of links) 
in the $\mathbb{R}$-direction!

<div class=boxed markdown=1>
TODO: a picture
</div>

This is associative because it doesn't matter, up to isotopy, if we 
repeatedly stack

<div class=boxed markdown=1>
TODO: a picture of this
</div>

But this _isn't_ commutative since we might not be able to swap which 
link is on the "inside":

<div class=boxed markdown=1>
The two obvious knots in a torus, which witness noncommutativity
</div>

There's a more nuanced story to tell here, which I'm glossing over. 
This algebra structure is really an [$E_1$ Algebra][7], and in case 
you make your $3$-fold even _more_ trivial (by taking a $1$-fold and 
crossing with $\mathbb{R}^2$) you get an $E_2$ Algebra! In particular, 
in this case the algebra will be commutative, basically because of the 
[Eckmann-Hilton Argument][8]:

<div class=boxed markdown=1>
TODO: $X \times \mathbb{R}^2$, move the knots around each other
</div>

TODO: say something about T(Q)FTs here. This hopefully serves as 
motivation for thinking about this stuff.

TODO: if $S$ is part of the boundary of $M$ then $\text{Sk}(M)$ 
becomes a module over $\text{Sk}(S \times \mathbb{R})$.

---

TODO: a cute, anachronistic, reason -- arithmetic/geometric intersection 
numbers of curves

TODO: lagrange multipliers? This is in your zotero somewhere...
maybe from a pascaleff talk?

TODO: the big one -- mirror symmetry

TODO: emphasize you're **not** an expert in fukaya categories

Next up, let's look at fukaya categories. 
The right way to tell this story is for general 
[Symplectic Manifolds][9], but I'm going to focus on punctured 
surfaces because I understand them much better and in 
this setting a lot of things simplify _dramatically_[^2].

Given a punctured surface $S$, the <span class=defn>Fukaya Category</span>
is a (stable $\infty$-)category whose objects are curves in $S$, and 
$\text{Hom}(\alpha, \beta)$ is a chain complex spanned by the intersection 
points of $\alpha$ and $\beta$.

<div class=boxed markdown=1>
TODO: a picture
</div>

In this picture, we see $\text{Hom}(\alpha,\beta)$ is the chain complex 

TODO: compute it 

In this post, I'm not going to tell you how to figure out the degrees and 
the differential, but trust that it's really not _that_ hard[^3]! Instead, 
I'll say a *lot* about this in a [sister post][13] which is coming out 
at the same time as this one.

I'm also not _really_ going to tell you how to "compose" two intersection 
points in this post. But the rough idea is that you sum over all triangles 
containing the two intersection points you have.

TODO: For instance, in this picture, 
$p \circ q$ is.... well, whatever it is, lol.

<div class=boxed markdown=1>
TODO: draw a picture, ideally where you have two triangles.
</div>

The fukaya category is a complicated and subtle invariant, and it's not 
obvious why you might care about it. One extremely interesting reason 
to care is [mirror symmetry][11], but I want to give a slightly 
anachronistic reason which I think is fairly down-to-earth.

TODO: write up a bunch of stuff about categorified intersection numbers...
Maybe you can copy this from an old draft? That would be convenient.

---

Given a category $\mathcal{C}$ with a notion of "exact sequence", we can
build its <span class=defn>Hall Algebra</span> as the vector space having
(isomorphism classes of) objects of $\mathcal{C}$ as a basis, where the 
product of objects $X$ and $Y$ is, roughly, the sum over all extensions $E$ 
fitting into an exact sequence $0 \to X \to E \to Y \to 0$. Of course, 
to really make sense of this we'll need there to be only finitely many 
extensions between any pair $X$ and $Y$!

This allows us to encode interesting *enumerative* information about 
$\mathcal{C}$ in this algebra, so that we can compute, say, the number 
of iterated extensions of $X$, $Y$, $Z$, and $W$ by just computing the 
product $XYZW$ in the algebra and reading off the coefficients. In this 
way, the hall algebra acts kind of like a souped up generating function.

For example, let's take $\mathcal{C} = \mathsf{Vect}(\mathbb{F}_q)$. Then 
our algebra is generated by $\mathbb{F}_q^k$ for each natural number $k$, 
and moreover we compute the coefficient of $[ \mathbb{F}_q^n ]$ 
in $[\mathbb{F}_q^k] [\mathbb{F}_q^\ell]$ is the number of exact sequences
$0 \to \mathbb{F}_q^k \to \mathbb{F}_q^n \to \mathbb{F}_q^\ell \to 0$.
This only happens if $n = k + \ell$, and in that case there's one exact 
sequence for every $k$ dimensional subspace of $\mathbb{F}_q^n$. Said
another way, we compute

$$
[\mathbb{F}_q^k] [\mathbb{F}_q^\ell] = 
|\text{Gr}(k,k+\ell; \mathbb{F}_q)| \ [\mathbb{F}_q^{k + \ell}] =
\binom{k+\ell}{k}_q [\mathbb{F}_q^{k+\ell}]
$$

where $\binom{k+\ell}{k}_q$ is the [$q$-binomial coefficient][15].

Now if we want to count the number iterated extensions of 
$\mathbb{F}_q^a$ by $\mathbb{F}_q^b$ by $\mathbb{F}_q^c$ -- 
that is if we want to count [partial flags][14] on $\mathbb{F}_q^{a+b+c}$ 
of the shape

$$
\mathbb{F}_q^a \subseteq 
\mathbb{F}_q^{a+b} \subseteq
\mathbb{F}_q^{a+b+c}
$$

then all we have to do is compute the product 

$$
[\mathbb{F}_q^a] [\mathbb{F}_q^b] [\mathbb{F}_q^c] =
\binom{a+b}{a}_q [\mathbb{F}_q^{a+b}] [\mathbb{F}_q^c] =
\binom{a+b}{a}_q \binom{a+b+c}{a+b}_q [\mathbb{F}_q^{a+b+c}]
$$

Writing our $q$-binomial ceofficient in terms of $q$-factorials and 
simplifying, this says the number of flags of this shape is 
$\frac{[a+b+c]_q!}{[a]_q! [b]_q! [c]_q!}$, which we recognize as the 
$q$-multinomial coefficient $\binom{a+b+c}{a,b,c}_q$. 
So we've successfully re-proven the fact that 
the $q$-multinomial counts partial flags of a certain shape. 
See [here][16], for example.

TODO: Toen accent

Toen extended this definition to work for stable $\infty$-categories. The 
precise details are a bit technical, but the idea is exactly the same.

In particular, we can take the hall algebra of $\text{Fuk}(S)$. This 
gives us an algebra whose elements are curves in $S$... But this sounds a 
lot like the skein algebra! It's natural to wonder if there's a relationship 
between these, and this brings me to an _extremely_ compelling fact:

Consider a disk with four punctures:

<div class=boxed markdown=1>
TODO: a picture
</div>

Then one can compute the following equation in $\text{Hall}(\text{Fuk}(D_4))$:

<div class=boxed markdown=1>
TODO: a picture of the skein relation, drawn out
</div>

I started this blog post because I finally understand all of these objects 
well enough to compute this relation for myself! I did it for the first 
time over the past few days, and I'm really excited to show how to do it!

Unfortunately, it requires a lot of background, and when I thought about 
how to structure a blog post where I prove it... I realized it probably 
needs to be a few blog posts, haha. So this post exists in order 
to motivate this computation that I'll be building to over the next 
few posts!

My rough plan is to have a post really diving into the hall algebra 
details next. There's a nice blend of high-brow and low-brow ideas here, 
and I'm excited to dig into it. After that I'll write a post going 
into fukaya categories of surfaces, and how to compute with them. I'm 
really excited about that because I think it has a chance to be really 
helpful for other people learning about fukaya categories. Lastly, 
I'll put the pieces together and check the skein relation holds in 
$\text{Hall}(\text{Fuk}(S))$!

Lots to do, so we'll talk _really_ soon! Take care all ^_^.

---

[1]: skein algebra
[2]: quantum algebra
[3]: fukaya category
[4]: hall algebra
[5]: fabian's website
[6]: jones polynomial
[7]: E_1 algebra
[8]: Eckmann Hilton
[9]: symplectic geometry
[10]: https://www.youtube.com/watch?v=Au5Uzfk-GU8
[11]: mirror symmetry
[12]: quantum group
[13]: sister post on computing in fukaya categories
[14]: https://en.wikipedia.org/wiki/Generalized_flag_variety
[15]: https://en.wikipedia.org/wiki/Gaussian_binomial_coefficient
[16]: https://golem.ph.utexas.edu/category/2007/10/geometric_representation_theor_1.html


[^1]:
    It's not obvious that this is well defined, since the procedure seemingly
    depends on both the order you resolve crossings and (more seriously) 
    on how you chose to draw your link. Thankfully no matter the order you 
    do things in or what link diagram you choose, you'll always get the same 
    polynomial at the end of the day!

[^2]:
    These two things are related.

[^3]:
    Although thinking that it's not that hard is a fairly new development 
    for me, haha. I think this is because I didn't see a ton of example 
    computations, though, and I had to figure a lot of it out myself. 
    Hopefully with me showing you what to do, it really will come off as 
    doable, even to a newcomer.

    If you just can't wait for the post where I talk about this, you should 
    absolutely watch Claire Amiot's _fantastic_ [lecture series][10] on 
    this stuff. It came out a few months ago, and I _really_ wish it had 
    existed when I was trying to figure out how to do these computations, haha.

[^4]:
    There's a fascinating story here allowing us to build skein modules 
    attached to various [quantum groups][12], and it turns out the classical
    jones polynomial skein relations is attached to quantum $SL_2$. 
    See, for instance, TODO: find a reference.

