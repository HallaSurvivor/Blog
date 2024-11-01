---
layout: default
---

This is a (very!) rough draft of my research statement

---

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
in computer science. My third result, currently in progress, is about the 
relationships between various notions of "theory", which has applications to 
both **homotopy theory** and **linear logic**.

Of course, in addition to these side projects I've worked hard on my thesis, 
which fits into a circle of ideas relating **low dimensional topology**, 
**representation theory**, and **quantum algebra** via the study of 
**topological field theories**. The modern way to study these ideas heavily 
uses the language of $(\infty,n)$-categories, and as such I'm well versed in 
that language too.

## First Paper: Right Angled Artin Groups

A **right angled artin group** (raag) is a way to interpolate between free groups 
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

A **topos** is many things -- a generalized topological space, a category 
of sheaves, a classifying space for models of a theory, etc. -- but in this 
project we consider a topos as an "alternate universe" in which one can do math. 
Mathematical logic tells us that everything in math can be compiled down 
to a statement about sets, and to draw an analogy with programming, we can 
think of a topos as an alternative implementation of the same set theoretic 
interface. By interpreting old theorems in these new worlds, we can often get 
interesting theorems without much work, and more excitingly still, we can 
build new topoi that are tailor made for studying some class of problems! 
This is the main idea behind the recent surge of interest in **Homotopy 
Type Theory**, which is a topos tailor made for doing homotopy theory. There's 
similar topoi for differential geometry, probability, computability, and 
many more.

Johnstone's Topological Topos is world tailor made for studying sequential 
topological spaces. It can be considered a historic precursor to 
**Clausen and Scholze's Condensed Topos**, which is tailor made for studying 
compact hausdorff spaces, and is better behaved in many respects.

These topoi, in addition to being of considerable theoretic interest, have 
concrete ties to programming languages and computer science. They give a 
compelling connection between the _computable_ and the _continuous_, and 
indeed there's a large research programme in programming language theory 
based on this connection. Originally Dana Scott used domain theory in order 
to meaningfully interpret the (untyped) lambda calculus, and ever since people 
have been giving topological interpretations of programming languages 
in order to prove properties of interest to computer scientists (such as 
_strong normalization_, which tells you that every program written in a 
language halts with a meaningful output). 

Johnstone's topological topos gives one popular way to interpret programming 
languages topologically, and my project was mainly motivated by the large 
amount of folklore surrounding this topos. Computer scientists interested in 
studying programming languages shouldn't be forced to learn the 
(fairly difficult) language of topos theory in order to do their research! 
But since there were so many results that hadn't been written down anywhere, 
many would be forced to. 

In this paper, I do all of the topos theory up front, in as explicit a way 
as possible, in order to give working computer scientists direct access to the 
folklore results from this field. Moreover, I prove a new result relating 
locales (a different notion of topological space) to objects in the 
topological topos. As corollaries of this new result, we get for free 
classical facts like the bar and fan theorems, as well as a very general 
strengthening of Brouwer's axiom that (inside the topos) all functions 
between metric spaces are continuous.

Going forward, I would love to prove similar results in the 
closely related Clausen-Scholze condensed topos. 
I suspect it can play a similar role to Johnstone's topological topos, which 
will allow programming language theory to make direct contact with 
functional analysis. This is surely known to experts in the 
condensed topos, but might not yet be appreciated by experts in 
programming language theory and more classical functional analysis.


## A Result without a Paper: Algebraic Theories

An **algebraic theory** is a structure like groups, rings, modules, etc. 
where we have a collection of "operations" of various arity 
(such as multiplication, addition, etc. and constants like $1$ and $0$ which 
count as "0-ary operations") and equational axioms such as $a(bc) = (ab)c$ 
or $gg^{-1} = e = g^{-1}g$. For a nonexample, fields are _not_ algebraic, since 
the axiom $x=0 \lor \exists y . xy=1$ is (much) more complicated than a mere 
equation. An **essentially algebraic theory** is a mild generalization 
that allows certain partially defined operations, such as composition 
in the definition of a category.

Algebraic theories are better behaved with respect to quotients than 
essentially algebraic theories, so it's natural to ask when an essentially 
algebraic theory is actually algebraic. Following Lawvere, we can look at the 
classifying categories, which are finite product categories in the algebraic 
case, and finite limit categories in the essentially algebraic case. Then 
asking when an essentially algebraic theory is algebraic amounts to asking 
when a finite limit category comes from a finite product category by freely 
adjoining equalizers. I characterized such free equalizer completions, but 
learned while writing up my results that this had already been done by 
Pedicchio and Wood[^5].

A (harder) question, which hasn't already been answered is to further identify 
which algebraic theories are PROPs! I'll say more about this in the 
"Ongoing Work" section.

## My Thesis: Topological Field Theories

I also have a deep interest in **Representation Theory** and especially 
its connections with **Low Dimensional Topology**. Given a quantum group 
$G$, its category of representations is a ribbon category. Thus a choice of 
representation gives, via the Reshetikhin–Turaev functor, invariants 
of braids and links in a $3$-manifold. In case our manifold is a surface 
cross an interval $\Sigma \times I$, the collection of such invariants 
assembles into a category (called the _Skein Category_) whose cocompletion 
is the **Factorization Homology** of $\Sigma$ with coefficients in 
the ribbon category $\text{Rep}(G)$.

The algebra of endomorphisms of the emptyset in the skein category recovers 
the classical _skein algebra_ of $\Sigma$, which is generated by 
curves in $\Sigma$ modulo local relations. The **Fukaya Category** of 
$\Sigma$ has such curves as objects, and so its **Hall Algebra** is 
another algebra generated by curves in $\Sigma$.

Results of Cooper--Samuelson[^6] and Haiden[^7] show that skein algebras are 
closely related to hall algebras of fukaya categories, and it's natural to ask 
if one can understand this relationship by first computing in a disk and then 
gluing the resulting algebras together to handle the general case of surfaces.

To this end, I've spent the last two years learning about globalization 
techniques for these objects. Using **Higher Segal Spaces** to try and glue 
hall algebras, gluing Fukaya Categories via Lagrangian Skeletons 
(which are well understood in the case of surfaces), and gluing skein algebras 
using Factorization Homology and Skein Categories.


## Ongoing and Future Work

### Skein = Hall(Fukaya)
Currently I'm using these globalization techniques in order to relate 
skein algebras to hall algebras of fukaya categories, ideally in a way 
explicit enough to compute presentations of the algebras in question.

We know that fukaya categories globalize by (homotopy) pulling back copies of 
(the derived categories of) representations of $A_n$ quivers. So a 
good start is to understand the (derived) hall algebra of a pullback 
of categories. Understanding the underlying vector space is fairly easy, 
since we have an explicit description of the objects of the pullback. 
Understanding the algebra structure should be in reach too, since it comes 
from a pull-push along the span 
$\mathcal{C} \times \mathcal{C} \leftarrow \mathcal{C}^\to \to \mathcal{C}$ 
where the left arrow outputs the source and target of a map in $\mathcal{C}$ 
and the right arrows outputs its cone. The presence of a cone functor to 
handle extensions for us is an important benefit to working in the derived 
setting, which is not available for classical hall algebras.

Since right adjoints (and thus exponentials) preserve limits, we can 
compute the span 
$$
( \mathcal{C} \times_\mathcal{D} \mathcal{E} ) \times 
( \mathcal{C} \times_\mathcal{D} \mathcal{E} ) \leftarrow 
( \mathcal{C} \times_\mathcal{D} \mathcal{E} )^\to \to 
( \mathcal{C} \times_\mathcal{D} \mathcal{E})
$$
by pulling back the spans defining the hall algebras for $\mathcal{C}$, 
$\mathcal{E}$, and $\mathcal{D}^\to$. Thus, in theory, one can reconstruct 
the hall algebra of the pullback $\mathcal{C} \times_\mathcal{D} \mathcal{E}$ 
by understanding the hall algebras of the pieces (noting that we have to 
shift the degree of $\mathcal{D}$ and compute the hall algebra of its 
arrow category)... Though progress in finding the correct framework to make 
this precise has been slow.

### Recognizing PROPs Among Algebraic Theories
Another ongoing project is a generalization of my third result 
(recognizing which essentially algebraic theories are algebraic) to 
try and recognize which algebraic theories are PROPs.
This is closely related to certain theories in a **linear logic**, 
where we demand that every variable is used exactly once on both sides of 
each axiom. For instance, associativity is a linear axiom, since in 
$(ab)c = a(bc)$ each variable shows up exactly once on each side, while 
the inverse law for groups $gg^{-1}=e$ is _not_ linear, since the variable 
$g$ shows up twice on the left, but not at all on the right.

One reason to care about these PROPs/linear theories is that they can be 
interpreted in any setting where we have access to a tensor product. 
Disallowing duplication or deletion of variables corresponds to the 
fact that many tensor products in nature do not admit natural maps 
$V \to V \otimes V$ and $V \to \mathbf{1}$. So asking when an algebraic 
theory is actually a PROP amounts to asking when you can define it in 
a "linear" setting, in terms of a tensor product.

Then, just as before we wanted to understand which finite limit categories 
were free completions of a finite product category, now we want to understand 
which finite product categories are freely built from some symmetric 
monoidal category. 

The strategy for doing this is the well known relationship between finite 
product categories and (the opposite of) the category of finite sets, which 
is the free finite product category on a point. There is a symmetric monoidal 
bicategory whose objects are symmetric monoidal categories, and the finite 
product categories are exactly those admitting an action of 
$\mathsf{FinSet}^\text{op}$. Following intuition from classical modules over 
monoids, I suspect there will be "base change" functors, so that the free 
finite product category on a symmetric monoidal category $\mathcal{C}$ will 
be $\mathsf{FinSet}^\text{op} \boxtimes \mathcal{C}$. As a pleasant side 
effect, it's a classical theorem of Fox that the cofree way to solve this 
problem is to look at the subcategory of cocommutative comonoids in $\mathcal{C}$,
but since $\mathsf{FinSet}^\text{op}$ moreover classifies the cocommutative 
comonoid objects, Fox's theorem should fit into this framework by realizing 
this cofree base change as $\text{Hom}(\mathsf{FinSet}^\text{op}, \mathcal{C})$.


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

[^5]:
    _A Simple Characterization of the Theories of Varieties_, Journal of Algebra, 2000

[^6]:
    _The Hall Algebra of Surfaces I_, 
    Journal of the Institute of Mathematics of Jussieu,
    2020

[^7]:
    _Legendrian Skein Algebras and Hall Algebras_, Mathematische Annalen, 2021
