---
layout: post
title: An Explicit Example of the Proof of the Nullstellensatz
tags:
  - sage
---

I'm in an algebraic geometry class right now, and a friend was struggling 
conceptually with the proof of the strong nullstellensatz. I thought it might be 
helpful to see a concrete example of the idea, since the proof is actually quite 
constructive! Which brings us to this post:

Formally, we're going to assume the weak nullstellensatz, and use it to show
the strong nullstellensatz. That is, we'll assume 

<div class=boxed markdown=1>
  <span class=defn>The Weak Nullstellensatz</span>

  $V(\mathfrak{a}) = \emptyset$ if and only if $\mathfrak{a} = (1)$

  Purely algebraically, this says:

  "The only way $f_1, f_2, \ldots, f_r$ can fail to have a common zero is if
  $(f_1, f_2, f_3, \ldots, f_r) = (1)$."
</div>

and we'll show

<div class=boxed markdown=1>
  <span class=defn>The Strong Nullstellensatz</span>

  $I(V(\mathfrak{a})) = \sqrt{\mathfrak{a}}$

  Again, purely algebraically, this says:

  "The only way $g, f_1, f_2, \ldots, f_r$ can all be $0$ simultaneously is
  if (for some $n$) $g^n$ is a linear combination of the $f_i$."
</div>

Both of these are theorems of the form "the obvious issue is the only one". 
Obviously if 
$1 = p_1 f_1 + p_2 f_2 + \ldots + p_r f_r$, then the $f_i$ cannot all be $0$
simultanously. Indeed, if $$f_i(x^*) = 0$$ for all $i$, then evaluating both
sides of the above at $$x^*$$ gives $1 = 0$, which is a problem. The weak 
nullstellensatz says that this is the _only_ reason a family of polynomials
won't have a common root.

Similarly, it's obvious that if $g^n = p_1 f_1 + \ldots + p_r f_r$, then
at any common zero of the $f_i$, $g = 0$ too. Again, if we evaluate both
sides at $x^*$ we find $$g(x^*)^n = 0$$, and so $$g(x^*) = 0$$ too 
(since a field has no nontrivial nilpotents). The strong nullstellensatz says
that this is the _only_ way for $g$ to share a zero with the $f_i$.

---

Now, it turns out the weak nullstellensatz has computational content. That 
is, if $f_1, \ldots, f_r$ _don't_ have a common zero, there's a computer
program[^1] that will actually _find_ the $p_i$ so that 
$1 = p_1 f_1 + \ldots + p_r f_r$. 

For instance, let's take a simple example:

$$
f_1 = xy - 1 \quad \quad f_2 = x+y \quad \quad f_3 = xy^3 \quad \quad f_4 = yx^3
$$

First, let's check that these polynomials really don't have any points in common:

<div class="auto">
<script type="text/x-sage">
# make a polynomial ring with generators x,y
# over QQbar, the algebraic closure of QQ.
R.<x,y> = QQbar[] 

f1, f2, f3, f4 = x*y - 1,  x+y,  x*y^3,  y*x^3

I = ideal(f1,f2,f3,f4)

I.variety() # should print out [], the empty set
</script>
</div>

Next we can see that they generate the ideal $(1)$. 

<div class="auto">
<script type="text/x-sage">
R.<x,y> = QQbar[] 
f1, f2, f3, f4 = x*y - 1,  x+y,  x*y^3,  y*x^3
I = ideal(f1,f2,f3,f4)

I == ideal(1)
</script>
</div>

Of course, this means we should be able to write $1$ as a linear combination
of the $f_i$:

<div class="auto">
<script type="text/x-sage">
R.<x,y> = QQbar[] 
f1, f2, f3, f4 = x*y - 1,  x+y,  x*y^3,  y*x^3
I = ideal(f1,f2,f3,f4)

R(1).lift(I) # prints [y^2 - 1, y, -1, 0]
</script>
</div>

and indeed, these are the coefficients to get $1$

<div class="auto">
<script type="text/x-sage">
R.<x,y> = QQbar[] 
f1, f2, f3, f4 = x*y - 1,  x+y,  x*y^3,  y*x^3

# should give 1
(y^2 - 1) * f1  +  y * f2  +  (-1) * f3  +  0 * f4 
</script>
</div>

---

So now what about the strong nullstellensatz?

Let's take $g = yx + x + 1$, which vanishes at 
every point of the variety defined by $x^2 + 2x + 1$ and $y$
(do you see why?).

Then we expect $g^n \in (x^2 + 2x + 1, y)$ for some $n$, and we'll
get there by the [Rabinowitsch trick][3]:

We'll add a variable $z$ to the mix, and notice that 
$x^2 + 2x + 1$, $y$, and $(yx + x + 1)z - 1$ don't have any
common zeroes. 

Indeed, if $x^2 + 2x + 1$ or $y$ is nonzero at some point, then we're done. 
But if they're both zero, then we know $g = yx + x + 1$ is zero as well. Then
$(yx + x + 1)z - 1 = gz - 1 = 0z - 1 = -1 \neq 0$.

But then, by the weak nullstellensatz, that means these three polynomials
must generate the ideal $(1)$ in $k[x,y,z]$! 

Indeed,

<div class="auto">
<script type="text/x-sage">
R.<x,y,z> = QQbar[]
f1, f2 = x^2 + 2*x + 1,  y
g = y*x + x + 1

p1,p2,p3 = var('p_1, p_2, p_3')

coeffs = R(1).lift(ideal(f1,f2,g*z-1))
show(p1 == coeffs[0])
show(p2 == coeffs[1])
show(p3 == coeffs[2])
</script>
</div>

So we know that

$$
1 = p_1 f_1 + p_2 f_2 + p_3 (gz - 1)
$$

or

$$
1 = z^2 (x^2 + 2x + 1) + (x^2 z^2 + xz^2 + xz) y + (-xz - z - 1)(gz - 1)
$$

Now for the slick trick! We're working in an ideal containing $zg - 1$,
which means that $z = \frac{1}{g}$ in all of our computations[^2]! So let's
take this expression and plug in $z = \frac{1}{g}$ to get

$$
1 = 
\frac{1}{g^2} f_1 + 
\left ( \frac{x^2}{g^2} + \frac{x}{g^2} + \frac{x}{g} \right ) f_2 +
\left ( -\frac{x}{g} - \frac{1}{g} - 1 \right ) 0
$$

Of course, we can clear the denominators by multiplying through by $g^2$ to see

$$
g^2 = f_1 + (x^2 + x + xg) f_2 \in (f_1, f_2)
$$

So we found that, for some $n$, $g^n \in (f_1, f_2)$. As desired.

---

It turns out that this is _exactly_ how the proof goes in general! 

Say you give me polynomials $f_1, \ldots, f_r, g \in k[x_1, \ldots, x_m]$
so that $g$ vanishes whenever all the $f_i$ do.

Then we look at the ideal (in $k[x_1, \ldots x_m, z]$)

$$(f_1, \ldots, f_r, zg - 1)$$

which must equal $(1)$ by the weak nullstellensatz.

Then a computation, which sage will happily do for us, gives us polynomials
$p_1, \ldots, p_{r+1} \in k[x_1, \ldots, x_m, z]$ so that

$$
1 = p_1 f_1 + \ldots + p_r f_r + p_{r+1} (zg - 1)
$$

Then we plug in $\frac{1}{g}$ for $z$ to get a new expression

$$
1 = 
p_1 \left ( \vec{x}, \frac{1}{g} \right ) f_1(\vec{x})
+ \ldots +
p_r \left ( \vec{x}, \frac{1}{g} \right ) f_r(\vec{x})
$$

This is a polynomial with $g$s in the denominator. So we multiply both sides
by some $g^n$ to clear denominators, and we find

$$
g^n = g^n p_1( \vec{x}, 1 ) f_1 + \ldots + g^n p_r( \vec{x}, 1 ) f_r
$$

Notice that the $p_i(\vec{x}, 1)$ are polynomials in $x_1, \ldots, x_m$, 
since we've plugged in $1$ for $z$ everywhere. This means we've shown
$g^n$ is a linear combination of the $f_i$, so $g^n \in (f_1, \ldots, f_r)$,
as desired.

---

Another quick post today! Hopefully other people find this helpful too ^_^.

I do have a few bigger ones in the pipeline, but I won't say exactly what.
I've learned that saying what post you're planning to write next is a 
guaranteed way to not actually write it, haha.

See you soon!

---

[^1]:
    If you're interested in this, you'll want to read about 
    [gröbner bases][1]. The actual algorithm for computing with
    these is [buchberger's algorithm][2].

    I really liked Adams and Loustaunau's 
    _An Introduction to Gröbner Bases_, which is a very polite 
    introduction. I've heard great things about Cox, Little, and O'Shea's
    _Ideals, Varieties, and Algorithms: An Introduction to 
    Computational Algebraic Geometry and Commutative Algebra_, though I 
    haven't gotten around to reading it myself.

[^2]:
    There's a lot to be said about precisely why this trick works. It's 
    really because we're looking at the homomorphism 

    $$
    k[x,y,z] \to k(x,y)
    $$

    sending $x \mapsto x$, $y \mapsto y$, and $z \mapsto \frac{1}{g}$.

    This is quickly seen to be injective, so it preserves and reflects truth.
    We solve our problem in $k(x,y)$, but recover a formula of polynomials
    in $x$ and $y$ that gets reflected back to $k[x,y]$ under this embedding.

    For more information about this technique of "permanence of identities",
    you can see [this][4] blog post of mine.



[1]: https://en.wikipedia.org/wiki/Gr%C3%B6bner_basis
[2]: https://en.wikipedia.org/wiki/Buchberger%27s_algorithm
[3]: https://en.wikipedia.org/wiki/Rabinowitsch_trick
[4]: /2021/05/05/initial-polynomial-proofs.html
