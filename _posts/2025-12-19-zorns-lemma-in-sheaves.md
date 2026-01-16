---
layout: post
title: Zorn's Lemma is True in Sheaf Topoi???
tags:
  - topos-theory
---

I've been burnt out on applying to postdocs lately, which means I'm back on 
my bullshit answering questions on math.stackexchange. There was a really 
[great question][1] a few days ago which had a wild premise: OP wanted to 
understand a proof in the Elephant (D4.5.14) that Zorn's Lemma is true in 
localic topoi! The proof has a nice balance between reasoning internally 
and externally, and it felt really good to write coherently about something 
that I would have found *extremely* intimidating at the start of grad school.

In this post, I want to expand a bit on that answer, and say some words about 
how you can have a "nonconstructive" principle like Zorn's lemma inside a 
"constructive" world like $\mathsf{Sh}(\mathbb{R})$. I haven't blogged in 
a while (because of the postdoc applications) but I'm back in NY with some 
loved ones, and at this point it's starting to feel like tradition to write 
something from their couch! Here's the obligatory picture of my beloved 
Nugget:

<p style="text-align:center;">
<img src="/assets/images/zorns-lemma-in-sheaves/nugget.jpg" width="50%">
</p>

Let's get started!

TODO: rewrite the introduction


---

I'm feeling [type-theoretic][16] today, so let's work with the internal logic 
of a topos type theoretically, rather than set theoretically. I'm actually 
not sure if I've spent much time working type theoretically on this blog, 
and so I might also use this as an excuse to talk about the difference in 
semantics between the (local) set theoretic logic and the (global) type 
theoretic logic. For a more detailed reference, I first learned a lot of this
from Steve Awodey, and the lecture notes from his class are 
[available online][19] (though I'm not sure exactly what's changed between
the 2019 version and the current one).

In the set theoretic approach to the internal logic, we consider the 
lattice of subobjects of a sheaf $A$. That is, we consider *monomorphisms* 
$A_0 \rightarrowtail A$ with codomain $A$.
We think of a subobject as being a 
"proposition" $\varphi$ on $A$ (as usual, we're identifying a proposition 
$\varphi(a)$ with the subobject $$\{ a \mid \varphi(a) = \top \}$$), 
and the intersection/union of subobjects gets identified with logical 
and/or. Next, given a map $f : A \to B$ we have a base change 
functor that sends a proposition $\varphi(b)$ on $B$ to the proposition
$\varphi(f(a))$ on $A$, which we usually write as $f^* \varphi$. Base change 
admits two adjoints, which we suggestively call 
$\exists_f \dashv f^* \dashv \forall_f$, and indeed this is where quantifiers
come from! 

In the type theoretic appraoch, we consider *all* maps $P \to A$ with 
codomain $A$! 
We think of a map $\pi : P \to A$ as being a *family* of objects parameterized 
by points of $A$, given by the fibres $P_a = \pi^* (a)$. We might think of 
$P$ as a souped-up proposition on $A$, and the various elements of $P_a$ are 
the "proofs" that $P$ is true at $a$. Then a proof that "$P$ and $Q$" holds at 
$a$ is a pair of proofs in $P_a$ and $Q_a$, so this should be represented 
by the fibre product. A proof that "$P$ or $Q$" holds at $a$ is either a proof
in $P_a$ or a proof in $Q_a$, so this should be represented by the fibre 
coproduct. Again, given a map $f : A \to B$ and a family $P \to B$, we have the 
pullback $f^* P$ over $A$, with adjoints that are now called 
$\Sigma_f \dashv f^* \dashv \Pi_f$.

Note that the set theoretic framework is "just" the type theoretic framework
restricted to the monomorphisms! So if we work type theoretically we can 
recover the set theoretic perspective by taking a map $\pi : P \to A$ and 
replacing it by its image[^16] $\text{im}(\pi)$, which is a subobject of $A$. 
This maneuver is called [propositional truncation][12], and we usually write 
$\lVert P \rVert$ for $\text{im}(\pi)$. We think of a subobject $\varphi(a)$ 
as being *merely a proposition* in the sense that it is nothing but a truth 
value saying whether $\varphi(a)$ is true or not[^17]. Contrast this with a 
bundle $P \to A$, where the fibre $P_a$ might have lots of elements and 
internal structure. When we pass to the image $\lVert P \rVert$ all of this 
extra structure is forgotten.

One special case of this which can be 
confusing to newcomers is the propositional truncation of the unique map 
$A \to 1$. Recall that in a topos there are lots of [subterminal][10] 
objects, which correspond to the truth values of our topos (or, geometrically,
to the open sets of our space).
We can think of $\lVert A \rVert$ as the *support* of $A$, since in a sheaf 
topos $\mathsf{Sh}(X)$ it's exactly the largest open $U$ of $X$ on which $A$ 
exists. 

<p style="text-align:center;">
<img src="/assets/images/zorns-lemma-in-sheaves/partial-support.png" width="50%">
</p>

Recall that we should think of the terminal object $1$ of the topos 
$\mathcal{E}$ as being "the space itself". For example, in this 
picture where $\mathcal{E}$ looks like $\mathsf{Sh}(\mathbb{R})$ 
we should think of the terminal object as being the real line.

Note also that $A$ doesn't have any sections defined on the entirety 
of its support, but this lack of "global" sections isn't visible when we 
pass to the truncation (read: the open set $(0,3) \subseteq \mathbb{R}$). 
Indeed, one way of defining the support is as the type defined by 
declaring all the sections equal (in a canonical way, for the HoTT crowd).

<div class=boxed markdown=1>
For those interested in learning topos theory, it might make a good (fun?)
exercise to try and write down this sheaf $A$ over $\mathbb{R}$ precisely, 
and compute that the image of the unique map $A \to 1$ really is the image 
of the open set $(0,3) \subseteq \mathbb{R}$ under the Yoneda embedding.
</div>

These objects are called <span class=defn>Subterminal</span> because they're
subobjects of the terminal object. The subterminal objects have a lattice 
structure (since they're the powerset of $1$) and this is exactly the 
lattice of "truth values" for the internal logic of the topos.
In a [localic topos][17], these are just the open sets of the locale we 
started with, and we think of the truth value $U$ as saying that the 
proposition is true at $U$, but possibly false elsewhere in the space. 
Even in general topoi, though, thinking of the subterminals as "open sets" 
is a useful heuristic. The subterminals (and their relative versions) 
assemble into a sheaf $\Omega$, the [subobject classifier][18] of our topos,
which we think of as being the type of *mere propositions*.

To work with more general bundles, we'll assume our type theory comes with a 
univalent [universe][5] $\mathcal{U}$. We'll be 
using stack semantics for this, in the style of Coquand, Mannaa, and Ruch's
[_Stack Semantics of Type Theory_][13]... I guess I haven't actually checked 
that the semantics in that paper actually restrict to the usual 
type theoretic semantics for the non-stacky objects, but like... 
why wouldn't it, lol[^13].

All you need to know for this is that we have a universe $\mathcal{U}$ 
so that terms $A : \mathcal{U}$ denote (small) objects of our sheaf topos.
Then just like a map $A \to \Omega$ classifies a subobject 
$A_0 \rightarrowtail A$, a map $A \to \mathcal{U}$ classifies an arbitrary 
bundle $P \to A$! Semantically, over an open set $V$ in a sheaf topos 
$\mathcal{E} = \mathsf{Sh}(X)$ we interpret $\mathcal{U}(V)$ as the 
groupoid of sheaves on $V$ with sheaf isomorphisms (you might prefer to 
write this as the groupoid core of $\mathcal{E} \big / V$).

Where the type theoretic
perspective on topoi works with arbitrary objects, the set theoretic logic 
is the restriction of the type theory to mere propositions. So to recover 
the set theoretic perspective we can use type theory and truncate down 
anytime we get something more interesting than a mere proposition!
Indeed, if $A$ is any type (semantically: any object of the topos) and 
$\varphi : A \to \Omega$ is an $A$-indexed family of propositions[^12] 
(semantically: an arrow from $A \to \Omega$) then we can define
$\forall x : A . \varphi(x)$ to be the dependent product 
$\prod_{x : A} \varphi(x)$, 
and we define $\exists x : A . \varphi(x)$ to be the *truncation* 
$\left \lVert \sum_{x:A} \varphi(x) \right \rVert$. Similarly, given 
propositions $\varphi$ and $\psi$ we define $\varphi \land \psi$ to be 
$\varphi \times \psi$ and $\varphi \lor \psi$ to be 
$\lVert \varphi + \psi \rVert$.

<div class=boxed markdown=1>
It's a *very* good exercise for a budding topos theorist to check that 
this really does allow us to phrase our usual Mac Lane and Moerdjik style 
set theoretic internal logic in terms of type theory. 

In particular, can you show that a section of $\lVert A \rVert$ over $U$
is the same thing as a family of sections of $A$ on an open cover 
$$\{U_\alpha\}$$ of $U$, which need not be compatible? This is one of the 
important steps for showing that the forcing language works as expected.
</div>

<p style="text-align:center;">
<img src="/assets/images/zorns-lemma-in-sheaves/jump-right-in.gif" width="50%">
</p>

The following definitions probably won't be exciting, but I'll include 
them for completeness. We're abusing notation slightly by identifying 
$S : \Omega^A$ with the subobject $\sum_{x:A} S \rightarrowtail A$ it 
classifies. Note also that everything in sight is proposition valued 
since we're using the truncated $\lor$ and $\exists$ rather than the 
untruncated $+$ and $\Sigma$.

A <span class=defn>Poset</span> is a type $A$ with a function 
$\leq : A \times A \to \Omega$ satisfying the usual axioms 

- $\mathtt{isRefl}(A) \triangleq \forall x : A . x \leq x$
- $\mathtt{isTrans}(A) \triangleq \forall x,y,z : A . (x \leq y) \land (y \leq z) \to x \leq z$
- $\mathtt{isAntiSym}(A) \triangleq \forall x,y : A . (x \leq y) \land (y \leq x) \to x=y$

We'll write $\mathsf{Poset}$ for the type of all posets in the universe:

$$
\mathsf{Poset} \triangleq 
\sum_{A : \mathcal{U}} 
\sum_{\leq : A \to A \to \Omega}
\mathtt{isRefl}(A) \land \mathtt{isTrans}(A) \land \mathtt{isAntiSym}(A)
$$

Recall that a <span class=defn>Chain</span> in a poset $(A,\leq)$ is a 
subset[^1] $S : \mathcal{P}(A)$ satisfying

$$
\mathtt{isChain}(S) \triangleq \forall x,y : S . (x \leq y) \lor (y \leq x)
$$

Next, given a subset $S : \mathcal{P}(A)$ and an element $a : A$ 
we say that $a$ <span class=defn>Upper Bounds</span> $S$ whenever

$$
\mathtt{isUpperBound}(a,S) \triangleq \forall s : S. a \geq s
$$

A poset is called <span class=defn>Inductive</span> if every 
chain admits an upper bound. That is, if

$$
\mathtt{isInductive}(A) \triangleq
\forall C : \mathcal{P}(A) . \mathtt{isChain}(C) \to 
(\exists a : A . \mathtt{isUpperBound}(a,C))
$$

and of course we write the collection of such as 

$$
\mathsf{InductivePoset} \triangleq 
\sum_{A : \mathsf{Poset}} \mathtt{isInductive}(A)
$$

Lastly we say that $m : A$ is <span class=defn>Maximal</span> if 

$$
\mathtt{isMaximal}(m) \triangleq \forall x : A . x \geq m \to x=m.
$$

Then Zorn's lemma says that "every inductive poset has a maximal element". 
In symbols,

$$
\mathsf{ZL} \triangleq 
\forall A : \mathsf{InductivePoset} . \exists m : A . \mathtt{isMaximal}(m)
$$

This is usually regarded as a nonconstructive principle, since it's 
[well known][2] to be equivalent to the axiom of choice. Thus it's remarkable 
that Johnstone proves the following metatheorem:

<div class=boxed markdown=1>
**Proposition D4.5.14:**
Assume Zorn's Lemma[^3] holds in $\mathsf{Set}$, and let 
$\mathcal{E}$ be a localic $\mathsf{Set}$-topos[^2]. If $(A,\leq)$ is an 
inductive poset in $\mathcal{E}$, then there exists a global section 
$m : 1 \to A$ which is (internally) a maximal element of $A$.
</div>

We would like to say "$\mathcal{E} \models \mathsf{ZL}$" in the sense that 
the proposition $\mathsf{ZL}$ is equal to $\top$ in the lattice of truth 
values of $\mathcal{E}$ -- and in fact this will be true! 
But this is actually stronger in some ways, and weaker 
in others, than Johnstone's metatheorem. I think the differences are 
enlightening, so let's go over them quickly!

Modeling $\mathsf{ZL}$ is *stronger* because of the quantification 
over the universe. Remember that a $\forall A : \mathcal{U}$ claim has 
to be true at *every stage* $V$! So the internal 
$\forall A : \mathcal{U}$ requires that Zorn's Lemma holds for every object 
$V \in \mathcal{E}$ and every sheaf of posets $A$ in $\mathcal{E} \big / V$!
Johnstone's statement, however, only references the globally defined 
inductive posets, which are much harder to come by[^14].

Thankfully, since slices of a localic topos are localic, we can apply 
Johnstone's theorem slice-by-slice (and use the fact that propositions 
automatically glue) in order to get the internal unbounded quantifier we want!

Modeling $\mathsf{ZL}$ is *weaker* because of the *mere existence* of a 
maximal element for $A$. 
Johnstone's statement gives a *global* element $m : 1 \to A$, whereas saying 
$\exists m : A . \mathtt{isMaximal}(m)$ means that $m$ need 
only exist on a local cover.
As far as I know, the usual set theoretic internal logic doesn't have a 
way to guarantee global existence... So Johnstone has to say (externally)
that there's a global section $m$, which (internally) satisfies the maximality
property.

Thankfully, since we're using type theory, we can write 
$\sum_{m:A} \mathtt{isMaximal}(m)$ to talk about the global existence of $m$!

There's just one problem... we can't do both of these at once!

In order to glue the existence of maximal elements we got slice-by-slice, 
we needed this existence to be a mere proposition... As soon as we replace 
$\exists m:A$ by $\sum_{m:A}$ we're not proving a proposition anymore! Instead 
we have the *data* of (external) maps $m_V$ which eats an $A \in \mathcal{U}(V)$
(with a choice of inductive poset structure)
and returns a choice of promised maximal element $m_V(A) \in A(V)$. Since 
we aren't truncating, these choices aren't unique, and we need to manually 
check that they cohere. Indeed, there are families of posets in sheaf topoi 
where this isn't possible[^15].

TODO: add a picture to footnote 15, and maybe explain it more?

TODO: picture?

Ok, we've been distracted for long enough! Let's get to the proof of the 
metatheorem, which is based on my answer [here][1], which is itself 
based on the proof Johnstone gives in D4.5.14. This is kind of hardcore,
but the fluid movement between internal and external reasoning is instructive!

$\ulcorner$
Let $(A,\leq)$ be a poset in a localic topos $\mathcal{E}$ which is 
(internally) inductive. Assume Zorn's Lemma holds in $\mathsf{Set}$.

Let $C$ be the inductive poset in $\mathsf{Set}$ whose elements are the 
subobjects of $A$ which are (internal) chains. Then using Zorn's Lemma
in $\mathsf{Set}$ we get an external maximal element of $C$. That is, we get 
a particular subobject $A_0 \rightarrowtail A$, which is an internal chain
(since it's an element of $C$).

Now since $A_0$ is an internal chain in $A$, by internal inductivity we 
learn that $\mathcal{E}$ models 
$\exists x \in A . \ulcorner \text{$x$ uppper bounds $A_0$} \urcorner$.
Using the semantics for logic in a sheaf topos[^6], we have a covering 
$\{U_\alpha\} \twoheadrightarrow 1$ and an element $x_\alpha \in A(U_\alpha)$
upper bounding $A_0(U_\alpha)$. Moreover, because our topos is localic, we 
can take all of the $U_\alpha$ to be [subterminal][10] (read: to be 
opens of our space).

The next step is to show that 
$x_\alpha \in A_0(U_\alpha)$ so that it's more than just an upper bound --
it's a maximum. By Yoneda, having $x_\alpha \in A(U_\alpha)$ is the same 
thing as having a map $U_\alpha \to A$, and to show $x_\alpha \in A_0$ 
is to show this map $U_\alpha \to A$ factors through the subobject 
$A_0 \rightarrowtail A$.

Since $U_\alpha$ is subterminal we see that $x_\alpha$ is monic[^7] 
so we can internally consider the union $A_0 \cup U_\alpha$ 
(as a subset of $A$). Next, since $U_\alpha$ is subterminal, it has 
at most one element so that $$U_\alpha = \{x_\alpha\}$$ in the internal 
logic[^8]. But now it's easy to internally prove $$A_0 \cup \{x_\alpha\}$$ 
is a chain! Even constructively we're allowed to case on which part of the 
union we're in[^9] so that the proof of 
"$$\forall p,q \in A_0 \cup \{ x_\alpha \} . p \leq q \lor q \leq p$$" becomes 
"If $p,q$ are both in $A_0$ then we're done since $A_0$ is a chain. If $p,q$ 
are both in $$\{x_\alpha\}$$, then $p=q$ and we're done. If $p \in A_0$ and 
$$q \in \{x_\alpha\}$$ then $q \geq p$ since $x_\alpha$ is an 
upper bound for $A_0$, so we're done."

Now that we know the subobject $$A_0 \cup \{x_\alpha\}$$ is a chain, 
we move back outside the topos to our poset $C$ in $\mathsf{Set}$ of chains 
in $A$. By construction $A_0$ is a maximal element of this poset, so that 
$$A_0 \cup \{x_\alpha\}$$, which contains it, must equal it! Internally 
again this means $x_\alpha \in A_0$, so that actually $x_\alpha$ is a 
maximum for $A_0$!

This is great because one can prove maximal elements are *unique*! 
Indeed the usual proof that if $a,b$ are two maximal elements of a chain then 
$a = b$ goes through internally. This lets us use another useful fact about 
topos logic -- *unique existence is global existence*! This is often
called "[unique choice][11]", and it's an extremely useful fact about 
topoi[^10]!

So what have we done? Inductivity of $A$ gave us mere existence of an 
$x$ upper bounding $A_0$. Then we showed that $x \in A_0$ so that $x$ is 
a maximum element of a chain, so is unique. Then unique choice kicks in so 
that mere existence of $x$ becomes *global* existence of $x$ (that is, an 
inhabitant of a $\Sigma$-type). All that's left is to show that this $x$ 
is actually a maximal element of $A$. This is believable since $A_0$
was a maximal chain in $A$ and $x$ is a maximum of $A_0$... But officially 
we have to check!

We want to prove, internally, that $\forall a \in A . a \geq x \to a = x$. 
But as before, knowing $a \geq x$ means that $a \geq a_0$ for every 
$a_0 \in A_0$ so that $A_0 \cup \{a\}$ is a chain. Then by (external) 
maximality of $A_0$ (in the poset of chains in $A$) we have 
$A_0 \cup \{a\} = A_0$ and so by (internal) maximality of $x$ in $A_0$ 
we have $x \geq a$. Thus $x \geq a$ and $a \geq x$ so that $x=a$, as desired.
<span style="float:right">$\lrcorner$</span>


TODO: flesh this out... We should be happy because we know this is true, 
but...

However, a type theorist would be very *dissatisfied* since we aren't actually 
able to exhibit a term inhabiting this type! We would have to postulate it 
in a proof assistant, since we show it's true by soem combination of 
internal and external reasoning, rather than by working internally the whole
time. This interplay between internal and external is *very* interesting, 
though, and very powerful, so every good topos theorist should try to get 
comfortable with these ideas.

---

This is weird, since we typically think of Zorn's Lemma as being a 
nonconstructive principle. The point is that to make any *use* of the 
maximal element we get, we need to use excluded middle. Indeed, how do
we typically use $\mathsf{ZL}$ to build something we want? We build a poset 
of "approximations" to the good thing we want, and use $\mathsf{ZL}$ to get a 
maximal element $\mathfrak{m}$. Then we assume that $\mathfrak{m}$ isn't 
good, and use maximality to get a contradiction. Of course, with our 
constructivist hats on, we see that we've actually proven $\mathfrak{m}$ 
is not "not good"... Which is not the same as being good, unless we have 
excluded middle to simplify our logic!

When I posted about this on mastodon, my friend Matteo [told me][14] about 
a [blog post by Tom Leinster][15] that talks about how $\mathsf{ZL}$ 
really doesn't need to be as choice-y as the marketing might lead you to 
believe. I would love to spend some time thinking about how exactly this 
relates to Johnstone's argument above, but unfortunately I have a thesis 
to write and a few more postdocs to apply to.

Thanks for hanging out, everyone! I'm so glad I finally had an excuse to 
spend some time with stack semantics. I feel like I understand things 
in the 1-topos case a *lot* better now, and this also helped me settle some 
worries I had about whether all the great work done in HoTT can say anything
about 1-topoi. Now that I'm more comfortable with the semantics of univalent 
universes for 1-topoi, I'll have a much easier time externalizing some 
facts I've wanted to use in the past!

Wish me luck on the postdoc search, and we'll talk soon 💖



---

[1]: https://math.stackexchange.com/questions/5114677/zorns-lemma-and-localic-toposes/5115004#5115004
[2]: https://en.wikipedia.org/wiki/Zorn%27s_lemma#Equivalent_forms_of_Zorn's_lemma
[3]: https://ncatlab.org/nlab/show/stack+semantics
[4]: https://mathoverflow.net/a/444719/145247
[5]: https://1lab.dev/1Lab.intro.html#universes
[6]: https://arxiv.org/pdf/2202.12012
[7]: https://proofassistants.stackexchange.com/questions/942/what-is-realignment-and-is-it-useful-in-non-univalent-theories
[8]: https://grossack.site/2022/02/16/talk-practical-topos-theory
[9]: https://grossack.site/2022/12/13/internal-logic-examples
[10]: https://ncatlab.org/nlab/show/subterminal+object
[11]: https://ncatlab.org/nlab/show/principle+of+unique+choice
[12]: https://1lab.dev/1Lab.Truncation.html
[13]: https://ieeexplore.ieee.org/document/8005130
[14]: https://mathstodon.xyz/@mc/115726909419013530
[15]: https://golem.ph.utexas.edu/category/2012/10/the_zorn_identity.html
[16]: https://en.wikipedia.org/wiki/Intuitionistic_type_theory
[17]: https://ncatlab.org/nlab/show/localic+topos
[18]: https://ncatlab.org/nlab/show/subobject+classifier
[19]: https://awodey.github.io/catlog/notes/catlogdraft.pdf

[^1]:
    Here, of course, a subset of $A$ is a point in the powerset 
    $\mathcal{P}(A) \cong \Omega^A$.

[^2]:
    A "localic $\mathsf{Set}$-topos" just means that there's some locale $X$ 
    so that $\mathcal{E} \simeq \mathsf{Sh}(X)$.

[^3]:
    Johnstone assume AC holds externally, but it's clear from the proof that 
    we only need Zorn's Lemma externally. Without excluded middle, ZL is 
    weaker than Choice, so this is a very slightly cripser statement of the 
    meta-theorem.
    
[^4]:
    Think of $V$ as an open set of the topos, and we're asking what truth 
    looks like when restricted to $V$. In what follows, think of $V'$ as a 
    further open contained in $V$.

[^5]:
    In the stack semantics, at stage $V$[^4] the quantifier 
    $\forall A . \varphi(A)$ gets interpreted as "for all stages $V' \to V$ 
    and all sheaves $A$ on $V'$, $\varphi(A)$ holds". This leverages the fact 
    that the family of categories over $\mathcal{E}$ which assigns an object 
    $V$ the slice topos $\mathcal{E} \big / V$ is actually a stack, so 
    satisfies nice descent properties. 
    See, for instance [this paper][3].

    Using universes instead, the previously unbounded 
    quantifier becomes the bounded $\forall A \in \mathcal{U} . \varphi(A)$. 
    At stage $V$ this gets interpreted as "for all stages $V' \to V$ and all 
    elements $A \in \mathcal{U}(V')$, $\varphi(A)$ holds". 
    See, for instance [this paper][6] and [this][7] stackexchange answer.

    I might ask a question somewhere about how these approaches 
    relate/differ, and if I do I'll link it here.

[^6]:
    See Chapter VI.7 of Mac Lane and Moerdijk, or some old blog posts 
    [here][8] and [here][9] for more about externalizing statements in a 
    sheaf topos.

[^7]:
    Indeed *every* map from a subterminal object is monic!

    Being subterminal means being a subobject of $1$. But then 
    (using the internal logic) if $u_1, u_2 \in U \subseteq 1$ we must 
    have $u_1=u_2$ since there's only one element of the terminal object $1$. 
    So if $f : U \to X$ is any map, then it's true for silly reasons 
    that $fu_1 = fu_2 \to u_1 = u_2$, so that $f$ is internally injective 
    (thus externally monic).

    If you prefer to reason externally, take any two maps
    $u_1,u_2 : Z \rightrightarrows U$. Then composing with 
    $!_{U} : U \rightarrowtail 1$ gives 
    $!_{U} u_1 = !_{U} u_2$ since both are equal to 
    $!_Z$. But then since $!_{U}$ is monic we learn that $u_1 = u_2$,
    so that again if $f : U \to X$ is any map and $fu_1 = fu_2$ we must 
    have $u_1 = u_2$ for silly reasons, and $f$ is monic.

    For those newer to topos theory, do you see how these were really the same 
    argument?

[^8]:
    This is really shorthand for $$\{x \in A \mid x = x_\alpha\}$$.

[^9]:
    Type theorists would probably say that the image is the propositional 
    truncation of $A_0 + U_\alpha$. Since we're trying to prove a 
    proposition we can eliminate out of the disjunction, which allows casework.

[^10]:
    Remember that when we have 
    $\exists x \in X . \varphi(x)$ internally, it corresponds to 
    "existence on an open cover" where there's no reason for the $x_\alpha$ on 
    $U_\alpha$ to have anything to do with each other! Buuuuut, if there exists a 
    *unique* $x$ satisfying $\varphi$, then two $x_\alpha$ and $x_\beta$ must 
    all agree on overlaps $U_\alpha \cap U_\beta$, since there's a unique 
    $x_{\alpha \beta}$ to restrict to! Thus the sheaf property kicks in and our 
    $x_\alpha$s glue to a global section $x$!!

[^11]:
    Type theorists might compare this to working without a [universe][5], 
    so that we have no way of quantifying over types -- we can only 
    quantify over the terms of a *particular* type.

[^12]:
    You know you're lost in the sauce when "proposition bundle" starts looking
    like an appealing name for something like this... Well, it's an appealing 
    name for the classified subobject $\sum_{a:A} P(a)$ at least!
    
[^13]:
    The paper gives semantics of MLTT with a univalent universe and 
    propositional truncation valued in sheaves of (1-)groupoids on a 
    site satisfying a descent condition. Such a sheaf of groupoids is often 
    called a *stack*. As usual, we recover classical sheaves as the stacks
    fibred in *discrete groupoids* (read: sets), but now we also have a 
    relative notion of discrete that allows us to make sense of the judgement 
    $\Gamma \vdash A \text{ discrete}$ for arbitrary $\Gamma$.

    In this model, type families $\Gamma \vdash A$ are fibrations of groupoids 
    $A \twoheadrightarrow \Gamma$, and the "universe of discrete types" 
    $\mathcal{U}$ is given by the "stack of slices" whose fibre over an object 
    $V$ is the groupoid core of the slice topos 
    $\mathcal{U}(V) = \text{Core}(\mathcal{E} \big / V)$.
    Said another way, $\mathcal{U}(V)$ is the groupoid of sheaves on $V$ 
    with sheaf isomorphisms.

    I didn't work things out carefully, but at a glance it looks like when 
    you restrict attention to the setting where everything is discrete you
    recover the usual MLTT semantics.

[^14]:
    Recall that a function like $\frac{1}{x}$ is continuous on the open set 
    $(0,\infty)$ but is *not* continuous (or even defined) on the whole of 
    $\mathbb{R}$! So when we pass to the smaller open subset 
    $(0,\infty) \subseteq \mathbb{R}$ we find more continuous functions.

    In exactly the same way, but using the sheaf $\mathcal{U}$ instead of the 
    sheaf of continuous functions, there might be more inductive posets 
    defined on a smaller open subset than there are on the whole space! 
    After all, inductiveness implies inhabitedness (consider the empty chain),
    and it's very possible for a poset to be inhabited on $V$ but not globally 
    inhabited! 

    Johnstone's metatheorem does not, on its face, address these locally 
    defined posets, but the quantifier 
    $\forall A : \mathsf{InductivePoset}$ does.

[^15]:
    It's not too hard to come up with a counterexample. We need open sets 
    $U \subseteq V_1, V_2$, with inductive posets $A_1$ and $A_2$ over 
    $V_1$ and $V_2$ that restrict to the same poset $B$ over $U$. Then we need 
    the maximal elements in $A_1$ and $A_2$ to restrict to *different* 
    maximal elements in $B$! This guarantees that no matter what $m_V$ 
    function we try it can't possibly be compatible with the restriction maps!
    So no such section exists.

    Note that by propositionally truncating, these two maxima are rendered 
    equal, so that both restrictions can simultanously work!

    TODO: picture

    It's a *great* exercise to check that 
    $V_i \Vdash \mathtt{isInductive}(A_i)$. Remember that in each 
    case you'll need to check the $V_i$-valued chains and the $U$-valued 
    chains.

[^16]:
    The image of $\pi : P \to A$ turns out to be the same thing as 
    $\exists_\pi P$, where $P$ is the top element of the lattice of 
    subobjects of $P$. It might make a fun exercise to see that this 
    really does fit into an epi-mono factorization system that makes it 
    deserve the name "image".

[^17]:
    Well, remember that the internal logic of a topos can have many truth 
    values besides just true and false... So it's better to say that 
    $\varphi(a)$ has no information besides "how true" it is, which lives 
    somewhere between true and false inclusive.
