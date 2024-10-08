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
\vec{\mathbf {p}} = \operatorname{softmax}\left(\beta \vec{\mathbf {x}} \right) \\

p_i = \left[\operatorname{softmax}\left(\beta \vec{\mathbf {x}} \right) \right]_i = \dfrac {\exp \left( {\beta x_i} \right)} {\sum_{k=1}^{N} \exp \left( {\beta x_k} \right)}
$$

where ${\vec{\mathbf {x}}}_i \in \mathbb {R}^{N}$.

### Log-Sum-Exp Function

$$
\operatorname{lse} \left ( \beta, \vec{\mathbf {x}} \right ) = \beta^{-1} \ln \left( {\sum_{k=1}^{N} \exp \left( {\beta x_k} \right)} \right)
$$

where ${\vec{\mathbf {x}}}_i \in \mathbb {R}^{N}$.

## Lemma 1
$$
\nabla _{\vec{\mathbf {x}}} \operatorname{lse} \left ( \beta, \vec{\mathbf {x}} \right ) = \operatorname{softmax}\left(\beta \vec{\mathbf {x}} \right)
$$

## Lemma 2
The Jacobian $J_s$ of $\vec{\mathbf {p}}=\operatorname{softmax}\left(\beta \vec{\mathbf {x}} \right) $ is

$$
J_s = \dfrac {\partial \operatorname{softmax}\left(\beta \vec{\mathbf {x}} \right)} {\partial \vec{\mathbf {x}}} = \beta \left(\operatorname{diag}\left(\vec{\mathbf {p}}\right) - \vec{\mathbf {p}}\vec{\mathbf {p}}^T \right)
$$

The Jacobian $J$ of $\vec{\mathbf {p}}=\operatorname{softmax}\left(\beta \boldsymbol{X}^T \boldsymbol{\xi} \right) $ is

$$
J = \dfrac {\partial \operatorname{softmax}\left(\beta \boldsymbol{X}^T\boldsymbol{\xi} \right)} {\partial \vec{\mathbf {x}}} = \beta \boldsymbol{X} \left(\operatorname{diag}\left(\vec{\mathbf {p}}\right) - \vec{\mathbf {p}}\vec{\mathbf {p}}^T \right) \boldsymbol{X}^T = \boldsymbol{X} J_s \boldsymbol{X}^T
$$

## Lemma 3
The Jacobian $J_s$ of $\vec{\mathbf {p}}=\operatorname{softmax}\left(\beta \vec{\mathbf {x}} \right) $ is symmetric and positive semi-definite.

### Proof
For any arbitrary $\vec{\mathbf {z}}$, we have

$$
\vec{\mathbf {z}}^T \left(\operatorname{diag}\left(\vec{\mathbf {p}}\right) - \vec{\mathbf {p}}\vec{\mathbf {p}}^T \right) \vec{\mathbf {z}} = \sum_{i} p_i {z_i}^2 - \left({\sum_{i} p_i z_i}\right)^2 \geqslant 0
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
    \left \{
    \begin{array}{l}
        {\vec{\mathbf {x}}}_k \to {{\vec{\mathbf {x}}}_{0}} \text{ as } k \to \infty \\
        \vec{\mathbf {y}}_k \to {\vec{\mathbf {y}}_{0}} \text{ as } k \to \infty \\
        {\vec{\mathbf {x}}}_k \in X \\
        \vec{\mathbf {y}}_k \in \mathcal{A} \left({\vec{\mathbf {x}}}_k \right)
    \end{array}
    \right\} \implies {\vec{\mathbf {y}}_{0}} \in \mathcal{A} \left({{\vec{\mathbf {x}}}_{0}} \right)
\end{align*}
$$

A point-to-set map $\mathcal{A}$ is said to be closed on $S \subset X$ if it is closed at every point of $S$.

### Fixed Point

A fixed point of the map

$$
\mathcal{A}: X \to \mathscr{P}(X)
$$

is any point $\vec{\mathbf {x}} \in X$ for which

$$
\mathcal{A} \left( \vec{\mathbf {x}} \right) = \left \{ \vec{\mathbf {x}} \right \}
$$

A generalized fixed point of $\mathcal{A}$ is any point $\vec{\mathbf {x}} \in X$ for which

$$
\vec{\mathbf {x}} \in \mathcal{A} \left( \vec{\mathbf {x}} \right)
$$

### Uniformly Compact

$\mathcal{A}$ is said to be uniformly compact on $X$ if there exists a compact set $H$ independent of $\vec{\mathbf {x}}$ such that:

$$
\forall \vec{\mathbf {x}} \in X, \mathcal{A} \left( \vec{\mathbf {x}} \right) \subset H
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
\forall \vec{\mathbf {x}} \in X, \forall \vec{\mathbf {y}} \in \mathcal{A} \left( \vec{\mathbf {x}} \right), l \left( \vec{\mathbf {y}} \right) \leqslant l \left( \vec{\mathbf {x}} \right)
$$

If, in addition,

$$
\forall \vec{\mathbf {x}} \in X, \forall \vec{\mathbf {y}} \in \mathcal{A} \left( \vec{\mathbf {x}} \right), l \left( \vec{\mathbf {y}} \right) = l \left( \vec{\mathbf {x}} \right) \implies \vec{\mathbf {y}} = \vec{\mathbf {x}}
$$

Then $\mathcal{A}$ is said to be strictly monotonic with respect to $l$.

### Global Convergence
Let $X$ be a set and ${{\vec{\mathbf{x}}}_{0}} \in X$ a given point. Then an algorithm, $\mathcal{A}$, with initial point ${{\vec{\mathbf {x}}}_{0}}$ is a point-to-set map which generates a sequence $\left \{{\vec{\mathbf {x}}}_t \right \}_{t=0} ^{\infty}$ via the rule

$$
{\vec{\mathbf {x}}}_{t + 1} \in \mathcal{A} \left ({\vec{\mathbf {x}}}_t \right ), t = 0, 1, \cdots
$$

$\mathcal{A}$ is said to be globally convergent if: For any chosen initial point ${{\vec{\mathbf {x}}}_{0}}$, the sequence $\left \{{\vec{\mathbf {x}}}_t \right \}_{t=0} ^{\infty}$ generated by ${\vec{\mathbf {x}}}_{t + 1} \in \mathcal{A} \left ({\vec{\mathbf {x}}}_t \right )$ (or a subsequence) converges to a point for which a necessary condition of optimality holds.

## Modern Hopfield Network

We have patterns that are represented by the matrix:
$$
\boldsymbol{X} = \left({\vec{\mathbf {x}}}_1, \dots, {\vec{\mathbf {x}}}_N \right)
$$

where ${\vec{\mathbf {x}}}_i \in \mathbb {R}^{d}$.
The largest norm of a pattern is:

$$
M = \max_{i \in \left[ N \right]} \left \lVert {\vec{\mathbf {x}}}_i \right \rVert _2
$$

The query or state of the Hopfield Network is $\boldsymbol{\xi} \in \mathbb {R}^{d}$.
Define energy $\operatorname {E} \left ( \boldsymbol{\xi}  \right )$ for a continuous query or state $\boldsymbol{\xi}$:
$$
\operatorname {E} \left ( \boldsymbol{\xi}  \right ) = - \operatorname{lse} \left ( \beta, \boldsymbol{X}^T \boldsymbol{\xi}  \right ) + \dfrac {1} {2} \boldsymbol{\xi}^T \boldsymbol{\xi} + \beta^{-1} \ln N + \dfrac {1} {2} M^2 \tag {1}
$$

## New Update Rule
$$
\boldsymbol{\xi}^{t + 1} = \mathcal{F} \left ( \boldsymbol{\xi}^{t} \right ) = \boldsymbol{X}\vec{\mathbf {p}} = \boldsymbol{X} \operatorname{softmax}\left(\beta \boldsymbol{X}^T {\boldsymbol{\xi}^{t}} \right)  \tag {2}
$$

where

$$
\vec{\mathbf {p}} = \operatorname{softmax}\left(\beta \boldsymbol{X}^T {\boldsymbol{\xi}^{t}} \right)
$$

## Theorem 1 Global Convergence

The update rule (2) converges globally: For $\boldsymbol{\xi}^{t+ 1} = \mathcal{F} \left ( \boldsymbol{\xi}^{t} \right )$, the energy $\operatorname {E} \left ( \boldsymbol{\xi}^{t} \right ) \to \operatorname {E} \left ( \boldsymbol{\xi}^{\text{*}} \right )$ for $t \to \infty $ and one accumulation point $\boldsymbol{\xi}^{\text{*}}$.


### Proof

$$
\left \lVert {\boldsymbol{\xi}^{t + 1}} \right \rVert _2
= \left \lVert {\boldsymbol{X}\vec{\mathbf {p}}} \right \rVert _2
= \left \lVert {\sum_{i=1}^{N} p_i {\vec{\mathbf {x}}}_i} \right \rVert _2
\leqslant \sum_{i=1}^{N} p_i \left \lVert {{\vec{\mathbf {x}}}_i} \right \rVert _2
\leqslant \sum_{i=1}^{N} p_i M = M
$$

Hence $\boldsymbol{\xi}^{t + 1}$ is in the sphere

$$
S = \left \{\vec{\mathbf {x}} | \left \lVert {\vec{\mathbf {x}}} \right \rVert _2 \leqslant M \right \}
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
\dfrac {\partial g(\boldsymbol{\xi}, \boldsymbol{\xi}^t)} {\partial {\boldsymbol{\xi}}} = \boldsymbol{\xi} - \nabla _{\boldsymbol{\xi}} \operatorname {E_2} \left ( \boldsymbol{\xi}^{t}  \right ) = \boldsymbol{\xi} - \boldsymbol{X} \operatorname{softmax}\left(\beta \boldsymbol{X}^T {\boldsymbol{\xi}}^t \right) = \vec {\mathbf {0}}
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
