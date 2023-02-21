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

Let's see what this means, show how to build the tensor product purely
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

But if I give you some functor to $\mathsf{Set}$, how can we _tell_ if it's
representable or not? After all, $\mathsf{BL}_{M,n}$ was representable,
but if you'd never heard of a tensor product before it would probably be 
hard to make a guess! 

<div class=boxed markdown=1>
Here's a cute example.
Is the functor $\mathsf{E}_M : \mathsf{Vect}^\text{op} \to \mathsf{Set}$
representable, where

$$
\mathsf{E}_{M,N}(X) = \{ \text{linear maps } f : M \oplus X \to N \}
$$

Notice this is a _contravariant_ functor, so a representing object would
be some vector space $Y$ with

$$
\mathsf{E}_{M,N}(-) \cong \mathsf{Vect}(-,Y)
$$
</div>

<!-- No. Such an object Y would be the exponential N^M, but Vect is not cartesian closed -->

We can answer this question more broadly using the 
<span class=defn>Adjoint Functor Theorems</span>


[1]: https://en.wikipedia.org/wiki/Universal_property
[2]: https://ncatlab.org/nlab/show/adjoint+functor+theorem
[3]: https://en.wikipedia.org/wiki/Moduli_space
[4]: https://en.wikipedia.org/wiki/Representable_functor
[5]: https://en.wikipedia.org/wiki/Stack_(mathematics)
[6]: https://sites.math.washington.edu/~jarod/moduli.pdf
[7]: https://en.wikipedia.org/wiki/Tensor_product
