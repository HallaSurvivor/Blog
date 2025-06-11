---
layout: post
title: A Proof that there's No Constructive Proof of the Intermediate Value Theorem
tags:
  - topos-theory
  - sage
---

The other day my friend [Lucas Salim][15] was asking me some questions about 
categorical logic and constructive math, and he mentioned he'd never seen a 
proof that there's no constructive proof of the intermediate value theorem before. 
I showed him the usual counterexample, and since my recent [blog post][1] 
about choice was so quick to write I decided to quickly write up a post 
about this too, since I remember being confused by it back when I was first 
learning it.

The key fact is <span class=defn>Soundness and Completeness</span> of 
the topos semantics of constructive logic. This says that 
there is a way of interpreting the usual syntax of mathematics into a topos 
in such a way that 

1. (Soundness) If you can constructively prove a statement, then its 
    interpretation in every topos is true

2. (Completeness) If a statement is interpreted as true in every 
    (elementary[^1]) topos, then there must exist a constructive proof

For a proof, see Chapter II of Lambek 
and Scott's [_Introduction to Higher Order Categorical Logic_][2] or 
Section D4.3 of [The Elephant][3].

This means that as long as we're careful to avoid choice and excluded 
middle, anything we prove will be true *when interpreted in any topos we like*!
Then there's a mechanical procedure that lets us convert this interpretation 
into a corresponding statement in the "real world[^2]", and this gives us 
lots of "theorems for free" for each individual constructive theorem! 
A nice case study is given by the [Weierstrass Approximation Theorem][9],
which I [gave a talk on][10] years ago[^3]. Since this theorem is 
constructively provable[^4]...

- by interpreting it in the [effective topos][12] we learn there's a 
    computer program $\mathtt{Approx}$ which takes as input 
    a function $f : [0,1] \to \mathbb{R}$[^5] and an $\epsilon \gt 0$ 
    and outputs the coefficients of a polynomial approximating $f$.
- by interpreting it in a sheaf topos $\text{Sh}(\Theta)$ we learn 
    that for any continuous *family* of functions 
    $f_\theta(x) : \Theta \times [0,1] \to \mathbb{R}$, there's locally[^6] 
    a polynomial $p_\theta(x)$ whose coefficients are continuous functions of 
    $\theta$ which approximates each $f_\theta(x)$
- etc. 

If you're interested in learning how to *externalize* a statement in a 
topos to a statement about the real world, I highly recommend 
Ingo Blechschmidt's excellent paper 
[_Exploring mathematical objects from custom-tailored mathematical universes_][13]
which gives a high level overview of the topic, while still giving enough 
details to let you externalize a few statements of your own!

<br>

But where were we? The usual proofs of the intermediate value theorem
aren't constructive. See, for instance, Bauer's 
[_Five Stages of Accepting Constructive Mathematics_][14] 
or Section 1 of Taylor's [_A Lambda Calculus for Real Analysis_][16] 
for a discussion of how some common proofs fail (as well as great lists of 
constructively provable alternatives). Since the usual proofs seem to fail, 
we might guess that IVT is not provable constructively... but how could we prove this?

Say, towards a contradiction, that there *were* a 
constructive proof of the intermediate value theorem. Then it would 
be true in every topos, and thus its various externalizations would 
all be true in the real world. So to show that there *isn't* a 
constructive proof, all we have to do is find a topos which doesn't 
think it's true!

Following *many* who came before me[^7], we're going to use the topos of 
sheaves on $(-1,1)$. It's been a minute since we've 
externalized a statement together, so let's do it now! 


In full symbolic glory, the IVT says 

$$ 
\forall f : \mathbb{R} \to \mathbb{R} . 
\forall a,b \in \mathbb{R} . 
(a \lt b \land f(a) \lt 0 \land f(b) \gt 0) 
\to
(\exists x \in \mathbb{R} . a \lt x \lt b \land f(x) = 0)
$$

So now using the *forcing language* for $\text{Sh}((-1,1))$
(check out Theorem $1$ in Chapter VI.7 of Mac Lane and Moerdijk's 
_Sheaves in Geometry and Logic_ if you're not sure what this means),
we compute:

$$
1 \Vdash 
\forall f : \mathbb{R} \to \mathbb{R} . 
\forall a,b \in \mathbb{R} . 
(a \lt b \land f(a) \lt 0 \land f(b) \gt 0) 
\to
(\exists x \in \mathbb{R} . a \lt x \lt b \land f(x) = 0)
$$

We cash out the universal quantifiers to get
"for every open $U \subseteq (-1,1)$, and for every continuous
$f : U \times \mathbb{R} \to \mathbb{R}$, $a : U \to \mathbb{R}$, $b : U \to \mathbb{R}$,
we have..."

$$
U \Vdash 
(a \lt b \land f(a) \lt 0 \land f(b) \gt 0) 
\to
(\exists x \in \mathbb{R} . a \lt x \lt b \land f(x) = 0)
$$

Next, cashing out the implication gives
"for every open $U \subseteq (-1,1)$, and for every continuous
$f : U \times \mathbb{R} \to \mathbb{R}$, $a : U \to \mathbb{R}$, $b : U \to \mathbb{R}$,
so that for all $t \in U$ we know $a(t) \lt b(t)$, $f(t,a(t)) \lt 0$, and $f(t,b(t)) \gt 0$,
we have..."

$$
U \Vdash \exists x \in \mathbb{R} . a \lt x \lt b \land f(x) = 0
$$

Finally, cashing out the existential quantifer and the stuff inside it 
we get the external statement:

<div class=boxed markdown=1>
The IVT is true inside $\text{Sh}((-1,1))$ if and only if the following 
is true externally:

For every open $U \subseteq (-1,1)$ <br>
for every continuous
$f : U \times \mathbb{R} \to \mathbb{R}$, $a : U \to \mathbb{R}$, $b : U \to \mathbb{R}$ <br>
so that for all $t \in U$ we know 
$a(t) \lt b(t)$, $f(t,a(t)) \lt 0$, and $f(t,b(t)) \gt 0$ <br>
there is an open cover $$\{U_\alpha\}$$ covering $U$ with
continuous functions $x_\alpha : U_\alpha \to \mathbb{R}$ so that <br>
for all $t \in U_\alpha$, $a(t) \lt x_\alpha(t) \lt b(t)$ and $f(t,x_\alpha(t)) = 0$.
</div>

What a mouthful!

Of course, we're trying to prove this *fails*, so all we have to do is 
find an open set $U$ and functions $f$, $a$, and $b$ satisfying the 
assumptions so that the conclusion fails. We'll choose $U = (-1,1)$ to be the 
whole set, $a(t) = -2$ and $b(t) = 2$ to be constant functions, and 
$f(t,x) : (-1,1) \times \mathbb{R} \to \mathbb{R}$ to be 

$$
f(t,x) = \max(\min(t+x+1, t), t+x-1)
$$

Then we see that, indeed, $f(t,a) \lt 0$ and $f(t,b) \gt 0$ for all 
$t \in (-1,1)$, so to prove the IVT fails in this topos we just need 
to show there's no open cover on which $x(t)$ with $f(t,x(t)) = 0$ 
can be chosen continuously.

The idea is that no matter how hard we try, $x(t)$ cannot be continuous 
in a neighborhood of $t=0$. Indeed, here's an animation showing how 
$x(t)$ changes as we change $t$:

<div class="auto">
<script type="text/x-sage">
x,t = var('x,t')

f(t,x) = max_symbolic(min_symbolic(t+x+1, t), t+x-1)

def mkFrame(t):
    graph = plot(lambda x: f(t,x), (x,-2,2), ymin=-2, ymax=2)
    zero = point((1-t if t<0 else -1-t, 0), size=40, color="orange")
    txt = text("t={}".format(t), (-1.5,1.5))
    return graph+zero+txt

frames = [mkFrame(t/10) for t in ([-5..5] + [-s for s in [-4..4]])]
a = animate(frames)
a.show()
</script>
</div>

You can see that when $t=0$ the root $x(t)$ jumps between $\pm 1$!

Indeed, if we plot $x(t)$ we get:

<div class="auto">
<script type="text/x-sage">
x,t = var('x,t')

f(t,x) = max_symbolic(min_symbolic(t+x+1, t), t+x-1)

p = implicit_plot(f(t,x), (t,-1,1), (x,-2,2))
p.axes_labels(['$t$', '$x$'])
p.show()
</script>
</div>

and it's obvious that this is not the graph of a continuous function in any 
neighborhood of $t=0$.

As long as we're showing pretty graphics, you can also visualize this whole 
function $f$ as a surface over the strip $(-1,1) \times \mathbb{R}$. 
Then choosing a $t$ amounts to choosing a "slice" of the surface, and 
we can see that where that slice intersects the $(t,x)$-plane jumps suddenly 
as we cross $t=0$. In this example the axes are labeled $x$ and $y$ rather than 
$x$ and $t$:

<iframe src="https://www.desmos.com/3d/ijgujx61ww" style="border: 0; width:100%; height: 500px; overflow: auto;"></iframe>

<br>

So where did we start, and where did we end? If the IVT were constructively 
provable, it would be true inside $\mathsf{Sh}((-1,1))$ and thus 
for our $f(t,x)$ we could find an open cover on which
the zero $x(t)$ varies continuously in $t$. But this can't possibly happen 
in a neighborhood of $t=0$, so we learn there *is no constructive proof*!

Buuuuut, all is not lost! Usually classical theorems *do* have constructive 
analogues, either by adding new assumptions, weakening the conclusion, or by 
finding a different statement of the theorem that's more positive. 
Andrej Bauer's paper [_Five Stages of Accepting Constructive Mathematics_][14] 
lists many possibilities.

For instance, one way to weaken the conclusion is to prove that for 
any $\epsilon$ you like, there's an $x$ with $|f(x)| \lt \epsilon$. 
In our example, if we plot those $x$ so that $|f(t,x)| \lt \epsilon$ we get

<div class="linked_auto">
<script type="text/x-sage">
x,t = var('x,t')

f(t,x) = max_symbolic(min_symbolic(t+x+1, t), t+x-1)

p = region_plot(abs(f(t,x)) <= 0.1, (t,-1,1), (x,-2,2))
p.axes_labels(['$t$', '$x$'])
p.show()
</script>
</div>

and it's easy to fit the graph of a continuous selection function $x(t)$ 
inside this thickened region.

Another approach is to recognize that the problem comes from $f$ "hovering"
at $0$ when $t=0$. If we forbid this hovering, for instance by assuming 
$f$ is strictly monotone, then we _can_ constructively prove the IVT
(See Bauer's _Five Stages_ paper again).

There's yet another version, coming from [Abstract Stone Duality][17], 
where we say that whenever $f(a) \lt 0 \lt f(b)$, the compact subspace 
$$Z_f = \{ x \in [a,b] \mid f(x) = 0 \}$$ is *occupied* (Cor 13.11 in 
_A Lambda Calculus for Real Analysis_). This is a condition 
that's weaker than *inhabited* but stronger than *nonempty*,
which you can read about in Section 8 of the same paper. 
I don't understand this condition very well, because I haven't spent as
much time thinking about ASD as I would like. Hopefully sometime soon
I'll find some time to work through some examples! 

---

Ok, thanks for reading, all! It's nice to get a few quick posts up while I'm 
working on some longer stuff. I'm still thinking a lot about a cool circle 
of ideas involving Fukaya Categories, Skein Theory and T(Q)FTs, and 
Hall Algebras, and I'm slowly making progress on writing posts about all these 
fun things.

Now, though, I have to go run a review session for a calculus class, haha.
I'll try to resist telling them about the fascinating subtleties that show 
up when you try to do everything constructively.

Stay safe, and we'll talk soon 💖

---

[1]: /2025/06/04/an-empty-product-of-nonempty-sets
[2]: https://raw.githubusercontent.com/Mzk-Levi/texts/master/Lambek%20J.%2C%20Scott%20P.J.%20Introduction%20to%20Higher%20Order%20Categorical%20Logic.pdf
[3]: https://global.oup.com/academic/product/sketches-of-an-elephant-9780198534259
[4]: https://ncatlab.org/nlab/show/Grothendieck+topos
[5]: https://ncatlab.org/nlab/show/topos#ElementaryTopos
[6]: https://mathoverflow.net/a/270923/145247
[7]: https://arxiv.org/pdf/math/9707206
[8]: https://ncatlab.org/nlab/show/natural+numbers+object
[9]: https://en.wikipedia.org/wiki/Stone%E2%80%93Weierstrass_theorem
[10]: /2022/02/16/talk-practical-topos-theory.html
[11]: https://en.wikipedia.org/wiki/Bernstein_polynomial#Elementary_proof
[12]: https://ncatlab.org/nlab/show/effective+topos
[13]: http://arxiv.org/abs/2204.00948
[14]: https://www.ams.org/journals/bull/2017-54-03/S0273-0979-2016-01556-4/S0273-0979-2016-01556-4.pdf
[15]: https://sites.google.com/ucr.edu/lucas-salim
[16]: https://www.paultaylor.eu/ASD/lamcra/lamcra.pdf
[17]: https://ncatlab.org/nlab/show/abstract+Stone+duality
[18]: https://ncatlab.org/nlab/show/overt+space

[^1]:
    Usually on this blog when I talk about topoi I mean [grothendieck topoi][4],
    but for this completeness result we really do need to allow more general 
    [elementary topoi][5] with [NNO][8]. Indeed there are statements true in all 
    grothendieck topoi that are *not* constructively provable (since they fail 
    in some elementary topos). See [here][6] for a partial list.

    I would actually love to know if there's a reference for what one has to 
    add to IHOL to get something sound and complete for *grothendieck* topoi...
    I spent some time looking, but the only thing I found was 
    [_Topological Completeness for Higher-Order Logic_][7] by Awodey and Butz,
    but it seems like they use $1+1$ in place of $\Omega$, so this isn't the 
    usual interpretation of logic in a grothendieck topos (which is also 
    where the *classical* completeness comes from).

[^2]:
    Maybe "base topos" would be less philosophically charged

[^3]:
    I was *really* fumbling around with topos theory back then, haha. 
    I'm much more confident now, and in the last few years I've just worked 
    through a lot more examples and done more computations and read more 
    papers and generally just learned a lot. Rereading that post was 
    surprisingly... nostalgic isn't the right word... but 
    it's fun to see how much I've grown!

[^4]:
    The usual proof with [bernstein polynomials][11] works if we're 
    careful to check some constructively relevant details. I'll copy it 
    here in case the wikipedia article changes someday:

    Fix $\epsilon > 0$. 

    We write $b_{k,n}(x) = \binom{n}{k} x^k (1-x)^{n-k}$, and note that:

    1. $\sum_{k=0}^n b_{k,n} = 1$
    2. $\sum_{k=0}^n \left ( x - \frac{k}{n} \right )^2 b_{k,n} = \frac{x(1-x)}{n}$

    These are all provable by just expanding the left hand side, which is 
    constructive.

    We also fix a $\delta$ so that whenever $|x-y| \lt \delta$ we have 
    $|f(x) - f(y)| \lt \epsilon$. This is because, constructively, every 
    continuous function on a compact sublocale of $\mathbb{R}$ is uniformly 
    continuous. Note that here we crucially need to be working with locales!
    (see, eg, Thm 10.7 in Taylor's [_A Lambda Calculus for Real Analysis_][16])

    Lastly, we fix $M$ an upper bound for $\lvert f \rvert$. This is possible since 
    $[0,1]$ is compact, overt, and inhabited
    (see Rmk 10.4 in Bauer and Taylor's _The Dedekind Reals in Abstract Stone Duality_)
    thus the continuous $\lvert f \rvert$ admits a maximum 
    (Thm 12.9 in _A Lambda Calculus for Real Analysis_).

    Now let $B_n f = \sum_{k=0}^n f(k/n) b_{k,n}$. We compute:

    $$
    \begin{aligned}
    \lvert f(x) - (B_n f)(x) \rvert 
    &\overset{(a)}{=} \lvert \sum_{k=0}^n (f(x) - f(k/n)) b_{k,n}(x) \rvert \\
    &\leq \sum_{k=0}^n \lvert f(x) - f(k/n) \rvert b_{k,n}(x) \\
    &\overset{(b)}{\leq}
        \sum_{k \text{ s.t. } |x-k/n| \lt \delta} 
            \lvert f(x) - f(k/n) \rvert b_{k,n}(x)
        +
        \sum_{k \text{ s.t. } |x-k/n| \gt \frac{1}{2}\delta}
            \lvert f(x) - f(k/n) \rvert b_{k,n}(x)
    \end{aligned}
    $$

    In step (a) we use (1), and in step (b) we use the fact that 
    $\forall x \in \mathbb{R} . x \lt \delta \lor x \gt \frac{\delta}{2}$ 
    is constructively true (since the intervals overlap we *don't* need 
    excluded middle here!)

    But we can bound the first sum by noticing in this region $|x-k/n| \lt \epsilon$ 
    so that (using (1) again)

    $$
    \begin{aligned}
        \sum_{k \text{ s.t. } |x-k/n| \lt \delta} 
            \lvert f(x) - f(k/n) \rvert b_{k,n}(x)
        &\leq
        \sum_{k \text{ s.t. } |x-k/n| \lt \delta} 
            \epsilon b_{k,n}(x) \\
        &\leq
        \sum_{k=0}^n \epsilon b_{k,n}(x) \\
        &= \epsilon
    \end{aligned}
    $$

    And since $\lvert f(x) - f(k/n)\rvert \leq \lvert f(x) \rvert + 
    \lvert f(k/n) \rvert \leq 2M$, we compute:
    
    $$
    \begin{aligned}
        \sum_{k \text{ s.t. } |x-k/n| \gt \frac{1}{2}\delta}
            \lvert f(x) - f(k/n) \rvert b_{k,n}(x)
        &\leq
        \sum_{k \text{ s.t. } |x-k/n| \gt \frac{1}{2}\delta}
            2M b_{k,n}(x) \\
        &\overset{(c)}{\leq}
        2M \sum_{k \text{ s.t. } |x-k/n| \gt \frac{1}{2}\delta}
            \left ( \frac{\delta}{2} \right )^{-2} 
            \left ( x - \frac{k}{k} \right )^2 b_{k,n}(x) \\
        &\leq
        \frac{8M}{\delta^2}
        \sum_{k=0}^n \left ( x - \frac{k}{k} \right )^2 b_{k,n}(x) \\
        &\overset{(d)}{=}
        \frac{8M}{\delta^2} \frac{x(1-x)}{n} \\
        &\leq 
        \frac{8M}{\delta^2} \frac{1}{4n}
    \end{aligned}
    $$

    In step (c) we use $|x - k/n| \gt \frac{\delta}{2}$ to say that 
    $\left ( \frac{\delta}{2} \right )^{-2} \left ( x - \frac{k}{k} \right )^2 \geq 1$,
    so that we can multiply through by it and make our sum bigger. 
    In step (d) we use (2), and at the end we use the fact that $x(1-x) \leq \frac{1}{4}$
    on $[0,1]$. 

    Now since $\mathbb{R}$ is constructively archimedian 
    (Defn. 1.1 in _The Dedekind Reals in Abstract Stone Duality_) we see 
    $\exists n \in \mathbb{N} . \frac{2M}{\delta^2n} \lt \epsilon$.

    Since these bounds were uniform in $x$, we learn that 

    $$\forall \epsilon \gt 0 . \exists n . \lVert f - B_n f \rVert_\infty \lt \epsilon$$

    as desired.

[^5]:
    A real number $x$ in this topos is a program that eats a natural number $n$ 
    and outputs a rational number $x(n)$. We think about this as a sequence of 
    rational approximations $x(n)$ converging to some real number $x$.
    So a function $[0,1] \to \mathbb{R}$ in this topos is a program that takes 
    as input a program $x$ (outputting rational approximations between $0$ and $1$) 
    and outputs a new program $f(x)$ which outputs rational approximations.

[^6]:
    Because our statement of Weierstrass 
    $\forall \epsilon . \forall f . \exists p . \lVert f - p \rVert_\infty \lt \epsilon$
    includes an existential quantifier there's no way to get around the fact 
    that the $p$ we build is only defined *locally* on an open cover.

    If you were more careful and gave a type theoretic proof that 
    $\prod_\epsilon \prod_f \sum_p \lVert f - p \rVert_\infty \lt \epsilon$
    then you could take $p$ to be a single polynomial defined on the whole of 
    $\Theta$... I haven't thought very hard about how possible this is
    (mainly because I haven't spent much time thinking about what theorems 
    about locales are provable in type theory), but I'm sure a talented 
    undergraduate could figure it out.

[^7]:
    The earliest version of this example which I've seen comes from 
    Stout's _Topological Properties of the Real Numbers Object in a Topos_
    back in 1976. I think basically every other paper I've cited in this 
    post gives some version of this example too, so it's very well 
    trodden ground!
