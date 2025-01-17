---
layout: post
title: Where Do Those Undergraduate Divisibility Problems Come From?
tags:
  - 
---

Oftentimes in your "intro to proofs" class or your first "discrete math" class 
or something similar, you'll be shown problems of the form "prove that for 
$n^6 + n^3 + 2n^2 + 2n$ is a multiple of $6$ for every $n$"... But where do 
these problems come from? And have you ever stopped to think how magical this 
is? If I gave you some random polynomial in $n$ and asked you if it always 
output multiples of $6$, the answer would almost always be "no"! So if you 
really needed to come up with an example of this phenomenon, how would you do it?
In this blog post, we give one approach!

I want to give some sort of attribution for this, since I remember reading 
about this exact topic... like a _long_ time ago. Maybe 6 or 7 years ago? 
I'm sure that I saved the relevant article[^1] 
in my zotero, but I can't find it for the life 
of me! Regardless, I want to emphasize that the whole idea for this topic 
(using [Pólya-Redfield counting][2] to build these divisibility problems) is not 
mine. 

I've wanted to write a post on Pólya-Redfield counting for _years_ now, since 
it was a pet topic of mine as an undergrad, but I think I was always planning 
too big a scope. This is a very bite-sized problem, and I won't go into the 
theory very deeply, so I think it should make for a blog post I can finish in 
a day[^2].

Let's get to it! 

---

Ok, first, how might we come up with problems like this? We want a polynomial 
$P(n)$ and an integer $k$ so that $P(n)$ is always a multiple of $k$. That is, 
so that $P(n) / k$ is always an integer! 

But what are sources of integers? If we put our combinatorial hats on, we learn 
that we had better be _counting something_! That's the quickest way to 
ensure that we get an integer answer at the end of the day. So we want a 
polynomial so that as we vary $n$, the value $P(n) / k$ counts... something.

At this point, you might be inspired by [The Lemma Which is Not Burnside's][4], 
which says that when a group $G$ acts on a set $X$, the number of orbits is 

$$
\left | X \big / G \right | = \frac{1}{|G|} \sum_g |X^g|
$$

where $$X^g = \{ x \mid gx = x \}$$ is the set of fixed points of $g$.

This is great, since in some sense it's "where division comes from". I don't 
want to get into [categorification][5] here, but when we say we're thinking of 
numbers as the cardinality of some set (to guarantee they're integers) 
we're really _categorifying_ our problem. There's been lots of work showing 
how various operations on numbers lift to categorified operations on 
the category of finite sets, and the only way I know of to categorify division 
is to take the orbits of some group action[^3]. Hopefully this also serves to 
show that categorification doesn't need to be scary! It can be incredibly 
simple, just thinking about finite sets and what we can do to them...
Though maybe people who read my blog are already convinced of that, haha.

Regardless, this orbit-counting formula is close to what we want! It gives 
us access to division. So if we could only find a family of sets $X_n$, 
all of which admit a $G$-action, then maybe we could have 
$P(n) = \sum_g |X_n^g|$ and thus $P(n)$ will always be divisible by $|G|$, 
since $P(n)/|G|$ counts the orbits $|X_n \big / G|$!

This is exactly what Pólya-Redfield counting buys us! 
I really want to write a blog post with lots of pretty pictures that 
explains this in detail, but maybe just for today I'll allow myself to be 
a bit less thorough. If you want to see this motivated with pretty pictures, 
I'll point you to [some slides][10] by my undergrad advisor Klaus Sutner[^4]. 
These are from the 2023 version of the class where I first met him back in...
2017? It's better to not think about that, haha.

---

Moving on, say we have a set $X$ with a $G$-action. Then we think about 
all the ways to "color" $X$ with $n$-many colors. Precisely these are 
functions from $$X \to [n]$$, and they pick up a natural $g$ action by sending 
the function $f : X \to [n]$ to the function $(gf)(x) = f(g^{-1}x)$[^5]. 
These function spaces[^6] $$(X \to [n])$$ will be our sets $X_n$, and all that's left 
is to see how to compute $|X_n \big / G|$, ideally in a way that's uniform in 
$n$. Now (a corollary of) the main Pólya-Redfield theorem says:

<div class=boxed markdown=1>

$$
\left | (X \to [n]) \big / G \right | = \frac{1}{|G|} \sum_g n^{c(g)}
$$

where $c(g)$ is the "cycle count" of $g$. We can view the action of $G$ on $X$ 
as a homomorphism $\alpha$ from $G$ to the symmetric group $\mathfrak{S}_X$. Then 
$\alpha(g) \in \mathfrak{S}_X$ is a permutation, so decomposes into a product 
of cycles. The number $c(g)$ is perhaps the dumbest invariant you can think of:
just count the number of cycles!
</div>

This is exactly what we want, since it tells us that the polynomial 
$P(n) = \sum_g n^{c(g)}$ is always divisible by $|G|$, since the quotient 
is exactly counting the orbits of the action of $G$ on $$(X \to [n])$$!

Again, unfortunately I'll leave the derivation of this formula 
(and the many many other useful things the Pólya-Redfield theory buys you)
for another day, but at least we can do some quick examples!

<br>

First, say we want to count the number of bracelets you can make with $6$ 
beads, provided you have $n$ many types of beads available. Obviously if you 
were looking at bracelets in the real world that you can move around, the
following two bracelets are actually the same:

<p style="text-align:center;">
<img src="/assets/images/undergrad-divisibility-problems/off-by-rotation.png" width="50%">
</p>

so we want to count the number of ways to _color_ this picture with $n$ 
colors (this is a choice of bead in each position), but only up to the 
obvious $\mathbb{Z} / 6$ action on the space of colorings[^8]! 

<p style="text-align:center;">
<img src="/assets/images/undergrad-divisibility-problems/configuration.png" width="50%">
</p>

Now choose an isomorphism between the colorable places of our configuration 
and the standard set of size $6$, for instance, this is likely to be 
a common choice:

<p style="text-align:center;">
<img src="/assets/images/undergrad-divisibility-problems/configuration-labelled.png" width="50%">
</p>

After making this identification our action is a map 
$\mathbb{Z}/6 \to \mathfrak{S}_6$, and thus we can compute cycle decompositions
as follows:

<div class=boxed markdown=1>

<table align="center" style="margin: 0px auto;">
    <tr>
        <td style="text-align: center; vertical-align: middle;">Element $g \in \mathbb{Z}/6$</td>
        <td style="text-align: center; vertical-align: middle;">Image in $\mathfrak{S}_6$</td>
        <td style="text-align: center; vertical-align: middle;">Number of Cycles, $c(g)$</td>
    </tr>
    <tr>
        <td style="text-align: center; vertical-align: middle;">$0$</td>
        <td style="text-align: center; vertical-align: middle;">$(1)(2)(3)(4)(5)(6)$</td>
        <td style="text-align: center; vertical-align: middle;">$6$</td>
    </tr>
    <tr>
        <td style="text-align: center; vertical-align: middle;">$1$</td>
        <td style="text-align: center; vertical-align: middle;">$(1 \ 2 \ 3 \ 4 \ 5 \ 6)$</td>
        <td style="text-align: center; vertical-align: middle;">$1$</td>
    </tr>
    <tr>
        <td style="text-align: center; vertical-align: middle;">$2$</td>
        <td style="text-align: center; vertical-align: middle;">$(1 \ 3 \ 5)(2 \ 4 \ 6)$</td>
        <td style="text-align: center; vertical-align: middle;">$2$</td>
    </tr>
    <tr>
        <td style="text-align: center; vertical-align: middle;">$3$</td>
        <td style="text-align: center; vertical-align: middle;">$(1 \ 4)(2 \ 5)(3 \ 6)$</td>
        <td style="text-align: center; vertical-align: middle;">$3$</td>
    </tr>
    <tr>
        <td style="text-align: center; vertical-align: middle;">$4$</td>
        <td style="text-align: center; vertical-align: middle;">$(1 \ 5 \ 3)(2 \ 6 \ 4)$</td>
        <td style="text-align: center; vertical-align: middle;">$2$</td>
    </tr>
    <tr>
        <td style="text-align: center; vertical-align: middle;">$5$</td>
        <td style="text-align: center; vertical-align: middle;">$(1 \ 6 \ 5 \ 4 \ 3 \ 2)$</td>
        <td style="text-align: center; vertical-align: middle;">$1$</td>
    </tr>
</table>

</div>

Using this, we see that the number of bracelets with $n$ beads, up to our 
$\mathbb{Z}/6$ action is 

$$
\frac{1}{|G|} \sum_g n^{c(g)} = 
\frac{1}{6} \left ( n^6 + n^1 + n^2 + n^3 + n^2 + n^1 \right ) =
\frac{1}{6} \left ( n^6 + n^3 + 2n^2 + 2n \right )
$$

Since this is counting the number of orbits, it must be an integer, and so 
for every $n$, the polynomial $P(n) = n^6 + n^3 + 2n^2 + 2n$ has to be 
divisible by $6$, as promised!

<br>

Let's see a harder one, which (in the interest of speed) I stole from Klaus's 
lectures:

<div class=boxed markdown=1>
How many ways can you fill a tic-tac-toe board with $X$s and $O$s, up 
to rotation and reflection?
</div>

We have configurations like the following 
(I've already chosen a bijection between our colorable places and the 
standard set with $9$ elements):

<p style="text-align:center;">
<img src="/assets/images/undergrad-divisibility-problems/tic-tac-toe-configuration.png" width="50%">
</p>

Now we want to color each slot $X$ or $O$, and quotient out the action of 
the dihedral group in order to view the following colorings as "the same"
(of course, these aren't the whole orbit! There's many other rotations 
and reflections which are also equivalent):

<p style="text-align:center;">
<img src="/assets/images/undergrad-divisibility-problems/rotate-and-reflect.png" width="50%">
</p>

Notice we're also not worried about which colorings come from actual games 
of tic-tac-toe! 

How does Pólya-Redfield tell us to proceed? Well, the dihedral group $D_{2 \cdot 4}$ 
has $8$ elements, built out of rotations and reflections. Say that $r$ is 
the clockwise rotation shown above, and $s$ is the horizontal flip shown above.
Then using the numbering system from before, we compute 

<p style="text-align:center;">
<img src="/assets/images/undergrad-divisibility-problems/r-and-s.png" width="50%">
</p>

so that, in cycle notation:

$$
r \mapsto (1 \ 7 \ 9 \ 3) (2 \ 4 \ 8 \ 6)(5)
$$

$$
s \mapsto (1 \ 3)(4 \ 6)(7 \ 9)(2)(5)(8)
$$

Since $r$ and $s$ generate the whole dihedral group, we're done with the 
hard work! Now a computer algebra system like [sage][15] can compute the 
rest of the table from these by multiplying them together:

<div class="linked_auto">
<script type="text/x-sage">
# Build a permutation group generated by r and s as above
r = '(1,7,9,3)(2,4,8,6)(5)'
s = '(1,3)(4,6)(7,9)(2)(5)(8)'
G = PermutationGroup([r,s])

# print the cycle decomposition of every element of G
for g in G:
    print(g.cycle_string(singletons=True))

</script>
</div>

<div class=boxed markdown=1>
As a cute exercise for those new to group theory, try computing 
these 8 permutations yourself! Can you figure out which one comes from 
which element of the dihedral group? Can you see how they relate to the 
usual presentation $G = \langle r, s \mid r^4, s^2, srs=r^{-1} \rangle$?
</div>

From here it's easy to read off the polynomial! If we have $n$-many available 
colors to put in each slot of the tic-tac-toe board, then the number of 
possible boards, counted up to rotation and reflection is given by 

$$
\begin{align}
\left | (\mathtt{TicTacToeBoard} \to [n]) \big / G \right | 
&= \frac{1}{|G|} \sum_g n^{c(g)} \\
&= \frac{1}{8} \left ( n^9 + 4n^6 + n^5 + 2n^3 \right )
\end{align}
$$

Since we're trying to color the board with only two colors, $X$ and $O$, 
we see the number of ways is 

$$
\frac{1}{8} \left ( 2^9 + 4 \cdot 2^6 + 2^5 + 2 \cdot 2^3 \right )
= 102
$$

Now we've really made two predictions here. First, that 
$P(n) = n^9 + 4n^6 + n^5 + 2n^3$ will be a multiple of $8$ for whichever
$n$ you plug in. Second, that this quotient really _is_ counting the 
tic-tac-toe boards! Let's take a quick second and ask sage how true those look.

First, we can just plug in a few thousand $n$s and see if we ever hit anything 
other than a multiple of $8$:

<div class="linked_auto">
<script type="text/x-sage">
foundException = False
for n in range(1,10000):
    p = n^9 + 4*n^6 + n^5 + 2*n^3
    if (p % 8) != 0:
        foundException = True
        print("uh oh! P({0}) is not a multiple of 8!".format(n))
        break
if not foundException:
    print("^_^")
</script>
</div>

Second, we know there's only $2^9 = 512$ many ways to 2-color a tic-tac-toe 
board without counting rotations and reflections. So it's not too time 
consuming to just list all of them and remove any we've seen before!

<div class="linked_auto">
<script type="text/x-sage">
from itertools import product
colors = [0,1]
boards = (((a,b,c), \
           (d,e,f), \
           (g,h,i)) \
           for (a,b,c,d,e,f,g,h,i) in \
           product(colors,repeat=9))

def rotate(b):
    ((a,b,c), \
     (d,e,f), \
     (g,h,i)) = b
    
    return ((g,d,a), \
            (h,e,b), \
            (i,f,c))
    
def reflect(b):
    ((a,b,c), \
     (d,e,f), \
     (g,h,i)) = b
    
    return ((c,b,a), \
            (f,e,d), \
            (i,h,g))

# this is actually kind of stupid, and computes 
# the orbit with duplicates... But that's fine 
# for numbers this small.
def orbit(b):
    return [b, \
            rotate(b), \
            rotate(rotate(b)), \
            rotate(rotate(rotate(b))), \
            reflect(b), \
            rotate(reflect(b)), \
            rotate(rotate(reflect(b))), \
            rotate(rotate(rotate(reflect(b))))] 
             


seen = []
for b in boards:    
    if set(seen).isdisjoint(orbit(b)):
        seen.append(b)

print(len(seen))
</script>
</div>

---

So there we go! This actually ended up taking two days to write, 
since yesterday I got distracted from my distraction when I was 
talking to a friend about [connections][16] and how 
curvature is related to force in physics. I realized I don't actually 
understand that as well as I thought I did, so I had to spend some 
time rereading a bunch of physics stuff, which was super fun, even if it took 
a while, haha.

If you're ever on a deserted island and you find yourself needing polynomials 
whose outputs are always divisible by some fixed number, this is an endless 
source! You might ask if _every_ such polynomial arises from Pólya-Redfield 
counting in this way, and that's obviously false (since, for instance, 
we'll never get any constant terms)... But it's _not_ obviously false that 
every such polynomial arises from Pólya-Redfield counting 
_after a change of variables_! So with no intuition at all for whether 
it's true or false, let me pose that as a conjecture:

<div class=boxed markdown=1>
Conjecture:

If $p$ is a polynomial so that $p(n)$ is a multiple of $k$ for every $n$, 
then there is a set $X$ and a group $G$ of order $k$ and a polynomial $f$ 
sending integers to integers so that 

$$\frac{1}{k}p(n) \text{ counts the orbits } |(X \to [f(n)]) \big / G|$$

Maybe $f$ can even be taken to be of the form $an+b$, why not. I haven't 
thought about it either way, haha.
</div>

For anyone interested in thinking about this conjecture, it'll be nice 
to know that every polynomial sending integers to integers is an integer 
linear combination of binomial coefficients (see [here][17]). Amusingly, 
this was also shown by Pólya! 

You can push this further (as mentioned in the same wikipedia article) to 
note that $k \mid p(n)$ for all $n$ if and only if in the above 
representation $p = \sum c_i \binom{x}{i}$, all the $c_i$s are multiples of $k$.
So we have an extremely concrete classification of these polynomials, which 
one might use to (dis)prove the conjecture[^9]!

As a cute aside, we've actually talked about this basis for polynomials in 
terms of binomial coefficients [before][18]! Seeing them turn up here was 
like seeing an old friend.

<br>

Thanks again for hanging out, all! This was super fun, and it was a nice 
diversion from the blog post about my thesis work. It's loooong, but really 
interesting, and I think people will enjoy it. This stuff relating 
fukaya categories, topological field theories, and representation theory 
is some of the coolest math I've ever seen, and I couldn't have asked for a 
more fun thesis topic. 

Of course, I also need to get the [topological topos posts][19] cleaned up 
and submitted to journals, and I have a fun project that I want to 
finish up which will be interesting to categorical logicians and 
algebraic geometers! (At least, algebraic geometers of a certain kind, haha).
There's always more to do, but that's part of the fun of it! After two months 
applying to postdocs and barely doing any math at all, I'm thrilled to be 
back at it ^_^.

Alright, stay safe, all! We'll talk soon 💖 



---

[1]: https://en.wikipedia.org/wiki/Cluster_algebra
[2]: https://en.wikipedia.org/wiki/P%C3%B3lya_enumeration_theorem
[3]: https://www.youtube.com/watch?v=N5Rg10SpoGE&list=PLFlhMm_qks4JzVHRy2sTGEnEKKE3PSJ0B&index=5
[4]: https://en.wikipedia.org/wiki/Burnside%27s_lemma#History:_the_lemma_that_is_not_Burnside's
[5]: https://en.wikipedia.org/wiki/Categorification
[6]: https://en.wikipedia.org/wiki/Combinatorial_species
[7]: https://ncatlab.org/nlab/show/structure+type
[8]: https://arxiv.org/pdf/math/0004133
[9]: https://mathoverflow.net/q/22860/145247
[10]: /assets/docs/undergrad-divisibility-problems/F23-26-polya-redfield.pdf
[11]: https://www.cs.cmu.edu/~cdm/pdf/F23-26-polya-redfield.pdf
[12]: https://www.cs.cmu.edu/~cdm/table.html
[13]: https://en.wikipedia.org/wiki/Wilson_loop
[14]: https://mathoverflow.net/q/238897/145247
[15]: https://sagemath.org
[16]: https://en.wikipedia.org/wiki/Connection_(mathematics)
[17]: https://en.wikipedia.org/wiki/Integer-valued_polynomial#Classification
[18]: /2021/05/13/stirling-basis-change
[19]: /2024/07/03/life-in-johnstones-topological-topos.html


[^1]:
    or maybe it was a blog post or an mse question or something... 
    Or maybe a footnote in a published paper? Part of why I can't find it 
    is because I don't remember anything about where I read it! And back
    when I was an undergrad I was much worse about leaving myself searchable 
    notes so I can quickly find interesting things again.

[^2]:
    If you're curious why I decided to make this blog post _now_, I just 
    started learning about [cluster algebras][1] today, and in the first 
    lecture of [Pavel Galashin's series on the subject][3] he mentions a 
    recurrence relation which magically always gives integers, despite 
    division happening. This reminded me of these polynomials which always 
    give outputs divisible by some number 
    (which is an easier version of the same phenomenon), and I went 
    looking for the original article to share on mastodon. I couldn't find it, 
    so... I guess I'm writing one!

    John Baez and Jim Dolan and I also talked about [species][6] 
    and [structure types][7] in our last meeting, and so I think I was also 
    somewhat primed to think about generating functions and Pólya-Redfield 
    counting based on that conversation.

[^3]:
    You need groupoids and "groupoid cardinality" to have access to 
    division in general, since this lets you get rational numbers 
    (and even certain real numbers!) as cardinalities. See, for instance, 
    John and Jim's famous paper [_From Finite Sets to Feynman Diagrams_][8]
    or [this MO post][9] for more.

[^4]:
    I saved a copy of these slides local to this blog to make sure they're 
    always available, but if you want them right from the horse's mouth you 
    can find them [here][11], and a course schedule with all the available 
    lecture slides [here][12].

[^5]:
    As long as I'm missing my undergrad years, I'll pass on an 
    insight from one of my favorite undergrad professors Clinton Conley 
    about this seemingly weird $g^{-1}$:

    Remember when you were learning how to graph functions and if you want to 
    move the graph of $f(x)$ to the _right_ by $c$, you look at the function 
    $f(x-c)$? This trips up a lot of students first learning things, since it 
    seems backwards to subtract $c$ to move to the right, especially 
    since moving up and down has the much more sane behavior that $f(x)+c$ 
    moves you up by $c$ units!

    This is the same phenomenon, where the action on the _input_ is 
    contravariant (and we act on $x$ by the _inverse_ of $c$) while the 
    action on the _output_ is covariant (and we act on $f(x)$ by $c$)!

    There's also something to be said here about left vs right actions, 
    but I won't say it, haha. Hopefully this Clinton-ism helps this make 
    more sense, since I remember it _really_ helped me when I was younger!

[^6]:
    I guess my type theory background is showing in this notation, haha.

[^7]:
    Actually, now that I've been thinking so hard about [Wilson Loops][13] 
    and the langlands programme, and other sources of "conjugation class valued" 
    invariants in representation theory,
    this feels a bit like that... Indeed, counting the number of cycles is a 
    (markov) trace operator (see [here][14]), so I think there's something real 
    going on here!


[^8]:
    I think when most people talk about these bracelet problems, they quotient 
    by the dihedral group instead of the cyclic group. This is because you 
    can flip a bracelet over in 3D, so you have access to reflections too. 
    I'm ignoring that for the sake of the example, though, and just counting 
    things up to rotation.

[^9]:
    This is also a much more efficient source of polynomials for 
    undergrad divisibility problems, but it wouldn't have been 
    anywhere _near_ as fun!
