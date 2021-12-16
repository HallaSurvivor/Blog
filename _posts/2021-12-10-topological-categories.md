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
<span class=defn>Discrete</span> algebra $\mathcal{A}_\Delta = \mathcal{P}(X)$
and the <span class=defn>Indiscrete</span> algebra $\mathcal{A}_\nabla = \{\emptyset, X\}$.

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

Thankfully, this abstraction has been done for us[^8]!

<div class=boxed markdown=1>
A (faithful) functor $U : \mathcal{T} \to \mathcal{C}$ is called a 
<span class=defn>Topological Forgetful Functor</span> if 

1. $U$ admits adjoints $\Delta \dashv U \dashv \nabla$ so that 
      $U \Delta = U \nabla = \text{id}$
2. Each fibre $$U^{-1}(C)$$ is a (possibly large) complete lattice
3. If $U C_1 = U C_2 = C$, then the identity arrow on $C$ lifts to an 
    arrow $C_1 \to C_2$ if and only if $C_1 \leq C_2$ in the lattice 
    over $C$.

If such a functor $U$ exists, we say that $\mathcal{T}$ is 
<span class=defn>Topological</span> over $\mathcal{C}$.
</div>

⚠ Take some care! Here we're ordering the fibre over $C$ so that the 
discrete topology is at the _bottom_ and the indiscrete topology is at 
the _top_! This lines up better with our idea that left adjoints are initial
and right adjoints are terminal, but is a bit backwards since usually we think
of the discrete topology as having "the most open sets".

---


- egs
  - topological/measure spaces, obviously
  - graphs
  - topological groups?
  - "nice" topological categories
      - historic motivation
  - sites over Cat

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
    ⚠ This is _not_ the standard presentation of the definition of 
    topologically concrete category!

    If you read _Joy of Cats_ or [the nlab][14], the definition you'll see
    is

    <div class=boxed markdown=1>
    $$U : \mathcal{T} \to \mathcal{C}$$ is called topological forgetful if
    "every $U$-structured source has a $U$-initial lift", or, to expand out 
    the jargon:

    If $C$ is in $\mathcal{C}$ and we have a (possibly large) family of objects
    $S_\alpha$ in $\mathcal{T}$, plus arrows $f_\alpha : C \to US_\alpha$ in
     $\mathcal{C}$, then 
     "there is a best topology on $C$ making the $f_\alpha$ continuous".
     Formally:

     1. There is an object $\tilde{C}$ in $\mathcal{T}$ and arrows 
        $\tilde{f_\alpha} : \tilde{C} \to S_\alpha$ so that $U\tilde{C} = C$
        and $U\tilde{f_\alpha} = f_\alpha$
     2. If $T$ is any other object of $\mathcal{T}$ and $g : UT \to C$ is an
     arrow in $\mathcal{C}$ so that each of the $f_\alpha \circ g : UT \to US_\alpha$
     is $U h_\alpha$ for some $h_\alpha$ in $\mathcal{T}$, then actually
     $g = U \tilde{g}$ where $\tilde{g} : T \to \tilde{C}$.
    </div>

    This is a fine definition (even if it took me a while to really internalize it),
    but it places the focus on the ability to lift maps in $\mathcal{C}$, whereas I
    think the focus should be on the lattice of possible topologies. 

    It's not too hard to see that these definitions are equivalent. 

    It's proved in _The Joy of Cats_ that we always get a complete lattice in
    the fibres, as well as the adjoint condition and the "compatibility" between
    identity arrows and the lattice order. See VI.21 for more.

    Conversely, let's say that $U : \mathcal{T} \to \mathcal{C}$ satisfies
    the fibrewise complete lattice conditions outlined in the main body 
    of this post. We'll show that it also satisfies the _Joy of Cats_ definition.

    Let $S_\alpha$ be a (possibly large) family of objects in $\mathcal{T}$,
    and fix arrows $f_\alpha : C \to U S_\alpha$. 

    Then we can consider the (possibly large) join

    $$
    \bigvee 
    \big \{ 
      \tilde{C} 
    \mid 
      \forall \alpha . 
      \exists \tilde{f_\alpha} : \tilde{C} \to S_\alpha . 
      U \tilde{f_\alpha} = f_\alpha
    \big \}
    $$

    and let $\tilde{C}$ be this element of the fibre over $C$.

    First, notice every $f_\alpha$ comes from an arrow 
    $\tilde{f_\alpha} : \tilde{C} \to S_\alpha$, basically by construction.

    Second, say $g : UT \to C$ is an arrow so that each 
    $f_\alpha \circ g : UT \to U S_\alpha$ comes from an arrow in $\mathcal{T}$.


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
