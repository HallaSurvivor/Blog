---
layout: post
title: Slaughtering Competition Problems with Quantifier Elimination
tags:
  - sage
---

Anytime I see questions on mse that ask something "simple", I feel a
powerful urge to chime in with "a computer can do this for you!". 
Obviously if you're a researching mathematician you shouldn't waste your
time with something a computer can do for you, but when you're still 
learning techniques (or, as is frequently the case on mse, 
solving homework problems), it's not a particularly useful comment
(so I usually abstain). The urge is _particularly_ powerful when it 
comes to the contrived inequalities that show up in a lot of competition math, 
and today I saw [a question][6] that _really_ made me want to say something
about this! I still feel like it would be a bit inappropriate for mse, but
thankfully I have a blog where I can talk about whatever I please :P
So today, let's see how to hit these problems with the proverbial nuke 
that is [quantifier elimination][1]!

I want this to be a fairly quick post, so I won't go into too much detail. 
The gist is the following powerful theorem from [model theory][2]:

<div class=boxed markdown=1>
<span class=defn>Tarski-Seidenberg Theorem</span>[^1]

If $\varphi$ is any formula of the form

- $p(\overline{x}) = 0$, for $p \in \mathbb{R}[\overline{x}]$
- $p(\overline{x}) \lt 0$, for $p \in \mathbb{R}[\overline{x}]$
- combinations of the above using $\lor$, $\land$, $\lnot$, $\to$
- combinations of the above using $\exists$ and $\forall$

Then $\varphi$ is equivalent to a formula _without_ quantifiers.
</div>

I'm legally required to use the following example:

The formula $\exists x . a x^2 + bx + c = 0$ (which has a quantifier)
is equivalent to the formula $b^2 - 4ac \geq 0$

As a more complicated example, we have

$$\forall x . \exists y . (x > 0 \to ax + by + xy > c)$$

is equivalent to 

$$b \geq 0 \lor c + ab \lt 0$$

Of course, this means if we want to know whether the above formula really 
is true for some choice of $a,b,c \in \mathbb{R}$, we can just plug into
this quantifier free formula and check!

Now, you might be wondering: "How did you find this quantifier free expression?",
and the answer is, of course, [sage][3]!
Sage has [interfaces][4] with a lot of pre-existing software, and for us
the relevant interface is to [QEPCAD][5], which will actually _do_
quantifier elimination for us!

To get started, you have to make sure you have qepcad installed

---

[^1]:
    As a cute thought exercise, you should try to provide geometric meaning
    to this claim. It's telling us that if you take the solution set of 
    polynomial inequations, then project from $\mathbb{R}^{n+m}$ down to 
    $\mathbb{R}^n$, the resulting set is _still_ definable by polynomial
    inequations!

    This should sound somewhat miraculous, and it's worth trying out some
    concrete examples to see just how shocking it is! 

    Thankfully, by the end of the post, you'll have all the tools you need
    in order to work out some examples on your own ^_^.



[1]: https://en.wikipedia.org/wiki/Quantifier_elimination
[2]: https://en.wikipedia.org/wiki/Model_theory
[3]: https://sagemath.org
[4]: https://wiki.sagemath.org/Interfaces
[5]: https://www.usna.edu/CS/qepcadweb/B/QEPCAD.html
[6]: https://math.stackexchange.com/questions/4339599/prove-15ab-ge1714-sqrt2ab
