---
layout: post
title: Abstraction and Problem Solving -- A Personal History
tags:
  - personal
---

I think that, on the famed spectrum between "problem solver" and "theorist"
(as put forward in Tim Gowers' [famed paper][1]), I'm more of a problem solver.
This probably comes as a surprise to a lot of people, seeing as I'm a logician,
and a category theorist at that. But looking back on things, I was drawn to
category theory because of its promise of a unifying language. For much of my
mathematical career I was unsure of what I wanted to study (I'm _still_ 
extremely interested in a fairly wide spread of subjects), and so I wanted to
focus my attention on things that were as broadly applicable as possible. In
some sense, I was learning abstractions with the hope that one day it would
make learning other things easier when I finally got around to choosing an
"actual subject" to study! This post is going to be substantially softer than
a lot of my other ones, as I'm not trying to actually exposit any mathematics
here. Instead, I want to take some time to settle my own thoughts about 
abstraction, and I want to take you all along for the ride ^_^.

---

Early days:

 - algebra and analysis, analysis prof had students teaching. This set me back.
 - I liked algebra because of axiomatic nature of it. 
    "As soon as I show something is a group, I get, for free, a bunch of info about it!"
 - Obviously knowing as many things about groups as possible will maximize my
    effectiveness when I finally _do_ meet a group in the wild!
 - I was also learning haskell, and it was a great gateway drug for category theory.
 - I think part of why I viewed CT as something "concrete" is precisely because 
    I was first grappling with it in the context of solving real programming problems with it.
 - 

Meeting Mathematical Logic:

 - I went to CMU, so logic was always "in the air" in a way that I didn't 
    really appreciate until I left.
 - As a junior I took CDM with Klaus, and learned that, as long as your
    problem has "simple enough" syntax, a computer can just tell you the answer! 
 - Again, I was drawn in because I wanted to know as many of these characterizations
    as possible, so that if I see a question in the wild that's of this form,
    I'll recognize it!
 - Lots of people at CMU were interested in PL theory, and haskell had pushed me
    in that direction as well. I knew there was a connection between CT and 
    programming languages, and I wanted to explore it. 

 - CS is an obvious source of problems, which heavy duty mathematics can help solve.
 - CDM more than anything showed me how tools from group theory, etc. can be used 
 - to solve real problems!  

AT and Homological Algebra:

 - I think an interesting case study for my "problem solving" tendencies was
     how I got into geometry.
 - I was initially disinterested in chain complexes, and homological algebra
      in its entirety, because it felt _super_ contrived. 
 - I had no idea why I should care about cohomology, but when I asked Florian,
      he told me that it solved so many problems he couldn't think of an example
      off hand. In particular, I remember him saying that you might as well ask
      what natural numbers are good for. Since I was sold on groups already,
      I set out to learn about group cohomology in the hopes that it would give
      me a real problem that cohomology solves. It didn't, but after a few years
      of struggling, I think I finally understand (link your MSE post).

 - only interested in cohomology _after_ I was given the promise of widespread utility
    
 - Also my senior year was DST and descriptive combinatorics. 
    Finally, concrete problems that I enjoyed solving... but measure theory 
    was an absolute _must_. This is the class that made me realize that I 
    really do need to know analysis, and it was only now (in the interest of
    solving real problems) that I began the (painful) process of "catching up"
    on analysis.

 - At this point I was also firmly interested in CT for its own sake. 
    Categorical logic was independently beautiful, and I kept hearing people
    talk about topoi... 

 - got interested in algebraic geometry not for its own sake, but so I could see
 - how people in the past have used the stuff I'm _really_ interested in
 - (topoi, category theory, etc) to solve _real problems_. The dream is that by
 - understanding these, I would have a better idea of how to solve _other_
 - problems myself!

 - nice example is kan extensions, or (co)end calculus, both of which are
 - often called useful, but neither of which I've been able to really focus on
 - because it always seems slightly too abstract.

 - wasn't interested in set theory until I heard about forcing. A super flexible
 - technique for showing that things can't be proven, or, more interestingly for
 - me, for custom building models of set theory where certain "nice" properties
 - are true (eg. solovay's model, where all subsets of R are measurable, BP, etc).
 -
 - It was the sales pitch of combining a knowledge of forcing, to custom build 
 - a universe where some claim is true, plus various absoluteness theorems, 
 - which let you trasnfer truth in the custom world to truth in the "real world"
 - that I finally got interested in set theory.
 -

 - I got interested in independence results and set theory _again_ when I 
 - was taking a measure theory class at UCR. .... Remember why you were interested
 - in RV Measurables... Maybe check your emails to Kelliher? 
 - Anyways, this was independent.
    
    
    
     

Other interests:

 - ggt, which seems to show up _everywhere_. For instance, in DST, as well
 - as in the study of FO theory of free groups.

 - ergodic theory, which is often touted as an _extremely_ fertile source of 
 - surprising solutions to difficult problems in surprisingly disparate areas of math

 - same thing with fourier analysis. 

When learning a new branch of math, I always have the question of
"why would someone from subject X care about this?". In part because I'm
a teacher, and in part because I feel a burden to explain how everything I 
learn can be used to solve problems.

This is probably in part because, as a category theorist, I get asked
"why should I care?" more often than I get asked literally any other question.

Because of this, I have an answer to a lot of these kinds of questions,
and I'm always surprised when I ask people why I should care, or what
concrete problems can be solved with some high powered machinery, or how a certain
branch of math interacts with other ones, or how/where a certain gadget arises in practice
(all of which I view as value-neutral questions), and (many) mathematicians 
don't have a good answer[^1].

---

[^1]:
    Mention you're thinking about starting a series answering these kinds of 
    questions.

[1]: https://www.dpmms.cam.ac.uk/~wtg10/2cultures.pdf
