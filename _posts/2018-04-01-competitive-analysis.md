---
layout:     post
title:      Regret minimization and competitive analysis
date:       2018-04-01
summary:    Regret minimization vs. competitive analysis
categories: online
---

These are notes for the first lecture of a course I am co-teaching with [Seb Bubeck][Seb] on
[Competitive analysis via convex optimization][course].

I want to set the groundwork by reviewing the bandits model in online learning
and the standard exponential weights algorithm, and then trying to extend it
to the setting of competitive analysis where the analogous
problem goes by the name of *metrical task systems*.
Seeing where things go wrong will give us a plan to follow for much of the course.
Some of the objects and algorithms in this lecture may appear
unmotivated; that will be addressed soon.

## Regret minimization

Here we review quickly the basic *multi-arm bandits model* in online learning.
For more background see, e.g., this [survey of Bubeck and Cesa-Binachi][bandits].
$$\def\seteq{\mathrel{\vcenter{:}}=}
\def\cE{\mathcal{E}}
\def\R{\mathbb{R}}
\def\argmin{\mathrm{argmin}}
\def\llangle{\left\langle}
\def\rrangle{\right\rangle}
\def\1{\mathbf{1}}
\def\e{\varepsilon}$$

In the standard bandits model, we have a set of
experts $\cE = \\{1,2,\ldots,N\\}$, and
loss functions
$\ell_1,\ell_2,\ldots$ arriving over time,
where $\ell_t : \cE \to [0,1]$.

For the sake of simplicity, we will work in the full
information model.  At time $t \geq 1$, we have seen $\ell_1,\ldots,\ell_{t-1}$.
We choose some strategy $x_t \in \cE$ and incur cost $\ell_t(x_t)$.
Our goal is to minimize the total cost incurred:
$\sum_{t=1}^T \ell_t(x_t)$.
In the setting of adversarial bandits, we will allow ourselves
to employ a randomized strategy, playing instead a distribution $p_t : \cE \to [0,1]$ at time $t$.

In the regret minimization framework, we compare our expected loss to
that of the optimal fixed strategy:  The *regret incurred up to time $T$* is
<p>
$$R_T \seteq \sum_{t=1}^T \langle p_t, \ell_t\rangle - \min_{x \in \cE} \sum_{t=1}^T \ell_t(x)\,,$$
</p>
where for $f,g : \cE \to \R$, we write $\langle f,g\rangle = \sum_{y \in \cE} f(y) g(y)$.

We will bound the regret in two steps.
Denote $x_T^* \seteq \argmin_{x \in \cE} \sum_{t=1}^T \ell_t(x)$.  Then:
<p>
\begin{align}
   R_T &= \sum_{t=1}^T \langle p_t - p_{t+1},\ell_t\rangle + 
   \sum_{t=1}^T \langle p_{t+1}, \ell_t-\ell_t(x_T^*)\rangle \nonumber \\
   &\leq \sum_{t=1}^T \|p_t-p_{t+1}\|_1 + 
   \sum_{t=1}^T \langle p_{t+1}, \ell_t-\ell_t(x_T^*)\rangle,\label{eq:pseudo-regret}
\end{align}
</p>
where the inequality uses that the losses lie in $[0,1]$.


### Continuous-time dynamics

For a number of reasons, the analysis will be much cleaner in continuous time.
We can think about the losses as a trajectory $\left\\{ \ell_t : \cE \to [0,1] \mid t \geq 0 \right\\}$,
where the instantaneous loss incurred is $\ell_t\,dt$.
As long as we are bounding the expression \eqref{eq:pseudo-regret},
our continuous-time model will be *more general*
than the discrete-time model.  The latter can be recovered by
considering a trajectory $\\{ \ell_t : t \geq 0 \\}$
that is piecewise-constant.
If we were bounding the regret itself, the continuous-time model would have a time advantage,
but once we shift time by one as in \eqref{eq:pseudo-regret},
this advantage disappears.

Now we can analogously bound the regret:
<p>
\begin{equation}\label{eq:cont-regret}
   R_T \leq \int_0^T \|\partial_t p_t\|_1 \,dt + \int_0^T \langle p_t, \ell_t-\ell_t(x_T^*)\rangle\,dt\,,
\end{equation}
</p>
where $x_T^* \seteq \argmin_{x \in \cE} \int_0^T \ell_t(x)\,dt$.

We will start with $p_0(x) = 1/N$ for every $x \in \cE$, and
employ the following exponential-weights strategy for updating $p_t$:
\begin{equation}\label{eq:dynamics}
\partial_t \log p_t(x) = \eta\left( - \ell_t(x) + \langle p_t, \ell_t\rangle\right),
\end{equation}
where $\eta > 0$ is a parameter called the *learning rate* that we will choose soon.
This algorithm will be motivated more in the next lecture, but for now one can note that
we are simply doing continuous-time gradient descent on the vector $\log p_t(x)$:  We are moving
in the direction $- \eta \ell_t dt$.  The additional additive term in \eqref{eq:dynamics}
is there to maintain the constraint that $p_t$ is a probability distribution.

One can see this clearly by rewriting \eqref{eq:dynamics} as:
\begin{equation}\label{eq:exp-form}
   \partial_t p_t(x) = p_t(x) \, \eta \left(- \ell_t(x) + \langle p_t,\ell_t\rangle\right),
\end{equation}
so that $\sum_{x \in \cE} \partial_t p_t(x) = 0$.


### The Lyapunov functional, aka the potential

In order to bound the regret $R_T$, we will employ the philosophy underlying
the entire course:  If we are incurring more cost than $x_T^\*$, we would like to be *learning*
about $x_T^\*$ in a suitable sense.

Define:
\[
   D(x; p) \seteq - \log p(x)\,.
\]
Note that for any $x \in \cE$, we have $D(x; p_0) = \log N$, and $D(x; p_t) \geq 0$ for all $t \geq 0$.

For any $x \in \cE$:
\begin{equation}\label{eq:lya}
   \partial_t D(x;p_t) = - \partial_t \log p_t(x) = \eta \left(\ell_t(x) - \langle p_t,\ell_t\rangle \right).
\end{equation}
If we think of $D(x;p_t)$ as the "distance" from $p_t$ to $x$, then our distance to $x$
is decreasing proportional to the advantage $x$ has over our strategy $p_t$.
Integrating \eqref{eq:lya} over $[0,T]$ gives
\[
   D(x; p_0) - D(x; p_T) = \eta \int_0^T \langle p_t, \ell_t-\ell_t(x)\rangle\,dt
\]

Applying this with $x=x_T^\*$ and recalling \eqref{eq:cont-regret}, we have
<p>
\begin{align*}
   R_T  &\leq \int_0^T \|\partial_t p_t\|_1\,dt + \frac{D(x_0^*;p_0)-D(x_T^*;p_T)}{\eta} \\
        &\leq \int_0^T \|\partial_t p_t\|_1\,dt + \frac{\log N}{\eta} \\
        &\leq \eta T + \frac{\log N}{\eta}\,,
\end{align*}
</p>
where the last inequality uses \eqref{eq:exp-form} and the fact that the losses are in $[0,1]$
to write $\\|\partial_t p_t\\|_1 \leq \eta \\|p_t\\|_1 = \eta$.

Setting $\eta = \sqrt{\frac{\log N}{T}}$ yields the standard regret bound
\[
   R_T \leq 2 \sqrt{T \log N}\,.
\]
If one does not know the final time $T$, it is not difficult to see that one can choose
a time-dependent learning rate $\eta=\eta(t)=\sqrt{\frac{\log N}{t}}$ to obtain a similar result.
result

## Competitive analysis

The competitive analysis analog of the bandits framework goes by the name of
*metrical task systems (MTS)*.  This problem was introduced in 1992 by
[Borodin, Linial, and Saks][BLS].

This setting has three major differences:
- At each time $t \geq 1$, we receive a *cost function* $c_t : \cE \to [0,\infty)$, and we choose
an action $x_t \in \cE$ *after* receiving $c_t$.
- There is a metric $d$ on $\cE$ that makes $(\cE,d)$ into a metric space,
and in addition to the *service cost* $c_t(x_t)$, we pay a *switching cost* $d(x_{t-1},x_t)$
for playing $x_t$.
- We compare ourselves against an offline optimum that has the *same ability to switch strategies*.

Say that an online algorithm $\llangle x_1, x_2, \ldots,x_T\rrangle$ is $\alpha$-competitive
if, for every $x_0 \in \cE$ and every cost sequence $c_1,c_2,\ldots,c_T$, it holds that
<p>
$$
   \sum_{t=1}^T c_t(x_t) + d(x_{t-1},x_t) \leq \alpha\left(\sum_{t=1}^T c_t(x^*_t) + d(x_{t-1}^*, x_t^*)\right) + O(1)\,,
$$
</p>
where $\llangle x_0^\*, x_1^\*, x_2^\*, \ldots, x_T^\*\rrangle$ is the optimal *offline* strategy
with $x_0^\*=x_0$, i.e., the optimal strategy in hindsight.  The additive $O(1)$ term is a constant
that should be independent of the request sequence.

It is conjectured that the competitive ratio is $O(\log N)$ for every $N$-point metric space.
In the coming weeks, we will see an $O((\log N)^2)$-competitive algorithm
based on upcoming joint work with Bubeck, Cohen, and Y. T. Lee.
This improves slightly on the $O((\log N)^2 \log \log N)$ bound of [Fiat and Mendel][FM04].

### Attempting exponential weights

The simplest setting for MTS is when the metric $(\cE,d)$ is uniform, i.e., $d(x,y)=\1_{\\{x\neq y\\}}$ for $x,y \in \cE$.

Just as in the bandits setting, we can consider a continuous-time trajectory
$\left\\{ c_t : \cE \to [0,\infty) \mid t \geq 0\right\\}$ on cost
functions.  And we might try to employ a similar strategy:
\begin{equation}\label{eq:cost-dynamics}
   \partial_t \log p_t(x) = - c_t(x) + \langle p_t, c_t\rangle.
\end{equation}

But now we run into a major hurdle:  Such an algorithm cannot be $\alpha$-competitive for any $\alpha < \infty$.

<p>
Suppose we arrange that for some $x_0 \in \cE$ and $t_0 > 0$ and small $\epsilon > 0$,
it holds that $p_{t_0}(x_0) = 1-\epsilon$.
We can do this by having an adversary play the cost function $c(x)=\1_{\cE \setminus \{x_0\}}(x)$
for a long enough period of time
so that any competitive algorithm must put almost all the probability mass on $x_0$.
</p>

<p>
Now the adversary changes the cost function to $c(x)=\1_{x_0}(x)$.
The dynamics specified by \eqref{eq:cost-dynamics} will move much too slowly!
Indeed:
\[
   \partial_t \log p_t(x_0) = -1+(1-p_t(x_0)) = - p_t(x_0),
\]
i.e.,
\[
   \partial_t p_t(x_0) = - p_t(x_0)^2,
\]
thus it will take roughly $1/\epsilon$ time before $p_t(x_0) < 1/2$.
</p>

Thus our algorithm will incur cost $\asymp 1/\epsilon$ while the optimal offline algorithm incurs cost $O(1)$.
In the bandits setting, this was fine because every fixed strategy incurs cost $\asymp 1/\epsilon$.
But in the setting of competitive analysis, our algorithm needs to be a lot more nimble
to keep up with an offline algorithm that can switch strategies.


### The exploration shift

To fix this, we will design an algorithm that devotes a constant fraction of the service cost
it is currently incurring to exploring the strategy space.
Essentially, this can be achieved by pretending that $p_t(x) \geq 1/(2N)$ for every $x \in \cE$.
(Recall that $N = |\cE|$.)
This transformation (mixing with the uniform distribution)
is not uncommon in the bandit literature.
In the setting of metrical task systems, I saw it for the first time
in this paper of [Bansal, Buchbinder, and Naor](/assets/papers/pot.pdf) on the weighted paging problem.

Define $p_0(x)=\1_{x_0}(x)$ where $x_0 \in X$ is the starting point.
Let $\delta > 0$ be a number we will choose soon,
and consider the dynamics:
\begin{equation}\label{eq:mts-dynamics}
   \partial_t \log (p_t(x)+\delta) = - \hat{c}_t(x) + \llangle \frac{p_t+\delta}{1+\delta N}, \hat{c}_t\rrangle\,,
\end{equation}
which can be written equivalently as
\begin{equation}\label{eq:mts-move}
   \partial_t p_t(x) = (p_t(x)+\delta) \left(- \hat{c}_t(x) + 
   \llangle \frac{p_t+\delta}{1+\delta N}, \hat{c}_t\rrangle\right).
\end{equation}
A natural choice is to take $\hat{c}_t(x)=c_t(x)$, but this presents a problem:
Unlike \eqref{eq:cost-dynamics}, these dynamics no longer enforce
that $p_t(x) \geq 0$.

#### Lagrangian multipliers

In this relatively simple setting,
we can consider reduced costs
$\hat{c}_t(x) \seteq c_t(x)-\lambda_t(x)$ satisfying:

- $\lambda_t(x) \geq 0$ for all $t \geq 0$,
- $p_t(x) = 0 \implies \partial_t p_t(x) \geq 0$,
- $\lambda_t(x) > 0 \implies p_t(x)=0$.

With these constraints in place,
the corresponding trajectory $\\{p_t : t \geq 0\\}$
will always be a probability measure,
and we can charge ourselves $\hat{c}_t(x)$ without
worrying about cheating, since $p_t(x) \hat{c}_t(x) = p_t(x) c_t(x)$
will always hold.
The existence of functions $\\{ \lambda_t : \cE \to [0,\infty) \mid t \geq 0\\}$
is a slightly subtle issue that will be addressed formally
in the coming lectures.  These are Lagrangian multipliers corresponding
to the constraints $p_t(x) \geq 0$ for $x \in \cE$.

As we will see in future lectures, the Lagrangian multipliers
will not adversely affect the potential analysis,
but they could cause our algorithm to incur movement cost.
In the present setting, things are going in the beneficial direction:
The multipliers correspond to *reduced* costs, and therefore
they actually slow down our movement.

#### The potential analysis

<p>
Define now the potential
\[
   D_{\delta}(x; p) \seteq - \log (p(x)+\delta).
\]
We are interested in $\partial_t D_{\delta}(x_t^*; p_t)$.
Let's first consider the derivative with respect to $x_t^*$.
For any $x,y \in \cE$:
\[
   \left|D_{\delta}(x; p) - D_{\delta}(y ;p)\right| \leq \log(1/\delta)\,.
\]
Thus for any $T \geq 0$:
\begin{equation}\label{eq:first-mts}
   D_{\delta}(x_{T}^*; p_T) - D_{\delta}(x_0^*, p_0)
   \leq \log(1/\delta) \sum_{t=1}^{\lfloor T\rfloor} d(x_t^*, x_{t-1}^*) + \int_0^T \partial_t D_{\delta}\left(x^*_{\lfloor t\rfloor}; p_t\right)\,dt\,.
\end{equation}
To analyze the latter term, use \eqref{eq:mts-dynamics}
to observe that for any $x \in \cE$,
\[
   \partial_t D_{\delta}(x;p_t) = \hat{c}_t(x) - \llangle \frac{p_t+\delta}{1+\delta N}, \hat{c}_t\rrangle,
\]
hence
\[
   \int_0^T \partial_t D_{\delta}\left(x_{\lfloor t\rfloor}^*; p_t\right)\,dt =
   \int_0^T \hat{c}_t(x_t^*)\,dt - \int_0^T \llangle \frac{p_t+\delta}{1+\delta N}, \hat{c}_t\rrangle\,dt\,.
\]
Plugging this into \eqref{eq:first-mts} and rearranging gives
\begin{align}\nonumber
   (1+& \delta N)^{-1} \int_0^T \langle p_t + \delta, \hat{c}_t\rangle\,dt \\
&\leq 
   \left[ D_{\delta}(x_{0}^*; p_0) - D_{\delta}(x_T^*, p_T) \right]
    + \log(1/\delta) \sum_{t=1}^{\lfloor T\rfloor} d(x_t^*, x_{t-1}^*) + 
   \int_0^T \hat{c}_t(x_t^*)\,dt  \nonumber \\
   &\leq
    \log(1/\delta) \sum_{t=1}^{\lfloor T\rfloor} d(x_t^*, x_{t-1}^*) + 
    \int_0^T c_t(x_t^*)\,dt\,,\label{eq:second-mts}
\end{align}
where we have used the fact that the term in brackets is nonpositive,
and $c_t \geq \hat{c}_t$ pointwise.
This looks great:  We have
bounded the service cost of our algorithm by the movement and service
costs of the optimal algorithm.
We are left to consider the movement cost of the algorithm.
</p>

### The movement cost

<p>
Here we use a trick from online algorithms:
Instead of bounding the total movement cost
$\int_0^T \|\partial_t p_t\|_1\,dt,$
we will bound only the <em>incoming movement</em>
$\int_0^T \|\left(\partial_t p_t\right)_+\|_1\,dt$.
</p>

Since "what goes in must come out (unless it stays there forever)," we have:
<p>
$$
   \int_0^T \|\partial_t p_t\|_1\,dt \leq
   2 \int_0^T \|\left(\partial_t p_t\right)_+\|_1\,dt + 1\,.
$$
And now \eqref{eq:mts-move} gives
$$
   \left\|\left(\partial_t p_t\right)_+\right\|_1 \leq \langle p_t+\delta,\hat{c}_t\rangle\,.
$$
</p>

<p>
Combining this with \eqref{eq:second-mts} and using the fact that $\langle p_t, c_t\rangle = \langle p_t, \hat{c}_t\rangle$
yields
\begin{align*}
   \int_0^T \left(\langle p_t,c_t\rangle + \|\partial_t p_t\|_1\right)\,dt &\leq
   1 + 3 \int_0^T \langle p_t + \delta ,\hat{c}_t\rangle\,dt \\
   & \leq 1 + 3(1+\delta N) \left[\log(1/\delta) \sum_{t=1}^{\lfloor T\rfloor} d(x_t^*, x_{t-1}^*) + 
\int_0^T c_t(x_t^*)\,dt\right].
\end{align*}
Thus setting $\delta = 1/N$ yields an $O(\log N)$-competitive algorithm for MTS on a uniform metric space.
</p>

#### A comment about absolute continuity

Note that in \eqref{eq:first-mts}, we have used the fundamental theorem of calculus
to integrate a derivative.
In order for this to be valid, it must be that $\log p_t(x)$ is absolutely continuous
as a function of $t$.
When we argue formally about the existence of the Lagrangian multipliers $\lambda_t$,
we will need to ensure that the resulting trajectory is absolutely continuous.


[Seb]: https://sbubeck.com/
[course]: https://homes.cs.washington.edu/~jrl/teaching/cse599I-spring-2018/
[bandits]: http://sbubeck.com/SurveyBCB12.pdf
[BLS]: http://www.cs.huji.ac.il/~nati/PAPERS/bls_online.pdf
[FM04]: https://arxiv.org/abs/cs/0406034
