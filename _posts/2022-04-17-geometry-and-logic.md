---
layout: post
title: Using Geometry in Logic
tags:
  - 
---

One thing that I talk a lot about is the (surprisingly tight) connection
between geometry and logic. I feel like this is something that one usually 
gains an appreciation for by seeing lots of examples, and I found a particularly
simple example today [on mse][1].

For completeness, OP wanted to know how to formally derive 

<div class=boxed markdown=1>
$$
B \leftrightarrow A \land B, \ A \leftrightarrow \lnot B \vdash A
$$
</div>

and when I first saw this, I thought it looked vaguely [LEM][2]-y, so my first
question was whether it was true intuitionistically. If it _isn't_ true 
intuitionistically, I would also want to find an intuitionistic model which
invalidates it in order to give a complete answer (since I like to justify my
uses of LEM for problems like this).

But how, you might ask, does geometry come into the picture? Well, [we know][3] that
a sequent is provable intuitionistically if and only if it's valid on all 
topological spaces with the following semantics[^1]:

 - primitive propositions $A,B,C,\ldots$ are open sets
 - $\varphi \land \psi$ is the intersection of $\varphi$ and $\psi$
 - $\varphi \lor \psi$ is the union of $\varphi$ and $\psi$
 - $\lnot \varphi$ is the interior of the complement of $\varphi$
 - $\varphi$ is "true" exactly when it's the whole space
 - $\varphi$ is "false" exactly when it's the empty set

In fact, we can say more: it's enough[^4] to check when the primitive propositions
are open subsets of $\mathbb{R}$. To summarize this situation, cool kids will
say that the topological semantics of $\mathbb{R}$ are 
<span class=defn>complete</span> for intuitionistic logic.

By this completeness theorem,

$$
B \leftrightarrow A \land B, \ A \leftrightarrow \lnot B \vdash A
$$

is provable intuitionistically if and only if[^5]

 - for any two open subsets $A$ and $B$ of $\mathbb{R}$
 - if $B = A \cap B$ and $A$ is the interior of $B^c$
 - then $A = \mathbb{R}$

But now we see that we can start applying our geometric intuition to this
problem! After all, we know what open subsets of $\mathbb{R}$ look like, and
(at least for me), it's much faster to show that $A$ must be all of $\mathbb{R}$
in the above example than to look for a formal derivation.

Of course, to really answer OP's question, we _should_ provide a derivation.
It's not enough to argue abstractly that one should exist[^2], and thankfully
this is also not hard. Since we now know that the claim is true 
intuitionistically, we can switch over to a programming interpretation by 
[curry-howard][5]! Since I have a lot of experience with functional programming,
this is _also_ easier for me than working with the logic directly. The idea is
that writing programs is the same thing as writing proofs, and there's a 
totally algorithmic way to convert some code (which I'll outline below) into
the desired proof tree:

Say we have programs 

- $f_1 : B \to A \times B$ 
- $f_2 : A \times B \to B$
- $g_1 : A \to B \to 0$
- $g_2 : (B \to 0) \to A$ 

You'll recognize these as 
our assumptions (where I've unpacked the $\leftrightarrow$s). We want to build
a program of type $A$.

By $g_2$, if we can build a program of type $B \to 0$, we'll be done! But
if we're given a $b:B$, then it's almost immediate to build the desired term
as follows

$$
B 
\overset{f_1}{\longrightarrow} A \times B 
\overset{g_1 \times \text{id}_B}{\longrightarrow} \lnot B \times B
\longrightarrow 0
$$

<div class=boxed markdown=1>
As a quick exercise, you might try to write down the actual code of type $A$
in your favorite functional programming language, assuming the existence of
these functions $f_1$, $f_2$, $g_1$, and $g_2$.

If you don't have anything better to do (or if you've never done it before)
you might then convert this program into the proof tree that OP asked for.
</div>

---

This all worked out quite smoothly, since it turned out that the claim
was actually true intuitionistically. If we got a claim that _isn't_ 
intuitionistically valid, can we use geometry in order to find a model
where it's false?

The answer, of course, is "yes"! 

As an easy example, let's take double negation elimination

$$
\vdash \lnot \lnot A \leftrightarrow A
$$

under our topological interpretation, this says that 
"the interior of the complement of the interior of the complement of $A$ is $A$".
A moment's thought shows that this is the same thing as 
"the interior of the closure of $A$ equals $A$", and there are well known 
open sets which don't have this property[^3].

<div class=boxed markdown=1>
As another quick exercise, find an open set $A$ which is _not_ the 
interior of its closure! 

Then the heyting algebra of open subsets of $\mathbb{R}$ equipped with this
open set $A$ provides a countermodel for double negation elimination.
</div>

---

Another quick one tonight! I know I talk a lot about how my interests lie in
the intersection of geometry and logic, but I think it can be tricky to really
understand what that means. When I answered this mse question, I realized it 
would make a good expository post to give the general flavor of my interests. 
The fact that these things are _also_ related to functional programming and
PL theory is not an accident, and I'm also interested in those fields for
similar reasons! 

Obviously the rabbit hole goes much deeper than this. First via locales,
which are geometric objects that "classify" propositional theories, and later
via toposes, which are geoemtric objects that classify predicate (and higher order)
theories in an analogous way.
For more details about this, see Vicker's excellent paper 
_Locales and Toposes and Spaces_, available [here][7], for instance.

Stay warm, and I'll see you all soon ^_^

---

[^1]:
    Here, for simplicity, I'm identifying a formula $\varphi$ with its 
    interpretation. If you want to be less sloppy than me, you should 
    write $$[ \! [ \varphi ] \! ]$$, but this is too annoying for me to
    type in mathjax -- there aren't enough hours in the day to write

    `[ \! [ \varphi ] \! ]`

    the number of times that would be required of me.

[^2]:
    I read [a great blog post][4] a while ago which gave an analogy that now
    lives in my head rent free. If there are any readers confused by the 
    (admittedly subtle!) distinction between giving a derivation and checking
    semantically that a sequent must be valid, hopefully this analogy helps!

    <div class=boxed markdown=1>
    When asked to derive a sequent $\Gamma \vdash \varphi$, it's not enough
    to just check that it's valid semantically.

    This would be like being asked to compute the inverse of a matrix, and
    instead checking that the determinant is nonzero. Yes, this is equivalent
    to the _existence_ of an inverse, but finding the inverse itself carries
    more information!
    </div>

[^3]:
    Indeed, those open sets which satisfy this property are called
    [regular][6].

[^4]:
    It's also enough to check 
    $\mathbb{R}^n$ for any fixed $n$ (I often have $\mathbb{R}^2$ in mind),
    or $2^\omega$ cantor space, or many other concrete spaces.

[^5]:
    Again we may take, for example, $\mathbb{R}^2$, $2^\omega$, etc. instead
    of $\mathbb{R}$ if we prefer.


[1]: https://math.stackexchange.com/q/4430107/655547
[2]: https://en.wikipedia.org/wiki/Law_of_excluded_middle
[3]: https://en.wikipedia.org/wiki/Intuitionistic_logic#Heyting_algebra_semantics
[4]: https://www.hedonisticlearning.com/posts/the-pedagogy-of-logic-a-rant.html
[5]: https://en.wikipedia.org/wiki/Curry%E2%80%93Howard_correspondence
[6]: https://en.wikipedia.org/wiki/Regular_open_set
[7]: https://www.cs.bham.ac.uk/~sjv/LocTopSpaces.pdf
