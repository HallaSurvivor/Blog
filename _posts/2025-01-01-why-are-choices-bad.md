---
layout: post
title: Why are "Choices" Bad?
tags:
  - 
---

In math it's not uncommong to hear people say that "choices are unnatural" 
and should be avoided. We often take our first linear algebra class and are 
thrilled to learn that every vector space is isomorphic to $\mathbb{R}^n$, 
if you just pick a basis! We also learn that bases are plentiful,
and we wonder about the point of abstract vector spaces at all. Then, in a 
second linear algebra class, we're told that picking a basis is Bad, Actually
and that we should avoid doing this whenever possible. Around this time we 
also learn about the Axiom of Choice, which we're told is controversial, or 

TODO: say more here about other examples of choice being bad. Choosing a 
chart on a manifold? Choosing a representative of an equivalence class?


Reason 1: to know that the thing we're defining doesn't depend on the choice. 
eg. defining something on $\mathbb{Q}$, we need to check that it doesn't 
depend on the choice of representative $a/b$ vs $2a/2b$, etc. 

Usually there's a "computational" definition and a "theoretical" definition. 
The first uses choices and tells you how to actually compute, so it's 
convenient for working out examples. But it's inconvenient to prove things 
with bc you have to check what you do is independent if your choice.
The second uses abstract theory to work without choices, which makes it 
convenient for proving things, but nearly impossible to compute with

(TODO: footnote on "computation" at different levels, which I want to 
write a blog post about someday)

Whenever learning something, it's important to learn _both_ the 
concrete and the theoretical definitions. Or to start, it's at least 
important to recognize which you're looking at! 

examples:
- trace/determinant (link to the xenamath post about this)
- something to do with equivalence classes in Q... or Z, even?
- projective resolutions vs derived functors 
- model structures vs oo-categories 
- local trivializations vs principal bundles
- something in harmonic analysis?
- something in undergrad level analysis?
- presentation of a group/etc vs the group itself

(TODO: a footnote, maybe, or longer if you need it, about 
presentations and bases and how usually the former is 
predicative while the latter isn't. eg, formal topology. 
You have to work harder, since you're only ever using the 
computational definition, but the upshot is that you get 
_very_ strong computability guarantees... obviously, lol.)

Also say something about how your _choice_ really matters for computation.
Depending on what you choose your life can be easy or hard (give examples, 
eg computing determinant of a diagonal vs nondiagonal matrix, a good vs a 
bad choice of projective resolution, or good vs bad groebner bases for 
an ideal)

(TODO: find a thing defined on Q that doesn't depend on the choice of 
representative and then check that it doesn't. Contrast this with a 
definition that doesn't depend on the choice)

Say something about the presentation/computational definition being 
_syntactic_ (another reason it can be treated in very weak foundations) 
while the abstract thing is _semantic_ (and is usually closer to the 
truth of what's "really going on". Eg, coordinatizing something geometric).


Reason 2: Objects in families
we need to know that our choices can be made _consistently_. 

eg
- vector bundles (maybe only defined on one open)
- pullbacks and semantics of type theory in LCCCs
- measurable functions, if we want to know that the representative of 
    $[fg]$ is the product of the representatives of $[f]$ and $[g]$.
- choosing a "cone" in a triangulated/model category functorially 
    (read: in a way compatible with the arrows)
- DEFINITELY more

Relate this to topos theory, and constructive math letting you do things 
in families "automatically"? 

Say something about AC or LEM?


https://math.stackexchange.com/questions/1703611/why-is-it-bad-to-pick-basis-for-a-vector-space
