---
layout: post
title: $F_2 \times F_2$ is Incoherent -- A Polite Spectral Sequence Computation
tags:
  - 
---

Yesterday I watched my friend [Jialin Wang][1] defend her thesis, 
and as part of her background section she mentioned that the group 
$F_2 \times F_2$ is *incoherent* in the sense that it has a subgroup 
that's finitely generated and not finitely presented. I was curious how 
one might prove something like this, and in the original paper 
(Stallings's [_Coherence of 3-Manifolds Fundamental Groups_][2]) this fact 
is boiled down to an "exercise which can be performed with the help of 
[a] spectral sequence". I've been slowly trying to make spectral sequences 
feel like friends, so this seemed like the perfect thing to work out quickly
and turn into a blog post! 

I've been doing a *lot* of writing lately, with two papers that I want out 
by the end of the summer *and* a new result (which will be my thesis) that 
I want out by the end of the year *and* an NSF proposal[^1], *and* even 
more stuff that I'm not talking about yet... So everyone in my life has 
heard me do nothing but complain about writing for the last month, haha. 
Weirdly, though, I've been itching to write a blog post! Maybe because it's 
so informal, or maybe because it's something I know I can *finish*, or maybe 
it's because I'm mainly sick of writing about the *same thing* all day. 
No matter what it is, I'm happy to be here, and happy to have the excuse to 
share something cool ^_^.

There's no way I can give an introduction to spectral sequences that's 
better than [Vakil's notes][3], so I won't even try. I highly recommend 
everyone give those a read at least once in your mathematical life, especially
if you're planning to do anything that might require you to actually use 
spectral sequences "in the wild". Going forwards in this post, I'll assume 
that you know the basics of what [spectral sequences][4] are, and how 
(roughly) to compute with them, but if you're feeling brave and know a bit 
about homology you can probably already understand a fair amount of the post.

---

First, though, a few words about our goal. We're trying to show that a 
product of free groups, $G = F_2 \times F_2$, is not *coherent*. To do this,
we need to find a subgroup of $G$ which is finitely generated but not 
finitely presented. Stalling's original paper tells us that we should look at 

$$
N = \langle a, c, bd \rangle \trianglelefteq F\{a,b\} \times F\{c,d\}
$$

which is the kernel of the homomorphism

$$
\begin{align}
F\{a,b\} \times F\{c,d\} &\to \mathbb{Z} \\
a,c &\mapsto 0 \\
b &\mapsto 1 \\
d &\mapsto -1
\end{align}
$$

This subgroup is obviously finitely generated (since we defined it in terms 
of $3$ generators!) so we need to show that it *isn't* finitely presented!
The key insight will be that 

<div class=boxed markdown=1>
Every finitely presented group has finitely generated $H_2$.
</div>

$\ulcorner$
Recall that the group homology $H_\bullet(G;M)$ is isomorphic to the 
"usual" homology[^2] of its [Eilenberg-MacLane Space][7] $K(G,1)$ with 
coefficients in the [local system][8] associated to the $G$-module $M$.
Now if $G = \langle x_1, \ldots, x_n \mid R_1, \ldots, R_m \rangle$ 
is finitely presented, we can explicitly build a $K(G,1)$ as follows:

First add a loop for every generator $x_i$. Then each relation $R_i$ is a
word in the generators, thus is a loop in our space, and we glue in a 
disk with boundary given by $R_i$. Note that this makes the loop vanish in 
$\pi_1$ so that we've forced the fundamental group of this space to be $G$. 
Finally we inductively add in higher cells to kill the higher 
homotopy groups, since we want our $K(G,1)$ to be aspherical.

Now we compute $H_2(G;\mathbb{Z}) = H_2(K(G,1); \mathbb{Z})$ using this 
description of the cell structure of $K(G,1)$. Since 
$G = \langle x_1, \ldots, x_n \mid R_1, \ldots, R_m \rangle$ was finitely 
presented, we see that there's $n$ many $1$-cells and $m$-many $2$-cells 
in $K(G,1)$. So the group of $2$-cycles is a subgroup of $\mathbb{Z}^m$, 
the free abelian group on our (finite) set of $2$-cells, and is itself 
finitely generated. Quotienting out the boundaries gives $H_2$, so we win
since the quotient of a finitely generated group is still finitely generated.[^3] 
<span style="float:right">$\lrcorner$</span>

<br>

So, to show that our 
$$N = \langle a, c, bd \rangle \trianglelefteq F\{a,b\} \times F\{c,d\}$$
isn't finitely presented, we just have to show its $H_2$ isn't finitely 
generated. We can simplify the discussion by computing 
$H_2(N; \mathbb{Q})$ instead, since fields make homological algebra 
*much* easier and the dimension of $H_2(N; \mathbb{Q})$ 
(as a $\mathbb{Q}$-vector space) is a lower bound on the number of generators 
for $H_2(N;\mathbb{Z})$ (do you see why?[^4]). So with this in mind 

<div class=boxed markdown=1>
It suffices to show that $H_2(N; \mathbb{Q})$ is not finite dimensional 
as a $\mathbb{Q}$-vector space!

Unless otherwise stated, all homology groups have coefficients in 
$\mathbb{Q}$ (with the trivial action) for the rest of this post.
</div>


If we could find some nice description of the isomorphism type of $N$ then 
we could maybe compute its $H_2$ directly... But why spend the effort looking?
We already have a short exact sequence

$$1 \to N \to F\{a,b\} \times F\{c,d\} \to \mathbb{Z} \to 1$$

and the homologies of $F_2 \times F_2$ and $\mathbb{Z}$ should be easier to
compute by hand. Experience shows there should be some way to relate the 
homologies of $N$, $F_2 \times F_2$, and $\mathbb{Z}$, and indeed we're saved 
by the [Hochschild-Serre Spectral Sequence][5]!

This says that whenever we have a short exact sequence

$$1 \to N \to G \to Q \to 1$$

we get a spectral sequence

$$
E^2_{pq} = H_p(Q; H_q(N)) \Rightarrow H_{p+q}(G)
$$

relating the homology of $G$ to the homologies of $Q$ and $N$.
See Ch. VII.6 in [Brown's classic textbook][6] for more details.

Concretely this means that we can compute the homology of $G$ in terms of 
"nested" homology groups: $Q$ acts on $N$ by conjugation, and this induces 
an action of $Q$ on $H_q(N)$ -- thus it makes sense to look at the homology of 
$Q$ with coefficients in $H_q(N)$! The spectral sequence gives a close 
relationship between $H_n(G)$ and the collection of "nested" homologies 
$H_p(Q; H_q(N))$ with $p+q = n$.

Precisely, the $E^2$-page of the spectral sequence is

$$
\begin{gather}
\vdots         && \vdots         && \vdots         && \vdots         && ⋰ \\
H_2(Q; H_0(N)) && H_2(Q; H_1(N)) && H_2(Q; H_2(N)) && H_2(Q; H_3(N)) && \cdots \\
H_1(Q; H_0(N)) && H_1(Q; H_1(N)) && H_1(Q; H_2(N)) && H_1(Q; H_3(N)) && \cdots \\
H_0(Q; H_0(N)) && H_0(Q; H_1(N)) && H_0(Q; H_2(N)) && H_0(Q; H_3(N)) && \cdots \\
\end{gather}
$$

In our case, we know that $Q = \mathbb{Z}$ has particularly simple homology.
Recall that a $\mathbb{Q}\mathbb{Z}$-module is just a $\mathbb{Q}$-vector space $V$ 
with a $\mathbb{Z}$ action. That is, it's just a vector space $V$ with a choice 
of automorphism $\varphi \in GL(V)$.

<div class=boxed markdown=1>
For any $\mathbb{Q}\mathbb{Z}$-module $(V, \varphi)$, we compute

$$
H_\bullet(\mathbb{Z}; V) =
\begin{cases}
V_\mathbb{Z} = V \big / (1-\varphi) V & \bullet = 0 \\
V^\mathbb{Z} = \text{Ker}(1-\varphi)  & \bullet = 1 \\
0 & \text{otherwise}
\end{cases}
$$
</div>

$\ulcorner$ 
Writing $\mathbb{Q}[t^\pm]$ for $\mathbb{Q}\mathbb{Z}$, we build a 
free resolution of $\mathbb{Q}$

$$0 \to \mathbb{Q}[t^\pm] \overset{1-t}{\to} \mathbb{Q}[t^\pm] \overset{1}{\to} \mathbb{Q} \to 0.$$

This tells us that $H_\bullet(\mathbb{Z}; V)$ is the homology of 

$$0 \to V \overset{1-t}{\to} V \to 0$$

where $t$ acts by the automorphism $\varphi$, giving the claim.
<span style="float:right">$\lrcorner$</span>

<br>

In case $V$ is finite dimensional (as a $\mathbb{Q}$ vector space), then 
it's easy to see that $\dim V^\mathbb{Z} = \dim \text{Ker} (1 - \varphi)$
and $\dim V_\mathbb{Z} = \dim \left ( V \big / \text{Im}(1 - \varphi) \right ) = \dim V - \dim \text{Im}(1 - \varphi)$
are equal, so that these two vector spaces are isomorphic.

In case $V$ is infinite dimensional, though, this can fail!
Let $V = \mathbb{Q}[t^\pm]$, of countable dimension, and let $\varphi$ be
the (invertible) "multiply by $t$" operator. The fixed points $V^\mathbb{Z}$ of 
this operator are the laurent polynomials $p$ so that $p = t \cdot p$ (read: so that 
$(1-t) \cdot p = 0$), and the only option is $p=0$. The co-fixed points
$V_\mathbb{Z}$ are given by $V \big / (1-t)$ which is isomorphic to $\mathbb{Q}$.
So $V^\mathbb{Z}$ is $0$-dimensional and $V_\mathbb{Z}$ is $1$-dimensional.

<div class=boxed markdown=1>
When $V$ is finite dimensional as a $\mathbb{Q}$-vector space we compute 

$$H_0(\mathbb{Z};V) \cong V_\mathbb{Z} \cong V^\mathbb{Z} \cong H_1(\mathbb{Z};V)$$

as vector spaces. So if these are *not* isomorphic, then $V$ must be 
infinite dimensional!

<p style="text-align:center;">
<img src="/assets/images/spectral-sequences-and-incoherence/surprise-tool-mickey-mouse.gif" width="50%">
</p>
</div>

This lets us start evaluating the terms of our spectral sequence:

$$
\begin{gather}
\vdots                  && \vdots                  && \vdots                  && \vdots                  && ⋰ \\
H_2(\mathbb{Z}; H_0(N)) && H_2(\mathbb{Z}; H_1(N)) && H_2(\mathbb{Z}; H_2(N)) && H_2(\mathbb{Z}; H_3(N)) && \cdots \\
H_1(\mathbb{Z}; H_0(N)) && H_1(\mathbb{Z}; H_1(N)) && H_1(\mathbb{Z}; H_2(N)) && H_1(\mathbb{Z}; H_3(N)) && \cdots \\
H_0(\mathbb{Z}; H_0(N)) && H_0(\mathbb{Z}; H_1(N)) && H_0(\mathbb{Z}; H_2(N)) && H_0(\mathbb{Z}; H_3(N)) && \cdots \\
\end{gather}
$$

becomes

$$
\begin{gather}
\vdots            && \vdots            && \vdots            && \vdots            && ⋰ \\
0                 && 0                 && 0                 && 0                 && \cdots \\
H_0(N)^\mathbb{Z} && H_1(N)^\mathbb{Z} && H_2(N)^\mathbb{Z} && H_3(N)^\mathbb{Z} && \cdots \\
H_0(N)_\mathbb{Z} && H_1(N)_\mathbb{Z} && H_2(N)_\mathbb{Z} && H_3(N)_\mathbb{Z} && \cdots \\
\end{gather}
$$

Moreover, we know that our 
$H_0(N; \mathbb{Q}) = \mathbb{Q}$ and 
$H_1(N; \mathbb{Q}) = N_\text{ab} \otimes \mathbb{Q} = \mathbb{Q}^3$, since 
the abelianization of $N = \langle a, c, bd \rangle$ is isomorphic to $\mathbb{Z}^3$. 
While we're here we can compute that the conjugation action of $Q = \mathbb{Z}$ 
on $N$ induces the trivial action on $H_0(N)$ and $H_1(N)$.

Since $Q = \mathbb{Z}$ is generated by the image of $b$, the conjugation 
action on $N$ is literally conjugation by $b$. On the generators we compute

- $a \mapsto b^{-1} a b = (bd)^{-1} a (bd)$ 
- $c \mapsto b^{-1} c b = c$
- $bd \mapsto b^{-1} (bd) b = bd$

In $H_0(N) = \mathbb{Q}$ the group $N$ doesn't even make an appearance, so 
the induced action is trivial. On $H_1(N) = N_\text{ab} \otimes \mathbb{Q}$ 
we need to see what the conjugation action induces on the abelianization, 
but that becomes trivial since in $N_\text{ab}$ we have $(bd)^{-1} a (bd) = a$.

Since the $\mathbb{Z}$-action is trivial on $H_0(N) = \mathbb{Q}$ and 
$H_1(N) = \mathbb{Q}^3$ we learn that 

- $H_0(N)_\mathbb{Z} = H_0(N)^\mathbb{Z} = \mathbb{Q}$
- $H_1(N)_\mathbb{Z} = H_1(N)^\mathbb{Z} = \mathbb{Q}^3$

So the $E^2$ page of our spectral sequence further reduces to

$$
\begin{gather}
\vdots     && \vdots         && \vdots            && \vdots            && ⋰ \\
0          && 0              && 0                 && 0                 && \cdots \\
\mathbb{Q} && \mathbb{Q}^3 && H_2(N)^\mathbb{Z} && H_3(N)^\mathbb{Z} && \cdots \\
\mathbb{Q} && \mathbb{Q}^3 && H_2(N)_\mathbb{Z} && H_3(N)_\mathbb{Z} && \cdots \\
\end{gather}
$$

The differential on the $E^2$ page points "up two, left one", so 
we see that every differential is $0$. In fact it's easy to see that all futher 
differentials vanish so that this is actually the $E^\infty$ page of our 
spectral sequence! General theory tells us that 
$H_n(G) = \bigoplus_{p+q = n} E^\infty_{pq}$, so we can compute
$H_n(F_2 \times F_2)$ by summing over the $n$th diagonal in the above table.

Of course, $H_n(F_2 \times F_2)$ is easy enough to compute by hand using 
the [Künneth formula][11] and the fact that $K(F_2, 1) = S^1 \vee S^1$ is 
a [bouquet][9] with two petals[^5]. So we can compute it in two ways 
(directly via Künneth and "indirectly" via the spectral sequence) and 
compare to see what it tells us about $H_\bullet(N)$!

In particular, we learn (the left isomorphism comes from Künneth and 
the right isomorphism comes from the spectral sequence):

$$
\begin{gather}
\mathbb{Q} 
&\cong 
H_0(F_2 \times F_2) 
\cong&
\mathbb{Q} \\

\mathbb{Q}^4 
&\cong
H_1(F_2 \times F_2) 
\cong&
\mathbb{Q} \oplus \mathbb{Q}^3 \\

\mathbb{Q}^4 
&\cong
H_2(F_2 \times F_2) 
\cong&
0 \oplus \mathbb{Q}^3 \oplus H_2(N)_\mathbb{Z} \\

0 
&\cong
H_3(F_2 \times F_2) 
\cong&
0 \oplus 0 \oplus H_2(N)^\mathbb{Z} \oplus H_3(N)_\mathbb{Z}
\end{gather}
$$

From the $H_2(F_2 \times F_2)$ computation, we learn that
$$H_2(N)_\mathbb{Z}$$ must be $1$ dimensional. 
But from the $H_3(F_2 \times F_2)$ computation we learn that 
$H_2(N)^\mathbb{Z}$ must be $0$ dimensional!

Since the invariants and coinvariants have different diemnsions,
our earlier discussion shows that $H_2(N)$ must be infinite dimensional!
This means $N$ cannot have been finitely presented, as desired ^_^.

---

Let's take a second to reflect on what just happened, since there were 
a decent number of moving parts.

We wanted to show that 
$$N = \langle a, c, bd \rangle \leq F\{a,b\} \times F\{c,d\}$$
is not finitely presented. First, we showed that every finitely presented 
group $G$ has finitely generated $H_2(G;\mathbb{Z})$ 
(using a concrete model of $K(G,1)$) so that it suffices to show 
$H_2(N; \mathbb{Z})$ is infinitely generated.
Since the dimension of $H_2(N;\mathbb{Q})$ is a lower bound for the number of 
$\mathbb{Z}$-generators, we can work over a field and show that $H_2(N; \mathbb{Q})$
is infinite dimensional. Next, we showed that $H_2(N)$ comes with a natural 
$\mathbb{Z}$ action, and argued that $H_2(N)$ must be infinite dimensional 
if the invariants and coinvariants $H_2(N)^\mathbb{Z}$ and $$H_2(N)_\mathbb{Z}$$
have different dimensions. Finally, using the Hochschild-Serre spectral 
sequence, we were able to compute that $H_2(N)_\mathbb{Z}$ is one dimensional 
while $H_2(N)^\mathbb{Z}$ is zero dimensional. This shows that $H_2(N)$ 
must be infinite dimensional, and we win!

This is a clever trick, and a fairly subtle one! It's something I'll have to 
try to remember, since the obvious approach is to try and compute the 
(co)invariants explicitly, but I'm not even sure[^7] how to compute the 
$\mathbb{Z}$-action on $H_2(N)$! This lets you get your hands on the 
infinite-dimensionality indirectly, which feels very useful.

Thanks for hanging out, everyone! It's wild to think that just a short week 
ago I was in Bozeman, Montana meeting a bunch of cool people and giving a 
talk about my thesis. Then all in a row over labor day weekend I had two 
little dinner parties and went to the beach to swim with leopard sharks! 
It wasn't very productive, but it was extremely good for the soul, haha. 
Now I have a few short days to try and get more done before I fly to Chicago
for the [Fall School on Quantizations and Lagrangians][14]. 
Take care all, and stay safe. We'll talk soon 💖

---

[1]: https://sites.google.com/ucr.edu/jialin-wang/home
[2]: https://www.numdam.org/item/SB_1975-1976__18__167_0.pdf
[3]: https://math.stanford.edu/~vakil/0708-216/216ss.pdf
[4]: https://en.wikipedia.org/wiki/Spectral_sequence
[5]: https://en.wikipedia.org/wiki/Lyndon%E2%80%93Hochschild%E2%80%93Serre_spectral_sequence
[6]: https://link.springer.com/book/10.1007/978-1-4684-9327-6
[7]: https://en.wikipedia.org/wiki/Eilenberg%E2%80%93MacLane_space
[8]: https://en.wikipedia.org/wiki/Local_system
[9]: https://en.wikipedia.org/wiki/Rose_(topology)
[10]: https://en.wikipedia.org/wiki/Finiteness_properties_of_groups
[11]: https://en.wikipedia.org/wiki/K%C3%BCnneth_theorem
[12]: https://en.wikipedia.org/wiki/Mayer–Vietoris_sequence
[13]: https://link.springer.com/article/10.1007/s002220050168
[14]: https://sites.google.com/view/frg-fall2025/home

[^1]:
    On the off chance the NSF still exists next year

[^2]:
    Depending on which book you read, this is either a definition or a 
    theorem. See, for instance, the Introduction or Chapter II.4 in 
    Brown's book on [Group Cohomology][6].

[^3]:
    In fact, there's a whole hierarchy of finiteness conditions on a group 
    $G$. We say that a group $G$ is "[of type $F_n$][10]" if its $K(G,1)$ has 
    a finite $n$-skeleton. That is, if there's only finitely many $0$-cells, 
    finitely many $1$-cells, ..., and finitely many $n$-cells.

    In the body we really showed that being finitely presented means being 
    type $F_2$... Well, we showed half of this. Showing the converse 
    (that $F_2$-groups are finitely presented) isn't so hard either, and 
    uses essentially the same idea.

    Note that being type $F_2$ implies that $H_2$ is finitely generated, since 
    (as we said in the main body) then $H_2$ is a quotient of a subgroup 
    of a finitely generated abelian group. But even if $G$ isn't of type 
    $F_2$, then $H_2$ might "accidentally" be finitely generated, if we have a
    big generating set but then quotient out by a similarly big set of 
    boundaries. In fact, this really does happen! Bestvina and Brady 
    constructed a group whose $H_2$ is finitely generated (indeed, whose 
    $H_n$ is finitely generated for all $n$) yet which is not finitely 
    presented! See [_Morse Theory and Finiteness Properties of Groups_][13]


[^4]:
    The universal coefficient theorem promises 
    $H_2(N;\mathbb{Q}) = H_2(N;\mathbb{Z}) \otimes \mathbb{Q}$, which kills 
    any torsion subgroups (so we don't see those generators) but keeps the 
    free abelian part.
    
[^5]:
    If this isn't obvious, it's a *fantastic* 
    exercise in algebraic topology! Can you compute the homology groups
    $H_\bullet \Big ( (S^1 \vee S^1) \times (S^1 \vee S^1) ; \mathbb{Q} \Big )$?

    Again, you'll want the [Künneth formula][11] to handle the product, and 
    then you'll want something like [Mayer-Vietoris][12] to handle the 
    wedge sums.

    To relate this to group homology, note that 
    $K(G \times H, 1) \cong K(G, 1) \times K(H, 1)$, so that the 
    Künneth formula also applies to group homology!

[^6]:
    No matter what the "junk" is, but of course you remember that it's 
    $H_0(\mathbb{Z}; H_3(N; \mathbb{Q}))$

[^7]:
    Though I gave up almost immediately, since I want this post finished so 
    I can go back to writing more important things
