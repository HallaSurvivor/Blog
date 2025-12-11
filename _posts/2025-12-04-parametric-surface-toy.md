---
layout: post
title: Parametric Surface Toy
tags:
  - 
---

Try to figure out how this blog post works: 
https://biomakerspace.org/jekyll/update/threejs/biomimicry/2018/01/27/weeds-trees-using-threejs.html

<script type="module" src="/assets/js/parametric-surface-toy/main.js"></script>

Here's the plan:

Write some code that has 3g-3 complex "sliders" that control the lengths 
and dehn twists for a genus g surface. Then draw to the screen a surface 
with the given parameters. It should be fast enough to redraw in real time
as you move the sliders.

You'll probably want to use some amount of *discrete* geometry for this, 
approximating the surface by a mesh rather than finding an equation and doing
an implicit plot? 

As a stretch goal, from the 3g-3 complex parameters try to find an 
embedding of the fundamental group into PSL(2,R) and show how the entries of 
the matrices change
