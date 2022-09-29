---
layout: post
title: 
tags:
  - 
---

In a first category theory course, a lot of emphasis is placed on 
[representability][1], but (at least when I was first learning) there might 
not be much justification for this. After all, representable functors have
some nice properties, but how can we recognize them in the wild? Similarly,
a lot of emphasis is placed on the [yoneda lemma][2], without a ton of 
example use cases. In this post, I'd like to fill both of those holes by 
outlining an extremely common mode of argument that lets us show the existence
of convenient objects (which we should view as [moduli spaces][3] for a 
given funtor), which we can _study_ using yoneda!

Hopefully this post will be pretty short. I have two longer form posts 
in the works -- 
 - one about topos theory, and how to solve real problems with it
 - one about what categories "are". One of the difficult parts of 
    getting into the subject are the many subfields from which 
    category theorists draw inspiration. We flexibly shift between
    viewing categories as universes to geometric objects to algebraic
    objects to logical objects and the terminology reflects this. 
    Hopefully in this post I'll be able to demystify some of the more
    nuanced ways a working category theorist might think of a category.
 - I also have a super-secret special project that I don't want to say more
    about in case it never sees the light of day. But it's taking up a fair
    amount of the expositional energy that I usually put into this blog.

Even though I have some big stuff coming, I still wanted to put something up,
and this idea struck me while I was rereading Emily Riehl's (excellent)
_Category Theory in Context_ while visiting some friends in New York. 
I think it'll be a nice and easy post, which people might still find useful!

Let's get to it ^_^

---

First things first, what's a "moduli space" anyways? The idea 
(as far as I know) has its origins in algebraic geometry, where 
a given family of related geometric objects itself assembles into 
a geometric object!

For instance, we can look at the family of lines through the origin
in $\mathbb{R}^{n+1}$. This is a family of related objects, and 
there's a space ($\mathbb{R}P^n$) whose _points_ are exactly these lines.

In the even special-er case of $\mathbb{R}P^1$, we're parametrizing 
lines through the origin in $\mathbb{R}^2$, but these are determined by
their slope! 

TODO: flesh this out, mention that we can have an "oriented line", 
given by a point in $S^1$, and then we quotient by the orientation.
This is typical for moduli spaces.

This idea is quite prevalent because it's _extremely_ useful! It turns out
that by studying the moduli space of some family of objects, we can study
the entire family at once! Moreover, since the moduli space is itself a 
geometric object, we can use all of our favorite preexisting geometric tools 
in order to study it!

For instance, say we want to continuously assign a line to each point 
of a space $M$. TODO: say something about line bundles.

In this way, we see that maps $M \to \mathbb{R}P^1$ are in bijection with
globally generated line bundles on $M$. Said another way, we get an
isomorphism

$$
\text{Hom}(M,\mathbb{R}P^1) \cong \{ \text{globally generated line bundles on $M$} \}
$$

natural in $M$.

So a moduli space is "just" a representable functor!

---

At this point, we can see lots of objects throughout math have this kind 
of flavor to them.

TODO: just a slew of examples, in various fields, of representable functors
(using kind of moduli theoretic language)

---

Now say you have a construction you want to understand. For instance, 
bilinear maps. These show up naturally in linear algebra, but are 
kind of tricky to understand (since all of our linear algebraic machinery
is about studying _linear_ maps). 

Inspired by moduli spaces, we might try to find a vector space 
(which I'll suggestively call $V \otimes W$) so that 
linear maps $V \otimes W \to X$ are in bijection with _bilinear_ maps 
$V \times W \to X$. In fancier language, we want to find an object 
$V \otimes W$ _representing_ the functor 

$$X \mapsto \{ \text{bilinear maps $V \times W \to X$} \}$$

since then we can study this $V \otimes W$ with our existing linear 
algebraic toolkit in order to extend it to work on bilinear maps!

This brings us to a crucial idea that is omitted from most first 
category theory courses:

<div class=boxed markdown=1>
  If $F : \mathcal{C} \to \mathsf{Set}$ is representable, then 
  $F$ preserves limits.

  Conversely, if $F : \mathcal{C} \to \mathsf{Set}$ preserves limits,
  then it is (usually) representable!
</div>

This is more-or-less the [adjoint functor theorem][4]. Indeed, if we can 
show that $F$ has a left adjoint $L \dashv F$ then we'll know that

$$
\text{Hom}_\mathcal{C}(L1, X) \cong \text{Hom}_\mathsf{Set}(1, FX) \cong FX
$$

so that $L1$ represents $F$!

The exact conditions on the adjoint functor theorem aren't super important.
What matters is that the conditions are often satisfied in categories
arising in practice[^1], so that the important requirement is the continuity of $F$.

---

In particular, for any category of $R$-modules, a continuous functor is 
automatically representable. So then let's look at our functor of interest

$$
F : X \mapsto \{ \text{bilinear maps $V \times W \to X$} \}
$$

We want to show it's continuous in the sense that 

$$
F \left ( \lim X_i \right ) \cong \lim F X_i
$$

TODO: write this up

---

This same mode of argument works in more complicated settings as well!
For instance, say we want to build the [Hilbert Scheme][6], 
$\text{Hilb}(X)$ whose points are (flat) subschemes of a scheme. 
This turns out to be quite complicated, but one important idea is to 
identify schemes with certain functors on $\mathsf{Ring}^\text{op}$. 
Then we can build the hilbert scheme by showing it's a sheaf on this
site, which can be covered by affine sheaves. See Chapter 1 of Jarod 
Alper's notes [here][7], for instance.

In some sense, this "functor of points" approach is to work directly with
functors, so that _every_ functor[^2] is trivially representable. The 
hard part is showing when such a functor actually comes from a _scheme_,
and we check this... TODO: What am I even saying here?

---

A post about how we can define an object as a kind of moduli space for a functor.

Go through, in detail, how to build the tensor product of two vector spaces 
using nothing but category theory (build the functor, show it preserves limits,
thus it's representable by (basically) the adjoint functor theorem... check 
Riehl's book for the precise statement)

The good news is that this method works in much more general contexts.
(For instance, link Alper's notes and say this is how we define the 
hilbert scheme)
The bad news is that it doesn't tell you anything about what your object 
looks like.

Of course, there are ways around this. Yoneda tells us that we, in theory,
perfectly understand an object once we understand the maps into (resp. out of)
it. And of course, since we _defined_ our object as the thing classifying
some functor, understanding these maps amounts to understanding that functor.

Mention that, in some sense, category theory lets you view everything as 
a moduli space of the functor it represents

---

[^1]:
    Though you _do_ have to be careful! Particularly when using the _Special_
    Adjoint Functor Theorem.

    While many categories have a small cogenerating set 
    (for instance, any category of $R$-modules. See [here][5]), 
    the category of Groups _doesn't_! 

    The SAFT is nice when we have it, but frequently we have to go back to the
    General Adjoint Functor Theorem to get the job done.

[^2]:
    This isn't strictly true -- we restrict attention to the "nice" functors,
    namely the sheaves on this site.

[1]: representable functor
[2]: yoneda lemma
[3]: moduli space
[4]: adjoint functor theorem
[5]: https://mathoverflow.net/questions/85331/on-a-special-case-of-the-adjoint-functor-theorem
[6]: hilbert scheme
[7]: https://sites.math.washington.edu/~jarod/moduli.pdf
