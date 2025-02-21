---
title: 均值方差均衡策略学习
date: 
    created: 2024-10-16
    updated: 2024-10-22
authors: 
  - zzh
categories:
  - Reinforcement Learning
draft: true
---

# Learning Equilibrium Mean-Variance Strategy

模板
<!-- more -->

**Autor：** Min DAI, Yuchao DONG, and Yanwei JIA


## 2 模型设置

### 2.1 市场环境

假设有两种资产可供投资：

* 无风险资产 (bond)：利率 $r$
* 风险资产 (stock)：股票价格服从

\begin{equation}
    \frac{\mathrm{d} S_{t}}{S_{t}}=\mu_{t} \mathrm{~d} t+\sigma_{t} \mathrm{~d} B_{t},
\end{equation}

:   * $B_t$ 是一个标量布朗运动
:   * $\mu_t$ 和 $\sigma_t$ 依赖随机市场状态 $X_t$

进一步假设 $X_t$ 是一个扩散过程，满足

\begin{equation}
    \mathrm{d} X_{t}=m_{t} \mathrm{~d} t+\nu_{t}\left[\rho \mathrm{~d} B_{t}+\sqrt{1-\rho^{2}} \mathrm{~d} \tilde{B}_{t}\right],
\end{equation}

:   * $\rho$ 是一个常数
:   * $\tilde{B}_{t}$ 是另一个标量布朗运动，与 $B_t$ 是独立的



假设 $\mu_{t} \equiv \mu\left(t, X_{t}\right), \sigma_{t} \equiv \sigma\left(t, X_{t}\right), m_{t} \equiv m\left(t, X_{t}\right), \text { and } \nu_{t} \equiv \nu\left(t, X_{t}\right)$ 都是确定性的函数，
尽管我们不知道他们是什么。

一个自融资的财富过程 $W_t$ 可以被表述如下：

\begin{equation*}
    \frac{d W_{t}}{W_{t}}=\left[r+\left(\mu_{t}-r\right) u_{t}\right] d t+\sigma_{t} u_{t} d B_{t},
\end{equation*}

:   * $u_t$ 表示在 $t$ 时刻投资于股票的总财富占比，是一个标量适应过程，可以看做是一种策略

??? Notes
    \[u_t = \frac{S_t}{W_t}\]

    \begin{align*}
        d W_{t} & =W_{t} u_{t} d S_{t}+\left(W_{t}-W_{t} u_{t}\right) r d t \\
        \frac{d W_{t}}{W_{t}} & =u_{t} d S_{t}+\left(1-u_{t}\right) r d t \\
        & =u_{t} (\mu_{t} d t+ \sigma_{t} d B_{t})+\left(1-u_{t}\right) r d t \\
        & =\left[r+\left(\mu_{t}-r\right) u_{t}\right] d t+ \sigma_{t} u_{t} d B_{t}
    \end{align*}

为方便后续使用，在此处引入投资组合的 log return process $R_t = log ~W_t$，满足：

\begin{equation}
    \mathrm{d} R_{t}=\left[r_{t}+\left(\mu_{t}-r_{t}\right) u_{t}-\frac{1}{2} \sigma_{t}^{2} u_{t}^{2}\right] \mathrm{d} t+\sigma_{t} u_{t} \mathrm{d} B_{t} .
\end{equation}
    
??? Notes
    \[d R_{t}=\frac{d W_{t}}{W_{t}}-\frac{1}{2 W_{t}^{2}}\left(d W_{t}\right)^{2}\]

### 2.2 带探索项的投资组合回报过程

设 $T$ 为投资期限，回忆 Dai 等人在2020年提出的动态均值方差准则——投资组合 $R_t$ log return 的均值和方差间的 trade-off，即：

\[\mathbb{E}_{t}\left[R_{T}\right]-\frac{\gamma}{2} \operatorname{Var}_{t}\left[R_{T}\right]\]

:   * $\mathbb{E}_{t}[\cdot]$ 和 $\operatorname{Var}_{t}[\cdot]$ 分别代表在 $t$ 时刻的条件期望和方差。
:   * $\gamma$ 衡量均值和方差间的 trade-off。

该准则可以得到符合一般投资智慧的解析均衡策略。本文将学习(即 exploration) 纳入到均值-方差公式。  

将策略过程 $u_t$ 随机化，得到一个分布策略过程，其密度函数为 $\left\{\pi_{t}, 0 \leq t \leq T\right\}$

由于我们建立的市场涉及市场状态 $X_t$ ，因此，与分布策略过程有关的投资组合收益过程的“探索”版本要与 Wang 等人在2019年的文章不同。
为了给出直觉上动态过程应该是如何的，让我们考察 $t$ 时刻离散时间情形：

\[\Delta R_{t}=\left[r+(\mu-r) u-\frac{1}{2} \sigma^{2} u^{2}\right] \Delta t+\sigma u \Delta B_{t}\]

让 $u$ 从一个独立的分布 $\pi$ 中采样，考虑以下的增量：

\begin{align*}
    \tilde{\Delta}:= & \left[r+(\mu-r) \int_{\mathbb{R}} u \pi(d u)-\frac{1}{2} \sigma^{2} \int_{\mathbb{R}} u^{2} \pi(d u)\right] \Delta t \\
    & +\sigma \int_{\mathbb{R}} u \pi(d u) \Delta B_{t} +\sqrt{\int_{\mathbb{R}} u^{2} \pi(d u)-\left(\int_{\mathbb{R}} u \pi(d u)\right)^{2} \Delta \bar{B}_{t}}
\end{align*}

其中 $\bar{B}_{t}$ 是另一个布朗运动。对上述增量取期望和方差，如下：

\begin{align*}
    \mathbb{E}[\tilde{\Delta}] & =\left[r+(\mu-r) \int_{\mathbb{R}} u \pi(d u)-\frac{1}{2} \sigma^{2} \int_{\mathbb{R}} u^{2} \pi(d u)\right] \Delta t, \\
    \operatorname{Var}[\tilde{\Delta}] & =\sigma^{2} \int_{\mathbb{R}} u^{2} \pi(d u) \Delta t+o(\Delta t), \quad \operatorname{Cov}\left[\tilde{\Delta}, \Delta X_{t}\right]=\rho \nu \sigma \int_{\mathbb{R}} u \pi(d u) \Delta t+o(\Delta t) .
\end{align*}

容易看出 $\tilde{\Delta}$ 在一阶矩和二阶矩上近似 $\Delta R_{t}$。

&emsp;&emsp;受上述观察启发，将对数回报 $\mathrm{d}R_t$ (3)式替换为以下过程，该过程与由 $\pi$ 刻画的随机策略有关，并将用于探索性的均值-方差公式：

\begin{equation}
    \begin{aligned}
        \mathrm{d} R_{t}^{\pi}= & {\left[r+\left(\mu_{t}-r\right) \int_{\mathbb{R}} u \pi_{t}(\mathrm{d} u)-\frac{1}{2} \sigma_{t}^{2} \int_{\mathbb{R}} u^{2} \pi_{t}(\mathrm{d} u)\right] \mathrm{d} t } \\
        & +\sigma_{t}\left[\int_{\mathbb{R}} u \pi_{t}(\mathrm{d} u) \mathrm{d} B_{t}+\sqrt{\int_{\mathbb{R}} u^{2} \pi_{t}(\mathrm{d} u)-\left(\int_{\mathbb{R}} u \pi_{t}(\mathrm{d} u)\right)^{2} } \mathrm{d}\bar{B}_{t}\right],
    \end{aligned}
\end{equation}

其中 $\bar{B}_t$ 是另一个与 $B_t$ 和 $\tilde{B}_{t}$ 相互独立的布朗运动。

??? tip

    &emsp;&emsp;(4) 式刻画了策略对投资组合收益过程的影响。  
    &emsp;&emsp;在一个完备的市场中，即 $\mu_t$ 和 $\sigma_t$ 不依赖市场状态 $X_t$ ，可以将 (4) 式中的两个布朗运动合并为一个布朗运动，从而恢复成 Wang 等人给出的公式。  
    &emsp;&emsp;在一个不完备的市场中，(4) 式涉及一个新的布朗运动 $\bar{B}_t$。  
    &emsp;&emsp;直观的说，(4) 式和 (2) 式中的 $B_t$ 和 $\tilde{B}_t$ 用于建模市场噪声，而 $\bar{B}_t$ 用于建模探索引起的噪声，可以看做是投资组合用来产生随机策略的“随机数生成器”。  
    &emsp;&emsp;$\mathrm{d}\bar{B}_t$ 项的系数反映了 $\pi_t$ 的方差，衡量了系统引入了多少额外的噪声。
 
### 2.3 熵正则化均值方差问题

在 $R_t^{\pi}$ 熵的均值-方差准则中加入熵正则项，得到如下奖励泛函：

\begin{equation}
    J\left(t, R_{t}^{\pi}, X_{t} ; \pi\right):=\mathbb{E}_{t}\left[R_{T}^{\pi}+\lambda \int_{t}^{T} H\left(\pi_{s}\right) d s\right]-\frac{\gamma}{2} \operatorname{Var}_{t}\left[R_{T}^{\pi}\right] .
\end{equation}

:   * $R_t^{\pi}$ 和 $X_t$ 各自服从 (4) 式和 (2)式
:   * $\lambda$ 代表探索权重
:   * $H$ 是策略分布的熵，定义如下：

\[
H(\pi)=\left\{\begin{array}{l}
    -\int_{\mathbb{R}} \pi(u) \log \pi(u) d u, \text { if } \pi(d u)=\pi(u) d u \\
    -\infty, \text { otherwise. }
    \end{array}\right.
\]

在求解熵正则化均值方差问题之前，我们首先要定义两个概念，容许的反馈控制和均衡策略。

***
#### Definition 1.

$\pi=\{\pi_s,t\leq s\leq T \}$ is called an **admissible feedback control**, if

(1) for each $t\leq s \leq T$ ,  $\pi_s \in \mathcal{P}(\mathbb{R})$ a.s., where $\mathcal{P}(\mathbb{R})$ stands for all probability measures on the real numbers;  
(2) $\pi_s = \pi(s,R_s,X_s)$, where $\pi(\cdot,\cdot,\cdot)$ is a deterministic mapping from $[t,T]\times \mathbb{R}\times\mathbb{R}$ to $\mathcal{P}(\mathbb{R})$;  
(3) $\mathbb{E}_{t}\left[\int_{t}^{T} \int_{\mathbb{R}}\left|\sigma_{s} u\right|^{2} \pi_{s}(d u) d s\right]+\mathbb{E}_{t}\left[\int_{t}^{T} \int_{\mathbb{R}}\left|\mu_{s} u\right| \pi(d u) d s\right]<\infty$

The collection of all the admissible controls in the feedback form at time $t$ is denoted as $\Pi_t$.  
***

***
#### Definition 2.

An admissible control $\pi^*$ is called an equilibrium policy, if, at any time $t$, for any perturbation control $\pi^{h,v}$ defined by  

\[
    \pi_{\tau}^{h, v}=\left\{\begin{array}{c}
        v, \text { for } t \leq \tau \leq t+h \\
        \pi_{\tau}^{*}, \text { for } t+h \leq \tau \leq T
        \end{array}\right.
\]

with any $h\in \mathbb{R}^+$ and $v\in\mathcal{P}(\mathbb{R})$, the entropy-regularized mean-variance functional is locally better off, namely  

\[
    \liminf _{h \rightarrow 0^{+}} \frac{J\left(t, R_{t}, X_{t} ; \pi^{*}\right)-J\left(t, R_{t}, X_{t} ; \pi^{h, v}\right)}{h} \geq 0 .
\]

Furthermore, for an equilibrium control $\pi^*$, the equilibrium value function $V^*$ is defined as

\[
    V^{*}\left(t, R_{t}, X_{t}\right):=J\left(t, R_{t}, X_{t} ; \pi^{*}\right) .
\]
***

均衡策略是一种在任何时候都是局部最优的策略。这与经济学中的动态博弈中的子博弈完美纳什均衡是一致的。

## 3. 均衡策略

本节给出了在一般不完全市场下的均衡解。

定理1 证明了在温和条件，一般存在一个半解析的均衡策略。

***
### Theorem 1.

Assume that $\mathbb{E}\left[\int_{0}^{T} \theta_{s}^{2} d s\right]$ and $\mathbb{E}\left[e^{\frac{\gamma^{2}}{1+\gamma^{2}}\left(\int_{0}^{T}\left(r_{t}+\theta^{2} / 2\right) d t+\int_{0}^{T} \theta_{t} / \rho d B_{t}^{X}\right.}\right]<\infty,$ where $\theta_t = \theta\left(t, X_{t}\right)=\frac{\mu\left(t, X_{t}\right)-r}{\sigma\left(t, X_{t}\right)}$ and $d B_{t}^{X}=\rho d B_{t}+\sqrt{1-\rho^{2}} d \tilde{B}_{t} .$ Then, we have the following results:

:  (i) An equilibrium policy is given by

\begin{equation}
    \pi^{*}(t, X) \sim \mathcal{N}\left(\frac{\mu_{t}-r_{t}}{(1+\gamma) \sigma_{t}^{2}}-\frac{\rho \gamma Z_{t}}{(1+\gamma) \sigma_{t}}, \frac{\lambda}{(1+\gamma) \sigma_{t}^{2}}\right),
\end{equation}

:  where $Z_t$ is uniquely determined by the following backward stochastic differential eqation(BSDE):

\begin{equation}
    d Y_{t}=-f\left(t, X_{t}, Z_{t}\right) d t+Z_{t} d B_{t}^{X}, \quad Y_{T}=0
\end{equation}

:  with $f(t, X, Z)=r-\frac{\lambda}{2(1+\gamma)}+\frac{1}{2} \theta^{2}(t, X)-\frac{\gamma^{2}(\theta(t, X)+\rho Z)^{2}}{2(1+\gamma)^{2}} .$

:  (ii) There exists a deterministic function $h(\cdot,\cdot)$ such that $Y_t = h(t, X_t)$. Moreover, if $h\in C^{1,2}$, then $h$ solves the following partial differential equation (PDE):

\begin{equation}
    \partial_{t} h+m \partial_{X} h+\frac{1}{2} \nu^{2} \partial_{X X} h+f\left(t, X, \nu \partial_{X} h\right)=0, \quad h(T, X)=0
\end{equation}

:  and $Z_{t}=\nu \partial_{x} h\left(t, X_{t}\right).$

:  (iii) Under the equilibrium policy (6), we have

\begin{equation}
    \begin{array}{l}
        V^{*}(t, R, X) \equiv J\left(t, R, X ; \pi^{*}\right)=U^{*}(t, X)+R; \\
        g^{*}(t, R, X) \equiv \mathbb{E}_{t}\left[R_{T}^{\pi^{*}} \mid R_{t}^{\pi^{*}}=R, X_{t}=X\right]=h^{*}(t, X)+R .
        \end{array}
\end{equation}

:  for some function $h^*$ and $U^*$ with $h^{*}(T, X)=U^{*}(T, X)=0 .$ Moreover, if $h^*, U^* \in C^{1,2}$, then $h^*$ satisfies (8) and $U^*$ satisfies

\begin{equation}
    \partial_{t} U+m \partial_{X} U+\frac{1}{2} \nu^{2} \partial_{X X} U+r+\frac{\left(\mu-r-\rho \gamma \nu \sigma \partial_{X} h^{*}\right)^{2}}{2(1+\gamma) \sigma^{2}}+\frac{1}{2} \log \frac{2 \pi \lambda}{(1+\gamma) \sigma^{2}}-\frac{\gamma}{2} \nu^{2}\left|\partial_{X} h^{*}\right|^{2}=0 .
\end{equation}

***

!!! Note
    * 上述定理指出在温和正则条件下，可以通过求解BSDE来构造均衡策略。  
    * 即使是在不完全市场，探索的均衡策略的分布仍然是 Gaussian。
    * 探索策略的均值与探索权重 $\lambda$ 无关，表明了探索与利用是分离的。

#### 定理1的应用

考虑时间变化的高斯均值回报模型 (time varying Gaussian mean return model)，即：

\begin{equation*}
    \mu(t, X)=r+\sigma X, \sigma(t, X)=\sigma, m(t, X)=\iota(\bar{X}-X) \text { and } \nu(t, X)=\nu,
\end{equation*}

:  其中 $r, \sigma, \iota,  \bar{X} , \nu$ 都是正的常数。

下面的命题表明该模型存在一个封闭形式的均衡解

***
### Proposition 1.

For the Gaussian mean return model, an equilibrium strategy is

\begin{equation}
    \pi^{*}(t, X) \sim \mathcal{N}\left(\frac{X}{(1+\gamma) \sigma}-\frac{\gamma \rho \nu}{(1+\gamma) \sigma}\left(a_{2}^{*}(t) X+a_{1}^{*}(t)\right), \frac{\lambda}{(1+\gamma) \sigma^{2}}\right)
\end{equation}

with

\begin{equation}
    \left\{\begin{array}{l}
        a_{2}^{*}(t)=\frac{(1+2 \gamma)}{(1+\gamma)^{2}} \frac{e^{2 C_{1}(T-t)}-1}{\left(C_{1}+C_{2}\right)\left(e^{2 C_{1}(T-t)}-1\right)+2 C_{1}} \\
        a_{1}^{*}(t)=\frac{\iota \bar{X}(1+2 \gamma)}{(1+\gamma)^{2}} \frac{\left(e^{C_{1}(T-t)}-1\right)^{2}}{C_{1}\left[\left(C_{1}+C_{2}\right)\left(e^{2 C_{1}(T-t)}-1\right)+2 C_{1}\right]},
        \end{array}\right.
\end{equation}

where $C_{1}=\frac{1}{\gamma+1}\left[\gamma^{2}(\iota+\rho \nu)^{2}+\iota^{2}(2 \gamma+1)\right]^{\frac{1}{2}}$ and $C_{2}=\iota+\frac{\gamma^{2} \rho \nu}{(1+\gamma)^{2}} .$

&emsp;Moreover, the associated $V^*$ and $g^*$ have the following form:

\begin{equation}
    \begin{array}{l}
        V^{*}(t, R, X)=R+\frac{1}{2} b_{2}^{*}(t) X^{2}+b_{1}^{*}(t) X+b_{0}^{*}(t), \\
        g^{*}(t, R, X)=R+\frac{1}{2} a_{2}^{*}(t) X^{2}+a_{1}^{*}(t) X+a_{0}^{*}(t)
        \end{array}
\end{equation}

where $a_2^*(t)$ and $a_1^*(t)$ are as given by (12), and $a_0^*(t)$, $b_1^*(t)$, and $b_2^*(t)$ are given in E-Companion (EC.13) and (EC.14).

***

## 4. 数值方法

在标准的 RL 算法中，一个学习过程通常包含两个迭代步骤：

1. 给定策略 $\pi$，计算对应的值函数 $V^{\pi}$;
2. 根据获得值函数 $V^\pi$ 去更新先前的策略 $\pi$ 为一个新的策略 $\tilde{\pi}$。

因此，我们需要去考虑两个问题：

**Q1.** 可行策略对应的值函数 $V^\pi$ 是什么?    (Policy Evaluation)  
**Q2.** 更新策略的准则是什么？  (Policy Update)

定义一些函数  

* $\pi_t = \pi(t,R_t,X_t)$ 为容许策略。  
* $V^{\pi}(t,R_t,X_t) = J(t,R_t^{\pi},X_t;\pi)$ 为策略 $\pi$ 对应的值函数。  
* $g^\pi(t,R,X):=\mathbb{E}_t[R_T^\pi|R_t^\pi = R, X_t = X]$ 是一个辅助值函数。

在E-Companion EC.5给出的确定的正则条件下，$(V^\pi,g^\pi)$ 会满足如下的PDE系统：

\begin{equation}
    \partial_{t} V^{\pi}+\mathcal{A}_{t}^{\pi} V^{\pi}+\gamma g^{\pi} \mathcal{A}_{t}^{\pi} g^{\pi}-\frac{\gamma}{2} \mathcal{A}_{t}^{\pi}\left(g^{\pi}\right)^{2}+\lambda H\left(\pi_{t}\right)=0, \quad V^{\pi}(T, R, X)=R,
\end{equation}

\begin{equation}
    \partial_{t} g^{\pi}+\mathcal{A}_{t}^{\pi} g^{\pi}=0, \quad g^{\pi}(T, R, X)=R,
\end{equation}

差分算子 $\mathcal{A}_{t}^{u}$,  $\forall u\in \mathbb{R}$ 和 $\mathcal{A}_{t}^{\pi}$, $\forall \pi\in \mathcal{P}(\mathbb{R})$ 定义如下：

\begin{equation}
    \begin{aligned}
        \mathcal{A}_{t}^{u} \varphi(t, R, X):= & {\left[r+(\mu(t, X)-r) u-\frac{1}{2} \sigma^{2}(t, X) u^{2}\right] \partial_{R} \varphi+m(t, X) \partial_{X} \varphi } \\
        & +\frac{1}{2} \sigma^{2}(t, X) u^{2} \partial_{R R} \varphi+\rho \nu(t, x) \sigma(t, x) u \partial_{R X} \varphi+\frac{1}{2} \nu^{2}(t, X) \partial_{X X} \varphi \\
         \mathcal{A}_{t}^{\pi} \varphi:=&\int_{\mathbb{R}} \mathcal{A}_{t}^{u} \varphi \pi(d u)
        \end{aligned}
\end{equation}

使用上述的记号，均衡条件变为

\begin{equation}
    \pi^{*}(t, R, X)=\underset{\pi \in \mathcal{P}(\mathbb{R})}{\operatorname{argmax}} \mathcal{A}_{t}^{\pi} V^{*}+\gamma g^{*} \mathcal{A}_{t}^{\pi} g^{*}-\frac{\gamma}{2} \mathcal{A}_{t}^{\pi}\left(g^{*}\right)^{2}+\lambda H(\pi),
\end{equation}

其中 $V^* = V^{\pi^*}$ 和 $g^* = g^{\pi^*}$

(14)(15)式回答了Q1。(16)式回答了Q2。

因此我们可以提出均衡策略的学习过程，如下：

* **Policy Evaluation Procedure:** given a policy $\pi$, compute the related value function

\begin{equation*}
    V^{\pi}\left(t, R_{t}, X_{t}\right):=J\left(t, R_{t}, X_{t} ; \pi\right)
\end{equation*}

and expectation function $g^{\pi}\left(t, R_{t}, X_{t}\right):=\mathbb{E}_{t}\left[R_{T}^{\pi} \mid R_{t}, X_{t}\right] ;$

* **Policy Update Procedure:** obtain a new policy $\tilde{\pi}$ according to optimality condition (17) with $(V^\pi,g^\pi)$ in place of $(V^*,g^*)$, i.e.

\begin{equation*}
    \tilde{\pi}(t, x)=\underset{v \in \mathcal{P}(\mathbf{R})}{\operatorname{argmax}} \mathcal{A}_{t}^{v} V^{\pi}+\gamma g^{\pi} \mathcal{A}_{t}^{v} g^{\pi}-\frac{\gamma}{2} \mathcal{A}_{t}^{v}\left(g^{\pi}\right)^{2}+\lambda H(v) .
\end{equation*}

