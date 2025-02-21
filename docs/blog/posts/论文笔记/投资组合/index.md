---
title: 离散时间马尔科夫时间不一致的随即控制理论
date: 
    created: 2024-10-30
    updated: 2024-10-30
authors: 
  - zzh
categories:
  - portfolio selection
draft: true
---

# A theory of Markovian time-inconsistent stochastic control in discrete time

模板
<!-- more -->

**Autor：** Tomas Björk · Agatha Murgoci


## 2 设置

### 2.1 设置

一些记号上的声明

* $X$ 受控的马尔可夫过程，$(\mathcal{X},\mathcal{G}_X)$ 可测的状态空间
* 控制取值的可测控制空间 $(\mathcal{U},\mathcal{G}_U)$
* 离散时间的动作，以自然数集合 $\mathbb{N}$ 为索引
* 如果 $X_n = x$，那么就选择控制 $u_n\in \mathcal{U}$，并且该控制会影响 $X_n \rightarrow X_{n+1}$ 的转移概率，其转移概率族表示如下：

\begin{equation*}
    \left\{p_{n}^{u}(d z ; x): n \in \mathbb{N}, x \in \mathcal{X}, u \in \mathcal{U}\right\} .
\end{equation*}

对于每一个固定的 $n\in \mathbb{N}, x\in\mathcal{X}$ 和 $u\in \mathcal{U}$，假定 $p_n^u(\cdot;x)$ 是 $mathcal{X}$ 上的概率测度。
并且对每一个 $A\in\mathcal{G}_X$ ，概率 $p_n^u(A;x)$ 在 $(x,u)$ 上是联合可测的。

$p_n^u(dz;x)$ 是在给定 $X_n = x$ 且在时间 $n$ 采用控制 $u$ 得到的 $X_{n+1}$ 概率分布。

\begin{equation*}
    p_{n}^{u}(d z ; x)=P\left[X_{n+1} \in d z \mid X_{n}=x, u_{n}=u\right] .
\end{equation*}

约束控制为反馈控制律，以得到马尔可夫结构。也就是说，在时间 $n$，控制 $u_n$ 可以依赖于与时间 $n$ 的状态 $X_n$。

\begin{equation*}
    u_{n}=\mathbf{u}_{n}\left(X_{n}\right),
\end{equation*}

* $\mathbf{u}: \mathbb{N} \times \mathcal{X} \rightarrow \mathcal{U}$ 是可测的

> 字体加粗代表映射，反之则表示一个可能的取值  
$\mathbf{u}_n: \mathcal{X} \rightarrow \mathcal{U}$  
$u\in \mathcal{U}$


:  给定转移概率族，定义一个作用在函数序列上的算子族。
***
#### Definition 2.2

A function sequence is a mapping $f : \mathbb{N} \times \mathcal{X} \rightarrow \mathbb{R}$, where we use the notation $(n, x) \mapsto f_{n}(x)$ .

- For each $u \in \mathcal{U}$ , the operator $\mathbf{P}^u$, acting on the set of integrable function sequences, is defined by

\begin{equation*}
    \left(\mathbf{P}^{u} f\right)_{n}(x):=\int_{\mathcal{X}} f_{n+1}(z) p_{n}^{u}(d z, x) 
\end{equation*}

:  The corresponding discrete-time “infinitesimal operator” $\mathbf{A}^u$ is defined by

\begin{equation*}
    \mathbf{A}^{u}=\mathbf{P}^{u}-\mathbf{I},
\end{equation*}

:  where $\mathbf{I}$ is the identity operator.

- For each control law $\mathbf{u}$, the operator $\mathbf{P^u}$ is defined by

\begin{equation*}
    \left(\mathbf{P}^{\mathbf{u}} f\right)_{n}(x):=\int_{\mathcal{X}} f_{n+1}(z) p_{n}^{\mathbf{u}_{n}(x)}(d z, x),
\end{equation*}

:  and $\mathbf{A^u}$ is defined correspondingly as

\begin{equation*}
    \mathbf{A}^{\mathbf{u}}=\mathbf{P}^{\mathbf{u}}-\mathbf{I} .
\end{equation*}
***

以概率论的记号，可以将算子表示为

\begin{equation*}
    \left(\mathbf{P}^{u} f\right)_{n}(x)=E\left[f_{n+1}\left(X_{n+1}\right) \mid X_{n}=x, u_{n}=u\right]
\end{equation*}

或者做一些简写

\begin{equation*}
    \left(\mathbf{P}^{u} f\right)_{n}(x)=E_{n, x}\left[f_{n+1}\left(X_{n+1}^{u}\right)\right],
\end{equation*}

$A^u$ 是连续时间无穷小算子的离散时间版本。

> \begin{flalign*}
    \left(\mathbf{A}^{u} f\right)_{n}(x) & = E_{n, x}\left[f_{n+1}\left(X_{n+1}^{u}\right)\right]-f_n(x) & \\
    &=E_{n, x}\left[f_{n+1}\left(X_{n+1}^{u}\right) - f_n(x)\right] &
  \end{flalign*}

***
#### Proposition 2.3

Consider a real-valued function sequence $(f_n(x))$ and a control law $\mathbf{u}$. 
The process $(f_n(X_n^\mathbf{u}))$ is then a **martingale** under the measure induced by $\mathbf{u}$ 
**if and only if** the following conditions are satisfied:

\- The process $(f_n(X_n^{\mathbf{u}}))$ is integrable.  
\- The sequence $(f_n)$ satisfies the equation

\begin{equation*}
    \left(\mathbf{A}^{\mathbf{u}} f\right)_{n}(x)=0, \quad n=0,1, \ldots, T-1
\end{equation*}
***

### 2.2 基本问题公式化

* a fixed $(n,x)\in\mathbb{N} \times \mathcal{X}$
* a fixed control law $\mathbf{u}=\left\{\mathbf{u}_{0}, \mathbf{u}_{1}, \ldots, \mathbf{u}_{T-1}\right\}$
* a fixed time horizon $T$

考虑一个基本形式的泛函

\begin{equation*}
    J_{n}(x, \mathbf{u})=E_{n, x}\left[\sum_{k=n}^{T-1} C\left(x, X_{k}^{\mathbf{u}}, \mathbf{u}_{k}\left(X_{k}^{\mathbf{u}}\right)\right)+F\left(x, X_{T}^{\mathbf{u}}\right)\right]+G\left(x, E_{n, x}\left[X_{T}^{\mathbf{u}}\right]\right).
\end{equation*}

直觉上，我们在 $(n,x)$ 选择一个能够最大化 $J$ 的控制律 $\mathbf{u}$，定义一个问题族 $(\mathcal{P}_{n,x})$ 如下：

\begin{equation*}
    \mathcal{P}_{n, x}: \quad \max _{\mathbf{u}} J_{n}(x, \mathbf{u}),
\end{equation*}

### 2.3 博弈论公式化

***
#### Definition 2.5

We consider a fixed control law $\hat{\mathbf{u}}$ and make the following construction:

1. Fix an arbitrary point $(n, x)$, where $n<T$, and choose an arbitrary control value $u\in \mathcal{U}$.  
2. Now define the control law $\mathbf{u}^{u,n}$ on the time set $\{n, n + 1,\dots,T - 1\}$ by setting, for any $y \in \mathcal{X}$,

\begin{equation*}
    \mathbf{u}_{k}^{u, n}(y)=\left\{\begin{array}{ll}
        \hat{\mathbf{u}}_{k}(y) & \text { for } k=n+1, \ldots, T-1, \\
        u & \text { for } k=n .
        \end{array}\right.
\end{equation*}

We say that $\hat{\mathbf{u}}$ is a subgame perfect Nash *equilibrium* strategy if for every fixed $(n, x)$, we have

\begin{equation*}
    \sup _{u \in \mathcal{U}} J_{n}\left(x, \mathbf{u}^{u, n}\right)=J_{n}\left(x, \hat{\mathbf{u}}_{n}\right) .
\end{equation*}

If an equilibrium control $\hat{\mathbf{u}}$ exists, we define the *equilibrium value function* $V$ by

\begin{equation*}
    V_{n}(x):=J_{n}(x, \hat{\mathbf{u}}) .
\end{equation*}
***

> 一种等价的，更具体的描述均衡策略的方式如下：  
&emsp;\- 在 $T-1$ 时刻优化 $J_{T-1}(x,\mathbf{u})$ ，得到均衡控制 $\hat{\mathbf{u}}_{T-1}(x)$  
&emsp;\- 在给定 $T-1$ 时刻选择均衡策略 $\hat{\mathbf{u}}_{T-1}$ 的情况下，优化 $T-2$ 时刻的 $J_{T-2}$，得到 $\hat{\mathbf{u}}_{T-2}(x)$   
&emsp;\- 逆向的数学归纳法

## 3. 扩展到贝尔曼方程

在本节中，假设存在一个均衡控制律 $\hat{\mathbf{u}}$ (可能不是唯一的)，并考虑对应的均衡值函数 $V$。
本节的目标是推导处一个方程组，扩展标准的Bellman方程，用于确定 $v$。主要通过以下两个步骤完成：

:  1. 对于任意的选取的控制律 $\mathbf{u}$，推导出 $J_n(x,\mathbf{u})$ 的递归方程。
2. 固定 $(n,x)$，考虑两种控制律，一种是均衡控制律 $\hat{\mathbf{u}}$，另一种是在时刻 $n$ 任意选取控制律 $u=\mathbf{u}_n(x)$，但是在 $[n+1,T-1]$ 内是服从均衡控制 $\hat{\mathbf{u}}$。

\begin{equation*}
    \sup _{u \in \mathcal{U}} J_{n}(x, \mathbf{u})=J_{n}(x, \hat{\mathbf{u}})=V_{n}(x)
\end{equation*}

### 3.1 简化问题

