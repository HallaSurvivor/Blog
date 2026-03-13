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

Anyways, one perspective on representation theory that I think I've 
de-emphasized for a long time is that irreducible representations 
give you access to "nonabelian Fourier theory". Recently I've become
super interested in this, and I want to write up some of the things
I've been learning. In particular, I want to do two computations 
together: First, we'll review Fourier duality for *abelian* groups 
in representation theoretic language. 

We'll start with the traditional case of functions on $S^1$, 
then handle the finite abelian groups $\mathbb{Z}/n$ just to see 
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

Consider the humble circle. 

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

TODO: check that characters are in bijection with irreps

Here we'll take for granted that characters of $S^1$ are in bijection 
with $\mathbb{Z}$, where (as you probably expect) 
$\chi_n(\theta) = \exp(2 \pi i n \theta)$.





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
