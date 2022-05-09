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
problem, you can hack or you can think, but you can't do both. Today I was in more
of a hacking mood, so I wrote up some haskell code to just _try_ all the
"reasonable" functions I could think of. 

That is, there's an obvious recursive way to build up functions which might
show up in a calculus class:

 - $f(x) = x$ should probably be a function, as should the constants
 - If $f(x)$ has previously been defined, $\sin(f(x))$, etc. should be functions
 - If $f(x)$ and $g(x)$ have previously been defined, $f + g$, etc. should be functions

We can formalize this with a datatype[^1]

<div class="no_eval">
<script type="text/x-sage">

data Expr = Const Int
          | X
          | Square Expr
          | Sqrt Expr
          | Sin Expr
          | Cos Expr
          | Tan Expr
          | ASin Expr
          | ACos Expr
          | ATan Expr
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

Now, these are far from the _only_ functions you might run into in a 
calculus class, but they certainly feel like a representative list. 
I would love to hear if there's any functions you find conspicuously missing,
and if you think it changes the final answer!

Next up, we need to tell haskell how to compute the derivative of a function.
Thankfully, derivatives can be computed recursively, so this is quite easy
to code up:

<div class="no_eval">
<script type="text/x-sage">
diff :: Expr -> Expr
diff (Const n)    = Const 0
diff X            = Const 1
diff (Square e)   = Mult (Const 2) (diff e)
diff (Sqrt e)     = Div (diff e) (Mult (Const 2) (Sqrt e))
diff (Sin e)      = Mult (Cos e) (diff e)
diff (Cos e)      = Mult (Const (-1)) (Mult (Sin e) (diff e))
diff (Tan e)      = Mult (Add (Const 1) (Square (Tan e))) (diff e)
diff (ASin e)     = Div (diff e) (Sqrt (Sub (Const 1) (Square e)))
diff (ACos e)     = Div (Mult (Const (-1)) (diff e)) (Sqrt (Sub (Const 1) (Square e)))
diff (ATan e)     = Div (diff e) (Add (Const 1) (Square e))
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
spend too long on this project[^2].

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
    unary = [ACos, Square, Sqrt, Sin, Cos, Tan, ASin, ATan, Exp, Log]
    binary = [Add, Sub, Mult, Div, Pow]

-- compute the largest size of diff e as e ranges over exprs of size n
b :: Int -> [Expr] -> (Int, Expr)
b n = maximumBy cmp . fmap (\e -> (size (diff e), e)) . filter (\e -> size e == n)
  where
    cmp (s1,_) (s2,_) = compare s1 s2
</script>
</div>

We put $\arccos$ at the front of the list because early experiments showed that
the best bang for your buck is to compose $\arccos$ with itself $n$ times.
In hindsight this isn't too surprising, since a single $\arccos$ symbol gets 
turned into $9$ symbols after differentiating[^3]! 

---

Now, my laptop can fully exhaust every function with $\leq 4$ symbols,
and we see that our best bets are

 - $x$, whose derivative has $1$ symbol
 - $\arccos(x)$, whose derivative has $9$ symbols
 - $\arccos(\arccos(x))$, whose derivative has $18$ symbols
 - $\arccos(\arccos(\arccos(x)))$, whose derivative has $28$ symbols

(note that the innermost $x$ counts as a symbol).

Moreover, if we remove $\arccos$ from the options, we get strictly smaller 
symbol lengths:

 - $x$, whose derivative has $1$ symbols
 - $\arcsin(x)$, whose derivative has $7$ symbols
 - $x^x$, whose derivative has $14$ symbols
 - $\arcsin(x)^x$, whose derivative has $23$ symbols

this is fairly good evidence that repeatedly composing $\arccos(x)$ with 
itself is the winner, and even though we can't test _every_ function with
$\geq 5$ symbols, we can test a lot of them, and after letting the code run
for just over $24$ hours, iterating $\arccos$ was still the winner. 

This makes some intuitive sense too. After all, $\arccos$ gets the most
symbols of all the unary options. So the only decision to make is whether
it's worth the cost to use $\times$, $\div$, or powers. It's intuitively 
believable that it's never worth it[^4], but we do have to prove it eventually.

At this point, it's time to stop hacking, and start thinking[^5]! Let's 
_prove_ that this is the best option, and while we're at it, let's compute
just how big it really gets!

---

<div class=boxed markdown=1>
If $f$ has $n$ symbols in its definition, then $f'$ has at most
$\frac{n^2}{2} + \frac{13n}{2} - 6$ symbols, and moreover this maximum is
attained for $f = \arccos(\arccos(\ldots(x)\ldots))$.
</div>

We'll induct on the number of symbols in $f$, denoted $\lvert f \rvert$.

If $\lvert f \rvert = 1,2$ then we can check by hand that the number of 
symbols satisfies the desired bounds.

If $\lvert f \rvert \geq 3$, then we case on the outermost constructor.

If it's unary, say $f = g(h)$, where $\lvert h \rvert = n-1$, then we see

$$
\lvert f' \rvert = \lvert g'(h) \cdot h' \rvert = 
\lvert g' \rvert + \lvert h \rvert + \lvert h' \rvert + 1
$$

this is clearly maximized whenever $\lvert g' \rvert$ is maximized, which we
know from the $n=2$ case happens when $g = \arccos$.

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

Aaaaaand.... ruh roh!

It turns out that $\lvert (g^h)' \rvert$ can't be bounded by this function!

---

This is a perfect example of Klaus's "Magic Spiral", which he shows in the 
first CDM lecture every year. It's certainly how I do a lot of math, as we
can see in this toy problem! 

<p style="text-align:center;">
<img src="/assets/images/diff-growth/magic-spiral.png" width="50%">
</p>

In this particular situation, there wasn't a ton to visualize, so we jumped 
straight from "compute/experiment" to "conjecture". Indeed, our computations 
seemed to suggest that iterating $\arccos$ was the right approach, but when
we tried to prove it we failed. 

But our failiure is instructive! If you try to bound $\lvert (g^h)' \rvert$,
it suggests that for $n=8$ we should start seeing failures. Of course, 
this is much to large to check exhaustively, but if we take the first 
100,000 or so functions of size $8$ (and if we restrict attention to those
functions built out of `Pow` and `Acos`), we can check if we start seeing
counterexamples. So we're computing again, and back around the spiral we go.

<div class="no_eval">
<script type="text/x-sage">
build :: Int -> [Expr]
build = (fmap go [0..] !!)
  where
    go :: Int -> [Expr]
    go 1 = [X]
    go 2 = [ACos X]
    go n = prev ++ (liftM2 Pow prev prev) ++ (fmap ACos prev) 
      where
        prev = build (n-1)

b :: Int -> [Expr] -> (Int, Expr)
b n = maximumBy cmp . fmap (\e -> (size (diff e), e)) . filter (\e -> size e == n)
  where
    cmp (s1,_) (s2,_) = compare s1 s2

main :: IO ()
main = b 8 $ take 100000 $ build 8
</script>
</div>


TODO: the question in the comic has no answer! (recall $A$ and $B$) 
  Since $B$ grows quadratically and $A$ grows linearly, we can find 
  arbitrarily high ratios. But that's ok, and was probably expected!

Exercise: try some variations on this. What if you add more functions?
  Or get pruning to work properly? Does multiplication count as a symbol,
  since we usually use concatenation to indicate it? Let me know what 
  you think!

Sign off

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

    Plus I've been talking with [Patricio Gallardo][5] about becoming an 
    algebraic geometer, and he wants me to start spending a serious amount of 
    time working through Hartshorne and Vakil's notes. This makes sense, 
    of course, and I'm having a ton of fun doing it, but it means I have less 
    time to work on silly projects like this.

[^3]:
    Again, the counting is kind of silly, since we're counting 
    $-1 \times 1$ as three symbols, where the $1$ comes from $\frac{d}{dx} x$.

    I think it's good enough, though.

[^4]:
    And this is borne out by another experiment where we use $\arccos$ as our
    only unary constructor, and we keep $\times$, $\div$, and exponentiation
    as binary constructors. Again, we maximize the complexity by playing the
    same $\arccos$ tune over and over agin.

[^5]:
    Of course, as is often the case, after spending enough time hacking 
    (to see what the right answer should be), the thinking becomes retroactively
    obvious, and it's easy to feel like you could have saved a lot of time by starting
    with the thinking.

    Try not to be overwhelmed by this. The only reason the answer seems obvious
    is _because_ we spent time computing lots of examples, working
    things out by hand (or by computer), and testing our conjectures to 
    see what _should_ be right. 



[1]: https://www.smbc-comics.com/
[2]: https://xkcd.com/356/
[3]: https://en.wikipedia.org/wiki/Model_category
[4]: https://sites.google.com/view/syeakel/
[5]: https://sites.google.com/site/patriciogallardomath/
