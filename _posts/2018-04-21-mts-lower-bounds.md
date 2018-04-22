---
layout:     post
title:      Lower bounds for MTS
date:       2018-04-20
summary:    We prove lower bounds for MTS on certain classes of ultrametrics
categories: online
---


<p>Consider a rooted tree <span class="math inline">\(T=(V,E)\)</span> with leaf set <span class="math inline">\(\mathcal L\subseteq V\)</span> and positive vertex weights <span class="math inline">\(w : V\setminus \mathcal L\to \mathbb R_+\)</span> that are non-increasing along root-leaf paths. We recall the ultrametric <span class="math inline">\(d_w\)</span> defined on <span class="math inline">\(\mathcal L\)</span> by 
<p>
$$
  d_w(\ell,\ell') \mathrel{\vcenter{:}}= w(\mathrm{lca}(\ell,\ell')).
$$
</p>

<p>
Say that <span class="math inline">\((\mathcal L,d_w)\)</span> is a <span><em><span class="math inline">\(\tau\)</span>-HST metric</em></span> for some <span class="math inline">\(\tau \geq 1\)</span> if <span class="math inline">\(\mathcal L\)</span> is the leaf set of some weighted tree <span class="math inline">\(T=(V,E)\)</span>, and <span class="math inline">\(d_w\)</span> is the ultrametric corresponding to a weight <span class="math inline">\(w\)</span> on <span class="math inline">\(T\)</span> with the property that <span class="math inline">\(w(y) \leq w(x)/\tau\)</span> whenever <span class="math inline">\(y\)</span> is a child of <span class="math inline">\(x\)</span>. (So for a finite metric space, the notions of <span class="math inline">\(1\)</span>-HST metric and ultrametic are equivalent.) Say that <span class="math inline">\((\mathcal L,d)\)</span> is a <span><em>strict <span class="math inline">\(\tau\)</span>-HST metric</em></span> if we require the stronger property that <span class="math inline">\(w(y)=w(x)/\tau\)</span> whenever <span class="math inline">\(x,y \in V\)</span> are internal nodes and <span class="math inline">\(y\)</span> is a child of <span class="math inline">\(x\)</span>.</p>
<p>Two metrics <span class="math inline">\(d\)</span> and <span class="math inline">\(d'\)</span> on a set <span class="math inline">\(X\)</span> are <span><em><span class="math inline">\(K\)</span>-equivalent</em></span> if there is a constant <span class="math inline">\(c &gt; 0\)</span> such that <span class="math display">\[d(x,y) \leq c\, d'(x,y) \leq K d(x,y)\qquad \forall x,y \in X\,.\]</span> We leave the following statements as an exercise:
For every <span class="math inline">\(\tau &gt; 1\)</span>, every <span class="math inline">\(1\)</span>-HST is <span class="math inline">\(\tau\)</span>-equivalent to some strict <span class="math inline">\(\tau\)</span>-HST.</p>

<a name="thm:bbm"></a>
<p class="theorem" text="Bartal-Bollobas-Mendel" ord="1">
There is a constant <span class="math inline">\(C \geq 1\)</span> such that if <span class="math inline">\((\mathcal L,d_w)\)</span> is a <span class="math inline">\(C (\log n)^2\)</span>-HST metric, where <span class="math inline">\(n=|\mathcal L|\)</span>, then the competitive ratio for MTS on <span class="math inline">\((\mathcal L,d_w)\)</span> is <span class="math inline">\(\Omega\left(\log n\right)\)</span>.</p>

While the preceding theorem applies only to $\tau$-HSTs with $\tau$ sufficiently large,
the next lemma shows how we can improve the separation parameter by passing
to a subset of leaves.

<p class="lemma">
If <span class="math inline">\((\mathcal L,d)\)</span> is a strict <span class="math inline">\(2\)</span>-HST, then for every <span class="math inline">\(k \in \mathbb N\)</span>, there is a subset <span class="math inline">\(\mathcal L' \subseteq \mathcal L\)</span> with
<p>
$$
|\mathcal{L}'| \geq |\mathcal{L}|^{1/k},
$$
</p>
and such that <span class="math inline">\((\mathcal L', d)\)</span> is a <span class="math inline">\(2^k\)</span>-HST metric.
</p>


<p>Combining this with <a href="#thm:bbm">Theorem 1</a> yields:</p>
<p class="corollary">
If <span class="math inline">\((\mathcal L,d)\)</span> is a <span class="math inline">\(1\)</span>-HST metric with <span class="math inline">\(n=|\mathcal L|\)</span>, then the competitive ratio for MTS on <span class="math inline">\((\mathcal L,d)\)</span> is at least
<span class="math inline">\(\Omega\left(\frac{\log n}{\log \log n}\right)\)</span>.
</p>

<p>Recall that the Metric Ramsey theorem from the preceding lecture implies that every <span class="math inline">\(n\)</span>-point metric space contains a subset of size <span class="math inline">\(\sqrt{n}\)</span> that is <span class="math inline">\(O(1)\)</span>-equivalent to a <span class="math inline">\(1\)</span>-HST. This yields:</p>

<p class="theorem">
For every <span class="math inline">\(n\)</span>-point metric space, the competitive ratio for MTS is at least <span class="math inline">\(\Omega(\log n/\log \log n)\)</span>.
</p>

<p>We will not prove <a href="#thm:bbm">Theorem 1</a>, but we will prove a lower bound for two special cases that together capture the essential elements of the full argument. The general case is discussed at the end.</p>

## The complete d-ary tree

<p>The first case we’ll consider is when <span class="math inline">\(T\)</span> is a <span class="math inline">\(d\)</span>-ary tree of height <span class="math inline">\(h\)</span>, so that <span class="math inline">\(|\mathcal L|=d^h\)</span>. Define <span class="math inline">\(w(x)=\tau^{-\mathrm{dist}_T(x,r)}\)</span>, where <span class="math inline">\(r\)</span> is the root of <span class="math inline">\(T\)</span> and <span class="math inline">\(\mathrm{dist}_T\)</span> denotes the combinatorial distance on <span class="math inline">\(T\)</span>. Then <span class="math inline">\((\mathcal L,d_w)\)</span> is a <span class="math inline">\(\tau\)</span>-HST.</p>
<p>Our goal is to establish a lower bound of <span class="math inline">\(\Omega(h \log d)\)</span> on the competitive ratio for MTS when <span class="math inline">\(\tau\)</span> is sufficiently large. Note that when <span class="math inline">\(\tau = \Theta(1)\)</span> and <span class="math inline">\(d=2\)</span>, it is an open problem to exhibit an <span class="math inline">\(\Omega(h)\)</span> lower bound, and proving such a bound is likely the most difficult obstacle in obtaining an <span class="math inline">\(\Omega(\log n)\)</span> lower bound for every <span class="math inline">\(n\)</span>-point ultrametric.</p>
<p>Our costs functions will be of the form <span class="math inline">\(\{\epsilon\cdot c_\ell : \ell \in \mathcal L\}\)</span>, where <span class="math inline">\(\epsilon&gt; 0\)</span> is a number, and <span class="math display">\[c_\ell(\ell') = \begin{cases}
                        0 &amp; \ell=\ell' \\
                        1 &amp; \ell \neq \ell'\,.
   \end{cases}\]</span> More succinctly: <span class="math inline">\(c_\ell \mathrel{\vcenter{:}}= \mathbf{1}-\mathbf{1}_\ell\)</span>.</p>
<p>Let <span class="math inline">\(\alpha_h\)</span> be the competitive ratio for height <span class="math inline">\(h\)</span>. We will prove inductively that <span class="math inline">\(\alpha_h \geq \Omega(h \log d)\)</span>.</p>
<p>Consider first the case <span class="math inline">\(h=1\)</span>. We define the height-<span class="math inline">\(1\)</span> cost sequence. The root <span class="math inline">\(r\)</span> has <span class="math inline">\(d\)</span> leaves beneath it. We do the following <span class="math inline">\(d \log d\)</span> times: Choose a random leaf <span class="math inline">\(\ell\)</span> and play the cost function <span class="math inline">\(c_\ell\)</span>. It is straightforward that if <span class="math inline">\(\mathrm{alg}_1\)</span> denotes the cost of an online algorithm, then:
<span class="math display">\[\mathbb{E}[\mathrm{alg}_1] \geq \log d\,.\]</span> (Note that if a cost comes at <span class="math inline">\(\ell\)</span>, then the algorithm must either move and pay movement cost <span class="math inline">\(1\)</span>, or stay in place and pay service cost <span class="math inline">\(1\)</span>.)</p>
<p>Consider the following offline algorithm: Move to the leaf that will be chosen the smallest number of times, and stay there. The movement cost if <span class="math inline">\(1\)</span>, and a standard coupon collecting argument shows that the service cost is <span class="math inline">\(O(1)\)</span>, hence: <span class="math display">\[\mathbb{E}[\mathrm{opt}_1] \leq O(1)\,.\]</span> We conclude that the competitive ratio satisfies <span class="math display">\[\alpha_1 \geq c \log d\]</span> for some <span class="math inline">\(c &gt; 0\)</span>.</p>
<p>Consider now the case of <span class="math inline">\(h \geq 2\)</span>. We define the height-<span class="math inline">\(h\)</span> cost sequence. The root has beneath it <span class="math inline">\(d\)</span> subtrees <span class="math inline">\(T_1, T_2, \ldots, T_d\)</span> of height <span class="math inline">\(h-1\)</span>. For some number <span class="math inline">\(\mu_h\)</span> to be chosen shortly, we do the following <span class="math inline">\(\mu_h d\)</span> times: Choose <span class="math inline">\(i \in \{1,2,\ldots,d\}\)</span> uniformly at random and play in <span class="math inline">\(T_i\)</span> the height-<span class="math inline">\((h-1)\)</span> cost sequence scaled by <span class="math inline">\(1/\tau\)</span>.</p>
<p>Consider first what an online algorithm can do. If the algorithm’s state lies in <span class="math inline">\(T_i\)</span> when a height-<span class="math inline">\((h-1)\)</span> cost sequence is imposed on <span class="math inline">\(T_i\)</span>, it can either leave <span class="math inline">\(T_i\)</span> at some point during the sequence, or it can remain in <span class="math inline">\(T_i\)</span>. Hence the algorithm pays at least
$\min\left(1,\tau^{-1} \mathbb{E}[\mathrm{alg}_{h-1}]\right)$.
It follows that:

<p>
\[\mathbb{E}[\mathrm{alg}_h] \geq \mu_h \min\left(1,\tau^{-1} \mathbb{E}[\mathrm{alg}_{h-1}]\right)
   \geq \mu_h \min\left(1,\tau^{-1} \alpha_{h-1} \mathbb{E}[\mathrm{opt}_{h-1}]\right)\,.\]
</p>
Thus if 
   <p>
   \begin{equation}\label{eq:tauchoice}
   \tau \geq \alpha_{h-1} \mathbb{E}[\mathrm{opt}_{h-1}]\end{equation}
   </p>
it holds that <span class="math display">\begin{equation}\label{eq:alg}
   \mathbb{E}[\mathrm{alg}_h] 
   \geq \mu_h \tau^{-1} \alpha_{h-1} \mathbb{E}[\mathrm{opt}_{h-1}]\,.\end{equation}</span>
We will choose <span class="math inline">\(\tau\)</span> so that
\eqref{eq:tauchoice} holds.</p>

<p>
Let us now analyze an offline algorithm. Let <span class="math inline">\(\rho_i\)</span> denote the number of times that <span class="math inline">\(T_i\)</span> is chosen. The offline algorithm first moves to some <span class="math inline">\(T_i\)</span> with <span class="math inline">\(\rho_i\)</span> minimal, and then plays optimally against level-<span class="math inline">\((h-1)\)</span> cost sequences arriving in <span class="math inline">\(T_i\)</span>.</p>
<p>If <span class="math inline">\(\mu_h \geq \Omega(\log d)\)</span>, then the normal approximation to a binomial distribution shows that there is a constant <span class="math inline">\(0 &lt; c' &lt; 1\)</span> such that <span class="math display">\[\mathbb{E}\left[\min(\rho_1,\ldots,\rho_d)\right] \leq \mu_h - c'\sqrt{\mu_h \log d}\,.\]</span> Hence incorporating the movement cost yields: <span class="math display">\[\mathbb{E}[\mathrm{opt}_h] \leq 1 + \left(\mu_h - c'\sqrt{\mu_h \log d}\right) \tau^{-1} \mathbb{E}[\mathrm{opt}_{h-1}]\,.\]</span></p>
<p>We now choose <span class="math inline">\(\mu_h\)</span> so that <span class="math display">\[c' \sqrt{\mu_h \log d} \tau^{-1} \mathbb{E}[\mathrm{opt}_{h-1}] = 2\,,\]</span> i.e., <span class="math display">\[\mu_h \mathrel{\vcenter{:}}= \frac{4}{\log d} \left(\frac\tau{c' \mathbb{E}[\mathrm{opt}_{h-1}]}\right)^2\]</span> Note from \eqref{eq:tauchoice}, we have <span class="math display">\begin{equation}\label{eq:muh}
   \mu_h \geq \frac{4}{(c')^2\log d} \alpha_{h-1}^2.\end{equation}</span> Since <span class="math inline">\(\alpha_{h-1} \geq \alpha_1 \geq \Omega(\log d)\)</span> it follows that <span class="math inline">\(\mu_h \geq \log d\)</span> for <span class="math inline">\(c'\)</span> chosen small enough. (In particular, the normal approximation applies.)</p>
<p>Our choice of <span class="math inline">\(\mu_h\)</span> ensures that
<span class="math display">
\begin{align}
   \mathbb{E}[\mathrm{opt}_h] &amp;\leq \left(\mu_h-\frac{c'}{2} \sqrt{\mu_h \log d}\right) \tau^{-1} \mathbb{E}[\mathrm{opt}_{h-1}]
\label{eq:opt}\end{align}</span>
Combining this with \eqref{eq:alg} yields
<p>
   $$
   \alpha_h \geq \frac{\mathbb{E}[\mathrm{alg}_h]}{\mathbb{E}[\mathrm{opt}_h]}
   \geq \frac{\alpha_{h-1}}{1-\frac{c'}{2} \sqrt{\frac{\log d}{\mu_h}}}
   \geq \alpha_{h-1} \left(1+\frac{c'}{2} \sqrt{\frac{\log d}{\mu_h}}\right),
   $$
</p>
</p>
where the latter inequality holds because <span class="math inline">\(c' &lt; 1\)</span> and <span class="math inline">\(\mu_h \geq \log d\)</span>. Using \eqref{eq:muh}, this gives <span class="math display">\[\alpha_h \geq \alpha_{h-1} + \frac{c'}{2} \log d\,,\]</span> completing the argument.</p>
<p>Note that in \eqref{eq:tauchoice}, we required <span class="math inline">\(\tau \geq \alpha_{h-1} \mathbb{E}[\mathrm{opt}_{h-1}]\)</span>. So let us use \eqref{eq:opt} to compute: <span class="math display">\[\mathbb{E}[\mathrm{opt}_h] \leq \mu_h \tau^{-1} \mathbb{E}[\mathrm{opt}_{h-1}] \leq \frac{O(1)}{\log d} \frac\tau{\mathbb{E}[\mathrm{opt}_{h-1}]}\]</span> Since <span class="math display">\[\mathbb{E}[\mathrm{opt}_h] \cdot \mathbb{E}[\mathrm{opt}_{h-1}] \leq O(\tau/\log d)\,,\]</span> and <span class="math inline">\(\mathbb{E}[\mathrm{opt}_h] \geq \mathbb{E}[\mathrm{opt}_{h-1}] \geq 1\)</span> for all <span class="math inline">\(h\)</span>,
it follows that <span class="math inline">\(\mathbb{E}[\mathrm{opt}_h] \leq O(\sqrt{\tau/\log d})\)</span>, meaning that <span class="math inline">\(\tau \geq \alpha_{h-1} \mathbb{E}[\mathrm{opt}_{h-1}]\)</span> will be satisfied for <span class="math inline">\(\tau \geq C(\alpha_{h-1}/\log d)^2 \asymp h^2\)</span>. Since <span class="math inline">\(h \asymp \frac{\log n}{\log d}\)</span>, this yields completes the proof of in the special case of a <span class="math inline">\(d\)</span>-regular HST.</p>

<h2>The “superincreasing” metric</h2>

We will now consider a highly unbalanced family of HSTs.  These were analyzed
in a paper of [Karloff, Rabani, and Ravid](https://epubs.siam.org/doi/pdf/10.1137/S0097539792224838).

<p>Let us define the trees <span class="math inline">\(\{T_n\}\)</span> as follows: The root <span class="math inline">\(r_{n}\)</span> of <span class="math inline">\(T_n\)</span> has two children. The left child is a copy of <span class="math inline">\(T_{n-1}\)</span> of rooted at <span class="math inline">\(r_{n-1}\)</span>, and the right child is a single leaf. We denote <span class="math inline">\(w_n(r_n)=1\)</span>, and <span class="math inline">\(w_n(r_{n-1}) = 1/\tau_n\)</span>, where <span class="math inline">\(\tau_n &gt; \tau_{n-1} &gt; \cdots &gt; 0\)</span> is a sequence of positive weights we will choose soon, and such that <span class="math inline">\(\tau_n \leq O(\log n)\)</span>.</p>
<p>The basic structure of our argument will be similar to the <span class="math inline">\(d\)</span>-regular case. We do the following <span class="math inline">\(2 \mu_n\)</span> times: Choose <span class="math inline">\(i \in \{L,R\}\)</span> uniformly at random. If <span class="math inline">\(i=L\)</span>, we play a height-<span class="math inline">\((n-1)\)</span> cost sequence on the left subtree (scaled by <span class="math inline">\(1/\tau_n\)</span>). Otherwise, we play <span class="math inline">\(c_\ell\)</span>, where <span class="math inline">\(\ell\)</span> is the leaf constituting the right subtree.</p>
<p>Consider an online algorithm. If the algorithm sits in the left subtree when <span class="math inline">\(i=L\)</span>, then either the algorithm moves out of the subtree (movement cost <span class="math inline">\(1\)</span>), or it incurs the cost of a height-<span class="math inline">\((n-1)\)</span> inductive sequence scaled by <span class="math inline">\(1/\tau_n\)</span>. If it sits in the right subtree, then it pays cost <span class="math inline">\(1\)</span> (either by moving or staying and incurring the service cost). If we choose
<span class="math inline">\(\tau_n \mathrel{\vcenter{:}}=\alpha_{n-1} \mathbb{E}[\mathrm{opt}_{n-1}]\)</span>, then such an algorithm always pays at least <span class="math inline">\(\tau_n^{-1} \alpha_{n-1} \mathbb{E}[\mathrm{opt}_{n-1}]\)</span> in any of these cases. Therefore:
</p>
<p>
\begin{equation}\label{eq:algn}
\mathbb{E}[\mathrm{alg}_n] \geq \mu_n \tau_n^{-1} \alpha_{n-1} \mathbb{E}[\mathrm{opt}_{n-1}].
\end{equation}
</p>
<p>We now bound the cost of the optimal offline algorithm. Let <span class="math inline">\(\rho_L\)</span> be the number of times <span class="math inline">\(i=L\)</span> and let <span class="math inline">\(\rho_R \mathrel{\vcenter{:}}= 2\mu_n - \rho_L\)</span>. The algorithm will always sit by default in the left subtree. If <span class="math inline">\(\rho_R=0\)</span>, it will move to the right subtree, suffer zero service cost there, and then move back to the left subtree (paying total cost <span class="math inline">\(2\)</span>). If <span class="math inline">\(\rho_R &gt; 0\)</span>, the algorithm will remain in the left subtree and play an optimal strategy for <span class="math inline">\(T_{n-1}\)</span>.</p>
<p>This yields: <span class="math display">\[\begin{aligned}
   \mathbb{E}[\mathrm{opt}_n] &amp;\leq \left(1-{\mathbb{P}}[\rho_R=0]\right) \mathbb{E}\left[\rho_L \tau_n^{-1} \mathrm{opt}_{n-1} \mid \rho_R &gt; 0\right]
   + 2 {\mathbb{P}}[\rho_R=0]  \\
   &amp;\leq (1-4^{-\mu_n}) \mu_n \tau_n^{-1} \mathbb{E}[\mathrm{opt}_{n-1}] + 2 \cdot 4^{-\mu_n}.\end{aligned}\]</span> Now choose: <span class="math display">\[\mu_n \mathrel{\vcenter{:}}=\frac{4 \tau_n}{\mathbb{E}[\mathrm{opt}_{n-1}]} = 4 \alpha_{n-1}\,.\]</span> This yields: <span class="math display">\[\mathbb{E}[\mathrm{opt}_n] \leq \left(1-\tfrac12 4^{-4 \alpha_n}\right) \mu_n \tau_n^{-1} \mathbb{E}[\mathrm{opt}_{n-1}].\]</span></p>
<p>Combined with \eqref{eq:algn}, we have
<span class="math display">\[\alpha_n \geq \frac{\mathbb{E}[\mathrm{alg}_n]}{\mathbb{E}[\mathrm{opt}_n]} \geq \alpha_{n-1} + \tfrac12 4^{-4\alpha_{n-1}}.\]</span> This implies that <span class="math inline">\(\alpha_n \geq \beta \log n\)</span> for some positive <span class="math inline">\(\beta &lt; 1\)</span>. (To see this observe, that if <span class="math inline">\(f(x)=\beta \log x\)</span>, then <span class="math inline">\(f'(x) = \beta/x &lt; \frac12 4^{-4 \beta \log x}\)</span> for <span class="math inline">\(\beta\)</span> chosen small enough.)</p>
<p>Note furthermore that <span class="math display">\[\mathbb{E}[\mathrm{opt}_n] \leq 4\,,\]</span> and therefore <span class="math inline">\(\tau_n \leq O(\log n)\)</span>.</p>

<h2>The general case</h2>

<p>We have demonstrated lower bounds in two cases: When the underlying tree <span class="math inline">\(T\)</span> is regular, and when it is unbalanced and binary. The general case can be proved by combining these two strategies along any <span class="math inline">\(\Omega((\log n)^2)\)</span>-HST. The next lemma contains the basic idea. We leave it to the reader as a basic exercise. (Hint: Use the concavity of <span class="math inline">\(x \mapsto \sqrt{x}\)</span>.)</p>
<p class="lemma">
Suppose that <span class="math inline">\(n=n_1+n_2+\cdots+n_m\)</span> where <span class="math inline">\(n_1 \geq n_2 \geq \cdots \geq n_m \geq 1\)</span>. Then either <span class="math inline">\(\sqrt{n_1}+\sqrt{n_2} \geq \sqrt{n}\)</span>, or there is some <span class="math inline">\(\ell \geq 3\)</span> such that <span class="math inline">\(\ell \cdot \sqrt{n_\ell} \geq \sqrt{n}\)</span>.</p>

<p>Suppose now that <span class="math inline">\(T\)</span> is a rooted tree with subtrees <span class="math inline">\(T_1, T_2, \ldots, T_m\)</span> beneath the root, and such that <span class="math inline">\(T_i\)</span> has <span class="math inline">\(n_i\)</span> leaves with <span class="math inline">\(n_1 \geq n_2 \geq \cdots \geq n_m \geq 1\)</span>. The lemma says we can either consider only the first two subtrees (the binary, possibly “unbalanced” case), or we can take the first <span class="math inline">\(\ell\)</span> subtrees for some <span class="math inline">\(\ell \geq 3\)</span>, prune them so they all have exactly <span class="math inline">\(n_\ell\)</span> leaves, and then prove a lower bound. Analyzing these two cases correspond roughly to the two lower bound arguments above.</p>
