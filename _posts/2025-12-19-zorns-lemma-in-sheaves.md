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

I'm feeling type theoretic today, so let's write things up in that style.
Recall that a <span class=defn>Chain</span> in a poset $(A,\leq)$ is a 
subset[^1] satisfying

$$
\mathtt{isChain} : \mathcal{P}(A) \to \Omega
\mathtt{isChain}(C) = \forall x, y : A . x,y \in C \to x \geq y \lor y \geq x
$$

TOOD: check this against the elephant

TODO: actually..... Can we do this? I'm kind of identifying types and terms 
here, aren't I? Hm... This would definitely be ok in HoTT...

and of course given a subset $S : \mathcal{P}(A)$ and an element $x : A$ 
we say 

TODO: isUpperBound(x,S)

Finally a poset is called <span class=defn>Inductive</span> if every 
chain admits an upper bound. That is, if

TODO: inductive

With all this in hand, we're able to state Zorn's Lemma:

**Proposition D4.5.14:**
Assume the Axiom of Choice holds in $\mathsf{Set}$, and let 
$\mathcal{E}$ be a localic $\mathsf{Set}$-topos. If $(A,\leq)$ is 
an inductive poset, then there exists 

TODO: actually, this "exists $a : A$" is global, so in the internal logic 
it should be represented by a $\Sigma_{a:A} \mathtt{isMaxElement}(a)$.


TODO: copy the proof from mse, say more

---

TODO: explain that you usually use zorn alongside LEM by showing that if the 
maximal element weren't what you wanted you could contradict maximality...

Say something about the Leinster ncat cafe post Matteo sent you?

---

[1]: https://math.stackexchange.com/questions/5114677/zorns-lemma-and-localic-toposes/5115004#5115004

[^1]:
    Here, of course, a subset of $A$ is a point in the powerset 
    $\mathcal{P}(A) \cong \Omega^A$.
