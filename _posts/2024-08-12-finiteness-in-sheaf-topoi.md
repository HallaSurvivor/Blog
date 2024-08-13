---
layout: post
title: Finiteness in Sheaf Topoi
tags:
  - 
---

The notion of "finiteness" is constructively subtle in ways that can be 
tricky for people new to the subject to understand. For a while now I've 
wanted to figure out what's going on with the different versions of "finite" 
in a way that felt concrete and obvious (I mentioned this in a few older 
blog posts [here][1] and [here][2]), and for me that means I want to 
understand them inside a sheaf topos $\mathsf{Sh}(X)$. I've thought about this 
a few times, but I wasn't able to really _see_ what was happening until a few 
days ago when I realized I had a serious misconception about picturing 
bundles and etale spaces! In this post, we'll talk about that misconception, 
and spend some time discussing constructive finiteness in its most important 
forms.

As a short life update before we get started, I'm going to Denmark with 
[my advisor][7] to hang out with [Fabian Haiden][3]. We're going to be talking 
about all sorts of fun things related to my thesis work, mainly about 
[Fukaya Categories][4]. These fukaya categories can be _really_ scary when 
you first start reading about them, but in the special case of surfaces 
they're really not that bad! In the process of prepping for meeting Fabian, 
I've been writing a blog post that explicitly details what fukaya categories 
are, why you should care, and (for surfaces) how to compute them. I know I 
would have loved an article like this, and I'm excited to have one to share!
I'm also _finally_ going to finish my [qual prep series][5] from 
_three years ago_! Way back then I promised a post on fourier theory
that I never got around to, but I recently found a draft of that post! 
So it might not be 100% true to what I was studying back then, but it'll be 
as true to that as I can make it[^1].

With all that out of the way, let's get to it!

---

First, let's just recall the notions of finiteness you're likely to 
find in the literature[^2]:

If $n : \mathbb{N}$, the <span class=defn>Finite Cardinal</span> of size $n$ 
is the set $$[n] = \{ x : \mathbb{N} \mid x \lt n \}$$. 

A set $X$ is called <span class=defn>Bishop Finite</span> if it's (locally)
isomorphic to a cardinal. That is, if for some $n:\mathbb{N}$ we can prove 
$$\exists f : X \cong [n]$$.

A set $X$ is called <span class=defn>Kuratowski Finite</span> if it's 
(locally) the image of a cardinal. That is, if for some $n:\mathbb{N}$ we can prove
$$\exists f : [n] \twoheadrightarrow X$$.

A set $X$ is called <span class=defn>Subfinite</span> if it's (locally) a 
subobject of a cardinal. That is, if for some $n:\mathbb{N}$ we can prove 
$$\exists f : X \hookrightarrow [n]$$.

A set $X$ is called <span class=defn>Dedekind Finite</span> if every 
mono $X \hookrightarrow X$ is actually an iso. That is, if we can prove 
$$\forall f : X \hookrightarrow X . \exists g : X \to X . fg = 1_X \land gf = 1_X$$.


It's pretty obvious from these definitions that dedekind finiteness is 
a bit different from the others. This comes with pros and cons, but in my 
experience it's rarely the thing to consider. I'm including its definition 
more for cultural growth than anything, and I won't say anything more about 
it in this post[^3].

Also, notice we're putting an existential quantifier in front of everything. 
In the internal logic, this means that we're allowed to pass to an open cover 
of our base space and use a different $f$ on each open. If you prefer 
type theory[^4], you can replace every instance of $\exists$ by the 
[propositional truncation][9] of a $\Sigma$-type.

It's interesting to ask what the "untruncated" versions of these will be. 
I think that untruncated bishop finite types are exactly the cardinals, 
untruncated subfinite types are disjoint unions of propositions... But 
it's not clear to me what the untruncated kuratowski finite types should be.
Something like "kuratowski finite objects that aren't allowed to twist", 
but I don't quickly see a characterization of them[^5].

---

TODO: picturing cardinals (constant covering spaces. Draw some pictures. 
Relate this to the definition in the elephant). Note that you can have a 
different number of fibres over a different component!


TODO: picturing bishop finite sets 
(covering spaces with finite fibres. Draw some pictures.)

Bishop finite sets always have decidable equality. Show this 
informally by showing two sections have an open neighborhood where they're 
either totally the same or totally different. Then show this in the case 
of the double cover of the circle to show the equality relation is clopen. 

TODO: picturing k-finite sets 
(etale spaces with finite fibres. Draw some pictures. Skyscraper sheaf)

Say a few words about nonhausdorffness, and how this took you a while to 
appreciate. Discuss the connection to decidable equality, especially 
for the "circle with two origins". Show that a k-finite set with decidable 
equality is b-finite. Show how this is the quotient of a b-finite set. 

Also talk about $\{T,p\}$. Draw a picture. 

TODO: picturing subfinite sets 
(non-surjective covering spaces with finite fibres. Draw some pictures.)

These are decidable, but need not be a quotient of a b-finite set 
(since it doesn't have to be surjective onto the base space).


TODO?: Can we picture dedekind finite sets? I might just... not bother, haha.

---

Closure properties:

TODO: cardinals are closed under LOTS of stuff. Bishop finite are closed under 
some stuff. Kuratowski finite is closed under more stuff again...

Write these all out (it's on the nlab and in the back of the elephant) 
and make them obvious with some pictures.

---

TODO: which finite set to use?

Almost always, if you're just doing "regular math" you want to work with 
kuratowski finite sets. These admit a surjection from $[n]$, and so can be 
thought of as sets whose elements can be "listed" (possibly with repeats).

Note that we can't remove the repeats! For instance, in the circle 
with two origins, there's an epi from $\[2]$ which usually has duplicates,
but doesn't have duplicates at the doubled point!

The feature of finiteness we usually need is the ability to list stuff, 
and it normally doesn't matter if our list happens to have duplicates. So 
this gets the job done. Sometimes, though, especially in combinatorics, 
we need to be able to _distinguish_ between the objects we've listed. 

As long as we work with _decidable_ finite sets, we can do this and then 
everything is exactly as you would expect. This is part of why constructive math 
doesn't have much to say about combinatorics and algebra. Most arguments 
are _already_ constructive for decidable finite sets (which is what you're 
picturing when you picture a finite set). Sometimes you can push 
things a bit farther though, and this can be interesting. See, for instance, 
Blass's paper on the Pigeonhole Principle. 

TODO: link that.

TODO: mention that cardinals are projective, so satisfy a version of choice. 
Do any of the others? (k-finite definitely don't). Can you show this 
with a picture?

TODO: which of these are preserved by pullback along a geometric morphism?

TODO: If you're interested in reading more, the last section (D5) of 
Johnstone's Elephant is a _fantastic_ resource on finite objects in a topos. 

---

[1]: /2024/03/25/continuous-max-function.html
[2]: /2022/12/13/internal-logic-examples
[3]: https://semistability.wordpress.com/
[4]: https://ncatlab.org/nlab/show/Fukaya+category
[5]: /tags/analysis-qual-prep/
[6]: /tags/life-in-the-topological-topos/
[7]: https://sites.google.com/view/petersamuelson/home
[8]: https://doi.org/10.1016/0022-4049(87)90130-7
[9]: https://ncatlab.org/nlab/show/bracket+type


[^1]:
    And, of course, I still really want to finish the blog post on 
    2-categories and why you should care... There's just _so_ many 
    other things to think about and to write! It also feels like a 
    big topic because I have a lot to say, and that makes me a bit 
    scared to actually start. Especially since I've been writing a 
    lot of longer form posts lately (like the three part series on 
    the [topological topos][6], and I can tell the fukaya post is 
    going to be long too...)

[^2]:
    Here we're using the expected abbreviations. 

    We write $f : X \cong Y$ to mean $f : X \to Y$ and 
    $\exists g : Y \to X . gf = 1_X \land fg = 1_Y$.

    We write $f : X \hookrightarrow Y$ to mean $f : X \to Y$ and 
    $\forall x_1, x_2 : X . fx_1 = fx_2 \to x_1 = x_2$

    We write $f : X \twoheadrightarrow Y$ to mean $f : X \to Y$ and 
    $\forall y : Y . \exists x : X . fx = y$.

[^3]:
    If you want to learn more about it, I highly recommend 
    Stout's [_Dedekind Finiteness in Topoi_][8]. I don't know of a 
    good way to visualize the dedekind finite objects in $\mathsf{Sh}(X)$
    (though I haven't tried at all -- I want this to be a fast post) which 
    was another reason to exclude them.

[^4]:
    Which I often do, but not today.

[^5]:
    And again, I want this to be a quick post, finished within a day or 
    two of starting it, so I don't have the time to think about it at all.
    I would love for an enthusiastic reader to chime in, though!
