---
layout: post
title: Automatic Asymptotics with Sage
tags:
  - sage
---

Recurrence relations show up _all_ the time in combinatorics and computer 
science, and even simple objects give recurrences that are difficult or 
impossible to solve. Thankfully, we _can_ often find a [generating function][1]
for our objects, and through the power of complex analysis and algebraic geometry, 
we can use the singularities of the generating function in order to get good
_asymptotic estimates_. Software like [Maple][2] can automatically compute
asymptotic expansions for a lot of generating functions using the 
[asympt][4] function... Can [sage][3]?

The answer is "yes", which is why I'm writing this post, but the longer answer
is "with some work". Which is the _real_ reason I'm writing this post. 
I had to slog through a lot of kind of crummy documentation to get this working,
and I want to make sure that the next people looking into this have an easier
time.

There are two modules (that I can find) which provide features for computing
asymptotics:

 - [multivariate generating functions][5]
 - [asymptotic rings][6]

These both have pros and cons:

The former is slightly easier to work with, and allows generating functions with
multiple variables. The downside is that it
only works for functions with polynomial denominators[^1]. 

The latter has nicer documentation, works for more general functions, and 
gives more detailed asymptotic expansions. The downside is that it only works
for functions of a single variable, and it's kind of annoying to use because
it doesn't accept symbolic inputs natively. You also have to manually provide 
a list of singularities[^2].

---

Let's start with the multivariate case, since it's more complicated. I'll give
a code dump, then explain what's going on.

The tl;dr is that it works for functions of the form $h / p$ where $h$ is
a holomorphic function and $p$ is a polynomial. The number of variables is
irrelevant.

<div class="no_eval">
<script type="text/x-sage">

from sage.rings.asymptotic.asymptotics_multivariate_generating_functions \
  import FractionWithFactoredDenominatorRing

def multivar_asy(f, N=5, alpha=None, numeric=0):
  """
  compute the first N terms of the asymptotic expansion of f

  setting numeric = n will give floats with n digits of precision.

  if 

    f = sum_{ns} F_{ns} x^{ns} 

  for ns = (n1,...,nk) a multi-index, then we compute an 
  expansion for F_{r alpha} for alpha = (a1 ... ak) a given
  "direction" and r --> oo

  By default, we assume alpha = [1,...,1], which reduces to what we 
  almost certainly want in the one variable case
  """
  fn = f.numerator()
  fd = f.denominator()

  R_internal = PolynomialRing(QQ, fd.variables())

  # FFPD is the ring of quotients p/q
  # where p is in SR and q is in R_internal
  # rather confusingly we put the denominator ring before the numerator ring
  FFPD = FractionWithFactoredDenominatorRing(R_internal, SR)

  # but when we make new element of the ring, we put things in the right order
  # for some reason units in the denominator get clobbered, so we manually
  # add it in the numerator (this is consistent with the examples in the docs)
  fdFactored = R_internal(fd).factor()

  f = FFPD(fn / fdFactored.unit(), fdFactored)

  # now we choose a "direction" alpha
  if alpha == None:
    alpha = [1] * f.dimension()

  decomp = f.asymptotic_decomposition(alpha)

  result = 0
  n = 0
  for part in decomp:
    n += 1
    # this is brittle, but makes things work
    if part == FFPD(0, []):
      continue

    # p is supposed to be a minimal critical point for the denominator of part.
    # let's first find the critical points

    # first we find the smooth points
    I = part.smooth_critical_ideal(alpha)
    smoothSols = solve([SR(v) for v in I.gens()], 
                  [SR(v) for v in R_internal.gens()], 
                  solution_dict=True)

    # next we find the singular points
    J = part.singular_ideal()
    singSols = solve([SR(v) for v in J.gens()], 
                [SR(v) for v in R_internal.gens()], 
                solution_dict=True)

    s = smoothSols + singSols

    # remove any varieties of dimension > 0 from the space of solutions
    # I don't know if this will break things or not, but in my (limited)!
    # testing it seems fine.
    # If I were less lazy I would probably make this take the minimum value
    # across the whole variety? But doing it this way makes things agree with
    # the examples.

    sFiltered = []
    for soln in s:
      keep = True
      for v in soln.values():
        if not v.is_constant(): # remove any solutions involving a parameter
          keep = False
      if keep:
        sFiltered += [soln]

    # if we didn't find any solutions at all, give up.
    if len(sFiltered) == 0:
      if len(s) != 0:
        print("We finally found something where removing the varieties caused problems")
        return None
      
      else:
        print("no critical points were found. Giving up.")
        return None

    # otherwise we get the _minimal_ singularity
    pMin = sFiltered[0]
    for p in sFiltered:
      if sum([xi^2 for xi in p.values()]) < sum([yi^2 for yi in pMin.values()]):
        pMin = p

    # and finally get the asymptotics
    (a,_,_) = part.asymptotics(pMin, alpha, N, numerical=numeric) 

    result += a

  return result
</script>
</div>

This is pretty obviously cribbed from the examples [here][5], but the basic idea
is this:

We need the denominator of our generating function to be a factored polynomial,
so we build a polynomial ring with the variables in the denominator and factor
over that ring.

Then, we put this into `FFPD` to get an object that the module 
knows how to deal with. 

We choose a multi-index $\alpha$ which controls the "direction" in which
we take our asymptotics[^3]. For instance, if our generating function is 
$f(x,y) = \sum_{m,n} F_{m,n} x^m y^n$, then

- $\alpha = (1,1)$ will give us the asymptotics of $F_{n \alpha} = F_{n,n}$ as $n \to \infty$
- $\alpha = (2,1)$ will give us the asymptotics of $F_{n \alpha} = F_{2n,n}$ as $n \to \infty$
- etc.

If we view the $F_{m,n}$ as being located at the lattice points $(m,n)$ in the plane,
then $\alpha$ picks out the direction in which we move.

Next we look at the critical points of the denominator. That is, the points 
where its gradient is either undefined or vanishing. The former is the 
_singular_ case, and the latter is the _smooth_ case. 

In the one variable case, we know the asymptotics are controlled by the
singularity closest to the origin. See chapter $5$ of 
[_Generatingfunctionology_][9], for instance. 

From skimming these articles, we now have a whole [algebraic variety][12] of
singularities, and for _reasons_ the asymptotics are now governed by the 
critical points on this variety. In particular, we're on the hunt for the 
critical point which is closest to the origin (which we'll call the 
<span class=defn>Dominant Singularity</span>).

So now, what does the code do? Well we look for the location of the minimal
smooth point and the minimal singular point. Then take the smaller one and
run the asymptotic function provided by the module.

It seems to work quite well, and is surprisingly fast too. For a simple
example, we can try

<div class="no_eval">
<script type="text/x-sage">
multivar_asy(z/(1-z-z^2))
</script>
</div>

which outputs[^4]

$$
\frac{1}{5} \, \sqrt{5} \left(\frac{2}{\sqrt{5} - 1}\right)^{r}
$$

Of course, $$\frac{z}{1-z-z^2}$$ is the generating function for the fibonacci
numbers, and we've successfully recovered the asymptotic formula 
(though it requires some massaging to make it look like its usual presentation).

This really shines when it comes to multivariate series, though. For instance,
we know that

$$
\binom{n}{k} = [x^n y^k] (1 - x(1+y))^{-1}
$$

So if we're interested in the asymptotics of $\binom{3n}{n}$ we can compute

<div class="no_eval">
<script type="text/x-sage">
multivar_asy((1-x*(1+y))^(-1), alpha=[3,1], N=3)
</script>
</div>

which quickly gives

$$
\frac{1}{41472} \, \left(\frac{27}{4}\right)^{r} {\left(\frac{10368 \, \sqrt{6} \sqrt{2}}{\sqrt{\pi} \sqrt{r}} - \frac{1008 \, \sqrt{6} \sqrt{2}}{\sqrt{\pi} r^{\frac{3}{2}}} + \frac{49 \, \sqrt{6} \sqrt{2}}{\sqrt{\pi} r^{\frac{5}{2}}}\right)}
$$

Now $\binom{15}{5} = 3003$ and evaluating the above at $r=5$ gives $3002.931$.

---

But what if we're interested in generating functions whose numerator isn't
holomorphic, or whose denominator isn't a polynomial? It's clear that we
should be interested in such things, since the famous [catalan numbers][13]
already have the generating function 

$$
\frac{1 - \sqrt{1 - 4z}}{2z}
$$

For cases like this (which must be of a single variable), we work with
the second asymptotics package [here][6].

This is nice because it returns an asymptotic expansion, which is quite
intuitive to work with. The major downside, though, might be surprising:

It only works with (callable) python functions.

This is annoying[^5], but it really isn't _that_ much of a hassle to rewrite 
your function using `def`. We also need to provide the dominant singularities
by hand, which is also a bit of work[^6].

If and when I get around to automatically finding singularities, I'll update
this code, but for now there's _much_ less boilerplate here than in the
previous case:

<div class="no_eval">
<script type="text/x-sage">
# interestingly, it seems like it doesn't matter at all
# what asymptotic ring you use.
AsyRing = AsymptoticRing('QQ^n * n^QQ * log(n)^QQ', QQ)

def singlevar_asy(f, N=5, sings=None):
  """
  compute the first N terms of the asymptotic expansion of f

  sings is a list of dominant singularities
  TODO: get these automatically somehow?
  """
  return AsyRing.coefficients_of_generating_function(f, sings, precision=N)
</script>
</div>

The documentation for this function is also quite good, so I'll stick to
one example. For the catalan numbers, we'll have:

<div class="no_eval">
<script type="text/x-sage">
def cat(z):
  return (1 - sqrt(1-4*z))/(2*z)
</script>
</div>

This looks like it has singularities at $0$ (which makes the denominator vanish)
and $1/4$ (which makes the $\sqrt{\cdot}$ vanish), but actually it only has the
singularity at $1/4$. The singularity at $0$ is removable. So we call

<div class="no_eval">
<script type="text/x-sage">
singlevar_asy(cat, sings=[1/4])
</script>
</div>

which outputs

$$
\frac{1}{\sqrt{\pi}} 4^{n} n^{-\frac{3}{2}} - \frac{9}{8 \, \sqrt{\pi}} 4^{n} n^{-\frac{5}{2}} + \frac{145}{128 \, \sqrt{\pi}} 4^{n} n^{-\frac{7}{2}} - \frac{1155}{1024 \, \sqrt{\pi}} 4^{n} n^{-\frac{9}{2}} + \frac{36939}{32768 \, \sqrt{\pi}} 4^{n} n^{-\frac{11}{2}} + O\!\left(4^{n} n^{-6}\right)
$$

A quick massage turns this into the (maybe not so) familiar

$$
\frac{4^n}{\sqrt{\pi}} 
\left ( 
  n^{-3/2} - 
  \frac{9}{8} n^{-5/2} +
  \frac{145}{128} n^{-7/2} -
  \frac{1155}{1024} n^{-9/2} +
  \frac{36939}{32768} n^{-11/2}
  \pm O \left ( n^{-13/2} \right )
\right )
$$

which you can find as formula (20) [here][14].

---

Lastly, we can combine these different asymptotic approximations into one 
function. In my `init.sage` file, which you can find [here][15], I've defined
the function

<div class="no_eval">
<script type="text/x-sage">
def asy(f, *args, **kwargs):
  try:
    return multivar_asy(f,*args,**kwargs)
  except:
    return singlevar_asy(f,*args,**kwargs)
</script>
</div>

This is definitely too brittle to give to other people, but it works
fine for my purposes. One day I'd like to make it a bit more robust
(this is not how `try`/`except` statements are supposed to be used), 
and ideally make it a bit more automatic (in particular following
the discussion of `singlevar_asy` above). Another option might be to try 
and get it working with the [`singularlity_analysis`][16] function, which
would require a certain amount of parsing...
Anyways, as it stands it's a plenty servicable substitute for maple's 
`asympt` function, and I'm glad I took the time to code it up. 

If anyone has any other ideas for making this more usable, or encounters
any problems, definitely let me know! 

If not, take care and stay warm!

I'll see you all in the next one ^_^.

---

[^1]:
    You can read about these algorithms and their proofs

    - [here][7] (for the smooth case)
    - [here][8] (for the singular case)

    There's also Pemantle and Wilson's 
    [_Analytic Combinatorics in Several Variables_][10] or Melczer's 
    [_An Invitation to Analytic Combinatorics_][11], which both look
    quite good. Unfortunately I haven't had time to read either.

[^2]:
    I'm curious if I can automate the search for these singularities... 
    I feel like it shouldn't be too hard, but I need to think about it.

[^3]:
    As an aside, I keep reading this as "asymptomatic" out of the corner of my
    eye, which definitely tells you something about my current mental state...

[^4]:
    Sorry I'm not making these evaluate inline like I normally do. You'll have
    to trust me (or check yourself!) that the computation really is quite fast.

    The issue is that I don't want to copy/paste the definition 
    of `multivar_asy` into each cell. I think that clutters things up.

    I could use _linked_ sage-cells, but linked cells have to be evaluated 
    in the right order, and aren't allowed to be auto-evaluated. I think that's
    a bit user-unfriendly, so I've decided to just show the inputs/outputs
    (which is what really matters in any case).

[^5]:
    And part of me wants to go in and try to fix it

[^6]:
    This is something I really think should be automate-able, though, and 
    I'll probably fight with it some more when I have the time.

[1]: https://en.wikipedia.org/wiki/Generating_function
[2]: https://en.wikipedia.org/wiki/Maple_(software)
[3]: https://sagemath.org
[4]: https://www.maplesoft.com/support/help/maple/view.aspx?path=asympt
[5]: https://doc.sagemath.org/html/en/reference/asymptotic/sage/rings/asymptotic/asymptotics_multivariate_generating_functions.html
[6]: https://doc.sagemath.org/html/en/reference/asymptotic/sage/rings/asymptotic/asymptotic_ring.html#introductory-examples
[7]: http://arxiv.org/abs/0803.2914
[8]: http://arxiv.org/abs/1009.5715
[9]: https://www2.math.upenn.edu/~wilf/gfology2.pdf
[10]: https://www.cambridge.org/core/books/analytic-combinatorics-in-several-variables/7FD6C5820465ECC25FBDF42236BFAEB2
[11]: https://melczer.ca/textbook/
[12]: https://en.wikipedia.org/wiki/Algebraic_variety
[13]: https://en.wikipedia.org/wiki/Catalan_number
[14]: https://mathworld.wolfram.com/CatalanNumber.html
[15]: https://github.com/HallaSurvivor/dotfiles/blob/master/init.sage
[16]: https://doc.sagemath.org/html/en/reference/asymptotic/sage/rings/asymptotic/asymptotic_expansion_generators.html#sage.rings.asymptotic.asymptotic_expansion_generators.AsymptoticExpansionGenerators.SingularityAnalysis
