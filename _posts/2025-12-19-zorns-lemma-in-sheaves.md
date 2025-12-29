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
something from their couch!

Let's get started!

---

Recall that a <span class=defn>Chain</span> in a poset $(A,\leq)$ is a 
subset[^1] $C : \mathcal{P}(A)$ satisfying

$$
\forall x, y : A . (x \leq y) \lor (y \leq x)
$$

and of course given a subset $S : \mathcal{P}(A)$ and an element $x : A$ 
we say that $x$ <span class=defn>Upper Bounds</span> $S$ whenever

$$
\forall s \in S. x \geq s.
$$

A poset is called <span class=defn>Inductive</span> if every 
chain admits an upper bound. That is, if

$$
\forall C : \mathcal{P}(A) . \ulcorner C \text{ is a chain} \urcorner \to 
( \exists x : A . \ulcorner x \text{ upper bounds } C \urcorner )
$$

and lastly we say that $m : A$ is <span class=defn>Maximal</span> if 

$$
\forall x : A . x \geq m \to x=m.
$$

Then Zorn's lemma says that "every inductive poset has a maximal element". 
This is usually regarded as a nonconstructive principle, since it's 
[well known][2] to be equivalent to the axiom of choice. Thus it's remarkable 
that Johnstone proves the following meta-theorem:

<div class=boxed markdown=1>
**Proposition D4.5.14:**
Assume Zorn's Lemma[^3] holds in $\mathsf{Set}$, and let 
$\mathcal{E}$ be a localic $\mathsf{Set}$-topos[^2]. If $(A,\leq)$ is an 
inductive poset in $\mathcal{E}$, then there exists $a : 1 \to A$ which is 
(internally) a maximal element of $A$.
</div>

We would like to say "$\mathcal{E}$ models Zorn's Lemma" in the sense that 

$$
\mathcal{E} \models 
\forall (A, \leq) : \mathtt{InductivePoset} . 
\exists a : A . \ulcorner a \text{ is maximal} \urcorner
$$

but this is actually stronger in some ways, and weaker in others, than 
Johnstone's statement. 

It's stronger because of the *unbounded* internal 
quantifier "$\forall (A, \leq)$". The typical sheaf semantics for a topos 
only let us quantify over (generalized) elements of some object, whereas 
here we're quantifying over objects themselves! Certain readers might 
consider how to express this quantifier in type theory without a 
[universe][5].

You can make sense of this unbounded quantifier in two ways -- with 
[stack semantics][3] or with [universes][5]. I know the basics of each[^5], 
but I'm not totally sure how these two approaches relate/differ... 

It's weaker because of the *mere existence* of a maximal element for $A$. 
Johnstone's statement gives a *global* element $a : 1 \to A$, whereas saying 
$\exists a . \ulcorner a \text{ is maximal} \urcorner$ means that $a$ need 
only exist on a local cover (the type theorists would say that $a$ 
"merely exists"). As far as I know, the usual "set theoretic" internal logic
doesn't have a way of explicitly saying an element is global, but 
type theoretically this is exactly what $\Sigma$-types buy us! So we can 
phrase the conclusion internally as inahbitation of 
$\sum_{a : A} \mathtt{isMaximal}(a)$ to get a global $a$. 

Using the stack semantics, Simon Henry makes it seem obvious that the 
stronger version with the unbounded quantifier is true, since we can check 
truth slice by slice and each of these is localic, as a slice of 
the localic $\mathcal{E}$.

I think a similar argument would work with universes (though I'm not certain)
so that a type theorist could very succinctly express the metatheorem by saying 
that whenever Zorn's Lemma holds in the metatheory, a localic $\mathcal{E}$ 
satisfies

$$
\prod_{A : \mathtt{InductivePoset}} \sum_{a : A} \mathtt{isMaximal}(a)
$$

where $\mathtt{InductivePoset}$ is 
$\Sigma_{A : \mathcal{U}} \mathtt{isInductivePoset}(A)$ and we've rewritten 
all the earlier definitions in type theoretic language... Though someone doing
this would need to figure out if the upper bound in the definition of 
"inductive" is supposed to merely exist or if we want it to be in a 
$\Sigma$-type... I haven't thought about this, but we can probably get by 
with the stronger theorem (since it has a weaker assumption) where we only 
have mere existence for upper bounds of chains in the definition of inductive.

However, a type theorist would be very *dissatisfied* since we aren't actually 
able to exhibit a term inhabiting this type! We would have to postulate it 
in a proof assistant, since we show it's true by soem combination of 
internal and external reasoning, rather than by working internally the whole
time. This interplay between internal and external is *very* interesting, 
though, and very powerful, so every good topos theorist should try to get 
comfortable with these ideas.

Ok, we've been distracted for long enough! Let's get to the proof of the 
metatheorem, which is based on my answer [here][1], which is itself 
based on the proof Johnstone gives in D4.5.14.

$\ulcorner$
Let $(A,\leq)$ be a poset in a localic topos $\mathcal{E}$ which is 
(internally) inductive. Assume Zorn's Lemma holds in $\mathsf{Set}$.

Let $C$ be the inductive poset in $\mathsf{Set}$ whose elements are the 
subobjects of $A$ which happen to be (internal) chains. Then using Zorn's Lemma
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

<br><br><br>

TODO: Finish this proof and clean up what came before... You can probably 
do MUCH more of the reasoning internally, which should make things less 
confusing

<br><br><br>


So we want to prove, internally, that $\forall b \in A . b \geq a \to b = a$. 
Using the same internal/external yoga as before, proving this is the same is 
proving that for every map $g : V \to A$ with $V$ subterminal (read: open) and 
every $b : 1_V \to g^* A$ with $b \geq g^* a$, we must have $b = g^* a$. 
But the same argument as before will work 
(we transpose this map to get a map $V \to A$, then look at the image of 
$(A_0 + V) \to A$, which is a subobject $A_0 \cup V \rightarrowtail A$ 
containing $A_0$, thus must equal $A_0$ by maximality. Then we learn that 
$b$ is a maximal element of $A_0$, thus equals $a$ since maximal elements of 
chains are unique).
<span style="float:right">$\lrcorner$</span>

---

TODO: break up all the text above with a few pictures

TODO: mention the utility of "subterminal" and thus "localic" in this proof.

TODO: explain that you usually use zorn alongside LEM by showing that if the 
maximal element weren't what you wanted you could contradict maximality...
Say something about the Leinster ncat cafe post Matteo sent you?

---

[1]: https://math.stackexchange.com/questions/5114677/zorns-lemma-and-localic-toposes/5115004#5115004
[2]: https://en.wikipedia.org/wiki/Zorn%27s_lemma#Equivalent_forms_of_Zorn's_lemma
[3]: https://ncatlab.org/nlab/show/stack+semantics
[4]: https://mathoverflow.net/a/444719/145247
[5]: https://ncatlab.org/nlab/show/type+universe
[6]: https://arxiv.org/pdf/2202.12012
[7]: https://proofassistants.stackexchange.com/questions/942/what-is-realignment-and-is-it-useful-in-non-univalent-theories
[8]: https://grossack.site/2022/02/16/talk-practical-topos-theory
[9]: https://grossack.site/2022/12/13/internal-logic-examples
[10]: https://ncatlab.org/nlab/show/subterminal+object
[11]: https://ncatlab.org/nlab/show/principle+of+unique+choice

[^1]:
    Here, of course, a subset of $A$ is a point in the powerset 
    $\mathcal{P}(A) \cong \Omega^A$.

[^2]:
    A "localic $\mathsf{Set}$-topos" just means that there's some local $X$ 
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

