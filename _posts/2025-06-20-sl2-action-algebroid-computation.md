---
layout: post
title: Explicitly Computing The Action Lie Algebroid for $SL_2(\mathbb{R}) \curvearrowright \mathbb{R}^2$
tags:
  - 
---

This is going to be a very classic post, where we'll chat about a computation 
my friend [Shane][1] did earlier today. His research is largely about 
[symplectic][2] [lie algebroids][3], and recently we've been trying to 
understand the rich connections between poisson geometry, lie algebroids, 
lie groupoids, and eventually maybe fukaya categories of lie groupoids
(following some [ideas of Pascaleff][4]). Shane knows *much* more about this
stuff than I do, so earlier today he helped me compute a super concrete example.
We got stuck at some interesting places along the way, and I think it'll be 
fun to write this up, since I haven't seen these kinds of examples written 
down in many places.

Let's get started!

---

First, let's recall what an [action groupoid][5] is. This is one of the 
main examples I have in my head for lie groupoids, which is why Shane 
and I started here.

<div class=boxed markdown=1>
If $G$ is a group acting on a set $X$, then we get a groupoid:

$$G \times X \rightrightarrows X$$

here we think of $X$ as the set of objects and $G \times X$ as the 
set of arrows, where

- the *source* of $(g,x)$ is just $x$
- the *target* of $(g,x)$ is $g \cdot x$, using the action of $G$ on $X$
- the *identity arrow* at $x$ is $(1,x)$
- if $(g,x) : x \to y$ and $(h,y) : y \to z$, then the *composite* is 
    $(hg,x) : x \to z$
- if $(g,x) : x \to y$ then its *inverse* is $(g^{-1},y) : y \to x$.
</div>

Action groupoids are interesting and important because they allow us to 
work with "stacky" nonhausdorff quotient spaces like [orbifolds][6] in 
a very fluent way. See, for instance, Moerdijk's 
[_Orbifolds as Groupoids: An Introduction_][7], which shows how you can 
easily define covering spaces, vector bundles, principal bundles, etc. 
on orbifolds using the framework of groupoids.

The point is that a groupoid $E \rightrightarrows X$ is a 
"proof relevant equivalence relation" in the sense that $E$ keeps track of
all the "proofs" or "witnesses" that two points in $X$ are identified, 
rather than just the *statement* that two points are identified. Indeed, 
we think of $e \in E$ as a witness identifying $s(e)$ and $t(e)$ in $X$. 
Then reflexivity comes from the identity arrow, symmetry comes from the 
inverse, and transitivty comes from composition. The "proof relevance" is 
just the statement that there might be multiple elements $e_1$ and $e_2$ 
which both identify $x$ and $y$ 
(that is, $s(e_1) = s(e_2) = x$ and $t(e_1) = t(e_2) = y$). By keeping track 
of this extra information that "$x$ and $y$ are related in multiple ways" we're 
able to work with a *smooth* object (in the sense that both $E$ and $X$ 
are smooth) instead of the nonsmooth, or even nonhausdorff quotient $X/E$.

Next, we know that a central part of the study of any lie group $G$ is 
its lie algebra $\mathfrak{g}$. This is a "linearization" of $G$ in the 
literal sense that it's a vector space instead of a manifold, which makes it 
much easier to study. But through the lie bracket $[-,-]$ it remembers enough 
of the structure of $G$ to make it an indispensable tool for understanding $G$.
See, for instance, Bump's excellent book [_Lie Groups_][8] or Stillwell's 
excellent [_Naive Lie Theory_][9]. With this in mind, just playing linguistic 
games we might ask if there's a similarly central notion of "lie algebroid" 
attached to any "lie groupoid". The answer turns out to be *yes*, but unlike 
the classical case, not every lie algebroid comes from a lie groupoid! We say 
that not every lie algebroid is *integrable*.

This, finally, brings us to the computation that Shane and I did together:

<div class=boxed markdown=1>
As explicitly as possible, let's compute the lie algebroid coming from 
the action groupoid of $SL_2(\mathbb{R}) \curvearrowright \mathbb{R}^2$.
</div>

Let's start with a few definitions coming from 
Crainic, Fernandes, and Mărcuț's [Lectures on Poisson Geometry][10].

<div class=boxed markdown=1>
A <span class=defn>Lie Algebroid</span> on a manifold $M$ is a 
vector bundle $A \to M$ whose space of global sections $\Gamma(A)$ 
has a lie bracket $[-,-]_A$, equipped with an *anchor map* $\rho : A \to TM$
to the tangent bundle of $M$ that's compatible with the lie bracket in the 
sense that for $\alpha, \beta \in \Gamma(A)$ and $f \in C^\infty(M)$ we have

$$
[\alpha, f \cdot \beta]_A = f \cdot [\alpha,\beta]_A + (\rho(\alpha) f) \cdot \beta
$$
</div>

Then, given a lie groupoid $E \rightrightarrows M$ with source and target 
maps $s,t : E \to M$ and identity map $r : M \to E$, its lie algebroid is 
explicitly given by letting 

- $A = r^* \text{Ker}(dt)$, which is a vector bundle over $M$
- $[-,-]_A$ coming from the usual bracket on $TE$ (since $\text{Ker}(dt)$ is 
    a subbundle of $TE$)
- $\rho : A \to TM$ given by $ds$ (which is a map $TE \to TM$, thus restricts to 
    a map on $\text{Ker}(dt)$, and so gives a map on the pullback $A = r^* \text{Ker}(dt)$)

If this doesn't make perfect sense, that's totally fine! It didn't make sense 
to me either, which is why I wanted to work through an example slowly with 
Shane. For us the action groupoid is 

$$SL_2(\mathbb{R}) \times \mathbb{R}^2 \rightrightarrows \mathbb{R}^2$$

where

$$s (M,v) = Mv$$

$$t (M,v) = v$$

$$r (v) = (\text{Id}, v)$$

$$(M_2, M_1 v) \circ (M_1, v) = (M_2 M_1, v)$$

<p style="text-align:center;">
<img src="/assets/images/sl2-action-algebroid-computation/stage-is-set.gif" width="60%">
</p>

---

First let's make sense of $A = r^* \text{Ker}(dt)$.

We know that $dt : T(SL_2(\mathbb{R}) \times \mathbb{R}^2) \to T\mathbb{R}^2$,
that is, $dt : TSL_2(\mathbb{R}) \times T\mathbb{R}^2 \to \mathbb{R}2$, and 
is the derivative of the map $t : (M,v) \mapsto v$. If we perturb a particular 
point $(M_0, v_0)$ to first order, say $(M_0 + \delta M, v_0 + \delta v)$, then 
projecting gives $v_0 + \delta v$, which gives $\delta v$ to first order. 
So the kernel of this map are all the pairs $(\delta M, \delta v)$ with 
$\delta v = 0$, and we learn 

$$\text{Ker}(dt) = TSL_2(\mathbb{R}) \times \mathbb{R}^2$$

where we're identifying the zero section of $T\mathbb{R}^2$ with 
$\mathbb{R}^2$ itself.

Now to get $A$ we're supposed to apply $r^*$ to this. 

By definition, this means the fibre of $r^* \text{Ker}(dt)$ above the point 
$v$ is supposed to be the fibre of $\text{Ker}(dt)$ over $r(v) = (\text{id},v)$.
But this fibre is $$T_{\text{id}}SL_2(\mathbb{R}) \times \{v\}$$, so that the 
pullback is a trivial bundle with fibre $\mathfrak{sl}_2(\mathbb{R})$:

$$A = \mathfrak{sl}_2(\mathbb{R}) \times \mathbb{R}^2$$

viewed as a trivial fibre bundle over $\mathbb{R}^2$. 
(Recall that the lie algebra $\mathfrak{sl}_2(\mathbb{R})$ is 
*defined to be* the tangent space of $SL_2(\mathbb{R})$ at the identity).

<br>

Next we want to compute the bracket $$[-,-]_A$$. Thankfully this is easy, 
since it's the restriction of the bracket on $TSL_2(\mathbb{R}) \times T\mathbb{R}^2$.
Of course, an element of $A$ comes from $T_\text{id}SL_2(\mathbb{R}) = \mathfrak{sl}_2(\mathbb{R})$
and the zero section of $T\mathbb{R}^2$, so we get the usual lie bracket on 
$\mathfrak{sl}_2(\mathbb{R})$ in the first component and the restriction of 
the bracket on $T\mathbb{R}^2$ to $$\{0\}$$ in the second slot. This zero 
section piece isn't doing anything interesting, and so after identifying 
this bundle with the trivial bundle $\mathfrak{sl}_2(\mathbb{R}) \times \mathbb{R}^2$ 
we see the bracket is just the usual bracket on $\mathfrak{sl}_2(\mathbb{R})$ 
taken fibrewise.

<br>

Lastly, we want to compute the anchor map. This caused me and Shane a 
bit of trouble, since we need to compute $ds$ at the identity,
and we realized neither of us knew a general approach for computing 
a chart for $SL_2(\mathbb{R})$ near $\text{id}$!

In hindsight for a $k$ dimensional submanifold of $\mathbb{R}^n$ the idea is 
obvious: Just project onto some well-chosen $k$-subset of the usual 
coordinate directions! I *especially* wish it were easier to find some examples
of this by googling, so I'm breaking it off into a [sister blog post][12]
which will hopefully show up earlier in search results than this one will.

The punchline for us was that $SL_2(\mathbb{R})$ is defined to be 

$$
\left \{ 
\begin{pmatrix} a & b \\ c & d \end{pmatrix} \in \mathbb{R}^4
\ \middle | \ 
ad-bc = 1
\right \}
$$

So a chart near a point $(a_0, b_0, c_0, d_0)$
can be computed by looking at the jacobian of 
$f : \mathbb{R}^4 \to \mathbb{R}$ with $f(a,b,c,d) = ad-bc$ 
evaluated at the matrix of interest $(a_0, b_0, c_0, d_0)$.
Since $1$ is a [regular value][11] for $f$, the jacobian will 
have at least one nonzero entry, and by locally inverting that 
coordinate we'll get our desired chart!

Since we want a chart near the identity, we compute the jacobian
of $ad-bc$ at the identity to be

$$
\begin{aligned}
\left . J f \right |_{\begin{pmatrix} 1 & 0 \\ 0 & 1 \end{pmatrix}}
&= 
\left . 
\langle d, -c, -b, a \rangle 
\right |_{\begin{pmatrix} 1 & 0 \\ 0 & 1 \end{pmatrix}} \\
&= \langle 1, 0, 0, 1 \rangle
\end{aligned}
$$

We see that $\frac{\partial f}{\partial a} \neq 0$, so that 
locally near $$\begin{pmatrix} 1 & 0 \\ 0 & 1 \end{pmatrix}$$
the manifold looks like

$$
\left \{ 
\begin{pmatrix}
a & b \\
c & \frac{1 + bc}{a}
\end{pmatrix}
\right \}
\cong_\text{diffeo}
\{ (a,b,c) \mid a \neq 0 \} \subseteq \mathbb{R}^3
$$

and this is our desired local chart!

<br>

Now... Why were we doing this? We wanted to compute the anchor map 
from $A = r^* \text{Ker}(dt)$ to the tangent bundle $T\mathbb{R}^2$.
This is supposed to be $ds$ (restricted to this subbundle).

So how can we compute this? In the main body, I'll make some identifications 
that make the presentation cleaner, and still show what's going on. 
If you want a *very very explicit* version of this computation, 
take a look at this footnote[^2].

Well 
$s : SL_2(\mathbb{R}) \times \mathbb{R}^2 \to \mathbb{R}^2$ 
is the map sending $(M,v) \mapsto Mv$. 

Explicitly, if we fix an $(x,y)$, this is the map

$$
\begin{pmatrix} a & b \\ c & d \end{pmatrix}
\mapsto
(ax+by, cx+dy)
$$

From the previous discussion, we can write this as a map in local charts
$$\{(a,b,c) \in \mathbb{R}^3 \mid a \neq 0 \} \to \mathbb{R}^2$$
given by

$$
s : (a,b,c) \mapsto \left ( ax+by, cx+ \frac{1+bc}{a}y \right )
$$

and now it's very easy to compute $ds$. It's just the jacobian

$$
\begin{pmatrix}
x & y & 0 \\ 
\frac{-(1+bc)}{a^2}y & \frac{c}{a} y & x + \frac{b}{a} y 
\end{pmatrix}
$$

but we only care about the value at the identity, since $A$ comes from pulling 
back this bundle along $r : v \mapsto (\text{id},v)$. So evaluating at 
$(a,b,c) = (1,0,0)$ we find our anchor map is 

$$
\begin{pmatrix}
x & y & 0 \\ -y & 0 & x
\end{pmatrix}
$$

Moreover, by differentiating 
$$\begin{pmatrix} a & b \\ c & \frac{1+bc}{a} \end{pmatrix}$$
in the $a$, $b$, and $c$ directions and evaluating at $(1,0,0)$ we 
see that the basis $(\partial_a, \partial_b, \partial_c)$ for the tangent 
space to $(1,0,0)$ in our chart gets carried to the following basis 
for the tangent space at the identity matrix in $SL_2(\mathbb{R})$:

$$
\partial_a \mapsto \begin{pmatrix} 1 & 0 \\ 0 & -1 \end{pmatrix}
\quad \quad
\partial_b \mapsto \begin{pmatrix} 0 & 1 \\ 0 & 0 \end{pmatrix}
\quad \quad
\partial_c \mapsto \begin{pmatrix} 0 & 0 \\ 1 & 0 \end{pmatrix}
$$

which we [recognize][13] as $H$, $E$, and $F$ respectively.

<br>

But this is great! Now we know that the lie algebroid of the 
action groupoid of $SL_2(\mathbb{R}) \curvearrowright \mathbb{R}^2$ 
is given by the trivial bundle 
$\mathfrak{sl}_2(\mathbb{R}) \times \mathbb{R}^2 \to \mathbb{R}^2$
with the usual bracket on $\mathfrak{sl}_2$ taken fibrewise, and 
the anchor map $\rho : \mathfrak{sl}_2 \times \mathbb{R}^2 \to T\mathbb{R}^2$
sending (in the fibre over $(x,y)$)

- $\rho_{(x,y)}(H) = (x, -y)$
- $\rho_{(x,y)}(E) = (y, 0)$
- $\rho_{(x,y)}(F) = (0, x)$

(which is the *standard representation* of $\mathfrak{sl}_2(\mathbb{R})$ on 
$\mathbb{R}^2$, viewed in a kind of bundle-y way.)

---

Thanks for hanging out, all! It was fun to go back to my roots and write 
a post that's "just" a computation. This felt tricky while Shane and I were 
doing it together, but writing it up now it's starting to feel a lot 
simpler. There's still some details I don't totally understand, which I think 
will be cleared up by just doing more computations like this, haha.

Also, sorry for not spending a lot of time motivating lie algebroids or 
actually *doing* something with the result of this computation... I actually 
don't totally know what we can do with lie algebroids either! This was just 
a fun computation I did with a friend, trusting that he has good reasons 
to care. I've been meaning to pester him into guest-writing a blog 
post (or very confidently holding my hand while I write the blog post)
about lie algebroids and why you should care. As I understand it, 
they give you tools for studying PDEs on manifolds which have certain mild 
singularities. This is super interesting, and obviously useful, and so I'd 
love to spend the time to better understand what's going on.

Stay safe, and if you're anywhere like Riverside try to stay cool!


---

[1]: https://sites.google.com/view/shane-rankin
[2]: https://en.wikipedia.org/wiki/Symplectic_manifold
[3]: https://en.wikipedia.org/wiki/Lie_algebroid
[4]: https://arxiv.org/abs/1803.07676
[5]: https://ncatlab.org/nlab/show/action+groupoid
[6]: https://en.wikipedia.org/wiki/Orbifold
[7]: http://arxiv.org/abs/math/0203100
[8]: https://www-fourier.ujf-grenoble.fr/~panchish/ETE%20LAMA%202018-AP/lecturesZETAS2018/BumpD-Lie%20groups.pdf
[9]: https://link.springer.com/book/10.1007/978-0-387-78214-0
[10]: https://publish.illinois.edu/ruiloja/files/2023/09/gsm217.pdf
[11]: https://en.wikipedia.org/wiki/Submersion_(mathematics)
[12]: /2025/06/20/explicit-charts-for-levelsets.html
[13]: https://en.wikipedia.org/wiki/Special_linear_Lie_algebra#Representation_theory

[^2]:
    If you want to be super duper explicit, our function $s$ sends 
    $SL_2(\mathbb{R}) \times \mathbb{R}^2 \to \mathbb{R}^2$, which 
    in a chart around the identity looks like the function 
    
    $$\{(a,b,c) \in \mathbb{R}^3 \mid a \neq 0 \} \times \mathbb{R}^2 \to \mathbb{R}^2$$

    given by

    $$(a,b,c,x,y) \mapsto \left ( ax+by, cx+ \frac{1+bc}{a}y \right )$$

    now we differentiate to get 
    $ds : TSL_2(\mathbb{R}) \times T\mathbb{R}^2 \to T\mathbb{R}^2$
    sending $(a,b,c,\delta a,\delta b,\delta c, x, y, \delta x, \delta y)$
    to $(ax+by, cx+\frac{1+bc}{a}y, ?, ?)$

    Where the two $?$s are the output of matrix multiplication against 
    the jacobian of $s$:

    $$
    \begin{pmatrix}
    x & y & 0 & a & b \\ 
    \frac{-(1+bc)}{a^2}y & \frac{c}{a} y & x + \frac{b}{a} y & c & \frac{1+bc}{a}
    \end{pmatrix}
    \begin{pmatrix} 
    \delta a \\ \delta b \\ \delta c \\ \delta x \\ \delta y
    \end{pmatrix}
    $$

    Then we're supposed to restrict this to $\text{Ker}(dt)$, which are the 
    points $(a,b,c, \delta a, \delta b, \delta c, x, y, 0, 0)$. 
    Since $\delta x = \delta y = 0$, we don't even bother writing those 
    entries of the matrix, and that's how we get $ds$ as written in the 
    main body.

    Now, as in the main body, we pull this bundle back along 
    $r : v \mapsto (\text{id},v)$,
    which in our chart is $(x,y) \mapsto (1,0,0,x,y)$ so that our bundle $A$ 
    (with its structure map to $\mathbb{R}^2$) is 

    $$A = \{(1,0,0, \delta a, \delta b, \delta c, x, y, 0, 0)\} \to \{(x,y)\} = \mathbb{R}^2$$

    which, in the main text, we identify with 
    $$
    \mathfrak{sl}_2 \times \mathbb{R}^2 = \{(\delta a, \delta b, \delta c, x, y)\} 
    \to \{(x,y)\} = \mathbb{R}^2
    $$

    so we learn that our anchor map $ds$ is the restriction of the above map 
    $ds$ to this pulled back subbundle, and sends

    $$(\delta a, \delta b, \delta c, x, y) \mapsto (x,y,?,?)$$

    where, again the $?$s are the result of the matrix multiplication

    $$
    \begin{pmatrix}
    x & y & 0 \\ -y & 0 & x
    \end{pmatrix}
    \begin{pmatrix}
    \delta a \\ \delta b \\ \delta c
    \end{pmatrix}
    $$

    which brings us back to the result of the main body.

    Of course, most working differential geometers wouldn't write out this 
    much detail to do this computation! I think it might be helpful to some 
    newcomers to the field, and I certainly found it clarifying to write 
    down exactly what happened, even if Shane and I weren't nearly this careful 
    when we were doing this together at a whiteboard.
