---
layout: default
---

We're shooting for ~2500 words.

## Introduction 

My research interests lie in the intersection between algebra, geometry, 
and logic -- an intersection often made clearer with the language of 
(higher) category theory. Moreover, I'm often (but not exclusively) interested 
in concrete problems, which may need category theoretic tools in their proof, 
but not their statement. Category theory offers a bridge between 
many different subjects, and I'm particularly interested in problems that use 
intuitions or techniques from one subject to shed light on problems in 
another area.

During my PhD, I solved three problems as a sole author, each by applying 
category theory to a different subject. The first was accepted in AGT, 
and studies a problem in **geoemtric group theory**.
The second was submitted to TAC, and is a study of what 
**point set topological** constructions you can do while guaranteeing that 
everything you can write is automatically sequentially continuous. This has 
surprising applications to the understanding of various **programming languages** 
in computer science. My third paper, currently in progress, is about the 
relationships between various notions of "theory", which has applications to 
both **homotopy theory** and **linear logic**.

Of course, in addition to these side projects I've worked hard on my thesis, 
which fits into a circle of ideas relating **low dimensional topology**, 
**representation theory**, and **quantum algebra** via the study of 
**topological field theories**. The modern way to study these ideas heavily 
uses the language of $(\infty,n)$-categories, and as such I'm well versed in 
that language too.

## First Paper: Right Angled Artin Groups

A _right angled artin group_ (raag) is a way to interpolate between free groups 
and free abelian groups by adding relations forcing only some of the 
generators to commute. These relations are encoded in a graph whose vertices 
are generators, and where an edge indicates that two generators should 
commute. The raags are central objects of study in 
geometric group theory, and have seen applications in the resolution of the 
virtual haken conjecture as well as in the study of mapping class groups 
(following an analogy between the commutation graph of a 
raag and the curve graph of a mapping class group).

It has been known for decades that combinatorial properties of a graph 
are faithfully reflected in algebraic properties of its raag, and vice versa,
but the relationship between graph homomorphisms and group homomorphisms 
between the raags has been less well studied. 

In my paper _The Right Angled Artin Group Functor as a Categorical Embedding_[^4],
I show that there's an extremely close connection between graph 
homomorphisms and raag homomorphisms. Indeed, I show the graph homomorphisms 
inject into the group homomorphisms, and moreover give a procedure for 
recognizing the image (so we can detect when a group homomorphism came 
from a graph homomorphism), and for inverting this procedure to 
recover the original graph homomorphism! This can be done purely 
algebraically, without making any reference to the graphs we started with 
(concretely) or indeed even to the category of graphs (abstractly). Instead, 
there's a certain _coalgebra structure_ on a group $G$ if and only if $G$ is 
a raag[^1], and a group homomorphism came from a graph homomorphism if and 
only if it moreover respects this coalgebra structure!

This, abstractly, tells us that _all_ of the combinatorics of a graph 
homomorphism has to be algebraically reflected in the algebra of the 
induced homomorphism of raags, since we can recover the graph homomorphism 
algebraically! An interesting direction for future work (which would make 
a great undergraduate project!) would be to use this to start building a 
concrete dictionary between combinatorial features of graph homomorphisms 
and algebraic features of the induced group homomorphisms. For instance an
$r$-coloring of a graph is a certain homomorphism[^2] to $K_r$, the complete 
graph on $r$-vertices, and it should be interesting to study this purely 
in terms of the raags.

Now even though the questions of recognizing raags amongst the groups and 
relating the combinatorics of graph homomorphisms to the algebra of 
group homomorphisms don't directly mention categories, the proof of this 
theorem crucially uses the machinery of **comonadic descent**, which is a 
generalization of the descent theorems from Grothendieck's school to 
other categories. Concretely this machinery lets us understand the images
of certain left adjoints, and that's exactly how we use it here 
(since the functor assigning a graph to its raag is a left adjoint).

It's an open question of Kim and Koberda[^3] to characterize which pairs 
of raags $(G,H)$ admit a group embedding $G \hookrightarrow H$, and while 
this paper primarily used the **comonad** attached to the raag construction, 
there's a dual **monad** attached to the raag construction, which could shed 
light on this conjecture. This would be an interesting avenue to pursue 
going forwards.


## Second Paper: The Topological Topos



---

[^1]: 
    Note that this means it's undecidable whether a given group 
    admits such a coalgebra structure, by the Adian-Rabin Theorem. But 
    all the undecidability is concentrated in whether the search for 
    this coalgebra structure will halt. Everything else in the paper is 
    completely effective.

[^2]:
    The result crucially uses graphs with self loops, so an $r$-coloring 
    is a homomorphism to $K_r$ and a _proper_ $r$-coloring is a homomorphism 
    to $K_r$ avoiding the self loops.

[^3]:
    _Embedability between Right Angled Artin Groups_, Geometry & Topology, 2013

[^4]:
    Accepted to Algebraic and Geoemtric Topology.
