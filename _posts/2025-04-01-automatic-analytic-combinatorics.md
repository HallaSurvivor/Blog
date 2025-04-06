---
layout: post
title: Analytic Combinatorics -- A Worked Example 
tags:
  - sage
---

TODO: change the name of this file, as well as the name of the 
associated folder, to match the new title.

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

This is extremely cool, but *where the hell did this approximation come from*?

The answer is called <span class=defn>Singularity Analysis</span>, and 
can be found in Chapter 2 Section 3 of Melczer's excellent 
[_An Invitation to Analytic Combinatorics_][7], or Chapters VI and VII 
of Flajolet and Sedgewick's [tome][18]. See especially Theorem 
VII.3 on pg 468.

Like seemingly every theorem in complex analysis, 
this is basically an application of the [Residue Theorem][11]. I won't say 
too much about why it works, but I'll at least gesture at a proof. You 
can read the above refrences if you want something more precise.

First, we [recall][19]

$$
t_n = \frac{1}{2\pi i} \int_C \frac{T}{z^{n+1}} \ \mathrm{d}z
$$

where $C$ is any contour containing the origin inside a region where $T$ 
is holomorphic. 

Then we draw the most important picture in complex analysis:

<p style="text-align:center;">
<img src="/assets/images/automatic-analytic-combinatorics/contour.png" width="50%">
</p>

Here the obvious marked point is our singularity $\omega$, and we've 
chosen a [branch cut][12] for $T$ (shown in blue[^4]) so that $T$ is 
holomorphic in the region where the pink curve lives. We'll estimate 
the value of this integral by estimating the contribution from the big 
circle, the little circle, and the two horizontal pieces[^5]. 

It turns out that the two horizontal pieces basically contribute $O(1)$ 
amount to our integral, so we ignore them. Since the big circle is compact,
$T$ will attain a maximal value on it, say $M$. Then the integral along 
the big circle is bounded by 
$2 \pi (\omega + \epsilon) \frac{M}{(\omega + \epsilon)^{n+1}} = O((\omega+\epsilon)^{-n})$

To estimate the integral around the little circle, it would be really 
helpful to have a series expansion at $\omega$ since we're staying 
really close to it... Unfortunately, $\omega$ is a singular point so we 
don't have a taylor series, but *fortunately* there's another tool 
for exactly this job: a [Puiseux Series][13]! 

I won't say much about what these are, especially since 
Richard Borcherds already put out such a [great video][14] on the topic.
What matters is is that Sage can compute this for us[^7], so we can actually 
get our hands on the approximation!

We compute the integral around the little circle to be roughly:

$$
\begin{align}
\frac{1}{2 \pi i} \int \frac{T}{z^{n+1}} 
\ \mathrm{d}z 
&\overset{(1)}{\approx}
\frac{1}{2 \pi i} \int \frac{c_\alpha (1-\frac{z}{\omega})^\alpha}{z^{n+1}}
\ \mathrm{d}z \\
&\overset{(2)}{=}
\frac{1}{2 \pi i} \int \frac{c_\alpha \sum_k \binom{\alpha}{k} (\frac{-z}{\omega})^k}{z^{n+1}}
\ \mathrm{d}z \\
&\overset{(3)}{=}
c_\alpha \binom{\alpha}{n} \frac{(-1)^n}{\omega^n}
\end{align}
$$

In step $(1)$ we approximate $T$ by the first term of its puiseux series,
in step $(2)$ we apply the generalized binomial theorem, so that in step 
$(3)$ we can apply the residue theorem to realize this integral as the 
coefficient of $z^{-1}$ in our laurent expansion.

This gives us something which grows like $\widetilde{O}(\omega^{-n})$,
dominating the contribution $O((\omega + \epsilon)^{-n})$ from the big circle,
so that asymptotically this is the only term that matters. If we were
more careful to keep track of the big-oh error for the puiseux series for $T$ 
we could easily sharpen this bound to see

$$
t_n = 
c_\alpha \binom{\alpha}{n} \frac{(-1)^n}{\omega^n} 
\left ( 1 + O \left ( \frac{1}{n} \right ) \right )
$$

This looks a bit weird with the $(-1)^n$, but remember that $\binom{\alpha}{n}$ 
also alternates sign. Indeed, asymptotics for $\binom{\alpha}{n}$ are 
[well known][20] so that we can rewrite this as[^9] 

TODO: finish footnote 9 by drawing a picture of a 2-keyhole contour

$$
t_n = 
\frac{c_\alpha}{\Gamma(-\alpha)} \frac{\omega^{-n}}{n^{\alpha + 1}} 
\left ( 1 + O \left ( \frac{1}{n} \right ) \right )
$$

Which finally shows us where our magic numbers came from! 
Sage happily tells us that the dominant singularity for $T$ is at 
$\omega = (0.2769\ldots)$ and that a puiseux expansion for $T$ at $\omega$ 
is

$$T \approx (0.65\ldots) - (0.8936\ldots) (1-z/\omega)^{1/2} + \ldots$$

so that for us $\alpha = 1/2$, and $C_{1/2} = -(0.8936\ldots)$.

Finally, since $\Gamma(-1/2) = -2 \sqrt{\pi}$ and 
$(0.2769\ldots)^{-1} = (3.6107\ldots)$ we see

$$
t_n = 
\frac{(0.8936\ldots)}{2 \sqrt{\pi}} \frac{(3.6107\ldots)^{n}}{n^{3/2}}
\left ( 1 + O \left ( \frac{1}{n} \right ) \right )
$$

as promised!

Indeed, here's how you could actually get sage to do all this for you!

<div class="linked_auto">
<script type="text/x-sage">
import abelfunctions

# to compute the discriminant we need P to be a polynomial whose 
# coefficients are polynomials.
R.<z> = QQbar[]
S.<T> = R[]

# our defining polynomial. We want to solve for T as a function of z
P = z*T^3 + z*T^2 + (z-1)*T + z

# following Example 2.12 in Melczer we compute the dominant singularity w. 
w = min([r for (r,_) in P.discriminant().roots() if r != 0], key=lambda r: r.abs())

# to work with abelfunctions we need P to be a polynomial in two variables
R.<z,T> = QQbar[]
P = R(P)

# compute the puiseux expansion for T at w. 
# I know from trial and error that the correct branch to pick is 
# entry [1] in the list. You just need to check which one gives 
# you positive real coefficients for T at 0.
s = abelfunctions.puiseux(P,w)[1]
c = -sqrt(-s.x0/s.xcoefficient)
</script>
</div>

---

Ok, now that we understand the warmup, let's get to the actual problem!

<div class=boxed markdown=1>
How many *unordered* rooted ternary trees are there, up to isomorphism?
</div>

Now we're counting up to graph isomorphism, so that our two trees 

<p style="text-align:center;">
<img src="/assets/images/automatic-analytic-combinatorics/two-trees.png" width="50%">
</p>

*are* now considered isomorphic. It's actually much less obvious how one 
might pin down a generating function for something like this, but the 
answer, serendipitously, comes from Pólya-Redfield counting! If this is 
new to you, you might be interested in my recent [blog post][17] where 
I talk a bit about it. Today, though, we'll be using it in a much more 
sophisticated way.

TODO: talk about plugging a generating function into a cycle-index polynomial

TODO: mention that you were anxious about doing this yourself, but 
serendipitously found literally *this* example worked out in F+S. 
So we're using a slightly different version than the one we used 
in the mse question proper... Maybe this goes in a footnote after this 
next paragraph?


For us, we realize an unordered rooted ternary tree is either empty, 
or a root with 3 recursive children (themselves possibly empty).
So by the previous discussion we learn that 

$$
T(z) = 1 + z P_{\mathfrak{S}_1}(T(z), T(z^2), T(z^3))
$$

where 
$$P_{\mathfrak{S}_3}(x_1, x_2, x_3) = \frac{1}{6}(x_1^3 + 3x_1 x_2 + 2 x_3)$$
is the cycle index polynomial for the symmetric group on three letters. 
Plugging this in we see 

$$
T(z) = 1 + \frac{z}{6} \left ( T(z)^3 + 3 T(z) T(z^2) + 2 T(z^3) \right )
$$

TODO: I'm not sure how to get an exact solution here, but a numerical 
solution is very possible. Explain $G(z,w)$ approach, use it to approximate 
$r,s$, say that these agree with the values in F&S, then use them for 
asymptotics. Make a graph like before


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
[11]: https://en.wikipedia.org/wiki/Residue_theorem
[12]: https://en.wikipedia.org/wiki/Branch_point#Branch_cuts
[13]: https://en.wikipedia.org/wiki/Puiseux_series
[14]: https://www.youtube.com/watch?v=paenRVq0vnc
[15]: https://github.com/abelfunctions/abelfunctions/
[16]: https://doc.sagemath.org/html/en/reference/power_series/sage/rings/puiseux_series_ring_element.html
[17]: /2025/01/16/undergrad-divisibility-problems.html
[18]: https://algo.inria.fr/flajolet/Publications/book.pdf
[19]: https://en.wikipedia.org/wiki/Cauchy%27s_integral_formula
[20]: https://en.wikipedia.org/wiki/Binomial_coefficient#Generalized_binomial_coefficients


[^3]:
    I'm actually lying a bit here, since $M$ is really a function of $r$ 
    and is *not* usually $O(1)$ as $r \to R$. But we're about to talk about 
    how to get a better estimate on $M$ anyways, and that more careful 
    analysis will handle this for us. 

[^4]:
    Just like $w = \sqrt{z}$, a solution to $w^2 = z$ has branches, 
    so too does $T$, a solution to $T = z + zT + zT^2 + zT^3$.

[^5]:
    Really these are circles with a little arc cut out, say by integrating from 
    $\epsilon$ to $2 \pi - \epsilon$... But we'll end up taking 
    $\epsilon \to 0$ and we're all friends here, so let's not worry about it.

[^7]:
    Though at time of writing you need the [abelfunctions][15] package 
    to do it. There *is* a [builtin implementation][16] of puiseux series, 
    but it won't actually compute a series expansion for you.

[^9]:
    Of course, it's easy to see how to extend this technique to get better 
    asypmtotics. The first approach is to just keep more terms of the 
    puiseux series of $T$. Then apply the generalized binomial formula 
    multiple times for each term you kept. 

    You can also do better by keeping track of more of the singularities. 
    Build a contour with multiple keyholes in order to get sharper lower 
    order asymptotics.
