---
layout: post
title: 
tags:
  - 
---

This is the sister post to the [main post][1] on the board game clue. 
In this post we give some sage code for analyzing a simpler game that 
my old professor [Adam Bjorndahl][2] used to use to introduce modal logic.
It won't make a ton of sense without the context in the main post,
so I suggest reading it first ^_^.

<div class="linked_auto">
<script type="text/x-sage">

def areAdj(v,w):
    """
    Check if v and w (n-tuples from [0,1]) are adjacent in the cube graph.

    If they are, return in which position they differ
    If the aren't, return None
    """
    diffs = [i for i in range(len(v)) if v[i] != w[i]]

    if len(diffs) == 1:
        return diffs[0]
    else:
        return None

def buildFrame(n):
    """
    Return the starting frame for the game
    """
    G = Graph()
    G.add_vertices([tuple(x) for x in Tuples([0,1],n)])

    for v in G.vertices(sort=True):
        for w in G.vertices(sort=True):
            l = areAdj(v,w)
            if l is not None:
                G.add_edge(v,w,l)

    G.delete_vertex((0,) * n)
    return G

def getLabeledNeighbors(G,v,l):
    """
    Get neighbors of v in G whose witnessing edge has label l
    """
    
    ns = []
    for w in G.neighbors(v):
        if (v,w,l) in G.edges(sort=True) or (w,v,l) in G.edges(sort=True):
            ns += [w]

    return ns

def isIsolated(G,v,l):
    """
    True iff v is l-isolated in G
    """

    ns = getLabeledNeighbors(G,v,l)
    return len(ns) == 0

def playTurn(G,l):
    """
    Player l takes their turn.

    We return a list of worlds ws where player l wins this turn,
    and *sigh* we muate G to delete all the vertices in ws.

    I'm not happy about this.
    """

    ws = []
    for v in G.vertices(sort=True):
        if isIsolated(G,v,l):
            ws += [v]

    G.delete_vertices(ws)

    return ws

@interact
def playGame(n=selector(values=list(range(1,11)), label="players", default=3)):
    """
    Play a game with n players.

    Return a list whose ith entry is a list of worlds where
    the game ended on turn i.

    Also, print the maximum length of a game, the average length of a game,
    and the probability that the game is of maximum length
    """

    G = buildFrame(n)

    out = [[]] # nobody wins on turn 0
    cur = 0 # player 0 goes first
    turn = 1 # we start at turn 1

    while G: # really while G has vertices
       out += [playTurn(G,cur)]
       cur = (cur + 1) % n
       turn += 1

    maxm = len(out) - 1
    avg  = 0

    for (i,ws) in enumerate(out):
        avg += i * len(ws)
    avg = avg / (2^n - 1)

    prob = len(out[-1]) / (2^n - 1)

    print("maximum game length: ", maxm)
    print("average game length: ", avg, " (", avg.n(), ")")
    print("probability of max length: ", prob, " (", prob.n(), ")")
    print("")

    for (i,ws) in enumerate(out):
        if i != 0:
            print("worlds where someone wins on turn {}:".format(i))
            # there MUST be a better way to do this, haha
            wsFormatted = [
                str(w).replace('(', '').replace(')', '').replace(',', '').replace(' ','')
                 for w in ws]
            print(wsFormatted)
</script>
</div>

---

[1]: /2023/01/17/clue.html
[2]: https://www.adambjorndahl.com/
