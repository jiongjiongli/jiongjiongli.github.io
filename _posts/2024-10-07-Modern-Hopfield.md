---
layout: post
title: Modern Hopfield Network
---

## Notations
### Common Notations

$$
\text{The }p\text{-norm of a vector is denoted} \left \lVert {\cdot} \right \rVert _p\text{,} 1 \leqslant p\text{.} \\
\beta > 0, \beta \in \mathbb {R} \\
\left[ N \right] = \left\{1, \cdots, N \right\}
$$

### Softmax Function

$$
\text {}{\mathbf {p}} = \operatorname{softmax}\left(\beta \text {}{\mathbf {x}} \right) \\

p_i = \left[\operatorname{softmax}\left(\beta \text {}{\mathbf {x}} \right) \right]_i = \dfrac {\exp \left( {\beta x_i} \right)} {\sum_{k=1}^{N} \exp \left( {\beta x_k} \right)}
$$

where $\text {} {\mathbf {x}_{i}} \in \mathbb {R}^{N}$.

### Log-Sum-Exp Function

$$
\operatorname{lse} \left ( \beta, \text {}{\mathbf {x}} \right ) = \beta^{-1} \ln \left( {\sum_{k=1}^{N} \exp \left( {\beta x_k} \right)} \right)
$$

where $\text {} {\mathbf {x}_{i}} \in \mathbb {R}^{N}$.

## Lemma 1
$$
\nabla _{\text {}{\mathbf {x}}} \operatorname{lse} \left ( \beta, \text {}{\mathbf {x}} \right ) = \operatorname{softmax}\left(\beta \text {}{\mathbf {x}} \right)
$$

## Lemma 2
The Jacobian $J_s$ of $\text {}{\mathbf {p}}=\operatorname{softmax}\left(\beta \text {}{\mathbf {x}} \right) $ is

$$
J_s = \dfrac {\partial \operatorname{softmax}\left(\beta \text {}{\mathbf {x}} \right)} {\partial \text {}{\mathbf {x}}} = \beta \left(\operatorname{diag}\left(\text {}{\mathbf {p}}\right) - \text {}{\mathbf {p}}\text {}{\mathbf {p}}^T \right)
$$

The Jacobian $J$ of $\text {}{\mathbf {p}}=\operatorname{softmax}\left(\beta \boldsymbol{X}^T \boldsymbol{\xi} \right) $ is

$$
J = \dfrac {\partial \operatorname{softmax}\left(\beta \boldsymbol{X}^T\boldsymbol{\xi} \right)} {\partial \text {}{\mathbf {x}}} = \beta \boldsymbol{X} \left(\operatorname{diag}\left(\text {}{\mathbf {p}}\right) - \text {}{\mathbf {p}}\text {}{\mathbf {p}}^T \right) \boldsymbol{X}^T = \boldsymbol{X} J_s \boldsymbol{X}^T
$$

## Lemma 3
The Jacobian $J_s$ of $\text {}{\mathbf {p}}=\operatorname{softmax}\left(\beta \text {}{\mathbf {x}} \right) $ is symmetric and positive semi-definite.

### Proof
For any arbitrary $\text {}{\mathbf {z}}$, we have

$$
\text {}{\mathbf {z}}^T \left(\operatorname{diag}\left(\text {}{\mathbf {p}}\right) - \text {}{\mathbf {p}}\text {}{\mathbf {p}}^T \right) \text {}{\mathbf {z}} = \sum_{i} p_i {z_i}^2 - \left({\sum_{i} p_i z_i}\right)^2 \geqslant 0
$$

## Definition

### Point-to-set Map

A point-to-set map $\mathcal{A}$ from a set $X$ into a set $Y$ is defined as

$$
\mathcal{A}: X \to \mathscr{P}(Y)
$$

which assigns a subset of $Y$ to each point of $X$, where $\mathscr{P}(Y)$ denotes the power set of $Y$.

### Closed

Suppose $X$ and $Y$ are two topological spaces. A point-to-set map $\mathcal{A}$ is said to be closed at $x_0 \in X$ if:

$$
\begin{align*}
    \left .
    \begin{array}{l}
        \text {} {\mathbf {x}_{k}} \to \text {} {\mathbf {x}_{0}} \text{ as } k \to \infty \\
        \text {} {\mathbf {y}_{k}} \to \text {} {\mathbf {y}_{0}} \text{ as } k \to \infty \\
        \text {} {\mathbf {x}_{k}} \in X \\
        \text {} {\mathbf {y}_{k}} \in \mathcal{A} \left(\text {} {\mathbf {x}_{k}} \right)
    \end{array}
    \right\} \implies \text {} {\mathbf {y}_{0}} \in \mathcal{A} \left(\text {} {\mathbf {x}_{0}} \right)
\end{align*}
$$

A point-to-set map $\mathcal{A}$ is said to be closed on $S \subset X$ if it is closed at every point of $S$.

### Fixed Point

A fixed point of the map

$$
\mathcal{A}: X \to \mathscr{P}(X)
$$

is any point $\text {}{\mathbf {x}} \in X$ for which

$$
\mathcal{A} \left( \text {}{\mathbf {x}} \right) = \left \{ \text {}{\mathbf {x}} \right \}
$$

A generalized fixed point of $\mathcal{A}$ is any point $\text {}{\mathbf {x}} \in X$ for which

$$
\text {}{\mathbf {x}} \in \mathcal{A} \left( \text {}{\mathbf {x}} \right)
$$

### Uniformly Compact

$\mathcal{A}$ is said to be uniformly compact on $X$ if there exists a compact set $H$ independent of $\text {}{\mathbf {x}}$ such that:

$$
\forall \text {}{\mathbf {x}} \in X, \mathcal{A} \left( \text {}{\mathbf {x}} \right) \subset H
$$

### Monotonic

Let

$$
l: X \to \mathbb {R}
$$

be a continuous function. The map

$$
\mathcal{A}: X \to \mathscr{P}(X)
$$

is said to be monotonic with respect to $l$ if

$$
\forall \text {}{\mathbf {x}} \in X, \forall \text {}{\mathbf {y}} \in \mathcal{A} \left( \text {}{\mathbf {x}} \right), l \left( \text {}{\mathbf {y}} \right) \leqslant l \left( \text {}{\mathbf {x}} \right)
$$

If, in addition,

$$
\forall \text {}{\mathbf {x}} \in X, \forall \text {}{\mathbf {y}} \in \mathcal{A} \left( \text {}{\mathbf {x}} \right), l \left( \text {}{\mathbf {y}} \right) = l \left( \text {}{\mathbf {x}} \right) \implies \text {}{\mathbf {y}} = \text {}{\mathbf {x}}
$$

Then $\mathcal{A}$ is said to be strictly monotonic with respect to $l$.

### Global Convergence
Let $X$ be a set and $\text {} {\mathbf {x}_{0}} \in X$ a given point. Then an algorithm, $\mathcal{A}$, with initial point $\text {} {\mathbf {x}_{0}}$ is a point-to-set map which generates a sequence ${\left \lbrace \text {} {\mathbf {x}_{t}} \right \rbrace} _{t=0} ^{\infty}$ via the rule

$$
\text {}{\mathbf {x}_{t + 1}} \in \mathcal{A} \left (\text {} {\mathbf {x}_{t}} \right ), t = 0, 1, \cdots
$$

$\mathcal{A}$ is said to be globally convergent if: For any chosen initial point $\text {} {\mathbf {x}_{0}}$, the sequence ${\left \lbrace \text {} {\mathbf {x}_{t}} \right \rbrace} _{t=0} ^{\infty}$ generated by $\text {}{\mathbf {x}_{t + 1}} \in \mathcal{A} \left (\text {} {\mathbf {x}_{t}} \right )$ (or a subsequence) converges to a point for which a necessary condition of optimality holds.

## Modern Hopfield Network

We have patterns that are represented by the matrix:
$$
\boldsymbol{X} = \left(\text {} {\mathbf {x}_{1}}, \dots, \text {}{\mathbf {x}_{N}} \right)
$$

where $\text {} {\mathbf {x}_{i}} \in \mathbb {R}^{d}$.
The largest norm of a pattern is:

$$
M = \max_{i \in \left[ N \right]} \left \lVert \text {} {\mathbf {x}_{i}} \right \rVert _2
$$

The query or state of the Hopfield Network is $\boldsymbol{\xi} \in \mathbb {R}^{d}$.
Define energy $\operatorname {E} \left ( \boldsymbol{\xi}  \right )$ for a continuous query or state $\boldsymbol{\xi}$:
$$
\operatorname {E} \left ( \boldsymbol{\xi}  \right ) = - \operatorname{lse} \left ( \beta, \boldsymbol{X}^T \boldsymbol{\xi}  \right ) + \dfrac {1} {2} \boldsymbol{\xi}^T \boldsymbol{\xi} + \beta^{-1} \ln N + \dfrac {1} {2} M^2 \tag {1}
$$

## New Update Rule
$$
\boldsymbol{\xi}^{t + 1} = \mathcal{F} \left ( \boldsymbol{\xi}^{t} \right ) = \boldsymbol{X}\text {}{\mathbf {p}} = \boldsymbol{X} \operatorname{softmax}\left(\beta \boldsymbol{X}^T {\boldsymbol{\xi}^{t}} \right)  \tag {2}
$$

where

$$
\text {}{\mathbf {p}} = \operatorname{softmax}\left(\beta \boldsymbol{X}^T {\boldsymbol{\xi}^{t}} \right)
$$

## Theorem 1 Global Convergence

The update rule (2) converges globally: For $\boldsymbol{\xi}^{t+ 1} = \mathcal{F} \left ( \boldsymbol{\xi}^{t} \right )$, the energy $\operatorname {E} \left ( \boldsymbol{\xi}^{t} \right ) \to \operatorname {E} \left ( \boldsymbol{\xi}^{\ast} \right )$ for $t \to \infty $ and one accumulation point $\boldsymbol{\xi}^{\ast}$.


### Proof

$$
{\left \lVert {\boldsymbol{\xi}^{t + 1}} \right \rVert} _2
= {\left \lVert {\boldsymbol{X}\text {}{\mathbf {p}}} \right \rVert} _2
= {\left \lVert {\sum_{i=1}^{N} p_i \text {} {\mathbf {x}_{i}}} \right \rVert} _2
\leqslant {\sum_{i=1}^{N} p_i \left \lVert \text {} {\mathbf {x}_{i}} \right \rVert} _2
\leqslant \sum_{i=1}^{N} p_i M
= M
$$

Hence $\boldsymbol{\xi}^{t + 1}$ is in the sphere

$$
S = \left \{\text {}{\mathbf {x}} | \left \lVert {\text {}{\mathbf {x}}} \right \rVert _2 \leqslant M \right \}
$$

which is a convex and compact set.

The Jacobian of the $\operatorname{softmax}$ is positive semi-definite according to Lemma 3. The Jacobian of the $\operatorname{softmax}$ is Hessian of the $\operatorname{lse}$, therefore $\operatorname{lse}$ is a convex.
Hence the energy function $\operatorname {E} \left ( \boldsymbol{\xi}  \right )$ is the difference of two convex functions $\operatorname {E_1} \left ( \boldsymbol{\xi}  \right )$ and $\operatorname {E_2} \left ( \boldsymbol{\xi}  \right )$:
$$
\begin{align*}
\operatorname {E} \left ( \boldsymbol{\xi}  \right ) &= \operatorname {E_1} \left ( \boldsymbol{\xi}  \right ) - \operatorname {E_2} \left ( \boldsymbol{\xi}  \right ) \\
\operatorname {E_1} \left ( \boldsymbol{\xi}  \right ) &= \dfrac {1} {2} \boldsymbol{\xi}^T \boldsymbol{\xi} + \beta^{-1} \ln N + \dfrac {1} {2} M^2 = \dfrac {1} {2} \boldsymbol{\xi}^T \boldsymbol{\xi} + C_1 \\
\operatorname {E_2} \left ( \boldsymbol{\xi}  \right ) &= \operatorname{lse} \left ( \beta, \boldsymbol{X}^T \boldsymbol{\xi}  \right )
\end{align*}
$$

where $C_1$ does not depend on $\boldsymbol{\xi}$.

Define minimization problem:

$$
\min _{\boldsymbol{\xi}} \operatorname {E} \left ( \boldsymbol{\xi}  \right ) = \min _{\boldsymbol{\xi}} \left ( \operatorname {E_1} \left ( \boldsymbol{\xi}  \right ) - \operatorname {E_2} \left ( \boldsymbol{\xi}  \right ) \right )
$$

Let

$$
\nabla _{\boldsymbol{\xi}} \operatorname {E_1} \left ( \boldsymbol{\xi}^{t + 1} \right ) = \nabla _{\boldsymbol{\xi}} \operatorname {E_2} \left ( \boldsymbol{\xi}^{t}  \right )
$$

The resulting update rule is:

$$
\boldsymbol{\xi}^{t + 1} = \boldsymbol{X} \operatorname{softmax}\left(\beta \boldsymbol{X}^T {\boldsymbol{\xi}}^t \right)
$$

Let

$$
\mathcal{A} \left ( \boldsymbol{\xi}^{t } \right ) = \left \{ \boldsymbol{X} \operatorname{softmax}\left(\beta \boldsymbol{X}^T {\boldsymbol{\xi}^{t}} \right) \right \}
$$

Therefore $\mathcal{A}$ is monotonic with respect to $\operatorname {E}$.

The point-set-map $\mathcal{A}$ is uniformly compact on $S$.

According to Lemma 4,

Let
$$
g(\boldsymbol{\xi}, \boldsymbol{\xi}^t) = \operatorname {E_1} \left ( \boldsymbol{\xi}  \right ) - \operatorname {E_2} \left ( \boldsymbol{\xi}^{t}  \right ) - \left ( \nabla _{\boldsymbol{\xi}} \operatorname {E_2} \left ( \boldsymbol{\xi}^{t}  \right ) \right )^T \left ( \boldsymbol{\xi} - \boldsymbol{\xi}^{t} \right )
$$

Since $\operatorname {E_2}$ is convex, the first order characterization of convexity holds:

$$
\operatorname {E_2} \left ( \boldsymbol{\xi}  \right ) \geqslant \operatorname {E_2} \left ( \boldsymbol{\xi}^{t}  \right ) + \left ( \nabla _{\boldsymbol{\xi}} \operatorname {E_2} \left ( \boldsymbol{\xi}^{t}  \right ) \right )^T \left ( \boldsymbol{\xi} - \boldsymbol{\xi}^{t} \right )
$$

Therefore:

$$
\begin{align*}
\operatorname {E} \left ( \boldsymbol{\xi}  \right ) &= \operatorname {E_1} \left ( \boldsymbol{\xi}  \right ) - \operatorname {E_2} \left ( \boldsymbol{\xi}  \right ) \\
& \leqslant \operatorname {E_1} \left ( \boldsymbol{\xi}  \right ) - \operatorname {E_2} \left ( \boldsymbol{\xi}^{t}  \right ) - \left ( \nabla _{\boldsymbol{\xi}} \operatorname {E_2} \left ( \boldsymbol{\xi}^{t}  \right ) \right )^T \left ( \boldsymbol{\xi} - \boldsymbol{\xi}^{t} \right ) \\
&= g(\boldsymbol{\xi}, \boldsymbol{\xi}^t) \\
&= \operatorname {E_1} \left ( \boldsymbol{\xi}  \right ) - \left ( \nabla _{\boldsymbol{\xi}} \operatorname {E_2} \left ( \boldsymbol{\xi}^{t}  \right ) \right )^T \boldsymbol{\xi} + C_2
\end{align*}
$$

where $C_2$ does not depend on $\boldsymbol{\xi}$.
Because

$$
\begin{align*}
\dfrac {\partial g(\boldsymbol{\xi}, \boldsymbol{\xi}^t)} {\partial {\boldsymbol{\xi}}}  &= \nabla _{\boldsymbol{\xi}} \operatorname {E_1} \left ( \boldsymbol{\xi} \right ) - \nabla _{\boldsymbol{\xi}} \operatorname {E_2} \left ( \boldsymbol{\xi}^{t}  \right ) = \boldsymbol{\xi} - \nabla _{\boldsymbol{\xi}} \operatorname {E_2} \left ( \boldsymbol{\xi}^{t}  \right ) \\
\dfrac {\partial ^2 g(\boldsymbol{\xi}, \boldsymbol{\xi}^t)} {\partial {\boldsymbol{\xi} ^2}} &= I
\end{align*}
$$

The Hessian is strict positive definite everywhere, therefore $g(\boldsymbol{\xi}, \boldsymbol{\xi}^t)$ is strict convex (if the domain is convex) and there exist only one minimum, which is the global minimum.
Let

$$
\dfrac {\partial g(\boldsymbol{\xi}, \boldsymbol{\xi}^t)} {\partial {\boldsymbol{\xi}}} = \boldsymbol{\xi} - \nabla _{\boldsymbol{\xi}} \operatorname {E_2} \left ( \boldsymbol{\xi}^{t}  \right ) = \boldsymbol{\xi} - \boldsymbol{X} \operatorname{softmax}\left(\beta \boldsymbol{X}^T {\boldsymbol{\xi}}^t \right) = \text {} {\mathbf {0}}
$$

The minimum is:

$$
\boldsymbol{\xi}^{t + 1} = \underset{\boldsymbol{\xi}} {\operatorname{argmin}} g(\boldsymbol{\xi}, \boldsymbol{\xi}^t) = \boldsymbol{X} \operatorname{softmax}\left(\beta \boldsymbol{X}^T {\boldsymbol{\xi}}^t \right)
$$

Hence

$$
\text { if } \boldsymbol{\xi}^{t + 1} \neq \boldsymbol{\xi}^t, g(\boldsymbol{\xi}^{t + 1}, \boldsymbol{\xi}^t) \lt g(\boldsymbol{\xi}^{t}, \boldsymbol{\xi}^t)
$$

Therefore

$$
\text { if } \boldsymbol{\xi}^{t + 1} \neq \boldsymbol{\xi}^t, \operatorname {E} \left ( \boldsymbol{\xi}^{t + 1} \right ) \leqslant g(\boldsymbol{\xi}^{t + 1}, \boldsymbol{\xi}^t) \lt g(\boldsymbol{\xi}^{t}, \boldsymbol{\xi}^t) = \operatorname {E} \left ( \boldsymbol{\xi}^t  \right )
$$

Let

$$
\mathcal{A} \left ( \boldsymbol{\xi}^{t } \right ) = \left \{ \boldsymbol{X} \operatorname{softmax}\left(\beta \boldsymbol{X}^T {\boldsymbol{\xi}^{t}} \right) \right \}
$$

Thus

$$
\forall \boldsymbol{\xi}^{t + 1} \in \mathcal{A} \left ( \boldsymbol{\xi}^t \right ), \text { if } \boldsymbol{\xi}^{t + 1} \neq \boldsymbol{\xi}^t, \operatorname {E} \left ( \boldsymbol{\xi}^{t + 1} \right ) \lt \operatorname {E} \left ( \boldsymbol{\xi}^t \right )
$$

Therefore $\mathcal{A}$ is strictly monotonic with respect to $\operatorname {E}$.

The point-set-map $\mathcal{A}$ is uniformly compact on $S$.

$\mathcal{A}$ is closed.
