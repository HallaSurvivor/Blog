---
layout: post
title: A Follow Up -- Explicit Error Bounds
tags:
  - quick-analysis-tricks
date: 2022-01-05 13:14
---

In my [previous post](/2022/01/05/probability-sums) I talked about how we can 
use probability theory to make certain scary looking limits obvious. I mentioned
that I would be writing a follow up post actually _doing_ one of the derivations
formally, and for once in my life I'm going to get to it quickly! Since I still
consider myself a bit of a computer scientist, it's important to know the rate
at which limits converge, and so we'll keep track of our error bounds throughout
the computation. Let's get to it!

<div class=boxed markdown=1>
Let $f : \mathbb{R} \to \mathbb{R}$ be bounded and locally lipschitz. Then
for every $x \gt 0$,

$$
\displaystyle 
e^{-nx} \sum_{k=0}^\infty \frac{(nx)^k}{k!} f \left ( \frac{k}{n} \right )
= f(x) \pm \widetilde{O}_x \left ( \frac{1}{\sqrt{n}} \right )
$$
</div>

$\ulcorner$

In the interest of exposition, I'll show far more detail than I think is
required for the problem. Hopefully this shows how you might come up with
each step yourself.

Let $X_n$ be poisson with parameter $nx$. Then notice

$$
e^{-nx} \sum_{k=0}^\infty \frac{(nx)^k}{k!} f \left ( \frac{k}{n} \right )
= \mathbb{E} \left [ f \left ( \frac{X_n}{n} \right ) \right ]
$$

Now we compute

$$
\begin{align}
\left | \mathbb{E} \left [ f \left ( \frac{X_n}{n} \right ) \right ] - fx \right |
&=
\left | \int f \left ( \frac{X_n}{n} \right ) \ d \mathbb{P}(X_n) - \int fx \ d \mathbb{P}(X_n) \right | \\
&=
\left | \int f \left ( \frac{X_n}{n} \right ) - fx \ d \mathbb{P}(X_n) \right |
\end{align}
$$

Now we use an _extremely_ useful trick in measure theory! We'll break up
this integral into two parts. One part where the integrand behaves well,
and one part (of small measure) where the integrand behaves badly.

Using our intuition that $\frac{X_n}{n} \approx x$, we'll partition into
two parts: 

- $\left \lvert \frac{X_n}{n} - x \right \rvert \lt \delta_n$ (the "good" set)
- $\left \lvert \frac{X_n}{n} - x \right \rvert \geq \delta_n$ (the "bad" set)

We'll be able to control the first part since there our integrand is $\approx 0$,
and we'll be able to control the second part since it doesn't happen often. 
Precisely, we'll use a [chernoff bound](https://en.wikipedia.org/wiki/Chernoff_bound).
There's a whole zoo of things called "chernoff bounds", all subtly different,
but any one of them will be good enough for our purposes here. I'm just using
[the first one that came up][1] when I googled "poisson chernoff bounds" :P.

So we split our integral:

$$
\begin{align}
& \left | \int f \left ( \frac{X_n}{n} \right ) - fx \ d \mathbb{P}(X_n) \right | \\
&\leq 
\left | 
  \int_{\left | \frac{X_n}{n} - x \right | \lt \delta_n} f \left ( \frac{X_n}{n} \right ) - fx \ d \mathbb{P}(X_n) 
\right |
+
\left |
  \int_{\left | \frac{X_n}{n} - x \right | \geq \delta_n} f \left ( \frac{X_n}{n} \right ) - fx \ d \mathbb{P}(X_n) 
\right | \\
&\leq 
\int_{\left | \frac{X_n}{n} - x \right | \lt \delta_n} 
\left |
  f \left ( \frac{X_n}{n} \right ) - fx 
\right |
\ d \mathbb{P}(X_n) 
+
\int_{\left | \frac{X_n}{n} - x \right | \geq \delta_n} 
\left |
  f \left ( \frac{X_n}{n} \right ) - fx 
\right |
\ d \mathbb{P}(X_n) 
\end{align}
$$

Now since $f$ is locally lipschitz, we know that in a neighborhood of $x$,
we must have $$|f(y) - f(x)| \leq M_x |y - x|$$. So for $\delta_n$ small enough,
we'll have (in the "good" set)

$$\left | f \left ( \frac{X_n}{n} \right ) - fx \right | \leq M_x \left | \frac{X_n}{n} - x \right | \leq M_x \delta_n$$

Since $f$ is bounded, say by $\lVert f \rVert_\infty$, 
we know that no matter what we'll have

$$
\left | f \left ( \frac{X_n}{n} \right ) - fx \right | \leq 
\left | f \left ( \frac{X_n}{n} \right ) \right | + \left | fx \right | \leq 
2 \lVert f \rVert_\infty
$$

Putting these estimates into the above integral, we find[^1]

$$
\begin{align}
&\leq 
\int_{\left | \frac{X_n}{n} - x \right | \lt \delta_n} M_x \delta_n \ d \mathbb{P}
+
\int_{\left | \frac{X_n}{n} - x \right | \geq \delta_n} 2 \lVert f \rVert_\infty \ d \mathbb{P} \\
&=
(M_x \delta_n) \mathbb{P} \left ( \left | \frac{X_n}{n} - x \right | \geq \delta_n  \right )
+
2 \lVert f \rVert_\infty \mathbb{P} \left ( \left | \frac{X_n}{n} - x \right | \geq \delta_n  \right ) \\
\end{align}
$$

since we can pull the constants out of the integral, then get the measures
of the "good" and "bad" sets.

Now the good set has measure at most $1$[^2], and [chernoff bounds][1]
show that the bad set has exponentially small measure:

$$
\begin{align}
\mathbb{P} \left ( \left | \frac{X_n}{n} - x \right | \geq \delta_n \right )
&=
\mathbb{P} \left ( \left | X_n - nx \right | \geq n\delta_n \right ) \\
&\leq
2 \exp \left ( \frac{-(n \delta_n)^2}{2(xn + n \delta_n)} \right ) \\
&=
2 \exp \left ( \frac{-n \delta_n^2}{2(x + \delta_n)} \right )
\end{align}
$$

So plugging back into our integral, we get

$$
\leq M_x \delta_n + 2 \lVert f \rVert_\infty 2 \exp \left ( \frac{-n \delta_n^2}{2(x + \delta_n)} \right )
$$

We want to show that this goes to $0$, and all we have in control over
the sequence $\delta_n$. 
$M_x$ is a constant, so we have to have $\delta_n \to 0$. 
Likewise $4 \lVert f \rVert_\infty$ is a constant, so we need 
$\exp \left ( \frac{-n \delta_n^2}{2(x + \delta_n)} \right ) \to 0$.
Since the stuff in the exponent is negative and 
$2(x + \delta_n) \approx 2x$ is a constant, that roughly means we need $n \delta_n^2 \to \infty$.

We can choose any $\delta_n$ we like which satisfies these two properties,
but it's somewhat difficult to find something that works.
We notice that $\delta_n = n^{-\frac{1}{2}}$ just _barely_ fails, since
$n^{- \frac{1}{2}} \to 0$, but $n \left ( n^{- \frac{1}{2}} \right )^2 \to 1$.

If we pick $\delta_n$ just a _smidge_ bigger than $n^{- \frac{1}{2}}$, say,
$n^{- \frac{1}{2}} \log(n)$, that should get the job done[^3]. 
Clearly $M_x n^{- \frac{1}{2}} \log(n) = \widetilde{O}\left ( n^{-\frac{1}{2}} \right )$,
and moreover

$$
\exp 
\left ( 
  \frac
  {-n \left ( n^{-\frac{1}{2}}\log(n) \right )^2}
  {2 \left ( x + n^{-\frac{1}{2}} \log(n) \right )} 
\right )
= n^{- \frac{1}{2} \frac{1}{\frac{x}{\log(n)} + \frac{1}{\sqrt{n}}}}
$$

and a tedious L'hospital rule computation shows that this is eventually less
than $n^{- \frac{1}{2}} \log(n)$.

So what have we done?

We started with

$$
\left | 
  e^{-nx} \sum_{k=0}^\infty \frac{(nx)^k}{k!} f \left ( \frac{k}{n} \right ) - f(x)
\right |
= \left | \mathbb{E} \left [ f \left ( \frac{X_n}{n} \right ) \right ] - f(x) \right |
$$

and we showed this is at most

$$
M_x \delta_n + 2 \lVert f \rVert_\infty 2 \exp \left ( \frac{-n \delta_n^2}{2(x + \delta_n)} \right )
= O_x \left ( \frac{\log(n)}{\sqrt{n}} \right )
= \widetilde{O}_x \left ( \frac{1}{\sqrt{n}} \right )
$$

So, overall, we have

$$
e^{-nx} \sum_{k=0}^\infty \frac{(nx)^k}{k!} f \left ( \frac{k}{n} \right ) 
= f(x) + \widetilde{O}_x \left ( \frac{1}{\sqrt{n}} \right )
$$

as promised.

<span style="float:right">$\lrcorner$</span>

---

[^1]:
    In the interest of continuing the quick analysis trick tradition of 
    saying the obvious thing, notice what we've done here. We want to 
    control an integral. How do we do it?

    We break it up into a "good" piece, which is big, and a "bad" piece, which
    is small.

    The "good" piece we can control because it's good. For us, this means
    $f \left ( \frac{X_n}{n} \right ) \approx f(x)$, so their difference is
    $\approx 0$.

    The "bad" piece we _can't_ control in this way. Indeed it's _defined_ to
    be the piece that we can't control in this way. Thankfully, if all is
    right with the world, the "bad" piece will be small! So we get some
    crummy (uniform) estimate on the bad piece, and then multiply by the 
    size of the piece. Since the size is going to $0$ and our bound is 
    uniform (even if it's bad), we'll win!

[^2]:
    Notice just like we were content with a crummy bound on the integrand
    of the bad piece because we're controlling the measure, we're content with
    a potentially crummy bound on the measure of the good piece because we're
    controlling the integrand!

    Of course, for our particular case, $1$ is actually a fairly good bound 
    for the measure of the good piece, but we don't need it to be.

[^3]:
    In fact, $\delta_n = n^{- \frac{1}{2} + \epsilon}$ _also_ gets the 
    job done, but the computation showing

    $$
    \exp \left ( \frac{-n \delta_n^2}{2(x + \delta_n)} \right ) = O(\delta_n)
    $$

    is _horrendous_. 

[1]: https://math.stackexchange.com/questions/2434883/chernoff-style-bounds-for-poisson-distribution
