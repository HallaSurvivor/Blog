---
layout: post
title: Proving Another "Real Theorem" with Topos Theory
tags:
  - 
---

Another day, another post that starts with "So I was on mse...", lol. 
Somebody [asked][6] whether maximizing over a compact set is a continuous thing 
to do. That is, given a continuous function $f : K \times X \to \mathbb{R}$ is the 
function $x \mapsto \max_{k \in K} f(k,x)$ continuous?

If you're me, this looks an awful lot like the usual 
[extreme value theorem][1], but where 
"everything in sight depends continuously on a parameter from $X$". Indeed,
say we had a family of compact sets $K_x$ depending on a parameter from $X$,
and a family of functions $f_x : K_x \to \mathbb{R}$ which is continuous both 
in the choice of $x$ and in the choice of $k \in K_x$. Then the usual extreme 
value theorem tells us that we have pointwise maxima 
$m_x = \max_{k \in K_x} f_x(k)$, and it's natural to ask whether these 
maxima _also_ vary continuously in the parameter $x$. 

Depending on your experience with [bundles][11], you might be aware that 
the usual way to encode a "family of sets $A_x$ continuously depending on $x \in X$"
is with a single space $A$ 
(usually called the <span class=defn>total space</span>)
equipped with a map $\pi : A \to X$. Then the fibres of $\pi$ give us the 
desired family of sets $A_x = \pi^{-1}(x)$[^4]. As a super concrete example, 
say we want to represent the constant family $A_x = \mathbb{R}$. Then 
we should use the <span class=defn>trivial bundle</span> 
$\mathbb{R} \times X$ with the obvious projection map 
$\pi : \mathbb{R} \times X \to X$[^1]. 

<div class=boxed markdown=1>
I bet you weren't expecting a cute exercise this early in the post!

Can you show that a family of functions $f_x : A_x \to B_x$ over $X$ 
is the same thing as a single function $f : A \to B$ making the following 
diagram commute:

<p style="text-align:center;">
<img src="/assets/images/continuous-max-function/bundle-map.png" width="50%">
</p>

To go from the family $f_x$ to a single function $f$ on the total spaces, 
it might be worth remembering that the total space $A$ is just the 
disjoint union of the fibres[^3] $\sum_{x \in X} A_x$ (suitably topologized).
</div>

So the constant family $K_x = K$ of compact sets is represented by the trivial
bundle $K \times X$, and (by the above exercise) a family of functions 
$f_x : K_x \to \mathbb{R}$ is represented by a function 
$f : K \times X \to \mathbb{R} \times X$ with $\pi_2 (f(k,x)) = x$. Since we 
know what the second component _must_ be, this is the same data as a function 
$K \times X \to \mathbb{R}$! This tells us that, if we can prove some 
"$X$-parameterized" version of the extreme value theorem 
(where the resulting maxima also depend continuously on a parameter $x \in X$), 
it should give us the OP's question in the special case where $K_x$ is a 
constant family!

If you've been exposed to some ideas in topos theory, you should be screaming 
something to do with the "internal logic" right now! Indeed, a theorem inside 
the topos of [sheaves][9] on $X$ externalizes to give a version of that 
theorem where everything is automatically continuous in a parameter from $X$.
So if we have access to the extreme value theorem inside $\mathsf{Sh}(X)$ 
(that is, if we have a [constructive][10] proof of the extreme value theorem)
we would _immediately_ get the parameterized version for free!

---

So then, we want to get our hands on a constructive proof of the extreme 
value theorem. Then, interpreting this proof inside the topos $\mathsf{Sh}(X)$ 
of sheaves on $X$ will give us the claim. In fact, as we'll see later, it 
gives us a slightly stronger claim.

Typically constructive theorems which assert the _existence_ of something 
(in this case, a maximum) require some ~bonus assumptions~ which are invisible 
in the classical case. This is because existence is a much stronger 
phenomenon constructively[^2].

To start, we probably want to be working with [locales][2] instead of 
topological spaces. Since the person on mse was happy with $K$ and $X$ 
_metrizable_, they'll certainly be ok with [sobriety][3] since hausdorff-ness 
already implies it! Since sober spaces and locales (with enough points) are 
the same thing, we lose nothing by moving to the world of locales. There's a 
good notion of compactness for locales, and so one can google
`"extreme value theorem"+"locale"`
to find [Graham Manuell's slides][5] from [TACL 2022][4] which give a 
constructive proof of the following:

<div class=boxed markdown=1>
If $K$ is a compact, overt, positive locale, and $f : K \to \mathbb{R}$ 
is continuous, then $f$ has a maximum $\max_K f$ given by a dedekind real.
</div>




---

[1]: https://en.wikipedia.org/wiki/Extreme_value_theorem#Generalization_to_metric_and_topological_spaces
[2]: https://ncatlab.org/nlab/show/locale
[3]: https://ncatlab.org/nlab/show/sober+topological+space
[4]: https://www.mat.uc.pt/~tacl2022/
[5]: https://www.mat.uc.pt/~tacl2022/slides/GMlecture5.pdf
[6]: https://math.stackexchange.com/q/4870971/655547
[7]: https://en.wikipedia.org/wiki/Dependent_type#%CE%A3_type
[8]: https://en.wikipedia.org/wiki/Fiber_bundle
[9]: https://ncatlab.org/nlab/show/sheaf
[10]: https://ncatlab.org/nlab/show/constructive+mathematics
[11]: https://en.wikipedia.org/wiki/Fiber_bundle

[^1]:
    Note that it's possible to have constant fibres, _without_ being the 
    trivial bundle! In this case, even though each fibre is the same as 
    every other, we _glue them together_ in an interesting way! To be the 
    trivial bundle, you need to know the fibres are all the same, _and_ that 
    we glued them together in the most naive way possible. For instance, 
    the trivial $\mathbb{R}$-bundle over the circle $S^1$ looks like a cylinder,
    since we glue the copies of $\mathbb{R}$ together in the simplest possible way.
    However, we could slowly "twist" our copies of $\mathbb{R}$ as we move around 
    the circle as we glue them together to get a moebius strip! 
    This is still a continuously varying family of copies of $\mathbb{R}$, 
    but now the bundle is nontrivial! Here's a picture from wikipedia:

    <p style="text-align:center;">
    <img src="/assets/images/continuous-max-function/mobius-bundle.png" width="75%">
    </p>


[^2]:
    As witnessed (pun intended) by the fact that, interpreted in suitable topoi, 
    a constructive existence proof gives rise to free theorems saying 
    there's an algorithm that produces the desired object, or that the 
    desired object can be defined continuously in a parameter, etc. This is 
    exactly the phenomenon we're trying to exploit!

[^3]:
    Any type theorists in the room are probably screaming
    [Dependent Sum][7] right around now! That's extremely fair, and I almost 
    put something in the main post about this, but I ended up editing it out.

[^4]:
    I really don't like Goldblatt's _Topoi_ as a book, but his section on the 
    relationship between bundles over $X$ and sets continuously "indexed" by $X$
    is super good. It's chapter 4 section 5, and it has some really helpful
    pictures and examples!
