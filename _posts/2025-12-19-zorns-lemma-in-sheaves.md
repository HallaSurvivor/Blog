---
layout: post
title: Zorn's Lemma is True in Sheaf Topoi???
tags:
  - topos-theory
---

I started writing this post back in mid-December when I was particularly 
burnt out on applying to postdocs. So when I saw a really [great question][1]
on math.stackexchange asking how Johnstone proves Zorn's Lemma holds inside 
localic topoi (D4.5.14), I had to take the time to answer it, and then to 
write a ~~quick~~ blog post about it. (Reader: There ended up being nothing 
quick about this, haha). The proof has a nice balance between reasoning 
internally and externally, and it felt really good to write coherently about 
something that I would have found *extremely* intimidating at the start of 
grad school!

I haven't blogged in 
a while (because of the postdoc applications) but I'm back in NY with some 
loved ones, and at this point it's starting to feel like tradition to write 
something from their couch! (or, at least I was back in NY when I started this,
haha. Now I've been back in Riverside for a few weeks).

Here's the obligatory wintertime picture of my beloved Nugget:

<p style="text-align:center;">
<img src="/assets/images/zorns-lemma-in-sheaves/nugget.jpg" width="50%">
</p>

Let's get started!

---

I'm feeling [type theoretic][16] today, so let's work with the internal logic 
of a topos type theoretically, rather than set theoretically. I'm actually 
not sure if I've spent much time working type theoretically on this blog, 
and so I might also use this as an excuse to talk about the difference in 
semantics between the (local) set theoretic logic and the (global) type 
theoretic logic. For a more detailed reference, I first learned a lot of this
from Steve Awodey, and the lecture notes from his class are 
[available online][19] (though I'm not sure exactly what's changed between
the 2019 version and the current one). In a (futile) effort to keep this 
post short, I'm going to be pretty terse with my descriptions here. Hopefully
it's still helpful to newcomers who know some type theory but not much 
topos theory!

To interpret type theory in a (1-)topos $\mathcal{E}$, we interpret a type 
$A$ in context $\Gamma$ as a sheaf $A$ in the slice topos 
$\mathcal{E} \big / \Gamma$. That is, as a map $\pi : A \to \Gamma$ in 
$\mathcal{E}$. We think of this as a *family* of types $A_\gamma$ parameterized
by elements $\gamma$ of $\Gamma$ by identifying $A_\gamma$ with the fibre of 
$\pi$ over $\gamma$. Then given a context extension $f : \Delta \to \Gamma$, we 
can treat $A$ as being in context $\Delta$ by pulling it back to 
$f^* \pi : f^* A \to \Delta$, which corresponds to "weakening" the definition 
of $A$ to rely on ~bonus assumptions~ in $\Delta$ and not in $\Gamma$[^18]. 
This has two adjoints, called $\Sigma_f \dashv f^* \dashv \Pi_f$, which we 
recognize as the dependent sum and product (respectively). We also have a 
(univalent!) [universe][5] $\mathcal{U}$ (thought of as 
the "space of types") so that a bundle $A \to \Gamma$ is 
the same thing as a map $\Gamma \to \mathcal{U}$. This universe has internal 
operations $\Pi$ and $\Sigma$ that correspond to $\Pi$ and $\Sigma$ externally.
The type theory is *global* in the sense that inhabiting a $\Sigma$-type (say)
means witnessing a global section of the corresponding bundle!

Let's contrast this with the usual Mac Lane and Moerdijk style set 
theoretic semantics in a (1-)topos. Here instead of working with *all* 
maps $A \to \Gamma$, we only work with *subobjects* 
$\Gamma_0 \rightarrowtail \Gamma$! In the family picture, we're only looking 
at bundles where each fibre has at most one element[^12]. Again, a subobject 
of $\Gamma$ pulls back along a map $f : \Delta \to \Gamma$ to give a subobject 
of $\Delta$, and again we have adjoints $\exists_f \dashv f^* \dashv \forall_f$,
which really do correspond to quantifiers in our logic! We have a 
[subobject classifier][18] $\Omega$ (thought of as the "space of propositions") 
so that a subobject $\Gamma_0 \rightarrowtail \Gamma$ is the same thing as 
a map $\Gamma \to \Omega$. This subobject classifier has internal operations 
$\land$ and $\lor$ which externally correspond to the intersection and union 
of subobjects. The set theory is *local* in the sense that truth of an 
$\exists$ claim (say) means witnessing enough *local* sections of the 
corresponding bundle, whether or not they cohere into a global section!

Note that the set theoretic framework is "just" the type theoretic framework
restricted to the monomorphisms! So we can recover the set theoretic 
framework as a special case of type theory by replacing every map 
$\pi : A \to \Gamma$ by its image[^16] $\text{im}(\pi)$, which is a subobject 
of $\Gamma$.
This maneuver is called [propositional truncation][12], and we usually write 
$\lVert A \rVert$ for $\text{im}(\pi)$. We think of a subobject 
as being *merely a proposition* in the sense that it is nothing but a truth 
value. Contrast this with a bundle $A \to \Gamma$, where the fibre 
$A_\gamma$ might have lots of elements and 
internal structure. When we pass to the image $\lVert A \rVert$ all of this 
extra structure is forgotten. 

Indeed, if $A$ is any type (semantically: any object of our topos) and 
$\varphi : A \to \Omega$ is an $A$-indexed family of propositions, 
then we can define $\forall a : A . \varphi(a)$ to be the dependent product
$\prod_{a:A} \varphi(a)$ and we define $\exists a : A . \varphi(a)$ to be 
the *truncation* $\left \lVert \sum_{a:A} \varphi(a) \right \rVert$. 
Similarly, given propositions $\varphi, \psi : A \to \Omega$ we recover
$\varphi \land \psi$ as a fibre product $\varphi \times \psi$ and 
$\varphi \lor \psi$ as the *truncation* of the fibre coproduct 
$\lVert \varphi + \psi \rVert$.


One special case of propositional truncation comes from the image of the 
unique map $A \to 1$. Recall that in a topos there are lots of [subterminal][10] 
objects, which correspond to the truth values of our topos (or, geometrically,
to the open sets of our space).
We can think of $\lVert A \rVert$ as the *support* of $A$, since in a sheaf 
topos $\mathsf{Sh}(X)$ it's exactly the largest open $U$ of $X$ on which $A$ 
exists. 

<p style="text-align:center;">
<img src="/assets/images/zorns-lemma-in-sheaves/partial-support.png" width="50%">
</p>

This is a useful mental model since all images are a 
"relative version of this".
Recall that we should think of the terminal object $1$ of the topos 
$\mathcal{E}$ as being "the space itself", while other objects 
of the topos are like "covering spaces[^19]" of $\mathcal{E}$. 
Then we can think of more general images as looking like open subsets[^20] of 
covering spaces of $\mathcal{E}$.

Note also that $A$ doesn't have any sections defined on the entirety 
of its support, but this lack of "global" sections isn't visible when we 
pass to the truncation/image (read: the open set $(0,3) \subseteq \mathbb{R}$). 
Indeed, one way of defining the support is as the type defined by 
declaring all the sections equal (in a canonical way, for the HoTT crowd).

<div class=boxed markdown=1>
For those interested in learning topos theory, it might make a good (fun?)
exercise to try and write down this sheaf $A$ over $\mathbb{R}$ precisely, 
and compute that the image of the unique map $A \to 1$ really is the image 
of the open set $(0,3) \subseteq \mathbb{R}$ under the Yoneda embedding.

It's also a fantastic (fun?) exercise to compare the 
syntactic description of the propositional truncation (in terms of "glue"
setting all terms equal) to the semantic description (in terms of the "image" 
of a map in a topos).

In particular, can you show that a section of $\lVert A \rVert$ over $U$
is the same thing as a family of sections of $A$ on an open cover 
$$\{U_\alpha\}$$ of $U$, which need not be compatible? This is one of the 
important steps for showing that the forcing language works as expected.
</div>

I'm sweeping a bit of this story under the rug, since the existence of
univalent universes requires some effort.
Naively, one would like to say that $\mathcal{U}$ is a sheaf which sends an 
open set $V$ to the set of all (small) sheaves on $V$... Unfortunately this
can't work! A sheaf on $V$ can have interesting automorphisms, so the 
collection of sheaves on $V$ is naturally a *groupoid* rather than a set,
and this will cause our naive $\mathcal{U}$ to not be a sheaf!

The problem will be familiar to algebraic geometers, since it's everpresent 
in moduli space theory (indeed, we can phrase this problem as trying to build 
a moduli space $\mathcal{U}$ of small sheaves). The standard way to solve it 
is by passing to [stacks][21], which are just "sheaves of groupoids" 
rather than "sheaves of sets". See, for instance,
Coquand, Manaa, and Ruch's [_Stack Semantics of Type Theory_][13].
It's important to know that every sheaf $\mathcal{F}$ is also a stack, just 
by treating every set $\mathcal{F}(V)$ as a trivial/discrete groupoid whose 
only isomorphisms are identity arrows.

In the stack semantics
a type $A$ in context $\Gamma$ gets interpreted as a fibration[^21] of 
groupoids $A \to \Gamma$. We can interpret $\Sigma$, $\Pi$, and identity types 
in a way that will be familiar to anyone who has thought about the semantics of 
HoTT, and in the special case that every groupoid is discrete we recover 
the usual MLTT semantics for sheaves[^22]! So if we want the usual 
semantics plus a univalent universe we just need to consider the stack 
$\mathcal{U}$ which sends an open set $V$ to the *groupoid* of sheaves on 
$V$ (with sheaf isomorphisms)[^23]. You might prefer to say that $\mathcal{U}(V)$
is "just" the groupoid core of the slice topos $\mathcal{E} \big / V$.

In case you find stacks intimidating, all you need to know for this is that 
we have a universe $\mathcal{U}$ 
so that terms $A : \mathcal{U}$ denote (small) objects of our sheaf topos.
Then just like a map $\Gamma \to \Omega$ classifies a subobject 
$\Gamma_0 \rightarrowtail \Gamma$, a map $\Gamma \to \mathcal{U}$ classifies an 
arbitrary bundle $A \to \Gamma$! Moreover, this universe is [univalent][23] 
in the sense that the identity type $A=B$ for $A,B : \mathcal{U}$ is 
exactly the sheaf of isomorphisms between $A$ and $B$.

Anyways, that's probably enough details about stacks and semantics, haha.

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
enlightening, so let's go over them quickly:

<br>

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

<br>

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

<br>

Unfortunately, I'm pretty sure we can't do both of these at once! 

In order to glue the existence of maximal elements we got slice-by-slice, 
we needed this existence to be a mere proposition... As soon as we replace 
$\exists m:A$ by $\sum_{m:A}$ we're not proving a proposition anymore! Instead 
we have the *data* of (external) maps $m_V$ which eats an $A \in \mathcal{U}(V)$
(with a choice of inductive poset structure)
and returns a choice of promised maximal element $m_V(A) \in A(V)$. Since 
we aren't truncating, these choices aren't unique, and we need to manually 
check that they cohere (read: that these choices can be made "naturally"). 

Unfortunately, I've spent the last month trying to find an explicit 
counterexample and I can't manage to make it happen! I would be very 
interested if someone else is able to build one, since I need to stop 
thinking about this and start writing my thesis. I've left some thoughts 
in a footnote, though, in case anyone wants to try[^26]!

<br>

Ok, we've been distracted for long enough! Let's get to the proof of the 
metatheorem, which is based on my answer [here][1], which is itself 
based on the proof Johnstone gives in D4.5.14. This is kind of hardcore,
but the fluid movement between internal and external reasoning is 
instructive[^24]!

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
$x_\alpha$ is more than just an upper bound for $A_0(U_\alpha)$ -- it's actually 
a *maximum* in the sense that $x_\alpha \in A_0(U_\alpha)$.
By Yoneda, having $x_\alpha \in A(U_\alpha)$ is the same 
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

---

Whew! What a proof, haha. Honestly, what a post! This has taken me *forever*
to write, since at first I wanted it to be quick, but then I wanted to 
say something about stack semantics... So then I had to finally sit down 
and figure out what's going on with stack semantics (which was *extremely* 
instructive, it was a great use of time!). But then I had so much fun 
figuring out how stack semantics work that I wanted to make the post about 
that instead, since I think it's really not *so* scary and should be more 
widely understood! (Especially by people who mainly think about 1-topoi, 
like myself. I'm sure this is childsplay for the people thinking 
about $\infty$-topoi and HoTT semantics day in and day out). That made me 
want to spend some time talking about the "classical" semantics of MLTT 
in a topos, as a stepping stone to the stack semantics, especially since I've 
been meaning to write a post explaining how the type theoretic semantics 
subsume the set theoretic ones for like.... a while now, haha. So I started 
writing all that, and I realized it would just take too long to do properly.
I would love to exposit all this some day, but it's hard to justify right 
now when I need to focus on writing my thesis. 

Soooooo, this blog post ended up being a bit more hodge-podged than my 
usual ones. It was still fun for me to write and to get a lot of ideas 
straight in my head, and hopefully people still find it helpful, or at least
interesting.

If nothing else, it serves to explain this weird fact that Zorn's Lemma can 
be true in a constructive context! We typically think of Zorn's Lemma as 
being a nonconstructive principle, and I think the way to square this circle 
is to realize that to make any *use* of the 
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
[20]: https://grossack.site/2024/08/19/finiteness-in-sheaf-topoi
[21]: https://en.wikipedia.org/wiki/Stack_(mathematics)
[22]: http://www.tac.mta.ca/tac/reprints/articles/7/tr7.pdf
[23]: https://ncatlab.org/nlab/show/univalence+axiom
[24]: https://www.danielgratzer.com/papers/type-theory-book.pdf

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
    $$!_{U} : U \rightarrowtail 1$$ gives 
    $$!_{U} u_1 = !_{U} u_2$$ since both are equal to 
    $$!_Z$$. But then since $$!_{U}$$ is monic we learn that $u_1 = u_2$,
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
    like an appealing name for something like this... 
    
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
    The image of $\pi : A \to \Gamma$ turns out to be the same thing as 
    $\exists_\pi A$, where $A$ is the top element of the lattice of 
    subobjects of $A$. It might make a fun exercise to see that this 
    really does fit into an epi-mono factorization system that makes it 
    deserve the name "image".

[^17]:
    Well, remember that the internal logic of a topos can have many truth 
    values besides just true and false... So it's better to say that 
    $\varphi(a)$ has no information besides "how true" it is, which lives 
    somewhere between true and false inclusive.

[^18]:
    Think of $\Gamma = P_1 \times P_2$ as a context with two assumptions, 
    and $\Delta = P_1 \times P_2 \times P_3$ as a context with three 
    assumptions. Then our map $f : \Delta \to \Gamma$ is the projection 
    map that forgets $P_3$, and if $A$ is definable using assumptions $P_1$
    and $P_2$, then $f^* A$ is just the definition using $P_1$, $P_2$, 
    and $P_3$ that just.... ignores $P_3$!

[^19]:
    It's better to say "etale spaces over $\mathcal{E}$". In particular, 
    these are the spaces that you get by gluing open subsets of $\mathcal{E}$
    together along open intersections. There's no reason for them to cover 
    the whole of $\mathcal{E}$, and there's no reason for them to be 
    "Hausdorff". See, for instance, my old blog post [here][20].

[^20]:
    Strictly speaking, this is only true for [localic topoi][17], where the 
    subterminal objects are the open sets of the locale we started with.
    We think of the truth value $U$ as saying that the 
    proposition is true at $U$, but possibly false elsewhere in the space. 

    Even in general topoi, though, thinking of the subterminals as "open sets" 
    is a useful heuristic. The subterminals (and their relative versions) 
    assemble into the sheaf $\Omega$, the [subobject classifier][18] of 
    $\mathcal{E}$, which we think of as being the type of *mere propositions*. 
    This is also the space of "open subsets" of its localic reflection 
    (the best localic topos approximating $\mathcal{E}$).

[^21]:
    I really want to link somewhere for this, but I can't (quickly) find a 
    good source for fibrations of groupoids that makes them look as simple 
    and combinatorial as they are... The point is that you have a map of 
    groupoids $A \to \Gamma$ so that for every path 
    $\gamma_0 \cong \gamma_1$ in $\Gamma$ and every point $a_0$ in the fibre 
    over $\gamma_0$, there's a lift of this path to a path $a_0 \cong a_1$ 
    in $A$. I think I learned a lot of this stuff from Higgins's book 
    [_Categories and Groupoids_][22], see especially Chapter 13 on 
    covering maps. You might also like the discussion in the 
    Coquand, Manaa, Ruch paper, but I suspect I would have found the highly 
    syntactic type theoretic presentation a bit daunting if I didn't already 
    have some familiarity with stacks.

[^22]:
    I guess I haven't checked this SUPER closely? But like... why wouldn't 
    it be true, lol.

[^23]:
    You might wonder what happens with these stack semantics when we start 
    including other, more exotic stacks, rather than just the sheaves and this 
    one special stack $\mathcal{U}$. After all, it seems like we're leaving 
    a lot of expressivity on the table!

    I'm fairly sure that what we get is a special case of HoTT, where 
    we look only at the $1$-truncated types (semantically: the sheaves of 
    1-groupoids). From this perspective, the type theory we're describing 
    is a further special case of HoTT where we look only at the $0$-truncated 
    types and a single, special $1$-truncated type called $\mathcal{U}$ --
    the $1$-type of $0$-types in the usual HoTT universe...

    This is definitely morally right, but I haven't thought hard enough about 
    the details of the usual semantics, the stack semantics, or the HoTT 
    semantics to confidently say this is correct without caveats.

[^24]:
    This method of moving between internal and external arguments is very 
    powerful, and every good topos theorist should be familiar with it! 
    Note, though, that this might be dissatisfying for certain type 
    theorists. Indeed, since we've mixed internal and external reasoning 
    (and used something like Zorn's Lemma in the metatheory) it's not obvious
    how one would go about getting their hands on a term witnessing this 
    theorem! Indeed, such a term almost certainly doesn't exist (since it 
    should be possible to find non-localic models which don't satisfy 
    $\mathsf{ZL}$) so the best we can do is postulate this in a proof 
    assistant.

    I have some pipe dreams of studying a modal type theory for localic 
    topoi over a base topos
    where one might try to formalize this entire argument internally... 
    But that's definitely a project for another day, haha. I still have to 
    write my thesis, which is about entirely different ideas in a fun 
    intersection of representation theory and sympelctic topology!

[^25]:
    Indeed, if it were it would have 
    a global section by Johnstone's theorem, but it might be fun to see more 
    directly why it isn't! As a hint, consider the (global!) subobject $C$ with 
    support away from a point and only one element 
    (choose one of the two fibres this can be done consistently since 
    we removed a point).

    Can you show this is a chain? Can you show $\mathsf{Sh}(S^1)$ doesn't 
    model $\exists a : A . \mathtt{isUpperBound}(a,C)$? As a hint, what 
    happens in a neighborhood of the point we removed? (Why do we still 
    have to consider a neighborhood of that point?)
    
[^26]:
    I'm pretty sure the example can't be based on a locally euclidean space...
    Indeed if you had two distinct maxima $a$ and $b$ for $A$ on a small open 
    ball $U \cong \mathbb{R}^n$ then you could look at the subobject
    $$\{a \mid x_1 \gt 0\} \cup \{b \mid x_1 \lt 0 \}$$ (using local 
    coordinates $(x_1, \ldots, x_n)$ on $U$). This is a chain since any 
    (generalized) element is contained in precisely one of the two opens 
    $$\{x_1 \gt 0\}$ and $$\{x_1 \lt 0\}$$, but on either open there's only 
    one element. Of course, this chain does not admit a local upper bound 
    in the neighborhood of $x_1 = 0$... So the poset we started with, which 
    had two distinct maxima, cannot have been inductive!

    Indeed, maxima seem to "persist" from small opens to larger opens. 
    If $U \subseteq V$ and we have a maximum $m$ in $A(U)$, then we can 
    consider the subobject (at stage $V$!) $\{m \mid U \}$, which is a chain,
    so has an upper bound. So there must be a section $m' \in A(V)$ which 
    restricts to $m$ on $U$ (since $m' \geq m$ on $U$, so $m' = m$ by 
    maximality).

    Another issue is that inductiveness is local, since it's phrased entirely 
    using set theoretic quantifiers. So in a general topological space 
    if we try to find opens $U$ and $V$ so that maxima on $A(U)$ and $A(V)$ 
    restrict to distinct maxima on $A(U \cap V)$ (which would show that no 
    choice of maximum can be consistently made for $A(U \cap V)$) then 
    actually $A$ must be inductive on the whole of $U \cup V$ so that 
    Johnstone's metatheorem kicks in on this slice and we get a global section 
    over $U \cup V$. In particular, there must be *some* way to consistently 
    make the choice of maximum for any particular configuration...

    This made me wonder if maybe 
    $\prod_{A : \mathtt{inductivePoset}} \sum_{m : A} \mathtt{isMax}(m)$
    *is* provable... but then I haven't been able to convince myself about it!
