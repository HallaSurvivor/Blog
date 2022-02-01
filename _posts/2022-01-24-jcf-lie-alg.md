---
layout: post
title: A New (to me) Perspective on Jordan Canonical Form
tags:
  - 
---

Lie Algebras have been on my to-learn list for a fairly long time now, and
I'm finally taking a class focusing on them (and their representation theory).
[Our professor][1] is very concrete in how she presents things, and so this
class is doubling as a higher level review of some matrix algebra, which I've
been enjoying. In particular, last week we talked about the 
[Jordan Canonical Form][3] in a way that I quite liked, and which I'd never
seen before. I'm sure this will be familiar to plenty of people, but I want
to write up a thing about it anyways just in case!

When I was a freshman, I took my first linear algebra class 
(and my first proof-based class) with [Pisztora][4]. This class played a huge
part in my decision to switch from physics to math, and I've consciously kept
some of Pisztora's notational quirks throughout my career as a kind of silent
homage. 

One of the last things we did in that class was a completely constructive 
proof that every matrix (over $\mathbb{C}$) has a Jordan Canonical Form. 
We were all completely lost, and (speaking for almost all of us, I'm sure)
we loved every second of it. I wasn't planning to get misty eyed or nostalgic
while writing this post, but I really do have great memories associated with
that class.

Now then, what _is_ JCF? 

First, a very computational angle. Not every matrix can be diagonalized, so
it's natural to ask if there's a "next best thing". The answer is "yes",
and it's the JCF. When a matrix is diagonal it means that it acts just by
rescaling along some axes, given by the basis we use to diagonalize it.
The JCF lets us write _any_ matrix[^1] as a diagonal matrix, plus a few $1$s
right above the diagonal. Stealing wikipedia's example, we see that

$$
\begin{pmatrix}
 5 &  4 &  2 &  1 \\
 0 &  1 & -1 & -1 \\
-1 & -1 &  3 &  0 \\
 1 &  1 & -1 &  2
\end{pmatrix}
$$

can be "almost diagonalized" as

$$
\begin{pmatrix}
1 & 0 & 0 & 0 \\
0 & 2 & 0 & 0 \\
0 & 0 & 4 & 1 \\
0 & 0 & 0 & 4 
\end{pmatrix}
$$

Notice this is diagonal except for $1$s immediately above the diagonal. 
Moreover, the $1$ lies "between" the repeated $4$s. This is typical, in the
sense that any matrix $M$ can be brought into the following form[^2]:

<p style="text-align:center;">
<img src="/assets/images/jcf-lie-alg/jordan-blocks.png" width="50%">
</p>

where the $\lambda_k$ are eigenvalues of $M$, possibly with repetition.

This says, roughly, that we can decompose our space into disjoint subspaces. 
Then $M$ acts on each subspace by a "scale and shift" action, where 
we send $$\vec{v}_{k+1}$$ to $$\lambda \vec{v}_{k+1} + \vec{v}_k$$. The 
top basis vector, $$\vec{v}_0$$, just gets rescaled: $$M \vec{v}_0 = \lambda \vec{v}_0$$.

Then a matrix is diagonalizable if and only if each of these subspaces is 
one dimensional.

One reason to care about this is classification. If we pick some reasonable
convention for ordering the eigenvalues, then every matrix has a unique JCF,
and two matrices are similar if and only if they have the same JCF. This lets 
us solve the similarity problem in polynomial time[^3], which is quite nice.
We'll see another, more theoretical application (to lie algebras), later 
in the post.

Geometrically, I never found the scale-and-shift action of the JCF particularly 
easy to visualize, but I can at least appreciate that it's symbolically simple. 
When it comes to standard forms for matrices, I always preferred the 
[Rational Canonical Form][5], which played an important role in my 
undergraduate research in finite state automata, and whose action is extremely
easy to understand (provided you view your vectors as polynomials).

This is a nice segue into the fact that the RCF and JCF are related by a 
higher-level theorem, which is another perspective I had on the JCF going into
last week.

I don't want to go into much detail here, since I want to keep this post fairly
quick for me to write and we haven't even gotten to the main point yet. But
the idea is that the 
[fundamental theorem of fintely generated modules over PIDs][7]
(which _really_ needs a snappier name) gives us two canonical ways to 
decompose a fg PID-module: the primary decomposition, and the invariant factor
decomposition. 

Now if we view $\mathbb{C}^n$ as a $\mathbb{C}[x]$ module where
$x$ acts by some linear transformation $T$, this theorem tells us we can decompose 
$\mathbb{C}^n$ into subspaces where $T$ acts in a particularly simple way.

The primary decomposition of $\mathbb{C}^n$ provides a basis on which $T$ 
attains its Jordan Canonical Form, and the invariant factor decomposition 
provides a basis on which $T$ is in Rational Canonical Form. For more details
about the specific link between this theorem and the JCF, you might try
[this][6] nice set of notes by Kiyoshi Igusa.

---

Now for the new perspective:

Everything we've done so far has been very basis-oriented. After all, the
entire point of JCF is to find a basis which renders our favorite 
linear transformation particularly easy to study. But it's natural to look
for a basis-agnostic way of getting our hands on the information JCF 
provides. 

I had never thought to look into this, because in my mind JCF was really a 
statement about bases. After all, the main theoretical use case I had in mind 
was for similarity checking of matrices! Obviously it's useful for carrying
out concrete computations as well (for instance, in solving ODEs. See [here][8]),
but I never thought to ask if we _could_ rephrase it in a basis-agnostic way.

So what's the idea?

If we allow ourselves to use addition as well as multiplication, than the JCF
says that there's a basis which makes $T$ look like the sum of a 
diagonal matrix and a (particularly sparse) strictly upper triangular matrix.

In the example from before, we write

$$
\begin{pmatrix}
1 & 0 & 0 & 0 \\
0 & 2 & 0 & 0 \\
0 & 0 & 4 & 1 \\
0 & 0 & 0 & 4 
\end{pmatrix}

=

\begin{pmatrix}
1 & 0 & 0 & 0 \\
0 & 2 & 0 & 0 \\
0 & 0 & 4 & 0 \\
0 & 0 & 0 & 4 
\end{pmatrix}

+

\begin{pmatrix}
0 & 0 & 0 & 0 \\
0 & 0 & 0 & 0 \\
0 & 0 & 0 & 1 \\
0 & 0 & 0 & 0 
\end{pmatrix}
$$

Another way to say this is that every linear map on $\mathbb{C}^n$ 
decomposes as the sum of two commuting maps, one of which is [semisimple][9]
one of which is nilpotent:

$$T = T_s + T_n$$

It's clear that the latter matrix is nilpotent 
(after all, it's strictly upper triangular)
and that nilpotent-ness is a condition which doesn't rely on a choice of basis.

Some meditation shows that semisimplicity corresponds exactly to diagonalizability.
The following famous example should help guide your meditation. In this context
we should view it as a $2 \times 2$ Jordan block:

$$
\begin{pmatrix}
1 & 1 \\ 0 & 1
\end{pmatrix}
$$

Notice there is an invariant subspace which is not complemented. Namely 
the space $$\left \{ \begin{pmatrix} a \\ 0 \end{pmatrix} \ \middle | \ a \in \mathbb{C} \right \}$$.

Of course, semisimplicity is a much trickier notion to come up with compared
to nilpotency. But once you've seen it it's clear that it's _also_ 
basis-agnostic. 

So the whole decomposition doesn't depend on a choice of basis[^4]! This makes 
it much more amenable to generalization, and in fact it _does_ go through
in a wide variety of settings where we don't directly have access to JCF[^5]. 
See the [Jordan-Chevalley Decomposition][2].


---

[^1]: Over an algebraically closed field

[^2]: This image, like the previous example, was stolen from wikipedia

[^3]: 
    Where we gloss over some subtle details of the complexity of working 
    with exact complex numbers.

[^4]:
    In fact, there's a ~ bonus property ~ as well, 
    which says that $T_s$ and $T_n$ are actually _polynomials_ in $T$!

    I'm still too new to this to have a concrete application in mind, but
    it's an extremely cool fact which seems obviously useful on an intuitive
    level.

[^5]:
    Though, as a quick exercise, you might wonder if this goes through for
    linear maps on an _infinite dimensional_ vector space. 

    I have a counterexample in mind, though I don't actually have a formal
    proof that it has no such decomposition.

    <!-- 
      I'm thinking about the shift map $v_k \mapsto v_{k+1}$ on a space
      with basis $\{ v_k \mid k \in \mathbb{N} \}$.
    -->


[1]: https://en.wikipedia.org/wiki/Vyjayanthi_Chari
[2]: https://en.wikipedia.org/wiki/Jordan%E2%80%93Chevalley_decomposition
[3]: https://en.wikipedia.org/wiki/Jordan_normal_form
[4]: https://www.cmu.edu/math/people/faculty/pisztora.html
[5]: https://en.wikipedia.org/wiki/Frobenius_normal_form
[6]: https://people.brandeis.edu/~igusa/Math101aF07/Math101a_notesB10.pdf
[7]: https://en.wikipedia.org/wiki/Structure_theorem_for_finitely_generated_modules_over_a_principal_ideal_domain
[8]: https://math.stackexchange.com/questions/2309707/whats-the-relationship-between-the-jordan-theory-and-odes
[9]: https://en.wikipedia.org/wiki/Semisimple_operator
