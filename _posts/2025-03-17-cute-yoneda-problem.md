---
layout: post
title: A Cute Application of the Yoneda Lemma
tags:
  - 
---

Every few weeks recently I've been putting a new fun problem on one of the 
whiteboards in the first year office. These are often inspired by something 
I saw on MSE, and I'm usually choosing problems that force you to understand 
something fundamental really well. Then I usually have a "challenge" bonus 
problem that uses the same ideas, but requires you to do some independent 
research to finish the puzzle! I've just decided what the next problem is 
going to be, and I'm going to post about it here because I think it's too 
cute to not share more widely! This is also going to serve as a nice excuse 
to talk about some important reasons to care about yoneda and representability 
that I don't think we often tell beginners!

Before we start, though, some quick life updates: I'm still waiting to hear 
back positively from postdocs, but there's still plenty of departments 
where I'd be very happy. I'm trying to not stress out until the end of april. 
What's more stressful is my actual dissertation -- because we had to move 
everything up a year, I didn't have as much time as I expected to solve my 
main problem, and while I solved some very simple thing that's needed along 
the way... It's really not a very good thesis, haha. So I'm trying really hard to 
finish the whole problem in the time I have, and we'll see how I manage. My 
mental health has been pretty hit or miss with the
\*gestures at the state of the world\*, but I'm doing what I can where I can 
to help, and that's been good for what would otherwise be an overwhelming 
sense of helplessness. I know everyone is feeling some amount of this, 
especially in the queer and trans community, and I encourage everyone to find 
something actionable to do on a local level -- it helps the community, and 
it really does help keep the feelings manageable.

BUT, enough about all that! I haven't been writing much because I've been 
so focused on research, and I've really missed posting here. The quicker I am 
the more likely I'll find time to do it again, so let's get to the fun part!

---

I'm going to assume that most people reading my blog have at least _heard_ 
of the [Yoneda Lemma][1]. But it's possible that some people reading this 
are confused as to why you might _care_ about it. Like, what does it 
buy you? How does it help prove theorems? One answer is that it's foundational 
for thinking about the [functor of points][2] approach to lots of subjects, 
which tells you how to study things like [stacks][3], etc. Said in a different 
way, it's an extremely useful perspective for studying certain moduli problems 
-- you can see my old blog post about this [here][4] if you're interested.

But that's all quite high powered. Is there a more concrete reason to care 
about yoneda? The answer here is inspired by one of 
[Terry Tao's old blog posts][5] -- the yoneda lemma tells you how to 
understand [polymorphic][6] transformations between two constructions 
(which are a priori complicated) by just studying regular old functions 
between representing objects!

For one version of this, say you want to understand 
[cohomology operations][7]. That is, say you want to understand when 
there's a map on cohomology $H^p(X,G_1) \to H^q(X,G_2)$ which is 
"polymorphic in $X$" or "uniform in $X$" in the sense that the same map works 
no matter which $X$ you choose[^1]. Just as in analysis where uniformity 
allows you to prove lots of ~bonus results~, requiring uniformity here gives 
us access to many additional theorems -- such as the yoneda lemma. 
Here this "uniformity" is usually called [naturality][8] of the transformation, 
and the precise relationship to polymorphism will be well understood by anyone 
who learned category theory via functional programming[^2], and is well 
explained in some of Bartosz Milewski's old blog posts [here][9] and [here][10].

Now we know that $H^p(-,G)$ is [represented][11] by a space called $K(G,p)$, 
so asking for one of these "cohomology operations" is asking for a natural 
transformation 

$$H^p(-,G_1) \Rightarrow H^q(-,G_2).$$ 

Which, by representability, is a natural transformation 

$$[-,K(G_1,p)] \Rightarrow [-,K(G_2,q)]$$

but now we finally get to use yoneda! These natural transformations are exactly
the same thing as _ordinary continuous functions_ (up to homotopy)

$$[K(G_1,p), K(G_2,q)]!$$

This means if we can understand all continuous functions between these 
_fixed_ spaces, that's enough to understand all cohomology operations 
$H^p(X,G_1) \to H^q(X,G_2)$ for _every space_ $X$ _simultaneously_! The 
ability to work with the representing objects directly is a huge reduction 
in complexity, and one of the main reasons people work with objects like 
"stacks" and "[spectra][12]" is because they want more things to be 
representable so that they can play exactly this game[^3].

That's well and good.... But surely that can't be the "down to earth" 
example, right? Cohomology operations are interesting, and might eventually 
_feel_ down to earth, but objectively most people would 
laugh at that idea. This, finally, brings us to the problem I'll be writing 
on the first year's whiteboard later today:

<div class=boxed markdown=1>
Let $R$ be a (commutative, unital) ring.

- Classify all "polymorphic" functions $R^n \to R$. That is, all (set) functions 
$R^n \to R$ that can be defined _uniformly_ for all rings $R$ simultaneously.
(Hint: yoneda)

<br>

If $G$ is a finite group, define a "$G$-torsion collection" in $R$ to be a 
group homomorphism $G \to R^\times$ from $G$ to the units of $R$. For example, 
a "$C_n$-torsion collection" is an element $x \in R$ so that $x^n = 1$, and a 
"$\mathfrak{S}_3$-torsion collection" is determined by elements $x,y \in R$
with $x^2 = 1$, $y^3 = 1$, and $xyx = y^2$ 
(because $\langle x, y \mid x^2=1, \ y^3=1, \ xyx=y^2 \rangle$ is a presentation 
for $\mathfrak{S}_3$)

<br>

- (Challenge) Classify all "polymorphic" (set) functions 
    $$
    \Big \{\mathfrak{S}_3\text{-torsion collections in $R$} \Big \}
    \to 
    \Big \{C_2\text{-torsion collections in $R$} \Big \}
    $$

</div>

I'm about to spoil both of these problems, so if you want to think about them 
(and I really encourage you to think about them! At least the first problem!)
now is your last chance to be unbiased by my explanation...

<p style="text-align:center;">
<img src="/assets/images/cute-yoneda-problem/no-turning-back.gif" width="50%">
</p>

Ok, so. Inspired by the rest of this post you'll want to think about how to 
_represent_ the constructions above. For the first problem, where we 
want set functions $R^n \to R$, that means we want to represent[^4]

- the functor sending a ring $R$ to the underlying set of $R^n$ 
- the functor sending a ring $R$ to its underlying set

The second one isn't so hard to do -- a moment's thought shows that 
ring homs $\mathbb{Z}[x_1] \to R$ are in bijection with elements of $R$ 
(we just have to choose where to send $x_1$). Once you've figured this out 
it's not such a big jump to see that ring homs 
$\mathbb{Z}[x_1, \ldots, x_n] \to R$ are in bijection with elements of $R^n$ 
(we just have to choose where to send each of the $x_i$ separately).

So classifying "polymorphic" transformations $R^n \to R$ is
classifying natural transformations 

$$[\mathbb{Z}[x_1, \ldots, x_n],-] \Rightarrow [\mathbb{Z}[y],-]$$

which, by yoneda, is asking to classifying good old fashioned _ring homs_ 

$$[\mathbb{Z}[y], \mathbb{Z}[x_1, \ldots, x_n]]$$

and, as before, we just need to decide where $y$ goes! So this is in bijection 
with the underlying set of $\mathbb{Z}[x_1, \ldots, x_n]$. That is, with 
integer-coefficient polynomials in $n$ variables.

It's not hard to see that any such polynomial gives you such a natural map! 
Indeed, for a concrete example take $p = x_1^2 + 2 x_1 x_2 - 3$. Then we get 
a function $R^2 \to R$ sending $(r_1, r_2) \mapsto r_1^2 + 2 r_1 r_2 - 3$, 
where an integer like $-3$ is interpreted in $R$ as $0_R - 1_R - 1_R - 1_R$.

If one thought about this problem without knowing category theory, I think 
it would be pretty easy to conjecture that integer polynomials are the _only_ 
polymorphic maps $R^n \to R$... But I'm not sure how you would prove it without 
basically rediscovering this special case of yoneda! 

<br>

Now... what about the challenge problem? We want to classify "polymorphic" maps 

$$
\Big \{\mathfrak{S}_3\text{-torsion collections in $R$} \Big \}
\to 
\Big \{C_2\text{-torsion collections in $R$} \Big \}
$$

Again we have a natural[^5] conjecture, since if we have a group homomorphism 
$\mathfrak{S}_3 \to R^\times$ we get some obvious group homomorphisms $C_2 \to R^\times$ 
too (namely the images of $(1 \ 2)$, $(2 \ 3)$ and $(1 \ 3)$, the 2-torsion 
elements in $\mathfrak{S}_3$)... Could this be all of them?

Well, a "$G$-torsion collection" in $R$ is a group homomoprhism 
$G \to R^\times$, and these are in bijection with ring maps $\mathbb{Z}G \to R$!
So the same idea as before shows that classifying natural transformations 

$$
\Big \{\mathfrak{S}_3\text{-torsion collections in $R$} \Big \}
\to 
\Big \{C_2\text{-torsion collections in $R$} \Big \}
$$

is the same as classifying natural transformations 

$$[\mathbb{Z}\mathfrak{S}_3, -] \Rightarrow [\mathbb{Z}C_2, -]$$

which, by yoneda, means classifying ring maps 

$$[\mathbb{Z}C_2, \mathbb{Z}\mathfrak{S}_3]$$

and thus means classifying $C_2$-torsion collections in $\mathbb{Z}\mathfrak{S}_3$.
So we want to understand the group of units in $\mathbb{Z}\mathfrak{S}_3$, 
and in particular we want to classify the $2$-torsion elements in this group!

Now is where the independent research comes in. You might naively guess that 
the group of units in $\mathbb{Z}G$ is just $G$ again... But you would be 
wrong! Of course if $g \in G$ then both $+g$ and $-g$ are units in $\mathbb{Z}G$, 
but even _this_ isn't enough! Understanding the units in group rings turns out 
to be a subtle and interesting problem, and I think it's extra cute that this 
little puzzle helps people learn about this surprisingly rich subject[^6].

We want to understand the group of units in $\mathbb{Z}\mathfrak{S}_3$, and 
searching for things related to this will quickly turn up the paper 
[_The Group of Units of the Integral Group Ring_ $\mathbb{Z}S_3$][15] 
by Hughes and Pearson, which certainly seems related!

This paper is only 6 pages long, and is a very polite read[^7]. Part (2) 
of their Theorem 1 is exactly what we're looking for:

> (2) ... there are $2$ conjugacy classes of elements of order $2$, 
> with generic elements $(12)$ and $t=(12) + 3(13) - 3(23) - 3(123) + 3(132)$
> respectively.

What does this mean for us? Their Part (1) to this same theorem gives an 
isomorphism of $$(\mathbb{Z}\mathfrak{S}_3)^\times$$ with a certain $2 \times 2$
matrix group, so it's easy to compute conjugation. So knowing this and knowing 
both conjugacy representatives we have a classification of _all_ order 2 elements 
in $\mathbb{Z}\mathfrak{S}_3$, and by extension (crucially using yoneda and 
representability!) a classification of all natural transformations 

$$
\Big \{\mathfrak{S}_3\text{-torsion collections in $R$} \Big \}
\to 
\Big \{C_2\text{-torsion collections in $R$} \Big \}
$$

Indeed from this we've learned that our naive conjecture was wrong! 
This element $t$ is not one of the 2-torsion elements we were expecting, 
and it gives us a _new_ and _unexpected_ natural transformation!

If $f : \mathfrak{S}_3 \to R^\times$ is a $\mathfrak{S}_3$-torsion collection 
in $R$, then of course we have $C_2$-torsion elements $f(1 \ 2)$, 
$f(2\ 3)$ and $f(1 \ 3)$. But it turns out we also have a secret, special 
$C_2$-torsion element

$$
f(t) = f(1\ 2) + 3 f(1 \ 3) - 3 f(2 \ 3) - 3 f(1 \ 2 \ 3) + 3 f (1 \ 3 \ 2)
$$

Or, said another way, if $x,y \in R^\times$ with $x^2 = 1$, $y^3 = 1$, and 
$xyx = y^2$ determine a $\mathfrak{S}_3$-torsion collection in $R$, then 

$$x + 3 yxy^{-1} - 3 y^{-1} x y - 3 y + 3 y^{-1}$$

is a (probably surprising!) $C_2$-torsion element in $R$.

Of course, as with the last problem, I'm not sure how you would even _begin_ 
to approach this classification problem without rediscovering the relevant 
version of the yoneda lemma!

---

Thanks again for hanging out, everyone! I'm working on a lot of really fun 
stuff and I can't wait to have time to talk about it. I think I want a quick 
outro today -- I've had the sniffles all weekend, probably because I didn't 
dress well before hanging out in the cold with one of my best friends who 
visited me last week! We made creme brulee for the first time 
(since I recently bought a blowtorch), and it was _surprisingly_ easy and 
turned out _delicious_! I already make a lot of lava cakes when I want a 
decadent and fancy dessert, but I'll have to add creme brulee into the rotation!

<p style="text-align:center;">
<img src="/assets/images/cute-yoneda-problem/Emilie.jpg" width="50%">
</p>

<p style="text-align:center;">
<img src="/assets/images/cute-yoneda-problem/Brulee.jpg" width="50%">
</p>

Talk soon, everyone! Stay warm 💖


---

[1]: https://en.wikipedia.org/wiki/Yoneda_lemma
[2]: https://ncatlab.org/nlab/show/functorial+geometryhttps://en.wikipedia.org/wiki/Stack_(mathematics)
[3]: https://en.wikipedia.org/wiki/Stack_(mathematics)
[4]: /2023/02/20/abstract-tensor-products
[5]: https://terrytao.wordpress.com/2023/08/25/yonedas-lemma-as-an-identification-of-form-and-function-the-case-study-of-polynomials/
[6]: https://en.wikipedia.org/wiki/Polymorphism_(computer_science)
[7]: https://en.wikipedia.org/wiki/Cohomology_operation
[8]: https://en.wikipedia.org/wiki/Natural_transformation
[9]: https://bartoszmilewski.com/2015/04/07/natural-transformations/
[10]: https://bartoszmilewski.com/2014/09/22/parametricity-money-for-nothing-and-theorems-for-free/
[11]: https://en.wikipedia.org/wiki/Representable_functor
[12]: https://en.wikipedia.org/wiki/Spectrum_(topology)
[13]: https://www.lgbtmath.org/
[14]: https://ncatlab.org/nlab/show/corepresentable+functor
[15]: https://www.cambridge.org/core/product/identifier/S0008439500061695/type/journal_article


[^1]:
    This "polymorphism" (which, of course, corresponds to [naturality][8]) 
    is because we want an operation that's really coming from the _cohomology_ 
    rather than being an "accidental" operation that comes from structure 
    on $X$.

[^2]:
    Like I did... about a decade ago... I realized when writing this post 
    that I remember waiting for many of these Bartosz Milewski posts to 
    be published! But these posts have been done since 2017. Wild.

[^3]: 
    I was _so_ close to making "spectra" in this sentence link to 
    [spectra][13] instead, which I think would be hilarious, but I 
    decided against it.

[^4]:
    Some pedants might prefer I say [corepresent][14]. This footnote 
    is purely to indicate that I do know better, I just don't care, haha.

[^5]:
    Pun very much intended

[^6]:
    I forget exactly when I learned that the units in $\mathbb{Z}G$ might be 
    bigger than just $\pm G$... But I remember being _extremely_ surprised 
    at the time! I'll mention, though, that this maybe shouldn't be that 
    surprising. Indeed the group ring and group of units constructions are 
    adjoint, so the unit of the adjunction gives a (natural) map 

    $$\eta : G \to (\mathbb{Z}G)^\times$$ 

    and there's no reason to suspect this unit is an isomorphism! Most units 
    aren't, haha.

[^7]:
    Though you have to get over the "function application on the right" 
    notation, which goes totally unmentioned and confused me for a second 
    when I read it.

    Functions on the right is absolutely objectively the better notation, 
    and unfortunately it's _just_ confusing enough when you aren't used 
    to it to make it so that it's unlikely to ever really catch on.
