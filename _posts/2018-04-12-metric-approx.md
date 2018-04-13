---
layout:     post
title:      Approximation by ultrametrics
date:       2018-04-12
summary:    The competitive ratio for MTS is controlled by ultrametrics
categories: online
---

We now take a short detour away from mirror descent, and
instead examine how a special class of metric spaces called *ultrametrics*
control the competitive ratio of MTS in general metric spaces.
Hold onto your seats; we're about to compress two decades and 
10 papers into a few paragraphs.
For the sake of continuity, bibliographic remarks are held to the end of the post.
$$\def\e{\varepsilon}$$


## Metric approximations

For a metric space $(X,d)$, let $\alpha_{\mathrm{mts}}(X,d)$ denote
the best competitive ratio for MTS on $(X,d)$.
Suppose $D$ is some other metric on $X$ that satisfies
<p>
\begin{equation}\label{eq:distortion}
   \frac{D(x,y)}{K} \leq d(x,y) \leq D(x,y) \qquad \forall x,y \in X\,.
\end{equation}
</p>
Then it is straightforward to verify that $\alpha_{\mathrm{mts}}(X,d) \leq K \cdot \alpha_{\mathrm{mts}}(X,D)$.

But there is a weaker form of approximation that still allows for such a conclusion.
Suppose that $\mathbf{D}$ is a *random* metric that satisfies, for every $x,y \in X$:

1. With probability one, $\mathbf{D}(x,y) \geq d(x,y)$,
2. $\mathbb{E}\left[\mathbf{D}(x,y)\right] \leq K \cdot d(x,y)$.

If $\alpha_{\mathrm{mts}}(X,\mathbf{D}) \leq \alpha$ with probability one, we claim that
$\alpha_{\mathrm{mts}}(X,d) \leq K \alpha$.

The algorithm achieving this is as follows:  Sample the random metric $\mathbf{D}$.
Now given a cost sequence $\left\langle c_t : X \to \mathbb{R}_+ \mid t \geq 1\right\rangle$,
let $\left\langle x_0, x_1, x_2, \ldots \right\rangle$ be the random sequence of points produced
by an $\alpha$-competitive randomized algorithm for $(X,\mathbf{D})$.  Then:
<p>
\[
   \mathbb{E}\left[\sum_{t=1}^T \left.\vphantom{\bigoplus}
         \mathbf{D}(x_t, x_{t-1}) \ \right| \mathbf{D}\right] \leq
         \alpha \sum_{t=1}^T \mathbf{D}\!\left(x_t^{*}, x_{t-1}^{*}\right)
         + O(1)\,,
\]
</p>
where $\left\langle x_t^\* : t \geq 0\right\rangle$
is an optimal offline sequence for $(X,d)$.
(This may not be the optimal sequence for $(X,\mathbf{D})$, but the algorithm
is certainly competitive against non-optimal sequences as well.)

Note that the expectation here is taken only with respect to the randomness in the online algorithm.
If we take expectation with respect to $\mathbf{D}$ as well, it follows that
<p>
\[
   \mathbb{E}\left[\sum_{t=1}^T d(x_t, x_{t-1})\right] \leq
   \alpha \mathbb{E}\left[\sum_{t=1}^T \mathbf{D}\left(x_t^{*}, x_{t-1}^{*}\right)\right]
         + O(1)
         \leq K \alpha
   \sum_{t=1}^T d\!\left(x_t^{*}, x_{t-1}^{*}\right) + O(1)\,,
\]
</p>
where we have used property (1) of $\mathbf{D}$ for the LHS and property (2) to bound the RHS.

## Ultrametrics

Let $T=(V,E)$ be a finite, rooted tree, and let $\mathcal{L}$ denote the leaves of $T$.
Suppose $w : V\setminus \mathcal{L} \to \mathbb{R}_+$ is a function that assigns
positive weights to the internal vertices of $T$ such that the vertex
weights are non-increasing along root-leaf paths.
Then one can define a distance on $\mathcal{L}$ by
\[
   d_w\left(\ell,\ell'\right) \mathrel{\vcenter{:}}= w\left(\mathrm{lca}(\ell,\ell')\right).
\]
This is an *[ultrametric](https://en.wikipedia.org/wiki/Ultrametric_space)* on $\mathcal{L}$ (and all finite ultrametrics
arise in this way).

It turns out that ultrametrics essentially control the competitive ratio
for metrical task systems on finite metric spaces.
This follows from the next two facts that
hold for an arbitrary $n$-point metric space $(X,d)$.

<a name="thm1"></a>
<p class="theorem" text="Random embedding" ord="1">
There is a random ultrametric $\mathbf{D}$ on $(X,d)$ such that (1) and (2) are satisfied with $K \leq O(\log n)$.
</p>

By our earlier remarks, this implies that the competitive ratio for MTS on $(X,d)$
is at most $O(\log n)$ times the competitive ratio for $n$-point ultrametrics.

<a name="thm2"></a>
<p class="theorem" text="Metric Ramsey" ord="2">
There is a subset $X' \subseteq X$ with $|X'| \geq \sqrt{n}$ and
an ultrametric $D$ on $X'$ such that 
\eqref{eq:distortion} is satisfied with $K \leq O(1)$.
</p>

Since $\alpha_{\mathrm{mts}}(X,d) \geq \alpha_{\mathrm{mts}}(X',d) \geq \Omega(\alpha_{\mathrm{mts}}(X',D))$,
lower bounds on the competitive ratio for ultrametrics yield lower bounds for $(X,d)$ as well.
Finally, we remark that MTS on ultrametrics is now well-understood.

<a name="thm3"></a>
<p class="theorem" text="MTS on ultrametrics" ord="3">
   If $(X,D)$ is an $n$-point ultrametric, then
   \[
      \Omega\left(\frac{\log n}{\log \log n}\right) \leq \alpha_{\mathrm{mts}}(X,D) \leq O(\log n)\,.
   \]
</p>

There are ultrametrics (e.g., as we have seen already, when $(X,D)$ is the uniform metric)
for which the $O(\log n)$ upper bound in <a href="#thm3">Theorem 3</a> is tight.
Whether the LHS can be made $\Omega(\log n)$ is an intriguing open problem;
we will address it in the next lecture.
In conjunction with <a href="#thm1">Theorem 1</a> and <a href="#thm2">Theorem 2</a>,
this yields:

<a name="cor4"></a>
<p class="corollary" text="MTS" ord="4">
For any $n$-point metric space $(X,d)$:
\[
   \Omega\left(\frac{\log n}{\log \log n}\right) \leq \alpha_{\mathrm{mts}}(X,d) \leq O((\log n)^2)\,.
\]
</p>

Perhaps the central remaining open question for MTS on general metric spaces
is whether the upper bound can be improved to $O(\log n)$.

## Ultrametrics from partitions

Consider a partition $P$ of $X$.  Say that $P$ is *$\Delta$-bounded*
if $S \in P \implies \mathrm{diam}_X(S) \leq \Delta$.
For a point $x \in X$, we write $P(x)$ for the unique set in $P$ that contains $x$.

Suppose now that $\mathcal{P} = \\{ P_j : j \in \mathbb{Z} \\}$ is a sequence of partitions of $X$
such that $P_j$ is $8^j$-bounded for every $j \in \mathbb{Z}$, and define the metric
<p>
\[
   D_{\mathcal{P}}(x,y) \mathrel{\vcenter{:}}= \max \left\{ 8^{j+1} : P_j(x) \neq P_j(y) \right\}.
\]
</p>
One can check that $D_{\mathcal{P}}$ is an ultrametric on $X$ (imagine
the tree structure induced by the partitions), and moreover
<p>
\begin{equation}\label{eq:exp}
   D_{\mathcal{P}}(x,y) \geq d(x,y) \qquad \forall x,y \in X\,.
\end{equation}
</p>
This follows from:  $D_{\mathcal{P}}(x,y) \leq 8^j \implies P_j(x)=P_j(y) \implies d(x,y) \leq 8^j$.

Define $B(x,r) \mathrel{\vcenter{:}}= \\{ y \in X : d(x,y) \leq r \\}$ to be the ball of radius $r$ about $x \in X$.

<p class="lemma" text="Random partition lemma">
   Suppose $(X,d)$ is an $n$-point metric space.  Then for every $\Delta > 0$,
   there is a random $\Delta$-bounded partition $P$ of $X$ such that for every $r \leq \Delta/8$:
   <p>
   \begin{equation}\label{eq:rp}
      \mathbb{P}\left[\vphantom{\bigoplus}
         B(x,r) \subseteq P(x)\right] \geq \exp\left(\frac{-8r}{\Delta} \log \frac{|B(x,\Delta)|}{|B(x,\Delta/8)|}\right).
   \end{equation}
   </p>
</p>

Remarkably, the random partitioning lemma can be used to prove both **Theorem 1** and **Theorem 2**.
We will first establish these consequences and then prove the lemma.

## Approximation by a random ultrametric

Let's prove <a href="#thm1">Theorem 1</a>.
Let $\mathcal{P} = \\{ P_j : j \in \mathbb{Z} \\}$ be the random sequence where $P_j$ results from the
random partitioning lemma applied with $\Delta = 8^j$ and we take the partitions to be mutually independent.
Then from \eqref{eq:exp}, we know $\mathbf{D}_{\mathcal{P}}(x,y) \geq d(x,y)$ for all $x,y \in X$.
Now fix $x \neq y \in X$, and let $j_0 \mathrel{\vcenter{:}}= \min \\{ j : 8^{j} \geq d(x,y) \\}$.  Then:
<p>
\[
   \mathbb{E}\left[\mathbf{D}_{\mathcal{P}}(x,y)\right] \leq 8^{j_0+1} + \sum_{j > j_0} \mathbb{P}[P_j(x) \neq P_j(y)] 8^{j+1},
\]
</p>
and using $\mathbb{P}[P_j(x) = P_j(y)] \geq \mathbb{P}[B(x, d(x,y)) \subseteq P_j(x)]$ yields
<p>
\begin{align*}
\sum_{j > j_0} \mathbb{P}[P_j(x) \neq P_j(y)] 8^{j+1}
&\leq \sum_{j \in \mathbb{Z}} 8^{j+2} \frac{d(x,y)}{8^{j}} \log \frac{|B(x, 8^j)|}{|B(x,8^{j-1})|} \\
&\leq 64\, d(x,y) \sum_{j \in \mathbb{Z}} \log \frac{|B(x, 8^j)|}{|B(x,8^{j-1}|} \\
&= 64 \,d(x,y) \log n\,.
\end{align*}
</p>
where the second inequality follows from \eqref{eq:rp} and the fact that $e^{-x} \geq 1-x$,
and in the last inequality we evaluate a telescoping sum.

## Finding a large approximate ultrametric inside $X$

Now we prove <a href="#thm2">Theorem 2</a>.
Let $\mathcal{P}$ be the same random partition sequence chosen above and fix some $0 < \e < 1/8$.
Define the random subset:
<p>
\[
   \mathbf{S} \mathrel{\vcenter{:}}= \left\{ x \in X : B(x, \e 8^j) \subseteq P_j(x) \ \forall j \in \mathbb{Z}\right\}\,.
\]
</p>
We claim that
<p>
\[
   D_{\mathcal{P}}(x,y) \geq d(x,y) \geq \frac{\e}{8} D_{\mathcal{P}}(x,y) \qquad \forall x,y \in \mathbf{S}\,.
\]
</p>
The LHS is simply from \eqref{eq:exp}.
For the RHS, observe that if $D_{\mathcal{P}}(x,y)=8^{j+1}$, then $P_j(x) \neq P_j(y)$,
hence $B(x,\e 8^j) \subseteq P_j(x) \implies d(x,y) \geq \e 8^j$.

Now the random partitioning lemma gives, for any $x \in X$,
<p>
\[
   \mathbb{P}[x \in \mathbf{S}] \geq \prod_{j \in \mathbb{Z}} \exp\left(- 8\e \log \frac{|B(x,8^j)|}{|B(x,8^{j-1})|}\right)
   = \exp\left(-8 \e \log n\right) = n^{-8\e}\,.
\]
</p>
By linearity of expectation: $\mathbb{E}[|\mathbf{S}|] \geq n^{1-8\e}$.  Taking $\e \mathrel{\vcenter{:}}= 1/16$ completes the proof.

## Proof of the random partitioning lemma

Let $\mathbf{R} \in [\Delta/4,\Delta/2]$ be chosen uniformly,
and let $X = \\{x_1, x_2, \ldots, x_n\\}$ be a uniformly random
ordering of the points in $X$.
Our random partitioning is formed by iteratively carving out balls:
<p>
\begin{equation}\label{eq:ckr}
   P \mathrel{\vcenter{:}}= \left\{ B(x_i, \mathbf{R}) \setminus \bigcup_{j < i} B(x_j, \mathbf{R}) : i=1,2,\ldots,n\right\}.
\end{equation}
</p>
Clearly $P$ is $\Delta$-bounded by construction.

Fix $r \leq \Delta/8$ and observe first that
<p>
\[
   \mathbb{P}\left[B(x,r) \subseteq P(x) \mid \mathbf{R}\right] \geq \frac{|B(x,\mathbf{R}-r)|}{|B(x,\mathbf{R}+r)|}.
\]
</p>
This follows because if we condition on $\mathbf{R}$, then the first center chosen in $B(x,\mathbf{R}+r)$
will decide the fate of $B(x,r)$, and the corresponding cluster will contain
all of $B(x,r)$ if the center lies in $B(x,\mathbf{R}-r)$.

Thus we have:
<p>
\begin{align*}
   \mathbb{P}\left[B(x,r) \subseteq P(x)\right] &\geq \mathbb{E}\left[\frac{|B(x,\mathbf{R}-r)|}{|B(x,\mathbf{R}+r)|}\right] \\
                                         &= \mathbb{E}\left[\exp\left(- \log \frac{|B(x,\mathbf{R}+r)|}{|B(x,\mathbf{R}-r)|}\right)\right]  \\
                                         &\geq 
   \exp \left(\mathbb{E}\left[- \log \frac{|B(x,\mathbf{R}+r)|}{|B(x,\mathbf{R}-r)|}\right]\right)  \\
&\geq \exp\left(\frac{- 8 r}{\Delta} \log \frac{|B(x,\Delta)|}{|B(x,\Delta/8)|}\right)\,,
\end{align*}
</p>
where the second inequality uses convexity of $e^{-x}$ and
the last inequality comes from the calculation
<p>
\begin{align*}
\mathbb{E}\left[ \log \frac{|B(x,\mathbf{R}+r)|}{|B(x,\mathbf{R}-r)|}\right] 
&= \frac{4}{\Delta} \int_{\Delta/4}^{\Delta/2} 
\log \frac{|B(x,R+r)|}{|B(x,R-r)|}\,dR \\
&\leq \frac{8r}{\Delta} \log \frac{|B(x,\Delta/2+r)|}{|B(x,\Delta/4-r)|} \\
&\leq \frac{8r}{\Delta} \log \frac{|B(x,\Delta)|}{|B(x,\Delta/8)|}\,,
\end{align*}
</p>
using $r \leq \Delta/8$.

## Historical remarks

The random embedding theorem (<a href="#thm1">Theorem 1</a>)
is due to [Fakcharoenphol, Rao, and Talwar][FRT].
The first such result was [proved by Bartal][Bartal96], and he later
[obtained a near-optimal bound][Bartal98]
of $O(\log n \log \log n)$ on the distortion.
The use of random tree approximations of arbitrary metric spaces
for online algorithms arose somewhat earlier in
the work of [Alon, Karp, Peleg, and West][AKPW],
specifically in relation to the $k$-server problem.

The metric Ramsey theorem (<a href="#thm2">Theorem 2</a>)
is a result of [Bartal, Linial, Mendel, and Naor][BLMN],
improving over an earlier bound of [Bartal, Bollobas, and Mendel][BBM]
who established that one can take $|X'| \geq \exp(c \sqrt{\log n})$ for some $c > 0$.

The upper bound in <a href="#thm3">Theorem 3</a>
is from a forthcoming paper with Bubeck, Cohen, and Y. T. Lee,
and improves the
$O(\log n \log \log n)$ upper bound of [Fiat and Mendel][FM]
to the optimal value (up to a constant factor).
The lower bound in <a href="#thm3">Theorem 3</a>
is from the aforementioned paper of Bartal, Bollobas, and Mendel;
we will discuss it in the next lecture.

The random partitioning lemma
and the proof of <a href="#thm2">Theorem 2</a>
presented here come from a paper of [Mendel and Naor][MN].
This proof of the random partitioning lemma is somewhat
cleaner than the one presented there.
The (now famous) distribution on random partitions 
described in \eqref{eq:ckr} is from [Calinescu, Karloff, and Rabani][CKR].

[FRT]: https://www.sciencedirect.com/science/article/pii/S0022000004000637
[Bartal96]: http://ieeexplore.ieee.org/iel3/4141/11790/00548477.pdf
[Bartal98]: https://dl.acm.org/citation.cfm?id=276725
[AKPW]: http://www.icsi.berkeley.edu/ftp/pub/techreports/1991/tr-91-066.pdf
[BLMN]: https://arxiv.org/abs/math/0406353
[BBM]: https://arxiv.org/abs/cs/0406028
[FM]: https://arxiv.org/abs/cs/0406034
[MN]: https://arxiv.org/abs/cs/0511084
[CKR]: https://epubs.siam.org/doi/abs/10.1137/S0097539701395978
