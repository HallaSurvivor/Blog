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
TODO: mention that you were the opening talk of the afternoon session?

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

TODO: where the hell did I put part 2 on the "what"?
TODO: Valeria's last name?

At this point in the talk I took a quick diversion to remind 
people about [Functorial Semantics][15]. This was extra easy
since in the morning session [Valeria][16] spent some time 
talking about the lawvere theory for monoids!

<br>

In (1-categorical) functorial semantics, we have _classifying categories_ 
associated to algebraic theories. Then a model of that 
theory is "just" a functor from the classifying category to 
$\mathsf{Set}$. For instance, the classifying category $\mathcal{A}$ 
for abelian groups looks like this[^5]:

TODO: put the picture here

and the classifying category for rings $\mathcal{R}$ is:

TODO: another picture.

Indeed, a finite product functor $\mathcal{A} \to \mathsf{Set}$ 
has to send $1$ to some set $A$. Then, since it's product preserving, 
it has to send $2$ to $A^2$, and $0$ to $A^0 = \{ \star \}$. Then 
the indicated maps get sent to honest operations on $A$, which give us 
the desired abelian group structure on $A$.

TODO: in footnote 5... have we talked about this kind of stuff before?
We must have, right? Link the relevant blog post. If not, link 
Awodey's notes on the topic.

Note that we have an embedding $j : \mathcal{A} \hookrightarrow \mathcal{R}$.

Now any ring $R$ is a (finite product) functor 
$\mathcal{R} \to \mathsf{Set}$, and if we _restrict_ along $j$ 
we get a new finite product functor $\mathcal{A} \to \mathsf{Set}$. 
That is, we get an abelian group! It should be believable that this is 
the underlying abelian group of the ring we started with!

TODO: picture of the restriction

More excitingly, can we go the other way? Given a functor 
$\mathcal{A} \to \mathsf{Set}$ (that is, an abelian group) 
is there a way to freely _extend_ this functor to one defined 
on all of $\mathcal{R}$? 

TODO: picture of extension

The answer, of course, is _yes_ and it's given by 
left kan extension! This recovers the usual free ring on an 
abelian group $A$.

<br>

Primed with this context, let's look at our definition of 
factorization homology again:

We have a (symmetric monoidal) functor $\mathcal{D}_n \to \mathcal{C}$.
This data is actually quite well studied, since it's a model for 
[$E_n$-algebras] in $\mathcal{C}$. These are monoids in $\mathcal{C}$ 
that are "commutative up-to-homotopy living in dimension $n$"[^6].

So we have something that looks like some kind of algebra, which is 
given by a functor out of $\mathcal{D}_n$. Then we want to _freely extend_ 
this data to a new kind of algebra, given by a functor out of 
$\mathcal{M}\text{an}_n$... 

Doesn't this setup sound familiar?

If $A : \mathcal{D}_n \to \mathcal{C}$ is our $E_n$-algebra, 
We define $\int_{(-)} A : \mathcal{M}\text{an}_n \to \mathcal{C}$,
the <span class=defn>Factorization Homology</span> to be the 
left kan extension of $A$ along $j$. We can think of this as a kind of 
"algebra" which is graded by connected manifolds. Moreover, we have 
operations between these graded pieces corresponding to smooth embeddings!

For instance, if $i : M_1 \coprod M_2 \to N$ is a smooth embedding, then 
we get an operation $\int_{M_1} A \otimes \int_{M_2} A \to \int_N A$.

TODO: write the section on "how"... Also, revise all of this, haha

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
[15]: functorial semantics
[16]: Valeria's website, if you can find it
[17]: algebraic theory
[18]: essentially algebraic theory
[19]: En algebra
[20]: braided monoidal category
[21]: symmetric monoidal category

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

[^5]:
    Precisely, the classifying category for the models of any 
    [algebraic theory][17] is always the opposite of the 
    category of the finitely generated free models.

    So, for instance, $\mathcal{A}^\text{op}$ is the full 
    subcategory of abelian groups spanned by 

    $$
    \{1, \mathbb{Z}, \mathbb{Z}^2, \mathbb{Z}^3, \ldots \}
    $$

    and $\mathcal{R}^\text{op}$ is the full subcategory of 
    (let's say commutative) rings spanned by 

    $$
    \{1, \mathbb{Z}[x], \mathbb{Z}[x,y], \mathbb{Z}[x,y,z], \ldots \}
    $$

    There's a similar version of this story that works for 
    [essentially algebraic theories][18] where we use the 
    finitely _presented_ models instead.

[^6]:
    I'm not going to tell you what that means, but here's an illustrative 
    example:

    An $E_1$-algebra in $\mathfrak{Cat}$ is a monoidal category. 

    An $E_2$-algebra in $\mathfrak{Cat}$ is a [_braided_][20] monoidal category. 
    That is, the multiplicative structure is commutative... but only up to a 
    homotopy (the braiding).

    An $E_3$-algebra in $\mathfrak{Cat}$ is a [symmetric][21] monoidal category.
    That is, a category whose multiplicative structure is _genuinely_ 
    commutative (at least, up to isomorphism, which is the best we ever 
    want to do in a category).

    All $E_n$-algebras for $n \geq 3$ are the same, since $\mathfrak{Cat}$ 
    is a $2$-category. There _aren't any_ interesting (read: nonidentity) 
    homotopies in dimension $\geq 3$, so if you're commutative up to a 
    higher homotopy, the only choice for that higher homotopy is the identity! 
    Which means you're just commutative without further qualification!

    But you can imagine that, for $\infty$-categories that do have higher 
    homotopies, we can have monoids that are commutative up to the data 
    of an $n$-homotopy, and that's exactly an $E_n$-algebra. In case you 
    want something that really is commutative, you can take $n=\infty$ here.
