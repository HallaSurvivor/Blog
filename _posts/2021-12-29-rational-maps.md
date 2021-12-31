---
layout: post
title: Rational maps $\mathbb{P}^1 \to \mathbb{P}^n$ are automatically regular
tags:
  - 
---

The other day a friend of mine was asking for help with an algebraic geometry
problem. I was happy to walk her through it, and because she and I were doing
this online, I actually have a record of what I sent her! She seemed to think 
it was helpful, so I figured I would post (a slightly edited version of) it ^_^.

What's the problem we're solving today? Well:

<div class=boxed markdown=1>
Prove every rational map $f : \mathbb{P}^1 \to \mathbb{P}^n$ is regular
</div>

Let's work with $f : \mathbb{P}^1 \to \mathbb{P}^2$ for concreteness. 
Everything we're about to say will also work for $\mathbb{P}^n$, though. 
It's just a bit more annoying to manage all the indices.

Let's first remember what a rational map 
(from $\mathbb{P}^1 \to \mathbb{P}^2$) _is_. It's given by a family of ratios 
of homogeneous polynomials $f_i(x,y)$ and $g_i(x,y)$:

$$f = \left ( \frac{f_0}{g_0} : \frac{f_1}{g_1} : \frac{f_2}{g_2} \right )$$

where $f_0$ and $g_0$ have the same degree, $f_1$ and $g_1$ have the same degree, 
and $f_2$ and $g_2$ have the same degree.

Why is this? Well we're choosing a point in $\mathbb{P}^2$ 
(which is given by an equivalence class of $3$ affine points) 
for each point of $\mathbb{P}^1$. Moreover, we want to do this in a "rational"
way. So each coordinate of the output should be a rational function of the input[^1].

Now, there are two things to remember about rational maps that might be 
counterintuitive at first:

The first is that $f$ is only defined on an _open set_ of $\mathbb{P}^1$. 
More generally, for a projective variety $V$, a rational map might not be
defined everywhere. After all, if one of the $g_i(a,b) = 0$, then $f$ will
be undefined at $(a:b)$! 

<div class=boxed markdown=1>
Can you show that any such $f$ is defined on some Zariski open set? 
Phrased another way, can you show the set of points where $f$ _isn't_ 
defined is Zariski closed?

Notice this sounds worse than it is! Remember that Zariski open sets are
always dense, so even though $f$ might not be defined _everywhere_, it's
defined on a dense set, which is almost as good.
</div>

The second pitfall is that it's entirely possible for the same rational map 
two have multiple _representations_. For a simple example, notice

$$
\left ( \frac{x^2}{y^2} : \frac{x}{y} : 1 \right )
$$

and

$$
\left ( \frac{3x^2}{y^2} : \frac{3x}{y} : 3 \right )
$$

define the same map $\mathbb{P}^1 \to \mathbb{P}^2$. After all, for any $(a:b)$
where both of these functions are defined (so where $b \neq 0$), the outputs
of these two functions differ by a factor of $3$, so they fall into the same
equivalence class in projective space.

But there's subtler examples too. For instance,

$$
\left ( \frac{x^2}{y^2} : \frac{x}{y} : 1 \right )
$$

and

$$
\left ( 1 : \frac{y}{x} : \frac{y^2}{x^2} \right )
$$

_also_ represent the same function! 

Why? Because if we only look at the places where both of these functions
are defined, they represent the same point in $\mathbb{P}^2$!

The first function is defined at $y \neq 0$, and the second at $x \neq 0$. 
So if we restrict attention to the points $(a:b)$ where $a \neq 0$ and $b \neq 0$,
we see the first map gives $$\left ( \frac{a^2}{b^2} : \frac{a}{b} : 1 \right )$$ and the second
gives $$\left (1 : \frac{b}{a} : \frac{b^2}{a^2} \right )$$. But these are the same point in 
projective space because they differ by a factor of $\frac{b^2}{a^2}$, which is a constant.

<div class=boxed markdown=1>
As an instructive exercise, show that if $h(x,y)$ is _any_ nonzero homogeneous polynomial, 
then 

$$\left ( \frac{f_0}{g_0} : \frac{f_1}{g_1} : \frac{f_2}{g_2} \right )$$

and

$$\left ( h \frac{f_0}{g_0} : h \frac{f_1}{g_1} : h \frac{f_2}{g_2} \right )$$

and 

$$\left ( \frac{1}{h} \frac{f_0}{g_0} : \frac{1}{h} \frac{f_1}{g_1} : \frac{1}{h} \frac{f_2}{g_2} \right )$$

all represent the same regular function from $\mathbb{P}^1 \to \mathbb{P}^2$.
</div>

Of course, it seems like we should be able to use this in order to solve the
"only defined on an open set" issue. After all, in light of the previous 
exercise, writing

$$
\left ( \frac{x^2}{y^2} : \frac{x}{y} : 1 \right )
$$

seems like a silly thing to do! We should just multiply everything in sight
by the (nonzero, homogeneous) polynomial $y^2$ to get the equivalent function

$$
(x^2 : xy : y^2)
$$

which is defined _everywhere_! Notice there doesn't seem to be anything special
about our particular function $f$. It feels like we should _always_ be able to
"clear denominators" in this way to find an equivalent function which is defined
everywhere... Right?

Unfortunately, no. For example, consider the map 
$\phi : \mathbb{P}^2 \to \mathbb{P}^2$ given by

$$
\phi : (a : b : c) \mapsto (bc : ac : ab)
$$

This looks fine, right? How could it be undefined at a point? Well remember 
that $(0 : 0 : 0)$ is _not_ a point in projective space! 

<div class=boxed markdown=1>
Can you see why $\phi$ is undefined at $(0:0:1)$, $(0:1:0)$, and $(1:0:0)$?

Moreover, you should (intuitively) convince yourself that no amount of 
rescaling by homogeneous polynomials will solve the problem.
</div>

Now, we say that a rational map $f$ is "**regular** at a point $p$" exactly when
$\tilde{f}(p)$ is defined for some $\tilde{f}$ representing the same map as $f$. 
If we simply say that $f$ is **regular**, then we mean it is regular everywhere.

So $f = (x^2 : xy : y^2) : \mathbb{P}^1 \to \mathbb{P}^2$ is regular, whereas
$\phi$ is regular everywhere except for the $3$ points listed above.

Importantly, $\tilde{f} = \left ( \frac{x^2}{y^2} : \frac{x}{y} : 1 \right )$ 
is regular as well! Because it has an equivalent representation, $f$, which
is regular everywhere.

Now, surprisingly, examples like $\phi$ cannot exist for maps 
$\mathbb{P}^1 \to \mathbb{P}^2$. The _only_ way for a rational function 
$f : \mathbb{P}^1 \to \mathbb{P}^2$ to be undefined at a point is because we 
did something stupid when writing $f$ down. If we rescale by an appropriate 
homogeneous polynomial, we can remove the apparently singular points.

---

So! How are we going to show this? Well it turns out regularity is like 
continuity/differentiability/etc. 

Just like continuity/differentiability of $f$ at $x$ only depends on what $f$ 
does in a _neighborhood_ of $x$, regularity only cares about what happens in a 
_neighborhood_ of $(a:b)$[^2]. 

Now importantly, there are two useful open sets which we _know_ cover 
$\mathbb{P}^1$! We have the "open affine charts"

- $$U_x = \{ (x:1) \}$$, which is open since it agrees with $$\{ y \neq 0 \}$$
- $$U_y = \{ (1:y) \}$$, which is open since it agrees with $$\{ x \neq 0 \}$$

So if we check that $f$ is regular at $(a:b)$ in each of these charts, we'll be done! 

Let's do the check for the $U_x$ chart together. You should work through the 
$U_y$ chart afterwards. Of course, it'll be extremely similar ^_^.

---

So let's take our representation

$$
f(x,y) = 
\left ( 
\frac{f_0(x,y)}{g_0(x,y)} : \frac{f_1(x,y)}{g_1(x,y)} : \frac{f_2(x,y)}{g_2(x,y)} 
\right )
$$

and plug in $y=1$ everywhere (since we're working in the $y=1$ chart). 
This will give us a new function

$$
f(x) = f(x,1) = 
\left ( 
\frac{f_0(x)}{g_0(x)} : \frac{f_1(x)}{g_1(x)} : \frac{f_2(x)}{g_2(x)} 
\right )
$$

where I'm somewhat abusively calling $f_i(x,1)$ simply $f_i(x)$ 
(and the same with the $g_i$s).

But now we have simple quotients of _single_ variable polynomials! 
We want to know that $f(a)$ is well defined, 
(or at least that we can massage $f$ in order to _make_ $f(a)$ well defined), 
so we ask, "what can go wrong"? 

There's two answers:

1. "one of the $g_i(a) = 0$". 
2. "all of the $f_i(a) = 0$ simultaneously".

The dream, then, is to show that we can massage the $f_i$ and $g_i$ to ensure
neither of these happens!

But now we can solve each of these problems in turn.

First, we can clear denominators. We rewrite

$$
\left ( \frac{f_0}{g_0} : \frac{f_1}{g_1} : \frac{f_2}{g_2} \right )
$$

as

$$
\left ( g_1 g_2 f_0 : g_0 g_2 f_1 : g_0 g_1 f_2 \right )
$$

which solves the "$0$ in the denominator" problem.

Next, we look to solve the "simultaneously $0$" problem. But these are all
polynomials of one variable! So the only way they can all be $0$ at a point $a$
is if $(x-a)$ divides all of them!

So we divide everything by the (nonzero, homogeneous) polynomial $x-a$!

Each of our three polynomials has only finitely many roots, so we only have
to clear away finitely many shared factors of this form. In particular, we 
eventually stop, and at that point the coordinates are never simultaneously $0$.

And we're done!

I'll leave it to you to do the (entirely symmetric!) argument showing that $f$ 
is regular at $(1:b)$ for every $b$ too, which will finish the problem.

<div class=boxed markdown=1>
As a quick exercise, which will hopefully be instructive nonetheless, where
in this proof do we use the fact that we're working with $\mathbb{P}^1$? 

Also, if you're feeling dedicated, can you generalize this to all rational
maps $f : \mathbb{P}^1 \to \mathbb{P}^n$? It's the exact same proof, there's
just more indices to worry about.
</div>

---

Hopefully this helps some people! I know algebraic geometry is a tricky subject,
and it seems like there aren't a _ton_ of really simple examples that are
easy to find. I'm happy to add one to the pile ^_^.

Now, though, I need to head out! It's new years eve, and I have to bake some
muffins for a little get together! 

Stay safe, stay warm, and happy new year everyone ^_^

---

[^1]:
    As an aside, have you thought about why the degrees of, say $f_0$ and $g_0$ must
    be equal? We want to know that our function is _well defined_, so if we pick
    two different representatives of the same projective point, we should get
    the same output. 

    But if $\text{deg}(f) = \text{deg}(g) = d$, then for 
    $(a,b) \sim (\lambda a , \lambda b)$ we have

    $$
    \frac{f(\lambda a , \lambda b)}{g(\lambda a , \lambda b)} =
    \frac{\lambda^d f(a , b)}{\lambda^d g(a , b)} =
    \frac{f(a , b)}{g(a , b)}
    $$

    so the function $(a:b) \mapsto \frac{f(a,b)}{g(a,b)}$ is well defined!

[^2]:
    As an aside, this is the telltale sign of a "sheaf" of functions, but
    I won't go into that here.
