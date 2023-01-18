---
layout: post
title: 
tags:
  - 
---

This is the sister post to blah blah blah

Make this interactive

<div class="linked_auto">
<script type="text/x-sage">
"""
Compute the maximum and expected game lengths for 
n players each wearing either a red or blue hat.
See the main blog post for more.
"""

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

    for v in G.vertices():
        for w in G.vertices():
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
        if (v,w,l) in G.edges() or (w,v,l) in G.edges():
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
    for v in G.vertices():
        if isIsolated(G,v,l):
            ws += [v]

    G.delete_vertices(ws)

    return ws

def playGame(n):
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
    print("average game length: ", avg, "   ", avg.n())
    print("probability of max length", prob, "   ", prob.n())
    return out

</script>
</div>
