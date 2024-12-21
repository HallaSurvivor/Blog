---
layout: post
title: $\mathsf{B}\text{Diff}(\Sigma)$ Classifies $\Sigma$-bundles
tags:
  - 
---

I've been trying to learn all about topological (quantum) field theories, the 
cobordism hypothesis, and how to use $(\infty,n)$-categories. This is all 
in service of some stuff I'm doing with skein algebras (which are part of a 
"$3+1$ TQFT" often named after [Crane--Yetter][1], but I believe the state 
of the art is due to [Costantino--Geer--Haïoun--Patureau-Mirand][2]), but 
it's incredibly interesting in its own right and it's been super fun to get a 
chance to learn more physics and learn _way_ more about topology and 
higher categories.

Along the way, I was watching [a lecture by Jacob Lurie][3] where he mentions 
something that should probably be obvious (but wasn't to me):

<div class=boxed markdown=1>
For a (smooth) manifold $F$, $\mathsf{B}\text{Diff}(F)$ classifies bundles 
with fibre $F$
</div> 

That is, given a manifold $M$ we have a natural bijection

$$
\begin{gather}
\Big \{ 
  \text{homotopy classes of maps } M \to \mathsf{B} \text{Diff}(F) 
\Big \} \\
\longleftrightarrow  \\
\Big \{
  \text{fibre bundles } \pi : E \to M \text{ where every fibre is diffeomorphic to $F$}
\Big \}
\end{gather}
$$

I asked about this in the [category theory zulip][4], and got some great 
responses that still took me a while to digest. Actually, it wasn't until 
I started reviewing a bunch of material on principal bundles[^2] that 
everything clicked into place for me.

Over the course of this post, I'll hopefully make this bijection obvious, and 
I'll explain some facts about bundles along the way. This should serve as a nice 
quick blog post to write during my winter break since I've been _extremely_ 
stressed for the last two months trying to get all my postdoc applications 
done[^1]. Thankfully it's all finally behind me, and I'm back in New York 
with people I love, so I'm resting up and doing math again (which have both 
been _fantastic_ for my mental health).

Let's get to it!

---

First, let's remember what a bundle even is. Say we have a base space $M$ 
and a map $\pi : E \to M$. Then for each point $m \in M$ we have the 
fibre $E_m = \pi^{-1}(m)$, and so we can view $\pi$ as a _family_ of spaces 
$(E_m)$ indexed by points of $M$. We think of $E_m$ as being "vertical" 
over $m \in M$, and we think of the topology on $E$ as telling us how these 
fibres are glued to each other "horizontally":

TODO: picture of a bundle, rectangle over a line with another vertical line 
indicating the fibre

We say that $\pi : E \to M$ is a 
[fibre bundle][5] if it's "locally trivial" in the sense that (locally)
the fibres are all $F$, and these copies of $F$ are all glued to each other 
in the most obvious possible way. Because we mathematicians feel the need to 
make newcomers feel inadequate, we call this most obvious way the "trivial" 
bundle: $\pi : M \times F \to M$.

For a bundle to be _locally_ trivial we don't ask for it to literally be 
$M \times F$, that's asking too much. Instead we ask that for every point 
$m \in M$ there should be a neighborhood $U_m$ so that 
$\pi^{-1}(U_m) \cong F \times U_m$[^3].

TODO: picture of a trivial and a locally trivial bundle, moebius strip obviously

We say that such a bundle is a <span class=defn>Fibre Bundle with Fibre $F$</span>,
and here's a completely natural question:

<div class=boxed markdown=1>
Can we classify all fibre bundles with fibre $F$ over a base space $M$?
</div>

Let's think about how we might do this from a conceptual point of view, 
and that will lead us to the answer in the title of this post. Then we'll 
reinterpret that conceptual understanding in much more concrete language, 
and hopefully explain why people care so much about principal bundles 
at the same time!

<br>

If we put our [type theory][6] hats on[^6], then we want to think about a fibre 
bundle as being a map from our base space $M$ into a 
"space of all $F$s". Then we think of this map as assigning an $F$ to 
every point of $M$, and this is exactly[^4] the data of a fibre bundle!

But what should a "space of all $F$s" look like[^5]? Well, as a first try 
let's just take a huge manifold $\mathcal{U}$ and look at all copies of 
$F$ sitting inside it! For instance, we might take $\mathbb{R}^\infty$, 
and then an "$F$ sitting inside it" is an embedding 
$\iota : F \hookrightarrow \mathbb{R}^\infty$... almost! A choice of 
embedding has the ~bonus data~ of a parameterization, which an abstract 
"copy of $F$" wouldn't have. We're only interested in what's morally 
the _image_ of a particular embedding, so we should quotient out by 
reparameterization. Concretely, if $\varphi : F \overset{\sim}{\rightarrow} F$ 
is a diffeomorphism, then $\iota$ and $\iota \circ \varphi$ represent 
the same "copy" of $F$ in $\mathbb{R}^\infty$, so we find ourselves interested 
in the space

$$\{ \iota : F \hookrightarrow \mathbb{R}^\infty \} \big / \text{Diff}(F).$$

Now it feels like we made a choice here, taking $\mathcal{U} = \mathbb{R}^\infty$,
but we can worm our way out of this choice with homotopy theory! Indeed it's 
believable that $$\{ \iota : F \hookrightarrow \mathbb{R}^\infty \}$$ should be 
contractible, since if $F$ is finite dimensional then any two embeddings 
lie in a small subspace of $\mathbb{R}^\infty$, so there's plenty of room to 
homotope them into each other. Then for any two such homotopies there's 
_still_ room to fill in the resulting circle, and so on. Since the 
space of embeddings is contractible, up to homotopy we're working with[^7] 

$$
\star \big / \text{Diff}(F)
$$

and if we make "$\mathcal{U}$ is sufficiently large" mean 
"the space of embeddings of $F$ in $\mathcal{U}$ is contractible", then 
we'll get $\star \big / \text{Diff}(F)$ independent of this choice. 
Of course, $\star \big / \text{Diff}(F)$ is frequently called the 
[Classifying Space][7] $\mathsf{B} \text{Diff}(F)$, and so we're halfway 
to our goal!

We normally think of $\mathsf{B}G$ for a group $G$ as an object classifying 
"principal $G$-bundles", so that a map $M \to \mathsf{B}G$ is the same 
thing as a bundle over $M$ whose fibres are all isomorphic to $G$...
So, naively, it sounds like a map $M \to \mathsf{B}\text{Diff}(F)$ should be 
the data of a bundle over $M$ whose fibres are $\text{Diff}(F)$! But we 
_wanted_ a bundle over $M$ whose fibres are $F$! What gives?

The answer comes from the [Associated Bundle Construction][9], which is 
_the reason_ to care about principal bundles at all! In a remarkably 
strong sense, we can understand _every_ "$G$-bundle" as long as we're able 
to understand the _principal_ $G$-bundles! Let's see how, then use it to 
solve our problem in a (more) down-to-earth way.

---

Concretely, we might understand a fibre bundle by picking a 
[good open cover][10] $$\{ U_\alpha \}$$. Then we pick local trivializations 
$\varphi_\alpha : \pi^{-1}(U_\alpha) \overset{\sim}{\to} U_\alpha \times F$. 

If we want to answer a (local) question about the bundle, we can use one of 
these $\varphi_\alpha$s to transfer the question to a question about 
$U_\alpha \times F$, which is often easier to work with. But crucially 
we need to know that we'll get the same answer no matter which of these 
"charts" $U_\alpha$ we work with. For instance, say our fibres are all 
$\mathbb{R}$. Then a natural question might be 
"is this element of the fibre $0$?". In the lefthand bundle we get a 
consistent answer since we always glue $0$ to $0$, but in the righthand 
bundle we can't answer this question since we glue $0$ to $1$, so the 
answer depends on if we're working in $U_\alpha$ or $U_\beta$:

TODO: draw this picture

It turns out that more fundamental than the particular choice of 
trivialization are the "transition maps" 
$\varphi_\beta \circ \varphi_\alpha^{-1} : 
(U_\alpha \cap U_\beta) \times F \overset{\sim}{\to} 
(U_\alpha \cap U_\beta) \times F$
which tell us how to translate computations between our $\alpha$ and $\beta$ 
charts. These have to be the identity on the $U_\alpha \cap U_\beta$ part, so 
the interesting data is a map $\varphi_{\beta \alpha} : F \overset{\sim}{\to} F$
which tells us how to glue the $\alpha$ and $\beta$ charts along their 
intersection. 

Now if we want to answer questions corresponding to "bonus structure" on 
our fibre, we need to make sure we only ever glue in a way that preserves 
the answers to these questions. That is, instead of $\varphi_{\beta \alpha}$ 
being _any_ old diffeomorphism of $F$, we want it to be in the subgroup 
of diffeomorphisms respecting this structure[^8]. If we call this 
subgroup $G$, then we call our bundle a $G$-bundle.

For example, if our fibres are all $\mathbb{R}^n$ and we want to ask 
vector-spacey questions, then we should only glue them using diffeomorphisms 
that respect the vector space structure. That is, we should only glue along 
$\mathsf{GL}(n) \subseteq \text{Diff}(\mathbb{R}^n)$, and so we're working 
with a $\mathsf{GL}(n)$-bundle. If we moreover want to ask questions about 
the usual inner product on $\mathbb{R}^n$, then we have to glue in a way 
that preserves the inner product so our transition functions will be 
valued in $\mathsf{O}(n)$[^9].

So it turns out the crucial data for a $G$-bundle are the transition maps 
$\varphi_{\beta \alpha} : U_\alpha \cap U_\beta \to G$. These have to satisfy 
the <span class=defn>Cocycle Condition</span>[^10] that 
$\varphi_{\gamma \beta} \varphi_{\beta \alpha} = \varphi_{\gamma \alpha}$, 
which crucially _never mentions the fibre $F$_! So we learn that $G$-bundles 
can be classified without referencing the fibre $F$ at all! 

Indeed, say we have the data of a $G$-cocycle $\varphi_{\beta \alpha}$. Then 
for _any_ space $F$ with a $G$-action we can build a bundle with fibres $F$ 
by using these as our transition functions. Since we can choose any $F$ we 
want (at least for the purposes of classification) it's reasonable to ask 
if there's a "best" choice of fibre that makes things easier. To answer this 
one might ask if there's a "best" choice of set that $G$ acts on, and from 
there we might be led to say that the best choice is $G$ acting on _itself_ 
by multiplication!

In this case our fibres are all $G$, and it's easy to see this preserves 
"relative information" about $G$ since $h^{-1}k = (gh)^{-1}(gk)$ and 
the value of $h^{-1}k$ is preserved by the multiplication action. However 
this action does _not_ preserve "absolute information" about $G$, such as 
the identity, since $ge = g \neq e$. The structure that's preserved is called 
a [torsor][12], and so we see that any $G$-valued cocycle on $M$ naturally 
gives us a bundle of $G$-torsors on $M$! This is called a 
<span class=defn>Principal $G$-Bundle</span>, and from the earlier discussion 
if we can classify the principal $G$-bundles, we can classify _all_ 
$G$-bundles easily! It turns out that in many many ways if we want to 
understand $G$-bundles it's enough to understand the principal ones. 
For instance [connections][13] on a $G$-bundle arise in a natural way from 
connections on a principal $G$-bundle, and principal $G$-bundles give us 
a way to work with bundles in a coordinate-invariant way. I won't say 
any more about this, in the interest of keeping this post quick, but I'll 
point you to the excellent blog posts by Nicolas James Marks Ford[^11] on 
[$G$-bundles][14] and [connections][15], as well as the relevant sections 
of Baez and Muniain's excellent book [Gauge Fields, Knots, and Gravity][16].

<br>

Concretely, how can we implement this bijection?

Well, given a $G$-bundle $\pi : E \to M$ we can fix a good open cover
$$\{ U_\alpha \}$$ of $M$, and we can read off the transition maps 
$\varphi_{\beta \alpha} : U_\alpha \cap U_\beta \to G$, and then we can 
build a new $G$-bundle $\widetilde{E} \to M$ whose fibres are all $G$ 
(called the <span class=defn>Associated Bundle</span> to $E$) by gluing 
copies of $G$ together with these same transition maps $\varphi_{\beta \alpha}$.
This is a principal $G$-bundle.

In the other direction, say we have a principal $G$-bundle $\pi : P \to M$. 
Then if $G$ acts on any space $F$ we can build a new $G$-bundle which is 
fibrewise given by $E_m = (P_m \times F) \big / \sim$ where we quotient by 
the relation $(hg,f) \sim (h, gf)$. This is, in some sense, coming from the 
"universality" of $G$ as a $G$-set that made $G$ the "best" choice of set 
with a $G$-action[^12]!

It's a cute exercise to check that these operations are inverse to each other!

<br>

Now. Where did we start, and where did we end? Well we can read on 
[wikipedia][7] that $\mathsf{B}G$ classifies principal $G$-bundles. 
But we know that once we fix an action of $G$ on $F$, 
the principal $G$-bundles are in bijection with $G$-bundles with 
fibre $F$! 

So using the obvious action of $\text{Diff}(F)$ on $F$, 
and remembering that _all_ bundles with fibre $F$ have transition functions 
landing in $\text{Diff}(F)$, we get a natural bijection 

$$
\begin{gather}
\Big \{ 
    \text{homotopy classes of maps } M \to \mathsf{B}\text{Diff}(F) 
\Big \} \\
\longleftrightarrow \\
\Big \{
    \text{principal } \text{Diff}(F) \text{ bundles on } M
\Big \} \\
\longleftrightarrow \\
\Big \{
    \text{bundles on $M$ with fibre $F$ whose transition maps live in $\text{Diff}(F)$}
\Big \} \\
\longleftrightarrow \\
\Big \{
    \text{all bundles on $M$ with fibre $F$}
\Big \}
\end{gather}
$$


Which is exactly what we were looking for! 



---

In hindsight, I'm not sure whether the story involving a "space of all $F$s" 
or the story about associated bundles is "more concrete"... I know the second 
story is easier to make precise, but I think both versions are good to see. 

I'm _super_ happy to have finished this post in two days. I started writing it 
last night when I got to my friends' house in New York, and I finished 
it this morning while they were addressing and signing a bunch of christmas 
cards. It's good to be thinking and writing about math again after my 
two months of postdoc application hell, and I'm feeling SO comfortable 
and relaxed it's just great to be around people I love.

I'm going to hopefully find time to finish writing a series on skein algebras,
hall algebras, and fukaya categories (which is the topic of my thesis) in the 
next month or two. That will be great, because I have a TON of fascinating 
stuff to share ^_^.

As always, thanks for hanging out. Now more than ever 
stay safe, stay warm, and take care of each other. Nobody else is going to.


---

[1]: https://ncatlab.org/nlab/show/Crane-Yetter+model
[2]: https://arxiv.org/abs/2306.03225
[3]: https://www.youtube.com/watch?v=h1fsumqDxqk
[4]: https://categorytheory.zulipchat.com/#narrow/stream/229199-learning.3A-questions/topic/Bundles.20with.20fibre.20F.20are.20classified.20by.20BDiff.28F.29.3F
[5]: https://en.wikipedia.org/wiki/Fiber_bundle
[6]: https://en.wikipedia.org/wiki/Dependent_type
[7]: https://en.wikipedia.org/wiki/Classifying_space
[8]: https://en.wikipedia.org/wiki/Moduli_space
[9]: https://en.wikipedia.org/wiki/Associated_bundle
[10]: https://ncatlab.org/nlab/show/good+open+cover
[11]: https://en.wikipedia.org/wiki/%C4%8Cech_cohomology
[12]: https://en.wikipedia.org/wiki/Principal_homogeneous_space
[13]: https://en.wikipedia.org/wiki/Connection_(vector_bundle)
[14]: http://nicf.net/articles/connections-gbundles/
[15]: http://nicf.net/articles/connections-crash-course/
[16]: http://home.ustc.edu.cn/~zcj12138/reference/Gauge%20Fields,%20Knots%20and%20Gravity.pdf
[17]: https://math.stackexchange.com/questions/3154727/is-there-a-tensor-product-of-g-sets


[^1]:
    For political reasons at UCR, it seems like _none_ of the rising 6th 
    years will get TA positions next year. Which means that me and a 
    LOT of people in my cohort are having to graduate a year earlier than 
    we planned. We found this out in _mid october_, crucially after the 
    NSF grant deadline, and only a month and a half before most postdoc 
    applications were due.

    I made it happen, but it's been a really unpleasant two months.

[^2]:
    I'm trying to learn some gauge theory for other reasons

[^3]:
    In this situation we say our condition is "local on the base" 
    or "local on the target" since we have a neighborhood $U_m$ for every 
    $m \in M$ the "base space", which is the target of the map 
    $\pi : E \to M$. 
    This is to be contrasted with a condition that's "local on the domain" 
    or "local on the total space" or "local on the source", where we have a 
    neighborhood $U_e$ for every $e \in E$ the "domain" or "total space" or 
    "source" of the map $\pi : E \to M$.

[^4]:
    It's reasonable to ask why this definition only gives us locally 
    trivial bundles. The reason is that a homotopy class of a map from 
    a contractible space to the "space of all $F$s" is the same thing as a 
    map from a point to this space. Composing with the 
    contraction homotopy we find that the bundle we classify is trivial. 
    So if you take a point if $M$ and restrict your map to a 
    contractible neighborhood of $m$, you'll find that the bundle is trivial 
    on that neighborhood.

[^5]:
    I got this argument from Kevin Carlson in the CT Zulip, from the 
    [same thread][4] I linked earlier.

[^6]:
    You could just as well put your [moduli space][8] hat on, if you're 
    more comfortable with that. One of the 

[^7]:
    Here, of course, we have to work $\infty$-categorically and interpret 
    this quotient as a _homotopy_ quotient in order for it to be interesting!

[^8]:
    This is what "structure groups" are all about. I had half a mind to 
    write up a longer thing explaining how structure groups work and why they 
    correspond to structure on the fibre surviving to global structure on 
    the bundle (especially because it was something that took me a while 
    to understand)... But I also want this post to be done quickly, and I 
    found myself wanting to draw a bunch of pictures and write a bunch of 
    stuff about that, so... I didn't 😌.

    I'm sure we'll talk more about it someday.

[^9]:
    If at this point you're thinking that if we don't want to preserve 
    ~any~ bonus structure we should take our structure group to be the 
    whole of $\text{Diff}(F)$, then congratulations! 
    You are making an observation that would have saved me... a lot of 
    time and confusion a few months ago, haha.

[^10]:
    I won't get into this here, and since I want this to be quick I don't want 
    to find a good reference, but this use of the word "cocycle" isn't an 
    accident, and indeed we're computing the [Čech cohomology][11] of 
    the base space with coefficients in $G$. The cocycle condition tells us 
    we're considering cocycles, and the coboundaries tell us when 
    we're describing the same bundle with different intitial choices of 
    trivialization.

[^11]:
    It's kind of hilarious how similar his blog looks to mine. We're using 
    _very_ similar color schemes.

[^12]:
    Note also that the action of left multiplication of $G$ on itself 
    commutes with ("preserves") the action of right multiplication of $G$ 
    on itself (this is associativity). So a principal $G$-bundle has a 
    _global_ right action of $G$, and a trivial bundle with fibre $F$ 
    has a global left action of $G$, since _the identity_ diffeomorphism 
    preserves the left action of $G$ on $F$.

    So we have two bundles, one with a global right $G$-action and one with 
    a global left $G$-action. So we can take thier [tensor product][17] 
    to be left with a new bundle, not necessarily admitting a global $G$-action.
