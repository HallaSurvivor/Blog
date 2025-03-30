---
layout: post
title: Some Doodles I'm Proud of -- The Capping Algorithm for Embedded Graphs
tags:
  - pretty-pictures
---

This will be a *really* quick one! Over the last two weeks I've been finishing 
up a big project to make [DOIs][1] for all the papers published in [TAC][2], 
and my code takes a while to run. So while testing I would hit "go" and 
have like 10 minutes to kill... which means it's time to start answering 
questions on [mse][3] again! I haven't been very active recently because I've 
been spending a lot of time on research and music, but it's been nice to 
get back into it. I'm especially proud of a few recent answers, so I think I 
might quickly turn them into blog posts like I did in the old days! 
In this post, we'll try to understand the Capping Algorithm which turns a 
graph embedded in a surface into a particularly nice embedding where the 
graph cuts the surface into disks. I drew some pretty pictures to explain 
what's going on, and I'm really pleased with how they turned out!

So, to start, what's this "capping algorithm" all about?

Say you have a (finite) graph $G$ and you want to know what surfaces it 
embeds into. For instance planar graphs are those which embed 
in $\mathbb{R}^2$ (equivalently $S^2$), and owners of [this novelty mug][4] 
know that even the famously nonplanar $K_{3,3}$ embeds in a torus[^1]:

<p style="text-align:center;" markdown=1>
<img src="/assets/images/proud-doodles/three-utilities-mug.jpg" width="50%">
</p>

Obviously every graph embeds into _some_ high genus surface -- just add an 
extra handle for every edge of the graph, and the edges can't possibly cross 
each other! Also once you can embed in some surface you can obviously embed 
in higher genus surfaces by just adding handles you don't use.

This leads to two obvious "extremal" questions:

1. What is the _smallest_ genus surface which $G$ embeds into?
2. What is the _largest_ genus surface which $G$ embeds into where all the 
handles are necessary?

Note we can check if a handle is "necessary" or not by cutting our surface 
along the edges of our graph. If the handle doesn't get cut apart then our 
graph $G$ must not have used it! This leads to the precise definition:

<div class=boxed markdown=1>
Defn: A <span class=defn>$2$-Cell Embedding</span> of $G$ in a surface $S$ 
is an embedding so that all the conected components of $S \setminus G$ are 
2-cells (read: homeomorphic to disks).
</div>

Then the "largest genus surface where all the handles are necessary" amounts 
to looking for the largest genus surface where $G$ admits a 2-cell embedding!
But in fact, we can restrict attention to 2-cell embeddings in the 
smallest genus case too, since if we randomly embed $G$ into a surface, 
there's an algorithm which _only ever decreases the genus_ and outputs 
a 2-cell embedding! So if $S$ is the minimal genus surface that $G$ embeds in, 
we can run this algorithm to get a 2-cell embedding of $G$ in $S$.

And what *is* that algorithm? It's called <span class=defn>Capping</span>,
see for instance [_Minimal Embeddings and the Genus of a Graph_][6] by 
J.W.T. Youngs. The idea is to cut your surface along $G$, look for 
anything that isn't a disk, and "cap it off" to _make_ it a disk. Then you 
repeat until everything in a disk, and you stop.

The other day somebody on mse [asked][7] about this algorithm, 
and I had a lot of fun drawing some pictures to show what's going on[^2]!
This post basically exists because I was really proud of how these drawings 
turned out, and wanted to share them somewhere more permanent, haha. 

Anyways, on with the show!

---

We'll start with an embedding of a graph 𝐺 (shown in purple) in a 
genus 2 surface:

<p style="text-align:center;">
<img src="/assets/images/proud-doodles/doodle1.png" width="75%">
</p>

we'll cut it into pieces along $G$, and choose one of our non-disk pieces 
(call it $S$) to futz with:

<p style="text-align:center;">
<img src="/assets/images/proud-doodles/doodle2.png" width="75%">
</p>

Now we choose[^3] a big submanifold $T \subseteq S$ which leaves behind cylinders 
when we remove it. Pay attention to the boundary components of $T$, called 
$J_1$ and $J_2$ below, since that's where we'll attach a disk to "cap off" 
where $T$ used to be

<p style="text-align:center;">
<img src="/assets/images/proud-doodles/doodle3.png" width="75%">
</p>

We glue all our pieces back together, but remove the interior of $T$

<p style="text-align:center;">
<img src="/assets/images/proud-doodles/doodle4.png" width="75%">
</p>

and then, as promised "cap off" the boundary components $J_1$ and $J_2$ 
with disks. Note that the genus _decreased_ when we did this! It used 
to be genus 2, and now we're genus 1!

<p style="text-align:center;">
<img src="/assets/images/proud-doodles/doodle5.png" width="75%">
</p>

Note also that $G$ still embeds into our new surface:

<p style="text-align:center;">
<img src="/assets/images/proud-doodles/doodle6.png" width="75%">
</p>

Let's squish it around to a homeomorphic picture, then do the same process 
a second time! But faster now that we know what's going on:

<p style="text-align:center;">
<img src="/assets/images/proud-doodles/doodle7.png" width="75%">
</p>

At this point, we can try to do it again, but we'll find that removing $G$ 
cuts our surface into disks:

<p style="text-align:center;">
<img src="/assets/images/proud-doodles/doodle8.png" width="75%">
</p>

This tells us the algorithm is done, since we've successfully produced a 
2-cell embedding of $G$ ^_^.

---

Wow that was a *really* quick one today! Start to finish in under an hour, 
but it makes sense since I'd already drawn the pictures and spent some time 
doing research for my answer the other day. Maybe I'll go play flute for a 
bit.

Thanks for hanging out, all! Stay safe, and see you soon ^_^

<p style="text-align:center;">
<img src="/assets/images/proud-doodles/thats-it.gif" width="50%">
</p>



---

[1]: https://en.wikipedia.org/wiki/Digital_object_identifier
[2]: http://www.tac.mta.ca/tac/
[3]: https://math.stackexchange.com/
[4]: https://games4life.co.uk/2019/10/14/st-thomas-of-canterbury-11-october-2019/
[5]: https://mathworld.wolfram.com/GraphGenus.html
[6]: https://www.jstor.org/stable/24900867
[7]: https://math.stackexchange.com/q/5050798/655547

[^1]:
    This photo of a solution was taken from [games4life.co.uk][4]

[^2]:
    You know it's funny, even over the course of drawing just these 
    pictures the other day I feel like I improved a _lot_... I have 
    half a mind to redraw all these pictures even better, but that would 
    defeat the point of a quick post, so I'll stay strong!

[^3]:
    It's possible there's a unique "best" choice of $T$ and I'm just 
    inexperienced with this algorithm. I hadn't heard of it until I 
    wrote this answer, so there's a lot of details that I'm fuzzy on. 
    
    If you happen to know a lot about this stuff, definitely let me know 
    more!
