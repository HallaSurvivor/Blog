---
layout: post
title: A Proof that there's No Constructive Proof of the Intermediate Value Theorem
tags:
  - topos-theory
---

Say that one of the first years asked you to write this, 
and it's quick so you're more than happy to!

Explain sheaf topoi, soundness/completeness for topos semantics of IHOL.

So if there *were* a constructive proof of IVT, you would have truth in 
all topoi... But we don't!

Say a few words about the usual proofs of IVT, cite Brouwer's "Five Stages"
paper as a good place to read about various constructively true weakenings,
and also figure out what's happening with Taylor's ASD proof of the IVT
in "A Lambda Calculus for Real Analysis".

<div class="linked_auto">
<script type="text/x-sage">
x = var('x')

def mkFrame(t):
    leftRising = plot(t+x+1, (x,-2,-1), ymin=-2, ymax=2)
    flat = plot(t, (x,-1,1), ymin=-2, ymax=2)
    rightRising = plot(t+x-1, (x,1,2), ymin=-2, ymax=2)
    zero = point((1-t if t<0 else -1-t, 0), size=40, color="orange")
    txt = text("t={}".format(t), (-1.5,1.5))
    return leftRising+flat+rightRising+zero+txt

frames = [mkFrame(t/10) for t in ([-5..5] + [-x for x in [-4..4]])]
a = animate(frames)
a.show()
</script>
</div>
