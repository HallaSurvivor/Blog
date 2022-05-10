---
layout: post
title: How many symbols can $f'(x)$ have if $f$ has $n$ symbols?
tags:
  - 
---

The other day [SMBC][1] put up a lovely comic which did a great job 
[nerdsniping][2] me. I knew that I wanted to try to solve it as soon
as I saw it, but I didn't have the time for a little while
(it's midterm season and I had grading to do). It's a cute problem, and 
I want to share my solution with all of you! First, here's the comic 
that started it all:

<p style="text-align:center;">
<a href="https://www.smbc-comics.com/comic/derivative">
<img src="/assets/images/diff-growth/smbc-derivative.png" width="50%">
</a>
</p>

Now, my old advisor (Klaus Sutner) used to say that whenever you're faced with a 
problem, you can hack or you can think, but you can't do both. ~~Today~~
Multiple weeks ago I was in more
of a hacking mood, so I wrote up some haskell code to just _try_ all the
"reasonable" functions I could think of. By this, of course, I mean the 
[elementary functions][9].

There's an obvious recursive way to build up the elementary functions
(which you should think of as those functions which might show up in a calculus class):

 - $f(x) = x$ should probably be a function, as should the constants
 - If $f(x)$ has previously been defined, $\sin(f(x))$, etc. should be functions
 - If $f(x)$ and $g(x)$ have previously been defined, $f + g$, etc. should be functions

We can formalize this with a datatype[^1]

<div class="no_eval">
<script type="text/x-sage">

data Expr = Const Rational
          | X
          | Square Expr
          | Sqrt Expr
          | Sin Expr
          | Cos Expr
          | Tan Expr
          | ASin Expr
          | ACos Expr
          | ATan Expr
          | Sinh Expr
          | Cosh Expr
          | Tanh Expr
          | ASinh Expr
          | ACosh Expr
          | ATanh Expr
          | Exp Expr
          | Log Expr
          | Add Expr Expr
          | Sub Expr Expr
          | Mult Expr Expr
          | Div Expr Expr
          | Pow Expr Expr
  deriving (Show, Eq)

</script>
</div>

Obviously this list, while exhausting the elementary functions, is 
still somewhat arbitrary. 
For instance, $\sec$ is nowhere on this list, but we can build it using
the functions that _are_ on this list[^8]. Conversely, we added a builtin 
function for $\tan$, even though we can express it using $\sin$ and $\cos$. 
The decision to add squaring and square roots as primitive, while relegating
cubes and cube roots, etc. to a definition using `Const` and `Pow` was 
similarly arbitrary. 

I went for this list basically because it's what the [wikipedia article][9]
names explicitly. Later on we'll show that our solution doesn't 
depend on the exact list chosen, so we don't need to worry about this.

Next up, we need to tell haskell how to compute the derivative of a function.
Thankfully, derivatives can be computed recursively, so this is quite easy
to code up:

<div class="no_eval">
<script type="text/x-sage">
diff :: Expr -> Expr
diff (Const n)    = Const 0
diff X            = Const 1
diff (Square e)   = Mult (Mult (Const 2) e) (diff e)
diff (Sqrt e)     = Div (diff e) (Mult (Const 2) (Sqrt e))
diff (Sin e)      = Mult (Cos e) (diff e)
diff (Cos e)      = Mult (Const (-1)) (Mult (Sin e) (diff e))
diff (Tan e)      = Mult (Add (Const 1) (Square (Tan e))) (diff e)
diff (ASin e)     = Div (diff e) (Sqrt (Sub (Const 1) (Square e)))
diff (ACos e)     = Div (Mult (Const (-1)) (diff e)) (Sqrt (Sub (Const 1) (Square e)))
diff (ATan e)     = Div (diff e) (Add (Const 1) (Square e))
diff (Sinh e)     = Mult (Cosh e) (diff e)
diff (Cosh e)     = Mult (Sinh e) (diff e)
diff (Tanh e)     = Mult (Sub (Const 1) (Square (Tanh e))) (diff e)
diff (ASinh e)    = Div (diff e) (Sqrt (Add (Const 1) (Square e)))
diff (ACosh e)    = Div (diff e) (Sqrt (Sub (Square e) (Const 1)))
diff (ATanh e)    = Mult (Square (Cosh e)) (diff e)
diff (Exp e)      = Mult (Exp e) (diff e)
diff (Log e)      = Div (diff e) e
diff (Add e1 e2)  = Add (diff e1) (diff e2)
diff (Sub e1 e2)  = Sub (diff e1) (diff e2)
diff (Mult e1 e2) = Add (Mult (diff e1) e2) (Mult e1 (diff e2))
diff (Div e1 e2)  = Div (Sub (Mult e2 (diff e1)) (Mult e1 (diff e2))) (Square e2)
diff (Pow e1 e2)  = Mult (Pow e1 e2) (Add (Mult (Log e1) (diff e2)) (Div (Mult e2 (diff e1)) (e1)))
</script>
</div>

This isn't perfect. For instance, it doesn't simplify multiplication by $1$, etc.
But I wanted a quick and dirty approximation, and importantly, I didn't want to
spend too long on this project[^4].

<div class=boxed markdown=1>
As a (fun?) exercise, write a `prune` function which makes some easy 
simplifications after differentiating. Does that change which functions
grow the most in complexity?
</div>

Next, we need a way to figure out how many symbols are in a given expression.
This is also easy to implement:

<div class="no_eval">
<script type="text/x-sage">
size :: Expr -> Int
size (Const n)    = 1
size X            = 1
size (Square e)   = 1 + size e
size (Sqrt e)     = 1 + size e
size (Sin e)      = 1 + size e
size (Cos e)      = 1 + size e
size (Tan e)      = 1 + size e
size (ASin e)     = 1 + size e
size (ACos e)     = 1 + size e
size (ATan e)     = 1 + size e
size (Sinh e)     = 1 + size e
size (Cosh e)     = 1 + size e
size (Tanh e)     = 1 + size e
size (ASinh e)    = 1 + size e
size (ACosh e)    = 1 + size e
size (ATanh e)    = 1 + size e
size (Exp e)      = 1 + size e
size (Log e)      = 1 + size e
size (Add e1 e2)  = 1 + size e1 + size e2
size (Sub e1 e2)  = 1 + size e1 + size e2
size (Mult e1 e2) = 1 + size e1 + size e2
size (Div e1 e2)  = 1 + size e1 + size e2
size (Pow e1 e2)  = 1 + size e1 + size e2
</script>
</div>

Lastly, we need a way to build up every expression with $n$ symbols. This way
we can differentiate them all, and see which gives us the largest output!

<div class="no_eval">
<script type="text/x-sage">
build :: Int -> [Expr]
build 1 = [X]
build n = 
    [comb e | comb <- unary, e <- (build (n-1))] ++ 
    [comb e1 e2 | comb <- binary, e1 <- (build (n-1)), e2 <- build((n-1))] ++
    (build (n-1))
  where
    unary = [Square, Sqrt, 
      Sin, Cos, Tan, ASin, ACos, ATan, 
      Sinh, Cosh, Tanh, ASinh, ACosh, ATanh, Exp, Log]
    binary = [Add, Sub, Mult, Div, Pow]

-- compute the largest size of diff e as e ranges over exprs of size n
b :: Int -> [Expr] -> (Int, Expr)
b n = maximumBy cmp . fmap (\e -> (size (diff e), e)) . filter (\e -> size e == n)
  where
    cmp (s1,_) (s2,_) = compare s1 s2
</script>
</div>

---

Now, my laptop can fully exhaust every function with $\leq 4$ symbols,
and we see that our best bets are

 - $x$, whose derivative has $1$ symbol
 - $\arccos(x)$, whose derivative has $9$ symbols
 - $\arccos(\arccos(x))$, whose derivative has $18$ symbols
 - $\arccos(\arccos(\arccos(x)))$, whose derivative has $28$ symbols

(note that the innermost $x$ counts as a symbol).

Moreover, it's pretty easy to see that we'll never use a unary function
other than $\arccos$. Indeed, if we write $\lvert f \rvert$ for `size f`,
it's easy to see that

$$\lvert \arccos(f)' \rvert = \lvert f \rvert + \lvert f' \rvert + 7.$$

More generally, $\lvert \text{blah}(f)' \rvert = \lvert f \rvert + \lvert f' \rvert + k$
where $k$ is the number of symbols in the derivative of $\text{blah}(x)$[^9]. 
Since this is biggest for $\arccos$, and we're trying to maximize the size of
$f'$, there's no reason to use a unary constructor other than $\arccos$.

This is fairly good evidence that repeatedly composing $\arccos(x)$ with 
itself is the winner, and even though we can't test _every_ function with
$\geq 5$ symbols, we can test a lot of them, and after letting the code run
for just over $24$ hours, iterating $\arccos$ was still the winner. 

So, in light of our computational evidence, we might _conjecture_ that 
$\lvert f' \rvert$ is maximized (among functions with $\lvert f \rvert = n$)
for $f = \arccos(\arccos(\ldots(x)\ldots))$. 

At this point, it's time to stop hacking, and start thinking! Let's try to
_prove_ that this is the best option. Notice we can easily compute 
$\lvert \arccos(\arccos(\ldots(x)\ldots))' \rvert = \frac{n^2}{2} + \frac{13n}{2} - 6$
(either by solving some recurrence, or by checking [oeis][10]), so we should 
have some simple proof by induction ahead of us.

---

<div class=boxed markdown=1>
If $f$ has $n$ symbols in its definition, then $f'$ has at most
$\frac{n^2}{2} + \frac{13n}{2} - 6$ symbols, and moreover this maximum is
attained for $f = \arccos(\arccos(\ldots(x)\ldots))$.
</div>

$\ulcorner$

We'll induct on $\lvert f \rvert$.

If $\lvert f \rvert = 1,2$ then we've already seen that $\lvert f' \rvert$ 
satisfied the desired inequality.

If $\lvert f \rvert \geq 3$, then we case on the outermost constructor.

If it's unary, say $f = g(h)$, where $\lvert h \rvert = n-1$, then we compute

$$
\lvert f' \rvert = \lvert g'(h) \cdot h' \rvert = \lvert h' \rvert + (n-1) + k
$$

where $k$ is a constant depending on $g$, which is maximized as $k = 7$ when
$g = \arccos(-)$. Then

$$
\lvert f' \rvert 
\leq \lvert h' \rvert + n + 6 
\overset{IH}{\leq} \frac{(n-1)^2}{2} + \frac{13(n-1)}{2} - 6 + n + 6
= \frac{n^2}{2} + \frac{13n}{2} - 6.
$$

If instead the outermost constructor of $f$ is binary, then we have

 - $f = g + h$
 - $f = g - h$
 - $f = g \cdot h$
 - $f = g \div h$
 - $f = g^h$

where $\lvert f \rvert = n = \lvert g \rvert + \lvert h \rvert + 1$.

In each of these cases we compute $\lvert f' \rvert$, and find

 - $\lvert (g+h)' \rvert = \lvert g' \rvert + \lvert h' \rvert + 1$
 - $\lvert (g-h)' \rvert = \lvert g' \rvert + \lvert h' \rvert + 1$
 - $\lvert (g \cdot h)' \rvert = \lvert g \rvert + \lvert h \rvert + \lvert g' \rvert + \lvert h' \rvert + 3$
 - $\lvert (g \div h)' \rvert = \lvert g \rvert + 2 \lvert h \rvert + \lvert g' \rvert + \lvert h' \rvert + 5$
 - $\lvert (g^h)' \rvert = 3 \lvert g \rvert + 2 \lvert h \rvert + \lvert g' \rvert + \lvert h' \rvert + 7$

Clearly these are maximized for $g^h$, so let's put $\lvert g \rvert = k$ 
and $\lvert h \rvert = n-1-k$. Then we see

$$
\begin{align}
\lvert (g^h)' \rvert 
&= 
3 \lvert g \rvert + 2 \lvert h \rvert + \lvert g' \rvert + \lvert h' \rvert + 7 \\
&\overset{IH}{\leq}
3k + 2(n-1-k) + \frac{k^2}{2} + \frac{13k}{2} - 6 + 
\frac{(n-1-k)^2}{2} + \frac{13(n-1-k)}{2} - 6 + 7 \\
&=
\frac{n^2}{2} + \frac{(15-2k)n}{2} + k^2 + 2k - 13
\end{align}
$$

So we want this to be $\leq \frac{n^2}{2} + \frac{13n}{2} - 6$ for 
every choice of $1 \leq k \leq n-2$. 

Aaaaaand.... ruh roh!

You can see by [this][11] desmos graph that this fails in general.
Indeed, the earliest failure happens when $n=8$ and $k=6$. Of course, 
this is _outside_ of the $n \leq 4$ range that I was able to exhaustively test,
and even the $n \leq 6$ range that I had tested a lot of[^15].

<span style="float:right">$\lrcorner$</span>

---

This is a perfect example of Klaus's "Magic Spiral", which he shows in the 
first CDM lecture every year. 

<p style="text-align:center;">
<img src="/assets/images/diff-growth/magic-spiral.png" width="50%">
</p>

In this particular situation, there wasn't a ton to visualize, so we jumped 
straight from "compute/experiment" to "conjecture". Indeed, our computations 
seemed to suggest that iterating $\arccos$ was the right approach, but when
we tried to prove it we failed. 

This is ok, though! Good, even, because our failure is instructive! 
We know where our proof failed, and this tells us where we should focus our 
computational effort on our next trip around the spiral.

Indeed, knowing that
we want $k = \lvert g \rvert = 6$ and $n = 8$ says we should try something like

$$
f = g^h = \arccos(\arccos(\arccos(\arccos(\arccos(x)))))^x
$$

and indeed, haskell tells us that $\lvert f' \rvert = 79$, which is 
bigger than the $78$ we would get by iterating $\arccos$. 

---

Now with `Pow` _and_ `ACos` to worry about, it's much less clear what the 
optimal function will be. After all, we'll need to balance the two, and I don't
have the processing power to do an exhaustive search of $n=8,9,10$ (say)
to try and guess at a pattern[^7].

Thankfully, this problem still admits an _asymptotic_ solution, and our 
earlier proof attempt is easily adapted to this setting. 

Now, the most important skill a mathematician should learn is how to cover
their tracks[^10]. So when presenting a result like this to journals, we should
never say that we're presenting an asymptotic solution because we didn't 
have the time to get a closed form. 

Instead, we should argue that the choice of constructors for the elementary
functions was arbitrary, and any closed form for the maximal size of 
$\lvert f' \rvert$ _necessarily_ depends on the choice of constructors! 
Indeed, there are other conventions one could make, such as deciding to 
not count multiplication towards the symbol count, since we often denote
multiplication by juxtaposition, which doesn't require a "symbol" at all.

Of course, one can show that the _asymptotics_ of $\lvert f' \rvert$ are
independent of these choices, which makes the asymptotics a better 
object of study.

... sounds good, doesn't it[^11]?

Now let's prove it!

<div class=boxed markdown=1>
  If $f$ has $n$ symbols in its definition, then $f'$ has $O(n^2)$ 
  symbols in its definition, and this is optimal.

  Moreover, our proof shows that this is independent of the choice of 
  presentation of the elementary functions.
</div>

$\ulcorner$

Again, we induct on $\lvert f \rvert$, the number of symbols in $f$.

Since we're only interested in asymptotics, there's nothing interesting to 
prove about the base case.

For the inductive case, we case on the outermost constructor of $f$.

If it's unary, say $f = c(g)$, then we see that 

$$
\lvert f' \rvert = 
\lvert c'(g) \cdot g'(x) \rvert =
\lvert c'(x) \rvert + O \left ( \lvert g \rvert \right ) + 
O \left ( \lvert g' \rvert \right ) \pm O(1)
$$

where the $O(1)$ term is independent of $c$ and keeps track of the symbols
involved in representing the multiplication, etc. The big-ohs
around $\lvert g \rvert$ and $\lvert g' \rvert$ account for the fact that
we might use each of these a constant number of times[^13].

Next we see that $\lvert c'(x) \rvert = O(1)$, 
since we can uniformly bound these by the size of the largest one,
as we did with $\arccos$ earlier in this post[^12]. So we see

$$
\begin{align}
\lvert f' \rvert 
&= \lvert c(g)' \rvert \\
&\leq O \left ( \lvert g \rvert \right ) + O \left ( \lvert g' \rvert \right ) + O(1) \\
&\overset{IH}{\leq} O \left ( n-1 \right ) + O \left ((n-1)^2 \right ) + O(1) \\
&\leq O(n^2)
\end{align}
$$

If instead the outermost constructor is binary, say $f = c(g,h)$,
where $c(g,h)$ might be $g+h$, $gh$, $g^h$, etc. then we similarly compute

$$
\lvert f' \rvert = 
\lvert c(g,h)' \rvert =
O \left ( \lvert g \rvert \right ) + O \left ( \lvert h \rvert \right ) + 
O \left ( \lvert g' \rvert \right ) + O \left ( \lvert h' \rvert \right ) + O(1)
$$

and since $\lvert g \rvert + \lvert h \rvert = n-1$, we see that this is 
bounded by 

$$
O(n-1) + O \left ( (n-1)^2 \right ) + O(1) = O(n^2)
$$

and the claim follows.

As for the tightness of this bound, any presentation of the elementary 
functions must have at least one trig function (since we cannot build 
the trig functions from the others), say $\sin$. Then the $n$-fold 
composition $\sin(\sin(\cdots(\sin(x) \cdots)))$ is easily seen to have
a derivative with quadratically many symbols.

<span style="float:right">$\lrcorner$</span>

---

So we see that the precise question posed in the comic has no answer! 
It asks for the maximal ratio of $\frac{\lvert f' \rvert}{\lvert f \rvert}$,
but we've just shown that this ratio is unbounded. Of course, it's still a
fun problem, and a natural variant _does_ admit a nice solution 
(which we found).

Moreover, this was a good way to showcase the back and forth between
computational experimentation and proof. Sometimes you get things wrong,
and that's ok! We learn, and we form new conjectures that are more likely
to be correct with every trip around the spiral.

<div class=boxed markdown=1>
  As a cute project idea, while I was writing this one of my friends
  ([Rahul][7]) sent me [a blog post][8] where Iago Leal de Freitas built
  a calculus evaluator in haskell that does simplification properly!

  A better hacker than me can probably modify this code to push things a bit 
  further (especially with some parallel computation) to try and find
  a family of functions $(f_n)$ attaining the maximum ratios
  $\frac{\lvert f_n' \rvert}{\lvert f_n \rvert}$.

  This should be a pretty approachable problem for an enthusiastic 
  combinatorics student, and I would love to see somebody do it ^_^
</div>

---

This was a lot of fun! It's been in the works for a while now 
(since April 28, apparently), but I really only worked on it 
for a few days. I'm busy working on a lot of other stuff[^2], and I'll
hopefully share some of it soon. 

One of the biggest things I've been spending time on 
(which probably also qualifies as an announcement)
has been the [HoTTEST Summer 2022][6],
where I'll be TAing this summer. I'm already pretty active answering questions
in the discord, and I've been brushing up on my HoTT to get 
ready[^14]. I can _not_ express how excited I am to be working on this, and 
if anybody wants to show up, you're more than welcome! We're quickly coming
up on 1000 participants (of all experience levels), 
and it's sure to be a great time!

For now, though, I'm off to bed. Goodnight all, and I'll see you in the next one ^_^

---

[^1]:
    Incidentally, this is why I chose haskell instead of sage. Python really
    doesn't handle algebraic datatypes with any sort of alacrity, and I wanted
    to exploit the recursive structure of the problem.

    Plus, it's been a hot second since I got to use haskell, and it's one of
    my favorite languages to work in, so I didn't spend very long on the decision :P.

[^2]:
    I'm reading a series of papers on [model categories][3] with 
    [Sarah Yeakel][4] (who recently got a permanent position at UCR!),
    as well as continuing my own readings on topos theory (which have filtered 
    into a reading course on locale theory that I'm teaching some undergrads). 
    I'm also in a class on riemann surfaces which has been really enlightening
    for me. I have a few ideas for blog posts of the "I wish someone had shown
    me this example sooner" variety, and hopefully I can get to them soon!

    On top of all this, I've been talking with [Patricio Gallardo][5] about becoming an 
    algebraic geometer, and he wants me to start spending a serious amount of 
    time working through Hartshorne and Vakil's notes. This makes sense, 
    of course, and I'm having a ton of fun doing it, but it means I have less 
    time to work on silly projects like this.

[^3]:
    Again, the counting is kind of silly, since we're counting 
    $-1 \times 1$ as three symbols, where the $1$ comes from $\frac{d}{dx} x$.

    I think it's good enough, though.

[^4]:
    ... and regrettably I failed in that regard.

[^7]:
    Looking at the formulas, we can tell that eventually `Pow` will win out
    over `ACos`, and it probably wouldn't take _too_ much work to sort this out...

    Maybe some reader with some free time wants to take this on as a project?

[^8]:
    Namely as `Div (Const 1) (Cos X)`

[^9]:
    Up to an additive constant, at least. If you want to be super precise, 
    then `size $ diff $ C e = size e + size (diff e) + size (C X) - 2` is 
    true for every unary constructor `C`.

[^10]:
    I'm only half joking

[^11]:
    It helps that this is actually a perfectly reasonable thing to do, and 
    jokes aside my original plan was to get asymptotics for exactly this reason
    (also because I anticipated that an exact solution might be hard to get).

    I thought we had gotten lucky with the iterated $\arccos$ construction,
    and if you _can_ get a closed form, you might as well. But with those 
    dreams dashed, it's back to the asymptotics at the end of the day.

[^12]:
    You might worry that there _is_ no largest unary constructor. But the 
    only infinite families of constructors 
    (at least that are listed on [wikipedia][9])
    are the rational powers and the bases for $\exp$ and $\log$. 

    It's clear, though, that the contributions of each of these derivatives 
    can be uniformly bounded as long as we're counting a constant as a single
    symbol.

[^13]:
    For example, we might choose to represent the derivative of $g^2$ by 
    $(g + g) g'$, in which case $\lvert (g^2)'$ would refer to $\lvert g \rvert$
    twice. 

    I haven't actually thought much about how badly things break if you do 
    something silly like this, but take it to an extreme (can we find a way to 
    make it so that there's _no_ uniform bound on this constant?), but I'm also
    ok to leave that particular avenue unexplored. 

    Officially I should probably add some hypotheses explicitly forbidding this --
    for instance, it should be enough to ask that we allow at most finitely many
    constructors. That said, I think it's ok to leave this a bit imprecise for
    the purposes of a blog post.

[^14]:
    Plus trying to gain some serious familiarity with model categories and
    $\infty$-categories before we start. This lined up quite nicely with my
    conversations with Sarah about model categories. Sometimes you just get
    lucky!

[^15]:
    Of course, we could simply _remove_ `Pow` as a constructor, since we 
    can simulate it using `Exp` and `Log`. It's not hard to show that the other
    binary operations _will_ let this proof go through, so we could have 
    "covered our tracks" by acting like we never even considered `Pow`!

    I thought it would make for a better narrative (and it might be more 
    instructive) to go the asymptotic approach instead. Plus, it really is
    more hygenic to prove a result that doesn't depend on a particular 
    choice of "basic" constructors.


[1]: https://www.smbc-comics.com/
[2]: https://xkcd.com/356/
[3]: https://en.wikipedia.org/wiki/Model_category
[4]: https://sites.google.com/view/syeakel/
[5]: https://sites.google.com/site/patriciogallardomath/
[6]: https://www.uwo.ca/math/faculty/kapulkin/seminars/hottest_summer_school_2022.html
[7]: https://rahulrajkumar.github.io/
[8]: https://iagoleal.com/posts/calculus-symbolic/
[9]: https://en.wikipedia.org/wiki/Elementary_function
[10]: https://oeis.org/search?q=1%2C9%2C18%2C28%2C39%2C51%2C64&language=english&go=Search
[11]: https://www.desmos.com/calculator/0eyfyqovj2
