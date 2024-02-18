---
layout: post
title: Internal Group Actions as Enriched Functors
tags:
  - 
---

Earlier ~~today~~ this month on the [Category Theory Zulip][1], Bernd Losert asked an 
extremely natural question about how we might study topological group 
actions via the functorial approach beloved by category theorists. 
The usual story is to treat a group $G$ as a one-object category $\mathsf{B}G$. 
Then an action $G \curvearrowright X$ is the same data as a functor 
$\mathsf{B}G \to \mathsf{Set}$ sending the unique object of $\mathsf{B}G$ to $X$.
Is there some version of this story that works for topological groups and 
continuous group actions?

I wouldn't be writing this post if the answer were "no", so let's get into it!
This is a great case study in the ideas behind both [internalization][2] and 
[enrichment][3], and I think it'll make a great learning tool for future 
mathematicians wondering why you might care about such things.

Hopefully people find this helpful ^_^.

(Also, I'm especially sorry for the wait on this one, since I know at least 
one person has been waiting on it for two weeks now! Life got busy, but I'm 
excited to finally get this posted.)

---

First, let's take a second to talk about <span class=defn>Internalization</span>.

The idea here is to take a construction that's usually defined for sets, and 
interpret it inside some other category. For instance, a group $G$ is usually 

- a set $G$
- a function $m : G \times G \to G$ (the multiplication)
- a function $i : G \to G$ (the inversion)
- a function $e : 1 \to G$ (the unit)

satisfying some axioms.

We can _internalize_ this definition into the category $\mathsf{Top}$ 
of topological spaces by looking at 

- a topological space $G$ 
- a continuous function $m : G \times G \to G$
- a continuous function $i : G \to G$
- a continuous function $e : 1 \to G$ 

satisfying the usual axioms. 
This recovers the usual definition of a [topological group][4].

Similarly we could ask for a manifold $G$ with smooth maps $m,i,e$, and 
this would recover the definition of a [lie group][5]. At the most general,
we ask for a <span class=defn>Group Object Internal to $\mathcal{C}$</span>.
This is the data of:

<div class=boxed markdown=1>
- a $\mathcal{C}$-object $G$
- a $\mathcal{C}$-arrow $m : G \times G \to G$
- a $\mathcal{C}$-arrow $i : G \to G$
- a $\mathcal{C}$-arrow $e : 1 \to G$

satisfying the usual axioms[^1].

</div>

As a quick aside, notice the crucial use of the terminal object $1$ and the 
product $G \times G$ in the above definition. This tells us that we can only 
define groups internal to a category with finite products[^2]. 

Now just like we can internalize a group object, we can also internalize a 
group _action_! If $G$ is a group object internal to $\mathcal{C}$ and $X$ 
is some object of $\mathcal{C}$ (if you like, $X$ is a "set internal to $\mathcal{C}$")
then an <span class=defn>Internal Group Action</span> is a $\mathcal{C}$-arrow 
$\alpha : G \times X \to X$ satisfying the usual axioms.

So then a group action internal to $\mathsf{Top}$ is the usual notion of a 
[continuous group action][8], and a group action internal to manifolds is a
[lie group action][9], etc.

---

Let's change tack for a second and talk about the other half of the story.

Now we start with a [(symmetric) monoidal closed category][11]. Roughly speaking, this is 
a category where the set of arrows $\text{Hom}_{\mathcal{C}}(X,Y)$ can be 
represented by an object of $\mathcal{C}$!

For instance, the category of vector spaces $\mathsf{Vect}$ is monoidal closed 
since the homset $\text{Hom}(V,W)$ of linear maps is _itself_ a vector space, 
which we'll write as $[V,W]$. 

Another example is the category of (nice[^3]) topological spaces. The 
set of continuous functions $\text{Hom}(X,Y)$ can be given the 
[compact-open topology][14], so that it is _itself_ a topological space 
$[X,Y]$.

<br>

The fact that these categories can "talk about their own homsets" might 
make you wonder about other categories with structured homsets.

For instance, there are _lots_ of categories in the wild whose homsets 
are vector spaces! If $R$ is any $k$-algebra, then for $R$-modules $M$ 
and $N$ the homset $\text{Hom}_{R\text{-mod}}(M,N)$ is a vector space.
Similarly, if $G$ is any group, then the homset between any two 
$G$-representations is actually a vector space! We say that the categories 
$R\text{-mod}$ and $G\text{-rep}$ are <span class=defn>Enriched</span> over 
$\mathsf{Vect}$.

Similarly, you can ask about categories where each homset is a 
topological space. It turns out that these give a _fantastic_ 
first-order approximation[^4] to the theory of [$\infty$-categories][15]!

More generally, we can define a 
<span class=defn>$\mathcal{C}$-Enriched Category</span> 
to be the data of 

<div class=boxed markdown=1>
- A set of objects
- For each pair of objects $x,y$, a $\mathcal{C}$-object $\text{Hom}(x,y)$
- For each triple of objects, a composition map in $\mathcal{C}$,
    $\circ : \text{Hom}(y,z) \otimes \text{Hom}(x,y) \to \text{Hom}(x,z)$
- For each object $x$, a distinguished element[^5] $\text{id}_x \in \text{Hom}(x,x)$
- Satisfying the usual axioms.
</div>

And what will be relevant for us, a $\mathcal{C}$-enriched *groupoid*, 
which moreover has an inverse map $i : \text{Hom}(x,y) \to \text{Hom}(y,x)$
showing that every arrow is an isomorphism.

Note that every (symmetric monoidal closed) $\mathcal{C}$ is enriched over 
itself in a canonical way. We take the $\mathcal{C}$-category whose 
objects are objects of $\mathcal{C}$, and define 
$\text{Hom}(x,y)$ to be the $\mathcal{C}$-object $[x,y]$. This specializes to 
the right notion for vector spaces and topological spaces which were examples 
earlier in this section.

We'll also need the notion of a $\mathcal{C}$-enriched functor, which is 
exactly what you might expect given the above definition.

<div class=boxed markdown=1>
Given two $\mathcal{C}$-enriched categories $\mathbf{A}$ and $\mathbf{B}$, an 
<span class=defn>Enriched Functor</span> $F : \mathbf{A} \to \mathbf{B}$ sends 
objects of $\mathbf{A}$ to objects of $\mathbf{B}$. Moreover, for every pair 
of objects in $\mathbf{A}$ there should be a $\mathcal{C}$-arrow
$$F_{x,y} : \text{Hom}_{\mathbf{A}}(x,y) \to \text{Hom}_{\mathbf{B}}(Fx,Fy)$$
which are compatible with identities and composition.
</div>

For example, a $\mathsf{Vect}$-enriched functor is just a functor so that 
the map $\text{Hom}(x,y) \to \text{Hom}(Fx,Fy)$ is moreover a linear map 
(recall our homsets are vector spaces). Similarly, a $\mathsf{Top}$-enriched 
functor is a functor so that the maps on homsets 
$\text{Hom}(x,y) \to \text{Hom}(Fx,Fy)$ are continuous.

---

Now we have all the pieces we'll need to prove

<div class=boxed markdown=1>
**Theorem**: Fix a [cartesian closed][10] category $\mathcal{C}$.

There is a natural bijection between group objects $G$ internal to $\mathcal{C}$ 
and $1$-object groupoids $\mathsf{B}G$ enriched over $\mathcal{C}$. 

Moreover, for a fixed group object $G$, there is a bijection between 
internal $G$-actions and enriched functors $\mathsf{B}G \to \mathcal{C}$.
</div>

$\ulcorner$
Say that we have a group object $G$ internal to a (cartesian closed)
category $\mathcal{C}$. Then let's build a $\mathcal{C}$-enriched category,
$\mathsf{B}G$ with a single object $\star$, where $\text{Hom}(\star,\star) = G$.
Of course, we write $\text{id}_\star = e$, and composition is multiplication.

Note that $G$ is an object of $\mathcal{C}$, and the identity/composition/inverse
maps are $\mathcal{C}$-arrows. So this really is a $\mathcal{C}$-enriched 
groupoid with one object!

Conversely, say we have a one-object $\mathcal{C}$-enriched groupoid 
$\mathcal{G}$. Then $\text{Hom}_\mathcal{G}(\star,\star)$ had better be an 
object of $\mathcal{C}$, and it's easy to check that composition and inverse 
in $\mathcal{G}$ gives this object an internal group structure!

So the data of an enriched $1$-object groupoid is *exactly* the data of an 
internal group!

<br>

Now, what is a $\mathcal{C}$-enriched functor $F : \mathsf{B}G \to \mathcal{C}$?

We have to send $\star$ to some object of $\mathcal{C}$, say $X$. Then we need 
a $\mathcal{C}$-morphism $\text{Hom}(\star,\star) \to \text{Hom}(X,X)$. But by 
the definitions of $\mathsf{B}G$ and $\mathcal{C}$ (enriched over itself) 
this is the data of a $\mathcal{C}$-arrow $G \to [X,X]$.

Now we use cartesian closedness! This arrow transposes (uncurries) to 
a $\mathcal{C}$-arrow $G \times X \to X$, and one can check that the identity 
and composition preservation for the functor corresponds exactly to the 
axioms for $G \times X \to X$ to be a group action internal to $\mathcal{C}$.

Of course, walking backwards through the above discussion shows that an 
internal group action $G \times X \to X$ in $\mathcal{C}$ is exactly the 
data of a $\mathcal{C}$-enriched functor $\mathsf{B}G \to \mathcal{C}$ 
sending $\star \mapsto X$!
<span style="float:right">$\lrcorner$</span>

<div class=boxed markdown=1>
Your category-theorist senses should be tingling after reading the 
statement of the previous theorem! 

Sure there's a bijection of group/group actions, but *what about the arrows!?*

As a cute exercise, prove that this theorem upgrades to an 
equivalence[^7] of categories between

$$
\left \{ 
    \begin{array}{c}
    \text{group objects internal to $\mathcal{C}$ with} \\
    \text{internal group homs as arrows}
    \end{array}
\right \}
\simeq
\left \{ 
    \begin{array}{c}
    \text{$1$-object groupoids enriched over $\mathcal{C}$ with} \\
    \text{enriched functors as arrows}
    \end{array}
\right \}
$$

and for fixed $G$

$$
\left \{ 
    \begin{array}{c}
    \text{Internal actions $G \times X \to X$ in $\mathcal{C}$ with} \\
    \text{internal $G$-equivariant arrows}
    \end{array}
\right \}
\simeq
\left \{ 
    \begin{array}{c}
    \text{Enriched functors $\mathsf{B}G \to \mathcal{C}$ with} \\
    \text{enriched natural transformations as arrows}
    \end{array}
\right \}
$$

Part of the puzzle is how to define some of these notions
(such as "internal $G$-equivariant arrows"). You might find it helpful 
to read the preexisting definition of an [enriched natural transformation][19].
</div>

---

Let's take a second to meditate on the difference between "internalization" 
and "enrichment". This difference is usually invisible, since for "ordinary" 
categories we're always working both internal to $\mathsf{Set}$[^8] and 
enriched over $\mathsf{Set}$. That is, our categories are always sets with 
some structure, and our homsets are always... well, sets!

When you have some gadget and you think 
"Gee! I sure wish this gadget automatically had the structure of a 
$\mathcal{C}$-object!"[^9], you want to work _internally_ to $\mathcal{C}$.
Doing this means that pretending that $\mathcal{C}$ _is_ the 
universe of sets, and the $\mathcal{C}$-arrows _are_ the universe of 
functions, and then just doing whatever we usually do but "inside $\mathcal{C}$".

Figuring out exactly how to do this is the purview of much of 
[categorical logic][7]. We can construct standard ways of interpreting 
set theoretic constructions 
(such as "$\{x \in \mathbb{N} \mid \exists y. y^2 = x\}$", etc.)
inside a (sufficiently structured) category $\mathcal{C}$. Then there's a 
routine, but slightly annoying[^10], method for cashing out these 
set theoretic constructions for an "internal" version in $\mathcal{C}$!
You can read all about this [here][21] or [here][22]. One of the reasons 
so many people care about [topos theory][23] is because a topos is 
a category with _so much_ structure that we can actually internalize 
_any concept we want_ inside it!

<br>

What about enrichment? This is useful when you have an otherwise "normal" 
category, but your homsets have ~bonus structure~ that you want to respect. 
For instance, your homsets might be abelian groups, or vector spaces,
topological spaces, or chain complexes! Then _enriched_ category theory tells 
you that, say, yoneda's lemma [still works][24] when you ask that everything 
in sight respects this ~bonus structure~. This turns out to be the start 
of an incredibly interesting subject called [formal category theory][18][^6].

<div class=boxed markdown=1>
To see how well you understand internal versus enriched things, here's a cute 
exercise:

Write out, in some detail, the definition of a category _internal_ to 
$\mathsf{Cat}$ (the category of categories).
Then write out, in some detail, the definition of a category _enriched_ over 
$\mathsf{Cat}$ (with $\times$ as its monoidal structure).

Both of these concepts are extremely useful in lots of ongoing research in 
algebra, logic, and applied category theory! 
A category internal to $\mathsf{Cat}$ is a [double category][29] (See 
Evan Patterson's [excellent blog post][30] on the subject).
A category enriched over $\mathsf{Cat}$ is a [2-category][31], these show 
up very naturally, as I'll hopefully show in an upcoming blog post!
</div>

---

Ok, this blog post became something much longer than I originally intended 
(to nobody's surprise), but let's have one more cute puzzle before we go.

Another common way group actions get treated is as a group homomoprhism 
$G \to \text{Aut}(X)$, where $\text{Aut}(X)$ is the group of automorphisms 
of $X$. Is there some way to make this perspective fit in with the 
internal/enriched perspectives we've been working with so far?

Again, the answer is _yes_, but now we need to work with a 
cartesian closed category _with all finite limits_. 

<div class=boxed markdown=1>
Given a cartesian closed category with finite limits $\mathcal{C}$, 
and an object $X \in \mathcal{C}$, can you build a group object 
$\underline{\text{Aut}}(X)$ internal to $\mathcal{C}$ so that the 
global elements $1 \to \underline{\text{Aut}}(X)$ are in bijection with 
the usual automorphism group $\text{Aut}(X)$ (which is just a set)?

Then, once you've defined $\underline{\text{Aut}}(X)$, can you show that an 
internal group action $G \times X \to X$ is the same data as an internal 
group hom $G \to \underline{\text{Aut}}(X)$?
</div>

If you find this exercise hard, maybe that's incentive to learn some 
categorical logic! The category $\mathcal{C}$ has enough structure[^11] for 
its internal language to support a definition

$$
\{ f : X \to X \mid \exists g : X \to X . fg = \text{id}_X \land gf = \text{id}_X \}
$$

which we can then cash out for an honest object $\underline{\text{Aut}}(X)$ 
in $\mathcal{C}$.

Since the usual proof that this set is a group is constructive, we get 
_for free_ that any object $\underline{\text{Aut}}(X)$ in any $\mathcal{C}$
is actually a group object in $\mathcal{C}$! Moreover, the usual proof that 
an action $G \curvearrowright X$ is a group hom $G \to \text{Aut}(X)$ is 
constructive. So we learn, for free, that in $\mathcal{C}$ an internal group 
action is the same thing as an internal group hom 
$G \to \underline{\text{Aut}}(X)$! 

---

Thanks for sticking around! This was a super fun post to write since it 
touches on a LOT of aspects of "more advanced" category theory that people 
might struggle with at first. I would normally give more of an outro, but I 
have some friends coming over in a half hour and I _really_ want to get 
this posted!

Stay warm, and stay safe, all! We'll talk soon ^_^

---

[1]: https://categorytheory.zulipchat.com/
[2]: https://ncatlab.org/nlab/show/internalization
[3]: https://ncatlab.org/nlab/show/enriched+category
[4]: https://en.wikipedia.org/wiki/Topological_group
[5]: https://en.wikipedia.org/wiki/Lie_group
[6]: https://ncatlab.org/nlab/show/generalized+element
[7]: https://en.wikipedia.org/wiki/Categorical_logic
[8]: https://en.wikipedia.org/wiki/Continuous_group_action
[9]: https://en.wikipedia.org/wiki/Lie_group_action
[10]: https://en.wikipedia.org/wiki/Cartesian_closed_category
[11]: https://ncatlab.org/nlab/show/closed+monoidal+category
[12]: https://ncatlab.org/nlab/show/convenient+category+of+topological+spaces
[13]: https://ncatlab.org/nlab/show/compactly+generated+topological+space
[14]: https://en.wikipedia.org/wiki/Compact-open_topology
[15]: https://ncatlab.org/nlab/show/%28infinity%2C1%29-category
[16]: https://en.wikipedia.org/wiki/Simplicial_set
[17]: https://ncatlab.org/nlab/show/relation+between+quasi-categories+and+simplicial+categories
[18]: https://ncatlab.org/nlab/show/formal+category+theory
[19]: https://ncatlab.org/nlab/show/enriched+natural+transformation
[20]: https://youtu.be/GCm4r0F0tts?si=C-Ib3E5NbugEg0el&t=145
[21]: https://ncatlab.org/nlab/show/internal+logic
[22]: https://github.com/awodey/CatLogNotes/blob/master/2019/catlog.pdf
[23]: https://en.wikipedia.org/wiki/Topos
[24]: https://ncatlab.org/nlab/show/enriched+Yoneda+lemma
[25]: https://ncatlab.org/nlab/show/metric+space#LawvereMetricSpace
[26]: https://ncatlab.org/nlab/show/regular+category
[27]: https://ncatlab.org/nlab/show/cartesian+logic
[28]: https://ncatlab.org/nlab/show/regular+logic
[29]: https://ncatlab.org/nlab/show/double+category
[30]: https://www.epatters.org/post/why-double-categories-1/
[31]: https://ncatlab.org/nlab/show/2-category

[^1]:
    Note that the "usual axioms" can all be expressed as equalities between 
    composites of these functions. For instance, the inverse law says that 
    the composite
    
    $$
    \begin{array}{ccccccc}
    G 
    & \overset{\Delta}{\longrightarrow} & G \times G
    & \overset{1_G \times i}{\longrightarrow} & G \times G 
    & \overset{m}{\longrightarrow} & G\\
    g 
    & \mapsto & (g,g) 
    & \mapsto & (g, g^{-1}) 
    & \mapsto & g \cdot g^{-1}
    \end{array}
    $$

    is the same arrow as 

    $$
    \begin{array}{ccccc}
    G & \overset{!}{\longrightarrow} & 1 & \overset{e}{\longrightarrow} & G \\
    g & \mapsto & \star & \mapsto & e
    \end{array}
    $$

    The elementwise definitions in the lower lines are primarily for clarity
    in showing what these composites "are really doing", but they can be made 
    precise using the language of "[generalized elements][6]".

[^2]:
    There turns out to be a deep connection between "algebraic theories" 
    (like groups, rings, etc) and categories with finite products, which I want
    to write about someday. This is the start of the story of [categorical logic][7], 
    which is near and dear to my heart.

    One can view this whole game of "internalization" as a subfield of 
    categorical logic, where we focus in on the things we normally do to sets,
    and precisely say 

    1. what categories can interpret various set-theoretic constructions
    2. how to figure out what the "right way" to internalize a given 
        construction is. This turns out to be totally algorithmic!

[^3]:
    There's a couple things I could mean by "nice" here. See [here][12]
    for some options, but if pressed I'd probably say 
    [compactly generated spaces][13]. Keep in mind that this makes 
    the compact-open topology I linked to incorrect in some edge cases,
    but morally what I've said is right, and I think it's literally true 
    for compactly generated hausdorff spaces.

[^4]:
    In fact, every $\infty$-category is equivalent (in the appropriate sense) 
    to a category enriched in [simplicial sets][16]. See [here][17], for instance.

    The claim then follows from the fact that the category of 
    simplicial sets (up to homotopy) is equivalent 
    (again, in an appropriate sense) to the category of 
    topological spaces (up to homotopy).

[^5]:
    Of course, by "element" here I mean a global element. That is, a 
    map from the monoidal unit $\text{id}_x : I \to \text{Hom}(x,x)$.

[^6]:
    Of course, there's other more exotic ways to use enriched categories where 
    the hom-objects _aren't_ structured sets! See, for instance, the famous 
    [Lawvere Metric Spaces][25]. These are still extremely interesting, but 
    are of a different flavor to the enriched categories that fit into the 
    story I'm trying to tell.

[^7]:
    Isomorphism?

[^8]:
    Ignoring size issues

[^9]:
    Which for some reason I'm hearing in 
    [Tom Mullica's voice][20]
    
[^10]:
    In exactly the same way that, say, gaussian elimination, 
    is routine but annoying.

[^11]:
    Notice that, in this definition, the $g$ in the existential quantifier 
    is provably unique. This is _super_ important because it means we can 
    make this definition using only finite limits. More complicted 
    existential quantifiers require more structure on our category, namely 
    [regularity][26]. For more information see the nlab pages on 
    [cartesian logic][27] and [regular logic][28].
