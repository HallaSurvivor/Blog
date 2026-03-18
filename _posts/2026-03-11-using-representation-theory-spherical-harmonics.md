---
layout: post
title: Using Representation Theory -- 
    Nonabelian Fourier Theory and Spherical Harmonics
tags:
  - 
---

Recently I've been spending a ton of time learning representation 
theory and physics, since my thesis is pushing me in the direction 
of a lot of math inspired by quantum field theory. Plus, I was 
recently offered a job at Montana State University working with 
Sam Gunningham and David Ayala!! I'm ecstatic to have a position,
especially in such a friendly department with such talented 
mathematicians, and I'm trying to learn as much math as I can 
in an attempt to not totally embarrass myself when I start.

With this in mind, one perspective on representation theory that 
shows up frequently in physics is that irreducible representations 
give you access to "nonabelian Fourier theory". Recently I've become
super interested in this, and I want to write up some of the things
I've been learning. In particular, I want to do two computations 
together: First, we'll review Fourier duality for *abelian* groups 
in representation theoretic language. 

We'll start with the traditional case of functions on $S^1$, 
then handle the finite abelian group $\mathbb{Z}/2$ just to see 
the same ideas in a different setting.

Next, we'll relax the abelian assumption, and study the ring of 
functions on the symmetric group $\mathfrak{S}_3$. This will 
decompose into pieces which transform nicely under the symmetry,
and we'll see what kind of complexity the nonabelianness introduces.

Lastly, we'll apply these ideas to a more serious problem -- one would
like a notion of Fourier duality that works for the 2-sphere 
$S^2$ rather than the circle $S^1$. The 2-sphere isn't a Lie group,
but it is the *quotient* of a Lie group: $S^2 \simeq SO(3) \big / SO(2)$
(do you see why?). So we'll still be able to decompose the ring of $L^2$
functions on $S^2$ according to the $SO(3)$-symmetry, which recovers the
[spherical harmonics][1]. 

---

## The Humble Circle: $S^1$

I'm going to move fairly quickly through this material since 
I'm assuming a lot of my readers have seen it before. For 
more details you can look at essentially any good book on 
representation theory.

Concretely we're interested in decomposing the Hilbert space 
$L^2(S^1)$ into pieces which "respect the $S^1$-symmetry", and 
we expect that when we do this we'll recover the usual Fourier 
transform... To start, let's look at finite dimensional vector spaces.
The famed [Peter-Weyl Theorem][2] says that every Hilbert space 
with an $S^1$-action decomposes into a direct sum of finite 
dimensional irreducible representations, so by studying the finite 
dimensional things we're already most of the way to studying 
arbitrary Hilbert spaces!
As usual we'll write $\theta \cdot v$ for the action of 
$\theta \in S^1$ on $v \in V$. 

Now since $S^1$ is abelian the irreps are particularly simple.
For any group $G$ and any $G$-module $V$, an operator $T : V \to V$
that commutes with the $G$-action on an irreducible representation $V$
is just multiplication by a scalar $\lambda$. Indeed, since we're 
working over the algebraically closed field $\mathbb{C}$ we know that 
$T$ has an eigenvalue $\lambda$ with associated eigenvector[^1] $v_\lambda$. 
Then $T - \lambda I$ still commutes with the $G$-action, so that 
its kernel is a $G$-submodule, and now that kernel is nonempty 
(since it contains $v_\lambda$)! But we know that $V$ has no interesting
$G$-invariant submodules, since it's irreducible, so the kernel 
must be everything! Then $T - \lambda I$ is the zero map 
and $T = \lambda I$ as desired. (This is part of what's usually called 
[Schur's Lemma][3])

Now since $S^1$ is abelian any $(\theta \cdot -)$ commutes with 
the $S^1$-action[^2]! So Schur's lemma tells us that each 
$(\theta \cdot -)$ acts by a nonzero scalar, 
say $\chi(\theta) \in \mathbb{C}^\times$. Since 
$\theta \cdot (\varphi \cdot v) = (\theta + \varphi) \cdot v$ 
we see that $\chi(\theta) \chi(\varphi) = \chi(\theta + \varphi)$
is a group homomorphism $S^1 \to \mathbb{C}^\times$. In general, 
group homomorphisms $G \to \mathbb{C}^\times$ are called 
<span class=defn>Characters</span> and they're in bijection with the
irreducible representations of $G$. Determining the characters for 
a particular compact group is one place where one has to do some work,
but thankfully in the 21st century most of that work has been 
done for us and all we have to do is learn to understand the 
[Weyl Character Formula][4].

Here we'll take for granted that characters of $S^1$ are in bijection 
with $\mathbb{Z}$, where (as you probably expect) 
$\chi_n(\theta) = \exp(2 \pi i n \theta)$. So that the irreps are exactly
$V_n = \mathbb{C}$ where for $v \in V_n$ we have the action 
$\theta \cdot v = \exp(2 \pi i n \theta) v$.

So every $S^1$-representation decomposes as a (completion of) a direct 
sum of irreducible representations

$$V = \bigoplus_{n \in \mathbb{Z}} V_n^{\oplus d_n}$$

where $d_n$ is the *multiplicity* of $V_n$ in $V$. 

One fancy way to say this is that there's an equivalence of categories 

$$
\{ S^1 \text{-representations} \}
\simeq
\{ \mathbb{Z}\text{-graded vector spaces} \}
$$

which sends an $S^1$-module $V$ to the isotypic decomposition[^3]
$$V = \bigoplus_{n \in \mathbb{Z}} V_n^{\oplus d_n}$$ and whose 
inverse sends a $\mathbb{Z}$-graded vector space 
$\bigoplus_{n \in \mathbb{Z}} W_n$
to the $S^1$-module where for $w_n \in W_n$ an angle $\theta \in S^1$
acts by $\theta \cdot w_n = \exp(2 \pi i n \theta) w_n$.

This is a kind of *categorified* Fourier duality[^4], and when you 
specialize it to the *particular* representation 
$L^2(S^1) \in \text{Rep}(S^1)$ you recover the *usual* Fourier duality --
an isomorphism $L^2(S^1) \simeq \bigoplus_{n \in \mathbb{Z}} V_n$ 
where each $V_n$ arises exactly once. Analogously, you can decategorify 
further and apply this isomorphism to a *particular* function $f \in L^2(S^1)$
in order to get an equality $f = \sum_n \hat{f}(n) \exp(2 \pi i n \theta)$.

There are two things that make $S^1$ special here:

- First, $S^1$ is compact. This guarantees that its set of characters
    is *discrete* so that we get a direct sum $\bigoplus_{n \in \mathbb{Z}}$
    instead of something more complicated. Contrast this with Fourier duality 
    for the noncompact group $\mathbb{R}$ where we get a *continuum* of 
    characters $\exp(2 \pi i \xi x)$ for $\xi \in \mathbb{R}$. 

- Second, $S^1$ is abelian. This ensures that each of its irreducible 
    representations is one dimensional, which tells you that the 
    character contains all of the information. 

With this in mind, we'll see that the story of Fourier transforms works 
essentially without change for other compact abelian groups. In this post 
we'll say quite a lot of words about the nonabelian case, but the 
noncompact case scares me, so I won't say much more about it. Someday I 
need to spend a bunch of time learning about it, but unfortunately I 
haven't had the time to do that yet.

Without further ado, then:

---

## Boolean Analysis: The Case of $\mathbb{Z}/2$

We want another compact abelian group, and this is the simplest one 
around! This is also a good case to start with since Fourier duality for 
$(\mathbb{Z}/2)^n$ shows up *all the time* in computer science! Though I might
be biased in this regard since one of my favorite classes as an undergrad 
was taught by Ryan O'Donnell, who literally [wrote the book][6] on this 
topic[^5].

We want to look at $L^2(\mathbb{Z}/2)$, which is isomorphic to $\mathbb{C}^2$
of course, and we want to decompose it into pieces that are acted on nicely 
by $\mathbb{Z}/2$. The characters of $\mathbb{Z}/2$ are the group homomorphisms 
$\mathbb{Z}/2 \to \mathbb{C}^\times$, but these are in bijection with elements
$x \in \mathbb{C}^\times$ with $x^2 = 1$. There's two such elements: $\pm 1$
so the characters of $\mathbb{Z}/2$ are 

$$
\chi_\text{even} = 
\begin{cases}
0 \in \mathbb{Z}/2 \mapsto 1 \in \mathbb{C}^\times \\
1 \in \mathbb{Z}/2 \mapsto 1 \in \mathbb{C}^\times
\end{cases}
$$

$$
\chi_\text{odd} = 
\begin{cases}
0 \in \mathbb{Z}/2 \mapsto 1 \in \mathbb{C}^\times \\
1 \in \mathbb{Z}/2 \mapsto -1 \in \mathbb{C}^\times
\end{cases}
$$

This tells us that the irreducible representations of $\mathbb{Z}/2$ are 

- $V_\text{even} = \mathbb{C}$ where $\mathbb{Z}/2$ acts trivially
- $V_\text{odd} = \mathbb{C}$ where $0 \cdot v = v$ and $1 \cdot v = -v$.

As before, this tells us that the category of $\mathbb{Z}/2$-representations
is equivalent to the category of $$\{\text{even, odd}\}$$-graded vector 
spaces. If we specialize this equivalence at a particular representation 
we recover the decomposition of a $\mathbb{Z}/2$-representation into 
even and odd parts. 

For example, if we specialize this at $L^2(\mathbb{Z}/2)$ then we get the 
decomposition $L^2(\mathbb{Z}/2) = 
\mathbb{C}\chi_\text{even} \oplus \mathbb{C} \chi_\text{odd}$, so that the 
characters $\chi_\text{even}, \chi_\text{odd} : \mathbb{Z}/2 \to \mathbb{C}$ 
form a basis for functions on $\mathbb{Z}/2$.

Writing this I realized I have *so much more to say*. For instance, for a
general representation $V$ you can compute its even and odd parts by 
integrating against the relevant character. This also works more generally, 
essentially because a representation of a group gives a representation of 
the group algebra, and thus an action of the *idempotents* in the group 
algebra -- these arise by averaging over the group and give the projection 
operators onto the isotypic subspaces. This kind of idea will show up 
later in the post as well when we use the [Casimir][8] -- an element in 
the enveloping algebra of a Lie algebra -- in order to understand a 
representation of $\mathfrak{so}(3)$. In general the Casimir acts like a 
Laplacian operator, so by doing representation theory we'll be able to 
sidestep solving the partial differential equation picking out the 
harmonic functions on $S^2$! 

I wasn't able to resist writing *something* about this in the last paragraph,
but I'm still in the position of feeling bad writing anything other than 
my thesis. It's hard, but I'll resist the urge to say more... For now, haha.
There's always more blog posts to write!

---

## The Nonabelian Case: The symmetric group $\mathfrak{S}_3$

This group is still compact, so we'll still have discretely many irreps.


TODO: find irreps, 

TODO: define characters (trace), these are a basis for the 
    *center* of $L^2(G)$ (right?)

TODO: to get a basis for the whole of $L^2(G)$ 
    we should use the matrix entries. See how these transform under the 
    group action -- this is more subtle now, but still doable

---

## The Punchline: $SO(3)$ and Spherical Harmonics

TODO: What do $J_x$ and $J_y$ do to these functions?

---

<div class="linked_auto">
<script type="text/x-sage">
from sage.plot.colors import mod_one
z, theta= var('z,θ')

@interact
def _(p=slider([1..10], default=1), k=slider([-20..20], default=3), opacity=(0.6,(0.1,1))):

    # the spherical harmonic to draw
    f(z,theta) = z^p * sqrt(1-z^2)^abs(k) * exp(I * k * theta)
    

    x(z,theta) = sqrt(1-z^2) * cos(theta)
    y(z,theta) = sqrt(1-z^2) * sin(theta)

    # The sphere on which f is a function
    S = parametric_plot3d((x,y,z), (z,-1,1), (theta,0,2*pi), color='white')
    
    f_mag(z,theta) = abs(f(z,theta))
    
    # the colormap expects a python function rather than a symbolic one
    def f_phase(z,theta): 
        # the colormap expects values between 0 and 1
        val = arg(f(z,theta)) / (2*pi)
        return mod_one(val.n())

    # shift the value up by 1 so that it appears above the surface of the sphere of radius 1
    f_shift(z,theta) = 1 + f_mag(z,theta)

    # plot the magnitude of the function and use the phase to determine the color
    cm = colormaps.hsv
    F = parametric_plot3d( (f_shift*x, f_shift*y, f_shift*z), (z,-1,1), (theta,0,2*pi), color=(f_phase, cm), opacity=opacity)

    (S+F).show()

</script>
</div>


---

[1]: https://en.wikipedia.org/wiki/Spherical_harmonics
[2]: https://en.wikipedia.org/wiki/Peter%E2%80%93Weyl_theorem#Decomposition_of_a_unitary_representation
[3]: https://en.wikipedia.org/wiki/Schur%27s_lemma
[4]: https://en.wikipedia.org/wiki/Weyl_character_formula
[5]: https://en.wikipedia.org/wiki/Semisimple_representation#Isotypic_decomposition
[6]: https://www.cs.cmu.edu/~odonnell/papers/Analysis-of-Boolean-Functions-by-Ryan-ODonnell.pdf
[7]: https://www.youtube.com/playlist?list=PLm3J0oaFux3YypJNaF6sRAf2zC1QzMuTA
[8]: https://en.wikipedia.org/wiki/Casimir_element

[^1]:
    I've been reading a lot of physics lately, and the temptation to write 
    $| \lambda \rangle$ is shockingly strong. This notation took me a while
    to get used to, but now I love it. Why relegate $\lambda$ to a subscript
    on $v_\lambda$ when it's really the star of the show? Plus bra-ket 
    notation lets you name your vectors whatever you want, which appeals 
    to the computer scientist in me.

[^2]:
    Indeed if $\varphi \in S^1$ then by abelian-ness 
    $\theta \cdot (\varphi \cdot v) = \varphi \cdot (\theta \cdot v)$
    and $(\theta \cdot -)$ commutes with the $S^1$-action.

[^3]:
    It's much better to say that

    $$
    V = \bigoplus_{n \in \mathbb{Z}} \text{Hom}(V_n,V) \otimes V_n
    $$

    where $\text{Hom}(V_n,V)$ is a vector space of dimension $d_n$. 
    Writing this [isotypic piece][5] as a tensor product is canonical,
    while writing it as a direct sum $V_n^{\oplus d_n}$ requires 
    *choosing* a decomposition into summands (for essentially the same 
    reason that identifying a 2D vector space with $\mathbb{R}^2$ is 
    the same thing as a *choice* of basis). 

    With this in mind, you actually *need* to write things in this way 
    for the statement to be canonical enough to give an equivalence of
    categories. I'm glossing over this in the main body of the post in 
    the hopes that it keeps things more approachable for more readers.

[^4]:
    If I'm being entirely honest, I only know how to do this precisely 
    for finite dimensional representations. I've heard tale that you 
    can do this for more general representations that show up in 
    analysis, but I haven't spent as much time as I should looking into 
    precisely how that works.

[^5]:
    He also taught a class based on this book, whose lectures are 
    recorded [here][7]. I actually haven't watched these, but I've 
    been meaning to for *years*. 
