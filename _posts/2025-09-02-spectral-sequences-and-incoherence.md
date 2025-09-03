---
layout: post
title: Incoherence in Groups -- An Example with Spectral Sequences
tags:
  - 
---

Earlier today I watched my friend [Jialin Wang][1] defend her thesis, 
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
(roughly) to compute with them. 

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

After all, remember that the group homology $H_2(G;M)$ is isomorphic to the 
"usual" homology[^2] $H_2(K(G,1), M')$ where $K(G,1)$ is an 
[Eilenberg-MacLane Space][7] and $M'$ is the [local system][8] on $K(G,1)$ 
associated to the $G$-module (read: the $\pi_1(K(G,1))$-module) $M$.
So now if $\pi = \langle x_1, \ldots, x_n \mid R_1, \ldots, R_m \rangle$ 
is a finitely presented group, we build a $K(\pi,1)$ by adding a loop 
for each generator, then gluing in $m$-many $2$-cells with boundaries given 
by the $R_i$ to make the relevant product of loops bound a disk and thus 
vanish in $\pi_1$. Then we inductively add higher cells to kill the higher 
homotopy groups.

From this, we compute $H_2(\pi;\mathbb{Z}) = H_2(K(\pi,1); \mathbb{Z})$ as the 
quotient of cycles (read: chains of $2$-cells) by boundaries (of $3$-cells).
But by construction there's only finitely many $2$-cells in our $K(\pi,1)$,
so the group of chains of $2$-cells is free abelian on $m$ many generators.
This means the subgroup of $2$-boundaries is free abelian on $\leq m$-many 
generators, and quotienting out boundaries gives the homology $H_2$ as the 
quotient of a finitely generated group, so it itself is finitely generated --
as desired[^3].

<br>

So, to show that our 
$$N = \langle a, c, bd \rangle \trianglelefteq F\{a,b\} \times F\{c,d\}$$
isn't finitely presented, we just have to show its $H_2$ isn't finitely 
generated. We can simplify the discussion by computing 
$H_2(N; \mathbb{Q})$ instead, since fields make homological algebra 
*much* easier and the dimension of $H_2(N; \mathbb{Q})$ 
(as a $\mathbb{Q}$-vector space) is a lower bound on the number of generators 
for $H_2(N;\mathbb{Z})$ (do you see why?[^4])

If we could find some nice description of the isomorphism type of $N$ then 
we could maybe compute $H_2$ directly... But we have a short exact sequence

$$1 \to N \to F\{a,b\} \times F\{c,d\} \to \mathbb{Z} \to 1$$

and the homologies of $F_2 \times F_2$ and $\mathbb{Z}$ should be easier to
compute by hand. Experience shows there should be some way to relate the 
homologies of $N$, $F_2 \times F_2$, and $\mathbb{Z}$, and indeed we're saved 
by the [Hochschild-Serre Spectral Sequence][5]!

In the case of a short exact sequence 

$$1 \to N \to G \to Q \to 1$$

this says that 

$$
E^2_{pq} = H_p(Q; H_q(N; \mathbb{Q})) \Rightarrow H_{p+q}(G; \mathbb{Q})
$$

So that we can compute the homology of $G$ with coefficients in $\mathbb{Q}$ 
(with the trivial action) in terms of "nested" homology groups: The homology 
of $Q$ with coefficients in the module, which happens to itself be 
a homology group, $H_q(N; \mathbb{Q})$. In fact this is true for any coefficient 
$G$-module $M$, see Ch. VII.6 in [Brown's classic textbook][6] for more.

The $E^2$-page of this spectral sequence is

$$
\begin{gather}
\vdots                     && \vdots                     && \vdots                     && ⋰ \\
H_2(Q; H_0(N; \mathbb{Q})) && H_2(Q; H_1(N; \mathbb{Q})) && H_2(Q; H_2(N; \mathbb{Q})) && \cdots \\
H_1(Q; H_0(N; \mathbb{Q})) && H_1(Q; H_1(N; \mathbb{Q})) && H_1(Q; H_2(N; \mathbb{Q})) && \cdots \\
H_0(Q; H_0(N; \mathbb{Q})) && H_0(Q; H_1(N; \mathbb{Q})) && H_0(Q; H_2(N; \mathbb{Q})) && \cdots
\end{gather}
$$

Now, in our case, we know that $Q = \mathbb{Z}$ which has particularly 
simple homology, living only in degrees $0$ and $1$ (since the circle $S^1$ is 
a $K(\mathbb{Z},1)$). This means 
$H_0(\mathbb{Z}; \mathbb{Q}^n) \cong H_1(\mathbb{Z}; \mathbb{Q}^n) \cong \mathbb{Q}^n$.
Moreover, we know that our 
$H_0(N; \mathbb{Q}) = \mathbb{Q}$ and 
$H_1(N; \mathbb{Q}) = N_\text{ab} \otimes \mathbb{Q} = \mathbb{Q}^3$, since 
the abelianization of $N$ is isomorphic to $\mathbb{Z}^3$. 

**At this point we'll assume, towards a contradiction, that $H_2(N;\mathbb{Q})$ 
is finite dimensional.**

Now evaluating $H_0(N)$ and $H_1(N)$ and using the vanishing of 
$H_{\geq 2}(\mathbb{Z})$ we get

$$
\begin{gather}
\vdots                      && \vdots                        && \vdots                              && ⋰ \\
0                           && 0                             && 0                                   && \cdots \\
H_1(\mathbb{Z}; \mathbb{Q}) && H_1(\mathbb{Z}; \mathbb{Q}^3) && H_1(\mathbb{Z}; H_2(N; \mathbb{Q})) && \cdots \\
H_0(\mathbb{Z}; \mathbb{Q}) && H_0(\mathbb{Z}; \mathbb{Q}^3) && H_0(\mathbb{Z}; H_2(N; \mathbb{Q})) && \cdots
\end{gather}
$$

and then moving the $(-)^n$ to the outside (since $H_\bullet(\mathbb{Z};-)$ 
commutes with coproducts) and crucially using our assumption that 
$H_2(N;\mathbb{Q}) \cong \mathbb{Q}^k$ for some $k$, we get

$$
\begin{gather}
\vdots     && \vdots       && \vdots             && ⋰ \\
0          && 0            && 0                  && \cdots \\
\mathbb{Q} && \mathbb{Q}^3 && H_2(N; \mathbb{Q}) && \cdots \\
\mathbb{Q} && \mathbb{Q}^3 && H_2(N; \mathbb{Q}) && \cdots
\end{gather}
$$

The differential on the $E^2$-page points "up two, left one", so 
we see that every differential is $0$ and this is also the $E^\infty$ page.
Then the general theory of spectral sequences tells us that 
$H_n(G;\mathbb{Q} = \bigoplus_{p+q = n} E^\infty_{pq}$ -- the sum over 
the diagonals. But $H_n(F_2 \times F_2; \mathbb{Q})$ is easy enough to compute 
by hand, since $K(F_2 \times F_2, 1) = K(F_2, 1) \times K(F_2, 1)$ and we 
know that $K(F_2, 1) = S^1 \vee S^1$ is a [bouquet][9] with two petals. 

So we can compute $H_n(F_2 \times F_2)$ in two ways -- using the spectral 
sequence and using the [Künneth formula][11] -- and play those off each other 
to see what $H_2(N; \mathbb{Q})$ must be!

This gives[^5] 
(the left isomorphism is Künneth and the right is the spectral sequence):

$$
\mathbb{Q} \cong 
H_0(F_2 \times F_2; \mathbb{Q}) \cong 
\mathbb{Q}
$$

$$
\mathbb{Q}^4 \cong
H_1(F_2 \times F_2; \mathbb{Q}) \cong
\mathbb{Q} \oplus \mathbb{Q}^3
$$

$$
\mathbb{Q}^4 \cong
H_2(F_2 \times F_2; \mathbb{Q}) \cong
0 \oplus \mathbb{Q}^3 \oplus H_2(N; \mathbb{Q})
$$

$$
0 \cong
H_3(F_2 \times F_2; \mathbb{Q}) \cong
0 \oplus 0 \oplus H_2(N; \mathbb{Q}) \oplus \text{junk}
$$

From the $H_2(F_2 \times F_2$ computation we see that $H_2(N; \mathbb{Q})$
must be $1$-dimensional. But then we would learn that[^6]
$H_3(F_2 \times F_2; \mathbb{Q})$ is $H_2(N; \mathbb{Q}) \oplus \text{junk}$
must have dimension at least $1$, a contradiction!

So, finally, we've learned that our assumption was false and 
$H_2(N; \mathbb{Q})$ must actually be infinite dimensional!

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

[^1]:
    On the off chance the NSF still exists next year

[^2]:
    Depending on which book you read, this is either a definition or a 
    theorem. See, for instance, the introduction to Brown's book on 
    [Group Cohomology][6], or Chapter II.4 for a more precise treatment.

[^3]:
    In fact, there's a whole hierarchy of finiteness conditions on a group 
    $G$. We say that a group $\pi$ is "[of type $F_n$][10]" if its $K(\pi,1)$ has 
    a finite $n$-skeleton. That is, if there's only finitely many $0$-cells, 
    finitely many $1$-cells, ..., and finitely many $n$-cells.

    In the body we really showed that being finitely presented means being 
    type $F_2$... Well, we showed half of this. Showing the converse 
    (that $F_2$-groups are finitely presented) isn't so hard either, and 
    uses essentially the same idea.

[^4]:
    The universal coefficient theorem promises 
    $H_2(N;\mathbb{Q}) = H_2(N;\mathbb{Z}) \otimes \mathbb{Q}$, which kills 
    any torsion subgroups (so we don't see those generators) but keeps the 
    free abelian part.
    
[^5]:
    If the left hand side isn't obvious, this will make a *fantastic* 
    exercise in algebraic topology! Can you compute the homology groups
    $H_\bullet \Big ( (S^1 \vee S^1) \times (S^1 \vee S^1) ; \mathbb{Q} \Big )?

    Again, you'll want the [Künneth formula][11] to handle the product, and 
    then you'll want something like [Mayer-Vietoris][12] to handle the 
    wedge sums.

[^6]:
    No matter what the "junk" is, but of course you remember that it's 
    $H_0(\mathbb{Z}; H_3(N; \mathbb{Q}))$
