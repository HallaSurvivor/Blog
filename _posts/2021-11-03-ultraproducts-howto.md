---
layout: post
title: Using Ultraproducts to Solve Problems
tags:
  - 
---

An <span class=defn>Ultraproduct</span> is a construction from mathematical
logic that lets us prove (first order) statements about some family of 
structures by studying a single object which somehow captures the behavior 
of the family. In this post we'll talk about ultraproducts -- what are they,
what do they do, and most importantly how can we actually _use_ them to solve
problems?

First, what _are_ ultraproducts anyways? 

Fix a sequence of groups (say) $$(G_n)_{n \in \mathbb{N}}$$. Then we can take 
their _product_ and get a new group $\prod G_n$ with coordinate-wise operations.
We would like to modify this construction in order to get a group 
$\prod_\mathcal{U} G_n$ (called the <span class="defn">Ultraproduct</span> of the $G_n$s)
which has better [model theoretic][1] properties. We'll go deeper into the
specifics of the construction later but for now, it's enough to know
that the ultraproduct has the following properties:

 - Elements of $\prod_\mathcal{U} G_n$ are (equivalence classes of) tuples $(g_1, g_2, g_3, \ldots)$,
    where $g_n \in G_n$.
 - $\prod_\mathcal{U} G_n$ thinks that some first-order property is true if and only if all
    but finitely many of the $G_n$s do[^1]. For example, if all but finitely many of the $G_n$
    are abelian, then the ultraproduct will be abelian too, since abelianness is 
    defined by the first order sentence $\forall x . \forall y. x^{-1}y^{-1}xy = 1$.

One special case of interest is where all the $G_n$ are actually the same! 
We call this the <span class=defn>Ultrapower</span> of $G$, written $G^\mathcal{U}$.

It might seem strange that this construction is useful. After all, by the 
bullet point above, we know that $G^\mathcal{U}$ thinks that something is true
if and only if $G$ does. So isn't it just $G$? What do we gain by moving to the
ultrapower?

The answer is caught up in the "first-order" qualifier! It turns out that there
can be _lots_ of differences between $G$ and $G^\mathcal{U}$. For instance,
$\mathbb{Z}^\mathcal{U}$ is uncountable, (in particular, it is not cyclic).

To know which properties we _can_ transfer back and forth between $G$ and $G^\mathcal{U}$,
then, we need to know what it means for a property to be "first order". 
I'm going to assume some familiarity with basic model theory, but I'll include
abbreviated definitions for completeness[^2]. See the footnote here[^3]

---

Ok, so let's quickly write down what an ultraproduct is. Even though I'm
assuming some familiarity with logic, it's nice to have a refresher[^4].
For concreteness, we'll work with countable ultraproducts,
since they're a bit simpler to think about and they're the only ones I've
ever personally needed. 

Fix a first order language $\mathcal{L}$, fix $\mathcal{L}$-structures
$A_n$ for $n \in \mathbb{N}$. Fix moreover a nonprincipal [ultrafilter][2] 
$\mathcal{U}$ on $\mathbb{N}$. Intuitively $\mathcal{U}$ is a family of
"large" subsets of $\mathbb{N}$. What do I mean by large? Well:

<div class=boxed markdown=1>
1. No finite set is large
2. If $A \subseteq \mathbb{N}$ is large, then every $B \supseteq A$ is also large
3. If $A_1$ and $A_2$ are both large, then so is $A_1 \cap A_2$
4. For every set $A$, either $A$ or $A^c$ is large
</div>


Then we can look at the <span class=defn>Ultraproduct</span>[^5]

$$\prod_\mathcal{U} A_n \triangleq \prod A_n  \big / \sim$$

where we say that $\overline{a} \sim \overline{b}$ whenever they agree 
"almost everywhere", in the sense that 

$$\{ n \mid a_n = b_n \} \in \mathcal{U}.$$

The critical result in this area is [Łoś's Theorem][3]
(pronounced roughly like "Wash's Theorem") which says that:

<div class=boxed markdown=1>
  $$\prod_\mathcal{U} \models \varphi \iff \{ n \mid A_n \models \varphi \} \in \mathcal{U}$$

  That is, truth in the ultraproduct is exactly truth in "almost all" of the $A_n$!

  As a fairly quick exercise, you should prove this if you have some experience
  with model theory.
</div>

The main character of today's post is the ultrapower, but I can't help but say
a few words about why ultraproducts are useful. I'll contain myself, though,
and just give the following idea:

If you have a sequence of objects you want to study, say the groups 
$$\mathsf{GL}_n(\mathbb{C})$$, then it might be worth considering their 
ultraproduct. Łoś's Theorem says that the ultraproduct will behave 
similarly to the $$\mathsf{GL}_n(\mathbb{C})$$s, so many of your well
trodden techniques will probably work. Conversely, anything (first order)
you can prove about the ultraproduct _immediately_ tells you the same is
true for all but finitely many $n$!

As a concrete example, consider the family $\overline{\mathbb{F}_p}$ of
algebraic closures of finite fields.

Then the ultraproduct $\prod_\mathcal{U} \overline{\mathbb{F}_p}$ is[^6]

1. cardinality continuum
2. algebraically closed 
3. characteristic $0$

Thus it's (noncanonically!) isomorphic to $\mathbb{C}$.

Since any question about polynomials and their roots is expressible in the
first order language of fields, this gives one formalization of the 
informal "Lefschetz Principle", which says that doing algebraic geometry
over $\mathbb{C}$ is "roughly the same" as doing algebraic geometry over
any algebraically closed field of sufficiently large characteristic.

---

So then, let's move on to ultrapowers!

If $A$ is one fixed $\mathcal{L}$-structure, then we can look at the 
ultraproduct of the constant sequence $A_n = A$. In this case, we call
the resulting structure the <span class=defn>Ultrapower</span>, which we
write as $A^\mathcal{U}$. Most notably, we get an inclusion

$$A \hookrightarrow A^\mathcal{U}$$

sending $a \in A$ to the (equivalence class of the) 
constant sequence $(a,a,a,a,a,\ldots)$. 

Moreover, since $A$ models its own [diagram][8], we see that $A^\mathcal{U}$
models the diagram of $A$ as well, in a way that's compatible with the above
embedding. This means the "constant sequence" function is actually an 
[elementary embedding][9]. 




<img src="/assets/images/ultraproducts-howto/dumb-meme.jpg">

How have ultraproducts been used to solve problems?

- Ramsey Theory
- Nonstandard analysis

Speculative example:

- Twin primes

---

[^1]:
    Technically this is only true of _nonprincipal_ ultraproducts. 

[^2]:
    Pun intended

[^3]:
    <div class=boxed markdown=1>
      Let $\sigma$ be a collection of "primitive symbols" which are necessary for
      talking about a given object of study. For example:

      - If we're interested in groups, we might take $\sigma = \langle 1, \cdot, {}^{-1} \rangle$ 
      - for ordered rings we might take $\sigma = \langle \leq, 0, 1, +, -, \cdot \rangle$
      - If we're interested in graphs, we might take $\sigma = \langle E \rangle$ 
        (where $E(x,y)$ says that $x$ and $y$ are adjacent)

      Then the <span class=defn>First Order Language</span> associated to $\sigma$
      (often written $\mathcal{L}(\sigma)$ (sometimes $$\mathcal{L}_\mathsf{FO}(\sigma)$$ or 
      $$\mathcal{L}_{\omega, \omega}(\sigma)$$ if we're working with multiple different
      logics at once) is the collection of formulas we can build using

      1. primitive symbols from $\sigma$
      2. connectives: $\land$, $\lor$, $\lnot$, $\to$, $\leftrightarrow$, etc.
      3. variables like $x$, $y$, etc.
      4. $=$
      5. quantifiers: $\forall x$, $\exists x$

      ⚠ our quantifiers can only quantify over _elements_ of our structure! 
      This is the "first" in "first order". 
    </div>


    Now we see that there's no way to write down "$G$ is cyclic" in a first order way.
    The obvious idea 

    $$\exists g . \forall x . \exists n \in \mathbb{Z} . g^n = x$$

    doesn't work because we're quantifying over $\mathbb{Z}$, which is _not_
    our structure. Similarly, we can't write

    $$ \exists g . \forall x . (x = 1) \lor (x = g) \lor (x = g^{-1}) \lor (x = g^2) \lor (x = g^{-2}) \lor \ldots $$

    since that is an _infinite_ string of symbols. We only allow finite 
    conjunctions or disjunctions.

    Lastly, given a formula $\varphi \in \mathcal{L}(\sigma)$ and a 
    <span class=defn>Model</span> $\mathfrak{M}$
    (that is, a set $M$ equipped with constants, operations, and relations for each
    symbol in $\sigma$) we write $\mathfrak{M} \models \varphi$ to mean that,
    when $\varphi$ is interpreted using the operations of $\mathfrak{M}$,
    it becomes true.

    <div class=boxed markdown=1>
      Here are some nice exercises you might try to get familiar with first order logic:

      For $\sigma = \langle E \rangle$ the language of graphs, for each 
      exercise below, write a formula $\varphi \in \mathcal{L}(\sigma)$ so that a 
      graph $G \models \varphi$ if and only if it satisfies the criterion in 
      the exercise:

      1. $G$ is complete.
      2. $G$ contains a triangle.
      3. For _any_ (fixed) finite graph $\Gamma$, express 
      $G$ contains a copy of $\Gamma$ as a subgraph. 
      What about as a _full_ subgraph? Can you make 
      $G \models \varphi_\Gamma$ if and only if $G \cong \Gamma$?

      For $\sigma = \langle 1, \cdot, {}^{-1} \rangle$ the language of groups:

      1. $\lvert G \rvert \leq n$. What about $\lvert G \rvert \geq n$?
      2. $G$ is $2$-step nilpotent (think about iterated commutators)
      3. For any (fixed) finite group $H$, express $H \leq G$.
        What about $G \cong H$? (Think about the (finite!) multiplication table for $H$).
    </div>

[^4]:
    Also, not all model theory courses include ultraproducts! For instance,
    I know the graduate model theory classes at CMU, 
    (for some inexplicable reason), don't talk about them. 

[^5]:
    This seems to depend only very mildly on the choice of ultraproduct, 
    and it's reasonable to ask how the choice of ultraproduct effects the 
    resulting structure. This tends to be quite subtle, see [here][4], say,
    and for most use cases we don't worry too much about which ultrafilter
    to take (even though it _does_ matter. See [here][7])

    That said, there are certain applications where we really do want to choose
    an ultrafilter with special properties, say 
    <span class=defn>regularity</span>. You can read about what kind of bonus
    information we get when we take ultrapowers over regular ultrafilters
    [here][5], say.

[^6]:
    In order, 

    1. is a fairly easy computation, see [here][6]
    2. is because we can write down sentences 
      $\varphi_n = \forall a_0, a_1 \ldots a_n . \exists x . a_0 + a_1 x + \ldots + a_n x^n = 0$
      which say that every polynomial of degree $n$ has a root. 
    3. is because for every $q \gt 0$, cofinitely many $\overline{\mathbb{F}_p}$
    think that $$\underbrace{1 + 1 + \ldots + 1}_{q \text{ times}} \neq 0$$. So
    the ultraproduct is a field, but cannot be characteristic $q$ for any $q \gt 0$.



[1]: https://en.wikipedia.org/wiki/Model_theory
[2]: https://en.wikipedia.org/wiki/Ultrafilter_(set_theory)
[3]: https://en.wikipedia.org/wiki/Ultraproduct#%C5%81o%C5%9B's_theorem
[4]: https://math.stackexchange.com/questions/3425868/does-the-isomorphism-type-of-this-specific-ultraproduct-depend-on-the-ultrafilte
[5]: https://www.kurims.kyoto-u.ac.jp/~kyodo/kokyuroku/contents/pdf/2081-04.pdf
[6]: https://math.stackexchange.com/questions/1417688/cardinality-of-ultraproduct
[7]: https://math.stackexchange.com/questions/3257887/the-ultraproduct-of-all-prime-fields
[8]: https://en.wikipedia.org/wiki/Elementary_diagram
[9]: https://modeltheory.fandom.com/wiki/Elementary_extension
[10]: /2020/10/01/elementary-vs-submodel.html
