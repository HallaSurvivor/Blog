---
layout: post
title: Automatic Asymptotics with Sage -- Redux
tags:
  - sage
---

Another day, another blog post that starts with 
"I was on mse the other day...". This time, someone asked 
[an interesting question][8] amounting to "how many *unordered* rooted 
ternary trees with $n$ 
nodes are there, up to isomorphism?". I'm a sucker for these kinds of 
combinatorial problems, and after finding a generating function solution 
I wanted to push myself to get an asymptotic approximation using 
Flajolet--Sedgewick style analytic combinatorics! I learned a lot, and 
want to share some of the things I learned, especially how to do this 
stuff in [sage][1]

Now, you might be thinking -- didn't you write a very similar blog post 
[three years ago][2]? Yes. Yes I did. Did I also *completely* forget what 
was in that post? Yes. Yes I did, haha. For some reason I was getting it mixed 
up with this [other post][3] from even more years ago, which isn't nearly 
as relevant. Thankfully it didn't matter much, 
since I'm fairly sure what I wanted to do wouldn't work in the framework of 
that post anyways, and now I have a better idea of what this machinery is 
*actually doing* which is really exciting (since I've been 
*wanting* to understand this stuff for years).

---

Let's start with a warmup problem! How might we count the number of 
rooted _ordered_ ternary trees with $n$ nodes?

These are the kinds of "ternary trees" that you might remember from a 
first class on algorithms and data structures. Such a tree is either 
a leaf or an internal node with 1,2, or 3 children. Crucially these 
children come with an _order_, because the datatype keeps track of which 
child is on the left/right (in the case of 2 children) or on the 
left/middle/right (in the case of 3 children). After all, from a CS 
perspective, we need to remember this in order to traverse the tree!

This means that the following two trees are distinct for our purposes, even 
though they're isomorphic as graphs:

<p style="text-align:center;">
<img src="/assets/images/automatic-analytic-combinatorics/two-trees.png" width="50%">
</p>

In a functional programming language, you might describe this datatype by 

```
T z = Leaf z
    | Unary z (T z)
    | Binary z (T z) (T z) 
    | Ternary z (T z) (T z) (T z)
```

and this translates immediately to give a functional equation for the 
[generating function][4] of $t_n$, which counts the number of rooted ordered 
ternary trees with $n$ nodes:

$$
T(z) = z + zT + zT^2 + zT^3
$$

We can rearrange this as 

$$
z = \frac{T}{1 + T + T^2 + T^3}
$$

so that we can compute the power series expansion of $T$ by 
[lagrange inversion][5]:

<div class="linked_auto">
<script type="text/x-sage">
R.<z> = QQbar[[]] # power series ring
T = (z/(1 + z + z^2 + z^3)).reverse()
show(T.O(10))
</script>
</div>

Incredibly, this agrees with [A036765][6], which is the 
"number of ordered rooted trees with n non-root nodes and all outdegrees 
&lt;= three", as we hoped! 

You might reasonably ask if there's a closed form for these numbers, and 
this is too much to ask for (indeed, it's already too much to ask for a 
closed form for fibonacci numbers, and this is *more* complicated). But like 
the fibonacci numbers, we can come up with an excellent approximation:

$$
t_n = [z^n] T \approx 
C \frac{(3.6107\ldots)^n}{n^{3/2}} 
\left (1 \pm O \left ( \frac{1}{n} \right ) \right )
$$

where $C = \frac{(0.8936\ldots)}{2 \sqrt{\pi}}$ is a constant.

Indeed, this gives *fantastic* results! Let's plot the ratio of this 
approximation to the true value so we can see *just* how good this approximation 
gets as $n$ gets large. Note that it respects the promised big-oh error bound 
too!

<div class="linked_auto">
<script type="text/x-sage">
def actual(n,N):
    R.<z> = PowerSeriesRing(QQbar, default_prec=N)
    T = (z/(1 + z + z^2 + z^3)).reverse()
    return T.coefficients()[n-1:]

def approx(n,N): 
    # very very magic
    C = 0.8936373911078061 / (2 * sqrt(pi))
    w = 3.610718613276040
    return [(C * w^k * (1/k^1.5)).n() for k in range(n,N+1)]

show(html("Plot the error ratios in the range [n,N]"))
@interact
def _(n=input_box(100, width=20, label="$n$"),
      N=input_box(120, width=20, label="$N$"),
      auto_update=False): 

    actuals = actual(n,N)
    approxs = approx(n,N)
    ratios  = [(actuals[i]/approxs[i]) for i in range(N+1-n)]
    show(html("ratio at n={}: {}".format(n, ratios[0])))
    show(html("ratio at N={}: {}".format(N, ratios[-1])))

    text_options = {'horizontal_alignment': 'right',
                    'vertical_alignment': 'bottom', 
                    'fontsize': 'large'}

    G = Graphics()
    G += scatter_plot([(n+i,r) for (i,r) in enumerate(ratios)])
    G += plot(1, (x,n,N))
    G += plot(1-1/x, (x,n,N))
    G += text('$y = 1$', (N, 1), **text_options)
    G += text('$y = 1-1/x$', (N, 1-1/N), **text_options)

    G.show()

</script>
</div>

This is extremely cool, but *where the hell did these asymptotics come from*?

The answer is called <span class=defn>Singularity Analysis</span>, and 
can be found in Chapter 2 Section 3 of Melczer's excellent 
[_An Invitation to Analytic Combinatorics_][7].

I won't go in depth into why it works[^1], but like every theorem in 
complex analysis[^2] it comes down to [Cauchy's Integral Formula][11]:

$$
t_n = \frac{1}{2\pi i} \int_C \frac{T}{z^{n+1}} \ \mathrm{d}z
$$

Recall that a holomorphic function will converge until it has a good reason 
not to -- that is, until we hit a singularity. See, for instance, [here][9]. 
This tells us that if $\omega$ is the **dominant singularity** 
(that is, the singularity of $T$ closest to the origin) then the radius 
of convergence is $R = \frac{1}{|\omega|}$. 
In fact, since all our coefficients are positive (they count things, after all),
$\omega$ will already by positive real by the [Vivanti–Pringsheim theorem][10],
so we don't need to write $|\omega|$.

Now let's compute $t_n$ using a circle of radius $r \lt R$:

$$
\begin{align}
t_n 
&= 
\left | 
    \frac{1}{2 \pi i} 
    \int_0^{2\pi} \frac{T(r e^{i \theta})}{(r e^{i \theta})^{n+1}} \ \mathrm{d} \theta
\right | \\
&\leq
\frac{1}{2 \pi}
\int_0^{2\pi} 
\frac{|T(r e^{i \theta})|}{|r e^{i \theta}|^{n+1}} \ \mathrm{d} \theta \\
&=
\frac{1}{r^{n+1}2 \pi} \int_0^{2 \pi} |T(r e^{i \theta})| \ \mathrm{d} \theta \\
&\overset{\star}{\leq}
\frac{1}{r^{n+1}2 \pi} M 2 \pi r \\
&= \frac{M}{r^n} = O(r^{-n})
\end{align}
$$

now letting $r \to R = \omega$, we see that $t_n \approx \omega^{-n}$.

In step $(\star)$ here, we've used compactness of the circle to argue that 
$|T|$ attains a maximum value $M$ somewhere on the circle, then estimated 
the integral by the circumference times this maximum value[^3].

This already gets us partway to our goal, since we'll soon compute that 
$\omega^{-1} \approx 3.6107\ldots$, explaining our first magic constant and 
our dominant term!

It also shows an obvious way to improve our estimate: We just need to 
better understand $M$!

To do this, let's draw the most important picture in complex analysis:

<p style="text-align:center;">
<img src="/assets/images/automatic-analytic-combinatorics/contour.png" width="50%">
</p>

Here the obvious marked point is our singularity $\omega$, and we've 
chosen a [branch cut][12] for $T$ (shown in blue[^4]) so that $T$ is 
holomorphic in the region where the pink curve lives. The hope is that 
integrating along this pink curve will give us better control over $M$.

Indeed, by taking the pink curve to stay *really* close to the branch cut,
we can approximate our integral by the sum of the integral over a big circle
(centered at $0$) circle and the integral over a little cirlce (centered at $\omega$).

The same argument as before shows the integral over the big circle 
(of radius $S \gt \omega$) is roughly $\frac{M}{S^n)$ for $M$ the maximum 
value on the big circle... It seems like we're not getting anywhere, until 
we remember that regardless of what $M$ is this is $o(\omega^{-n})$ 
(since $S^{-n} \lt \omega^{-n}$), so asymptotically vanishes compared to 
our dominant term, no matter *what* constant $M$ happens to be!

This tells us that our estimate for $t_n$ has to be entirely based in our 
estimate for the integral over the little circle[^5], which stays really 
close to $\omega$. This means if we can get a good estimate of $T$ near 
$\omega$ we would win, and thankfully, there's a tool for exactly this job:
[Puiseux Series][13]! 

I won't say much about what these are[^6], especially since 
Richard Borcherds already put out such a [great video][14] on the topic.
What matters is that we can expand $T$ into a kind of power series near 
$\omega$, and use this to improve our estimate! For us, we'll have 

$$T \approx (0.65\ldots) - (0.8936\ldots) (1-z/\omega)^{1/2} \pm O(z/\omega)$$

This shows where our second magic number came from -- it's the coefficient 
of $(1-z/\omega)^{1/2}$ in the puisseux series expansion of $T$!
But again... why?

Well let's estimate our integral around the small contour -- (most of) a 
circle of radius $r$ centered at $\omega$. We're going to be a bit 
sloppy here, but it gets the point across:

$$
\begin{align}
t_n 
&\approx 
\frac{1}{2\pi} \int_\epsilon^{2 \pi - \epsilon} 
\frac{|T(\omega + r e^{i \theta})|}{|\omega + r e^{i \theta}|^{n+1}} 
\ \mathrm{d} \theta \\
&\approx
\frac{1}{2\pi}
\int_{\epsilon}^{2 \pi - \epsilon}
\frac
{|c_0  + c_{1/2} \left ( \frac{r}{\omega} e^{i \theta} \right )^{1/2} \pm O(\frac{r}{\omega})|}
{\omega^{n+1}} \ \mathrm{d} \theta \\
&\leq
\frac{1}{2\pi \omega^{n+1}}
\left (
\int_{\epsilon}^{2 \pi - \epsilon} |c_0| \ \mathrm{d} \theta
+
\int_{\epsilon}^{2 \pi - \epsilon} |c_{1/2}| (\frac{r}{\omega})^{1/2} \ \mathrm{d} \theta
\pm
O \left ( \int_\epsilon^{2 \pi - \epsilon} \frac{r}{\omega} \ \mathrm{d} \theta \right )
\right ) \\
&\approx 
\frac{1}{2 \pi \omega^{n+1}}
\left ( O(1) + |c_{1/2}| (\frac{r}{\omega})^{1/2} 2 \pi r \pm O(\frac{r^2}{\omega}) \\
&\approx

\end{align}
$$

TODO: fix this. You need to use the general binomial theorem to expand 
$(1 - z/\omega)^{1/2}$...

---

[1]: https://sagemath.org
[2]: /2022/01/20/automatic-asymptotics.html
[3]: /2021/06/17/iteration-asymptotics.html
[4]: https://en.wikipedia.org/wiki/Generating_function
[5]: https://en.wikipedia.org/wiki/Lagrange_inversion_theorem
[6]: https://oeis.org/A036765
[7]: https://melczer.ca/files/Melczer-SubmittedManuscript.pdf
[8]: https://math.stackexchange.com/q/5050941/655547
[9]: https://en.wikipedia.org/wiki/Analyticity_of_holomorphic_functions
[10]: https://en.wikipedia.org/wiki/Vivanti%E2%80%93Pringsheim_theorem
[11]: https://en.wikipedia.org/wiki/Cauchy%27s_integral_formula
[12]: https://en.wikipedia.org/wiki/Branch_point#Branch_cuts
[13]: https://en.wikipedia.org/wiki/Puiseux_series
[14]: https://www.youtube.com/watch?v=paenRVq0vnc

[^1]:
    After all, I want this to be a fairly quick post like my other 
    recent ones. Though it's already shaping up to be... less quick, haha.

[^2]:
    This is only a little bit of an exaggeration. 

[^3]:
    I'm actually lying a bit here, since $M$ is really a function of $r$ 
    and is *not* usually $O(1)$ as $r \to R$. But we're about to talk about 
    how to get a better estimate on $M$ anyways, and that more careful 
    analysis will handle this for us. 

[^4]:
    Just like $w = \sqrt{z}$, a solution to $w^2 = z$ has branches, 
    so too does $T$, a solution to $T = z + zT + zT^2 + zT^3$.

[^5]:
    Really a circle with a little hole cut out, say by integrating from 
    $\epsion$ to $2 \pi - \epsilon$... But we'll end up taking 
    $\epsilon \to 0$ and we're all friends here, so let's not worry about it.

[^6]:
    This post isn't getting *quicker*, haha.
