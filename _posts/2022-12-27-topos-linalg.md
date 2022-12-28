---
layout: post
title: Doing Linear Algebra in a Topos
tags:
  - 
---

In the [last post][1] we talked about the internal logic of topoi, and 
externalized some simple statements. But we didn't really see how to 
prove new facts from old ones by using the internal logic. Today let's 
take one of very few subjects that I actually understand (linear algebra)
and start proving things. Then we'll externalize to see what our 
(internal) theorems tell us about the objects of our topos!

---

Let's start at the beginning[^1]. 

<div class=boxed markdown=1>

An object $R$ of a topos $\mathcal{E}$ 
is called a <span class="defn">Ring Object</span> if it is equipped with
arrows 

- $+ : R^2 \to R$
- $- : R \to R$
- $\times : R^2 \to R$
- $0 : \mathbb{1} \to R$
- $1 : \mathbb{1} \to R$

satisfying the usual axioms for a (commutative) ring:

- $0 + a = a = a + 0$
- $a + (-a) = (-a) + a = 0$
- $(a + b) + c = a + (b + c)
- $a + b = b + a$
- $1 \times a = a = a \times 1$
- $(a \times b) \times c = a \times (b \times c)$
- $a \times b = b \times a$

</div>

I include these axioms, which I expect most of my readers are familiar with,
in order to make a point. They're all _equational_ in nature! That is,
they do nothing but specify what equations must hold between the operations.
Theories whose axioms are all equational are, unsurprisingly, called
<span class=defn>Equational Theories</span> or <span class=defn>Algebraic Theories</span>,
and these are some of the most simple theories that get studied.

Since these theories have very simple _syntax_ (defining axioms), they
necessarily have simple _semantics_ as well (that is, their interpretations 
in various topoi are simple to study). This is another instance of a very 
broad phenomenon in mathematics, and you can find more examples in an 
[old blog post of mine][2].

Let's contrast this with the case of fields. There's a handful of ways you
might try to write down the extra axiom:

$$(F1) \quad \quad a = 0 \lor \exists b . ab = 1$$
$$(F2) \quad \quad a \neq 0 \to \exists b . ab = 1$$
$$(F3) \quad \quad \not \exists b . ab = 1 \implies a = 0$$

Notice these are all "more complicated" than the other axioms in a way
we can make precise. They all feature logical connectives, like $\lnot$,
$\lor$, and $\to$. Not to mention an existential quantifier! 

It is for this reason that fields in a general topos are not as well 
behaved as we might like. They are a more complicated (read: nonalgebraic) 
theory and thus have more complicated semantics!

For example, say $R$ is a ring object in $\mathcal{E}$, 
$S$ is a ring object in $\mathcal{F}$, and 
$(f_*, f^*) : \mathcal{E} \to \mathcal{F}$ is a [geometric morphism][3].

Then $f_* R$ is a ring object in $\mathcal{F}$ and $f^* S$ is a ring object
in $\mathcal{E}$! The ring-ness both pushes forwards and pulls back 
under geometric morphisms. 

Contrast this with the field axioms above. Axiom $F1$ is a 
[geometric formula][4], so it pulls back under geometric morphisms,
but it can be shown that every $F1$-field is [decidable][5].
Since many objects that we _want_ to be fields are not often decidable
(for instance, the dedekind real numbers object $\mathbb{R}$) we're forced to 
consider axioms $F2$ and $F3$, which are not preserved under 
_any_ part of a geometric morphism in general!

So, perhaps counterintuitively, I think it's easier to do linear algebra over a 
ring $R$ inside a topos than it is to work over a field $k$. Obviously we can
prove more using the field axioms, but it's not obvious which of the three
(constructively inequivalent!) axiomatizations $F1$, $F2$, or $F3$ to use[^2].

Thus, for the rest of this post we'll be working with $R$-module objects,
for a fixed ring object $R$. Obviously I'll say more about what precisely 
this means, but first let's have some quick exercises which you might find
fun. 

Fair warning, these are harder than the usual problems I pose in these 
posts, but I'll include references which work out the details in case you
want to read more ^_^.

<div class=boxed markdown=1>
1. Show that the category of fields (in $\mathsf{Set}$) does not have an 
initial object.

2. Show that every category of models for some algebraic theory has 
an initial object (this might be hard to do without 
[functorial semantics][8] or something of similar strength. See Steve Awodey's 
[lecture notes on categorical logic][7], especially section TODO.)

3. Conclude that there is no algebraic axiomatization of fields.
</div>

<div class=boxed markdown=1>
Show that models of any algebraic theory is preserved under pushforward and 
pullback of a geometric morphism. You'll also want to think about 
functorial semantics for this exercise.
</div>

<div class=boxed markdown=1>
Show that the following are (constructively!) equivalent for a ring object
$R$ with $0 \neq 1$:

1. $R$ satisfies $F1$
2. $R$ is decidable and satisfies $F2$
3. $R$ satisfies $F3$ and $(\exists b . ab = 1) \lor (\lnot \exists b . ab = 1)$

In particular, $F1$ is constructively strictly stronger than $F2$ or $F3$,

For more information about these axioms, and field objects in topoi, 
see Johnstone's article [_Rings, Fields, and Spectra_][9]
</div>

---

So we want to define $R$-modules in a topos $\mathcal{E}$, but before
we can do that we need to start simpler:

<div class=boxed markdown=1>
An <span class=defn>Abelian Group</span> object in a topos $\mathcal{E}$ 
is an object $A$ equipped with arrows

- $+ : A^2 \to A$
- $- : A \to A$
- $0 : 1 \to A$

satisfying the usual (equational!) axioms for an abelian group.
</div>

From here we can give our first constructive proof! This is the key to
the definition of an $R$-module, as it is in $\mathsf{Set}$ as well:

<div class=boxed markdown=1>
Thm: The automorphisms of any abelian group $A$ form a (possibly noncommutative) 
ring $\text{End}(A)$.
</div>

$\ulcorner$
First, we need to define all of our operations. We start with

- $0(a) = 0_A$ is the constant $0_A$ function
- $1(a) = a$ is the identity function

Next, if $\varphi$ and $\psi$ are elements of $\text{End}(A)$, we define

- $(\varphi + \psi)(a) = \varphi(a) +_A \psi(a)$
- $(- \varphi)(a)
- $\varphi \times \psi)(a) = \varphi(\psi(a))$

From here it suffices to check all of the ring axioms, but these follow 
immediately from the abelian group axioms for $A$ and the category axioms of
$\mathcal{E}$. For instance:

$$
\begin{align}
((\varphi + \psi) + \chi)(a) 
&= (\varphi + \psi)(a) + \chi(a) \\
&= (\varphi(a) + \psi(a)) + \chi(a) \\
&= \varphi(a) + (\psi(a) + \chi(a)) \\
&= \varphi(a) + (\psi + \chi)(a) \\
&= (\varphi + (\psi + \chi))(a)
\end{align}
$$

so addition is associative. 

Similarly,

$$
\begin{align}
((\varphi \times \psi) \times \chi)(a) 
&= ((\varphi \circ \psi) \circ \chi)(a) 
&= (\varphi \circ (\psi \circ \chi))(a)
&= (\varphi \times (\psi \times \chi))(a)
\end{align}
$$

so multiplication is associative too.

The other axioms follow similarly

<span style="float:right">$\lrcorner$</span>

Notice that this proof feels exactly like doing "ordinary" math! There's 
very literally nothing that can distinguish it from a proof one might find
in an algebra textbook.

But since this proof is _constructive_ (in the sense that we never used 
[LEM][10] or [AC][11]), it's automatically true in every topos! 

In the _internal logic_ (which we just implicitly used) a 
"ring object in $\mathcal{E}$" feels exactly like an ordinary ring! 
Of course, once we externalize this theorem, we can see the power of 
the internal language:

<div class=boxed markdown=1>
Say that $A$ is a "sheaf of abelian groups on $X$", in the sense
that 

- $A(U)$ is an abelian group for every open set $U \subseteq X$
- there are "restriction maps" $r_{U,V} : A(U) \to A(V)$ for each $U \supseteq V$
    satisfying the compatibility conditions $r_{U,U} = \text{id}$ and 
    $r_{V,W} \circ r_{U,V} = r_{U,W}$
- if $\{ V_i \}$ is an open cover of $U$ and we have elements $a_i \in A(V_i)$
    so that for every pair $V_i, V_j$ we have 
    $r_{V_i, V_i \cap V_j} a_i = r_{V_j, V_i \cap V_j} a_j$,
    then there is a unique $a \in A(U)$ so that, for each $i$, 
    $r_{U, V_i} a = a_i$.

Then the assignment $U \mapsto \text{End}(A(U))$ is a "sheaf of rings" 
in a similar sense that I'm too lazy to write up. 
</div>

$\ulcorner$
Externalize the previous theorem in the topos $\mathsf{Sh}(X)$ of 
sheaves on $X$.
<span style="float:right">$\lrcorner$</span>

<div class=boxed markdown=1>
Say that $A$ is a [quiver representation][12] valued in abelian groups. 

Then the assignment TODO: externalize $\text{End}(A)$ 
is a ring-valued quiver representation.
</div>

$\ulcorner$
Externalize the previous theorem in the topos of presheaves on $Q$,
viewed as a category.
<span style="float:right">$\lrcorner$</span>

<div class=boxed markdown=1>
Say that $A$ is an abelian group equipped with an encoding 
$\mathtt{enc} : A \to \mathbb{N}$ so that all of the abelian group
operations are computabile in the sense that some program $\mathtt{plus}_A$
correctly computes 
$\mathtt{plus}_A(\mathtt{enc}(a), \mathtt{enc}(b)) = \mathtt{enc}(a+b)$
(and similar for $-$). 

Then the endomorphism ring $\text{End}(A)$ admits a similar encoding into
$\mathbb{N}$ and programs that compute the ring operations.
</div>

$\ulcorner$
Externalize the previous theorem in the [effective topos][13].
<span style="float:right">$\lrcorner$</span>

<div class=boxed markdown=1>
Say that $A$ is an abelian group equipped with a compatible $M$-action for some
monoid $M$.

Then $\text{End}(A)$ also admits an $M$-action compatible with the 
ring structure.
</div>

$\ulcorner$
Externalize the previous theorem in the topos of $M$-sets
<span style="float:right">$\lrcorner$</span>

Now we can clearly see one common application of the internal language.

In all of the above cases, we had some extra structure floating around
(respectively: a continuous parameter coming from $X$, a parameter 
coming from the quiver, programs to effectively compute, or an $M$ action)
and we want to know that the endomorphism ring should have this same 
structure. One of the most naive applications of topos theory is simply 
hiding this "plumbing". We work with our objects as though they're merely
sets, and as long as we pay the toll of working constructively, we can 
sleep soundly knowing that anything we build will still have the structure
we want it to have[^3].

It turns out that there's even more power latent in the internal logic,
since certain topoi satisfy ~bonus axioms~ that are false in $\mathsf{Set}$! 
For instance, if you can prove something using the bonus axiom that 
"every function $f : \mathbb{R} \to \mathbb{R}$ is continuous" then 
it's true in Johnstone's topological topos! We can then externalize this to
get a theorem about honest topological spaces. 

The search for topoi validating certain axioms is a hard one, but the 
benefits are hard to overstate! The idea is to cook up a mathematical 
universe in which a certain kind of object is particularly easy to work 
with. Then we work in that universe as long as possible, and externalize 
at the end to get a theorem that old fuddy-duddy $\mathsf{Set}$-valued 
mathematicians will care about. This has seen real traction recently with
[Homotopy Type Theory][16], which cooks up a topos[^4] where everything
has homotopy structure, and every function is continuous! This makes some
arguments much easier, by leveraging [path induction][17] or other tools, 
which are simply _false_ in $\mathsf{Set}$!



---

[^1]:
    For some sick and twisted notion of "beginning"...

[^2]:
    For a masterclass in the use of $F3$-fields (and topos theory besides), 
    see Ingo Blechschmidt's excellent thesis 
    [_Using the Internal Language of a Topos in Algebraic Geometry][6].

    You can find a quick discussion of this axiom and its utility as early as 
    section $3.3$, on page $28$ of my edition.

[^3]:
    Hopefully this also explains why so many people were looking for topoi 
    closely related to preexisting categories, such as Johnstone's 
    [_topological topos_][14] or any of the many topoi containing all the 
    manifolds (see [here][15] for an overview).

    By working in a topos we can sidestep all the usual verifications 
    that our construction still results in an object with the structure 
    that we want (a topological space, manifold, etc). 

    Though many of these topoi never _really_ caught on, I think that there's 
    still utility in the ideas. 

[^4]:
    Actually an $\infty$-topos

[1]: /2022/12/13/internal-logic-examples.html
[2]: /2021/09/07/examples-of-sns-theorems.html
[3]: nlab geometric morphism page
[4]: geometric formula
[5]: decidable object
[6]: ingo's thesis
[7]: awodey's lecture notes on categorical logic
[8]: functorial semantics
[9]: johnstone rings fields and spectra
[10]: LEM
[11]: AC
[12]: quiver representation
[13]: effective topos
[14]: johnstone's topological topos
[15]: nlab page on models for SDG
[16]: HoTT
[17]: path induction
