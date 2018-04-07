---
layout:     post
title:      Navigating a convex body online
date:       2018-04-06
summary:    Continuous-time mirror descent analysis
categories: online
---

In the last lecture, we saw some algorithms that, while simple and appealing,
were somewhat unmotivated.  We now try to derive them from general
principles, and in a setting that will allow us to attack other
problems in competitive analysis.
$$\def\K{\mathsf{K}}
\def\R{\mathbb{R}}
\def\seteq{\mathrel{\vcenter{:}}=}
\def\cE{\mathcal{E}}
\def\argmin{\mathrm{argmin}}
\def\llangle{\left\langle}
\def\rrangle{\right\rangle}
\def\1{\mathbf{1}}
\def\e{\varepsilon}$$


## Gradient descent:  The proximal view

Let us first recall the upper bound we derived for the regret in the last lecture:

<p>
\begin{equation}\label{eq:regret}
   R_T \leq \sum_{t=1}^T \left[ \|p_t-p_{t+1}\|_1 + \left\langle p_{t+1}, \ell_t - \ell_t(x_T^*) \right\rangle\right].
\end{equation}
</p>

Trying to minimize this expression leads to the question of how we should update our probability distribution $p_t \to p_{t+1}$
to simultaneously be stable (control the first term) and competitive (the second term).

A very natural algorithm in this setting is gradient descent.
Indeed, suppose that $\ell : \R^n \to \R$ is differentiable, and consider the optimization
<p>
\[
   \min \left\{  \frac12 \|x-x_0\|^2 + \eta \ell(x) : x \in \R^n \right\},
\]
</p>
where $\eta > 0$ is a small constant and $\\|\cdot\\|$ denotes the Euclidean norm.  Then first-order optimality
conditions dictate that the optimizer satisfies
\[
   x^* = x_0 - \eta \nabla \ell(x_0) + O(\eta^2)\,.
\]

Two questions immediately arise:  Why do we use the Euclidean norm when our reference problem \eqref{eq:regret}
refers to the $\ell_1$ norm, and if $x$ is meant to encode a probability distribution,
how do we maintain this constraint for $x^*$?

## Projected gradient descent

Let's address the feasibility problem first.  Suppose $\K \subseteq \R^n$ is a closed convex set
and $F : \R^n \to \R^n$ is a sufficiently smooth vector field (think of $F = \nabla \ell$).
How should we move in the direction of $F$ while simultaneously remaining inside $\K$?

The unconstrained flow along $F$ can be described as
a trajectory $x : [0,\infty) \to \R^n$ given by
\[
   x'(t) = F(x(t))\,.
\]
The most natural way to keep this flow inside $\K$ is to project back into the body whenever we leave.
Define the Euclidean projection
<p>
\[
   P_{\K}(y) \seteq \argmin \left\{ \|y-z\|^2 : z \in \K \right\},
\]
</p>
and the result of taking an infinitesimal step in direction $v$ and and then projecting:
\[
   \Pi_{\K}(x,v) \seteq \lim_{\e \to 0} \frac{P_{\K}(x+\e v) -x}{\e}\,.
\]
Then the projected dynamics looks like
\[
   x'(t) = \Pi_{\K} \left(x(t), F(x(t))\right)\,.
\]
(As we will see, this is well-defined under mild assumptions.)
This maintains feasibility,
but still leaves us with the question of what
role the Euclidean norm is playing.

## A Riemannian version

One can view $\Pi_{\K}(x, \cdot)$ as a function on the tangent space at $x$.
To specify such a projection,
we only need a local Euclidean structure.
An inner product $\langle \cdot,\cdot\rangle_x$ that varies smoothly
over $x \in \R^n$ is precisely a Riemannian metric.

Equivalently, we specify at every point $x \in \R^n$, a smoothly varying positive-definite matrix $M(x)$
so that
<p>
\begin{align*}
   \langle u,v\rangle_{M,x} &= \langle u, M(x) v\rangle \\
   \|u\|^2_{M,x} &= \langle u,u\rangle_{M,x}.
\end{align*}
</p>
The associated projection operator is then given by
<p>
\begin{align*}
   P_{\K}^M(y; x) &\seteq \argmin \left\{ \left\|y-z\right\|_{M,x}^2 : z \in \K \right\} \\
   \Pi_{\K}^M(x,v) &\seteq \lim_{\e \to 0} \frac{P_{\K}^M(x+\e v,x)-x}{\e}\,.
\end{align*}
</p>
This leads to the dynamical system:
<p>
\begin{align*}
   x'(t) &= \Pi^M_{\K}\left(x(t),F(x(t))\right) \\
   x(0) &= x_0 \in \K\,.
\end{align*}
</p>

## Lyapunov functions

The problem with stating things at this level of generality is that even when
$F = \nabla \ell$ is the gradient of a convex function $\ell : \R^n \to \R$,
we don't have a global way of controlling convergence of $F(x(t))$ to $\min \\{ F(x) : x \in \K \\}$.
In the Euclidean setting ($M(x) \equiv \mathrm{Id}$), there is a natural [Lyapunov function](https://en.wikipedia.org/wiki/Lyapunov_function):
If $\ell$ is convex and $\ell(x^\*) = \min \\{ \ell(x) : x \in \K \\}$,
then for every $x \in \K$:
<p>
\[
   \langle - \nabla \ell(x), x^* - x\rangle \geq 0\,.
\]
</p>
In other words,
gradient descent always makes progress toward $x^\*$.

If $x'(t) = \Pi_{\K}\left(x(t), \nabla \ell(x(t))\right)$, then
in the language of competitive analysis, the quantity $\frac12 \\|x(t)-x^\*\\|^2$
acts a potential function (a global measure of progress).

We will consider geometries that come equipped with such a
Lyapunov function.  In a sense that can be formalized in various ways,
these are the *Hessian structures on $\R^n$*, i.e., those
arising when $M(x) = \nabla^2 \Phi(x)$ for some strongly convex function $\Phi : \K \to \R$.

# Mirror descent dynamics

Consider now a compact, convex set $\K \subseteq \R^n$,
a strongly convex function $\Phi : \K \to \R$,
and a continuous time-varying vector field $F : [0,\infty) \times \K \to \R^n$.
We will refer to **continuous-time mirror descent**
as the dynamics specified by
<p>
\begin{align*}
   x'(t) &= \Pi_{\K}^{\nabla^2 \Phi}\left(\vphantom{\bigoplus} x(t), F(t, x(t))\right) \\
   x(0)  &= x_0 \in \K.
\end{align*}
</p>
We will sometimes refer to $\Phi$ as the *mirror map.*

As one might expect, we can decompose $x'(t)$ into two components:  One flowing in the direction $F(t,x(t))$,
and the other component arising from the normal forces that are keeping $x(t)$ inside $\K$.
We recall the **normal cone to $\K$ at $x$** is given by
<p>
\[
   N_{\K}(x) = \left\{ p \in \R^n : \langle p,y -x \rangle \leq 0 \textrm{ for all } y \in \K \right\}.
\]
</p>
This is the set of directions that point out of the body $\K$.
The next theorem is proved in 
the paper
<a href="https://homes.cs.washington.edu/~jrl/papers/pdf/kserver.pdf">k-server via multiscale entropic regularization</a>.

<p class="theorem" text="MD">
<a name="thm:md"></a>
   If $\nabla^2 \Phi(x)^{-1}$ is continuous on $\K$, then for any $x_0 \in \K$, there
   is an absolutely continuous trajectory $x : [0,\infty) \to \K$ satisfying
   \begin{align*}
      \nabla^2 \Phi(x(t)) x'(t) &\in F(t,x(t)) - N_{\K}(x(t)), \\
      x(0) &= x_0.
   \end{align*}
   Moreover, if $\nabla^2 \Phi(x)$ is Lipschitz on $\K$ and $F$ is locally Lipschitz, then the solution is unique.
</p>

## Lagrangian multipliers

If $\K$ is a polyhedron, the one can write
<p>
\begin{equation}\label{eq:polyhedron}
   \K = \{ x \in \R^n : Ax \leq b \}, \qquad A \in \R^{m \times n}, b \in \R^m\,.
\end{equation}
</p>
In this case, the normal cone at $x$ is the cone spanned by the normals of the tight constraints at $x$:
<p>
\begin{equation}\label{eq:cone-poly}
   N_{\K}(x) = \left\{ A^T y : y \geq 0 \textrm{ and } y^T(b-Ax)=0 \right\}.
\end{equation}
</p>

Consider now the application of <A href="#thm:md">Theorem MD</a> to a polyhedron and a solution $x : [0,\infty) \to \K$,
$\lambda : [0,\infty) \to \R^n$ such that
<p>
\begin{equation}\label{eq:traj}
   \nabla^2 \Phi(x(t)) x'(t) = F(t,x(t)) - \lambda(t),
\end{equation}
</p>
and $\lambda(t) \in N_{\K}(x(t))$ for $t \geq 0$.

Let us consider the dual variables to the constraints \eqref{eq:polyhedron}:
We can fix a measurable $\hat{\lambda} : [0,\infty) \to \R^m_+$ such that
\[
   A^T \hat{\lambda}(t) = \lambda(t), \quad t \geq 0.
\]
Now \eqref{eq:cone-poly} and $\lambda(t) \in N_{\K}(x(t))$ yield the complementary-slackness
conditions:  For all $i=1,2,\ldots,m$ and $t \geq 0$:
\[
   \hat{\lambda}_i(t) > 0 \implies \langle A_i,x(t)\rangle = b_i,
\]
where $A_i$ is the $i$th row of $A$.

## The Bregman divergence as a Lyapunov function

We promised earlier the existence of a functional to control the dynamics,
and this is provided by the **Bregman divergence associated to $\Phi$**:
<p>
\[
   D_{\Phi}(y; x) \seteq \Phi(y) - \Phi(x) - \langle \nabla \Phi(x), y-x\rangle\,.
\]
</p>
Let $x(t)$ be a trajectory satisfying \eqref{eq:traj}.  Then for any $y \in \K$:
<p>
\begin{align}
   \partial_t D_{\Phi}(y; x(t)) &= - \langle \nabla \Phi(x(t)), x'(t)\rangle  + \langle \nabla \Phi(x(t)), x'(t) \rangle
   -\langle \partial_t \Phi(x(t)), y-x(t)\rangle \nonumber \\
                                &= - \langle \nabla^2 \Phi(x(t)) x'(t), y - x(t) \rangle \nonumber \\
                                &= - \langle F(t,x(t)) - \lambda(t), y-x(t)\rangle \nonumber \\
                                &\leq - \langle F(t,x(t)), y-x(t)\rangle \label{eq:div}\,,
\end{align}
</p>
where the last inequality used that $y \in \K$ and $\lambda(t) \in N_{\K}(x(t))$.

If $F(t,x(t)) = - c(t)$ is a *cost function*, say, then this inequality
aligns with a goal stated at the beginning of the first lecture:
As long as the algorithm $x(t)$ is suffering more cost than some feasible point $y \in \K$,
we would like to be "learning" about $y$.

## The algorithm from last time

In the next lecture, we will use this framework to derive and analyze
algorithms for metrical task systems (MTS) and the $k$-server problem.
For now, let us show that the algorithm and analysis
from last time (for MTS on uniform metrics) fit precisely into our framework.

Suppose that $\K = \\{ x \in \R_+^n : \sum_{i=1}^n x_i = 1 \\}$ is the probability simplex and
<p>
\[
   \Phi(x) = \sum_{i=1}^n (x_i+\delta) \log (x_i+\delta)
\]
</p>
is the (negative) entropy with some shift by $\delta > 0$.
In the next lecture, we will see why the negative entropy
arises naturally as a mirror map.

Then $\nabla^2 \Phi(x)$ is a diagonal matrix with $\left(\nabla^2 \Phi(x)\right)_{ii} = \frac{1}{x_i+\delta}$.
Let $F(t,\cdot) = -c(t)$ be a time-varying cost vector with $c(t) \geq 0$.

Therefore \eqref{eq:traj} gives
<p>
\begin{equation}\label{eq:shifted}
   x_i'(t) = (x_i(t)+\delta) \left(-c_i(t) + \hat{\mu}(t) - \hat{\lambda}_i(t)\right).
\end{equation}
Here, $\hat{\lambda}_i(t)$ is the Lagrangian multiplier corresponding to the constraint $x_i \geq 0$,
and $\hat{\mu}(t)$ is the multiplier corresponding to $\sum_{i=1}^n x_i = 1$.
</p>

This is precisley the algorithm described before (as an exercise,
one might try rewriting it to match exactly), and \eqref{eq:div} constitutes half of the analysis.
In the next lecture, we will discuss some general methods for the other half:  Tracking the movement cost.

