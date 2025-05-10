---
layout: post
title: Analytic Combinatorics Redux
tags:
  - my-talks
  - sage
---

Earlier today I gave a talk in the graduate student seminar titled 
"Counting is Hard. Complex Analysis is Easy." based in part on my 
[recent blog post][1] about analytic combinatorics and based in part 
on [Varilly's notes on Dirichlet's Theorem][2], showing how to count 
the number of trees of a certain shape and the number of 
"primes of a certain shape" by doing complex analysis. While prepping 
for this talk, I realized there's a very pretty geometric way to see 
what's going on when counting rooted ordered ternary trees! I don't 
usually write blog posts about my local seminar talks anymore, but 
I think this is more than worthy of an exception! For instance, I think
this could serve as a great visiual example of branches and mild singularities
in complex analysis.

---

So, let's remember the problem! 

We want to count the number of rooted ordered ternary trees with 
$n$ nodes. Call this number $t_n$. We note that every such tree 
is either
- a root node
- a root with one child 
- a root with two children 
- a root with three children 

where each child is recursively a rooted ordered ternary tree. 
If we define $T(z) = \sum_n t_n z^n$ 
to be the [(ordinary) generating function][3] for the $t_n$ we see 
from this recurrence relation that it must satisfy the functional equation

$$
T = z + zT + zT^2 + zT^3
$$

That is, if $P(z,w) = -w + z + zw + zw^2 + zw^3$ then $P(z,T(z)) = 0$. 

If we draw (the real locus of) $P$ it looks like

<div class="auto">
<script type="text/x-sage">
P(z,w) = -w + z + z*w + z*w^2 + z*w^3
implicit_plot(P, (z,-3,3), (w,-3,3), axes=True)
</script>
</div>

and the [implicit function theorem][4] says that we can find functions 
$f(z)$ so that $P(z,f(z)) = 0$ through any starting point $P(z_0,f_0)$ on the curve
for as long as $\frac{\partial P}{\partial w} \neq 0$. In particular, 
we know that our $T(0) = t_0 = 0$ since there are no trees with zero vertices,
so that our $T(z)$ takes $z$ to the unique part of this curve 
passing through the origin, for as long as this is defined. Here we'll plot
our curve $P$ in blue, and the implicit function $T(z)$ in orange.

<div class="auto">
<script type="text/x-sage">
P(z,w) = -w + z + z*w + z*w^2 + z*w^3

singularity = solve([diff(P,w) == 0, P == 0], [z,w])[0]
singZ, singW = singularity[0].rhs(), singularity[1].rhs()

full = implicit_plot(P, (z,-3,3), (w,-3,3), color='blue')
T    = implicit_plot(P, (z,-3,3), (w,-1,singW), color='orange')
pt   = point((singZ, singW), rgbcolor='orange', pointsize=30)
name = text('  ({},{})'.format(n(singZ, digits=5), n(singW, digits=5)),
            (singZ, singW),horizontal_alignment='left',color='black')
show(full+T+pt+name, xmin=-3, xmax=3, ymin=-3, ymax=3, axes=True)
</script>
</div>

Note we have to stop at $z \approx 0.27695$ since here 
$\frac{\partial P}{\partial w} = 0$ so that the slope 
is infinite and we can't continue. Said another way, we bend backwards 
and if we tried to continue we would fail the vertical line test. 
But since we have to stop here, we see that $0.27695$ is the 
radius of convergence for $T$, and is the dominant singularity!

Next, can we find a good approximation for $T$ near this singularity? In the 
main post we used [puiseux series][5] for this, but it's instructive to 
do it by hand!

Note that $\frac{\partial P}{\partial z} \neq 0$ at 
$(0.27695, 0.65730)$ so there's nothing stopping us from 
approximating $z$ as a function of $w$ at this point (then inverting it).

Indeed, we can solve for $z = \frac{w}{1+w+w^2+w^3}$ and then just 
taylor expand this at our point of interest:

<div class="auto">
<script type="text/x-sage">
P(z,w) = -w + z + z*w + z*w^2 + z*w^3

singularity = solve([diff(P,w) == 0, P == 0], [z,w])[0]
singZ, singW = singularity[0].rhs(), singularity[1].rhs()

show((w/(1+w+w^2+w^3)).series(w==singW,5))

</script>
</div>

Of course, we chose this point because 
$\frac{\mathrm{d}z}{\mathrm{d}w} = 
\frac{- \frac{\partial P}{\partial w}}{\frac{\partial P}{\partial z}}$
is $0$ here. So we know this $2.97 \times 10^{-8}$ is a rounding error and 
our leading order expansion is 

$$
z - 0.27695 \approx -0.34680 (w - 0.6573)^2
$$

Here's a graph zoomed into near the singularity. The actual graph of $P$ is 
shown in blue, and our approximating parabola is shown in orange:

<div class="auto">
<script type="text/x-sage">
P(z,w) = -w + z + z*w + z*w^2 + z*w^3

singularity = solve([diff(P,w) == 0, P == 0], [z,w])[0]
singZ, singW = singularity[0].rhs(), singularity[1].rhs()
eps = 0.25

D2 = (w/(1+w+w^2+w^3)).diff(w,2).subs(w=singW)/factorial(2)

S(z,w) = z - singZ - D2 * (w - singW)^2

full = implicit_plot(P, (z,singZ-eps,singZ+eps), (w,singW-eps,singW+eps), 
                        color='blue')
S    = implicit_plot(S, (z,singZ-eps,singZ+eps), (w,singW-eps,singW+eps), 
                        color='orange')
pt   = point((singZ, singW), rgbcolor='orange', pointsize=30)
name = text('  ({},{})'.format(n(singZ, digits=5), n(singW, digits=5)),
            (singZ, singW),horizontal_alignment='left',color='black')
show(full+S+pt+name, xmin=singZ-1.1*eps, xmax=singZ+1.1*eps, 
        ymin=singW-1.1*eps, ymax=singW+1.1*eps, axes=True)
</script>
</div>

But of course if $z - 0.27695 \approx -.34680 (w - 0.6573)^2$ then we 
can solve for 

$$w - 0.6573 \approx \pm 0.8936 \sqrt{1- \frac{z}{0.27695}}$$

and if we want this to agree with our $w = T(z)$ branch through the 
origin we obviously have to choose the *negative* square root 
(since we want the *lower* half of this sideways parabola[^2]). Here we 
draw our $T(z)$ in blue, and we draw the approximation 
$0.6573 - 0.8936 \sqrt{1 - \frac{z}{0.27695}}$ in orange so you 
can see how well they line up!

<div class="auto">
<script type="text/x-sage">
P(z,w) = -w + z + z*w + z*w^2 + z*w^3

singularity = solve([diff(P,w) == 0, P == 0], [z,w])[0]
singZ, singW = singularity[0].rhs(), singularity[1].rhs()
eps = 0.01

D2 = (w/(1+w+w^2+w^3)).diff(w,2).subs(w=singW)/factorial(2)

S = singW - sqrt(singZ/-D2) * (1 - z/singZ)^(1/2)


T    = implicit_plot(P, (z,-0.1,0.3), (w,-0.1,singW+eps), color='blue')
S    = plot(S, (z,singZ-eps,singZ), color='orange')
pt   = point((singZ, singW), rgbcolor='black', pointsize=30)
show(T+S+pt, xmin=-0.1, xmax=0.3, ymin=-0.1, ymax=singW+eps, axes=True)
</script>
</div>

But now from here we can run exactly the same argument as in the 
previous post! We compute 
$t_n = \frac{1}{2\pi i} \oint \frac{T}{z^{n+1}} \ \mathrm{d}z$, 
along a keyhole contour around the singular point $z=0.27695$ 
with a branch cut along the real axis. The brunt of this integral 
comes from the cutout near the singular point, where $T$ is well 
approximated by $0.6573 - 0.8936 \sqrt{1 - \frac{z}{0.27695}}$ 
so that 

$$
\begin{align}
t_n 
&\approx 
\frac{-0.8936}{2\pi i} \oint \frac{(1 - \frac{z}{0.27695})}{z^{n+1}} \ \mathrm{d}z \\
&=
\frac{-0.8936}{2\pi i} \oint \frac{\sum_k \binom{1/2}{k} 
\left ( \frac{-z}{0.27695} \right )^k}{z^{n+1}} \ \mathrm{d}z \\
&=
(-0.8936) \binom{1/2}{n} (-0.27695)^{-n} \\
&\approx
\frac{0.8936}{2 \sqrt{\pi}} \frac{(3.6107)^n}{n^{3/2}}
\end{align}
$$

Again, for more details about exactly what this keyhole contour is and 
how you estimate this integral along it, see the [main post][1].

---

Let's go ahead and call it here! My actual talk was slightly longer 
than this, since I also sketched a proof of [Dirichlet's Theorem][6] 
following Varilly's [notes on the subject][2], but there's no sense 
in me writing that up since those notes are already so good! Plus it's 
getting late and I want to go to bed, haha.

As always, here's a copy of my title and abstract. Unfortunately I don't 
have any slides or recordings today, but I'm giving another talk at 
[WiSCons in Madison][7] next week and I should have slides for that. 
I'm also hoping to finish a sister blog post for that talk where I do 
more example computations in more detail than I could possibly do in a 
20 minute talk. Lots of writing to do this week!

Take care all, stay safe, and I can't wait to talk soon ^_^


---

Counting is Hard. Complex Analysis is Easy.

Don't you miss being a kid, when your mom would ask you to count how many of 
your alphabet fridge magnets were both red and vowels? When you saw the 
answer was "2", you felt such accomplishment.... But counting has only gotten 
harder since then, and now if you want to count how many objects satisfy some 
properties (say, being both red and vowels) it can be borderline impossible! 
In this talk we'll show how you can solve counting problems by doing complex 
analysis instead. First we'll count the number of trees of a certain shape, 
then (given time) we'll count how many prime numbers are of a (different) 
certain shape.

---

[1]: /2025/04/08/analytic-combinatorics-example
[2]: https://math.rice.edu/~av15/Files/Dirichlet.pdf
[3]: https://en.wikipedia.org/wiki/Generating_function
[4]: https://en.wikipedia.org/wiki/Implicit_function_theorem
[5]: https://en.wikipedia.org/wiki/Puiseux_series
[6]: https://en.wikipedia.org/wiki/Dirichlet%27s_theorem_on_arithmetic_progressions
[7]: https://awm-math.org/abstract/explicitly-computing-with-fukaya-categories-of-surfaces/

[^1]:
    Use implicit differentiation and compute! 
    We know $P(z,w) = 0$ so 

    $$
    \frac{\partial P}{\partial z} \frac{\mathrm{d}z}{\mathrm{d}w} 
    +
    \frac{\partial P}{\partial w} = 0
    $$

    and rearranging gives the claim.

[^2]:
    In the main post we used puiseux series for this, and we had 
    to essentially guess which branch was correct. Now we see how the 
    geometry of the situation tells us that we have to choose the 
    negative branch of the square root! After all, this is the one 
    that locally agrees with the rest of the graph of $T$!
