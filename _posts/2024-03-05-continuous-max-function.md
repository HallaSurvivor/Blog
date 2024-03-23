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
we can answer the OP's question by looking at the special case where $K_x$ 
is a constant family!

If you've been exposed to some ideas in topos theory, you should be screaming 
something to do with the "internal logic" right now! Indeed, a theorem inside 
the topos of [sheaves][9] on $X$ externalizes to give a version of that 
theorem where everything is automatically continuous in a parameter from $X$.
So if we have access to the extreme value theorem inside $\mathsf{Sh}(X)$ 
(that is, if we have a [constructive][10] proof of the extreme value theorem)
we would _immediately_ get the parameterized version for free!

---

So then, we want to get our hands on a constructive proof of the extreme 
value theorem. 
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

Before we copy his proof[^5], we should probably say some words about 
what all these new adjectives mean!

First, let's handle the easiest one: <span class=defn>Compact</span>.

The most familiar definition of compactness is that every open cover 
has a finite subcover. Precisely, if $\mathcal{U}$ is a family of open 
subsets of $X$ with $X = \bigvee \mathcal{U}$, then there should be a 
([kuratowski-][13])finite subfamily $\mathcal{U}_0 \subseteq \mathcal{U}$ 
so that actually $X = \bigvee \mathcal{U}_0$.

However, constructively it's better to avoid saying the word "finite" 
if you can. The notion of finiteness splits into different inequivalent 
notions (kuratowski-finite, bishop-finite, dedekind-finite, etc) which makes 
the whole thing a bit of a mess[^6]. For this reason, there's a different,
equivalent definition of compactness which we often prefer:

We say $X$ is called compact if for every _directed_ open cover $\mathcal{U}$[^7]
with $X = \bigvee \mathcal{U}$, we must actually have $X \in \mathcal{U}$!

<div class=boxed markdown=1>
As a cute exercise, prove these two definitions are equivalent! Try your 
hardest to make sure your proof is constructive!
</div>

There's one last angle on compactness that I want to emphasize here as well:
We say a locale is compact if _universal quantification is open_. That is, 
if $U \subseteq K \times X$ is open, we want to know if 
$$\{ x \mid \forall k . (k,x) \in U \} \subseteq X$$ is open.

This turns out to be true (for every $X$ and every $U$) if and only if $K$ 
is compact[^8]!

<br>

The next adjective on the list is <span class=defn>Overt</span>. This is 
a kind of tricky notion to work with, since it's invisible classically. 
We say a locale $O$ is overt iff for any locale $X$ and open subset 
$U \subseteq O \times X$, the projection 
$\{ x \mid \exists o \in O . (o,x) \} \subseteq X$ is open. Note how this is 
dual to the universal quantifier present for compact sets. Also note that 
this set is exactly the image of $U$ under $\pi_X : O \times X \to X$. 
Since, classically, this projection map is always [open][16], we learn that 
classically _every_ locale is overt[^9].

There's an equivalent characterization of overtness, which is often useful 
in practice. We want to check that the unique map $X \overset{!}{\to} 1$ 
is open. Since open maps are preserved by pullbacks, this gives the 
original definition for free. It also shows how this definition is classically 
invisible, since every subset of the terminal locale is open when the terminal 
locale is $\{\star\}$.

However, recall that in a sheaf topos $\text{Sh}(X)$ the terminal locale is 
$X$! Then a locale in $\text{Sh}(X)$ is just an external locale with a map 
into $X$, and overtness of the internal locale corresponds to openness of the 
external map! So there's obviously no reason to expect every locale to be 
overt constructively, since it's easy to find continuous functions 
that aren't open.

<br>

Lastly, we say that a locale is <span class=defn>Positive</span> iff every 
open cover must be inhabited. That is, if $X = \bigvee \mathcal{U}$ for 
$\mathcal{U}$ a family of open sets, the family $\mathcal{U}$ must be inhabited.

Recall we say $A$ is \emph{inhabited} exactly when $\exists a \in A$ is true.
In $\text{Sh}(X)$, this means that there's an open cover of $X$ so that $A$ 
has a section on every element of the cover. That is, exactly when the 
structure map $A \to X$ is surjective.

---

Now, let's outline the proof of the theorem. Recall a 
<span class=defn>Dedekind Real</span> is a pair of cuts $(L,U)$ where

- $L$ is a \emph{lower cut} in the sense that 
- $U$ is an \emph{upper cut} in the sense that
- $L$ and $U$ "have no gap" in the sense that

Now say $f : K \to \mathbb{R}$ is a map from a positive, overt, compact 
locale $K$. We'll use positive compactness to build 
$U = \{ q \mid \forall k \in K . k \lt q \}$ 
Then we'll use positive overtness to build 
$L = \{ q \mid \exists k \in K . q \lt k \}$. Lastly, we need to show 
that the $L$ and $U$ we just built "have no gap", which requires a 
small argument that you can read in Manuell's [slides][5].

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
[12]: http://logicandanalysis.org/index.php/jla/article/view/63/25
[13]: https://ncatlab.org/nlab/show/finite+set
[14]: https://pedromarun.github.io/
[15]: https://en.wikipedia.org/wiki/Tube_lemma
[16]: https://en.wikipedia.org/wiki/Open_and_closed_maps#Open_maps
[17]: https://ncatlab.org/nlab/show/overt+space
[18]: https://mathoverflow.net/questions/405866/what-does-overtness-mean-for-metric-spaces
[19]: https://en.wikipedia.org/wiki/Base_(topology)
[20]: https://www.mat.uc.pt/~tacl2022/slides/GMlecture3.pdf

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
    exactly the phenomenon we're trying to exploit, and we have to do work 
    somewhere!

[^3]:
    Any type theorists in the room are probably screaming
    [Dependent Sum][7] right around now! That's extremely fair, and I almost 
    put something in the main post about this, but I ended up editing it out.

[^4]:
    I really don't like Goldblatt's _Topoi_ as a book, but his section on the 
    relationship between bundles over $X$ and sets continuously "indexed" by $X$
    is super good. It's chapter 4 section 5, and it has some really helpful
    pictures and examples!

[^5]:
    Which he, in turn, mentions was based on the treatment in Paul Taylor's 
    [_A Lambda-Calculus for Real Analysis_][12]. I actually have this paper 
    saved, but it's long and I wasn't sure how easy it would be to translate 
    Taylor's results into language I'm more familiar with. Now that I've seen 
    Manuell do it, though, I have plans to read this paper pretty soon!

[^6]:
    I still haven't taken the time to _really_ familiarize myself with the 
    various notions of finiteness, and how they "feel". One day soon I want 
    to, though. 

[^7]:
    Recall a partial order $(D,\leq)$ is called <\span class=defn>directed</span>
    if it's inhabited and for any $x,y \in D$ their join $x \lor y$ is 
    in $D$ too.

    This is really hiding kuratowski-finiteness again, since directedness 
    guarantees that for any kuratowski-finite subset $F \subseteq D$ that 
    $\bigvee F \in D$. This is the usual argument that binary joins 
    imply finite (nonempty) joins.

[^8]:
    I was curious about this, and [Pedro][14] pointed out that one 
    direction is basically the classical [tube lemma][15]. I don't 
    actually see how to do the other direction (at least quickly) 
    and I don't really have time to think about it right now. If 
    someone figures it out I'd love to hear about it in the comments!

[^9]:
    Constructively it's still true that every locale with enough points is 
    automatically overt (see the [nlab][17]). It seems like a very mild 
    condition, see the discussion [here][18], for instance.
