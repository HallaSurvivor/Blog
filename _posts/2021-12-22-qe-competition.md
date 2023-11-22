---
layout: post
title: Slaughtering Competition Problems with Quantifier Elimination
tags:
  - sage
  - featured
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

I'm legally required to give the following example:

The formula $\exists x . a x^2 + bx + c = 0$ (which has a quantifier)
is equivalent to the formula $b^2 - 4ac \geq 0$

As a more complicated example, we have

$$\forall x . \exists y . (x > 0 \to ax + by + xy > c)$$

is equivalent to 

$$b \geq 0 \ \lor \ c + ab \lt 0$$

Of course, this means if we want to know whether the above formula really 
is true for some choice of $a,b,c \in \mathbb{R}$, we can just plug into
this quantifier free formula and check!

Now, you might be wondering: "How did you find this quantifier free expression?",
and the answer is, of course, [sage][3]!
Sage has [interfaces][4] with a lot of pre-existing software, and for us
the relevant interface is to [QEPCAD][5], which will actually _do_
quantifier elimination for us!

To get started, you have to make sure you have qepcad installed in a way
that sage can access. You'll want to run `sage -i qepcad` just in case
(it wasn't installed for me).

Next, let's see how we eliminated quantifiers from the "more complicted example"
above!

<div class="auto">
<script type="text/x-sage">
qepcad('(A x)(E y)[x > 0 ==> a x + b y + x y > c]', vars='(a,b,c,x,y)')
</script>
</div>

Yup. It's _that_ easy! 

If you're interested in reading more about this, you should check out
[the documentation][9], but I'm also going to give a handful of examples
in the next section[^2]!

---

So then, let's slaughter some competition problems[^3]!

First, the problem that made me write this post in the first place
([here][6] is the mse link again)

<div class=boxed markdown=1>
Let $a,b \geq 0$ with $a^4 + b^4 = 17$.

Prove $15(a+b) \geq 17 + 14 \sqrt{2ab}$
</div>

This isn't given to us as polynomials, but of course it's easy for us to
fix that by rewriting it as 

$$(15(a+b) - 17)^2 \geq 14^2 \cdot 2ab$$

then we simply ask sage[^4]:

<div class="auto">
<script type="text/x-sage">
qf = qepcad_formula
a,b = var('a,b')
P = qf.and_(a >= 0, b >= 0, a^4 + b^4 == 17)
Q = qf.atomic((15 * (a+b) - 17)^2 >= 14^2 * 2 * a * b)
qepcad(qf.implies(P,Q))
</script>
</div>

We can extend this too. The asker conjectures that $(1,2)$ and $(2,1)$
are the only choices of $(a,b)$ for which we get equality. As a bonus, 
we can check this:

<div class="auto">
<script type="text/x-sage">
qf = qepcad_formula
a,b = var('a,b')
Q = qf.atomic((15 * (a+b) - 17)^2 == 14^2 * 2 * a * b)
qepcad(Q, assume=[a >= 0, b >= 0, a^4 + b^4 == 17], solution='all-points')
</script>
</div>

So we see that these really _are_ the only points where equality holds!

---

Let's take another example I remember seeing recently 
(the original mse link is [here][10]):

<div class=boxed markdown=1>
Let $x,y,z$ be positive real numbers. Show

$$
\left ( x + \frac{1}{x} \right )
\left ( y + \frac{1}{y} \right )
\left ( z + \frac{1}{z} \right )
\geq
\left ( x + \frac{1}{y} \right )
\left ( y + \frac{1}{z} \right )
\left ( z + \frac{1}{x} \right )
$$
</div>

Again, we cannot plug this into sage directly, because it's not a 
_polynomial_ inequality. But multiplying through by $xyz$ on both sides
solves that issue.

<div class="auto">
<script type="text/x-sage">
qf = qepcad_formula
x,y,z = var('x,y,z')
Q = x*y*z * (x + 1/x)*(y + 1/y)*(z + 1/z) >= x*y*z * (x + 1/y)*(y + 1/z)*(z + 1/x)
Q = qf.atomic(Q.expand())
qepcad(Q, assume=[x > 0, y > 0, z > 0])
</script>
</div>

and even though the asker doesn't mention it, one thing that Steele makes
very clear in the (excellent) book _The Cauchy-Schwarz Masterclass_ is that
whenever working with a new inequality, we should ask where it's sharp.

So we ask sage! 

It turns out this inequality is sharp at infinitely many points, so 
instead of asking for the list of all points, we ask for a geometric 
description of the solution set.

<div class="auto">
<script type="text/x-sage">
qf = qepcad_formula
x,y,z = var('x,y,z')
Q = x*y*z * (x + 1/x)*(y + 1/y)*(z + 1/z) == x*y*z * (x + 1/y)*(y + 1/z)*(z + 1/x)
Q = qf.atomic(Q.expand())
qepcad(Q, assume=[x > 0, y > 0, z > 0], solution='geometric')
</script>
</div>

Now, this admits some simplification, since we know that $x = y$ by the
second line. I'll leave it to you to figure out exactly what set this is
if you're interested.

<div class=boxed markdown=1>
As an exercise, you should be on the lookout for places to use this tool!

Next time somebody is asking about some wacky inequality, or really
_any_ question about sets definable by polynomial (in)equations in
$\mathbb{R}^n$, you should think about whether you can slaughter 
the problem without much thought by asking a computer!

As a more concrete exercise to show the flexibility of this method, 
pick your favorite theorem in euclidean geometry. Rephrase it using
coordinates, then ask sage if it's true!

As a _very_ concrete exercise, can you do this with [Ptolemy's Theorem][11]?
</div>

Also, if you find yourself using this, definitely come back and let me know!
I would love to hear about places where this comes up in the wild! 

Also also, if you have other (possibly surprising) uses for sage or other
programs that automatically answer ceretain problems, definitely let me know!
This is one of the parts of mathematical logic that I get most geeky about!

See you next time ^_^

---

[^1]:
    As a cute thought exercise, you should try to provide geometric meaning
    to this claim. It's telling us that if you take the solution set of 
    polynomial inequations, then project from $\mathbb{R}^{n+m}$ down to 
    $\mathbb{R}^n$, the resulting set is _still_ definable by polynomial
    inequations!

    This should sound somewhat miraculous, and it's worth trying out some
    

    Thankfully, by the end of the post, you'll have all the tools you need
    in order to work out some examples on your own ^_^.

[^2]:
    In fact, there are 
    $\sim \star \sim$ bonus quantifiers $\sim \star \sim$
    built into QEPCAD! For instance, we can ask for

    - "there exist exactly 5 $x$ so that $\varphi(x)$" 
        (and obviously there's nothing special about $5$)
    - "there exist infinitely many $x$ so that $\varphi(x)$"
    - "the set of $x$ so that $\varphi(x)$ is a connected set"

    and while these aren't going to be useful for the purposes of
    this post, I still wanted to mention them!

[^3]:
    I know that I'm currently treating this like a kind of party trick,
    but being able to ask a computer whether an implication between 
    polynomial inequalities is true 
    (and being able to find a counterexample if it isn't) is
    _super_ useful in practice! In fact, [André Platzer][7] at CMU 
    crucially uses this machinery in order to automatically prove that 
    robots will not bump into each other (etc.). See, for instance,
    his book _Logical Foundations of Cyber-Physical Systems_, as well as
    the accompanying lectures [on youtube][8].

[^4]:
    For some reason typing this out wasn't working for me, but using the 
    constructors directly got things going... There's probably something
    to do with the parsing that I don't understand, and this isn't too much
    of a hassle!


[1]: https://en.wikipedia.org/wiki/Quantifier_elimination
[2]: https://en.wikipedia.org/wiki/Model_theory
[3]: https://sagemath.org
[4]: https://wiki.sagemath.org/Interfaces
[5]: https://www.usna.edu/CS/qepcadweb/B/QEPCAD.html
[6]: https://math.stackexchange.com/questions/4339599/prove-15ab-ge1714-sqrt2ab
[7]: http://www.cs.cmu.edu/~aplatzer/andre.html
[8]: https://www.youtube.com/watch?v=eYfsPLl7zTk&list=PLnQeVMgmt_JdGIqhUDNoKQsPPWRjZzIo_
[9]: https://doc.sagemath.org/html/en/reference/interfaces/sage/interfaces/qepcad.html#sage.interfaces.qepcad.qepcad
[10]: https://math.stackexchange.com/questions/4303525/proving-an-inequality-with-3-variables/4303737#4303737
[11]: https://en.wikipedia.org/wiki/Ptolemy%27s_theorem
