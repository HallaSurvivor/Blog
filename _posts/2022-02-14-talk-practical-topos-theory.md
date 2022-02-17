---
layout: post
title: Talk -- Let's Solve a Simple Analysis Problem. Together.
tags:
  - my-talks
---

Last Friday I gave a talk in GSS where I tried to give a super concrete
application of topos theory to "mainstream" mathematics. The idea was to solve
a simple analysis problem, streamlining the argument by using the internal
logic of a sheaf topos. The _good_ news is that I think I was quite successful
in making my point that "ordinary mathematicians" should care about topos 
theory and constructive logic. The _bad_ news is that the last 10 minutes of
my talk were false... It didn't end up mattering, but I was still pretty torn 
up about it. Anyways, in this post I'll give an overview of the talk, which
should double as a nice description of how to actuallly _use_ topos theory
to solve problems.
I'm planning to start a new series soon where I go over this
proof in more detail, explaining the relevant aspects of topos theory along
the way!

So then, what was the talk about? 

Recall the [Weierstrass Approximation Theorem][1], which says that

<div class=boxed markdown=1>
For every continuous $f : [0,1] \to \mathbb{R}$, for every $\epsilon > 0$,
there is a polynomial $p$ so that $\lVert f - p \rVert_\infty < \epsilon$.
</div>

Let's look into a natural generalization of this. Say 
$$(f_\omega : [0,1] \to \mathbb{R})_{\omega \in X}$$ is a 
continuous family of continuous functions. That is, 
$f : X \times [0,1] \to \mathbb{R}$ is continuous, and we think of 
$f(\omega,-)$ as a function $f_\omega$. 

If we fix an $\epsilon > 0$, then we know that each $f_\omega$ can be 
approximated by some polynomial $p_\omega$. It's natural to ask if the $p_\omega$
also vary continuously in $\omega$. That is, are the coefficients continuous
functions of $\omega$?

In case $f$ is "nice", then the answer is obviously yes. After all, if we look
at $\sin(\omega t) : [0,2] \times [0,1] \to \mathbb{R}$, then if 
$\epsilon = 0.025$ we see that the family 

$$p_\omega(t) = \omega t - \frac{\omega^3}{6} t^3 + \frac{\omega^5}{120} t^5$$

has $\lVert f_\omega - p_\omega \rVert_\infty \lt \epsilon$ for every $\omega$,
and the coefficients are continuous in $\omega$.

In case $f$ is "not nice", the situation is much murkier. For instance, say[^1]

$$
f_\omega(t) = \sum_{n=0}^\infty \omega^n \cos(12^n \pi t)
$$

each of these are continuous, nowhere differentiable, and _highly_ oscillatory.
With this in mind, a reasonable person might wonder if these $f_\omega$ are 
too sensitive to initial conditions for us to have continuity of the polynomial
approximators[^2].

So, what to do? Notice that naively applying the theorem to each $f_\omega$
in no way guarantees continuity. We need a cleverer argument in order to treat
the $f_\omega$ uniformly (at least locally) in $\omega$.

This brings us to the, probably quite surprising, idea motivating the talk:

<div class=boxed markdown=1>
Let's solve this analysis problem with high powered category theory and constructive logic!
</div>

---

I spent the next little while "defining" a [topos][4] as a category which
"looks like $\mathsf{Set}$". Since we know that we can encode all of mathematics
in set theory (formally, $\mathsf{ZFC}$) then we should be able to translate
that encoding to a topos too. I then drew an evocative picture on the board,
which I completely ripped off from Ingo Blechschmidt's [website][5]. In this
post I'll spare you my art, and just rip off the photo directly:

<p style="text-align:center;">
<img src="/assets/images/talk-practical-topos-theory/external-internal.jpeg" width="50%">
</p>

(Except when I drew this on the board, I used "weierstrass approximating polynomial"
instead of "finitely generated module")

Later in the talk I went into more detail about what exactly the 
"complicated external statement" is. But before we could go into that,
we need to get an important caveat out of the way:

<div class=boxed markdown=1>
If we want to do mathematics inside of a topos, it has to be 
<span class=defn>Constructive</span>
</div>

What do I mean by "constructive"? Well to start, it shouldn't use the axiom of choice.
Indeed, even _very_ weak principles like [countable choice][6] can fail[^3]. 
It really doesn't take too long (imo) to get used to working without choice[^4].
But more importantly, we have to work without the [Law of Excluded Middle][7]
(LEM), and this can take quite a bit of getting used to.

At this point in the talk I introduced the notion of a 
[sheaf][8] on a topological space, as well as sheaf maps, and thus
the category $\mathsf{Sh}(X)$ of sheaves on $X$[^7]. Of course, the canonical
example of a sheaf on $X$ is the sheaf of continuous real valued functions 
on $X$, and I went over this example in some detail.

Then I said
that the truth values $\mathsf{Sh}(X)$ are exactly the opens of $X$. I used
this to explain how LEM fails[^5] in this topos.
As you might expect, this is relevant because it means that we'll need to know our proof of the
weierstrass approximation theorem is constructive if we want to interpret it
inside $\mathsf{Sh}(X)$. 

At this point I talked about the [natural numbers object][9] in $\mathsf{Sh}(X)$
(which assigns to each open set $U$ the set $\mathbb{N}$, with the 
identity as the restriction maps. Then I showed how we can use this to build
$\mathbb{Z}$ and $\mathbb{Q}$ inside $\mathsf{Sh}(X)$ just like we do in
$\mathsf{Set}$. This was a multipurpose discussion, because it showed how we
can do mathematics in a topos just as we do with sets. It also let me introduce
the real numbers object $\mathbb{R}$ as the object you get by doing dedekind
cuts inside $\mathsf{Sh}(X)$[^6], which I then externalized (without proof)
as the sheaf of continuous functions on $X$ from before[^8]!

Next I introduced the notation for forcing, where we say that 
$U \Vdash \varphi$ (read as "$U$ forces $\varphi$") if $\varphi$ is true on
$U$. I told the audience I would formally define this later, but the important
"theorem" is called <span class=defn>Soundness</span>:

<div class=boxed markdown=1>
If we can prove $\varphi$ without LEM or choice, then it is true inside 
the topos $\mathsf{Sh}(X)$ in the sense that $X \Vdash \varphi$.
</div>

Here "theorem" is in scare quotes because I haven't given anywhere near enough
details to make this precise. But the purpose of the talk was to get the point
across that we should care about constructive mathematics, and this idea of a
theorem was good enough for that purpose.

Now that we have the soundness "theorem" in hand, let's see if the 
weierstrass approximation theorem is even provable constructively! The 
next step of the talk was formally writing down the theorem we're proving:

<div class=boxed markdown=1>
Thm (Weierstrass):

$$
\forall f : C \big ( [0,1], \mathbb{R} \big ) . \ 
\forall \epsilon : \mathbb{R}_{> 0} . \ 
\exists p : \mathbb{R}[t] . \ 
\forall t : [0,1] . \ 
|f(t) - p(t)| \lt \epsilon
$$
</div>

Now, it looks like there _is_ a completely constructive proof of this theorem
(see chapter $4$ of Bridges' _Constructive Functional Analysis_[^9]), but I
wanted to show how easy it is to miss a usage of LEM, so I gave the proof
via [bernstein polynomials][10], which you can find in the "elementary proof"
section of the wikipedia page.

In this proof we separate a sum into "good" and "bad" parts, which we
approximate separately. But knowing that each summand is either "good" or "bad"
requires LEM[^10].

At this point, I said that this proof _does_ go through in 
$$\mathsf{Sh}_{\lnot \lnot}(X)$$, the topos of "double negation sheaves",
which is equivalent to $$\mathsf{Sh}(X_{\lnot \lnot})$$, the topos of sheaves
on the (typically pointfree) [locale][11] of regular opens in $X$.
I talked about how we actually go about externalizing statements internal to
a sheaf topos to get statements about sheaves, but I got muddled up in how
truth in $$\mathsf{Sh}(X_{\lnot \lnot})$$ relates to truth in $\mathsf{Sh}(X)$.

Normally I would use this as a learning experience, and show you all what my
mistake was. But I was _so_ muddled up I don't think it would be worth it[^12]. 

Next up was forcing semantics. If we want to know how to externalize 
theorems proved by mathematicians inside the topos, we need to know how to
interpret logic inside as statements we can see from outside. In the talk
I spent some time going over these, but they're available in lots of places
already (for instance, on page $316$ of Mac Lane and Moerdijk's 
_Sheaves in Geometry and Logic_), so I won't go into it in this post.
I _will_ show how to translate the weierstrass approximation theorem 
step by step, though:

$$
X \Vdash 
\forall f : C \big ( [0,1], \mathbb{R} \big ) . \ 
\forall \epsilon : \mathbb{R}_{> 0} . \ 
\exists p : \mathbb{R}[t] . \ 
\forall t : [0,1] . \ 
|f(t) - p(t)| \lt \epsilon
$$

we unravel the outer universal quantifier, and find[^13]:

For every $U$ open in $X$, for every $f : U \times [0,1] \to \mathbb{R}$,

$$
U \Vdash 
\forall \epsilon : \mathbb{R}_{> 0} . \ 
\exists p : \mathbb{R}[t] . \ 
\forall t : [0,1] . \ 
|f(t) - p(t)| \lt \epsilon
$$

Unraveling this, we see:

For every $U_1$ open in $U$, for every positive $\epsilon : X \to \mathbb{R}$,

$$
U_1 \Vdash
\exists p : \mathbb{R}[t] . \ 
\forall t : [0,1] . \ 
|f(t) - p(t)| \lt \epsilon
$$

Then we see:

There is an open cover $V_\alpha$ of $U_1$, and polynomials $p_\alpha$ with
coefficients continuous on $V_\alpha$ so that, for each $V_\alpha$ we have

$$
V_\alpha \Vdash
\forall t : [0,1] . \ 
|f(t) - p(t)| \lt \epsilon
$$

That is, for every $V_{\alpha, 1}$ open in $V_\alpha$, and
every $t : V_{\alpha, 1} \to [0,1]$ we have

$$
V_{\alpha, 1} \Vdash
|f(t) - p(t)| \lt \epsilon
$$

That is, $$\lvert f(x,t(x)) - p_{\alpha}(x,t(x)) \rvert \lt \epsilon(x)$$ for each $x \in V_{\alpha, 1}$.

Putting these pieces together, and choosing $U_1 = U = X$, as well as $V_{\alpha, 1} = V_\alpha$,
then letting $\epsilon$ and $t$ be constant functions, we find

<div class=boxed markdown=1>
There is an open cover $V_\alpha$ of $X$ and polynomials $p_\alpha$ with 
coefficients continuous on $V_\alpha$ so that, on each $V_\alpha$ we have

$$| f(x,t) - p_\alpha(x,t) | \lt \epsilon$$

for every $t \in [0,1]$.
</div>

which is exactly what we wanted! 

---

Now, this is true because we have Bridges' genuinely constructive proof of 
the weierstrass approximation theorem. The proof that I gave in the talk,
involving LEM doesn't quite provide this. Instead, it shows that
there's a dense open set $U$ of $X$, and an open cover $V_\alpha$ of $U$,
so that the rest holds.

I'm still thinking about the double negation modality, and a while ago I asked
[a question about this][13] on mse. 

I'm planning to start a series on topos theory and how we can actually solve
problems with it, and this double negation stuff will definitely get its own
post.

In the meantime, I'll leave you with the abstract for the talk. Take care
everyone, see you soon ^_^.

---

Solving An Easy Analysis Problem: Together.

\*asmr voice\* Let's all take a break. Unwind. And solve a nice friendly problem in elementary analysis.
Now that I've lulled you into a false sense of security, you should know that we'll be solving this
(very concrete!) problem by using heavy duty machinery from category theory and logic. In particular,
we'll be using the language of topos theory. In the process, we'll see why people care about constructive
mathematics, how category theory can solve real problems, and whether topos theory really is as
scary as its reputation makes it out to be.
We assume no background in topos theory, or indeed anything but basic category theory.


---

[^1]:
    Don't worry about the $12$. It's just there to make sure this family is
    continuous and nowhere differentiable for $\omega \in (1/2, 1)$. See 
    [here][2].


[^2]:
    As an aside, [desmos][3] shows this doesn't happen, but it's super nonobvious
    from just the definition of $f$. This is yet another reason that computers
    can be invaluable for guessing whether a theorem should be true or false!

[^3]:
    In fact, this is probably the biggest reason I care about AC at all!

[^4]:
    Maybe this is because I did my undergrad in a very logic-heavy department,
    so lots of my classes were somewhat sensitive to choice anyways?

[^5]:
    Since truth values are opens, if the truth value associated to $\varphi$
    (denoted $[ \! [ \varphi ] \! ]$) is, say, $(0, \infty) \subseteq \mathbb{R}$
    then $[ \! [ \lnot \varphi ] \! ]$ is _not_ the complement of $[ \! [ \varphi ] \! ]$,
    as you might expect. It's the _interior_ of that set. 

    So then 

    $$
    [ \! [ \varphi \lor \lnot \varphi ] \! ] = 
    [ \! [ \varphi ] \! ] \cup [ \! [ \varphi ] \! ] =
    (0, \infty) \cup (-\infty, 0) \neq \mathbb{R}
    $$

    and we see that $\varphi \lor \lnot \varphi$ is not true in $\mathsf{Sh}(X)$!

    I know I'm glossing over a lot of details here, but only because I want to 
    write up a more detailed post in the nearish future.

[^6]:
    I elected to omit the fact that dedekind and cauchy reals are different in
    the absence of LEM or CC. 

[^7]:
    I gave this definition without saying the word "functor" or "natural transformation"
    since I think it's important for this talk to be accessible to people with
    as little category theoretic background as possible.

[^8]:
    As an aside, I was quite pleased with this section of the talk! I thought
    it flowed really well, since I gave this sheaf as my main example earlier,
    and then built up to it as the real numbers object. 

[^9]:
    Candidly, though. I haven't read the whole book. I looked through that 
    chapter, but apparently Bridges uses some nonstandard definitions that
    might be misleading... I haven't actually checked to see how this squares
    with the definitions we usually use in a topos.

[^10]:
    For a while I thought we could get around this since $\mathbb{Q}$ has 
    decidable equality, but we really can't.

    For instance, let $a$ be the "real number" which is given by the continuous
    function $x \mapsto -|x|$. Then $a \geq 0$ is true only at $0$ 
    (thus its truth value is $\emptyset$, the interior of $\{0\}$) 
    and $a \lt 0$ is true on $(-\infty,0) \cup (0,\infty)$. 

    So even comparing a real $x$ to a _natural_ number $n$ doesn't guarantee 
    $x \geq n \lor x \lt n$ is valid.

[^12]:
    If you really want to have an idea, I that that semantics in 
    $\mathsf{Sh}(X_{\lnot \lnot})$ was "basically the same" as truth in
    $\mathsf{Sh}(X)$, except we have to restrict attention to [regular opens][12].

    Since $\mathbb{R}$ has a basis of regular opens, this really doesn't change
    anything at all, and it wasn't sitting right with me, because it felt like
    we could really just use double negation for free. I thought it was too
    good to be true and it was ¯\_(ツ)_/¯. 

    I'll spend more time talking about double negation in a future post.

[^13]:
    using the fact that continuous maps $[0,1] \to \mathbb{R}$ inside 
    $\mathsf{Sh}(X)$ correspond to continuous maps $[0,1] \times X \to \mathbb{R}$
    externally. See, for instance, Fourman's _Sheaf Models for Analysis_,
    on written page $286$.


[1]: https://en.wikipedia.org/wiki/Stone%E2%80%93Weierstrass_theorem#Weierstrass_approximation_theorem
[2]: https://en.wikipedia.org/wiki/Weierstrass_function
[3]: https://www.desmos.com/calculator/jvax2h3tui
[4]: https://en.wikipedia.org/wiki/Topos
[5]: https://www.ingo-blechschmidt.eu/
[6]: https://en.wikipedia.org/wiki/Axiom_of_countable_choice
[7]: https://en.wikipedia.org/wiki/Law_of_excluded_middle
[8]: https://en.wikipedia.org/wiki/Sheaf_(mathematics)
[9]: https://en.wikipedia.org/wiki/Natural_numbers_object
[10]: https://en.wikipedia.org/wiki/Bernstein_polynomial
[11]: https://ncatlab.org/nlab/show/locale
[12]: https://en.wikipedia.org/wiki/Regular_open_set
[13]: https://math.stackexchange.com/questions/4378270/externalizing-a-concrete-application-of-double-negation-toposes
