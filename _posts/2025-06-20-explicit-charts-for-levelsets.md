---
layout: post
title: How to Explicitly Compute Charts for a Levelset Submanifold
tags:
  - 
---

While doing a computation with my friend [Shane][2] the other day, 
we realized we needed to explicitly compute a local chart near the 
identity of $SL_2(\mathbb{R})$. It took us longer than I'd like to 
admit to figure out how to do this (especially since it's so geometrically 
obvious in hindsight), and so I want to write down the process for 
future grad students looking to just do a computation! 
If you want to see what Shane and I were *actually* interested in, 
you can check out the main post [here][1].

---

Ok, let's hop right in! Say you have a $2$-manifold in $\mathbb{R}^3$ 
to start[^1]:

<p style="text-align:center;">
<img src="/assets/images/explicit-charts-for-levelsets/example1.jpg" width="75%">
</p>

If we think of the purple manifold $M$ as being an open disk, 
representing a small neighborhood of some possibly larger 2-manifold, 
then we can see the projection onto the $xy$-plane is a diffeomorphism 
onto its image (an open disk in $\mathbb{R}^2$) while the projections 
onto the $yz$ and $xz$ planes are *not* open in $\mathbb{R}^2$!
This is because the normal to $M$ is parallel to the $z$ axis inside $M$,
(indeed, at the "top of the hill") so the tangent plane at that point 
degenerates and projects to a line whenever we project onto a coordinate plane 
containing the $z$-direction.

For a more computational example, let's try the hyperboloid 
$x^2 + y^2 - z^2 = 1$, and let's see what happens near a few points.

<p style="text-align:center;">
<img src="/assets/images/explicit-charts-for-levelsets/hyperboloid.jpg" width="75%">
</p>

The tangent plane at a point is controlled by the jacobian of the 
defining equation, which for us is $\langle 2x, 2y, -2z \rangle$. 

This gives us three (disconnected) charts: $$\{2x \neq 0\}$$, $$\{2y \neq 0\}$$, and 
$$\{-2z \neq 0\}$$, which we can see visually here (and we also drop the unnecessary scalars):

<p style="text-align:center;">
<img src="/assets/images/explicit-charts-for-levelsets/hyperboloid-x-chart.jpg" width="50%">
</p>

<p style="text-align:center;">
<img src="/assets/images/explicit-charts-for-levelsets/hyperboloid-y-chart.jpg" width="50%">
</p>

<p style="text-align:center;">
<img src="/assets/images/explicit-charts-for-levelsets/hyperboloid-z-chart.jpg" width="50%">
</p>

These turn into 6 honest-to-goodness charts where we turn the disconnected 
condition $$\{x \neq 0\}$$ into the pair of connected conditions 
$$\{x \gt 0\}$$ and $$\{x \lt 0\}$$. Indeed it's easy to see that 
the 6 connected components in the above pictures are all diffeomorphic 
to an open subset of $\mathbb{R}^2$, and we can see this algebraically 
by *projecting* onto the plane avoiding the nonzero coordinate.

On $$\{x \gt 0 \}$$, for example, we have an open set of the $yz$-plane,
shown here in orange:

<p style="text-align:center;">
<img src="/assets/images/explicit-charts-for-levelsets/hyperboloid-x-pos-chart.jpg" width="50%">
</p>

Algebraically, we compute this chart by noting on $$\{x \gt 0 \}$$, we can 
solve for $x$ and (using the positive square root, since $x \gt 0$) 
write our surface locally as

$$\{ (+\sqrt{1+z^2-y^2}, y, z) \mid z^2 - y^2 \gt -1 \}$$

which is diffeomorphic in the obvious way to its projection onto the $yz$-plane

$$\{ (y,z) \mid z^2 - y^2 \gt -1 \}$$

so this is one of our charts!

Similarly, we can look at $$\{z \gt 0\}$$, solve for $z$ and locally write 
our surface as 

$$\{ (x,y,+\sqrt{x^2+y^2-1}) \mid x^2 + y^2 \gt 1 \}$$

which is diffeomorphic to $$\{ (x,y) \mid x^2 + y^2 \gt 1 \}$$ -- another chart.

<p style="text-align:center;">
<img src="/assets/images/explicit-charts-for-levelsets/hyperboloid-z-pos-chart.jpg" width="50%">
</p>

On the intersection of these charts, $$\{x, z \gt 0 \}$$, it's now easy to 
write down our transition maps (if one is so inclined):

<p style="text-align:center;">
<img src="/assets/images/explicit-charts-for-levelsets/transition-map.jpg" width="50%">
</p>

Here our charts are the diffeomorphisms

$$
\{(+\sqrt{1+z^2-y^2},y,z) \mid z^2-y^2 \gt -1, \ z \gt 0 \} 
\to 
\{(y,z) \mid z^2-y^2 \gt -1, \ z \gt 0 \}
$$

$$
\{(x,y,+\sqrt{x^2+y^2-1}) \mid x^2+y^2 \gt 1, \ x \gt 0 \}
\to
\{(x,y) \mid x^2+y^2 \gt 1, \ x \gt 0 \}
$$

so it's easy to compose them to see our transition maps between these 
charts are 

$$
(y,z) \mapsto (+\sqrt{1+z^2-y^2},y) : 
\{(y,z) \mid z^2-y^2 \gt -1, \ z \gt 0 \}
\to
\{(x,y) \mid x^2+y^2 \gt 1, \ x \gt 0 \}
$$

$$
(x,y) \mapsto (y,+\sqrt{x^2+y^2-1}) : 
\{(x,y) \mid x^2+y^2 \gt 1, \ x \gt 0 \}
\to
\{(y,z) \mid z^2-y^2 \gt -1, \ z \gt 0 \}
$$

<div class=boxed markdown=1>
As a (fun?) exercise, compute the $$\{y \gt 0 \}$$ chart, 
and the other two transition maps. 
</div>

---

For another example, let's take a look at $SL_2(\mathbb{R})$, 
which is defined to be 
$$\left \{ \begin{pmatrix} a & b \\ c & d \end{pmatrix} \mid ad-bc = 1 \right \}
\subseteq \mathbb{R}^4$$.

Then the jacobian of our defining map is $\langle d, -c, -b, a \rangle$, 
and we get charts corresponding to $$\{d \neq 0 \}$$, 
$$\{-c \neq 0 \}$$, $$\{ -b \neq 0 \}$$, and $$\{ a \neq 0 \}$$.

In the $$\{d \neq 0\}$$ chart, for instance, our defining equation looks like 
$a = \frac{1+bc}{d}$, so that $SL_2(\mathbb{R})$ looks locally like

$$
\left \{ \begin{pmatrix} \frac{1+bc}{d} & b \\ c & d \end{pmatrix} 
\ \middle | \ 
d \neq 0
\right \}
\cong_\text{diffeo}
\{ (b,c,d) \in \mathbb{R}^3 \mid d \neq 0 \}
$$

In the [main post][1] you can see how my friend Shane and I used this 
to compute the anchor map for a certain lie algebroid.

<div class=boxed markdown=1>
Again, it makes a nice exercise to explicitly write out the various 
charts and transition maps
</div>

---

What about a codimension 2 example?

Let's go back to our happy little hyperboloid, and intersect it 
with the surface $xyz = 1$. That is, we want to consider the manifold

$$
\left \{ (x,y,z) 
\ \middle | \ 
\begin{array}{c} x^2 + y^2 - z^2 = 1 \\ xyz = 1 \end{array}
\right \}
$$

This is the levelset of the map $\mathbb{R}^3 \to \mathbb{R}^2$ 
sending $(x,y,z) \mapsto (x^2 + y^2 - z^2, \ xyz)$ 
taking value $(1,1)$. So we compute the jacobian

$$
\begin{pmatrix} 2x & 2y & -2z \\ yz & xz & xy \end{pmatrix}
$$

and our charts are all the ways this matrix can have full rank.
These conditions are:

- $2x \neq 0$ and $xz \neq 0$
- $2x \neq 0$ and $xy \neq 0$
- $2y \neq 0$ and $yz \neq 0$
- $2y \neq 0$ and $xy \neq 0$
- $-2z \neq 0$ and $yz \neq 0$
- $-2z \neq 0$ and $xz \neq 0$

If we look at the $$\{2x \neq 0, \ xz \neq 0\}$$ chart, we can ask 
sage to solve for $x$ and $z$ as functions of $y$:

<div class="linked_auto">
<script type="text/x-sage">
x,y,z = var('x,y,z')
solns = solve([x^2 + y^2 + z^2 == 1, x*y*z == 1], [x,z])
for soln in solns:
    show(soln)
</script>
</div>

So as in the previous hyperboloid example, we need to break this 
into *four* charts, depending on whether $x$ and $z$ are positive or negative.

Following the sage computation, in the $$\{x \gt 0, z \gt 0\}$$ chart, 
we can write our curve as

$$
\left ( 
\sqrt{\frac{1}{2}} \sqrt{-\frac{y^{3} - y - \sqrt{y^{6} - 2 \, y^{4} + y^{2} - 4}}{y}},
\ y, \ 
\frac{2 \, \sqrt{\frac{1}{2}}}{y \sqrt{-\frac{y^{3} - y - \sqrt{y^{6} - 2 \, y^{4} + y^{2} - 4}}{y}}}
\right )
$$

which, by projecting out the $y$ coordinate, is diffeomorphic to the open 
subset of $\mathbb{R}$ where all these square roots are defined.

---

Ok, thanks for reading, all! This was extremely instructive for me, 
and hopefully it's helpful to some of you as well! Sometimes it's 
nice to just *do some computations*. Talk soon!


---

[1]: /2025/06/20/sl2-action-algebroid-computation.html
[2]: https://sites.google.com/view/shane-rankin
[11]: https://www.zotero.org/


[^1]:
    That's right. I finally bought an ipad. This has already dramatically 
    improved my paper-reading experience (I love you [Zotero][11]) and my 
    remote teaching experience, and I'm *so* glad that the example-drawing
    experience is shaping up to be everything I wanted it to be as well!
