---
layout: post
title: "Talk -- What is Algebraic Geometry and Why Should You Care?"
tags:
  - my-talks
---

So an _embarrassing_ amount of time ago (Feburary 17?) I gave a talk for the 
undergraduate math club titled 
"What is Algebraic Geometry, and Why Should You Care?". I think it went quite
well, and the audience seemed like they had a good time. I really wanted to 
have the talk recorded, since this is _exactly_ the kind of talk I would have 
wanted to see as an undergrad and I think it should be available to more people.
Unfortunately we weren't able to make it happen, so we'll have to wait until 
the next time I give this talk[^1]. 

I actually told the audience that I would have a blog post with the slides 
posted later that night, but uh... clearly that didn't happen, haha. In my 
defense, I really wanted to add some sage code to this post in order to 
replicate some of the demos that I did during the talk, and to let readers 
play around with some of this stuff themselves. I never really built up the 
energy to write those demos, and I picked up two more projects along the way[^2]
so the post never got made.

Well the other day I bumped into some students from the math club, and 
they teased me for never posting the slides! To be totally honest, I was 
surprised that they had noticed, haha. I'm happy to see that people were 
actually interested in reading them, so that interaction was exactly the 
motivation I needed to finally post this! The unfortunate fact, though, 
is that I'm still to busy to really make the demos as nice as I would like 
to... So we're going to have to go without. You can see the kind of thing 
I would have made at an old blog post [here][1], and you can imagine 3d 
versions of some of the pictures in the slides.

---

As a quick summary of what's _in_ the talk, I make an analogy to 
linear algebra (which is about as elementary as I think you can go 
while still giving an honest look into how the machinery works). Here 
we study a close connection between the _algebra_ of linear equations 
and the _geometry_ of linear subspaces! We can build a dictionary between 
these two worlds where, loosely:

- Geometry provides the intuition for what the algebra is "doing"
- Algebra provides the machinery which lets us do computations with the geometry

So the geometers want powerful algebra to solve their problems, and conversely 
the algebraists want to make more general ideas of "geometry" that allow them 
to visualize the algebra they're studying abstractly[^3]. Then the geometers 
start studying these more complicated structures as geometry, and they ask 
for more algebra to study them, but then these newer more complicated 
algebraic gadgets work in more general settings, so we build a more general 
notion of "geometry" to visualize all of them at once, and so on.

Round and round we go, until we get to today, where algebraic geometry has a 
fearsome reputation for being incredibly abstract and challenging[^4]. Our 
"geometric objects" are now things like [schemes][4] and [topoi][2] and 
[stacks][3] and they're valued with points in an arbitrary ring 
(as opposed to the classical case of complex numbers), and it's hard to believe 
that anyone can reasonably say they're doing "geometry" when studying these.
But of course, with practice, you really _can_ come to visualize these 
objects! They really _do_ deserve to be called geometric! And the benefit of 
taking the time to do this is that suddenly _everything_ feels like it has 
geometric content, and the whole of math (well, a lot of it at least) becomes 
more fun!

Perhaps most surprisingly, though, is that these high abstraction notions of 
"geometry" really _solve problems_. This is something I emphasize at the 
end of the talk, since I think that beautiful math should solve problems, 
and it's important to remember how these computations tether us to reality!

<br>

At the most basic level, the theory of [gröbner bases][5] allow us to 
computationally solve polynomial equations! This is useful almost everywhere 
in the real world, since polynomials arise naturally in physics, engineering, 
and really _anywhere_ math is used to model the world!

<br>

Then we have "middle abstraction" tools from algebraic geometry, like 
schemes. These arise naturally as limiting cases of "honest" geometric 
objects, and they remember more information that the naive approach to 
these situations.
Importantly this bonus information helps us solve problems! For instance, 
if we intersect the parabola $y = x^2$ with the line $y=0$, we 
get a single point $(x,y)=(0,0)$. However, this "single point" should really 
be counted twice if we want to make our formulas work properly. 

Geometrically this is because if we wiggle the $y=0$ line slightly[^5] 
we actually get TWO intersection points ($y=\epsilon$ intersects $y = x^2$ 
at $\pm \sqrt{\epsilon}$ for each $\epsilon \neq 0$) and we want the number 
of intersection points to be _continuous_. 

But even though this single point (viewed as a "classical" geometric object) 
doesn't know it, if we take the intersection as _schemes_ 
(the more advanced geometric object) we remember more about where we came 
from, and the scheme "has one point" but that point "counts twice"!

Indeed, the ring $k[x,y] \big (y = x^2, y = 0)$ gives the intersection, 
and this becomes $k[x] \big / (x^2 = 0)$. This has a single point[^6] yet 
it's 2-dimensional (it has a basis $\{1,x\}$). The nilpotency of $x$ says 
our scheme sees something "infinitesimally bigger" than just the point $x=0$.
In fact, it "remembers" that it came from the intersection of a curve with 
its tangent line (that is, we get not just a point of intersection, but an 
infinitesimally small "line segment" of intersection)! 

Much of this "middle abstraction" level is learning to visualize these 
infinitesimals and other similar phenomena, which (as we've seen) 
contain the answer to many geometric problems[^7]!

<br>

Finally the "high abstraction" machinery, like stacks allow us 
to solve problems for whole _families_ of geometric objects at once. I won't 
say more about this here, since I want this post to be fairly short, but the 
relevant buzzword is "moduli stack". These are geometric objects where a 
single point can still "have symmetry". 

Separately, topoi are geometric objects which are characterized not by 
their points, but by their [_sheaves_][8]. Sheaves are certain objects 
associated to a geometric space, and we can rephrase a lot of geometry 
in terms of operations on sheaves. A (grothendieck) topos, then, is a 
category of sheaves that "looks like" a category of sheaves on some 
geometric space. Then we can pretend that it really _is_ sheaves on some 
space, and use the fact that we can do geometry in terms of just sheaves 
in order to ask what properties this space must have! 

This turns out to be extremely useful, even for surprisingly simple to 
state problems. After all, hard problems demand hard solutions, and 
sometimes easy to state problems are still hard to solve! 
[Fermat's Last Theorem][9], for instance, is famously easy to state,
but requires the use of both stacks _and_ topoi in order to complete 
the proof!

<br>

Lastly, I invite the people who have tuned out[^8] to tune back in for 
a more concrete ending to the talk. We show how to use a simple idea from 
algebraic geometry in order to classify all pythagorean triples! The fact 
that geometry should be useful here is surprising, and this is a very 
concrete example which forms the inspiration for the very fruitful subject 
of [arithmetic geometry][10].

---

As usual, here is the title and abstract, and slides are available 
[here][11].

What is Algebraic Geometry, and Why Should You Care?

Algebraic Geometry, at its core, is the study of solutions of polynomial 
equations. However in the 20th century it gained a reputation for both its 
abstraction and difficulty. In this talk we will outline what connects 
algebra and geometry, and explain what led to the explosion in abstraction 
that occurred in Grothendieck's school. We will end the talk with some 
applications in both pure and applied math. We assume no prerequisites at all, 
except possibly some linear algebra.

---

[^1]:
    It went well enough that I'll probably add it into my list of 
    "talks I'm happy to give without much preparation", so there's 
    likely to be more opportunities.

[^2]:
    Both of which are super interesting problems, that I'll likely talk about 
    someday, but neither of which I'm comfortable talking about right now.

[^3]:
    Since this can help them intuit what's true!

[^4]:
    Which is somewhat well deserved, but I would argue it's no harder than 
    what a lot of functional analysts get up to...

[^5]:
    Grown-up mathematicians would probably prefer I say "perturb" instead 
    of "wiggle", but they can get over it.

[^6]:
    If you're in the know, this means "a single prime ideal". See 
    [here][6], for instance.

[^7]:
    In fact, this scheme-theoretic intersection _still_ doesn't always 
    compute intersections properly... In some extreme situations it 
    still "forgets too much". This is one of the motivations behind the 
    "high abstraction" notion of [derived algebraic geometry][7], which 
    is even harder to visualize (I certainly can't... At least not yet) 
    but which correctly solves _even more problems_!

[^8]:
    And anyone who tuned out for some of this discussion of high abstraction 
    tools would of course be completely forgiven!

[1]: /2021/11/16/dense-pythagorean-triples.html
[2]: https://en.wikipedia.org/wiki/Topos
[3]: https://en.wikipedia.org/wiki/Stack_(mathematics)
[4]: https://en.wikipedia.org/wiki/Scheme_(mathematics)
[5]: https://en.wikipedia.org/wiki/Gr%C3%B6bner_basis
[6]: https://math.stackexchange.com/questions/2139078/kx-x2-has-only-one-prime-ideal
[7]: https://en.wikipedia.org/wiki/Derived_algebraic_geometry
[8]: https://en.wikipedia.org/wiki/Sheaf_(mathematics)
[9]: https://en.wikipedia.org/wiki/Fermat%27s_Last_Theorem
[10]: https://en.wikipedia.org/wiki/Arithmetic_geometry
[11]: /assets/docs/ag-for-undergrads/ag-talk.pdf
