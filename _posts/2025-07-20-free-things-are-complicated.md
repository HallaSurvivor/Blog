---
layout: post
title: Free Things Are Complicated (Especially the Sphere Spectrum!)
tags:
  - 
---

I've spent the last week at [CT2025][1], which has just come to a close. 
It was great getting to see so many old friends and meet so many new ones,
and every time I go to a CT I'm reminded of *just* how much category theory 
there is in the world, as well as *just* how much I enjoy all of it! Right 
before this I was in Antwerp for some [Noncommutative Geometry][2], 
where I learned a *ton* and met even *more* new friends! Then next week
I go to Bonn for my [*third* conference][3] in a row. 
I'm trying to stay energetic, and thankfully I have a few days off between CT 
and QTMART to help me rest up!

I want to write up a lot of things I learned over the last month, since I have 
a *lot* of new thoughts on noncommutative geometry, mirror symmetry, and 
deformation theory, all coming from just my time in Antwerp! I've also learned 
a lot at CT and talked to a lot of interesting people about interesting 
things, and I'm sure I'll have even more to say after my time in Bonn.

I think organizing all of those thoughts are going to take a while, though 
(if I end up writing them down at all), but today I have a quick observation 
inspired by a few lovely conversations I had with [Clark Barwick][4] at CT. 
One of the many questions I asked him was if there's a conceptual reason the 
[Sphere Spectrum][5] (read: the homotopy groups of spheres) is so darn 
complicated. He gave me an answer that's obvious in hindsight, but which 
totally rearranged the way I think about things:

<blockquote>
The Sphere Spectrum is complicated because it's *free*
</blockquote>

I think I internalized a while ago that "free" constructions are fairly 
concrete. After all, you look at the syntax of whatever object you're interested 
in, quotient out by the relations you want to be true and you're done! Plus,
mapping out of a free thing is as simple as possible, since it's a left 
adjoint! All you have to do is find a (usually simpler) map from your 
generating set to a structure of interest and let the magic of category theory 
build your (usually more complicated) map for you...

Of course, this view is heavily influenced by the kind of free structures 
I have experience with, and the kinds of questions I was asking about them.
I was thinking about free groups and monoids, which you can study with 
word combinatorics, free (dg-)algebras on (graded) vector spaces, 
which look like polynomials,
free categories on graphs, free $k$-linear or dg-categories on categories, 
and free [cauchy completions][17] of these, all of which come from just 
looking at paths, linear combinations, concentrating things 
in degree $0$, or working with twisted closures to add shifts and 
cones and whatnot[^6].
I was thinking about relatively free constructions like the universal 
enveloping algebra, with its [PBW-basis][18], or the right angled artin group 
attached to a (reflexive, simple) graph... All of these constructions feel 
like friends to me, in part because I know how to compute with them.
Why would the sphere spectrum -- the free spectrum on a *single point* -- 
be so different?

The point is that I've internalized these constructions as being tractable 
because I'm usually mapping *out* of them, in the direction the 
category theory encourages. I'm also usually relying on serious 
"normal form" theorems that make computing with these things tractable,
or I'm doing fairly simple combinatorics with my generating set
before arguing that these extend in some obvious way
to things defined on the whole free object. All of these constructions 
become much less friendly when you start mapping *into* them, or asking more 
difficult questions about their internal structure. In hindsight, I've even 
personally struggled with *tons* of questions about free structures in my 
research! 

Free groups are extremely interesting from basically any perspective, with 
deep questions about their first order theory ([Tarski's Problem][6]), the 
combinatorics relating their generating sets ([The Andrews-Curtis Conjecture][7]),
or the coarse geometry of their outer automorphisms.

Free cauchy completions are *obviously* complicated when you want to understand 
them on their own terms! If you take an algebra $A$ and view it as a one-object 
dg-category, then its cauchy completion[^6] is its whole category of 
[perfect complexes][8]! An *enormous* chunk of representation theory is, 
in that lens, dedicated to nothing more than the study of a certain, 
complicated, free construction!

I've personally given up[^1] on a problem about relatively free constructions 
in right angled artin groups! These interpolate between free and free-abelian 
groups, and geometric group theory is teeming with interesting open problems 
about raags. For instance, can you understand, at the level of the underlying 
graphs, when one raag will embed into another? I thought about this off and on 
for a year before I started working seriously with my current advisor, and 
I made almost no progress at all.

I also spent some time working with the adjunctions

$$
\{ \text{finite limit categories} \} 
\leftrightarrows
\{ \text{finite product categories} \}
\leftrightarrows
\{ \text{symmetric monoidal categories} \}
$$

It's interesting to try and construct these explicitly, and to understand 
the essential images of the left adjoints. This amounts to understanding 
which essentially algebraic theories are actually algebraic, and which 
algebraic theories are actually [props][9]. One of the big difficulties 
here is that we have a relatively free construction which adds *relations*
rather than just *operations*. Adding new operations tends to be a 
fairly mild thing to do -- consider the free algebra on an abelian group,
which sends $A$ to its tensor algebra $\bigoplus_n A^{\otimes n}$ where 
it's easy to recover the $A$ you started with. If instead we want to add 
new relations or axioms, for instance by freely sending a group $G$ to its
abelianization $G \big / [G,G]$, then we lose lots of information in this 
construction.

After some conversations with John Baez and Todd Trimble I came quite close to 
characterizing the image of the left adjoint between finite product categories 
and symmetric monoidal categories by factoring it into a "lossy" construction 
adding new axioms forcing the monoidal unit to be terminal 
and a much simpler construction which freely adds new operations corresponding
to the product projections. I've had to put that project on hold while I 
focus on my thesis work, but I *really* want to come back and finish it soon.

<br>

Of course as soon as you're interested in logic, you have to accept that 
free things are complicated! The freest version of any theory lives in its 
classifying category, where truth and provability coincide. Then proving 
anything at all about the free model gives immediate understanding about 
*all other models* of that theory! This is already true for groups, 
whose classifying finite-product category is just the category of 
finitely generated free groups and homomorphisms.
We don't usually think about it because the kinds of 
statements you prove in equational logic aren't very deep. But if you look 
instead at the classifying topos for groups and ask 
*geometric* questions suddenly you're able to do a lot more, and the game 
becomes *much* harder!

Perhaps this is clearest in the semantics of programming languages, where 
the free model (often called the "term model" in this context[^2]) *is*
the programming language, and checking whether two terms are equal in this 
free model *literally* amounts to evaluating two programs and seeing if their
respective values agree. Because of this, many important structural results 
about a programming language (such as [canonicity][10]) can be proven by 
building another model whose semantics you understand, and then producing a 
section of the unique map from the free model.

Also coming from logic are various lattices, whose free models can be 
quite intricate. Famously the free [modular lattice][11] on $3$ generators 
has $28$ elements, while the free modular lattice on $4$ generators is 
infinite! Indeed, this lattice has an undecidable word problem[^3], so that 
no program can tell whether two descriptions of its elements are the same 
or not! Heyting algebras are extremely important for semantics of 
intuitionistic logic, yet already the free heyting algebra on *one* generator
is infinite, and the free heyting algebra on *two* generators is famously 
complicated. The study of free heyting algebras is still ongoing and seems 
quite difficult (at least as an outsider). See, for instance, Almeida's 
recent preprint [_Colimits and Free Constructions of Heyting Algebras 
through Esakia Duality_][13].

<br>

With all this in mind, it shouldn't be surprising at *all* that the 
sphere spectrum is so complicated! It's the free [spectrum][15] on a point, 
and as such the only "relations" it will have are those that hold in 
*all spectra*! But of course spectra should *obviously* be complicated -- 
They control all possible (co)homology theories for all spaces! So in this 
sense one should expect the internal structure of the sphere spectrum to be 
quite complicated, since any simplification would persist to something true 
of all cohomology theories.

Of course, it's easy to be complicated without being interesting, and 
I still think it's a bit of a miracle that the sphere spectrum should have 
all this intricate structure inside it. As I understand it, 
much of [Chromatic Homotopy Theory][16] came from trying to explain patterns 
in the homotopy groups of spheres, and this subject is now as famously 
intimidating to outsiders[^4] as it is famously fascinating once you put in 
the work to become an insider[^5].

---

Thanks for reading all! This really was a quick one for once, since I already
had a lot of these examples floating around in my head. I really had all 
of the tools to realize that free things are *obviously* complicated in 
general, *especially* their "internal structure" that doesn't ride the 
coattails of the universal property, but for some reason I just didn't 
put it together until my conversation with Clark.

It's always dangerous to say what I'm thinking about writing about, but 
I at least have one more short post planned from my time in Antwerp, and 
maybe a longer one too if I have the energy. I'm doing a *ton* of writing 
right now, since I have two half-finished papers that I want to submit by the 
end of the summer. I think I'll be able to get it done, but between writing 
these and going to conferences it's been a tiring month. It's tiring in a fun 
way, though, and I really feel like I've been productive in a way that I 
haven't felt in a little while. I'm excited to start crossing a lot of these 
projects off my long-term-todo-list, especially since I already have three 
more projects I want to start!

Regardless, I hope you're having a more restful summer than I am! 
Stay safe, all, and we'll talk soon ^_^.

<p style="text-align:center;">
<img src="/assets/images/free-things-are-complicated/Brno-with-bear.jpg" width="50%">
</p>

<p style="text-align:center;" markdown=1>
(photo by the amazing [Emily Roff][20], taken at the top of the main 
tower in Brno)
</p>


---

[1]: https://conference.math.muni.cz/ct2025/
[2]: https://www.slmath.org/summer-schools/1077
[3]: https://www.mathematics.uni-bonn.de/hcm/events/workshops-conferences/qtmart_2025
[4]: https://webhomes.maths.ed.ac.uk/~cbarwick/
[5]: https://en.wikipedia.org/wiki/Sphere_spectrum
[6]: https://en.wikipedia.org/wiki/Free_group#Tarski's_problems
[7]: https://en.wikipedia.org/wiki/Andrews%E2%80%93Curtis_conjecture
[8]: https://en.wikipedia.org/wiki/Perfect_complex
[9]: https://ncatlab.org/nlab/show/PROP
[10]: https://ncatlab.org/nlab/show/canonical+form
[11]: https://en.wikipedia.org/wiki/Modular_lattice
[12]: https://golem.ph.utexas.edu/category/2015/09/the_free_modular_lattice_on_3.html
[13]: https://arxiv.org/pdf/2402.08058v3
[14]: https://www2.mathematik.tu-darmstadt.de/~herrmann/houston.pdf
[15]: https://en.wikipedia.org/wiki/Spectrum_(topology)
[16]: https://en.wikipedia.org/wiki/Chromatic_homotopy_theory
[17]: https://ncatlab.org/nlab/show/Cauchy+complete+category#InEnrichedCategoryTheory
[18]: https://en.wikipedia.org/wiki/Poincar%C3%A9%E2%80%93Birkhoff%E2%80%93Witt_theorem
[19]: http://www.tac.mta.ca/tac/volumes/37/28/37-28.pdf
[20]: https://webhomes.maths.ed.ac.uk/~emilyroff/

[^1]:
    At least for now

[^2]:
    Pun intended

[^3]:
    Which is made more interesting by the fact that if you look at the 
    class of lattices coming from lattices of subgroups of abelian groups,
    the corresponding free lattice on $4$ generators *does* have solvable 
    word problem!

    This is remarkable since (as I understand it) 
    modular lattices are called that because they 
    look like lattices of submodules (in particular, sublattices 
    of a lattice of subgroups of an abelian group).

    This is apparently proven in Herrmann's 
    [_On the Equational Theory of Submodule Lattices_][14], and I learned all this 
    from Ralph Freese the comments of [this][12] n-Category Cafe post.

[^4]:
    Such as myself.

[^5]:
    Which it seems like I might start doing soon, for a project I'm not ready
    to talk about yet.

[^6]:
    Actually it's not *completely* obvious to me that the cauchy completion
    of a dg-category should be its idempotent triangulated closure... The 
    cauchy completion will certainly be idempotent complete and triangulated,
    but in the well-named paper 
    [_Cauchy Completeness for DG-Categories_][19], Nicolić, Street, and 
    Tendas show that to be cauchy complete you also need to be closed under 
    "cokernels of protosplit chain maps"... I think this is some kind of 
    split idempotent condition? But I haven't read the paper closely enough 
    to know for sure.

    If you want to be guaranteed to be correct, instead of "cauchy completion" 
    you can say "the idempotent closure of the twisted closure". That's still 
    a free construction and it still gives you the derived category in the 
    special case your dg-category is a ring.

