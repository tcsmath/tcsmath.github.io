---
layout:     post
title:      Metrical task systems on a weighted star
date:       2018-04-09
summary:    Using the mirror descent framework for MTS
categories: online
---

Let's recall the definition of MTS.
$$\def\K{\mathsf{K}}
\def\R{\mathbb{R}}
\def\seteq{\mathrel{\vcenter{:}}=}
\def\cE{\mathcal{E}}
\def\argmin{\mathrm{argmin}}
\def\llangle{\left\langle}
\def\rrangle{\right\rangle}
\def\1{\mathbf{1}}
\def\e{\varepsilon}
\def\Lip{\mathrm{Lip}}$$
There is a metric space $(X,d)$.
At each time, we receive a cost function $c_t : X \to \R_+$,
and need to respond with a point $x_t \in X$.
The cost we pay at time $t$ is the sum of the *service cost*
and the *movement cost:*

<p>
\[
   c_t(x_t) + d(x_{t-1},x_t).
\]
</p>
Our goal is to be competitive against the best *offline* algorithm:
It should hold that for every $T \geq 1$,

<p>
   \[
   \sum_{t=1}^T c_t(x_t) + d(x_{t-1},x_t) \leq \alpha \left(\sum_{t=1}^T c_t(x^*_t) + d(x^*_{t-1},x^*_t)\right) + C
\]
</p>

where $C > 0$ is some constant independent of the cost sequence, and $\llangle x^\*_t : t=0,1,\ldots,T\rrangle$
is some optimal offline sequence for $\llangle c_t : t=1,2,\ldots,T\rrangle$.
Such an online algorithm is said to be *$\alpha$-competitive.*

It is a long-standing conjecture that there is an $O(\log n)$-competitive randomized algorithm
for MTS on every $n$-point metric space.
Actually, it is conjectured that the competitive ratio is $\Theta(\log n)$ for every $n$-point metric space.
We will see the known $\Omega\left(\frac{\log n}{\log \log n}\right)$ lower bound of
[Bartal, Bollobas, and Mendel](https://arxiv.org/abs/cs/0406028) in a few lectures.

Let us remark that a lower bound of $\Omega(\log n)$ for the $n$-point uniform metric is straightforward.
At every point in time, the adversary chooses a uniformly random $z_t \in X$ and defines
the cost function by $c_t(z_t)=+\infty$ and $c_t(z)=0$ for $z \neq z_t$.
Clearly any online algorithm incurs movement cost $\asymp t/n$ in expectation after $t$ steps.
On the other hand, an offline algorithm can break the request sequence into phases
$0 = t_0 < t_1 < t_2 < \cdots$ such that the times $\\{t_i\\}$
are minimal subject to the constraint $\\{1,2,\ldots,n\\} = \\{z_{t_i+1}, \ldots, z_{t_{i+1}}\\}$.
Clearly the offline algorithm only has to move once per phase, and by a standard coupon collector
argument, the expected length of each phase is $\asymp n \log n$.  Thus the offline algorithm
only incurs movement cost $\asymp t/(n \log n)$.

In this lecture, we'll establish
the conjectured upper bound for the special case
when $(X,d)$ is the path metric on an $n$-point weighted star:  $X=\{1,2,\ldots,n\}$
and $d(i,j)=w_i+w_j$ for some collection $w_1,w_2,\ldots,w_n > 0$
of positive weights.
This will be a building block of our eventual algorithm
for trees, which will then be used to obtain
an $O((\log n)^2)$-competitive algorithm for any metric space.

## The transportation distance

As in the first lecture, instead of a randomized strategy,
we will play a fractional strategy:  At every time $t$, a probability
distribution $p_t : X \to [0,1]$.
In this case, our service cost is $\sum_{x \in X} p_t(x) c_t(x)$, and our movement cost is
the *transportation distance* $W_1(p_{t-1},p_t)$.  Also known as the Earthmover distance,
$W_1(p,q)$ this is the cost of the minimal transport plan between probability distributions
$p$ and $q$.

A primary reason for looking first at weighted star metrics is that their transportation
distance can be described by a weighted $\ell_1$ norm:
$W_1(p,q) = \\|p-q\\|_{\ell_1(w)},$ where
<p>
\[
   \|v\|_{\ell_1(w)} = \sum_{x \in X} w_x |v(x)|.
\]
</p>

## The online algorithm

As in the first lecture, we will design our algorithm in continuous time
(and this is without loss of generality).
Given some continuous trajectory of cost functions $c_t : X \to \R_+$ with $t \geq 0$,
our algorithm will be a trajectory $p_t$ of distributions, and our instantenous
cost is described by
<p>
\[
   \|\partial_t p_t\|_{\ell_1(w)} + \langle c_t,p_t\rangle,
\]
</p>
where $\langle f,g\rangle = \sum_{x \in X} f(x) g(x)$.

We will design the algorithm in the mirror descent framework of the previous lecture.
The underlying convex body will be the probability simplex on $X$:
<p>
\[
   \K \seteq \left\{ p \in [0,1]^X : \sum_{x \in X} p(x)=1\right\}.
\]
</p>

The second object we need is the *mirror map* $\Phi : \K \to \R$.
Our control will be $F(t,\cdot)=- c_t$.
Recall from the preceding lecture that if we do continuous-time mirror descent on $\K$ using $\Phi$,
it will hold
that the corresponding Bregman divergence $D_{\Phi}$ acts as a Lyapunov functional:
For every fixed distribution $q \in \K$:
<p>
\begin{equation}\label{eq:lya}
   \partial_t D_{\Phi}(q; p_t) \leq \langle c_t, q-p_t\rangle.
\end{equation}
</p>
In other words, if our algorithm is paying more cost than $q$, then we are getting "closer" to $q$
in the Bregman distance.

This allows us to control our service cost against a *fixed* target $q \in \K$.
We need to choose $\Phi$ with two additional things in mind:  We also want the movement cost
to be controlled, and we want to compare ourselves to a possibly moving target $q_t^\* = \1_{x_t^\*}$.

## Controlling the movement cost by the service cost

In order to control the movement cost, we will simply try to make it comparable
to the current instananeous service cost.
Let us recall the trajectory of mirror descent from the preceding lecture:
<p>
\begin{equation}\label{eq:evo}
   \partial_t p_t = (\nabla^2 \Phi(p_t))^{-1} \left(- c_t - \lambda_t\right),
\end{equation}
</p>
where $\lambda_t \in N_{\K}(p_t)$.  Recall that $\lambda_t$ represents the set of normal forces
that are constraining us to lie in $\K$.

Let's ignore $\lambda_t$ for the moment, and calculate the instaneous movement cost induced by the cost function alone:

<p>
\begin{equation}\label{eq:compare}
   \|\partial_t p_t\|_{\ell_1(w)} = \sum_{x \in X} w_x \left((\nabla^2 \Phi(p_t))^{-1} c_t\right)(x).
\end{equation}
</p>

Thus if we want $\\|\partial_t p_t\\|_{\ell_1(w)} \asymp \langle c_t,p_t\rangle$, it make sense to choose $\Phi$
to be a weighted entropy:
<p>
\[
   \Phi_w(p) \seteq \sum_{x \in X} w_x p(x) \log p(x).
\]
</p>
In this case, the Hessian $\nabla^2 \Phi_w(p)$ is a diagonal matrix with:
<p>
\[
   \left(\nabla^2 \Phi_w(p)\right)_{x,x} = \frac{w_x}{p(x)},
\]
</p>
and \eqref{eq:compare} becomes
<p>
\[
   \|\partial_t p_t\|_{\ell_1(w)} = \sum_{x \in X} p_t(x) c_t(x),
\]
</p>
as desired.

## Tracking a moving target

The second thing we need to address is that \eqref{eq:lya} compares our service cost
against that of a fixed distribution $q$.  In order to analyze how we track a moving target,
let's take a step back and compute $\partial_t D_{\Phi}(z_t; y)$ for a general 
strictly convex function $\Phi$.  Recall that
<p>
\[
   D_{\Phi}(z;y) = \Phi(z) - \Phi(y) - \langle \nabla \Phi(y), z-y\rangle,
\]
</p>
and therefore
<p>
\begin{align}
   \partial_t D_{\Phi}(z_t; y) &= \langle \nabla \Phi(z_t) - \nabla \Phi(y), \partial_t z_t \rangle \nonumber \\
                               &\leq \left(\|\nabla \Phi(y)\|_* + \|\nabla \Phi(z_t)\|_*\right) \|\partial_t z_t\| \nonumber \\
                               &\leq 2 \Lip_{\K, \|\cdot\|_*} (\Phi) \cdot \|\partial_t z_t\|.\label{eq:move}
   \end{align}
</p>
The first inequality holds for any norm $\\|\cdot\\|$, we use $\\|\cdot\\|_\*$ for the dual norm, and
we write
<p>
\[
   \Lip_{\K,\|\cdot\|_*}(f) = \sup_{z \in \K} \|\nabla f(z)\|_*.
\]
</p>

Returning from the abstract to our current setting, it makes sense to choose $\\|\cdot\\| = \\|\cdot\\|_{\ell_1(w)}$,
and then \eqref{eq:move} exactly says that when a point moves away
from us in the Bregman divergence, it must pay for this with its own movement cost!
Using the chain rule, we now have
<p>
\begin{equation}\label{eq:breg2}
   \partial_t D_{\Phi}(q_t; p_t) \leq \langle c_t, q_t-p_t\rangle +
2 \Lip_{\K, \|\cdot\|_{*}} (\Phi) \cdot \|\partial_t q_t\|_{\ell_1(w)}
\end{equation}
</p>

This looks great, except that we need to calculate the Lipshitz constant of $\Phi$.
If we try
this for the weighted entropy $\Phi_w$, we immediately run into a problem:
Since $(\nabla \Phi_w(p))(x) = w_x (1+\log p(x))$, the $\ell_{\infty}$ norm blows up as $p(x) \to 0$.
This is a manifestation of the fact, demonstrated in the first lecture,
that exponential weights is too conservative to be competitive against a moving target.

## The exploration shift, revisited

To fix this problem, we will consider the shifted entropy:
<p>
\[
   \Phi \seteq \Phi_{w,\delta}(p) \seteq \sum_{x \in X} w_x (p(x) + \delta) \log (p(x)+\delta).
\]
</p>

Observe that now:
<p>
\[
   \Lip_{\K,\|\cdot\|_*} (\nabla \Phi) \leq \log (1/\delta).
\]
</p>
Plugging this into \eqref{eq:move} gives
<p>
\begin{equation}\label{eq:move2}
   \partial_t D_{\Phi}(q_t; p_t) \leq \langle c_t, q_t-p_t\rangle + 2 \log(1/\delta) \|\partial_t q_t\|_{\ell_1(w)}.
\end{equation}
</p>
Note that rearranging yields
<p>
\begin{equation}\label{eq:anal}
   \langle c_t, p_t \rangle \leq \langle c_t,q_t\rangle + 2  \log(1/\delta) \|\partial_t q_t\|_{\ell_1(w)} - \partial_t
   D_{\Phi}(q_t;p_t).
\end{equation}
</p>
If $q_0=p_0$, then $D_{\Phi}(p_0;q_0) = 0$ and $D_{\Phi} \geq 0$ always, so integrating would seem
to give us an $O(\log (1/\delta))$-competitive algorithm.

But this is only true if $\\|\partial_t p_t\\|_{\ell_1(w)} \asymp \langle c_t, p_t\rangle$,
and our previous calculations toward this end do not necessarily hold
once we incorporate the shift by $\delta$.
This will be the fundamental tension in the course:
Making $\delta$ larger encourages "exploration" that is necessary
to respond quickly enough to changes in the cost function.
But exploration comes at the cost of movement.

In the setting where $\K$ is the simplex, it is possible to control things by hand,
but for more complicated convex bodies, the normal forces described by $\lambda_t$
in \eqref{eq:evo} will be substantially more complicated.
In the next lecture, we will use this approach to 
derive an $O(\log k)$-competitive algorithm for the weighted $k$-paging problem,
and we will implement a different strategy for the exploration shift.

## Analyzing the movement of $p_t$

So now let us describe the algorithm $p_t$ using our shifted entropy map and \eqref{eq:evo}:
<p>
\begin{equation}\label{eq:evo2}
   \partial_t p_t(x) = \frac{p_t(x)+\delta}{w_x} \left(-c_t(x) - \lambda_t(x)\right).
\end{equation}
</p>

Toward this end, let us write 
<p>
\[
   \lambda_t = \xi_t + \mu_t,
\]
</p>
where $\xi_t : X \to \R_+$ are the multipliers corresponding to the positivity constraints $p(x) \geq 0$
and $\mu_t : X \to \R$ is the multiplier corresponding to the constraint $\sum_{x \in X} p(x) = 1$.
Note that this decomposition is not necessarily unique, but what we want is that
the complementary slackness conditions hold:  $\xi_t(x) > 0 \implies p_t(x)=0$.
(See the discussion of the normal cone for a polytope from the preceding lecture.)


As in the first lecture, it will suffice to bound only one direction of the movement.
In this case, we will consider the negative coordinates in $\partial_t p_t$.
It is a straightforward calculation to check that $\mu_t \leq 0$ by summing over $x$ in \eqref{eq:evo2}
(we are reducing the probability mass in response to a cost function, so $\mu_t$ is keeping
the total probability mass from dropping).  Therefore \eqref{eq:evo2} gives
<p>
\[
   \left\|\left(\partial_t p_t\right)_-\right\|_{\ell_1(w)} \leq \llangle p_t+\delta \1, c_t + \xi_t\rrangle.
\]
</p>
Note first that $\langle p_t, c_t+\xi_t\rangle = \langle p_t, c_t\rangle$
by complementary slackness.

Finally, consider any fixed $r_0 \in \K$ and
use $\langle \mu_t, r_0- p_t\rangle=0$ to write
<p>
\[
   \langle c_t + \xi_t, r_0 - p_t\rangle = \langle c_t + \lambda_t, r_0 - p_t\rangle
   = \llangle \nabla^2 \Phi(p_t) \partial_t p_t, p_t-r_0 \rrangle = \partial_t D_{\Phi}(r_0; p_t).
\]
</p>

Putting this all together and using $r_0 = \frac{1}{n} \1$ yields
<p>
\[
   \left\|\left(\partial_t p_t\right)_-\right\|_{\ell_1(w)}
   \leq \left((1+\delta n) \langle c_t,p_t\rangle + \delta n \partial_t D_{\Phi}(\tfrac{1}{n} \1; p_t)\right).
\]
</p>
Thus if we set $\delta = 1/n$, our movement cost becomes proportional to our service cost, and \eqref{eq:anal}
shows that our algorithm is $O(\log n)$-competitive.

