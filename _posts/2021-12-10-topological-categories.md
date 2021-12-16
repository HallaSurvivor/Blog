---
layout: post
title: Topological Categories -- A Unifying Framework
tags:
  - 
---

I think there is an obvious analogy that most mathematicians notice, perhaps
subconsciously, when learning about topological spaces and measure spaces
(often within a year or two of each other). The definitions look similar, as
do the associated maps (continuous maps pull back open sets to open sets,
and measurable maps pull back measurable sets to measurable sets). Seeing this,
it's reasonable to ask if measure spaces and topological spaces share any
similarities. More abstractly, one can ask whether their _categories_ share
any similarities. The answer turns out to be a resounding _yes_, and the study
of these <span class=defn>Topological Categories</span> will be the subject
of today's post!

First, let's recall some definitions:

<div class=boxed markdown=1>
  A <span class=defn>Topology</span> on a set $X$ is a family of subsets of $X$,
  called $\tau$, satisfying the following well known axioms:

  1. $\emptyset \in \tau$, $X \in \tau$
  2. $\tau$ is closed under finite intersections
  3. $\tau$ is closed under _arbitrary_ unions

  We call the sets $U \in \tau$ the <span class=defn>Open Sets</span> of the 
  topology[^1].

  Moreover, let $\tau$ be a topology on $X$ and $\sigma$ a topology on $Y$. 
  Then a function 

  $$f : X \to Y$$ 

  is called ($\tau$,$\sigma$)-<span class=defn>Continuous</span>
  if and only if 

  $$f^{-1}[U] \in \tau$$ 

  for every $U \in \sigma$. When the topologies are clear from context, we
  simply say $f$ is continuous.
</div>

Now let's notice some superficial observations straight from the definition.

First of all, we have two "obvious" topologies, which are simple in opposite
ways. There's the <span class=defn>Discrete Topology</span> where we take
$\tau_\Delta = \mathcal{P}(X)$ (so every set is open), and there's the 
<span class=defn>Indiscrete Topology</span> where we take $$\tau_\nabla = \{\emptyset, X\}$$
(so only the sets required in the definition are open).

These are the maximal and minimal topologies it's possible to put on a set
(respectively), and they have some interesting properties:

<div class=boxed markdown=1>
  As a cute exercise, if you haven't seen them before:

  1. Every function $f : (X,\tau_\Delta) \to (Y,\sigma)$ is continuous,
      no matter what $\sigma$ is.
  2. Every function $g : (Y,\sigma) \to (X,\tau_\nabla)$ is continuous,
      no matter what $\sigma$ is.
</div>

Next, you might think that topologies are horribly complicated objects! 
How do we ever verify that $\tau$ is closed under arbitrary unions? How do these
show up in nature?

Of course, we almost never _actually_ build topologies by hand. Instead, we
give a [basis][4] for the topology, where we specify some "basic" sets that we
would like to be open, and then formally add in everything else that we need 
to have. Bases have combinatorial properties which make them nice to work with
in practice, but we can actually get by with less!

<div class=boxed markdown=1>
  Again, as a cute exercise, show that if $\tau_\alpha$ is a family of 
  topologies on $X$, then $\bigcap \tau_\alpha$ is again a topology.

  Since we know $\mathcal{P}(X)$ is a complete lattice, and 
  $\mathcal{P}(X) = \tau_\Delta$ is itself a topology, we can hit this with some
  general nonsense from lattice theory[^2]! 

  The topologies on $X$ form a complete lattice, and every family 
  $T \in \mathcal{P}(X)$ has a unique smallest topology containing it

  $$
  \tau_T \triangleq \bigwedge 
  \{ \tau_\alpha \supseteq T \mid \tau_\alpha \text{ is a topology } \}
  $$

  In fact, show that this topology $\tau_T$ is what is traditionally called
  the topology with [subbasis][7] $T$.
</div> 

This means we almost _never_ need to build a topology by hand[^3]. Instead, we
pick a family of subsets that we _want_ to be open for some reason, then just...
look at the topology they generate!

Now, I said earlier that we're going to be interested in $\mathsf{Top}$,
the _category_ of topological spaces. So let's take a moment to rephrase 
what we've just done in categorical language:

<div class=boxed markdown=1>
There is a <span class=defn>Forgetful Functor</span> 

$$U : \mathsf{Top} \to \mathsf{Set}$$

sending $(X,\tau)$ to its underlying set $X$ and sending a continuous map 
$f : (X,\tau) \to (Y,\sigma)$ to the underlying function $f : X \to Y$.

Moreover, the fibre of $U$ over a set $X$ 
(that is, the set of all topologies on $X$) is a complete 
lattice, and thus has two distinguished elements: $\tau_\Delta$ and 
$\tau_\nabla$.

The functors $\Delta$ and $\nabla : \mathsf{Set} \to \mathsf{Top}$ sending a set
$X$ to the spaces $(X,\tau_\Delta)$ and $(X,\tau_\nabla)$ respectively form an
adjunction:

$$
\Delta \dashv U \dashv \nabla
$$
</div>

This is great, because it means $U$ has to respect all limits and colimits.

We can compute limits/colimits in $\mathsf{Top}$ by first computing
the limit/colimit of underlying sets, then choosing the smallest 
(resp. largest) topologies making the limiting arrows continuous[^5].

<div class=boxed markdown=1>
  Show that this is how we actually _do_ define most interesting topological
  constructions! 

  For instance, the product topology is defined to have the
  cartesian product as its underlying set, with the smallest topology making
  the projection maps continuous. As another example, we define the quotient
  topology to be the quotient set with the largest topology making the 
  quotient map continuous.
</div>

---

Next we recall

<div class=boxed markdown=1>
A <span class=defn>Measure Algebra</span> on a set $X$ is a 
family of subsets of $X$, called $\mathcal{A}$, satisfying the following
well known properties:

1. $\emptyset \in \mathcal{A}$, $X \in \mathcal{A}$
2. $\mathcal{A}$ is closed under finite intersections
3. $\mathcal{A}$ is closed under _countable_ unions
4. $\mathcal{A}$ is closed under complementation.

We call the sets $E \in \mathcal{A}$ <span class=defn>Measurable</span>.

Moreover, if $\mathcal{A}$ is a measure algebra on $X$ and 
$\mathcal{B}$ is a measure algebra on $Y$, then a function 

$$f : X \to Y$$

is called ($\mathcal{A}$,$\mathcal{B}$)-<span class=defn>Measurable</span>

if and only if

$$f^{-1}[E] \in \mathcal{A}$$

for every $E \in \mathcal{B}$. 
When the measure algebras are clear from context, we simply say $f$ is measurable.
</div>

Again, we note the similarities between the definitions of topological spaces
and measure spaces, as well as their associated notions of map.
Not only that, the similarities in definition beget similarities in structure!

Again, we find two "obvious" measure algebras on $X$: the 
<span class=defn>Discrete</span> algebra $$\mathcal{A}_\Delta = \mathcal{P}(X)$$
and the <span class=defn>Indiscrete</span> algebra $$\mathcal{A}_\nabla = \{\emptyset, X\}$$.

And again, we find 

<div class=boxed markdown=1>
  1. Every function $f : (X, \mathcal{A}_\Delta) \to (Y, \mathcal{B})$ is measurable
  2. Every function $g : (Y, \mathcal{B}) \to (X, \mathcal{A}_\nabla)$ is measurable
</div>

Again, these are the maximal and minimal elements of a complete lattice of 
possible measure algebras on a set $X$, and again instead of building a 
measure algebra by hand we almost always have some sets in mind that we 
_want_ to be measurable. Then we can look at the smallest measure algebra
containing those sets and call it a day[^4].

Lastly, we can assemble these into some facts about $\mathsf{Meas}$, the 
category of measure spaces:

<div class=boxed markdown=1>
There is a <span class=defn>Forgetful Functor</span> 

$$U : \mathsf{Meas} \to \mathsf{Set}$$

sending $(X, \mathcal{A})$ to its underlying set $X$ and sending a 
measurable map $f : (X, \mathcal{A}) \to (Y, \mathcal{B})$ to its underlying
function $f : X \to Y$.

Moreover, the fibre of $U$ over a set $X$ (that is, the set of all measure algebras on $X$)
is a complete lattice, with two distinguished elements $$\mathcal{A}_\Delta$$
and $$\mathcal{A}_\nabla$$.

The functors $\Delta$ and $\nabla : \mathsf{Set} \to \mathsf{Meas}$
sending a set $X$ to the measure spaces $$(X,\mathcal{A}_\Delta)$$ and
$$(X, \mathcal{A}_\nabla)$$ respectively form an adjunction

$$\Delta \dashv U \dashv \nabla$$
</div>

And again, this means that $U$ respects all limits and colimits, and that
we can _compute_ (co)limits in $\mathsf{Meas}$ by computing what the underlying
set should be, then "choosing the right measure algebra" $\mathcal{A}$ on this
(co)limit.

<div class=boxed markdown=1>
And for our last "again", show that this really is how we define our
interesting constructions on measure spaces! The canonical examples are 
the product of measure algebras, or the 
(much less frequently taught[^7])
quotient algebra[^6].
</div>

---

TODO: redo this based on Borceux's definition, cite it, and replace the
"evil" footnote with one saying the Joy of Cats defn is evil, but morally
equivalent.

Ok, so we're obviously onto something here. We have some clear parallels 
between these two categories, and some features which are obviously 
characteristic of both settings. 

The natural thing to do, then, is to abstract these common features into a 
definition, and see if anything else fits the bill! This lets us more 
efficiently draw analogies between the different subjects, and (if we're lucky)
will let us unify previously separate theorems. After all, once we prove a 
theorem using only the abstract properties of these categories, we'll immediately
know that it's true for $\mathsf{Top}$, $\mathsf{Meas}$, and any other categories
we find along the way!

Thankfully, this abstraction has been done for us! You can see the
[nlab][14] or Adámek, Herrlich, and Strecker's _The Joy of Cats_ 
(mainly VI.21) for more details[^8]. 

<div class=boxed markdown=1>
Let $U : \mathcal{T} \to \mathcal{C}$ be a surjective faithful functor that 
lifts limits uniquely[^9] and has a right adjoint $\nabla$ so that 
$U \nabla = \text{id}$.

Then $U$ is called a <span class=defn>Topological Functor</span>, and we say
$\mathcal{T}$ is <span class=defn>Topological</span> over $\mathcal{C}$.
</div>

This definition is nice and minimal in the sense that we have very little to
check. Can we compute limits in $\mathcal{T}$ by computing limits in 
$\mathcal{C}$ and then lifting? Do indiscrete objects exist? Then we're golden!

In fact, from this simple definition, _lots_ of results follow. Many of these
will look familiar from our motivating examples of 
$\mathsf{Top}$ and $\mathsf{Meas}$. You can find proofs of these in 
_Joy of Cats_.

1. The $U$-fibre over any object in $\mathcal{C}$ is a (possibly large) complete lattice
2. $U$ has a left adjoint $\Delta$ so that $U \Delta = \text{id}$
3. $U$ lifts colimits uniquely[^10]

In fact, we can use these properties to show that as long as $\mathcal{C}$ 
is nice, $\mathcal{T}$ must be nice too! Since in practice we often work with
categories topological over $\mathsf{Set}$ (which is _extremely_ nice),
we see that most topologically concrete categories are nice too!

1. If $\mathcal{C}$ is (co)complete, so is $\mathcal{T}$
2. If $\mathcal{C}$ is (co)well-powered and $U$ has small fibres[^11], so is $\mathcal{T}$
3. If $\mathcal{C}$ has a (co)generator, so does $\mathcal{T}$
4. If every arrow in $\mathcal{C}$ factors as a [regepi][16] followed by a [mono][17],
    then every arrow in $\mathcal{T}$ factors in the same way

Notice that the first three conditions conspire to tell us that whenever we can 
apply the [Special Adjoint Functor Theorem][15] to $\mathcal{C}$, we can
_also_ do so to $\mathcal{T}$! This tells us that 
limit preserving functors out of a topological category almost always 
have left adjoints, and dually that colimit preserving functors almost always
have right adjoints!

There's also the nice "preservation" properties for topological categories:

1. A full concrete[^12] subcategory $\mathcal{T}'$ of $\mathcal{T}$ 
    is itself topological over $\mathcal{C}$ if and only if 
    it is concretely (co)reflective in $\mathcal{T}$

---

So then, what do topological categories _look_ like? 

Here's the picture which I have in my head. Moreover, when a category I'm
interested in looks intuitively like this picture, I always take a second to 
check if it's topologically concrete. So far it _always_ has been!

TODO: the picture. You know the one

---

Now that we have the machinery of topological categories, we can see that
there's a _slew_ of examples! Off the top of my head, there's 

### Graphs

The category $\mathsf{DiGph}$ of directed graphs, possibly with self loops. That is, 
the category whose 

  - objects are $(V,E)$ for $V$ a set and $E \subseteq V \times V$
  - arrows $f : (V,E) \to (W,F)$ are exactly the functions $f : V \to W$ so that

$$xEy \implies f(x) E f(y)$$

  - obviously $U(V,E) = V$

Notice how there's a complete lattice of graphs (indeed, $\mathcal{P}(V \times V)$)
over every vertex set $V$. Moreover, there are discrete and indescrte objects
(though the indiscrete graph is traditionally called "complete" instead).

Moreover, this gives us lots of _other_ graph categories for free!
The following (full) subcategories are all reflective in $\mathsf{DiGph}$,
so are topological over $\mathsf{Set}$ because $\mathsf{DiGph}$ is!

- Undirected Graphs (allowing self loops)
- Reflexive Graphs (every vertex has a self loop)
- Undirected, Reflexive Graphs (obviously)

Notice we _cannot_ get the idea of a graph as most graph theorists understand
it. That is, the category of loop free undirected graphs is _not_ topological
over $\mathsf{Set}$! If it were, it would need to be complete, but the 
category of irreflexive graphs has no terminal object.

### Orders

The category $\mathsf{PreOrd}$ of preorders (reflexive, transitive relations)
with monotone maps is topological over $\mathsf{Set}$.

Next, we notice that the category of sets $V$ equipped with an equivalence
relation $\sim$ is topological over $\mathsf{Set}$! This is because it is
a (concretely) reflective subcategory of $\mathsf{PreOrd}$.

Since the category of sets with an equivalence relation is 
equivalent (indeed, isomorphic) to the category of sets with a partition,
we see that partitions are topological too!

<div class=boxed markdown=1>
⚠ Importantly, $\mathsf{Poset}$ is _not_ topological over $\mathsf{Set}$
(do you see why?). This is despite the fact that it is a reflective 
subcategory of $\mathsf{PreOrd}$! Why is there no contradiction here?
</div>

Additionally, given any (possibly large) complete lattice, we can view it 
as a category in the standard way. A category is topological over the 
terminal category $\mathbf{1}$ if and only if it's of this form.

### Functor Structured Objects

The earlier examples all had objects that looked like $(V,\alpha)$ 
where $V$ was a set and $\alpha$ was some "relational structure" on $V$.
The arrows in each of these categories are just set theoretic maps that
"respect this structure". 

We can now take a vast generalization of all of these, and work with 
categories of 
"functor structured objects" each of which will
automatically be topological!

<div class=boxed markdown=1>
Let $T : \mathcal{C} \to \mathsf{Set}$ be a functor. Following _Joy of Cats_,
we write $\mathsf{Spa}(T)$ for the category where

- objects are pairs $(C,\alpha)$ where $\alpha \subseteq T(C)$
- arrows $(C,\alpha) \to (D,\beta)$ are $\mathcal{C}$-arrows $C \to D$ 
    so that $(Tf)[\alpha] \subseteq \beta$.

A category of this form is always concrete over $\mathcal{C}$, and is called
<span class=defn>Functor Structured</span>
</div>

For example, consider the functor 
$S : \mathsf{Set} \to \mathsf{Set}$ with $SX = X^2$.
Then $\mathsf{DiGph}$ is exactly $\mathsf{Spa}(S)$!

Of course, any (co)reflective subcategories of these will also automatically
be topological, and it turns out that basically _every_ topological category is
of this form! Theorem VI.22.3 in _Joy of Cats_ says[^13]

<div class=boxed markdown=1>
  $(\mathcal{T}, U)$ is fibre-small and topological over $\mathcal{C}$ 
  if and only if it is a concretely reflective subcategory of $\mathsf{Spa}(T)$
  for some $T : \mathcal{C} \to \mathsf{Set}$.
</div>

### Topological Algebras

If you give me some algebriac gadget, like groups, then the category of
topological models is probably topological over it.

For instance, $\mathsf{TopGrp}$, the category of topological groups with
continuous homomorphisms, is topological over $\mathsf{Grp}$.

This is emblematic of a much more general phenomenon! 

Let $(\mathcal{T}, U)$ be topological over $\mathcal{C}$. Then actually the
functor category $[\mathcal{D}, \mathcal{T}]$ is topological over 
$[\mathcal{D}, \mathcal{C}]$!

How?

Well, $U \circ - : [\mathcal{D}, \mathcal{T}] \to [\mathcal{D}, \mathcal{C}]$
is surjective and faithful. It admits a right adjoint $\nabla \circ -$,
and since limits are computed pointwise in functor categories, we can 
lift any limits in $[\mathcal{D}, \mathcal{C}]$ to limits in 
$[\mathcal{D}, \mathcal{T}]$ by lifting them pointwise.

Now the same argument works if we focus our attention on those functors
which preserve finite products. This is excellent because, following Lawvere,
an algebraic structure in $\mathcal{C}$ is exactly a finite product preserving
functor from a certain "syntactic category" to $\mathcal{C}$!

So then if $\mathcal{T}$ is topological over $\mathcal{C}$, we see that 
(for example) groups in $\mathcal{T}$ are topological over groups in $\mathcal{C}$!

### A Quick Nonexample

Interestingly, the category of [locales][18] is _not_ topological over
$\mathsf{Set}$! This is related to the fact that locales many not have enough
points, so what should the forgetful functor be?

Even _more_ interestingly, according to the [nlab][19], the category of 
_spatial_ locales (that is, those with enough points) is still not topological!
Even though it's equivalent to a reflective subcategory of $\mathsf{Top}$
(the full subcategory of sober spaces). This is because the reflector sending 
a space to its sober-fication is _not_ concrete.

### Grothendieck Sites?

This last section is a bit more speculative, because I haven't checked the 
details (and probably won't). But I wanted to include it anyways because 
it's what reminded me to make this post at all[^14]!

Let's look at the category whose objects are small categories equipped
with a grothendieck topology, and whose arrows are functors 
"respecting the topologies". See [here][21] for more, because 
(at time of writing) I don't feel qualified to explain the definition.

We know there is a complete lattice of topologies on a given category 
$\mathcal{C}$, and moreover that discrete and indiscrete topologies exist.
All we need to do, then, is verify the condition about lifting limits,
but this seems intuitively clear to me: Take the limit of the underlying
categories, and then pick the largest topology on $\mathcal{C}$ rendering
all the cone maps continuous.

This should mean that the category of sites is topological over $\mathcal{Cat}$,
which we might view as a categorification of the fact that 
$\mathsf{Top}$ is topological over $\mathsf{Set}$. 

It might be interesting to know if there is some "$2$-topological" structure here, 
but I think I'm not the person to look into that (at least not yet). 

---

[^1]:
    I've been thinking a _lot_ about toposes lately, and these axioms are 
    beginning to take on a new flavor. If we view $\tau$ as a poset with 
    $\subseteq$ as the ordering, then it becomes a complete [Heyting Algebra][1]
    (indeed, a [Frame][2]). In particular, it's naturally closed under finite
    intersections and arbitrary unions, but it also has a "nonstandard" 
    meet operation, which agrees with intersection for finite meets, but is
    actually defined more generally. 

    If we view $(\tau, \subseteq)$ as a poset category, then we see it is 
    closed under finite limits and arbitrary colimits. However, it's 
    "accidentally" closed under _all_ limits, though they're not exactly 
    what you might guess. 

    This, we see, is entirely analogous to the notion of topos! Toposes have
    arbitrary colimits and finite limits. Even though they _technically_ 
    admit all limits, these limits don't behave as nicely. For some more
    details about this, see [this][3] excellent talk by Colin McLarty 
    (Nevertheless, One Should Learn the Language of Topos).

    This observation isn't going to be used at all in the rest of this post,
    I just needed to say something about it.

[^2]:
    [Closure operators][5] are ubiquitous in universal algebra and lattice theory,
    and it's _definitely_ worth spending some time with them! Basically any
    book on universal algebra will do, but my first was 
    Burris and Sankappanavar, which is freely (and legally!) available 
    [here][6]. Another great resource is Davey and Priestley's 
    _Introduction to Lattices and Order_.

[^3]:
    Except to torture our new topology students. 

[^4]:
    Though the construction of this closure operator is _much_ more complicated
    than the corresponding closure operator for topologies! Indeed every set of
    $\tau_T$ is a union of finite intersections of elements of $T$. But the 
    measurable sets in what is traditionally denoted $\sigma(T)$ are can be 
    _very_ complicated! See the [Borel Hierarchy][11] for more details.

[^5]:
    Aggravatingly, these are classically called the [initial topology][9]
    (for limits) and the [final topology][10] (for colimits), despite the 
    fact that the initial topology is final in the category of cones
    and the final topology is initial in the category of cocones... 🙃

[^6]:
    Again, the terminology has been all muddled up. Instead of calling the
    product of measure algebras the "product", it's traditional to call it
    a "tensor product" (see the [wikipedia page][12], for instance), 
    presumably because it's _generated_ by products of measurable sets in a 
    way that's analogous to the tensor product of two modules being 
    _generated_ by the pure tensors... 

[^7]:
    See [here][13], for instance.

    Oh well, it seems the terminology has stuck.

[^8]:
    ⚠ The definition I give here is actually a _theorem_ in Joy of Cats
    (VI.21.18). That said, I think it's a bit simpler to understand than the
    "classical" definition:

    $U$ is topological if and only if every $U$-structured source has a 
    unique $U$-initial lift. 

    Yeah... the language in Joy of Cats takes some getting used to. 
    This is actually a perfectly natural thing to consider, it's just 
    full of jargon. This [nlab article][14] does a pretty good job explaining
    what this definition "really means".

[^9]:
    This is a kind of "evil" version of creating limits. In fact,
    this whole definition is evil... We ask for surjectivity rather than
    essential surjectivity, as well as $U \nabla = \text{id}$ rather than just
    a natural isomorphism.

    I'm not sure if anyone has tried to redo _Joy of Cats_ in a way that
    works up to isomorphism instead of asking for equality on-the-nose in
    so many places. Thankfully it's not that big an issue in practice.

[^10]:
    The fact that our definition only has to do with limits and indiscrete 
    objects, but as a consequence we get the same properties for colimits
    and discrete objects, is a kind of categorification of the fact that a 
    complete meet-semilattice with a top element is automatically join complete
    with a bottom element.

    In fact, I really feel like topological categories are best understood in
    terms of the complete lattice living in each fibre. In an earlier draft
    of this post I tried to make that precise, but ran into some issues. 
    Morally it's right, but figuring out precisely what conditions you want 
    to put on the lattice was getting tiring and I wanted to get this post out.

    The (extremely dedicated) reader can find my attempt in the git history.

[^11]:
    This is one of those silly size conditions that we logicians care about.
    It's almost always satisfied in practice. For instance, there are only
    a set worth of topologies, measure spaces, graphs, partitions, etc. on 
    a fixed set $X$. 

[^12]:
    Here a <span class=defn>Concrete</span> category over $\mathcal{C}$
    is a category $\mathcal{T}$ equipped with a faithful functor 
    $U : \mathcal{T} \to \mathcal{C}$.

    A functor $F$ between concrete categories $(\mathcal{T},U)$ 
    and $(\mathcal{S},V)$ is called concrete when the 
    obvious triangle commutes:

    <img src="/assets/images/topological-categories/concrete-functor.png" width="50%">

    So a concretely (co)reflective subcategory is a subcategory where the 
    inclusion functor is concrete (this means the forgetful functor on the
    subcategory is the restriction of the forgetful functor on the whole 
    category) whose (co)reflector is also concrete.

    It turns out that (co)reflective subcategories often inherit nice 
    properties from their parent category, and they are surprisingly 
    common. One day I'd like to write up a blog post giving some examples
    and summarizing the nice properties that get preserved, but we'll see 
    if/when that happens.

[^13]:
    It actually says more than this, and the authors consider "topological axioms"
    and give lots of examples of how topological categories arise in this way.
    It's super interesting, but this post is already getting quite long.
    
[^14]:
    I've been planning a post on topological categories for some time,
    because I really _do_ think they're an important unifying framework.
    In fact, it's the analogy to topological categories that finally got 
    me to understand how grothendieck topologies work. You don't _actually_
    build any. You pick a collection of things that you _want_ to be covering,
    then say "give me the topology generated by these". And why can we do that?
    Because there's a complete lattice (indeed, a frame!) of topologies on 
    any fixed site. See Borceux's excellent second lecture from 
    "Toposes at Como" [here][20] for more details about this. The whole 
    series is fantastic!


[1]: https://en.wikipedia.org/wiki/Heyting_algebra
[2]: https://en.wikipedia.org/wiki/Pointless_topology
[3]: https://www.youtube.com/watch?v=vmcbm5FxRJE
[4]: https://en.wikipedia.org/wiki/Base_(topology)
[5]: https://en.wikipedia.org/wiki/Closure_operator#Closure_operators_on_partially_ordered_sets
[6]: http://www.math.uwaterloo.ca/~snburris/htdocs/ualg.html
[7]: https://en.wikipedia.org/wiki/Subbase
[8]: https://proofwiki.org/wiki/Definition:Fortissimo_Space
[9]: https://en.wikipedia.org/wiki/Initial_topology
[10]: https://en.wikipedia.org/wiki/Final_topology
[11]: https://en.wikipedia.org/wiki/Borel_hierarchy
[12]: https://en.wikipedia.org/wiki/Product_measure
[13]: https://mathoverflow.net/questions/71407/quotients-of-measurable-spaces
[14]: https://ncatlab.org/nlab/show/topological+concrete+category
[15]: https://ncatlab.org/nlab/show/adjoint+functor+theorem#statement
[16]: https://ncatlab.org/nlab/show/regular+epimorphism
[17]: https://ncatlab.org/nlab/show/monomorphism
[18]: https://ncatlab.org/nlab/show/locale
[19]: https://ncatlab.org/nlab/show/topological+concrete+category#examples
[20]: https://www.youtube.com/watch?v=kqOSk4ZWFpE
[21]: https://ncatlab.org/nlab/show/morphism+of+sites
