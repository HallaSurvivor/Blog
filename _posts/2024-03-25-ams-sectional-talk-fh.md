---
layout: post
title: Talk - What is Factorization Homology?
tags:
  - my-talks
---

I was recently invited to speak at the [AMS Sectional][1] in 
Tallahassee, Florida. In particular, at the special session on 
_Homotopy Theory and Category Theory in Interaction_. The 
conference was this weekend, and I'm typing this up on my 
plane ride home. I had a great time, and met a lot of great 
people! The special session was pretty small, so we all 
got to talk to each other, and I got surprisingly close 
with the people I went out for lunch (and later, drinks...) with!

I was nervous at first, since Florida... isn't politically friendly 
towards trans people. Thankfully everybody that I interacted 
with was lovely, and I didn't have any issues at all. What's more,
the campus was _beautiful_, and the surrounding area was 
surprisingly walkable. We had a _4 hour_ lunch break on the first 
day (which is part of how I got so close with my lunch group), 
and after we ate some great barbecue we all hung out under 
some fantastic trees.

TODO: add a few words about traveling with Kaya? 
TODO: Also a few words about how they helped answer silly questions 
    while drafting the talk... on friday, lol

TODO: put some pictures here

It was like $400 cheaper to fly out on Monday evening, even 
though the conference ended on Sunday, so [Kaya][2] and I had 
almost a whole day to ourselves. We went to the FSU 
[Museum of Modern Art][3] and walked around until it was 
airport time. 

These first few paragraphs were a bit bloggier than usual, 
but I had a _great_ time and wanted to talk about it! 
Now that we've had a chance to catch up, though, let's 
get to the math ^_^.

---

My talk was on [Factorization Homology][4], and I 
split it up into three sections:

- Why?
- What?
- How?

In the first section, I wanted to provide some motivation for 
the technology, and to explain why it deserves to be called 
"homology". 

The second section was all about what factorization 
homology _is_, at least in broad strokes. I left out a bunch of 
details about orientation and framings since the talk was only 
20 minutes and I wanted to stay light on my feet. This was 
also the section I got to express myself the most, since I 
view factorization homology through the lens of categorical logic[^1],
and I was able to spend some time on that perspective.

The third section was on actually _doing things_ with factorization 
homology. That is, on how we can really compute it, and how we can 
interpret what these computations mean. I wasn't able to spend 
_too_ much time on the interpretation, but I said a few words, 
and it was worth it for the extra time spent on a 
(sketchy version of a) simple example computation.

TODO: spelling on Phil's name below?
TODO: check that he was the one who invited you

There were some great questions after the talk, including one 
from [Phil Hackney][5] 
(one of the organizers, and the person who invited me) which 
gave me the chance to talk about what factorization homology 
has to do with my research.

All in all, I think the talk went super well. I don't think I 
came off as particularly manic, which can happen when I give 
short talks, and it seems like people were able to take some 
intuition away, which is everything I wanted! It helps that 
everyone at the conference was super nice, so I didn't have to 
worry at all about being judged or grilled.

---

So then, in more detail, what all did we talk about? 
In what follows, I'll always mean $\infty$-category, 
$\infty$-functor, etc. whenever I write "category", 
"functor", etc.

First, the _why_. 

We recall that "classical" cohomology $H^n(X,A)$ can be 
seen as $\pi_0 \text{Map}(X, K(n,A))$. Unraveling these 
hieroglyphics says that the cohomology of $X$ with 
coefficients in $A$ can be computed as the connected 
components of the [space of maps][6] from $X$ to the 
[eilenberg-mac lane space][7] $K(n,A)$[^2]. That is, 
with the set of maps up-to-homotopy $X \to K(n,A)$.

TODO: finish footnote 2 by showing that $H^1(X)$ classifies 
line bundles on $X$... you probably want to say $\mathbb{C}P^\infty$ 
here or something?

This encourages a rather broad perspective, which says 
that we can think of $\pi_0 \text{Map}(X,Y)$ as the 
"cohomology of the space $X$ with coefficients in the space $Y$". 
This is sometimes called [nonabelian cohomology][8], and 
many cohomology theories can be subsumed by this one 
(basically because lots of algebraic and topological things 
can be seen as spaces! See [here][9], for instance).

If we're calling this thing cohomology, it's natural to ask 
which "classical" theorems in cohomology are true in this 
setting. And one natural theorem to want is [Poincare Duality][10].

TODO: fix poincare accents wherever necessary

One motivation for factorization homology is that it's the 
right homology theory to make this "Nonabelian Poincare Duality" 
true!

In the talk I said some words about this, but online there's no 
need for me to say anything. If you're interested, you should 
just go read [Lurie's notes on the topic][11] instead. After all, 
I basically just paraphrased them!

If you insist on sticking around here, though, the idea is this:

To prove the "classical" poincare duality $H_i(X,A) \cong H^{n - i}_c(X,A)$,
one can show 

1. The functors $C_\bullet(-,A)$ and $C_c^\bullet(-,A)$ from 
the category of $n$-manifolds and smooth embeddings to the 
category of chain complexes are both [cosheaves][12]. 
2. _Just check_ that 
$C_\bullet(\mathbb{R}^n,A) \simeq C_c^\bullet(\mathbb{R}^n,A)$
3. Conclude that, since every manifold $\mathbb{R}^n$ is a bunch of 
$\mathbb{R}^n$s in a trenchcoat, this equivalence is actually 
true for all manifolds.
4. Taking homology of both sides to get the claim.

Basically, a cosheaf is something we can compute for a big thing 
by gluing together the computations for small things 
(you should have something like [Mayer-Veitoris][13] in mind). 
In particular, since every manifold is glued from copies of 
$\mathbb{R}^n$, a cosheaf is _totally determined_ by what it 
does to $\mathbb{R}^n$! So once we check that 
$C_\bullet(-,A)$ and $C_c^\bullet(-,A)$ agree on $\mathbb{R}^n$,
we get for free that they must agree _for every manifold_[^3]!

TODO: in footnote 3, find references to the "many places".

Now, if we _wanted_ to cook up a homology theory making 
some kind of "nonabelian poincare duality" true, we might 
try something like this:

1. Show $\text{Map}_c(-,Y) : \mathcal{M}\text{an} \to \mathcal{S}$ 
    is a cosheaf
2. Define the "nonabelian homology" of $\mathbb{R}^n$ to be 
    $\text{Map}_c(\mathbb{R}^n,Y)$
3. Use the cosheaf-ness to extend this definition to all manifolds by 
    "doing what you have to do".

This turns out to not _quite_ work, but if we define "nonabelian homology"
for all _disjoint unions_ 

$$
\emptyset, \ 
\mathbb{R}^n, \ 
\mathbb{R}^n \coprod \mathbb{R}^n, \ 
\mathbb{R}^n \coprod \mathbb{R}^n \coprod \mathbb{R}^n, \ldots
$$

we're able to get the job done[^4]!

So then, we've found ourselves with a functor defined on 
$\mathcal{D}_n$ -- the category of disjoint unions of $\mathbb{R}^n$s 
with smooth embeddings. Then we _freely extend_ this functor 
to the whole category of manifolds $\mathcal{M}\text{an}_n$ by 
defining the functor to be "compatible with gluing". The keyword 
here is [left kan extension][14].

If you're me, this feels a _whole_ lot like a familiar story 
from categorical logic!


---

[1]: AMS Sectional
[2]: kaya's website
[3]: get the museum of modern art link
[4]: factorization homology
[5]: phil hackney's website
[6]: mapping space
[7]: eilenberg-mac lane space
[8]: nonabelian cohomology
[9]: dold-kan correspondence
[10]: poincare duality
[11]: lurie's nonabelian poincare duality notes
[12]: cosheaf
[13]: mayer-veitoris
[14]: left kan extension

---

[^1]:
    Though honestly, I view _most_ things through the lens of either 
    categories or logic. So this should come as no surprise, haha.

[^2]:
    If you haven't seen this before, it's a _super_ useful perspective 
    to have on hand! For example, 

[^3]:
    This is one _killer_ example of why people care about this kind 
    of abstract nonsense. Not only do we need to know stuff about 
    (co)sheaves, we also have to care about $\infty$-categories! 

    This is basically because $\infty$-categorical things tend to 
    glue more nicely than $1$-categorical things. _This_, in turn, 
    is related to the idea that "Chain Complex: Good. Homology: Bad",
    as talked about in many places.

[^4]:
    This is basically because checking the cosheaf condition requires 
    some version of Mayer-Veitoris. But the "usual" version of 
    Mayer-Veitoris crucially uses the ability to add functions 
    (since $A$ is an abelian group). Now that $Y$ is any old space, 
    we lose addition.

    But by working with disjoint unions of $\mathbb{R}^n$s, we can 
    get a notion of "addition" back by taking the disjoint union of the 
    functions!

    You can read more about precisely what's going on in 
    [Lurie's notes][11].
