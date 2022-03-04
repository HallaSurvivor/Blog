---
layout: post
title: Why is the Completion of a Local Ring "More Local" than just Localizing?
tags:
  - 
---

An oft-repeated piece of intuition I've seen while trying to learn algebraic
geometry is that localizing a ring at a prime is like "zooming in" on that 
point. But if you want to zoom in "really close" then you have to take the
[completion][1] of this ring... Why is that?

This is definitely an observation well known to experts 
(and even many nonexperts, probably), but I know I would have liked to
have seen it spelled out explicitly, so here we are. I also would have
realized it sooner if I'd read Hartshorne sooner, since he gives this exact
observation in chapter $I.5$, in the section on completion[^1]. 

The idea, in hindsight, is obvious:

<div class=boxed markdown=1>
Open subsets in the Zariski topology are dense!

So knowing what happens in some neighborhood means knowing what happens
almost everywhere!
</div>

Let $R$ be a ring, and consider $X = \text{Spec}(R)$.

Then the ring of regular functions on $X$ is exactly $R$, where we think of
$f(\mathfrak{p}) \triangleq f / \mathfrak{p}$. In particular, 
$f(\mathfrak{p}) = 0$ if and only if $f \in \mathfrak{p}$.
Notice the codomain of $f$ might vary with its input 
(so $f$ is like an element of a [dependent product][2]).

Now, what does it mean to "zoom in" on a point $\mathfrak{p}$ in $X$?

Well, one obvious idea is to look at functions defined on smaller and smaller
open sets containing $\mathfrak{p}$. This is formalized by the idea of 
[germs][3], and a fairly easy computation shows that the ring of germs at 
$\mathfrak{p}$ is exactly the localization $R_\mathfrak{p}$. Indeed, that's
where the name comes from. This also makes some intuitive sense, since
(for integral domains) 

$$
R_\mathfrak{p} = \left \{ \frac{f}{g} \ \middle | \ g(\mathfrak{p}) \neq 0 \right \}
$$

but if $g(\mathfrak{p}) \neq 0$, then (by continuity) there's a 
_neighborhood_ of $\mathfrak{p}$ where $g$ doesn't vanish. So near 
$\mathfrak{p}$, $g$ looks invertible!

This sounds like a great definition of "local", so what's the problem?
Well, remember the boxed statement! Zariski open sets are _dense_,
and thus remember information from "most of" $X$!

Here is one striking example:

Let $X$ and $Y$ be varieties over an (algebraically closed) field $k$.

Say the local rings of $\mathfrak{p} \in X$ and $\mathfrak{q} \in Y$ are
isomorphic (as $k$-algebras). Then (exercise $I.4.7$ in Hartshorne) 
$\mathfrak{p}$ and $\mathfrak{q}$ have neighborhoods $U \subseteq X$ and 
$V \subseteq Y$ so that $U$ and $V$ are isomorphic as varieties.

This doesn't sound too bad until you remember that $U$ is dense in $X$ 
and $V$ is dense in $Y$. So already $X$ and $Y$ have to be 
[birationally equivalent][4]!

So even though we only knew that $\mathfrak{p}$ and $\mathfrak{q}$ had
isomorphic neighborhoods, we were able to lift this to a (coarse) 
equivalence of the whole of $X$ and $Y$!

---

Now, most of my geometric intuition comes from manifolds, and in that setting
this would be extremely strange! After all, manifolds are locally euclidean,
so if $X$ and $Y$ have the same dimension, then _every_ point of $X$ and
_every_ point have $Y$ have isomorphic neighborhoods!

See, for instance, this picture I stole from the nlab[^2]:

<p style="text-align:center;">
<img src="/assets/images/locality-in-alg-geom/Chart.png" width="50%">
</p>

Every point on this surface has a neighborhood homeomorphic to an open disk,
and the same is true of every other point of every other $2D$ manifold!

Intuitively, then we want to say that locally, every point of every 
variety "looks the same" as every other point, as long as the two varieties
have the same dimension. We can't get this behavior with just open sets in
the case of varieties because there simply aren't enough open sets to 
"get close enough" to a point.

But now let's look at the completion.

The [Cohen Structure Theorem][5] says that any two complete regular local
rings containing the same field $k$ of the same dimension are isomorphic.
In fact, every such ring is isomorphic to $k[\\![ x_1, \ldots, x_n ] \\!]$.

So _now_ if $X$ and $Y$ are varieties of the same dimension, and 
$\mathfrak{p}$ and $\mathfrak{q}$ are (regular) points, then even if
the _local_ rings $$k[X]_\mathfrak{p}$$ and $$k[Y]_\mathfrak{q}$$ might not
be isomorphic the _complete_ local rings $$\widehat{k[X]_\mathfrak{p}}$$
and $$\widehat{k[Y]_\mathfrak{q}}$$ _will_ be! 

This is the analogue in algebraic geometry of the fact that any two points
of manifolds of the same dimension must have homeomorphic neighborhoods!

As a last aside, notice we had to squeeze in the word 
<span class=defn>regular</span> earlier. What does that mean?

Well manifolds have to be smooth _everywhere_, whereas varieties are allowed
to have a small set of [singular points][6]. Broadly speaking, these are points
where the tangent space has the wrong dimension. When a point _isn't_ singular,
we call it regular, and the set of regular points is open and dense, so it's
most of the variety.

Since we expect the tangent space of a point to "look like" some small 
neighborhood of that point, it makes sense that "zooming in" too close to 
a singular point might make it look unlike the rest of the regular points
on the variety, and indeed that's the case.

At this point I encourage everyone to go look at example $I.5.6.3$ in 
Hartshorne. I _could_ transcribe it here for convenience, but I wanted this
to be a lower effort post, so... I won't :P.

I have some higher effort posts in the pipeline, but for now, it's time for bed.

Stay warm, all! See you soon ^_^

---

[^1]:
    I was scared of Hartshorne for a long time, and in hindsight I really 
    didn't need to be. I haven't read it cover to cover, but I'm at a place
    now where chapter $I$ on varieties all feels quite natural, and I'm 
    reading chapter $II$ on schemes right now. I'm skimming quite lightly,
    because I only have so much time, and I have other things I'm reading
    about too, but I'm really enjoying it so far.

    I've actually had this post idea in my todo list for a little while now,
    and when I saw the exact observation spelled out in Hartshorne, it 
    was the last push I needed to actually get to it. Of course that push was
    a few weeks ago now, but it takes time to actually get around to writing
    these posts, haha.

[^2]:
    This image actually has some ~bonus information~ about transition maps,
    which muddles the picture somewhat, but that's what I get for using 
    someone else's diagram



[1]: https://en.wikipedia.org/wiki/Completion_of_a_ring
[2]: https://en.wikipedia.org/wiki/Dependent_type#%CE%A0_type
[3]: https://en.wikipedia.org/wiki/Germ_(mathematics)
[4]: https://en.wikipedia.org/wiki/Birational_geometry
[5]: https://en.wikipedia.org/wiki/Cohen_structure_theorem
[6]: https://en.wikipedia.org/wiki/Singular_point_of_an_algebraic_variety
