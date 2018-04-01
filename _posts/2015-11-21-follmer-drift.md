---
layout:     post
title:      An entropy optimal drift
date:       2015-11-21
summary:    F&ouml;llmer's drift, Ito's lemma, and the Gaussian log-Sobolev inequality
categories: jekyll pixyll
---

## Construction of F&ouml;llmer's drift

In a previous post, we saw how an entropy-optimal drift process
could be used to prove the Brascamp-Lieb inequalities.
Our main tool was a result of F&ouml;llmer that we now recall and justify.
Afterward, we will use it to prove the Gaussian log-Sobolev inequality.

Consider $f : \mathbb R^n \to \mathbb R_+$ with $\int f \,d\gamma_n = 1$,
where $\gamma_n$ is the standard Gaussian measure on $\mathbb R^n$.
Let $\\{B_t\\}$ denote an $n$-dimensional Brownian motion with $B_0=0$.
We consider all processes of the form
\begin{equation}\label{eq:drift}
W_t = B_t + \int_0^t v_s\,ds\,,
\end{equation}
where $\\{v_s\\}$ is a progressively measurable drift
and such that $W_1$ has law $f\,d\gamma_n$.

<div class="theorem" text="Energy-entropy">
It holds that
\[
D(f d\gamma_n \,\|\, d\gamma_n) = \min D(W_{[0,1]} \,\|\, B_{[0,1]}) = \min \frac12 \int_0^1 \mathbb{E}\,\|v_t\|^2\,dt\,,
\]
where the minima are over all processes of the form \eqref{eq:drift}.
</div>

<div class="proof">
In the preceding post (Lemma 2), we have already seen that
for any drift of the form \eqref{eq:drift}, it holds that
\[
D(f d\gamma_n \,\|\,d\gamma_n) \leq \frac12 \int_0^1 \mathbb{E}\,\|v_t\|^2\,dt \leq D(W_{[0,1]} \,\|\, B_{[0,1]})\,,
\]
thus we need only exhibit a drift $\\{v_t\\}$ achieving equality.

<p>
We define
\[
v_t = \nabla \log P_{1-t} f(W_t) = \frac{\nabla P_{1-t} f(W_t)}{P_{1-t} f(W_t)}\,,
\]
where $\\{P_t\\}$ is the Brownian semigroup defined by
\[
P_t f(x) = \mathbb{E}[f(x + B_t)]\,.
\]
</p>

<p>
Note that $v_t$ is almost surely constant conditioned on the past, hence the chain rule yields
\begin{equation}\label{eq:chain}
D(W_{[0,1]} \,\|\, B_{[0,1]}) =
\frac12 \int_0^1 \mathbb{E}\,\|v_t\|^2\,dt\,.
\end{equation}
(See line (7) of Lemma 2 in the previous post.  Note that $h(v_t)=0$ since $v_t$ is deterministic given the past.)
We are left to show that $W_1$ has law $f \,d\gamma_n$ and $D(W_{[0,1]} \,\|\, B_{[0,1]}) = D(f d\gamma_n \,\|\,d\gamma_n)$.
</p>

<p>
We will prove the first fact using Girsanov's theorem to argue about
the change of measure between $\{W_t\}$ and $\{B_t\}$.
As in the previous post, we will argue somewhat informally
using the heuristic that the law of $dB_t$ is a Gaussian
random variable in $\mathbb R^n$ with covariance $dt \cdot I$.
It&ocirc;'s formula states that this heuristic is justified (see our use
of the formula below).
</p>

The following lemma says that, given any sample path $\{W_s : s \in [0,t]\}$
of our process up to time $s$, the probability that Brownian motion (without drift)
would have
"done the same thing is $\frac{1}{M_t}$.
</div>

<div class="remark">
I chose to present various steps in the next proof at varying levels of formality.
The arguments have the same structure as corresponding formal proofs,
but I thought (perhaps na&iuml;vely) that this would be instructive.
</div>

<div class="lemma" text="Heuristic Girsanov">
Let $\mu_t$ denote the law of $\\{W_s : s \in [0,t]\\}$.
If we define
\[
M_t = \exp\left(-\int_0^t \langle v_s,dB_s\rangle - \frac12 \int_0^t \|v_s\|^2\,ds\right)\,,
\]
then under the measure $\nu_t$ given by
\[
d\nu_t = M_t \,d\mu_t\,,
\]
the process $\\{W_s : s \in [0,t]\\}$ has the same law as $\\{B_s : s \in [0,t]\\}$.
</div>

<div class="proof">
We argue by analogy with the discrete proof.
First, let us define the infinitesimal ``transition kernel'' of Brownian motion
using our heuristic that $dB_t$ has covariance $dt \cdot I$:
\[
p(x,y) = \frac{e^{-\|x-y\|^2/2dt}}{(2\pi dt)^{n/2}}\,.
\]
<p>
We can also compute the (time-inhomogeneous) transition kernel $q_t$ of $\\{W_t\\}$:
\[
q_t(x,y) =  \frac{e^{-\|v_t dt + x - y\|^2/2dt}}{(2\pi dt)^{n/2}} = p(x,y) e^{-\frac12 \|v_t\|^2 dt} e^{-\langle v_t, x-y\rangle}\,.
\]
Here we are using that $dW_t = dB_t + v_t\,dt$ and $v_t$ is deterministic conditioned on the past, thus
the law of $dW_t$ is a normal with mean $v_t\,dt$ and covariance $dt \cdot I$.
</p>

<p>
To avoid confusion of derivatives, let's use $\alpha_t$ for the density of $\mu_t$ and $\beta_t$ for the density of
Brownian motion (recall that these are densities on paths).
Now let us relate the density $\alpha_{t+dt}$ to the density $\alpha_{t}$.
We use here the notations $\\{\hat W_t, \hat v_t, \hat B_t\\}$ to denote
a (non-random) sample path of $\\{W_t\\}$:
\begin{align*}
\alpha_{t+dt}(\hat W_{[0,t+dt]}) &= \alpha_t(\hat W_{[0,t]})  q_t(\hat W_t, \hat W_{t+dt}) \\
&=  \alpha_t(\hat W_{[0,t]}) p(\hat W_t, \hat W_{t+dt}) e^{-\frac12 \|\hat v_t\|^2\,dt-\langle \hat v_t,\hat W_t-\hat W_{t+dt}\rangle} \\
&=
\alpha_t(\hat W_{[0,t]})  p(\hat W_t, \hat W_{t+dt}) e^{-\frac12 \|\hat v_t\|^2\,dt+\langle \hat v_t,d \hat W_t\rangle} \\
&=
\alpha_t(\hat W_{[0,t]})  p(\hat W_t, \hat W_{t+dt}) e^{\frac12 \|\hat v_t\|^2\,dt+\langle \hat v_t, d \hat B_t\rangle}\,,
\end{align*}
where the last line uses $d\hat W_t = d\hat B_t + \hat v_t\,dt$.
</p>

Now by ``heuristic'' induction, we can assume $\alpha_t(\hat W_{[0,t]})=\frac{1}{M_t} \beta_t(\hat W_{[0,t]})$, yielding
\begin{align*}
\alpha_{t+dt}(\hat W_{[0,t+dt]}) &= \frac{1}{M_t} \beta_t(\hat W_{[0,t]})  p(\hat W_t, \hat W_{t+dt}) e^{\frac12 \|\hat v_t\|^2\,dt+\langle \hat v_t, d \hat B_t\rangle} \\
&=
\frac{1}{M_{t+dt}}  \beta_t(\hat W_{[0,t]}) p(\hat W_t, \hat W_{t+dt}) \\
&=
\frac{1}{M_{t+dt}}  \beta_{t+dt}(\hat W_{[0,t+dt]})\,.
\end{align*}
In the last line, we used the fact that $p$ is the infinitesimal transition kernel for Brownian motion.
</div>

## The Gaussian log-Sobolev inequality

Consider again a measurable $f : \mathbb R^n \to \mathbb R_+$ with $\int f\,d\gamma_n=1$.
Let us define $\mathrm{Ent}_{\gamma_n}(f) = D(f\,d\gamma_n \,\\|\,d\gamma_n)$.
Then the classical log-Sobolev inequality in Gaussian space asserts that

\begin{equation}\label{eq:logsob}
\mathrm{Ent}_{\gamma_n}(f) \leq \frac12 \int \frac{\|\nabla f\|^2}{f}\,d\gamma_n\\,.
\end{equation}

First, we discuss the correct way to interpret this.
Define the Ornstein-Uhlenbeck semi-group $\\{U_t\\}$ by its action
\\[
U_t f(x) = \mathbb{E}[f(e^{-t} x + \sqrt{1-e^{-2t}} B_1)]\\,.
\\]
This is the natural stationary diffusion process on Gaussian space.  For every measurable $f$, we have
\\[
U_t f \to \int f d\gamma_n \quad \textrm{ as $t \to \infty$}\,,
\\]
or equivalently
\\[
\mathrm{Ent}_{\gamma_n}(U_t f) \to 0 \quad \textrm{ as $t \to \infty$}\,.
\\]

<p>
The log-Sobolev inequality yields quantitative convergence in the relative entropy
distance as follows:
Define the <em>Fisher information</em>
\[
I(f) = \int \frac{\|\nabla f\|^2}{f} \,d\gamma_n\,.
\]
</p>

<p>
One can check that
$$
\frac{d}{dt} \mathrm{Ent}_{\gamma_n} (U_t f)\Big|_{t=0} = - I(f)\,,
$$
thus the Fisher information describes the instantaneous decay of the relative entropy of $f$
under diffusion.
</p>

<p>
So we can rewrite the log-Sobolev inequality as:
\[
- \frac{d}{dt} \mathrm{Ent}_{\gamma_n}(U_t f)\Big|_{t=0} \geq \mathrm{Ent}_{\gamma_n}(f)\,.
\]
This expresses the intuitive fact that when the relative entropy is large,
its rate of decay toward equilibrium is faster.
</p>
