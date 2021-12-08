---
layout: post
title: Talk - The Weil Conjectures and Topos Theory
tags:
  - my-talks
---

This quarter I took a class on analytic number theory with 
[Dr Lapidus][1], and as a final project I wrote up a survey
about the [Weil Conjectures][2], which were the impotus for 
[Topos Theory][3], an extremely deep subject that I'm always
trying to learn more about. For bonus points, we could give
a talk on our project, and since I'm ~~an attention whore~~
always happy to give a talk, I went for this option.

This was definitely one of the most difficult topics I've 
ever had to research for a talk, and I spent a _lot_ of 
time on it. I'm glad I did, because my knowledge of toposes,
cohomology, and their interaction has gotten much more solid.
Of course, now I'm more intimately aware of _just_ how much
more about this I have to learn. It's daunting and exciting
in equal parts!

As for the talk itself, I wanted to give some very concrete 
examples showcasing what the Weil Conjectures _say_, as well
as how we can use them to solve concrete problems. I read a 
_lot_ of papers and watched a lot of videos about them, and I
didn't see anybody giving these kinds of concrete examples. 
I'll almost certainly write up a blog post soon giving some[^1],
because the computations aren't super difficult and I think
they're worth showing.

In the associated paper, I spend some more time talking about
toposes and how they relate to the Weil Conjectures through 
their cohomology theory. The subject is so deep that it's 
hard to know exactly what to include, but I gave what I hope 
is a good introduction for beginners. 

Both the paper and the talk are based heavily on 
[this][4] excellent talk by Sophie Morel 
(for the information about the Weil Conjectures) and on
[this][5] excellent talk by Colin McLarty[^2] 
(for the historical development of toposes). There's also 
Milne's excellent paper [here][6], and you can find a more
complete bibliography in the paper[^3]. At one point, I 
cite some geometric facts about the [Grassmannians][8] 
$\mathsf{Gr}(2,4)$, and while these are well known[^4], you can
find some references for the computation [here][9], [here][10],
and [here][11].

Of course, I wasn't the only speaker today! There were other 
presentations as well. Notably [Will Hoffer][13] gave a nice talk
on [explicit formulas][14], which you can find [here][15]. Then 
[Adam Richardson][16] gave a talk generalizing these "explicit formulas"
to the setting of fractal geometry. This is one of the major subects that 
Dr Lapidus studies, and I think both of them are working with him, so it
makes sense. You can tell that they collaborated, and Will's talk was a great
setup for Adam's. As far as I know, Adam's slides are not available online,
but if he posts them somewhere I'll be sure to link them! Next was 
[Khoi Vo][17], who proved the [prime number theorem][18]. He's planning
to upload his project [here][19] sometime soon. Lastly was little old me.
It was kind of a shame, because the talks were running almost 45 minutes
behind schedule by the time it was my turn, which means I would have needed
to fit my talk into a 15 minute slot if we wanted to end on time. Of course,
that's not possible, so almost everyone had to leave either before or during
the talk. Thankfully, we recorded it so that people who are interested will
still be able to watch ^_^.

---

The Weil Conjectures and Topos Theory

The Weil Conjectures are a set of conjectures governing the number of solutions 
to diophantine equations mod $p^n$. Surprisingly, a certain generating function 
(due to Hasse and Weil) for the number of solutions is intimately related to the 
geometry of the complex solutions to the same equations! Grothendieck's famed 
"toposes" were instrumental in the formalization and solution of these 
conjectures, and remain an independently interesting topic of study to this day. 
In this talk we explain concretely what the Weil Conjectures are, then survey 
how the theory of toposes was used to solve them.

You can find the slides [here][20], the paper [here][21], and a recording
below:

<iframe width="560" height="315" src="https://www.youtube.com/embed/q2xln8f8Tg8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


---

[^1]:
    Though saying I'll write up a post on something seems to be 
    a quick way to guarantee I never actually do it, haha.

[^2]:
    _The Weil Conjecturs, from Abel to Deligne_ and 
    _Nevertheless One Should Learn the Language of Topos_ respectively

[^3]:
    It's not directly related to the Weil Conjectures, but one great paper
    I found while looking into this stuff is Connes's 
    _An Essay on the Riemann Hypothesis_, available [here][7].

[^4]:
    On this note, I really need to spend some time playing around with
    [Schubert Calculus][12]... It seems like it has the nice blend of 
    algebra and combinatorics that I've always found appealing.

[1]: https://math.ucr.edu/~lapidus/
[2]: https://en.wikipedia.org/wiki/Weil_conjectures
[3]: https://en.wikipedia.org/wiki/Topos
[4]: https://www.youtube.com/watch?v=iDgtP6ZpR70
[5]: https://www.youtube.com/watch?v=vmcbm5FxRJE
[6]: http://arxiv.org/abs/1509.00797
[7]: http://arxiv.org/abs/1509.05576
[8]: https://en.wikipedia.org/wiki/Grassmannian
[9]: https://math.stackexchange.com/questions/381345/how-to-compute-the-cohomology-ring-of-grassmannian-g4-2/1398455
[10]: https://math.stackexchange.com/questions/45292/how-to-compute-the-euler-characters-of-a-grassmannian
[11]: https://www.math.drexel.edu/~jblasiak/grassmannian.pdf
[12]: https://en.wikipedia.org/wiki/Schubert_calculus
[13]: https://willhoffer.com/
[14]: https://en.wikipedia.org/wiki/Explicit_formulae_for_L-functions
[15]: https://willhoffer.com/2021-12-07/explicit-formulae-in-number-theory/
[16]: https://adamdrichardson.com/
[17]: https://way2stars.org/
[18]: https://en.wikipedia.org/wiki/Prime_number_theorem
[19]: https://way2stars.org/research
[20]: /assets/docs/weil-conjectures-talk/slides.pdf
[21]: /assets/docs/weil-conjectures-talk/paper.pdf
