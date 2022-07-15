---
layout: post
title: Embedding Dihedral Groups in Vanishingly Small Symmetric Groups
tags:
  - sage
  - pretty-pictures
---

After the long and arduous process of writing my previous posts on
homotpy theories and $\infty$-categories, it's nice to go back to a
relaxed post based on an [mse question][1] I answered the other day.
Nature is healing ^_^. 

This post was asking about the smallest set certain groups can faithfully
act on. I actually wrote about this same idea almost exactly a year ago
in a blog post [here][2], and while answering this question I remembered 
that I wanted to follow up on that post. I mentioned some asymptotic result
at the end of it that's super hard to use, 
and I was sure I could get a more legible result if I wanted to[^1].

Well, when I saw this post I was reminded that I want to!

---

First, let's recall what question we want to answer:

In the [last post][2], we showed that the dihedral group of an $n$-gon's symmetries
$$D_{2n}$$ can embed into the symmetric group $$\mathfrak{S}_m$$ even if $m \lt n$.
For instance, $$D_{2 \cdot 6} \hookrightarrow \mathfrak{S}_5$$.

A perfectly natural question, then, is _how much smaller_ can we make this?

We showed that if $n = \prod p_i^{k_i}$ is the prime factorization of $n$,
then $D_{2n} \hookrightarrow \mathfrak{S}_{\sum p_i^{k_i}}$. 
For instance, since $6 = 2 \cdot 3$, we have 
$$D_{2 \cdot 6} \hookrightarrow \mathfrak{S}_{2+3} = \mathfrak{S}_5$$.

With this in mind, it seems entirely believable that we can get the ratio to
be _very_ small.

As is usually the case, before trying to prove this, I wanted to compute 
some values and see how quickly things are decreasing. This wasn't really 
necessary in hindsight, but it did make for some pretty pictures!

---

First, here's a plot of the minimal $m$ so that $D_{2n} \hookrightarrow \mathfrak{S}_m$[^3].

TODO: a scatter plot of m vs n

You can see that the maximal values are always $m=n$, which occurs at all the
prime powers. However, you can _also_ see that the minimal values can be 
substantially smaller.

To get a handle on just how much smaller, let's plot the ratios $m/n$ instead

TODO: that

and then let's take the minimal ratio we've seen so far

TODO: that

I would love to find a nice curve upper bounding this last scatter plot,
but it seems like a possibly tricky problem in number theory. Formally:

<div class=boxed markdown=1>
Define

$$f(n) \triangleq \text{min}_{\prod p_i^{k_i} \leq n} \frac{\sum p_i^{k_i}}{\prod p_i^{k_i}}$$

Can you find asymptotics for $f$?
</div>

If anyone wants to take a stab at this, I would love to hear what you find ^_^.

---

Whatever the asymptotics are, it's clear that $f(n) \to 0$. That is,
for any $\epsilon$ you like, there's a dihedral group $D_{2n}$ embedding into
a symmetric group $\mathfrak{S}_{n \epsilon}$. I don't know why, but this 
feels remarkable to me. It says that somehow asymptotically, we can get away
with practically no objects at all in order to faithfully represent a dihedral
group action. Said another way, there's some $n$-gon whose symmetries can be
faithfully represented in the symmetries of only $\frac{n}{1000000}$ many points.


For completeness, let's give a quick proof of this fact. It's fairly easy, 
so I encourage you to try it yourself! In fact, it's quite easy to prove
various strengthenings of this fact. For instance, the proof we're about 
to give shows that we can take $n$ to be a product of $2$ primes, and is
easily tweaked to allow us to put lots of bonus conditions on the prime
factorization of $n$.

$\ulcorner$
TODO: this
<span style="float:right">$\lrcorner$</span>

---

This was an exciting post because it gave me an excuse to submit another
sequence to the OEIS. The inputs for which $f(n)$ changes are 
interesting, but were not in the OEIS already, so I submitted them 
while I was writing this up! If all goes well, they should be available as 
[A354424][3] in the near future[^2]. 

It's also nice to go back to an older post and give it the closure it really
deserves. The asymptotic result I cited there is borderline unusable, and
this post answers the question that I really _wanted_ to ask in that post.

It's off to bed, though. A close friend is visiting me tomorrow, and I want to make 
sure she has all the time she deserves!

Take care, and stay safe all ^_^. Talk Soon!

---

[^1]:
    While writing that post all those months ago, I certainly did _not_ 
    want to. If I remmeber right, I finished writing that post at like
    3 or 4 in the morning...

[^2]:
    I don't know why, but submitting to the OEIS always makes me kind of
    giddy with excitement!

[^3]:
    The code is simple enough that I probably don't _need_ to include it?
    It also disrupts the flow of the post more than I would like, so I'll 
    put it here for completeness:

    <div class="no_eval">
    <script type="text/x-sage">
      memo = {0: (2,1)}
      def a(n):
          """
          returns a pair (a_n, ratio)
          """
          if n in memo.keys():
              return memo[n]

          prev, prevRatio = a(n-1)

          ratio = 1
          N = prev
          while ratio >= prevRatio:
              N += 1

              # compute m so that S_m has an element of order N
              principalDivisors = list(factor(N))
              m = sum([a^b for (a,b) in principalDivisors])
              ratio = m/N

          memo[n] = (N, ratio)
          return (N, ratio)
    </script>
    </div>

[1]: https://math.stackexchange.com/questions/4491025/the-smallest-number-for-faithful-operation/4491030#4491030
[2]: /2021/08/16/embedding-dihedral-groups-efficiently.html
[3]: https://oeis.org/A354424
