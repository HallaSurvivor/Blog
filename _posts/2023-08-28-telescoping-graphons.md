---
layout: post
title: Estimating a Difference of Products
tags:
  - quick-analysis-tricks
---

Wow, it's been a long time! Both since my last blog post, and since my last 
[quick analysis trick](/tags/quick-analysis-tricks). But I've been itching to 
write more blog posts lately, and I thought that something quick and easy like 
this would be a good way to get back into it without the kind of effort that 
goes into some of my longer-form posts (which I'm still working on, of course).

I got back from a conference yesterday night, and gave myself the day off to 
recover (and do some chores...) so I decided to do some low-energy math while 
my laundry was going. I _love_ watching lectures in computer-science-y and 
combinatorics-y subjects that I don't get to spend much time doing anymore.
It doesn't take much effort to get the gist of the subject, learn 
some surface level techniques, etc. that keep me feeling like I'm improving,
even though I don't have the time to read papers and do serious research 
in these areas right now.
This year I've been slowly been making progress in 
Yufei Zhao's phenomenal course on "Graph Theory and Combinatorics", available 
freely on [youtube][1]. 

While talking about [graphons][2], Zhao gives an 
analytical argument that I can see being _extremely_ applicable in other 
settings, so I figured I would talk about it here[^1]!

---

Let's get right into the trick, then I'll give a few situations where it 
might be helpful. Say you have two sequences $a_1, \ldots, a_n$ 
and $b_1, \ldots, b_n$ and you want to control the difference 

$$
\prod_{i=1}^n a_i - \prod_{i=1}^n b_i.
$$

The quick-analysis-trick du jour is to rewrite this difference as 

$$
\prod_1^n a_i - \prod_1^n b_i = 
\sum_{j=1}^n \left ( \prod_{i \lt j} b_i \right ) (a_j - b_j) \left ( \prod_{i \gt j} a_i \right )
$$

This looks a bit unwieldy, but it follows a very easy pattern. Let's see what 
this looks like for a few small values of $n$:

$$ 
a_1 a_2 - b_1 b_2 = 
(a_1 - b_1) a_2 + b_1 (a_2 - b_2) 
$$

<br>

$$ 
a_1 a_2 a_3 - b_1 b_2 b_3 = 
(a_1 - b_1) a_2 a_3 + b_1 (a_2 - b_2) a_3 + b_1 b_2 (a_3 - b_3) 
$$

<br>

$$ 
\begin{align}
a_1 a_2 a_3 a_4 - b_1 b_2 b_3 b_4 
&= (a_1 - b_1) a_2 a_3 a_4 \\ 
&+ b_1 (a_2 - b_2) a_3 a_4 \\
&+ b_1 b_2 (a_3 - b_3) a_4 \\
&+ b_1 b_2 b_3 (a_4 - b_4)
\end{align}
$$

You start with $(a_1 - b_1)$ and all the $a_i$s on the right. Then
to get from one term to the next you hop an $a_i$ over the difference, 
turning it into a $b_i$ along the way. You finish when you're left with 
all the $b_i$s on the left.

This has a kind of "product rule" feeling to it, where we replace the 
difference of products (analogous to the derivative of a product) with 
a sum of products over all places we could "put" the difference 
(analogous to the sum over all places we can "put" the derivative). Indeed,
we can _prove_ the product rule using this trick! 

<div class=boxed markdown=1>
As a cute exercise, you might use this to prove the product rule formula 

$$
\left ( \prod_{i=1}^n f_i \right )' = 
\sum_j \left ( \prod_{i \lt j} f_i \right ) f_j' \left ( \prod_{i \gt j} f_i \right )
$$

If the $\prod$s are unwieldy, it's worth doing the $n=3$ case without them 
to see what's going on.
</div>

Notice the key idea of this proof of the product formula is that we 
controlled a _difference of products_ by rewriting it as a sum where 
each term only had a _single difference_ in it! This is the main idea of 
the technique. For instance, here's another problem you might try:

<div class=boxed markdown=1>
Say that each $\lvert a_i \rvert, \lvert b_i \rvert \leq 1$ for $1 \leq i \leq n$. Prove

$$
\left \lvert \prod_{i=1}^n a_i - \prod_{i=1}^n b_i \right \rvert \leq 
\sum_{i=1}^n \lvert a_i - b_i \rvert
$$
</div>

In fact, this problem was exactly the flavor of the graphon application 
from Zhao's lectures! Say we have two graphons $W, U : [0,1]^2 \to [0,1]$
which are "close" in the sense that 

$$\iint_{[0,1]^2} \Big ( W(x,y) - U(x,y) \Big ) \phi(x) \psi(y) \ dy \ dx \quad \quad (\star)$$ 

is small for each pair of weight functions $\phi$ and $\psi$.

The "number of triangles in $W$" is given by 

$$t(W) = \iiint_{[0,1]^3} W(x,y) W(y,z) W(z,x) \ dx \ dy \ dz$$

since we think of $W(x,y)$ as being the "probability of an edge" 
between $x$ and $y$.

Then if we want to know that $W$ and $U$ have a similar number of triangles, 
we want to show the difference $\lvert t(W) - t(U) \rvert$ is small. Of course,
this expands to

$$\left \lvert \iiint W(x,y) W(y,z) W(z,x) - U(x,y) U(y,z) U(z,x) \ dx \ dy \ dz \right \rvert$$

which is bounded by 

$$\iiint \left \lvert W(x,y) W(y,z) W(z,x) - U(x,y) U(y,z) U(z,x) \right \rvert \ dx \ dy \ dz$$

and thus, by our trick-du-jour, by the sum

$$
\begin{align}
\iiint (W_{x,y} - U_{x,y}) W_{y,z} W_{z,x} \ dx \ dy \ dz + \\
\iiint U_{x,y} (W_{y,z} - U_{y,z}) W_{z,x} \ dx \ dy \ dz + \\
\iiint U_{x,y} U_{y,z} (W_{z,x} - U_{z,x}) \ dx \ dy \ dz
\end{align}
$$

(where I've replaced $W(x,y)$ by $W_{x,y}$ and I'm eliding some absolute 
values in order to improve readability).

But note if we fix $z$ in the first integral, then we get something that 
$(\star)$ tells us how to control! We can then integrate over $z$ at the end 
to get a bound. The story is similar, fixing $x$ in the second integral 
and $y$ in the third. Taken together we're able to get exactly the kind of 
bound that we're after[^2]!

---

Ok, that one really _was_ quick[^3]! I've been traveling a TON lately 
(I've been to way too many conferences this year...) but now I'm finally done and 
I should have time to work on blog posts more regularly. I have a lot of 
ideas, and a lot of drafts, and hopefully I'm able to get them out soon ^_^.

Thanks for hanging out, all. Stay safe, and we'll talk soon!

---

[^1]: 
    He uses this trick in the service of _the counting lemma_. 
    If we fix a graph $H$, the counting lemma says that two "similar" 
    graphons have to contain a "similar" number of copies of $H$. 
    This is around the 16 minute mark of [Lecture 15][3] in that playlist, 
    if you're interested in seeing more.

[^2]:
    Again, I'm glossing over a lot of details here. Thankfully they're all in
    [the relevant lecture][3].

[^3]:
    I actually had a couple extra things I was considering saying in this 
    post, but that goes against the low-effort spirit of quick-analysis-tricks!
    I'm glad I was able to get this written quickly, because I have a fair 
    amount of stuff to do around the house today.

[1]: https://www.youtube.com/playlist?list=PLUl4u3cNGP62qauV_CpT1zKaGG_Vj5igX
[2]: https://en.wikipedia.org/wiki/Graphon
[3]: https://youtu.be/9gy-CAwx0Ls?si=E2ZFePCdidTBbKzk
