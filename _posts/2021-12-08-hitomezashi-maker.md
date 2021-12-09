---
layout: post
title: A Hitomezashi Maker
tags:
  - pretty-pictures
---

It's been a hot second since I've done something artistic, and a recent
[numberphile video][1] gave me something small and simple to do! 
Plus, a really close friend of mine is a talented fibre artist, 
and since this type of artwork ([hitomezashi][2]) is originally a kind
of decorative mending, I thought it would be fun to code this up and
send it to her! It makes a great demo even without the fibre background,
and I hope you all have fun playing with it ^_^.

It's probably worth watching the video first, as otherwise it won't make
a _ton_ of sense what this is doing, but the idea is pretty simple: 
You turn a pair of bitstrings into a pattern by reading a $0$ as 
"start at the edge" and a $1$ as "start off the edge". You can input your
own bitstrings (or words, which we can convert to bitstrings), or you can 
pick random bitstrings, where you can set the vertical or horizontal 
probability of choosing a $0$ or a $1$ in any given position in the string.

It turns out the regions you build in this way are always $2$-colorable,
which is a cute exercise that they bring up in the video. The proof follows
once you make the right observation, and I encourage you to give it a go! 
In addition to the choice of bitsring, I've added a slightly more nuanced
way you can show your artistry by adding an option to choose the $2$ colors
that get used!

Apologies in advance that this is a bit slow, haha. It turns out that
making graphs in [sage](https://sagemath.org) is _really_ not the right
tool for this! Still, this gets the job done ^_^.

---

<div class="linked_auto">
<script type="text/x-sage">

def mkLine(n,b,d,t,sc):
  """
  Make one row/col of the diagram.

  @n is the index for which row/col to make
  @b is the bit -- start on or start off the line
  @d is the direction -- is this a row or a col
  @t is the total number of dashes to make
  @sc is the color to use for the stitches
  """

  p = Graphics()
  for k in range(t):
    if k % 2 == b:
      if d=="row":
        p += line([(n,k),(n,k+1)],rgbcolor=sc) 
      if d=="col":
        p += line([(k,n),(k+1,n)],rgbcolor=sc) 
  
  return p


def mkSquare(r,c,color):
  """
  Make a square at row @r column @c with color @color
  """

  return polygon([(r,c),(r,c+1),(r+1,c+1),(r+1,c)], rgbcolor=color, alpha=0.75)



def mkPattern(rowString, colString, color1, color2, stitchColor, showBits):
  """
  Make the whole pattern
  """

  p = Graphics()
  p.set_aspect_ratio(1)
  p.set_axes_range(-1,len(rowString)+1,-1,len(colString)+1)

  # make the horizontal stitches
  for (n,b) in enumerate(rowString):
    p += mkLine(n,b,"row",len(colString),stitchColor)
    if showBits:
      p += text(b,(n, -0.5))

  # make the vertical stitches
  for (n,b) in enumerate(colString):
    p += mkLine(n,b,"col",len(rowString),stitchColor)
    if showBits:
      p += text(b,(-0.5,n))

  # shade in the regions
  cur = color1
  curRow = color1
  for r in range(len(rowString)):
    for c in range(len(colString)):

      if (r,c) == (0,0):
        p += mkSquare(r,c,cur)

      elif c != 0:
        if r%2 == colString[c]:
          if cur == color1:
            cur = color2
          else:
            cur = color1
        p += mkSquare(r,c,cur)

      elif c == 0:
        if c%2 == rowString[r]:
          if curRow == color1:
            curRow = color2
          else:
            curRow = color1
        cur = curRow
        p += mkSquare(r,c,cur)

  return p


def mkRandString(t,p):
  """
  Make a random string of length @t of 0s and 1s 

  0 is chosen with probability @p
  """
  s = []
  for _ in range(t):
    if random() < p:
      s += [0]
    else:
      s += [1]

  return s


def stringToBits(s):
  """
  Convert a string to a bitstring.

  If s is already a bitstring, leave it alone.
  If s is entirely numerical, reduce each digit mod 2
  If s is entirely alphabetical, use vowels/consonants, like the video.
  Otherwise, convert to unicode and use parity.
  """

  # we remove any spaces so that sentences can be converted as letters
  s = s.replace(" ", "")

  if s.isdigit():
    return [int(c) % 2 for c in list(s)]

  if s.isalpha():
    return [int(c in ["a", "e", "i", "o", "u"]) for c in list(s)]

  return [ord(c) % 2 for c in list(s)]
    

# We have to do this hacky nested-interact thing to make everything go smoothly.
# First we say whether we want the rows/cols to be randomized.
# Depending on the answer, we display either a text box or a slider for each.
# Then we put the aesthetic choices like colors in the innermost layer so that
# changing them won't re-randomize anything from earlier layers.

@interact
def _(randomRow=('randomize row?', True), randomCol=('randomize col?', True)):

  # we want the random starting probabilities to be interesting,
  # so make sure we wind up between, say, .33 and .66
  r_init = round(0.33 + 0.33*random(),2)
  c_init = round(0.33 + 0.33*random(),2)

  if randomRow:
    if randomCol:
      @interact
      def _(rowPercent=slider([(k/100).n(digits=2) for k in range(0,101)], default=r_init),
            colPercent=slider([(k/100).n(digits=2) for k in range(0,101)], default=c_init)):

        rowLen = randint(20,40)
        rowString = mkRandString(rowLen, rowPercent)

        colLen = randint(20,40)
        colString = mkRandString(colLen, colPercent)

        @interact
        def _(color1=Color('white'), 
              color2=Color('white'), 
              stitchColor=Color('black'), 
              showBits=True):
          print("rowString: {}".format("".join([str(b) for b in rowString])))
          print("colString: {}".format("".join([str(b) for b in colString])))

          show(mkPattern(rowString, colString, color1, color2, stitchColor, showBits), 
               axes=false)


    else:
      @interact
      def _(rowPercent=slider([(k/100).n(digits=2) for k in range(0,101)], default=r_init),
            colString=""):

        rowLen = randint(20,40)
        rowString = mkRandString(rowLen, rowPercent)

        colString = stringToBits(colString)

        @interact
        def _(color1=Color('white'), 
              color2=Color('white'), 
              stitchColor=Color('black'), 
              showBits=True):
          print("rowString: {}".format("".join([str(b) for b in rowString])))
          print("colString: {}".format("".join([str(b) for b in colString])))

          show(mkPattern(rowString, colString, color1, color2, stitchColor, showBits), 
               axes=false)



  else:
    if randomCol:
      @interact
      def _(rowString="",
            colPercent=slider([(k/100).n(digits=2) for k in range(0,101)], default=c_init)):

        rowString = stringToBits(rowString)

        colLen = randint(20,40)
        colString = mkRandString(colLen, colPercent)

        @interact
        def _(color1=Color('white'), 
              color2=Color('white'), 
              stitchColor=Color('black'), 
              showBits=True):
          print("rowString: {}".format("".join([str(b) for b in rowString])))
          print("colString: {}".format("".join([str(b) for b in colString])))

          show(mkPattern(rowString, colString, color1, color2, stitchColor, showBits), 
               axes=false)

    else:
      @interact
      def _(rowString="",
            colString=""):

        rowString = stringToBits(rowString)

        colString = stringToBits(colString)

        @interact
        def _(color1=Color('white'), 
              color2=Color('white'), 
              stitchColor=Color('black'), 
              showBits=True):
          print("rowString: {}".format("".join([str(b) for b in rowString])))
          print("colString: {}".format("".join([str(b) for b in colString])))

          show(mkPattern(rowString, colString, color1, color2, stitchColor, showBits), 
               axes=false)

</script>
</div>

<div class=boxed markdown=1>
  Later on in the video, they switch over to an isoperimetric version of this
  idea, where they work with triangles instead of squares, and they have
  _three_ input strings. Can you write code, analogous to the above, which 
  lets people play around with this alternative approach?
</div>


[1]: https://www.youtube.com/watch?v=JbfhzlMk2eY
[2]: https://en.wikipedia.org/wiki/Sashiko
