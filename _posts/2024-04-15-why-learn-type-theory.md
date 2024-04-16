---
layout: post
title: 
tags:
  - 
---

Every topos theorist should learn type theory. 

Yes, there's the internal set theory of a topos, using 
the usual quantifiers $\forall$ and $\exists$. But these come 
with a problem:

Any time you prove a theorem that says $\exists$ or $\lor$, 
the resulting external statement is only _locally_ true on a cover!
This is frustrating if you want to show the _global_ existence of some 
object!

Enter type theory! If we use $\sum$ and $+$ instead of their 
propositional truncations $\exists$ and $\lor$, then we're able to 
keep track of more data (the global witnesses) and thus prove more 
powerful, global claims!

TODO: come up with some examples
