---
layout: post
title: Using Ultrapowers to Solve Problems
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
[elementary embedding][9]. So $A$ and $A^\mathcal{U}$ agree on _every_ first
order question you can ask about $A$.

<img src="/assets/images/ultraproducts-howto/dumb-meme.jpg" width="50%">

Of course, we, from the outside looking in, can tell that $A$ and 
$A^\mathcal{U}$ look _very_ different! Maybe we can leverage these 
differences in order to prove things in the $A^\mathcal{U}$ setting!

The canonical example of this phenomenon is [nonstandard analysis][11],
where we study the "hyperreal numbers"

$${}^* \mathbb{R} \triangleq \mathbb{R}^\mathcal{U}$$

which have lots of nice properties[^7]. For instance, the hyperreal number

$$\epsilon \triangleq (1, 1/2, 1/3, 1/4, 1/5, \ldots)$$

is an <span class=defn>infinitesimal</span> in the sense that

1. $\epsilon \gt 0 = (0,0,0,0,0,\ldots)$
2. $\epsilon \lt a = (a,a,a,a,a,\ldots)$ for any real number $a \gt 0$.

Then nonstandard analysis uses the extra elements given to us by the 
ultrapower in order to give us neat and intuitive definitions like the 
following:

<div class=boxed markdown=1>
  If $x, y \in {}^* \mathbb{R}$, we say that $x \approx y$ when their
  difference is infinitesimal.
</div>

<div class=boxed markdown=1>
  $f$ is continuous[^8] at $x \in \mathbb{R}$ if and only if
  $f(x) \approx f(y)$ whenever $x \approx y$
</div>

Not only do these new definitions give us a new way of thinking[^9] about 
classical analysis, they're even useful for letting us prove _new_ things! 
Nowhere is this clearer than on [Terry Tao's blog][12], where he uses 
nonstandard analysis to great effect!

---

The trick behind ultrapowers, then, is to use our new 
~bonus elements~ in $A^\mathcal{U}$ in order to study some limiting propeties
of elements of $A$. For instance, the infinitesimal $\epsilon$ from before
is a _single_ element of $A^\mathcal{U}$ which expresses the features held 
simultaenously by the sequence $1/n$. 

Following the example of prime fields, we can also use ultrapowers to kill
certain "bad properties" of elements. If we have a sequence of elements of $A$ 
that are related (in that they share certain first order properties) but all 
have different "defects" (maybe they have torsion, etc.), then the sequence of
these elements, viewed as a member of the ultrapower, will share all the 
properties that relate the original elements, but will share none of the
defects! In this way, we can view elements of $A^\mathcal{U}$ as 
"idealized elements" of $A$. 

We can also use ultrapowers to kill "bad properties" of $A$ as a whole, 
as long as those bad properties are non-first order. For instance, in the
passage from $\mathbb{R}$ to ${}^* \mathbb{R}$, we kill the archimedian-ness
by introducing infinitesimals. Similarly, there are proofs that are much easier
for infinite sets than for finite sets. Having infinitely many elements gives 
you more flexibility with certain arguments. Well if your desired outcome is
first-order expressible, then just prove it for $A^\mathcal{U}$ 
(which is always infinite. Indeed, of size continuum when $A$ is finite),
and transfer back to $A$!

More speculatively, maybe there's 
a proof in $\mathbb{N}$ that you want to perform, but for some reason 
you need to know that you can always keep subtracting. Well, that's a problem
because $\mathbb{N}$ is well ordered. So you can only subtract for so long
before you have to stop. In the ultrapower $\mathbb{N}^\mathcal{U}$, though
we don't have this issue! You can keep subtracting from any nonstandard element 
as many times as you like. So do your argument here, and show a nonstandard
element does what you want. Then write your claim as 
"there exists a number doing what I want", and transfer back to $\mathbb{N}$!

---

As a last aside, I'll leave you with an old example from [the class][13]
where I met my undergraduate advisor. I'll leave it as an exercise that 
might be somewhat tricky depending on how much nonstandard analysis you've
seen:

<div class=boxed markdown=1>
  We work inside $\mathbb{N}^\mathcal{U}$.

  Say you were able to prove that there is a nonstandard twin prime.
  That is, a pair of numbers $p$ and $p+2$ which are both prime, and 
  neither of which is equivalent to the constant $(q,q,q,q,q,\ldots)$ 
  for any $q \in \mathbb{N}$.

  Then the twin prime conjecture is true[^10].
</div>

We've "simplified" the search for infinitely many twin primes into the search
for _one_ nonstandard twin prime! 

Of course, I have no idea how one would go about _finding_ a nonstandard 
twin prime! But this is a cute problem nonetheless ^_^.

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

[^7]:
    Properties that you can (and should!) read more about in the fantastic 
    _Lectures on the Hyperreals_ by Goldblatt.

    I have particularly fond memories of this book, because it was one of the
    first math textbooks that I read by myself, rather than having to read it 
    for a class.

[^8]:
    It's important here that $x \in \mathbb{R}$. If we allow 
    $x \in {}^* \mathbb{R}$, we actually get uniform continuity!

    This may appear counterintuitive at first, but does make some intuitive 
    sense after a while. Again, I'll point you to Goldblatt's book for more.

[^9]:
    An old way of thinking? This is much closer to how analysis was thought
    about before it was placed on a truly rigorous footing through limits.

[^10]:
    As a hint, first show that a nonstandard natural number must be bigger
    than every standard natural number. For instance, the standard number $3$
    satisfies the formula

    $$\forall x . x \lt 3 \iff x = 0 \lor x = 1 \lor x = 2$$

    so the only numbers less than $3$ are standard. Obviously we can do this
    for any standard number, and the claim follows.

    Next, show that, since $p$ is nonstandard, we must have

    $$\exists p . \text{isTwinPrime}(p) \land p \gt 3$$

    $$\exists p . \text{isTwinPrime}(p) \land p \gt 10,000$$

    $$\exists p . \text{isTwinPrime}(p) \land p \gt 10^{100}$$

    etc. in $\mathbb{N}^\mathcal{U}$. 

    Do you see why (after transferring these theorems back to $\mathbb{N}$)
    this means there must be infinitely many twin primes?

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
[11]: https://en.wikipedia.org/wiki/Nonstandard_analysis
[12]: https://terrytao.wordpress.com/tag/nonstandard-analysis/
[13]: https://www.cs.cmu.edu/~sutner/CDM/index.html
