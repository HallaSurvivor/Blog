---
layout: post
title: Talk -- What is Factorization Homology?
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
with the people I went out for lunch (and later, drinks) with!

I was nervous at first, since Florida... isn't politically friendly 
towards trans people. Thankfully everybody that I interacted 
with was lovely, and I didn't have any issues at all. What's more,
the campus was _beautiful_, and the surrounding area was 
surprisingly walkable. We had a _4 hour_ lunch break on the first 
day (which is part of how I got so close with my lunch group), 
and after we ate some great barbecue we all hung out under 
some fantastic trees.

I also felt safer because I was hanging out with [Kaya Arro][2], 
a postdoc at UCR, for basically the whole time. They were great 
company, and also helped a ton with silly homotopy questions 
while I was making my slides (on the day before the talk...).

Anyways here are some of the trees _right_ outside the conference building[^7]!

<p style="text-align:center;">
<img src="/assets/images/ams-sectional-talk-fh/fsu-trees.jpg" width="50%">
</p>

It was like $400 cheaper to fly out on Monday evening, even 
though the conference ended on Sunday, so Kaya and I had 
almost a whole day to ourselves. We went to the FSU 
[Museum of Fine Arts][3] and walked around until it was 
airport time. 

It was the _perfect_ size museum for the amount of time we had, with 
some amazing installation pieces, and a whole section dedicated to 
book making! That was particularly exciting for me, since one of my 
best friends, [Ashley Chan][22], is a super talented book maker!

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

There were some great questions after the talk, including one 
from [Philip Hackney][5] 
(one of the organizers, and the person who invited me) which 
gave me the chance to talk about what factorization homology 
has to do with my research.

All in all, I think the talk went super well. I don't think I 
came off as particularly manic, which can happen when I give 
short talks, and it seems like people were able to take some 
intuition away, which is everything I wanted! It helps that 
everyone at the conference was super nice, so I didn't have to 
worry at all about being judged or grilled. I think people were 
in a _particularly_ good mood, since I was the first talk after 
lunch, so everyone was full and happy, haha.

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
[eilenberg-mac lane space][7] $K(A,n)$[^2]. That is, 
with the set of maps up-to-homotopy $X \to K(A,n)$.

This encourages a rather broad perspective, which says 
that we can think of $\pi_0 \text{Map}(X,Y)$ as the 
"cohomology of the space $X$ with coefficients in the space $Y$". 
This is sometimes called [nonabelian cohomology][8], and 
many cohomology theories can be subsumed by this one 
(basically because lots of algebraic and topological things 
can be seen as spaces! See [here][9], for instance).

If we're calling this thing cohomology, it's natural to ask 
which "classical" theorems in cohomology are true in this 
setting. And one natural theorem to want is [Poincaré Duality][10].

One motivation for factorization homology is that it's the 
right homology theory to make this "Nonabelian Poincaré Duality" 
true!

In the talk I said some words about this, but online there's no 
need for me to say anything. If you're interested, you should 
just go read [Lurie's notes on the topic][11] instead. After all, 
I basically just paraphrased them in the talk!

If you insist on sticking around here, though, the idea is this:

To prove the "classical" poincaré duality $H_i(X,A) \cong H^{n - i}_c(X,A)$,
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

Now, if we _wanted_ to cook up a homology theory making 
some kind of "nonabelian poincaré duality" true, we might 
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
\emptyset, \quad
\mathbb{R}^n, \quad 
\mathbb{R}^n \coprod \mathbb{R}^n, \quad
\mathbb{R}^n \coprod \mathbb{R}^n \coprod \mathbb{R}^n, \quad \ldots
$$

we're able to get the job done[^4]!

So then, we've found ourselves with a functor defined on 
$$\mathcal{D}_n$$ -- the category of disjoint unions of $\mathbb{R}^n$s 
with smooth embeddings. Then we _freely extend_ this functor 
to the whole category of manifolds $\mathcal{M}\text{an}_n$ by 
defining the functor to be "compatible with gluing". The keyword 
here is [left kan extension][14].

If you're me, this feels a _whole_ lot like a familiar story 
from categorical logic!

This, of course, is all part of the _what_!

At this point in the talk I took a quick diversion to remind 
people about [Functorial Semantics][15]. This was extra easy
since in the morning session [Valentina Zapata Castro][16] spent some time 
talking about the lawvere theory for monoids!

<br>

In (1-categorical) functorial semantics, we have _classifying categories_ 
associated to algebraic theories. Then a model of that 
theory is "just" a functor from the classifying category to 
$\mathsf{Set}$. For instance, the classifying category $\mathcal{A}$ 
for abelian groups looks like this[^5]:

<p style="text-align:center;">
<img src="/assets/images/ams-sectional-talk-fh/A-cat.png" width="50%">
</p>

and the classifying category for rings $\mathcal{R}$ is:

<p style="text-align:center;">
<img src="/assets/images/ams-sectional-talk-fh/R-cat.png" width="50%">
</p>

Indeed, a finite product functor $\mathcal{A} \to \mathsf{Set}$ 
has to send $1$ to some set $A$. Then, since it's product preserving, 
it has to send $2$ to $A^2$, and $0$ to $A^0 = \{ \star \}$. Then 
the indicated maps get sent to honest operations on $A$, which give us 
the desired abelian group structure on $A$.

Note that we have an embedding $j : \mathcal{A} \hookrightarrow \mathcal{R}$.

Now any ring $R$ is a (finite product) functor 
$\mathcal{R} \to \mathsf{Set}$, and if we _restrict_ along $j$ 
we get a new finite product functor $\mathcal{A} \to \mathsf{Set}$. 
That is, we get an abelian group! It should be believable that this is 
the underlying abelian group of the ring we started with!

<p style="text-align:center;">
<img src="/assets/images/ams-sectional-talk-fh/res.png" width="50%">
</p>

More excitingly, can we go the other way? Given a functor 
$\mathcal{A} \to \mathsf{Set}$ (that is, an abelian group) 
is there a way to freely _extend_ this functor to one defined 
on all of $\mathcal{R}$? 

<p style="text-align:center;">
<img src="/assets/images/ams-sectional-talk-fh/exn.png" width="50%">
</p>

The answer, of course, is _yes_ and it's given by 
left kan extension! This recovers the usual free ring on an 
abelian group $A$.

<br>

Primed with this context, let's look at our definition of 
factorization homology again:

We have a (symmetric monoidal) functor $$\mathcal{D}_n \to \mathcal{C}$$.
This data is actually quite well studied, since it's a model for 
[$E_n$-algebras][19] in $\mathcal{C}$. These are monoids in $\mathcal{C}$ 
that are "commutative up-to-homotopy living in dimension $n$"[^6].

So we have something that looks like some kind of algebra, which is 
given by a functor out of $$\mathcal{D}_n$$. Then we want to _freely extend_ 
this data to a new kind of algebra, given by a functor out of 
$\mathcal{M}\text{an}_n$... 

Doesn't this setup sound familiar?

If $$A : \mathcal{D}_n \to \mathcal{C}$$ is our $E_n$-algebra, 
We define $\int_{(-)} A : \mathcal{M}\text{an}_n \to \mathcal{C}$,
the <span class=defn>Factorization Homology</span> to be the 
left kan extension of $A$ along $j$. We can think of this as a kind of 
"algebra" which is graded by connected manifolds. Moreover, we have 
operations between these graded pieces corresponding to smooth embeddings!

For instance, if $i : M_1 \coprod M_2 \to N$ is a smooth embedding, then 
we get an operation $\int_{M_1} A \otimes \int_{M_2} A \to \int_N A$.

In particular, for a <span class=defn>Collared Manifold</span> 
(that is, a manifold of the form $M = M_0 \times \mathbb{R}$) we get 
an algebra structure $\int_M A \otimes \int_M A \to \int_M A$ 
from the embedding

<p style="text-align:center;">
<img src="/assets/images/ams-sectional-talk-fh/algebra.png" width="50%">
</p>

Similarly, if $M$ embeds into $N$, then we get a $\int_M A$-module structure on 
$\int_N A$:

<p style="text-align:center;">
<img src="/assets/images/ams-sectional-talk-fh/module.png" width="50%">
</p>

This brings us to the most important part of the _How_:

We can actually compute factorization homology by using "collared excision":

<p style="text-align:center;">
<img src="/assets/images/ams-sectional-talk-fh/excision.png" width="50%">
</p>

If you want to read more about all of this, I _highly_ recommend 
the relevant section in [Juliet Cooke][30]'s [Thesis][28]. If you want to 
really understand it well, there's also Alaya and Francis's 
[_Factorization Homology Primer_][29] and [Hiro Lee Tanaka][31]'s 
excellent lectures on the subject, which are available on [youtube][32].

---

Thanks again for reading, all! I'm really pleased with how this talk went,
and I'm happy to have made as many friends as I did at the conference.

It was great to be invited to speak in person somewhere for the first time, 
and to feel super welcomed in the homotopy theory world 
(which I'm only tangentially a part of... at least for now).

Stay safe, all, and we'll talk soon!

---

What is Factorization Homology?

Ayala, Francis, and Rozenblyum introduced Factorization Homology in order to 
compare category theory and (topological quantum) field theory. It has since 
grown into a useful invariant of surfaces and algebras which, 
through excision, is often computable in practice. In this survey talk we 
will discuss the basics of factorization homology, emphasizing its connections 
to both homotopy theory and category theory (via infinity categories). 
Given time, we will also discuss some applications to the speaker’s ongoing 
dissertation work in skein theory.

The talk wasn't recorded, but you can find the slides [here][33].

<p style="text-align:center;">
<img src="/assets/images/ams-sectional-talk-fh/me.jpg" width="50%">
</p>

---

[1]: https://www.ams.org/meetings/sectional/2313_program_ss13.html
[2]: https://kayaarro.site/
[3]: https://mofa.fsu.edu/
[4]: https://ncatlab.org/nlab/show/factorization+homology
[5]: http://phck.net/
[6]: https://ncatlab.org/nlab/show/compact-open+topology
[7]: https://en.wikipedia.org/wiki/Eilenberg%E2%80%93MacLane_space
[8]: https://ncatlab.org/nlab/show/nonabelian+cohomology#NonabelianSheafCohomology
[9]: https://ncatlab.org/nlab/show/Dold-Kan+correspondence
[10]: https://en.wikipedia.org/wiki/Poincar%C3%A9_duality
[11]: https://www.math.ias.edu/~lurie/282ynotes/LectureVIII-Poincare.pdf
[12]: https://en.wikipedia.org/wiki/Cosheaf
[13]: https://en.wikipedia.org/wiki/Mayer%E2%80%93Vietoris_sequence#Basic_versions_for_singular_homology
[14]: https://en.wikipedia.org/wiki/Kan_extension
[15]: https://ncatlab.org/nlab/show/Lawvere+theory
[16]: https://math.virginia.edu/people/vz6an/
[17]: https://ncatlab.org/nlab/show/algebraic+theory
[18]: https://ncatlab.org/nlab/show/essentially+algebraic+theory
[19]: https://ncatlab.org/nlab/show/En-algebra
[20]: https://en.wikipedia.org/wiki/Braided_monoidal_category
[21]: https://en.wikipedia.org/wiki/Symmetric_monoidal_category
[22]: https://www.ashleyjchan.com/stories
[23]: https://ncatlab.org/nlab/show/complex+projective+space
[24]: https://mathoverflow.net/questions/308253/classification-of-line-bundles-by-second-cohomology-of-a-manifold
[25]: https://arxiv.org/abs/math/0501094
[26]: https://mathoverflow.net/questions/450835/what-is-the-motivation-for-infinity-category-theory
[27]: /2023/11/14/ctoctoberfest2023.html
[28]: https://julietcooke.net/CookeThesis.pdf
[29]: https://www3.nd.edu/~stolz/2021S_Math80440/2019_Ayala_Francis.pdf
[30]: https://julietcooke.net/
[31]: https://www.hiroleetanaka.com/
[32]: https://www.youtube.com/watch?v=yeTngpqaAmk
[33]: /assets/docs/ams-sectional-talk-fh/slides.pdf

[^1]:
    Though honestly, I view _most_ things through the lens of either 
    categories or logic. So this should come as no surprise, haha.

[^2]:
    If you haven't seen this before, it's a _super_ useful perspective 
    to have on hand! For example, [$\mathbb{C}P^\infty$][23] is both 
    a model for $K(\mathbb{Z},2)$ and $BU(1)$.

    Now (homotopy classes of) maps $X \to K(\mathbb{Z},2)$ are the same 
    thing as elements of $H^2(X,\mathbb{Z})$ by the fact from the main 
    post.

    But homotopy classes of maps $X \to BU(1)$ are the same thing as 
    complex line bundles on $X$! 

    So, since these spaces are the same, we learn that complex line 
    bundles on $X$ are classified by $H^2(X,\mathbb{Z})$!

    You can read more about this [here][24], for instance.

[^3]:
    This is one _killer_ example of why people care about this kind 
    of abstract nonsense. Not only do we need to know stuff about 
    (co)sheaves, we also have to care about $\infty$-categories! 

    This is basically because $\infty$-categorical things tend to 
    glue more nicely than $1$-categorical things. _This_, in turn, 
    is related to the idea that "Chain Complex: Good. Homology: Bad",
    as talked about in many places. (for instance, [here][25] and 
    [here][26])

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

    We've talked a bit about this on the blog [before][27], and I 
    have plans to talk quite a bit about it sometime in the future.

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

[^7]:
    The hilariously named "HCB" (Huge Classroom Building).
