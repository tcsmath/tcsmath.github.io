---
layout:     post
title:      Optimization against adversarial uncertainty
date:       2018-05-21
summary:    Mirror descent in competitive analysis
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
explicit in the vernacular: Professional players talk of "balancing
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
in developing a theory of entropic regularization strong enough
to attack some of the long-standing open problems in the field.

## The randomized $k$-server conjecture

The $k$-server problem has been referred to as the "holy grail" of online algorithms,
largely because of the central role it has played in the development of the field.
Fix an integer $k \geq 1$ and let $(X,d)$ denote a metric space.
The input is a sequence $\left\langle \rho_1,\rho_2, \ldots \right\rangle$
of requests $\rho_t \in X$ that arrive online.
The algorithm maintain a configuration of $k$ *servers*
at points of $X$, and at time $t=1,2,\ldots$, must move one of the servers to $\rho_t$
to service the request.
The cost incurred is the total server movement of the algorithm (in the metric $d$).

[Koutsoupias and Papadimitriou][KP] famously established that the deterministic *Work Function Algorithm* is $2k-1$ competitive.
It has long been conjectured that *randomized* online algorithms should be capable of achieving a $(\log k)^{O(1)}$ competitive ratio
(a strong version of the conjecture asserts that the competitive ratio is $\Theta(\log k)$ for *every* metric space on more
than $k$ points).
Over the course of a decade, primal-dual algorithms were the weapon of choice, culminating
in a result of [Bansal, Buchbinder, Mądry, and Naor][BBMN] that established
a $\mathrm{poly}(\log n)$-competitive algorithm for the case when the underlying metric space has $n$ points.

## From Berkeley, to Seattle, to Cambridge, and back

During the reunion workshop for the [ASGT program][ASGT], I spoke about joint work that
Prasad Raghavendra, David Steurer, and I had completed a year earlier
establishing lower bounds on the size of semidefinite programming relaxations.
A major theme in that work is the use of quantum entropy maximization.
After my talk extoling the virtues of entropy maximizers, Olek Mądry (MIT)
suggested that recent work on [weighted paging][BBN] (a special case of the $k$-server
problem) seemed to match the narrative.

I returned to UW and taught a course on [entropy optimality][eo-course];
Seb Bubeck (Microsoft Research) sat in on the lectures,
and we began discussing the theory of mirror descent and
its recent applications in online learning.
One thing that became clear early on is that
the classical exponential weights approach
is *too conservative* to be competitive 
for $k$-server and related problems.
While exponential weights is very effective in the bandit
setting, there one generally competes against the
optimal *fixed* strategy.

A solution to this problem
(for the special case of weighted paging) lies
in the paper of [Bansal, Buchbinder, and Naor][BBN], where
the authors consider an algorithm that can be interpreted
in the following way:  Run exponential weights,
but never let the algorithm become too confident
about its server placement.  If the algorithm
asserts "I am 99.9% sure there should be a server here,"
we cap this confidence at 95% (more formally, at $1-1/2k$).
One can [consult these lecture notes][ca-course]
where this is referred to as the "exploration shift."

Since the work of [Bartal][Bartal-hst] (1996), it has been understood
that solving $k$-server on *hierarchically separated tree (HST) metrics*
is a fundamental first step in designing an algorithm
for general metric spaces.
Problematically, even with the above understanding for weighted paging,
the HST case is far more daunting
because one cannot write down the dynamics of the algorithm explicitly.
This is where a [general theory of mirror descent][mirror] becomes crucial,
though the correct notion of *multiscale entropy* (suitable for
hedging simultaneously at many scales) requires a detailed understanding
of the associated polytope.

Fortunately, Olek recruited an ambitious young graduate student named
Michael Cohen, and they understood well the structure of the 
*allocation polytope* underlying previous work on HSTs.
At the same time, Yin Tat Lee had joined us in Seattle (as
a postdoc at MSR, and then as faculty at UW), and we continued to study the dark side
of the exploration shift:  When the confidence of the
algorithm is artificially reduced, it becomes more willing
to move servers, and one has to control the corresponding increase
in movement cost.
(The resulting analytic mess is enough to make 
"inverse Hessian" start to sound like foul language.)

## With a little help from 0.1 friends

A rather ingenious observation of Michael is that the cost of the 
exploration shift can be controlled almost effortlessly
if we just have a little extra help:  Instead of $k$ servers,
$k+0.1$ servers.  (This requires passing to a fractional
relaxation of the $k$-server problem, which we had
already done implicitly five paragraphs and 10+ years ago.)
Moreover, on HSTs one can show that $k+0.1$ fractional servers
can always be simulated by $k$ fractional servers while
increasing the movement costs by only a constant factor.

Seb, Michael, Yin Tat, Olek, and I were all long-term partipants in
the [Optimization program][CDO] (Olek was an organizer) this past fall.
Our work culminated in an $O((\log k)^2)$-competitive randomized
algorithm for the $k$-server problem on HSTs: [$k$-server via multiscale entropic regularization][BCLLM].
In followup work, I show how this can be utilized
to obtain a [$\mathrm{poly}(\log k)$-competitive algorithm
for any metric space][fusible].

Tragically, Michael passed away unexpectedly during the program.
The [memorial symposium held in his honor][michael] offers
a glimpse of the brilliance and impact of his short time with us.

## Additional references

- The book [Competitive Analysis][ca-book] by Borodin and El-Yaniv.
- [Algorithms and Uncertainty program][AUprog] (Fall 2016) at the Simons Institute.
- The course [Competitive analysis via convex optimization][ca-course] (Spring 2018), taught 
at UW, jointly with Sebastien Bubeck.

[competitive]: https://en.wikipedia.org/wiki/Competitive_analysis_(online_algorithm)
[tree-rotate]: https://en.wikipedia.org/wiki/Tree_rotation
[splay-tree]: https://en.wikipedia.org/wiki/Splay_tree
[stable-general]: https://www.offconvex.org/2016/03/14/stability/
[BB20]:  https://link.springer.com/article/10.1023/A:1007621832648
[ABBS10]: https://link.springer.com/chapter/10.1007/978-3-642-16108-7_23
[ASGT]: https://simons.berkeley.edu/programs/spectral2014
[CDO]: https://simons.berkeley.edu/programs/optimization2017
[MTS-blog]: http://blog.tcsmath.org/online/2018/04/01/competitive-analysis/
[ca-book]: https://www.amazon.com/Online-Computation-Competitive-Analysis-Borodin/dp/0521619467
[AUprog]: https://simons.berkeley.edu/programs/uncertainty2016
[ca-course]: https://homes.cs.washington.edu/~jrl/teaching/cse599I-spring-2018/
[KP]: https://dl.acm.org/citation.cfm?id=210128
[BBMN]: https://dl.acm.org/citation.cfm?id=2783434
[eo-course]: https://homes.cs.washington.edu/~jrl/teaching/cse599swi16/
[BBN]: https://dl.acm.org/citation.cfm?id=2339126
[shift-lec]: http://blog.tcsmath.org/online/2018/04/09/mts-on-star/
[Bartal-hst]: https://ieeexplore.ieee.org/document/548477/
[mirror]: http://blog.tcsmath.org/online/2018/04/06/navigating/
[BCLLM]: https://arxiv.org/abs/1711.01085
[fusible]: https://homes.cs.washington.edu/~jrl/papers/pdf/fusion.pdf
[michael]: https://simons.berkeley.edu/workshops/schedule/8815
