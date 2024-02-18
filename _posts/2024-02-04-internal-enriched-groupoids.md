---
layout: post
title: Internal Group Actions as Enriched Functors
tags:
  - 
---

TODO: maybe box more things?

Earlier today on the [Category Theory Zulip][1], Bernd Losert asked an 
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
are vector spaces! If $R$ is any $k$-algebra, then for any modules 
$M$ and $N$, we have a vector space of module homs $\text{Hom}(M,N)$.
If $G$ is any group, then the category of $G$-representations has vector 
spaces for homsets.

Similarly, the idea of categories where each homset is a topological space 
(and functors which have to be "continuous") gives a fantastic first-order 
approximation[^4] to the theory of [$\infty$-categories][15].

<br>

This leads to the definition of a 
<span class=defn>$\mathcal{C}$-Enriched Category</span> 
which has 

- A set of objects
- For each pair of objects $x,y$, a hom-$\mathcal{C}$-object $\text{Hom}(x,y)$
- For each triple of objects, we should have a composition map in $\mathcal{C}$:
    $\circ : \text{Hom}(y,z) \otimes \text{Hom}(x,y) \to \text{Hom}(x,z)$
- For each object $x$, a distinguished element[^5] $\text{id}_x \in \text{Hom}(x,x)$
- Satisfying the usual axioms.

And what will be relevant for us, a $\mathcal{C}$-enriched *groupoid*, 
which moreover has an inverse map $i : \text{Hom}(x,y) \to \text{Hom}(y,x)$
showing that every arrow is an isomorphism.

Note that every (symmetric monoidal closed) $\mathcal{C}$ is enriched over 
itself in a canonical way. We take the $\mathcal{C}$-category whose 
objects are objects of $\mathcal{C}$, and define 
$\text{Hom}(x,y)$ to be the $\mathcal{C}$-object $[x,y]$. This specializes to 
the right notion for vector spaces and topological spaces which were examples 
earlier in this section.

<br>

We'll also need the notion of a $\mathcal{C}$-enriched functor, which is 
exactly what you might expect given the above definition.

Given two $\mathcal{C}$-enriched categories $\mathbf{A}$ and $\mathbf{B}$, an 
<span class=defn>Enriched Functor</span> $F : \mathbf{A} \to \mathbf{B}$ sends 
objects of $\mathbf{A}$ to objects of $\mathbf{B}$. Moreover, for every pair 
of objects in $\mathbf{A}$ there should be a $\mathcal{C}$-arrow
$$F_{x,y} : \text{Hom}_{\mathbf{A}}(x,y) \to \text{Hom}_{\mathbf{B}}(Fx,Fy)$$
which are compatible with identities and composition.

For example, a $\mathsf{Vect}$-enriched functor is just a functor so that 
the map $\text{Hom}(x,y) \to \text{Hom}(Fx,Fy)$ is moreover a linear map 
(recall our homsets are vector spaces). Similarly, a $\mathsf{Top}$-enriched 
functor is a functor so that the maps on homsets 
$\text{Hom}(x,y) \to \text{Hom}(Fx,Fy)$ are continuous.

---

Now we have all the pieces we'll need!

Say that we have a group object $G$ internal to a ([cartesian closed][10])
category $\mathcal{C}$. Then let's build a $\mathcal{C}$-enriched category,
$\mathsf{B}G$ with a single object $\star$, where $\text{Hom}(\star,\star) = G$.
Of course, we write $\text{id}_\star = e$, and composition is multiplication.

Note that $G$ is an object of $\mathcal{C}$, and the identity/composition/inverse
maps are $\mathcal{C}$-arrows. So this really is a $\mathcal{C}$-enriched 
groupoid with one object!

Now, what is a $\mathcal{C}$-enriched functor $F : \mathsf{B}G \to \mathcal{C}$?

We have to send $\star$ to some object of $\mathcal{C}$, say $X$. Then we need 
a $\mathcal{C}$-morphism $\text{Hom}(\star,\star) \to \text{Hom}(X,X)$. But by 
the definitions of $\mathsf{B}G$ and $\mathcal{C}$ (enriched over itself) 
this is the data of a $\mathcal{C}$-arrow $G \to [X,X]$.

Now we use cartesian closedness! This arrow transposes (uncurries) to 
a $\mathcal{C}$-arrow $G \times X \to X$, and one can check that the identity 
and composition preservation for the functor corresponds exactly to the 
axioms for $G \times X \to X$ to be a group action internal to $\mathcal{C}$.

Conversely, given a (this works the other way too)

---

Spend a bit of time meditating on enrichment vs internalization as two 
different ways to make a category have structure related to the structure 
of $\mathcal{C}$. It's natural to ask how much category theory you can 
redo in the setting of enriched/internal categories. Can you recover some 
kind of yoneda lemma? This is the start of [formal category theory][18]

Maybe also meditate on the way that working over $\mathcal{C}$ clarifies 
the two ways that $\mathsf{Set}$ functions (internalization vs enrichment)
even in the classical case. But this difference is usually invisible to us 
since every category[^6] is always both $\mathsf{Set}$-enriched and internal 
to $\mathsf{Set}$.

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
    Ignoring size issues
