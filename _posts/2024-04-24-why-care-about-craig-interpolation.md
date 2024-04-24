---
layout: post
title: Why Care about the Craig Interpolation Theorem?
tags:
  - 
---

The [Craig Interpolation Theorem][1] says that whenever we can prove a 
formula $\varphi \to \psi$, there's always an "interpolant" $\rho$ whose 
variables appear in _both_ $\varphi$ and $\psi$ so that 
$\varphi \to \rho \to \psi$. In logic textbooks this is usually treated as 
a major result, but I've always struggled to understand why I should care 
about it. See, for instance, this [old MO question of mine][2]. Well, I 
was watching an interesting [talk][3] today that mentioned interpolants, 
so I decided to try looking into it agian, and it turns out there's 
_lots_ of reasons to care! In this (hopefully quick) blog post, I'll just 
say some reasons why this theorem is interesting, and outline some stuff 
you can do with it.


---

Craig:

From wikipedia, consider 
- $\varphi = \lnot (P \land Q) \to (\lnot R \land Q)$
- $\psi = (S \to P) \lor (S \to \lnot R)$

One can check that $\varphi \to \psi$, but how would you 
_intuitively explain_ this implication?

Well, it's not hard to show that $\varphi \to (P \lor \lnot R)$, and 
it's obvious that $(P \lor \lnot R) \to \psi$. So in some sense this 
formula $\rho = P \lor \lnot R)$ is "the reason" $\varphi \to \psi$. 

Say more about this. It's related to the fact that variables in $\rho$ 
are the variables in _both_ $\varphi$ and $\psi$.


Not only is this useful for getting an intuitive explanation for why an 
implication is true, it's also useful for explaining this intuition to 
a computer.

TODO: Talk some about model checking


TODO: talk some about "uniform interpolation"


TODO: Craig-Lyndon and Robinson

This becomes useful when trying to understand a contradiction. 

come up with an example of two structures which are obviously incompatible.
The interpolation theorem says that _every_ example looks kind of like 
this. There's a property true of all A-structures which is _never_ true in 
a B-structure!

So, in some sense, incompatibility of structures must be "simple".


TODO: Beth:

Much more obvious why someone would care about this. Say a logic is able to 
_implicitly_ pin down a construction. (Say some words about this).

Then it's natural to ask if the logic _explicitly_ pins it down, in the 
sense that there's a formula $\chi$ so that $P(x) \leftrightarrow \chi(x)$.


---

[1]: https://en.wikipedia.org/wiki/Craig_interpolation
[2]: https://mathoverflow.net/q/376441/145247
[3]: https://www.youtube.com/watch?v=3PWtnuEx71I
