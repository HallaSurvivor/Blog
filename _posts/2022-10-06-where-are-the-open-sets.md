---
layout: post
title: Talk - Where Are The Open Sets? 
tags:
  - my-talks
---

I was invited to give a talk at [HoTTEST 2022][1], and was more than 
happy to accept! Ever since I was first learning [HoTT][3] I was curious how
we could be sure that theorems in HoTT give us corresponding theorems in
"classical" homotopy theory. Earlier this summer I spent a lot of 
time wrestling wtih $\infty$-categories (culminating in a series of 
[blog posts][2]) and I realized I was quite close to finally understanding
the connection between HoTT and classical topology. I think this is a 
question that should have a more accessible answer 
(the machinery is fairly intense, but that shouldn't prevent a high level overview)
and I'm happy I was able to help fill this gap!

All in all, I think the talk went quite well! I think I did a good job
making the broad ideas involved in the semantics accessible to an audience
without much background, though my actual delivery was a bit jittery -- 
I had to wake up at 7.30 to give the talk and I was basically being held up
by willpower and caffeine, haha.

<!-- As a secret life update, I got prescribed my hormones today as well! -->

Now that I've napped, let's write up a quick summary of the talk ^_^

---

The basic idea is to interpret the syntax of HoTT in the model category
of [simplicial sets][4] $s\mathsf{Set}$. This means that anything we do in
HoTT externalizes to a statement about $s\mathsf{Set}$. 
Then we use the quillen equivalence of $s\mathsf{Set}$ with $\mathsf{Top}$[^1] in 
order to transfer our statement in $s\mathsf{Set}$ to a statement about 
$\mathsf{Top}$ (up to homotopy).

First, I spent some time discussing (_very_ roughly) what a model structure
on a category is. As a reference for a less rough idea, I mentioned a famous
paper [_Homotopy Theories and Model Categories_][5] by Dwyer and Spalinski.
Next, I gave some intuition for what a simplicial set might be, and outlined how 
they combinatorially encode topological spaces. For more detailed references
I mentioned Friedman's [_An Elementary Illustrated Introduction to Simplicial Sets_][6]
as well as Singh's thesis [_A Survey of Simplicial Sets_][7].

Then came a discussion of the functors converting back and forth between 
$s\mathsf{Set}$ and $\mathsf{Top}$:

 - [geometric realization][10], $\lvert \cdot \rvert : s\mathsf{Set} \to \mathsf{Top}$
 - [singular chains][9], $\text{Sing}(\cdot) : \mathsf{Top} \to s\mathsf{Set}$

these form an adjunction ($\lvert \cdot \rvert \ \dashv \ \text{Sing}(\cdot)$)
which respects the model structure on both categories in the sense that they
form a [quillen equivalence][11]: 

<div class=boxed markdown=1>
1. They induce functors on the homotopy categories
 - $\mathbb{L} \lvert \cdot \rvert : s\mathsf{Set}[\mathcal{W}^{-1}] \to \mathsf{Top}[\mathcal{W}^{-1}]$
 - $\mathbb{R}\text{Sing}(\cdot) : \mathsf{Top}[\mathcal{W}^{-1}] \to s\mathsf{Set}[\mathcal{W}^{-1}]$
2. $\mathbb{L} \lvert \cdot \rvert$ and $\mathbb{R} \text{Sing}(\cdot)$ 
form an adjoint equivalence $s\mathsf{Set}[\mathcal{W}^{-1}] \simeq \mathsf{Top}[\mathcal{W}^{-1}]$
</div>

The punchline is that _any_ question[^2] we have about the homotopy theory of
topological spaces can be answered by transporting to $s\mathsf{Set}$ and
answering the question there[^3]!

This is great news for two reasons: 

 - Concretely, simplicial sets are combinatorial, so we can describe many 
   interesting simplicial sets to a computer with only a finite amount of data.
   This is the backbone of most implementations of algebraic topology -- 
   see [here][14], for instance.

 - Abstractly, simplicial sets assemble into a (grothendieck) [topos][15],
   which gives us access to lots of heavy duty category theoretic machinery
   when working with them.

Speaking of heavy duty category theoretic machinery, this marked the end of 
section $1$ of the talk. Section $2$ is about the interpretation of HoTT 
in $s\mathsf{Set}$, and there's a notable spike in vagueness here. 
Unfortunately the math becomes quite a bit more technical
(and involves a lot of category theory I didn't want to assume of the 
audience) but I still wanted to give a flavor for externalizing 
HoTT statements into statements about $s\mathsf{Set}$. That means I 
wasn't able to give many details at all[^4], but I still tried to
roughly sketch the ideas involved.

Again, I pointed to the literature for those who want to see things 
more precisely. There's an excellent set of three talks by [Emily Riehl][16],
_On the $\infty$-Topos Semantics for Homotopy Type Theory_
(lectures [1][17], [2][18], and [3][19]), as well as associated 
[lecture notes][20]. They do a good job motivating the semantics
in any $\infty$-topos (as the title suggests) at the cost of being
somewhat more abstract. There's also a paper 
([_The Simplicial Model of Univalent Foundations (After Voevodsky)_][21],
by Kapulkin and Lumsdaine) which works only for $s\mathsf{Set}$,
but is much more concrete. I forgot to mention it during the talk,
but [Subramaniam's talk][23] in the HoTTEST Summer School Colloquium is
another fantastic resource.

Morally, the idea is that types in HoTT are [kan complexes][22]
(that is, simplicial sets which are "honestly geometric" in some sense).
Then constructions on types externalize to (categorical) constructions 
on kan complexes, and terms inhabiting a type correspond to global points
of the associated kan complex.

This is a bit of a fib, since the syntax of HoTT is strict on-the-nose
whereas the categorical constructions we do in $s\mathsf{Set}$ are only 
defined up to isomorphism. It turns out that this is a serious technical 
obstruction, since we need to _choose_ a particular object from each 
isomorphism class in order to interpret the syntax. But we need to do this
in a way that the constructions are all compatible. 

For instance, say $P$ is a dependent type over $B$ and $f : A \to B$ 
is a function. Then if $a : A$ we could first evaluate $f(a)$ then 
consider the type $P(f(a))$, _or_ we could first compose $P$ with $f$ 
to get a type family $P(f(-))$ over $A$, then take the fibre at $a:A$.

No matter what, we end up with the syntax $P(f(a))$[^5], so we get 
literal equality at the level of syntax. 

However, in $s\mathsf{Set}$ if we _choose_ a representative for each
isomorphism class, and define our constructions to manipulate those 
specific objects, it's possible that we chose poorly so that we end up
with _different objects_ depending on which order we choose to perform
the above substitutions 
(they'll be isomorphic of course, but this is not good enough).

The key to solving this issue is to somehow make _one_ really hard 
choice, then define all of our other choices in terms of it! This is 
the idea behind Voevodsky's _(weak) universal fibration_, which you can
read all about in the linked paper of Kapulkin and Lumsdaine.

Lastly, I mentioned a good exercise to keep in mind when trying to learn
this material: 

<div class=boxed markdown=1>
Can you show that if HoTT proves $\mathtt{isContr}(A)$ is 
inhabited, then $$[ \! [ A ] \! ]$$ (the kan complex that $A$ denotes) is 
contractible in the sense of simplicial sets? 

After this, can you show that
the geometric realization $$\lvert [ \! [ A ] \! ] \rvert$$ is contractible too?

If you can do both of the above exercises, you'll have successfully proven 
a fact about an honest topological space by proving some theorem in HoTT!
</div>

---

All in all, I was pleased with how the talk went, and I learned a _ton_
while writing it! I still have to work through the details of the 
semantics to fully feel comfortable externalizing HoTT statements,
but I have a much more nuanced appreciation for the issue of 
strictness.

As usual, here's the title, abstract, and recording. 

Take care, all ^_^

---

Where Are The Open Sets? -- Comparing HoTT with Classical Topology

It's often said that Homotopy Type Theory is a synthetic description of 
homotopy theory, but how do we know that the theorems we prove in HoTT are true 
for mathematicians working classically? In this expository talk we will outline 
the relationship between HoTT and classical homotopy theory by first using the 
simplicial set semantics and then transporting along a certain equivalence 
between (the homotopy categories of) simplicial sets and topological spaces. 
We will assume no background besides some basic knowledge of HoTT and 
classical topology.

You can find the slides [here][24], and I'll post the recording as 
soon as it's up.

**Edit:** 

Here's the recording ^_^

<iframe width="560" height="315" src="https://www.youtube.com/embed/syftUuf5Hpk" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

---

[^1]:
    With their usual model structures

[^2]:
    Well, any question that transports along categorical equivalences...
    But that means every question we can phrase categorically! 

    This is part of the reason so many category theorists get a bit
    obsessive about phrasing everything in terms of category theoretic
    jargon. It's not _just_ to make life hard for people who don't 
    know the lingo (even though it might feel that way), nor is it 
    _just_ to help us organize our own thoughts and relate different 
    constructions to each other (though that's a big part of it). 
    One big reason to go through with the endeavor is to be able to
    transport as many things as possible across an equivalence of categories,
    and things phrased in a categorical language are _automatically_ 
    invariant under these equivalences!

[^3]:
    In the questions and discussion after the talk, [Dan Christensen][12]
    mentioned an important point: This equivalence goes much deeper than
    just the homotopy categories. In fact, we get an equivalence of 
    $\infty$-categories between the [simplicial localizations][13]
    of $\mathsf{Top}$ and $s\mathsf{Set}$ at their weak equivalences,
    which tells us that much more homotopical structure is preserved by 
    this translation! For instance, the _mapping spaces_.

    On the one hand, this is great (since it means our translation is 
    _even better_ than my talk lets on) and necessary (since this higher
    structure is useful when working with the semantics of HoTT in 
    $s\mathsf{Set}$). 

    On the other hand, it requires one to say the words "$\infty$-category",
    which I was trying to avoid for concreteness reasons 
    (and because I'm less comfortable with them). 

    I figured I would mention it here, though, since it's a lot easier to 
    have footnotes and asides in a blog post than in a talk ^_^.

[^4]:
    Though this ended up being good for time-management reasons as well.
    My talk was basically 30 minutes on-the-nose, which I'm pretty pleased 
    with to be honest. It was pretty ambitious, and I'm glad I managed to 
    stay on time!

    This was also good because I'm less comfortable with the
    translation from HoTT into $s\mathsf{Set}$, and glossing over details
    saved me from accidentally saying something false.

[^5]:
    Or, if you want to be _extremely_ precise, $P([f[a/x]/b])$.


[1]: https://www.uwo.ca/math/faculty/kapulkin/seminars/hottest.html
[2]: /tags/homotopy-theories/
[3]: https://en.wikipedia.org/wiki/Homotopy_type_theory
[4]: https://en.wikipedia.org/wiki/Simplicial_set
[5]: https://math.jhu.edu/~eriehl/616-s16/DwyerSpalinski.pdf
[6]: https://arxiv.org/pdf/0809.4221.pdf
[7]: https://www.abdn.ac.uk/staffpages/uploads/r01gs19/Gyan_Singh_sSet.pdf
[8]: https://ncatlab.org/nlab/show/geometric+realization#idea
[9]: https://kerodon.net/tag/001Q
[10]: https://kerodon.net/tag/001X
[11]: https://ncatlab.org/nlab/show/Quillen+equivalence
[12]: https://jdc.math.uwo.ca/
[13]: https://ncatlab.org/nlab/show/simplicial+localization
[14]: https://doc.sagemath.org/html/en/reference/topology/index.html
[15]: https://en.wikipedia.org/wiki/Topos
[16]: https://math.jhu.edu/~eriehl/
[17]: https://www.youtube.com/watch?v=PejZfl5kOlU
[18]: https://www.youtube.com/watch?v=m2_ObHxDcQs
[19]: https://www.youtube.com/watch?v=hcGKmEuJJMY
[20]: https://emilyriehl.github.io/files/semantics.pdf
[21]: https://arxiv.org/pdf/1211.2851.pdf
[22]: https://ncatlab.org/nlab/show/Kan+complex
[23]: https://www.youtube.com/watch?v=NpzqeZd4Yw0
[24]: /assets/docs/where-are-the-open-sets/slides.pdf
