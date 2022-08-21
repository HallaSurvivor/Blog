---
layout: post
title: Monoidal Monoidoidoids
tags:
  - 
---

So I was on the [nlab][1] the other day, and I saw a fantastic joke: 
A 2-category is "just" a monoidal monoidoidoid! Here's a screenshot
in case the nlab page for [2-categories][2] changes someday:

<p style="text-align:center;">
<img src="/assets/images/monoidal-monoidoidoids/screenshot.png" width="50%">
</p>

There's a thing called the _Category Theorist's "Just"_, which describes 
the joy that many category theorists take in telling other mathematicians
that an X is "just" a \[categorical gibberish\]. This is often seen as 
unhelpful at best and annoying at worst by other mathematicians, and I think
there's room for a bit of honest discussion here, if you'll give me a second
to preach (I'll get to the joke in the title soon, I promise).

I've met category theorists who do this _purely_ to try and look smart,
and to make other people who aren't fluent in abstract nonsense feel inadequate.

I do not like these category theorists.

That said, when you spend a long time around the language of category theory,
you really _do_ build an intuition for what certain common 
constructions (monoids, adjunctions, co/limits, etc.) look like in certain 
common kinds of categories 
(algebraic categories, topological categories, functor categories, etc.).

In this way, if someone knows the lingo, you can really convey a _lot_ of 
information very efficiently by the use of this language. For instance, I 
genuinely think the meme 

> monads are "just" monoids in the category of endofunctors

is a useful way to explain monads provided you're talking to 
another category theorist. How this hypothetical category theorist got 
comfortable with algebra internal to functor categories before getting 
comfortable with monads is beyond me, but weirder things have happened.

Of course, this quip is _entirely unhelpful_ if you're trying to explain 
monads to a software engineer with little to no knowledge of category theory...

---

Now, I personally try to never use the category theorist's "just" when I'm
talking to someone who I don't know well. Or if I do, I always make sure to 
preface it by a question of how much category theory they know, and the promise
that I can translate whatever abstract nonsense I say into concrete terms 
if they want me to.

The unique exception is when making jokes, because sometimes it's hilarious
to give the worst possible definition for a simple object. And 9 times out of 10
that definition will be categorical in nature. 

This leads to a fun little game where you try to obfuscate a definition as 
much as possible, and if you're like me, it's also fun to _deobfuscate_ 
the definition to see why it works! Which (finally) leads us to the title 
of this post:

<div class=boxed markdown=1>
Why is a 2-category "just" a Monoidal Monoidoidoid?
</div>

This is possibly the worst way to introduce 2-categories, and has the added
benefit of being incredibly silly to say out loud. 10/10. No notes. I'm 
absolutely adding this to my vocabulary.

<p style="text-align:center;">
<img src="/assets/images/monoidal-monoidoidoids/talented-brilliant.gif" width="50%">
</p>

But what does it _mean_?

Well first things first, we want to parenthesize this correctly. 
A 2-category is a (monoidal monoidoid)oid.

Category theorists love to put the suffix "[oid][3]" at the end of a preexisting 
word. In general if X is a gadget that can be seen as a one-object category,
then an X-oid will be that same kind of gadget, but allowing multiple objects.

For instance, a group can be seen as a one object category where every arrow
is invertible. So a <span class=defn>groupoid</span> is _any_ category where 
every arrow is invertible.

Similarly, an algebra over a field $k$ can be seen as a one object category
whose homset is a $k$-vector space[^1]. So an <span class=defn>algebroid</span>
is a category all of whose homsets are $k$-vector spaces. 

The exception is monoid, which historically already has an "oid" suffix. 
A monoid is "just" a one object category, so a monoidoid should be _any category_.
Obviously nobody calls categories "monoidoids", but it's kind of cute to know
we _could_.

<br>

Next we need to understand monoidal monoidoids. That is, [monoidal categories][4].
We're about to oid-ify this into (monoidal monoidoid)oids, so we should be
able to view a monoidal category as a kind of one-object category in its 
own right.

We know that monoidal categories are categories $\mathcal{C}$ with a multiplication 
$\otimes : \mathcal{C} \times \mathcal{C} \to \mathcal{C}$. So by analogy with
groupoids and algebroids from before, we should expect this multiplication to
become composition in some kind of one-object category.

Inspired by this, say $\mathcal{C}$ is a monoidal category. Let's build a 
new category with one object $\star$, and we'll take $\text{Hom}(\star,\star)$
to be the objects of $\mathcal{C}$. Then "composition" of two objects $C_1$
and $C_2$ (viewed as arrows $\star \to \star$) should be the object $C_1 \otimes C_2$
(viewed as an arrow $\star \to \star$).

Of course, $\mathcal{C}$ has arrows too! Since in our one-object category 
the objects of $\mathcal{C}$ became arrows $\star \to \star$, the _arrows_ of
$\mathcal{C}$ need to be "arrows between the arrows", and these 2-arrows are
compatible with 1-composition of 1-arrows in the sense that 1-composition was 
given by $\otimes$, which is a bifunctor 
(so has an action on arrows of $\mathcal{C}$, or 2-arrows of our new category).

So then, a monoidal category $\mathcal{C}$ is "just" a category with 
one object $\star$ equipped with a collection of "2-arrow"s 
$\text{2Hom}(C_1,C_2)$ for each pair of arrows $C_1, C_2 : \star \to \star$.
These 2-arrows can compose in the expected way 
(this is often called <span class=defn>vertical composition</span>)
and are also compatible with composition of 1-arrows (in the sense that 
1-composition acts on 2-arrows like a bifunctor $\otimes$. This is often
called <span class=defn>horizontal composition</span>)[^2]. 

<br>

So finally, we see that we can oid-ify the notion of monoidal category by
removing the assumption that there be a single object $\star$.

Now a "monoidal category"-oid (or a monoidal monoidoid oid, or a 2-category)
has

 - Objects
 - 1-Arrows between the objects
 - 2-Arrows between the 1-arrows

We can compose 1-arrows in the expected way, and we can compose 2-arrows
_vertically_ (which is the obvious way) and _horizontally_ (which says that 
2-arrows are compatible with composition of 1-arrows)[^3].

---

Another short post for once! I'm once again on my way to New York tonight
to see some friends, but when I saw "monoidal monoidoidoid" on the nlab 
I literally laughed out loud. I spent a bit of time yesterday figuring out
what it meant (though in hindsight the nlab page just tells you...) and wanted
to write this up and share it today before I head to the airport.

As another little life update, I was at [BLAST][6] last week, and had a _ton_
of fun[^4]! It was great to hang out with other logicians, and it's super exciting
to know that there's likeminded people so near me -- It was getting kind of 
lonely being the only logician at UC Riverside. Everyone was super nice, and 
I had a lot of great conversations. I'll definitely be at BLAST next year,
and I might try to spend a bit of time at Chapman too.

For now, though, I have to start packing. Take care everyone, and 
see you soon ^_^

---

[^1]: 
    Do you see why? As a hint, multiplication in your algebra becomes 
    composition in the category, just like group multiplication becomes composition.

[^2]:
    Concretely, if we have 2-arrows $f : C_1 \to C_2$ and $g : C_2 \to C_3$
    then we can compose these "vertically" to get a single 2-arrow $gf : C_1 \to C_3$.

    <p style="text-align:center;">
    <img src="/assets/images/monoidal-monoidoidoids/vertical.png" width="50%">
    </p>

    If instead we have objects $C_1$, $C_1'$, $C_2$, and $C_2'$ with arrows
    $f$ and $f'$ as in the following setup

    <p style="text-align:center;">
    <img src="/assets/images/monoidal-monoidoidoids/horizontal.png" width="50%">
    </p>

    then 
    (recalling that the "composition" $C_1' \circ C_1 : \star \to \star$ is 
    given by the monoidal product $\otimes$)
    we can compose these "horizontally" to get a 2-arrow 
    $f' \otimes f : C_1' \otimes C_1 \to C_2' \otimes C_2$.

[^3]:
    Another way to see this is to say that a monoidal category is a 
    category with one object $\star$ whose homset $\text{Hom}(\star, \star)$ 
    is itself a category.

    Then we recover (strict) 2-categories as the oid-ified version of this.
    That is, as a category where each homset $\text{Hom}(A,B)$ is itself a 
    category. That is, a 2-category is "just" a category [enriched][5] in
    $\mathsf{Cat}$.

    This is _perfectly_ analogous to the case of $k$-algebroids being 
    categories enriched in $k$-mod.

[^4]:
    One could say I.... Had a blast? :P

[1]: https://ncatlab.org/nlab/show/HomePage
[2]: https://ncatlab.org/nlab/show/2-category
[3]: https://ncatlab.org/nlab/show/oidification
[4]: https://en.wikipedia.org/wiki/Monoidal_category
[5]: https://ncatlab.org/nlab/show/enriched+category
[6]: https://math.chapman.edu/blast2022/
