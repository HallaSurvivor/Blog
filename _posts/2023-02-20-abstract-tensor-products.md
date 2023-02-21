---
layout: post
title: Building Objects with Category Theory
tags:
  - 
---

Typically category theory is useful for showing the _uniqueness_
of certain objects by checking that they satisfy some 
[universal property][1]. This makes them unique up to unique isomorphism.
However, category theory can _also_ be used in order to show that objects
exist _at all_, usually with the help of the [Adjoint Functor Theorems][2].

The plan is to build a functor which does something useful. Then we'll show 
that the functor is [representable][4]. In particular, there's an object
$X$ representing the functor, and we'll have shown the existence of $X$
purely abstractly!

This is a very common mode of argument nowadays in algebraic geometry. 
You want to build a [moduli space][3] for some family of objects, but it
can be tricky to build it explicitly. Since it's a moduli space, though,
we _know_ what its "functor of points" should be. So if we can show 
its functor of points is representable, we'll be in business! This is
one reason to pass to the category of [stacks][5], since oftentimes 
a moduli functor is representable as a stack but is _not_ representable
by a scheme. For more information, see Alper's excellent notes on 
[Stacks and Moduli][6].

The algebro-geometric examples are quite intricate, but we can already
find a small example in [tensor products][7]. After all, we know the 
tensor product $M \otimes N$ is supposed to represent bilinear maps from
$M$ and $N$! 

Let's see what this means, sketch how to build the tensor product purely
abstractly, and then talk about the benefits and shortcomings of this approach.

---

First, what do we mean when we say the tensor product "represents"
bilinear maps? The answer is summed up in the 
_universal property of the tensor product_:

<div class=boxed markdown=1>
Linear maps $M \otimes N \to X$ are in (natural) bijection 
with bilinear maps $M \times N \to X$.

Moreover, there is a _universal_ bilinear map $M \times N \to M \otimes N$
which corresponds to the identity map under this bijection.
</div>

This universal property, like all universal properties,
pins down $M \otimes N$ up to unique isomorphism _if it exists_. 
But it (crucially) doesn't tell us whether $M \otimes N$ really _does_ exist!
Maybe there's no such object. 

In the language of representable functors, we consider the functor 
$\mathsf{BL}_{M,N} : \mathsf{Vect} \to \mathsf{Set}$ so that

$$
\mathsf{BL}_{M,N}(X) = \{ \text{bilinear maps } f : M \times N \to X \}
$$

Then the universal property says that there's a bijection (natural in $X$)

$$
\mathsf{Vect}(M \otimes N, X) \cong \mathsf{BL}_{M,N}(X)
$$

so that $M \otimes N$ <span class=defn>represents</span> $\mathsf{BL}_{M,N}$.

---

So the question, generally, is this:
If I give you some functor to $\mathsf{Set}$, how can we _tell_ if it's
representable or not? We know from experience that $\mathsf{BL}_{M,N}$ is 
representable, but if you'd never heard of a tensor product before it would 
probably be hard to make a guess! 

<div class=boxed markdown=1>
Here's a cute example.
Is the functor $\mathsf{E}_M : \mathsf{Vect}^\text{op} \to \mathsf{Set}$
representable, where

$$
\mathsf{E}_{M,N}(X) = \{ \text{linear maps } f : M \oplus X \to N \}?
$$

Notice this is a _contravariant_ functor, so a representing object would
be some vector space $Y$ with

$$
\mathsf{E}_{M,N}(-) \cong \mathsf{Vect}(-,Y)
$$
</div>

<!-- No. Such an object Y would be the exponential N^M, but Vect is not cartesian closed -->

We can answer this general question using the 
<span class=defn>Adjoint Functor Theorems</span>. 
While this is _presented_ in a lot of category theory
classes, I think it's often left mysterious how and 
why to use it. Well here's a prime example of the adjoint functor theorem in action:

<div class=boxed markdown=1>
Theorem: Every representable functor preserves limits.

Theorem: If $\mathcal{C}$ is "nice", then every limit-preserving functor is 
representable!
</div>

The key to proving this (and to figuring out what "nice" means) lies in 
the adjoint functor theorems. There are a whole bunch of adjoint functor
theorems, each of which is impossible to remember in its own special way. For instance:

<div class=boxed markdown=1>
<span class=defn>General Adjoint Functor Theorem</span>

If $F : \mathcal{C} \to \mathcal{D}$ is a functor which preserves limits,
then $F$ admits a left adjoint provided the following conditions are met:

1. $\mathcal{C}$ is complete and locally small
2. For each $d \in \mathcal{D}$ there's a set $\{c_i\}$ of objects in $\mathcal{C}$
    and arrows $f_i : d \to F c_i$ so that every arrow $g : d \to F x$ factors as 
    $$d \overset{f_i}{\to} Fc_i \overset{Ft}{\to} Fx$$
    for some arrow $t : c_i \to x$.
</div>

Condition (2) above is usually called the [solution set condition][8].

Thankfully, in many nice settings we don't have to remember this condition!
Here are two easy to remmeber settings where adjoint functors always exist:

<div class=boxed markdown=1>
 - Any colimit preserving functor between grothendieck topoi is a left adjoint
 - Any limit preserving functor between grothendieck topoi is a right adjoint
</div>

<div class=boxed markdown=1>
 - Any colimit preserving functor between "essentially algebraic" categories[^1]
     is a left adjoint
 - Any limit preserving functor that _also preserves filtered colimits_ 
      between essentially algebraic categories is a right adjoint
</div>

This is great and all, but what do adjoint functors have to do with representables? Here's the key,
which for some reason wasn't taught to me in any classes I took:

<div class=boxed markdown=1>
If $F : \mathcal{C} \to \mathsf{Set}$ has a left adjoint $L$, then $F$ is representable
</div>

$\ulcorner$
We claim $$L \{ \star \}$$ works. Indeed, 
$$\mathcal{C}(L \{ \star \}, X) \cong \mathsf{Set}(\{ \star \}, FX) \cong FX$$,
naturally in $X$.

<span style="float:right">$\lrcorner$</span>

In fact, this is typically the _only_ way for $F$ to be representable:

<div class=boxed markdown=1>
Exercise 4.6.iii in Emily Riehl's _Category Theory in Context_:

Suppose $\mathcal{C}$ is a locally small category with coproducts. Show
$F : \mathcal{C} \to \mathsf{Set}$ is representable if and only if it admits
a left adjoint
</div>

---

Ok, so now we have a strategy! To prove (purely abstractly) that tensor 
products exist, we'll show that $$\mathsf{BL}_{M,N} : \mathsf{Vect} \to \mathsf{Set}$$
has a left adjoint. Since $\mathsf{Vect}$ and $\mathsf{Set}$ are both 
essentially algebraic (indeed they're both _algebraic_), we just need to show 
that it preserves limits and filtered colimits.

Thankfully, neither of these is too hard to check! Here's a sketch, which can
be turned into a real proof by someone who doesn't want to go to sleep soon[^2] :P.
They key insight is that for an arrow $f : X \to Y$, $\mathsf{BL}_{M,N}(f)$
is extremely simple: just compose your bilinear map $M \times N \to X$ 
with $f$! This, paired with the fact that everything here plays nicely with
the forgetful functor to $\mathsf{Set}$ makes the computations fairly painless.

$\ulcorner$
We start by showing that $\mathsf{BL}_{M,N}$ preserves limits,
and we can do this by checking that it preserves products and equalizers.

First, it's easy to see that a bilinear map into $\prod X_\alpha$
is the same thing as a family of bilinear maps into each $X_\alpha$.
Next, we need to show that $$\mathsf{BL}_{M,N}$$ preserves equalizers. 
So if $f_\alpha : X \to Y$ is a family of maps, we'll consider the equalizer

$$E = \{ x \in X \mid \forall \alpha, \beta . f_\alpha x = f_\beta x \}$$

Now $$\mathsf{BL}_{M,N}(E)$$ is the set of bilinear maps $M \times N \to E$.
We would like this to agree with the equalizer in $\mathsf{Set}$ of the
$$\mathsf{BL}_{M,N}(f_\alpha) : \mathsf{BL}_{M,N}(X) \to \mathsf{BL}_{M,N}(Y)$$.
That is, with the set of bilinear maps $g : M \times N \to X$ so that all of
the $$f_\alpha \circ g$$ are equal. But if all the $$f_\alpha \circ g$$ are equal,
then $g$ lands in the equalizer of the $$f_\alpha$$ (computed in $\mathsf{Set}$)
which is the underlying set of $E$!

So $\mathsf{BL}_{M,N}$ preserves limits. Let's move onto filtered colimits.

Say $\mathcal{D}$ is a filtered category and $X_{(-)}$ is a functor sending 
each object $i$ of $\mathcal{D}$ to a vector space $X_i$. Then we want to show that 
bilinear maps $M \times N$ into the colimit of the $X_i$ agrees with the 
colimit of the sets of bilinear maps.

But what is $\varinjlim X_i$? It's the disjoint union of the $X_i$, where we
glue together the points $x_i$ and $f x_i$ for each arrow $f$ in the diagram.
What makes this diagram filtered is that any two arrows are eventually 
merged. So if we have a bilinear map $M \times N \to \varinjlim X_i$, we're 
choosing some equivalence class $[x_i]$ for each $(m,n)$ pair. 

But if we have a family of sets of bilinear maps $M \times N \to X_i$, 
their colimit is the disjoint union of these sets, where we glue together any 
maps that are eventually merged. So we are left with equivalence classes
$[f_i]$ of maps landing in $X_i$.

Now it's not hard to see that the function sending $[f_i]$ to the 
$\varinjlim X_i$-valued bilinear map $(m,n) \mapsto [f_i(m,n)]$ is 
well defined, and really _does_ output a valid equivalence class. It's 
also not hard to see that, given some bilinear map 
$f : M \times N \to \varinjlim X_i$, we can get a family of maps $f_i$
by letting $f_i(m,n)$ be the element of $X_i$ in the equivalence class of
$[x_i] = f(m,n)$. Checking that these maps are well defined is where we 
crucially use filteredness of $\mathcal{D}$. 

Then we check these maps are inverse to each other, so that $\mathsf{BL}_{M,N}$
preserves filtered colimits.
<span style="float:right">$\lrcorner$</span>

So $$\mathsf{BL}_{M,N}$$ is representable! Call the representing object 
$M \otimes N$, and we're done ^_^.

---

Now I would argue that the above construction of the tensor product 
is worse than the explicit definition (by generators and relations)
we typically see in an algebra class. It's very high powered, and 
gives very little insight into how to make computations with $M \otimes N$.

This, more generally, is the downside to showing the existence of objects
in this way. We have very little control over what the resulting object
looks like. We only know how to probe it by maps to other objects[^3].
The yoneda lemma tells us that this is enough to fully 
understand the object we've built, and it's often good enough in the 
abstract, but sometimes you need to get your hands dirty and compute.

The big _benefit_ to working this way is that it really doesn't get _much_
harder than this. Yes this was a superpowered proof of the existence of
tensor products. But this proof doesn't get any more complicated no matter
_what_ we want to exist! If we want to build something particularly 
complicated, then frequently this method (or one like it, tailored to the
category of interest) will be easier than having to construct the relevant 
object by hand.

---

Anyways, that's going to do it for today's post! I have like 4 or 5 posts
all most of the way done, and I want to start wrapping them up soon,
so hopefully there will be more Content™ for all of you in the near future ^_^.

As a quick story for how addled my brain is, though, I went to mark this post
off my todo list of blog post ideas[^4], and I couldn't find it on the todo list...
I knew I'd thought about making this post before, so it was weird it wasn't there.

It turns out that I never bothered putting it in the todo list, because I 
had _started writing_ a version of this post in September of last year! 
I actually remember doing that, because I had this realization about the
link between the adjoint functor theorems and representability[^5]
while (re)reading Emily Riehl's _Category Theory in Context_ on a trip to 
New York. That became the impetus for this entire post, since it makes for
a good excuse to clarify the adjoint functor theorems. 

In fact, that old draft is still in my git history, and I looked through it
after finishing the post, but before writing this epilogue. It's 
structurally pretty similar to this one, but longer[^7], and with more examples
of moduli spaces in geometry. That's not _so_ surprising, since only a few 
months prior I had been doing a reading course on stacks and moduli spaces
with [Patricio Gallardo Candela][10]. There's part of me that wants to 
move some of those examples here (for instance, projective space as a
moduli space of lines through the origin), but a bigger part of me that
wants to go to sleep, haha.
I'm sure I'll have plenty of time to talk about moduli spaces in some 
other post! 

Thanks as always for reading. Stay warm, and we'll chat soon[^6] ^_^.


---

[^1]:
    More generally, [locally presentable][9] categories. It turns out that
    models of an essentially algebraic theory form particularly nice 
    locally presentable categories, namely the "locally _finitely_ presentable"
    ones.

    In particular, this includes your categories of groups, rings, modules, etc.

[^2]:
    I was actually working on a _different_ blog post earlier today about
    2-categories and why you should care (which is almost done), but I got 
    distracted and decided to work on this instead, haha.
    So I _really_ want this to be a one-night kind of blog post.

[^3]:
    Though the examples that show up geometrically are usually contravariant,
    so we probe them with maps _from_ other objects.

[^4]:
    Which, at time of writing, has 209 items...

[^5]:
    Which again, nobody taught me for some reason!

[^6]:
    I'm _slowly_ finalizing all these posts that are mostly done, after all!

[^7]:
    It's also notably _unfinished_ :P.

[1]: https://en.wikipedia.org/wiki/Universal_property
[2]: https://ncatlab.org/nlab/show/adjoint+functor+theorem
[3]: https://en.wikipedia.org/wiki/Moduli_space
[4]: https://en.wikipedia.org/wiki/Representable_functor
[5]: https://en.wikipedia.org/wiki/Stack_(mathematics)
[6]: https://sites.math.washington.edu/~jarod/moduli.pdf
[7]: https://en.wikipedia.org/wiki/Tensor_product
[8]: https://ncatlab.org/nlab/show/solution+set+condition
[9]: https://ncatlab.org/nlab/show/locally+presentable+category
[10]: https://sites.google.com/site/patriciogallardomath/
