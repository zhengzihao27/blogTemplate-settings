---
title: 毕业设计
date: 
    created: 2024-10-22
    updated: 2024-10-22
authors: 
  - zzh
categories:
  - git
draft: true
---

# 毕业设计

模板
<!-- more -->

**Autor：** 模板


## 2 模板
* 2.1 市场环境
* 2.2 离散时间探索性的均值方差问题

### 2.1 市场环境

首先考虑由两个资产组成的市场：

* 无风险资产，回报率 $r$
* 风险资产，t到t+1的超额回报率 $r_t$

设 $T$ 为投资期限，$u_t$ 是分配在风险资产的资金份额，考虑动态均值-方差准则的优化问题，投资组合 $X_t$ 的均值和方差间的 trade-off 即：

\[\mathbb{E}_{t}\left[X_{T}\right]-\frac{\gamma}{2} \operatorname{Var}_{t}\left[X_{T}\right]\]

:   * $\mathbb{E}_{t}[\cdot]$ 和 $\operatorname{Var}_{t}[\cdot]$ 分别代表在 $t$ 时刻的条件期望和方差。
:   * $\gamma$ 衡量均值和方差间的 trade-off。
:   * $X_{t+1} = r_f X_t + r_t u_t$

### 2.2 离散时间探索性的均值方差问题

在强化学习框架中，随机化策略过程 $\mathbf{u} = \{u_t,0\le t <T\}$，得到一个分布策略过程，其密度函数为 $\boldsymbol{\pi} = \{\pi_t,0\le t < T\}$.

---
Notation:

$\boldsymbol{\pi} : \mathbb{N}\times\mathcal{X} \rightarrow\mathcal{P}(\mathcal{\mathcal{U}})$

* $\mathcal{X}$ 是状态空间，$\mathcal{U}$ 是策略空间。

* 策略 $\boldsymbol{\pi}=\{\pi_t\}_{t=0}^{T-1}$ 是马尔科夫的，只依赖于当前状态。

* $\pi_t:\mathcal{X} \rightarrow\mathbb{P}(\mathcal{\mathcal{U}})$，将当前状态 $x_t$ 映射到策略空间上的一个分布。

:   * $\pi_t(x)\in \mathcal{P}(\mathcal{U})$ 表示给定状态 $x$ 的策略分布。
:   * $\pi_t(x,u)$ 表示在状态 $x$ 采取策略 $u$ 的概率
---

因此，财富的动态过程可以表示为：

\begin{equation}
    x_{t+1}^\pi = r_f x_t^\pi + r_t u_t^\pi.
\end{equation}

更一般的，$x_T$ 可以表示成：

\begin{equation}
    x_{T}^\pi =  r_f^{T-t} x_t^\pi + \sum_{s=t}^{T-1} r_f^{T-s-1} r_s u_s^{\pi}  .
\end{equation}

??? Notes

    \begin{aligned}
        x_{t+1}^\pi &= r_f x_t^\pi + r_t u_t^\pi \\
        x_{t+2}^\pi &= r_f x_{t+1}^\pi + r_{t+1} u_{t+1}^\pi \\
        &= r_f^{2} x_t^\pi + r_f r_t u_t^\pi + r_{t+1} u_{t+1}^\pi \\
        x_{t+3}^\pi &= r_f^3 x_t^\pi + r_f^2 r_t u_t^\pi + r_f r_{t+1} u_{t+1}^\pi + r_{t+2} u_{t+2}^\pi 
    \end{aligned}

**假定：** $\{r_t\}_{t=0}^{T-1} \text{ are i.i.d }$

* 超额收益 $r_t$ 服从一个均值为 $a$ 和方差 $\sigma^2$ 的分布。
* $u_t^\pi$ 是一个随机控制过程，概率密度为 $\pi_t$。
* $r_t$ 与 $u_t^\pi$ 是独立的。

根据假设，我们能求出 $t$ 时刻，在策略 $\pi$ 下 $x_T^{\pi}$ 的条件期望和方差如下：

\begin{aligned}
    \mathbb{E} _{t}\left[x_{T}^{\pi}\right] &= r_{f}^{T-t}x_t^{\pi} + a\sum_{s=t}^{T-1}r_f^{T-s-1}\mathbb{E}[u_s^\pi] \\
    \operatorname{Var}_t(x_T^\pi) &= \sum_{s=t}^{T-1} r_{f}^{2(T-s-1)}\left[(a^2+\sigma^2)\mathbb{E}[(u_s^{\pi})^2]-a^2(\mathbb{E}(u_s^\pi))^2   \right]
\end{aligned}

??? Notes
    
    \begin{aligned}
        \mathbb{E} _{t}\left[x_{T}^{\pi}\right] &= \mathbb{E}_t \left[ r_{f}^{T-t} x_t^{\pi} +\sum_{s=t}^{T-1} r_{f}^{T-s-1} r_{s} u_{s}^{\pi} \right] \\
        &= r_{f}^{T-t}~\mathbb{E}_t[x_t^{\pi}] + \sum_{s=t}^{T-1}r_f^{T-s-1}\mathbb{E}_t[r_s u_s^{\pi}] \\
        &= r_{f}^{T-t}x_t^{\pi} + \sum_{s=t}^{T-1}r_f^{T-s-1}\mathbb{E}_t[r_s]\mathbb{E}_t[u_s^\pi] \\
        &= r_{f}^{T-t}x_t^{\pi} + \sum_{s=t}^{T-1}r_f^{T-s-1}\mathbb{E}[r_s]\mathbb{E}[u_s^\pi] \\
        &= r_{f}^{T-t}x_t^{\pi} + a\sum_{s=t}^{T-1}r_f^{T-s-1}\mathbb{E}[u_s^\pi]
    \end{aligned}

    \begin{aligned}
        \operatorname{Var}_t(x_T^\pi) &= \operatorname{Var}_t \left[r_{f}^{T-t} x_t^{\pi} +\sum_{s=t}^{T-1} r_{f}^{T-s-1} r_{s} u_{s}^{\pi}\right] \\
        &= \operatorname{Var}_t \left[\sum_{s=t}^{T-1} r_{f}^{T-s-1} r_{s} u_{s}^{\pi}\right] \\
        &= \sum_{s=t}^{T-1} r_{f}^{2(T-s-1)}\operatorname{Var}_t \left[ r_{s} u_{s}^{\pi}\right] \\
        &= \sum_{s=t}^{T-1} r_{f}^{2(T-s-1)}\left\{\mathbb{E}_t[(r_su_s^{\pi})^2]-(\mathbb{E}_t[r_su_s^{\pi}])^2 \right\} \\
        &= \sum_{s=t}^{T-1} r_{f}^{2(T-s-1)}\left\{\mathbb{E}_t[r_s^2]\mathbb{E}_t[(u_s^\pi)^2]-(\mathbb{E}_t[r_s])^2(\mathbb{E}_t[u_s^{\pi}])^2 \right\} \\
        &= \sum_{s=t}^{T-1} r_{f}^{2(T-s-1)}\left[(a^2+\sigma^2)\mathbb{E}[(u_s^{\pi})^2]-a^2(\mathbb{E}(u_s^\pi))^2   \right]
    \end{aligned}


用分布策略过程 $\boldsymbol{\pi} = \{\pi_t,0\le t < T\}$ 的累积熵去刻画强化学习的探索过程。

\begin{equation*}
    \mathcal{H}(\boldsymbol{\pi}) := \sum_{t=0}^{T-1}H(\pi_t).
\end{equation*}

其中，$H(\pi_t)$ 是 $t$ 时刻策略分布的熵，定义如下：

\begin{equation*}
    H(\pi_t)= -\int_{\mathbb{R}} \pi_t(u) \log \pi_t(u) d u
\end{equation*}

将探索过程引入均值方差准则。可以得到，在离散时间的市场背景下，带熵正则的动态均值方差准则的奖励泛函为：

\begin{equation}
    J\left(t, x ; \pi\right):=\mathbb{E}_{t}\left[x_{T}^{\pi}+\lambda \sum_{s=t}^{T-1} H\left(\pi_{s}\right) \right]-\frac{\gamma}{2} \operatorname{Var}_{t}\left[x_{T}^{\pi}\right] .
\end{equation}

:   * $\lambda$ 是一个代表探索权重，用于实现探索和利用的最佳平衡。

给定 $(t,x)$ ，投资者在原则上需要寻找约束在区间 $[t,T]$ 反馈控制 $\pi$ 去最大化 $J(t,x;\boldsymbol{\pi})$ ，如下：

\begin{align*}
    \max_{\boldsymbol{\pi}}\ & J(t,x;\pi), \\[2mm]
    \text{where }~ &\boldsymbol{\pi} = \{\pi_t, \pi_{t+1}, \cdots, \pi_{T-1}\}
\end{align*}

然而在金融市场中的投资决策问题中，投资者只能根据当前市场信息和当下的投资组合来选择投资策略。
由于未来的市场条件、信息和风险状况未知，投资者不能预先制定未来每一个时刻的投资策略，只能选择当前时刻的投资策略 $\pi_t$。
因此，我们不去寻找"最优"的反馈控制分布，而是从博弈论的角度出发，进行逐步决策，即基于当前的状态动态的调整投资策略。

我们考虑子博弈完美纳什均衡策略。定义如下：

***
**Definition 1.** 考虑一个策略分布 $\boldsymbol{\pi}^*$ ，如果它满足以下构造：

1. 固定任意的点 $(t,x)$，其中 $t<T$ ，选择任意的策略分布 $v\in \mathcal{P}(\mathbb{R})$
2. 定义一个在 $\{t,t+1,\cdots,T-1\}$ 上的扰动控制 $\boldsymbol{\pi}^{v,t}$

\[\boldsymbol{\pi}^{v,t}=\{\pi_t^{v,t},\pi_{t+1}^{v,t},\cdots,\pi_{T-1}^{v,t}\}\]

\begin{equation*}
    \mathbf{\pi}_{k}^{v, t}=\left\{\begin{array}{ll}
        v & \text { for } k=t \\
        {\pi}_{k}^* & \text { for } k=t+1, \ldots, T-1
    \end{array}\right.    
\end{equation*}

如果对每一个固定的 $(t,x)$ 有

\[\sup _{v \in \mathcal{P}(\mathbb{R})} J\left(t,x; \boldsymbol{\pi}^{v,t} \right)=J\left(t,x; \boldsymbol{\pi}^*\right) .\]

那么将 $\boldsymbol{\pi}^*$ 称作子博弈完美纳什均衡策略。

对于一个均衡策略 $\boldsymbol{\pi}^*$ ，定义均衡值函数 $V^*$ 为：

\[V^*(t,x):= J(t,x;\boldsymbol{\pi}^*)\]

***

***
**Thm 1.** 

定义：$g_t(x)$

\begin{aligned}
    g_t(x) &= \mathbb{E}_{t,x}[g(X_{t+1}^{\pi^*})] \\
    g_T(x) &=x
\end{aligned}

$(V^*(t,x),g_t(x))$ 满足以下方程：

\begin{aligned}
    V^*(t,x)=\sup _{v \in \mathcal{P}(\mathbb{R})} \{ E_{t}\left[ V^*(t+1,X_{t+1}^{v})\right]-\frac{\gamma}{2} \operatorname{Var}_{t}[g_{t+1}(X_{t+1}^{v})] +\lambda H(v)\}
\end{aligned}

$t$ 时刻的均衡策略 $\pi_t^*$ 为

\[\pi_t^* = \mathcal{N}\left(\frac{a}{\gamma\sigma^2}r_f^{-(T-t-1)},\frac{\lambda }{\gamma (a^2+\sigma^2)}r_f^{-2(T-t-1)}  \right)\]

***
