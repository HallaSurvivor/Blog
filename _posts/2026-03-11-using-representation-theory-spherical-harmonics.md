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
mathematicians. I've already thought a lot about factorization 
homology, and I'm excited to spend time with people really on the 
cutting edge of that machinery.

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
