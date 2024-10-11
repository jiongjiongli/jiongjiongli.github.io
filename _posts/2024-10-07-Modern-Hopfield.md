---
layout: post
title: Global Convergence of Modern Hopfield Network
---

## Notations
1. The $$p$$-norm of a vector is denoted: $$\left \lVert {\cdot} \right \rVert _p\text{,} 1 \leqslant p$$

2. Let $$\beta > 0, \beta \in \mathbb {R}$$

3. Let $$\left[ N \right] = \left\lbrace1, \cdots, N \right\rbrace$$

## Softmax Function

$$
\begin{align*}
&\text {}{\mathbf {p}} \left(\text {}{\mathbf {x}} \right) = \operatorname{softmax}\left(\beta \text {}{\mathbf {x}} \right) \\
&p_i = \left[\operatorname{softmax}\left(\beta \text {}{\mathbf {x}} \right) \right]_i = \dfrac {\exp \left( {\beta x_i} \right)} {\sum_{k=1}^{N} \exp \left( {\beta x_k} \right)}
\end{align*}
$$

where $$\text {} {\mathbf {x}_{i}} \in \mathbb {R}^{N}$$.

## Log-Sum-Exp Function

$$
\operatorname{lse} \left ( \beta, \text {}{\mathbf {x}} \right ) = \beta^{-1} \ln \left( {\sum_{k=1}^{N} \exp \left( {\beta x_k} \right)} \right)
$$

where $$\text {} {\mathbf {x}_{i}} \in \mathbb {R}^{N}$$.

## Lemma 1
$$
\nabla _{\text {}{\mathbf {x}}} \operatorname{lse} \left ( \beta, \text {}{\mathbf {x}} \right ) = \operatorname{softmax}\left(\beta \text {}{\mathbf {x}} \right)
$$

where $$\text {} {\mathbf {x}} \in \mathbb {R}^{N}$$.

$$
\nabla _{\text {}{\boldsymbol{\xi}}} \operatorname{lse} \left ( \beta, \boldsymbol{X}^T \boldsymbol{\xi}  \right ) = \boldsymbol{X} \operatorname{softmax}\left(\beta \text {}{\boldsymbol{X}^T \boldsymbol{\xi}} \right)
$$

where $$\text {} {\boldsymbol{X}} \in \mathbb {R}^{d \times N}, \text {} {\boldsymbol{\xi}} \in \mathbb {R}^{d}$$.
## Lemma 2
The Jacobian $$J_s \left(\text {}{\mathbf {x}} \right)$$ of $$ \text {}{\mathbf {p}} \left(\text {}{\mathbf {x}} \right)= \operatorname{softmax}\left(\beta \text {}{\mathbf {x}} \right) $$ is

$$
J_s \left(\text {}{\mathbf {x}} \right) = \dfrac {\partial \operatorname{softmax}\left(\beta \text {}{\mathbf {x}} \right)} {\partial \text {}{\mathbf {x}}} = \beta \left(\operatorname{diag}\left(\text {}{\mathbf {p}}\right) - \text {}{\mathbf {p}}\text {}{\mathbf {p}}^T \right)
$$

where $$\text {} {\mathbf {x}} \in \mathbb {R}^{N}$$.
The Jacobian $$J \left(\boldsymbol{\xi} \right)$$ of $$\text {} {\boldsymbol{X}} \text {}{\mathbf {p}} \left(\boldsymbol{X}^T \boldsymbol{\xi} \right)= \text {} {\boldsymbol{X}} \operatorname{softmax}\left(\beta \boldsymbol{X}^T \boldsymbol{\xi} \right) $$ is
$$
J  \left(\boldsymbol{\xi} \right) = \dfrac {\partial \left( \text {} {\boldsymbol{X}} \operatorname{softmax}\left(\beta \boldsymbol{X}^T\boldsymbol{\xi} \right) \right)} {\partial \text {}{\boldsymbol{\xi}}} = \beta \boldsymbol{X} \left(\operatorname{diag}\left(\text {}{\mathbf {p}}\right) - \text {}{\mathbf {p}}\text {}{\mathbf {p}}^T \right) \boldsymbol{X}^T = \boldsymbol{X} J_s \boldsymbol{X}^T
$$

where $$\text {} {\boldsymbol{X}} \in \mathbb {R}^{d \times N}, \text {} {\boldsymbol{\xi}} \in \mathbb {R}^{d}$$.
## Lemma 3
The Jacobian $$J_s \left(\text {}{\mathbf {x}} \right)$$ of $$\text {}{\mathbf {p}} \left(\text {}{\mathbf {x}} \right)=\operatorname{softmax}\left(\beta \text {}{\mathbf {x}} \right) $$ is symmetric and positive semi-definite where $$\text {} {\mathbf {x}} \in \mathbb {R}^{N}$$.
The Jacobian $$J  \left(\boldsymbol{\xi} \right)$$ of $$\text {} {\boldsymbol{X}} \text {}{\mathbf {p}} \left(\boldsymbol{X}^T \boldsymbol{\xi} \right)=\text {} \boldsymbol{X} \operatorname{softmax}\left(\beta \boldsymbol{X}^T \boldsymbol{\xi} \right) $$ is symmetric and positive semi-definite where $$\text {} {\boldsymbol{X}} \in \mathbb {R}^{d \times N}, \text {} {\boldsymbol{\xi}} \in \mathbb {R}^{d}$$.

### Proof
According to Lemma 2, obviously they are symmetric.
Given any $$\text {}{\mathbf {x}} \in \mathbb {R}^{N}$$, we have

$$
\text {}{\mathbf {x}}^T J_s \text {}{\mathbf {x}} = \beta \text {}{\mathbf {x}}^T \left(\operatorname{diag}\left(\text {}{\mathbf {p}}\right) - \text {}{\mathbf {p}}\text {}{\mathbf {p}}^T \right) \text {}{\mathbf {x}}
= \beta \left[ \sum_{i} p_i {x_i}^2 - \left({\sum_{i} p_i x_i}\right)^2 \right]
\geqslant 0
$$

Given any $$\text {} {\boldsymbol{\xi}} \in \mathbb {R}^{d}$$, we have

$$
\text {}{\boldsymbol{\xi}}^T J \text {}{\boldsymbol{\xi}} = \text {}{\boldsymbol{\xi}}^T \boldsymbol{X} J_s \boldsymbol{X}^T \text {}{\boldsymbol{\xi}}
= {\left(\boldsymbol{X}^T \text {}{\boldsymbol{\xi}}\right)}^T J_s {\left(\boldsymbol{X}^T \text {}{\boldsymbol{\xi}}\right)}
\geqslant 0
$$

## Lemma 4

$$\operatorname{lse} \left ( \beta, \text {}{\mathbf {x}} \right )$$ is a convex with respect to $$\text {} {\mathbf {x}}$$ where $$\text {} {\mathbf {x}} \in \mathbb {R}^{N}$$.

$$\operatorname{lse} \left ( \beta, \boldsymbol{X}^T \boldsymbol{\xi}  \right )$$ is a convex with respect to $$\text {} {\boldsymbol{\xi}}$$ where $$\text {} {\boldsymbol{X}} \in \mathbb {R}^{d \times N}, \text {} {\boldsymbol{\xi}} \in \mathbb {R}^{d}$$.

### Proof

The Jacobian of the $$\operatorname{softmax}$$ is Hessian of the $$\operatorname{lse}$$ according to Lemma 1. The Jacobian of the $$\operatorname{softmax}$$ is positive semi-definite according to Lemma 3. Therefore $$\operatorname{lse}$$ is a convex.

## Definitions

### Point-to-set Map

A point-to-set map $$\mathcal{A}$$ from a set $$X$$ into a set $Y$ is defined as

$$
\mathcal{A}: X \to \mathscr{P}(Y)
$$

which assigns a subset of $Y$ to each point of $$X$$, where $$\mathscr{P}(Y)$$ denotes the power set of $Y$.

### Closed

Suppose $$X$$ and $Y$ are two topological spaces. A point-to-set map $$\mathcal{A}: X \to \mathscr{P}(Y)$$ is said to be closed at $$\mathbf x_0 \in X$$ if:

$$
\begin{align*}
    \left .
    \begin{array}{l}
        \text {} {\mathbf {x}_{t}} \to \text {} {\mathbf x_0} \text{ as } t \to \infty \\
        \text {} {\mathbf {y}_{t}} \to \text {} {\mathbf {y}_{0}} \text{ as } t \to \infty \\
        \text {} {\mathbf {x}_{t}} \in X \\
        \text {} {\mathbf {y}_{t}} \in \mathcal{A} \left(\text {} {\mathbf {x}_{t}} \right)
    \end{array}
    \right\rbrace \implies \text {} {\mathbf {y}_{0}} \in \mathcal{A} \left(\text {} {\mathbf x_0} \right)
\end{align*}
$$

A point-to-set map $$\mathcal{A}$$ is said to be closed on $S \subset X$$ if it is closed at every point of $S$.

### Fixed Point

A fixed point of the map

$$
\mathcal{A}: X \to \mathscr{P}(X)
$$

is any point $$\text {}{\mathbf {x}} \in X$$ for which

$$
\mathcal{A} \left( \text {}{\mathbf {x}} \right) = \left\lbrace \text {}{\mathbf {x}} \right\rbrace
$$

A generalized fixed point of $$\mathcal{A}$$ is any point $$\text {}{\mathbf {x}} \in X$$ for which

$$
\text {}{\mathbf {x}} \in \mathcal{A} \left( \text {}{\mathbf {x}} \right)
$$

### Uniformly Compact
A point-to-set map $$\mathcal{A}: X \to \mathscr{P}(X)$$ is said to be uniformly compact on $$X$$ if there exists a compact set $H$ independent of $$\text {}{\mathbf {x}}$$ such that:

$$
\forall \text {}{\mathbf {x}} \in X, \mathcal{A} \left( \text {}{\mathbf {x}} \right) \subset H
$$

### Monotonic

Let

$$
\operatorname {E}: X \to \mathbb {R}
$$

be a continuous function. The map

$$
\mathcal{A}: X \to \mathscr{P} \left(X \right)
$$

is said to be monotonic with respect to $$\operatorname {E}$$ at $$\mathbf {x} \in X$$ if

$$
\forall \text {}{\mathbf {y}} \in \mathcal{A} \left( \text {}{\mathbf {x}} \right), \operatorname {E} \left( \text {}{\mathbf {y}} \right) \leqslant \operatorname {E} \left( \text {}{\mathbf {x}} \right)
$$

$$\mathcal{A}$$ is said to be strictly monotonic with respect to $$\operatorname {E}$$ at $$\mathbf {x} \in X$$ if

$$
\mathcal{A} \left( \text {}{\mathbf {x}} \right) \neq \left \lbrace \text {}  \mathbf {x} \right \rbrace \implies \forall \text {}{\mathbf {y}} \in \mathcal{A} \left( \text {}{\mathbf {x}} \right), \operatorname {E} \left( \text {}{\mathbf {y}} \right) < \operatorname {E} \left( \text {}{\mathbf {x}} \right)
$$

### Global Convergence
Let $$X$$ be a set and $$\text {} {\boldsymbol{\xi}_0} \in X$$ a given point. Then an algorithm, $$\mathcal{A}$$, with initial point $$\text {} {\boldsymbol{\xi}_0}$$ is a point-to-set map $$\mathcal{A}: X \to \mathscr{P} \left(X \right)$$ which generates a sequence $${\left \lbrace \text {} {\boldsymbol{\xi}_t} \right \rbrace} _{t=0} ^{\infty}$$ via the rule

$$
\text {}{\boldsymbol{\xi}_{t + 1}} \in \mathcal{A} \left (\text {} {\boldsymbol{\xi}_t} \right ), t = 0, 1, \cdots
$$

$$\mathcal{A}$$ is said to be globally convergent if: Given any chosen initial point $$\text {} {\boldsymbol{\xi}_0}$$, the sequence $${\left \lbrace \text {} {\boldsymbol{\xi}_t} \right \rbrace} _{t=0} ^{\infty}$$ generated by $$\text {} {\boldsymbol{\xi}_{t + 1}} \in \mathcal{A} \left (\text {} {\boldsymbol{\xi}_t} \right ), t = 0, 1, \cdots$$ (or a subsequence) converges to a point for which a necessary condition of optimality holds.

## Lemma 5
Consider an energy function $$\operatorname {E}: X \to \mathbb {R}$$:

$$
\operatorname {E} \left ( \boldsymbol{\xi}  \right ) = \operatorname {E_1} \left ( \boldsymbol{\xi}  \right ) - \operatorname {E_2} \left ( \boldsymbol{\xi}  \right )
$$

where $$\operatorname {E_1}$$ and $$\operatorname {E_2}$$ are differentiable convex functions of $$\boldsymbol{\xi}$$ respectively. Then the discrete CCCP (Concave Convex Procedure) algorithm

$$
\text {} {\boldsymbol{\xi}_{t + 1}} \in \mathcal{A} \left (\text {} {\boldsymbol{\xi}_t} \right ), t = 0, 1, \cdots
$$

given by:

$$
\nabla _{\boldsymbol{\xi}} \operatorname {E_1} \left ( \boldsymbol{\xi}_{t + 1} \right ) = \nabla _{\boldsymbol{\xi}} \operatorname {E_2} \left ( \boldsymbol{\xi}_{t}  \right )
$$

guarantees the sequence $${\left \lbrace \operatorname {E} \left ( \text {} {\boldsymbol{\xi}_t} \right ) \right \rbrace} _{t=0} ^{\infty}$$ monotonically decreases.

In addition, if $$\operatorname {E_1}$$ or $$\operatorname {E_2}$$ is strictly convex function, and $$\boldsymbol{\xi}_{t + 1} \neq \boldsymbol{\xi}_{t}$$, then

$$
\operatorname {E} \left(\boldsymbol{\xi}_{t + 1}\right) < \operatorname {E} \left(\boldsymbol{\xi}_{t}\right)
$$


### Proof
$$\operatorname {E_1}$$ and $$\operatorname {E_2}$$ are convex functions, so that $$\forall t \geqslant 0$$,

$$
\begin{align*}
    &
    \left .
    \begin{array}{l}
        \operatorname {E_1} \left(\boldsymbol{\xi}_{t}\right) \geqslant \operatorname {E_1} \left(\boldsymbol{\xi}_{t + 1}\right) + {\left(\nabla \operatorname {E_1} \left(\boldsymbol{\xi}_{t + 1}\right)\right)}^T \left(\boldsymbol{\xi}_{t} - \boldsymbol{\xi}_{t + 1}\right) \\
        \operatorname {E_2} \left(\boldsymbol{\xi}_{t + 1}\right) \geqslant \operatorname {E_2} \left(\boldsymbol{\xi}_{t}\right) + {\left(\nabla \operatorname {E_2} \left(\boldsymbol{\xi}_{t}\right)\right)}^T \left(\boldsymbol{\xi}_{t + 1} - \boldsymbol{\xi}_{t}\right) \\
        \nabla \operatorname {E_1} \left(\boldsymbol{\xi}_{t + 1}\right) = \nabla \operatorname {E_2} \left(\boldsymbol{\xi}_{t}\right)
    \end{array}
    \right\rbrace \\
    & \implies \operatorname {E_1} \left(\boldsymbol{\xi}_{t}\right) + \operatorname {E_2} \left(\boldsymbol{\xi}_{t + 1}\right) \geqslant \operatorname {E_1} \left(\boldsymbol{\xi}_{t + 1}\right) + \operatorname {E_2} \left(\boldsymbol{\xi}_{t}\right) \\
    & \implies \operatorname {E_1} \left(\boldsymbol{\xi}_{t + 1}\right) - \operatorname {E_2} \left(\boldsymbol{\xi}_{t + 1}\right) \leqslant \operatorname {E_1} \left(\boldsymbol{\xi}_{t}\right) - \operatorname {E_2} \left(\boldsymbol{\xi}_{t}\right) \\
    & \implies \operatorname {E} \left(\boldsymbol{\xi}_{t + 1}\right) \leqslant \operatorname {E} \left(\boldsymbol{\xi}_{t}\right)
\end{align*}
$$

Therefore $$\mathcal{A}$$ is monotonic with respect to $$\operatorname {E}$$.

In addition, if $$\operatorname {E_1}$$ is strictly convex function, and $$\boldsymbol{\xi}_{t + 1} \neq \boldsymbol{\xi}_{t}$$, then

$$
\begin{align*}
    &
    \left .
    \begin{array}{l}
        \operatorname {E_1} \left(\boldsymbol{\xi}_{t}\right) > \operatorname {E_1} \left(\boldsymbol{\xi}_{t + 1}\right) + {\left(\nabla \operatorname {E_1} \left(\boldsymbol{\xi}_{t + 1}\right)\right)}^T \left(\boldsymbol{\xi}_{t} - \boldsymbol{\xi}_{t + 1}\right) \\
        \operatorname {E_2} \left(\boldsymbol{\xi}_{t + 1}\right) \geqslant \operatorname {E_2} \left(\boldsymbol{\xi}_{t}\right) + {\left(\nabla \operatorname {E_2} \left(\boldsymbol{\xi}_{t}\right)\right)}^T \left(\boldsymbol{\xi}_{t + 1} - \boldsymbol{\xi}_{t}\right) \\
        \nabla \operatorname {E_1} \left(\boldsymbol{\xi}_{t + 1}\right) = \nabla \operatorname {E_2} \left(\boldsymbol{\xi}_{t}\right)
    \end{array}
    \right\rbrace \\
    & \implies \operatorname {E_1} \left(\boldsymbol{\xi}_{t}\right) + \operatorname {E_2} \left(\boldsymbol{\xi}_{t + 1}\right) > \operatorname {E_1} \left(\boldsymbol{\xi}_{t + 1}\right) + \operatorname {E_2} \left(\boldsymbol{\xi}_{t}\right) \\
    & \implies \operatorname {E_1} \left(\boldsymbol{\xi}_{t + 1}\right) - \operatorname {E_2} \left(\boldsymbol{\xi}_{t + 1}\right) < \operatorname {E_1} \left(\boldsymbol{\xi}_{t}\right) - \operatorname {E_2} \left(\boldsymbol{\xi}_{t}\right) \\
    & \implies \operatorname {E} \left(\boldsymbol{\xi}_{t + 1}\right) < \operatorname {E} \left(\boldsymbol{\xi}_{t}\right)
\end{align*}
$$

## Modern Hopfield Network

We have patterns that are represented by the matrix:
$$
\boldsymbol{X} = \left(\text {} {\mathbf {x}_{1}}, \dots, \text {}{\mathbf {x}_{N}} \right)
$$

where $$\text {} {\mathbf {x}_{i}} \in \mathbb {R}^{d}$$. Thus $$\text {} {\boldsymbol{X}} \in \mathbb {R}^{d \times N}$$.
The largest norm of a pattern is:

$$
M = \max_{i \in \left[ N \right]} \left \lVert \text {} {\mathbf {x}_{i}} \right \rVert _2
$$

The query or state of the Hopfield Network is $$\boldsymbol{\xi} \in \mathbb {R}^{d}$$.
Define energy $$\operatorname {E} \left ( \boldsymbol{\xi}  \right )$$ for a continuous query or state $$\boldsymbol{\xi}$$:
$$
\operatorname {E} \left ( \boldsymbol{\xi}  \right ) = - \operatorname{lse} \left ( \beta, \boldsymbol{X}^T \boldsymbol{\xi}  \right ) + \dfrac {1} {2} \boldsymbol{\xi}^T \boldsymbol{\xi} + \beta^{-1} \ln N + \dfrac {1} {2} M^2 \tag {Eq.1}
$$

## New Update Rule

$$
\boldsymbol{\xi}_{t + 1} = \mathcal{F} \left ( \boldsymbol{\xi}_{t} \right ) = \boldsymbol{X}\text {}{\mathbf {p}} = \boldsymbol{X} \operatorname{softmax}\left(\beta \boldsymbol{X}^T {\boldsymbol{\xi}_{t}} \right)  \tag {Eq.2}
$$

where

$$
\text {}{\mathbf {p}} = \operatorname{softmax}\left(\beta \boldsymbol{X}^T {\boldsymbol{\xi}_{t}} \right)
$$

## Theorem 1 Global Convergence: Energy

The update rule (Eq.2) converges globally: For $$\boldsymbol{\xi}_{t+ 1} = \mathcal{F} \left ( \boldsymbol{\xi}_{t} \right )$$, the energy $$\operatorname {E} \left ( \boldsymbol{\xi}_{t} \right ) \to \operatorname {E} \left ( \boldsymbol{\xi}^{\ast} \right )$$ for $$t \to \infty$$ and one limit point $$\boldsymbol{\xi}^{\ast}$$.


### Proof

$$
{\left \lVert {\boldsymbol{\xi}_{t + 1}} \right \rVert} _2
= {\left \lVert {\boldsymbol{X}\text {}{\mathbf {p}}} \right \rVert} _2
= {\left \lVert {\sum_{i=1}^{N} p_i \text {} {\mathbf {x}_{i}}} \right \rVert} _2
\leqslant {\sum_{i=1}^{N} p_i \left \lVert \text {} {\mathbf {x}_{i}} \right \rVert} _2
\leqslant \sum_{i=1}^{N} p_i M
= M
$$

Hence

$$
\forall t \geqslant 1, \boldsymbol{\xi}_{t} \in S = \left\lbrace\text {}{\boldsymbol{\xi}} \middle \vert \left \lVert {\text {}{\boldsymbol{\xi}}} \right \rVert _2 \leqslant M \right\rbrace \tag {Theo1.1}
$$

which is a convex and compact set.

Obviously $$\dfrac {1} {2} \boldsymbol{\xi}^T \boldsymbol{\xi}$$ is a strictly convex function.

According to Lemma 4, $$\operatorname{lse}$$ is a convex function.

Hence the energy function $$\operatorname {E} \left ( \boldsymbol{\xi}  \right )$$ is the difference of a strictly convex function $$\operatorname {E_1} \left ( \boldsymbol{\xi}  \right )$$ and a convex function $$\operatorname {E_2} \left ( \boldsymbol{\xi}  \right )$:

$$
\begin{align*}
\operatorname {E} \left ( \boldsymbol{\xi}  \right ) &= \operatorname {E_1} \left ( \boldsymbol{\xi}  \right ) - \operatorname {E_2} \left ( \boldsymbol{\xi}  \right ) \\
\operatorname {E_1} \left ( \boldsymbol{\xi}  \right ) &= \dfrac {1} {2} \boldsymbol{\xi}^T \boldsymbol{\xi} + \beta^{-1} \ln N + \dfrac {1} {2} M^2 = \dfrac {1} {2} \boldsymbol{\xi}^T \boldsymbol{\xi} + C_1 \\
\operatorname {E_2} \left ( \boldsymbol{\xi}  \right ) &= \operatorname{lse} \left ( \beta, \boldsymbol{X}^T \boldsymbol{\xi}  \right )
\end{align*} \tag {Theo1.2}
$$

where $C_1$ does not depend on $$\boldsymbol{\xi}$$.

Define minimization problem:

$$
\min _{\boldsymbol{\xi}} \operatorname {E} \left ( \boldsymbol{\xi}  \right ) = \min _{\boldsymbol{\xi}} \left ( \operatorname {E_1} \left ( \boldsymbol{\xi}  \right ) - \operatorname {E_2} \left ( \boldsymbol{\xi}  \right ) \right ) \tag {Theo1.20}
$$

Let

$$
\nabla _{\boldsymbol{\xi}} \operatorname {E_1} \left ( \boldsymbol{\xi}_{t + 1} \right ) = \nabla _{\boldsymbol{\xi}} \operatorname {E_2} \left ( \boldsymbol{\xi}_{t}  \right )
$$

The resulting update rule is:

$$
\boldsymbol{\xi}_{t + 1} = \boldsymbol{X} \operatorname{softmax}\left(\beta \boldsymbol{X}^T {\boldsymbol{\xi}}_t \right)
$$

Let

$$
\mathcal{A} \left ( \boldsymbol{\xi}_{t } \right ) = \left\lbrace \boldsymbol{X} \operatorname{softmax}\left(\beta \boldsymbol{X}^T {\boldsymbol{\xi}_{t}} \right) \right\rbrace
$$

According to (Theo1.1), all points $$\boldsymbol{\xi}_t, t \geqslant 1$$ are in a compact set $S$. Hence there must be a convergent subsequence

$$
\boldsymbol{\xi}_{t_k} \to \boldsymbol{\xi}^{\ast}, \text{ as } k \to \infty
$$

where $$\boldsymbol{\xi}^{\ast} \in S$$ is a limit point.
Continuity of $$\operatorname {E}$$ provides
$$
\operatorname {E}\left(\boldsymbol{\xi}_{t_k}\right) \to \operatorname {E}\left(\boldsymbol{\xi}^{\ast}\right), \text{ as } k \to \infty \tag {Theo1.3}
$$

According to Lemma 5, $$\mathcal{A}$$ is monotonic with respect to $$\operatorname {E}$$. So that

$$
\forall t \geqslant 0, \operatorname {E}\left(\boldsymbol{\xi}_{t}\right) \geqslant \operatorname {E}\left(\boldsymbol{\xi}^{\ast}\right)\tag {Theo1.4}
$$

Using (Theo1.3) and the definition of limit, given $$\varepsilon_{1} > 0$$, there is a $$t_{\varepsilon_{1}}$$ such that

$$
\operatorname {E}\left(\boldsymbol{\xi}_{t_{\varepsilon_{1}}}\right) < \operatorname {E}\left(\boldsymbol{\xi}^{\ast}\right) + \varepsilon_{1}
$$

$$\mathcal{A}$$ is monotonic with respect to $$\operatorname {E}$$, then

$$
\forall t > t_{\varepsilon_{1}}, \operatorname {E}\left(\boldsymbol{\xi}_{t}\right) \leqslant \operatorname {E}\left(\boldsymbol{\xi}_{t_{\varepsilon_{1}}}\right) < \operatorname {E}\left(\boldsymbol{\xi}^{\ast}\right) + \varepsilon_{1}
$$

Equations then yield

$$
\forall t > t_{\varepsilon_{1}}, \left \lvert \operatorname {E}\left(\boldsymbol{\xi}_{t}\right) - \operatorname {E}\left(\boldsymbol{\xi}^{\ast}\right) \right \rvert < \varepsilon_{1}
$$

Therefore

$$
\operatorname {E}\left(\boldsymbol{\xi}_{t}\right) \to \operatorname {E}\left(\boldsymbol{\xi}^{\ast}\right) = \operatorname {E}^{\ast}, \text{ as } t \to \infty \tag {Theo1.5}
$$

## Lemma 6
Given a continuous function $$h \left(\mathbf {x}, \mathbf {y} \right)$$ on $$X \times Y$$, where $$X$$ and $$Y$$ are closed sets, define the point-to-set map $$\mathcal{A}: X \to \mathscr{P}(Y)$$ by

$$
\mathcal{A} \left ( \mathbf {x} \right ) = \underset{\mathbf {y} \in Y} {\operatorname{argmin}} h \left(\mathbf {x}, \mathbf {y} \right)
$$

If $$\mathcal{A}$$ is nonempty at each $$\mathbf {x} \in X$$, then $$\mathcal{A}$$ is closed.

### Proof
Suppose

$$
\begin{align*}
  \left \lbrace
\begin{array}{l}
{\mathbf {x}_{t}} \to {\mathbf {x}_{0}} \text{ as } t \to \infty \\
{\mathbf {y}_{t}} \to {\mathbf {y}_{0}} \text{ as } t \to \infty \\
{\mathbf {x}_{t}} \in X \\
{\mathbf {y}_{t}} \in \mathcal{A} \left ( \mathbf {x}_{t} \right ) = \underset{\mathbf {y} \in Y} {\operatorname{argmin}} h \left(\mathbf {x}_{t}, \mathbf {y} \right)
\end{array}
\right.
\end{align*}
$$

Since $$X$$ and $$Y$$ are closed sets, $$\left(\mathbf {x}_{0}, \mathbf {y}_{0} \right) \in X \times Y$$.

By continuity of $${h}$

$$
\begin{align*}
h \left(\mathbf {x}_{t}, \mathbf {y}_{t} \right) & \to h \left(\mathbf {x}_{0}, \mathbf {y}_{0} \right) \text{ as } t \to \infty \\
\forall \mathbf {y} \in Y, h \left(\mathbf {x}_{t}, \mathbf {y} \right) & \to h \left(\mathbf {x}_{0}, \mathbf {y} \right) \text{ as } t \to \infty
\end{align*}
$$

Using the definition of limit, $$\forall \mathbf {y} \in Y, \forall \varepsilon_{2} > 0$$, there is a $$t_{\varepsilon_{2}}$$ such that $$\forall t > t_{\varepsilon_{2}}$$,

$$
\begin{align*}
h \left(\mathbf {x}_{t}, \mathbf {y}_{t} \right) &> h \left(\mathbf {x}_{0}, \mathbf {y}_{0} \right) - \varepsilon_{2} \\
h \left(\mathbf {x}_{t}, \mathbf {y} \right) &< h \left(\mathbf {x}_{0}, \mathbf {y} \right) + \varepsilon_{2} \tag{Lemma6.1}
\end{align*}
$$

Because

$$
{\mathbf {y}_{t}} \in \mathcal{A} \left ( \mathbf {x}_{t} \right ) = \underset{\mathbf {y} \in Y} {\operatorname{argmin}} h \left(\mathbf {x}_{t}, \mathbf {y} \right) \implies h \left(\mathbf {x}_{t}, \mathbf {y}_{t} \right) \leqslant h \left(\mathbf {x}_{t}, \mathbf {y} \right) \tag{Lemma6.2}
$$

Using (Lemma6.1), (Lemma6.2)

$$
h \left(\mathbf {x}_{0}, \mathbf {y}_{0} \right) < h \left(\mathbf {x}_{t}, \mathbf {y}_{t} \right) + \varepsilon_{2} \leqslant h \left(\mathbf {x}_{t}, \mathbf {y} \right) + \varepsilon_{2} < h \left(\mathbf {x}_{0}, \mathbf {y} \right) + 2 \varepsilon_{2}
$$

Hence

$$
h \left(\mathbf {x}_{0}, \mathbf {y}_{0} \right) \leqslant h \left(\mathbf {x}_{0}, \mathbf {y} \right)
$$

Therefore

$$
{\mathbf {y}_{0}} \in \mathcal{A} \left(\text {} {\mathbf {x}_{0}} \right) = \underset{\mathbf {y} \in Y} {\operatorname{argmin}} h \left(\mathbf {x}_{0}, \mathbf {y} \right)
$$

## Theorem 2 Global Convergence: Stationary Points
For the iteration (Eq.2) we have

$$
\operatorname {E}\left(\boldsymbol{\xi}_{t}\right) \to \operatorname {E}\left(\boldsymbol{\xi}^{\ast}\right) = \operatorname {E}^{\ast}, \text{ as } t \to \infty
$$

for some stationary point $$\boldsymbol{\xi}^{\ast}$$. Furthermore

$$
\left \lVert \boldsymbol{\xi}_{t + 1} - \boldsymbol{\xi}_{t} \right \rVert _2 \to 0, \text{ as } t \to \infty
$$

And either $${\left \lbrace \text {} {\boldsymbol{\xi}_t} \right \rbrace} _{t=0} ^{\infty}$$ converges, or, in the other case, the set of limit points of $${\left \lbrace \text {} {\boldsymbol{\xi}_t} \right \rbrace} _{t=0} ^{\infty}$$ is a connected and compact subset of $$\mathcal{L} \left ( \operatorname {E}^{\ast} \right )$$, where $$\mathcal{L} \left ( a \right ) = \left \lbrace \boldsymbol{\xi} \in \mathcal{L} \middle \vert \operatorname {E} \left ( \text {} {\boldsymbol{\xi}} \right ) = a \right \rbrace$$ and $$\mathcal{L}$$ is the set of stationary points of the iteration (Eq.2). If $$\mathcal{L} \left ( \operatorname {E}^{\ast} \right )$$ is finite, then any sequence $${\left \lbrace \text {} {\boldsymbol{\xi}_t} \right \rbrace} _{t=0} ^{\infty}$$ generated by the iteration (Eq.2) converges to some $$\boldsymbol{\xi}^{\ast} \in \mathcal{L} \left ( \operatorname {E}^{\ast} \right )$$.

### Proof

Let

$$
g \left(\boldsymbol{\xi}, \boldsymbol{\xi}_t \right) = \operatorname {E_1} \left ( \boldsymbol{\xi}  \right ) - \operatorname {E_2} \left ( \boldsymbol{\xi}_{t}  \right ) - \left ( \nabla _{\boldsymbol{\xi}} \operatorname {E_2} \left ( \boldsymbol{\xi}_{t}  \right ) \right )^T \left ( \boldsymbol{\xi} - \boldsymbol{\xi}_{t} \right ) = \operatorname {E_1} \left ( \boldsymbol{\xi}  \right ) - \left ( \nabla _{\boldsymbol{\xi}} \operatorname {E_2} \left ( \boldsymbol{\xi}_{t}  \right ) \right )^T \boldsymbol{\xi} + C_2 \left ( \boldsymbol{\xi}_{t}  \right ) \tag {Theo2.1}
$$

where $$\operatorname {E_1}, \operatorname {E_2}$$ are defined by (Theo1.2). $$C_2 \left ( \boldsymbol{\xi}_{t}  \right )$$ does not depend on $$\boldsymbol{\xi}$$.

Let

$$
\mathcal{A} \left ( \boldsymbol{\xi}_{t } \right ) = \underset{\boldsymbol{\xi} \in S} {\operatorname{argmin}} g \left(\boldsymbol{\xi}, \boldsymbol{\xi}_t \right) \tag {Theo2.5}
$$

where $$S$$ is a compact set defined in (Theo1.1). Then $$\mathcal{A}$$ is uniformly compact on $S$.

$$\operatorname {E_1} \left ( \boldsymbol{\xi}  \right ) = \dfrac {1} {2} \boldsymbol{\xi}^T \boldsymbol{\xi} + C_1$$ is continuous, so given any $$\boldsymbol{\xi}_t$$, $$g \left(\boldsymbol{\xi}, \boldsymbol{\xi}_t \right)$$ is continuous on the compact set $$S$$, by the Weierstrass theorem, it has minimum on $$S$$. So $$\mathcal{A} \left ( \boldsymbol{\xi} \right )$$ is nonempty at any $$\boldsymbol{\xi}$$.

$$\operatorname {E_1} \left ( \boldsymbol{\xi}  \right )$$ is continuous. $$\nabla _{\boldsymbol{\xi}} \operatorname {E_2} \left ( \boldsymbol{\xi} \right ) = \boldsymbol{X} \operatorname{softmax}\left(\beta \boldsymbol{X}^T {\boldsymbol{\xi}} \right)$$ is continuous. Hence $$g \left(\mathbf {x}, \mathbf {y} \right)$$ is continuous in $$\mathbf {x}, \mathbf {y}$$.

Let

$$
h \left(\mathbf {x}, \mathbf {y} \right) = g \left(\mathbf {y}, \mathbf {x} \right)
$$

Then $$h \left(\mathbf {x}, \mathbf {y} \right)$$ is continuous.
Using (Theo2.5)
$$
\mathcal{A} \left ( \mathbf {x} \right ) = \underset{\mathbf {y} \in S} {\operatorname{argmin}} g \left(\mathbf {y}, \mathbf {x} \right) = \underset{\mathbf {y} \in S} {\operatorname{argmin}} h \left(\mathbf {x}, \mathbf {y} \right)
$$

According to Lemma 6, $$\mathcal{A}$$ is closed on $$S$$.

Using Lemma 4 $$\operatorname {E_2}$$ is convex , the first order characterization of convexity holds:
$$
\operatorname {E_2} \left ( \boldsymbol{\xi}  \right ) \geqslant \operatorname {E_2} \left ( \boldsymbol{\xi}_{t}  \right ) + \left ( \nabla _{\boldsymbol{\xi}} \operatorname {E_2} \left ( \boldsymbol{\xi}_{t}  \right ) \right )^T \left ( \boldsymbol{\xi} - \boldsymbol{\xi}_{t} \right )
$$

Therefore:

$$
\begin{align*}
\operatorname {E} \left ( \boldsymbol{\xi}  \right ) &= \operatorname {E_1} \left ( \boldsymbol{\xi}  \right ) - \operatorname {E_2} \left ( \boldsymbol{\xi}  \right ) \\
& \leqslant \operatorname {E_1} \left ( \boldsymbol{\xi}  \right ) - \operatorname {E_2} \left ( \boldsymbol{\xi}_{t}  \right ) - \left ( \nabla _{\boldsymbol{\xi}} \operatorname {E_2} \left ( \boldsymbol{\xi}_{t}  \right ) \right )^T \left ( \boldsymbol{\xi} - \boldsymbol{\xi}_{t} \right ) \\
&= g \left(\boldsymbol{\xi}, \boldsymbol{\xi}_t \right) \tag {Theo2.2}
\end{align*}
$$

$$\operatorname {E_1} \left ( \boldsymbol{\xi}  \right ) = \dfrac {1} {2} \boldsymbol{\xi}^T \boldsymbol{\xi} + C_1$$ is strictly convex with respect to $$\text {} {\boldsymbol{\xi}}$$.
$$- \left ( \nabla _{\boldsymbol{\xi}} \operatorname {E_2} \left ( \boldsymbol{\xi}_{t}  \right ) \right )^T \boldsymbol{\xi} + C_2 \left ( \boldsymbol{\xi}_{t}  \right )$$ is both concave and convex with respect to $$\text {} {\boldsymbol{\xi}}$$.
Therefore $$g \left(\boldsymbol{\xi}, \boldsymbol{\xi}_t \right)$$ is strictly convex with respect to $$\text {} {\boldsymbol{\xi}}$$ (if the domain is convex) and there exist only one minimum, which is the global minimum.

Let

$$
\dfrac {\partial g \left(\boldsymbol{\xi}, \boldsymbol{\xi}_t \right)} {\partial {\boldsymbol{\xi}}} = \nabla _{\boldsymbol{\xi}} \operatorname {E_1} \left ( \boldsymbol{\xi} \right ) - \nabla _{\boldsymbol{\xi}} \operatorname {E_2} \left ( \boldsymbol{\xi}_{t}  \right ) = \boldsymbol{\xi} - \nabla _{\boldsymbol{\xi}} \operatorname {E_2} \left ( \boldsymbol{\xi}_{t}  \right ) = \boldsymbol{\xi} - \boldsymbol{X} \operatorname{softmax}\left(\beta \boldsymbol{X}^T {\boldsymbol{\xi}}_t \right) = \text {} {\mathbf {0}} \tag {Theo2.8}
$$

The minimum is:

$$
\boldsymbol{\xi}_{t + 1} = \boldsymbol{X} \operatorname{softmax}\left(\beta \boldsymbol{X}^T {\boldsymbol{\xi}}_t \right) \tag {Theo2.3}
$$

Obviously $$\boldsymbol{\xi}_{t + 1} \in S$$. Thus
$$
\mathcal{A} \left ( \boldsymbol{\xi}_{t } \right ) = \underset{\boldsymbol{\xi} \in S} {\operatorname{argmin}} g \left(\boldsymbol{\xi}, \boldsymbol{\xi}_t \right) = \left \lbrace \boldsymbol{X} \operatorname{softmax}\left(\beta \boldsymbol{X}^T {\boldsymbol{\xi}}_t \right) \right \rbrace \tag {Theo2.5}
$$
Hence
$$
\text { if } \boldsymbol{\xi}_{t + 1} \neq \boldsymbol{\xi}_t, g \left(\boldsymbol{\xi}_{t + 1}, \boldsymbol{\xi}_t \right) \lt g \left(\boldsymbol{\xi}_{t}, \boldsymbol{\xi}_t \right)  \tag {Theo2.4}
$$

Using (Theo2.1), (Theo2.2), (Theo2.4)

$$
\text { if } \boldsymbol{\xi}_{t + 1} \neq \boldsymbol{\xi}_t, \operatorname {E} \left ( \boldsymbol{\xi}_{t + 1} \right ) \leqslant g \left(\boldsymbol{\xi}_{t + 1}, \boldsymbol{\xi}_t \right) \lt g \left(\boldsymbol{\xi}_{t}, \boldsymbol{\xi}_t \right) = \operatorname {E} \left ( \boldsymbol{\xi}_t  \right )
$$

Thus

$$
\forall \boldsymbol{\xi}_{t + 1} \in \mathcal{A} \left ( \boldsymbol{\xi}_t \right ), \text { if } \boldsymbol{\xi}_{t + 1} \neq \boldsymbol{\xi}_t, \operatorname {E} \left ( \boldsymbol{\xi}_{t + 1} \right ) \lt \operatorname {E} \left ( \boldsymbol{\xi}_t \right ) \tag {Theo2.6}
$$

If $$\mathcal{A} \left( \text {}{\boldsymbol{\xi}_{t}} \right) \neq \left \lbrace \text {}  \boldsymbol{\xi}_{t} \right \rbrace$$, suppose $$\text {}{\boldsymbol{\xi}_{t}} \in \mathcal{A} \left( \text {}{\boldsymbol{\xi}_{t}} \right)$$, then $$\exists \text {}{\boldsymbol{\xi}^{'}_{t + 1}} \in \mathcal{A} \left( \text {}{\boldsymbol{\xi}_{t}} \right), \boldsymbol{\xi}^{'}_{t + 1} \neq \boldsymbol{\xi}_t$$. Using (Theo2.4)

$$
g \left(\boldsymbol{\xi}^{'}_{t + 1}, \boldsymbol{\xi}_t \right) \lt g \left(\boldsymbol{\xi}_{t}, \boldsymbol{\xi}_t \right)
$$

which is in contradiction with (Theo2.5). Thus if $$\mathcal{A} \left( \text {}{\boldsymbol{\xi}_{t}} \right) \neq \left \lbrace \text {}  \boldsymbol{\xi}_{t} \right \rbrace$$, then $$\forall \text {}{\boldsymbol{\xi}_{t + 1}} \in \mathcal{A} \left( \text {}{\boldsymbol{\xi}_{t}} \right), \boldsymbol{\xi}_{t + 1} \neq \boldsymbol{\xi}_t$$.

Using (Theo2.6)

$$
\mathcal{A} \left( \text {}{\boldsymbol{\xi}_{t}} \right) \neq \left \lbrace \text {}  \boldsymbol{\xi}_{t} \right \rbrace \implies \forall \text {}{\boldsymbol{\xi}_{t + 1}} \in \mathcal{A} \left( \text {}{\boldsymbol{\xi}_{t}} \right), \operatorname {E} \left( \text {}{\boldsymbol{\xi}_{t + 1}} \right) < \operatorname {E} \left( \text {}{\boldsymbol{\xi}_{t}} \right)
$$

Therefore point-set-map $$\mathcal{A}$$ is strictly monotonic with respect to $$\operatorname {E}$$.

Given any convergent subsequence

$$
\boldsymbol{\xi}_{t_k} \to \boldsymbol{\xi}^{\ast}, \text{ as } k \to \infty \tag {Theo2.7}
$$

where $$\boldsymbol{\xi}^{\ast} \in S$$ is a limit point, consider subsequence:

$$
{\left \lbrace \boldsymbol{\xi}_{t_k + 1} \right \rbrace} _{k=1} ^{\infty}
$$

According to (Theo2.5), all points $$\boldsymbol{\xi}_{t_k + 1}, k \geqslant 1$$ are in the compact set $S$. Hence it must have a convergent subsequence

$$
\boldsymbol{\xi}_{t_{k_l} + 1} \to \boldsymbol{\xi}^{\ast\ast}, \text{ as } l \to \infty
$$

where $$\boldsymbol{\xi}^{\ast\ast} \in S$$ is a limit point.

Using (Theo2.7)

$$
\boldsymbol{\xi}_{t_{k_l}} \to \boldsymbol{\xi}^{\ast}, \text{ as } l \to \infty
$$

Since

$$
\boldsymbol{\xi}_{t_{k_l} + 1} \in \mathcal{A} \left ( \boldsymbol{\xi}_{t_{k_l}} \right )
$$

And $$\mathcal{A}$$ is closed on $$S$$, thus

$$
\boldsymbol{\xi}^{\ast\ast} \in \mathcal{A} \left ( \boldsymbol{\xi}^{\ast} \right )
$$

According to theorem 1, $$\operatorname {E} \left ( \boldsymbol{\xi}^{\ast\ast} \right ) = \operatorname {E} \left ( \boldsymbol{\xi}^{\ast} \right )$$.

If $$\boldsymbol{\xi}^{\ast} \neq \boldsymbol{\xi}^{\ast\ast}$$, using (Theo2.6), $$\operatorname {E} \left ( \boldsymbol{\xi}^{\ast\ast} \right ) \lt \operatorname {E} \left ( \boldsymbol{\xi}^{\ast} \right )$$. A contradiction. Therefore $$\boldsymbol{\xi}^{\ast} = \boldsymbol{\xi}^{\ast\ast}$$.

Hence

$$
\boldsymbol{\xi}^{\ast} \in \mathcal{A} \left ( \boldsymbol{\xi}^{\ast} \right )
$$

In addition, $$\mathcal{A}$$ is strictly monotonic with respect to $$\operatorname {E}$$, so that

$$
\mathcal{A} \left ( \boldsymbol{\xi}^{\ast} \right ) = \left \lbrace \boldsymbol{\xi}^{\ast} \right \rbrace
$$

Therefore $$\boldsymbol{\xi}^{\ast}$$ is a fixed point.

Because constrains in (Theo2.5) are qualified at $$\boldsymbol{\xi}^{\ast}$$, then there exists Lagrange multipliers such that the following KKT conditions hold:

$$
\begin{align*}
  \left \lbrace
\begin{array}{l}
\dfrac {\partial g \left(\boldsymbol{\xi}, \boldsymbol{\xi}^{\ast} \right)} {\partial {\boldsymbol{\xi}}} + \eta \cdot \nabla _{\boldsymbol{\xi}} c\left(\boldsymbol{\xi} \right) = 0 \\
c\left(\boldsymbol{\xi} \right) \leqslant 0, \eta \geqslant 0, \eta \cdot c\left(\boldsymbol{\xi} \right) = 0
\end{array}
\right.
\end{align*}
$$

where $$c$$ is defined according to (Theo1.1):

$$
c\left(\boldsymbol{\xi} \right) = \dfrac {1} {2} \boldsymbol{\xi}^T \boldsymbol{\xi} - M
$$

Using (Theo2.8)

$$
\begin{align*}
  \left \lbrace
\begin{array}{l}
\nabla _{\boldsymbol{\xi}} \operatorname {E_1} \left ( \boldsymbol{\xi} \right ) - \nabla _{\boldsymbol{\xi}} \operatorname {E_2} \left ( \boldsymbol{\xi}^{\ast}  \right ) + \eta \cdot \nabla _{\boldsymbol{\xi}} c\left(\boldsymbol{\xi} \right) = 0 \\
c\left(\boldsymbol{\xi} \right) \leqslant 0, \eta \geqslant 0, \eta \cdot c\left(\boldsymbol{\xi} \right) = 0
\end{array}
\right.
\end{align*} \tag{Theo2.9}
$$

Since $$\boldsymbol{\xi}^{\ast}$$ is a fixed point

$$
\begin{align*}
  \left \lbrace
\begin{array}{l}
\nabla _{\boldsymbol{\xi}} \operatorname {E_1} \left ( \boldsymbol{\xi}^{\ast} \right ) - \nabla _{\boldsymbol{\xi}} \operatorname {E_2} \left ( \boldsymbol{\xi}^{\ast}  \right ) + \eta \cdot \nabla _{\boldsymbol{\xi}} c\left(\boldsymbol{\xi}^{\ast} \right) = 0 \\
c\left(\boldsymbol{\xi}^{\ast} \right) \leqslant 0, \eta \geqslant 0, \eta \cdot c\left(\boldsymbol{\xi}^{\ast} \right) = 0
\end{array}
\right.
\end{align*} \tag{Theo2.10}
$$

That is

$$
\begin{align*}
  \left \lbrace
\begin{array}{l}
\nabla _{\boldsymbol{\xi}} \operatorname {E} \left ( \boldsymbol{\xi}^{\ast} \right ) + \eta \cdot \nabla _{\boldsymbol{\xi}} c\left(\boldsymbol{\xi}^{\ast} \right) = 0 \\
c\left(\boldsymbol{\xi}^{\ast} \right) \leqslant 0, \eta \geqslant 0, \eta \cdot c\left(\boldsymbol{\xi}^{\ast} \right) = 0
\end{array}
\right.
\end{align*} \tag{Theo2.11}
$$

(Theo2.10) is exactly KKT conditions of $$\operatorname {E}$$ on $$S$$ and therefore, is a stationary point of $$\operatorname {E}$$ on $$S$$.

Suppose

$$
\left \lVert \boldsymbol{\xi}_{t + 1} - \boldsymbol{\xi}_{t} \right \rVert _2 \not \to 0, \text{ as } t \to \infty
$$

Then there exists a $$\varepsilon_{3} > 0$$ and a subsequence

$$
{\left \lbrace \boldsymbol{\xi}_{t_k} \right \rbrace} _{k = 1} ^{\infty}
$$

such that

$$
\left \lVert \boldsymbol{\xi}_{t_k + 1} - \boldsymbol{\xi}_{t_k} \right \rVert _2 \geqslant \varepsilon_{3}, \forall k \geqslant 1 \tag {Theo2.17}
$$

According to (Theo2.5), all points $$\boldsymbol{\xi}_{t_k}, k \geqslant 1$$ are in the compact set $S$. Hence it must have a convergent subsequence

$$
\boldsymbol{\xi}_{t_{k_l}} \to \boldsymbol{\xi}^{\ast}, \text{ as } l \to \infty \tag {Theo2.12}
$$

where $$\boldsymbol{\xi}^{\ast} \in S$$ is a limit point.

Consider subsequence:

$$
{\left \lbrace \boldsymbol{\xi}_{t_{k_l} + 1} \right \rbrace} _{k=1} ^{\infty}
$$

It must also have a convergent subsequence

$$
\boldsymbol{\xi}_{t_{k_{l_m}} + 1} \to \boldsymbol{\xi}^{\ast\ast}, \text{ as } m \to \infty \tag {Theo2.13}
$$

where $$\boldsymbol{\xi}^{\ast\ast} \in S$$ is a limit point.

Using (Theo2.12)

$$
\boldsymbol{\xi}_{t_{k_{l_m}}} \to \boldsymbol{\xi}^{\ast}, \text{ as } l \to \infty \tag {Theo2.14}
$$

Since

$$
\boldsymbol{\xi}_{t_{k_{l_m}} + 1} \in \mathcal{A} \left ( \boldsymbol{\xi}_{t_{k_{l_m}}} \right )
$$

And $$\mathcal{A}$$ is closed on $$S$$, thus

$$
\boldsymbol{\xi}^{\ast\ast} \in \mathcal{A} \left ( \boldsymbol{\xi}^{\ast} \right )
$$

According to theorem 1, $$\operatorname {E} \left ( \boldsymbol{\xi}^{\ast\ast} \right ) = \operatorname {E} \left ( \boldsymbol{\xi}^{\ast} \right )$$.

If $$\boldsymbol{\xi}^{\ast} \neq \boldsymbol{\xi}^{\ast\ast}$$, using (Theo2.6), $$\operatorname {E} \left ( \boldsymbol{\xi}^{\ast\ast} \right ) \lt \operatorname {E} \left ( \boldsymbol{\xi}^{\ast} \right )$$. A contradiction. Therefore $$\boldsymbol{\xi}^{\ast} = \boldsymbol{\xi}^{\ast\ast}$$.

Using (Theo2.13)

$$
\boldsymbol{\xi}_{t_{k_{l_m}} + 1} \to \boldsymbol{\xi}^{\ast}, \text{ as } m \to \infty \tag {Theo2.15}
$$

Using (Theo2.14), (Theo2.15)

$$
\begin{align*}
& \left \lVert \boldsymbol{\xi}_{t_{k_{l_m}} + 1} - \boldsymbol{\xi}_{t_{k_{l_m}}} \right \rVert _2 \\
= & \left \lVert \left(\boldsymbol{\xi}_{t_{k_{l_m}} + 1} - \boldsymbol{\xi}^{\ast}\right) - \left(\boldsymbol{\xi}_{t_{k_{l_m}}} - \boldsymbol{\xi}^{\ast}\right) \right \rVert _2 \\
\leqslant & \left \lVert \boldsymbol{\xi}_{t_{k_{l_m}} + 1} - \boldsymbol{\xi}^{\ast} \right \rVert _2 + \left \lVert \boldsymbol{\xi}_{t_{k_{l_m}}} - \boldsymbol{\xi}^{\ast} \right \rVert _2 \\
\to & 0, \text{ as } m \to \infty \tag {Theo2.16}
\end{align*}
$$

which is in contradiction with (Theo2.17).

Therefore

$$
\left \lVert \boldsymbol{\xi}_{t + 1} - \boldsymbol{\xi}_{t} \right \rVert _2 \to 0, \text{ as } t \to \infty \tag {Theo2.18}
$$

Let $$S_{lim}$$ denote the set of limit points of $${\left \lbrace \text {} {\boldsymbol{\xi}_t} \right \rbrace} _{t=0} ^{\infty}$$.

According to (Theo2.5), all points $$\boldsymbol{\xi}_{t}, t \geqslant 1$$ are in the compact set $S$. Thus $$S_{lim}$$ is not empty and bounded.

If

$$
\exists \boldsymbol{\xi}^{\ast}, \boldsymbol{\xi}^{\ast}_{k} \to \boldsymbol{\xi}^{\ast} \text{ as } k \to \infty \tag {Theo2.19}
$$

where $${\left \lbrace \boldsymbol{\xi}^{\ast}_{k} \right \rbrace} _{k=1} ^{\infty}$$ is a subset of $$S_{lim}$$.

Using the definition of limit,

$$
\forall k \geqslant 1, \exists \boldsymbol{\xi}_{t_k} \in {\left \lbrace \text {} {\boldsymbol{\xi}_t} \right \rbrace} _{t=0} ^{\infty}, \left \lVert \boldsymbol{\xi}_{t_k} -  \boldsymbol{\xi}^{\ast}_{k} \right \rVert _2 < \dfrac {1} {k}
$$

Thus

$$
\left \lVert \boldsymbol{\xi}_{t_k} -  \boldsymbol{\xi}^{\ast}_{k} \right \rVert _2 \to 0, k \to \infty
$$

That is

$$
\boldsymbol{\xi}_{t_k} - \boldsymbol{\xi}^{\ast}_{k} \to \mathbf {0}, k \to \infty
$$

Then

$$
\boldsymbol{\xi}_{t_k} = \left(\boldsymbol{\xi}_{t_k} - \boldsymbol{\xi}^{\ast}_{k} \right) + \boldsymbol{\xi}^{\ast}_{k} \to \boldsymbol{\xi}^{\ast}, k \to \infty
$$

Hence

$$
\boldsymbol{\xi}^{\ast} \in S_{lim}
$$

Therefore $$S_{lim}$$ is closed. It is also bounded, so it is a compact set.

If $${\left \lbrace \text {} {\boldsymbol{\xi}_t} \right \rbrace} _{t=0} ^{\infty}$$ does not converge, $$S_{lim}$$ must contain at least two points.

Suppose $$S_{lim}$$ is not connected. Then it can be decomposed into the union of two nonempty closed sets of points without common points.

Suppose

$$
S_{lim} = S^{1}_{lim} \cup S^{2}_{lim} \tag {Theo2.20}
$$

where $$S^{1}_{lim} \cup S^{2}_{lim}$$ are both nonempty, closed and:

$$
S^{1}_{lim} \cap S^{2}_{lim} = \emptyset \tag {Theo2.22}
$$

Let

$$
d = \inf \left \lbrace { \left \lVert \boldsymbol{\xi}^{1}_{lim} -  \boldsymbol{\xi}^{2}_{lim} \right \rVert _2 } \middle \vert \boldsymbol{\xi}^{1}_{lim} \in S^{1}_{lim}, \boldsymbol{\xi}^{2}_{lim} \in S^{2}_{lim} \right \rbrace \tag {Theo2.23}
$$

If $$d = 0$$, then there is a sequence $${\left \lbrace \boldsymbol{\xi}^{1}_{lim_{k}} \right \rbrace} _{k=1} ^{\infty}$$ that belongs to $$S^{1}_{lim}$$, and a sequence $${\left \lbrace \boldsymbol{\xi}^{2}_{lim_{k}} \right \rbrace} _{k=1} ^{\infty}$$ that belongs to $$S^{2}_{lim}$$, and

$$
\boldsymbol{\xi}^{1}_{lim_{k}} - \boldsymbol{\xi}^{2}_{lim_{k}} \to \mathbf {0}, k \to \infty \tag {Theo2.21}
$$

Because $$S^{1}_{lim}$$ and $$S^{2}_{lim}$$ are closed, each of the sequences  $${\left \lbrace \boldsymbol{\xi}^{1}_{lim_{k}} \right \rbrace} _{k=1} ^{\infty}$$ and $${\left \lbrace \boldsymbol{\xi}^{2}_{lim_{k}} \right \rbrace} _{k=1} ^{\infty}$$ has a convergent subsequence. Using (Theo2.21), two subsequences converge to the same limit point. Then this limit point belongs to both closed set $$S^{1}_{lim}$$ and $$S^{2}_{lim}$$, which is a contradiction with (Theo2.22). Thus $$d > 0$$.

Because $$S^{1}_{lim}$$ and $$S^{2}_{lim}$$ are nonempty, there exists two limit points $$\boldsymbol{\xi}^{\ast 1}_{lim} \in S^{1}_{lim}, \boldsymbol{\xi}^{\ast 2}_{lim} \in S^{2}_{lim}$$.

Suppose

$$
\begin{align*}
& \boldsymbol{\xi}^{1}_{t_k} \to \boldsymbol{\xi}^{\ast 1}_{lim}, \text{ as } k \to \infty \\
& \boldsymbol{\xi}^{2}_{t_k} \to \boldsymbol{\xi}^{\ast 2}_{lim}, \text{ as } k \to \infty
\end{align*} \tag {Theo2.24}
$$

where $${Q}_1 = \left \lbrace \boldsymbol{\xi}^{1}_{t_k} \right \rbrace _{k=0} ^{\infty}$$ and $${Q}_2 = \left \lbrace \boldsymbol{\xi}^{2}_{t_k} \right \rbrace _{k=0} ^{\infty}$$ are subsequences of $${\left \lbrace \text {} {\boldsymbol{\xi}_t} \right \rbrace} _{t=0} ^{\infty}$$.

Using (Theo2.18)

$$
\exists t_d, \forall t > t_d, \left \lVert \boldsymbol{\xi}_{t + 1} - \boldsymbol{\xi}_{t} \right \rVert _2 < \dfrac {d} {3} \tag {Theo2.25}
$$

Let

$$
\begin{align*}
d^1 \left( \boldsymbol{\xi} \right) = \inf \left \lbrace { \left \lVert \boldsymbol{\xi} - \boldsymbol{\xi}^{1}_{lim} \right \rVert _2 } \middle \vert \boldsymbol{\xi} \in {\left \lbrace \text {} {\boldsymbol{\xi}_t} \right \rbrace} _{t=0} ^{\infty}, \boldsymbol{\xi}^{1}_{lim} \in S^{1}_{lim} \right \rbrace \\
d^2 \left( \boldsymbol{\xi} \right) = \inf \left \lbrace { \left \lVert \boldsymbol{\xi} - \boldsymbol{\xi}^{2}_{lim} \right \rVert _2 } \middle \vert \boldsymbol{\xi} \in {\left \lbrace \text {} {\boldsymbol{\xi}_t} \right \rbrace} _{t=0} ^{\infty}, \boldsymbol{\xi}^{2}_{lim} \in S^{1}_{lim} \right \rbrace
\end{align*} \tag {Theo2.26}
$$

Using (Theo2.23), (Theo2.26)

$$
\forall \boldsymbol{\xi} \in {\left \lbrace \text {} {\boldsymbol{\xi}_t} \right \rbrace} _{t=0} ^{\infty}, d^1 \left( \boldsymbol{\xi} \right) + d^2 \left( \boldsymbol{\xi} \right) \geqslant d \tag {Theo2.27}
$$

Using (Theo2.24)

$$
\exists m > t_d, d^1\left( \boldsymbol{\xi}_{m} \right) < \dfrac {d} {3} \\
\exists n >   m, d^2 \left( \boldsymbol{\xi}_{n} \right) < \dfrac {d} {3}
\tag {Theo2.28}
$$

Let index sequence

$$
I = \left \lbrace m \leqslant i \leqslant n \right \rbrace \tag {Theo2.29}
$$

Using (Theo2.27), (Theo2.28)

$$
d^2 \left( \boldsymbol{\xi}_{m} \right) \geqslant \dfrac {2} {3}d \\
d^1 \left( \boldsymbol{\xi}_{n} \right) \geqslant \dfrac {2} {3}d
\tag {Theo2.30}
$$

Using (Theo2.28), (Theo2.29), (Theo2.30)

$$
\exists t_{k_1} = \min \left \lbrace i \in I \middle \vert d^1 \left( \boldsymbol{\xi}_{i} \right) \geqslant \dfrac {d} {3} \right \rbrace
$$

Obviously:

$$
\begin{align*}
& t_{k_1} > m \\
& d^1 \left( \boldsymbol{\xi}_{t_{k_1} } \right) \geqslant \dfrac {d} {3} \\
& d^1 \left( \boldsymbol{\xi}_{t_{k_1} - 1} \right) < \dfrac {d} {3}
\end{align*} \tag {Theo2.31}
$$

Using (Theo2.27), (Theo2.31)

$$
d^2 \left( \boldsymbol{\xi}_{t_{k_1} - 1} \right) \geqslant\dfrac {2} {3}d  \tag {Theo2.32}
$$

Using (Theo2.25), (Theo2.32)

$$
d^2 \left( \boldsymbol{\xi}_{t_{k_1}} \right) \geqslant\dfrac {d} {3} \tag {Theo2.33}
$$

Using (Theo2.31), (Theo2.33),

$$
\begin{align*}
    \left .
    \begin{array}{l}
    \boldsymbol{\xi}_{t_{k_1}} \not \in S^{1}_{lim} \\
    \boldsymbol{\xi}_{t_{k_1}} \not \in S^{2}_{lim}
    \end{array}
    \right \rbrace
    \implies \boldsymbol{\xi}_{t_{k_1}} \not \in S^{1}_{lim} \cup S^{2}_{lim}
\end{align*} \tag {Theo2.34}
$$

Follow this way, there exists therefore an infinite sequence of $$k_1, k_2, \cdots$$ for which (Theo2.34) holds. Threfore all of its convergent subsequences converge to limit points for which (Theo2.34) holds, which is in contradiction with (Theo2.20). Therefore $$S_{lim}$$ is connected.
