---
layout:     post
title:      Optimization in the face of uncertainty
date:       2018-05-21
categories: online, expository
---

The rise of machine learning in recent decades
has generated a renewed interest in online decision-making,
where algorithms are
equipped only with partial information about the world,
and must take actions in the face of uncertainty about the future.
There are various ways to analyze how much the presence 
of uncertainty 
degrades optimization.  Two of the most general models
are "probability free" (aka "worst-case," or "adversarial"),
in the sense that one can measure the performance of algorithms
without making distributional assumptions on the input.

## Competitive analysis

One such model goes by the name of [competitive analysis][competitive],
and has been studied in theoretical CS since the 1970s.
Imagine, for instance, that one maintains a binary search tree (BST)
with key-value pairs at the nodes.
At every point in time, a key is requested, and
the corresponding value is looked up via binary search.
Along the search path, the algorithm is allowed to modify the
tree using standard [tree rotation operations][tree-rotate].

The cost of such an algorithm is the average number
of binary search steps per key-lookup over a long sequence
of requests.
To minimize the cost, it is beneficial for the algorithm
to dynamically rebalance the tree so that frequently-requested
keys are near the root.  Sleator and Tarjan had this
model in mind when they invented the [Splay Tree][splay-tree]
data structure.
Their (still unproven) *Dynamic Optimality Conjecture*
asserts that, for every sequence of key requests,
the number of operations used by the Splay Tree
is within a constant factor of the number of operations
used by *any binary search tree,*
even an *offline algorithm* that is allowed to see
the entire sequence of key requests in advance.
(This is a very strong requirement!  We make no assumption
on the structure of the request sequence, and have to compare
our performance to an algorithm that sees the entire
request sequence up front.)

In the language of competitive analysis, the conjecture 
states that the Splay Tree algorithm is "competitive."
In general, an *$\alpha$-competitive* online algorithm
is one whose total cost on every input sequence
is within an $\alpha$ factor of the cost incurred by the optimal *offline* algorithm
that sees the whole input sequence in advance.

## Multi-arm bandits

Another compelling model arising in online learning
is the *multi-armed bandit problem.*
Here, an agent has a set $\mathcal{A}$ of feasible actions.
At time $t=1,2,3,\ldots$, the agent plays an action $a_t \in \mathcal{A}$,
and only then the cost of that action is revealed.
Imagine, for instance, 
choosing an advertisement $a_t \in \mathcal{A}$ to present to a user,
and then learning afterward the probability it
led to a sale.
The goal of an algorithm in this model is to achieve
a total cost (often called the *loss*) that
is not too much worse than the best *fixed* action
in hindsight.  The gap between the two is called the *regret.*

At first blush, it may seem that these two models (multi-arm bandits and competitive analysis)
are quite different.  But their relationship rests on a common theme
in machine learning:  [The intimate connection between stability and generalization][stable-general].
A competitive binary search tree algorithm aspires to be *stable*
in the sense that the search tree changes little between lookups
because the requested key is often near the root.
A low-regret advertiser aspires for her decisions to *generalize*
in the sense that her past observations about users
are predictive of their future actions.
(One can consult [a more in depth look at this connection][MTS-blog] in the context
of *Metrical Task Systems*.)

## Hedging and entropic regularization

A fundamental feature of algorithms
designed in both models is *hedging,* i.e., making 
decisions now that protect against the cost of uncertainty in future inputs.
In the bandit model, where one only learns the cost associated to the
action played, hedging involves exploring the action space
(the cost protected against here is opportunity cost).
In competitive analysis, one can think of hedging as maintaining a state
that avoids exploitation by an adversary.  For instance, if there are 10 keys
that are very frequently requested in a BST, hedging might involve a preference
for a configuration in which all 10 keys are within distance 100 of the root,
rather than a configuration in which 9 keys are within distance 3 and the 10th key
is at distance 1000.  This might be preferable even if those 9 keys are requested
twice as often as the 10th.

In these settings, hedging is a tradeoff between cost (or utility)
and entropy.
In modern play of no-limit Texas hold 'em, this tradeoff is now
explicit in the vernacular.  Poker players talk of "balancing
their range."  For instance, it generally makes sense to bet with strong hands,
and even to bet more as a hand gets stronger.  But a player has to
weigh this against their loss in entropy (from the perspective of an observer
who does not know their hole cards):
If I only go all-in before the flop
with aces, my opponent will be able to play optimally against me whenever
that occurs.

The idea of adding an entropic regularizer to the cost function
has played a central (and rather explicit) role in online learning.
The possible application of these ideas to competitive analysis
was already suggested in work of [Blum and Burch (2000)][BB20] and
more recently in a paper conceived at Berkeley by [Abernethy,
Barlett, Buchbinder, and Stanton (2010)][ABBS10].
Those early attempts, while prescient,
were not able to yield better general
approaches for the classical problems in online algorithms.

But a collaboration seeded at the Simons Institute,
and spanning from the [Algorithmic Spectral Graph Theory][ASGT] program (Fall 2014)
to the [Continuous and Discrete Optimization][CDO] program three years later was key
in developing a theory of entropic regularization suited to competitive analysis,
and leading to the resolution of some long-standing open problems in the field.

[competitive]: https://en.wikipedia.org/wiki/Competitive_analysis_(online_algorithm)
[tree-rotate]: https://en.wikipedia.org/wiki/Tree_rotation
[splay-tree]: https://en.wikipedia.org/wiki/Splay_tree
[stable-general]: https://www.offconvex.org/2016/03/14/stability/
[BB20]:  https://link.springer.com/article/10.1023/A:1007621832648
[ABBS10]: https://link.springer.com/chapter/10.1007/978-3-642-16108-7_23
[ASGT]: https://simons.berkeley.edu/programs/spectral2014
[CDO]: https://simons.berkeley.edu/programs/optimization2017
[MTS-blog]: http://blog.tcsmath.org/online/2018/04/01/competitive-analysis/
