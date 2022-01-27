---
layout: post
title: A New (to me) Perspective on Jordan Canonical Form
tags:
  - 
---

Every fd matrix (over an AC field?) admits a JCF. So it admits a basis where 
it's the sum of a diagonal matrix and a (particularly sparse) strictly upper 
triangular matrix.

A basis-agnostic way to phrase this is that every fd linear map decomposes
as a sum of two commuting maps, one of which is [semisimple] and one 
of which is nilpotent: 

$$T = T_s + T_n$$

There's a ~ bonus property ~ as well, which says that $T_s$ and $T_n$ are 
actually _polynomials_ in $T$!

This is neat, and not how I was thinking of JCF. Should make a quick post.

Exercise: Is this true for infinite dimensional linear maps? (no)


https://en.wikipedia.org/wiki/Jordan%E2%80%93Chevalley_decomposition
