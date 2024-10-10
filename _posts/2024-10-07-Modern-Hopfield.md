---
layout: post
title: Modern Hopfield Network
---

## Notations
1. The $$p$$-norm of a vector is denoted: $$\left \lVert {\cdot} \right \rVert _p\text{,} 1 \leqslant p$$

2. Let $$\beta > 0, \beta \in \mathbb {R}$$

3. Let $$\left[ N \right] = \left\{1, \cdots, N \right\}$$

## Softmax Function

$$
\begin{align*}
&\text {}{\mathbf {p}} \left(\text {}{\mathbf {x}} \right) = \operatorname{softmax}\left(\beta \text {}{\mathbf {x}} \right) \\
&p_i = \left[\operatorname{softmax}\left(\beta \text {}{\mathbf {x}} \right) \right]_i = \dfrac {\exp \left( {\beta x_i} \right)} {\sum_{k=1}^{N} \exp \left( {\beta x_k} \right)}
\end{align*}
$$

where $\text {} {\mathbf {x}_{i}} \in \mathbb {R}^{N}$.

## Log-Sum-Exp Function

$$
\operatorname{lse} \left ( \beta, \text {}{\mathbf {x}} \right ) = \beta^{-1} \ln \left( {\sum_{k=1}^{N} \exp \left( {\beta x_k} \right)} \right)
$$

where $\text {} {\mathbf {x}_{i}} \in \mathbb {R}^{N}$.

## Lemma 1
$$
\nabla _{\text {}{\mathbf {x}}} \operatorname{lse} \left ( \beta, \text {}{\mathbf {x}} \right ) = \operatorname{softmax}\left(\beta \text {}{\mathbf {x}} \right)
$$

where $\text {} {\mathbf {x}} \in \mathbb {R}^{N}$.

$$
\nabla _{\text {}{\boldsymbol{\xi}}} \operatorname{lse} \left ( \beta, \boldsymbol{X}^T \boldsymbol{\xi}  \right ) = \boldsymbol{X} \operatorname{softmax}\left(\beta \text {}{\boldsymbol{X}^T \boldsymbol{\xi}} \right)
$$

where $$\text {} {\boldsymbol{X}} \in \mathbb {R}^{d \times N}, \text {} {\boldsymbol{\xi}} \in \mathbb {R}^{d}$$.
## Lemma 2
The Jacobian $J_s \left(\text {}{\mathbf {x}} \right)$ of $$ \text {}{\mathbf {p}} \left(\text {}{\mathbf {x}} \right)= \operatorname{softmax}\left(\beta \text {}{\mathbf {x}} \right) $$ is

$$
J_s \left(\text {}{\mathbf {x}} \right) = \dfrac {\partial \operatorname{softmax}\left(\beta \text {}{\mathbf {x}} \right)} {\partial \text {}{\mathbf {x}}} = \beta \left(\operatorname{diag}\left(\text {}{\mathbf {p}}\right) - \text {}{\mathbf {p}}\text {}{\mathbf {p}}^T \right)
$$

where $\text {} {\mathbf {x}} \in \mathbb {R}^{N}$.
The Jacobian $J \left(\boldsymbol{\xi} \right)$ of $$\text {} {\boldsymbol{X}} \text {}{\mathbf {p}} \left(\boldsymbol{X}^T \boldsymbol{\xi} \right)= \text {} {\boldsymbol{X}} \operatorname{softmax}\left(\beta \boldsymbol{X}^T \boldsymbol{\xi} \right) $$ is
$$
J  \left(\boldsymbol{\xi} \right) = \dfrac {\partial \left( \text {} {\boldsymbol{X}} \operatorname{softmax}\left(\beta \boldsymbol{X}^T\boldsymbol{\xi} \right) \right)} {\partial \text {}{\boldsymbol{\xi}}} = \beta \boldsymbol{X} \left(\operatorname{diag}\left(\text {}{\mathbf {p}}\right) - \text {}{\mathbf {p}}\text {}{\mathbf {p}}^T \right) \boldsymbol{X}^T = \boldsymbol{X} J_s \boldsymbol{X}^T
$$

where $$\text {} {\boldsymbol{X}} \in \mathbb {R}^{d \times N}, \text {} {\boldsymbol{\xi}} \in \mathbb {R}^{d}$$.
## Lemma 3
The Jacobian $J_s \left(\text {}{\mathbf {x}} \right)$ of $\text {}{\mathbf {p}} \left(\text {}{\mathbf {x}} \right)=\operatorname{softmax}\left(\beta \text {}{\mathbf {x}} \right) $ is symmetric and positive semi-definite where $\text {} {\mathbf {x}} \in \mathbb {R}^{N}$.
The Jacobian $J  \left(\boldsymbol{\xi} \right)$ of $$\text {} {\boldsymbol{X}} \text {}{\mathbf {p}} \left(\boldsymbol{X}^T \boldsymbol{\xi} \right)=\text {} \boldsymbol{X} \operatorname{softmax}\left(\beta \boldsymbol{X}^T \boldsymbol{\xi} \right) $$ is symmetric and positive semi-definite where $$\text {} {\boldsymbol{X}} \in \mathbb {R}^{d \times N}, \text {} {\boldsymbol{\xi}} \in \mathbb {R}^{d}$$.

### Proof
According to Lemma 2, obviously they are symmetric.
For any arbitrary $\text {}{\mathbf {x}} \in \mathbb {R}^{N}$, we have

$$
\text {}{\mathbf {x}}^T J_s \text {}{\mathbf {x}} = \beta \text {}{\mathbf {x}}^T \left(\operatorname{diag}\left(\text {}{\mathbf {p}}\right) - \text {}{\mathbf {p}}\text {}{\mathbf {p}}^T \right) \text {}{\mathbf {x}}
= \beta \left[ \sum_{i} p_i {x_i}^2 - \left({\sum_{i} p_i x_i}\right)^2 \right]
\geqslant 0
$$

For any arbitrary $\text {} {\boldsymbol{\xi}} \in \mathbb {R}^{d}$, we have

$$
\text {}{\boldsymbol{\xi}}^T J \text {}{\boldsymbol{\xi}} = \text {}{\boldsymbol{\xi}}^T \boldsymbol{X} J_s \boldsymbol{X}^T \text {}{\boldsymbol{\xi}}
= {\left(\boldsymbol{X}^T \text {}{\boldsymbol{\xi}}\right)}^T J_s {\left(\boldsymbol{X}^T \text {}{\boldsymbol{\xi}}\right)}
\geqslant 0
$$

## Lemma 4

$$\operatorname{lse} \left ( \beta, \text {}{\mathbf {x}} \right )$$ is a convex respect to $$\text {} {\mathbf {x}}$$ where $\text {} {\mathbf {x}} \in \mathbb {R}^{N}$.

$$\operatorname{lse} \left ( \beta, \boldsymbol{X}^T \boldsymbol{\xi}  \right )$$ is a convex respect to $$\text {} {\boldsymbol{\xi}}$$ where $$\text {} {\boldsymbol{X}} \in \mathbb {R}^{d \times N}, \text {} {\boldsymbol{\xi}} \in \mathbb {R}^{d}$$.

### Proof

The Jacobian of the $\operatorname{softmax}$ is Hessian of the $\operatorname{lse}$ according to Lemma 1. The Jacobian of the $\operatorname{softmax}$ is positive semi-definite according to Lemma 3. Therefore $\operatorname{lse}$ is a convex.

## Definitions

### Point-to-set Map

A point-to-set map $\mathcal{A}$ from a set $X$ into a set $Y$ is defined as

$$
\mathcal{A}: X \to \mathscr{P}(Y)
$$

which assigns a subset of $Y$ to each point of $X$, where $\mathscr{P}(Y)$ denotes the power set of $Y$.

### Closed

Suppose $X$ and $Y$ are two topological spaces. A point-to-set map $\mathcal{A}: X \to \mathscr{P}(Y)$ is said to be closed at $\mathbf x_0 \in X$ if:

$$
\begin{align*}
    \left .
    \begin{array}{l}
        \text {} {\mathbf {x}_{k}} \to \text {} {\mathbf x_0} \text{ as } k \to \infty \\
        \text {} {\mathbf {y}_{k}} \to \text {} {\mathbf {y}_{0}} \text{ as } k \to \infty \\
        \text {} {\mathbf {x}_{k}} \in X \\
        \text {} {\mathbf {y}_{k}} \in \mathcal{A} \left(\text {} {\mathbf {x}_{k}} \right)
    \end{array}
    \right\} \implies \text {} {\mathbf {y}_{0}} \in \mathcal{A} \left(\text {} {\mathbf x_0} \right)
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
A point-to-set map $\mathcal{A}: X \to \mathscr{P}(X)$ is said to be uniformly compact on $X$ if there exists a compact set $H$ independent of $\text {}{\mathbf {x}}$ such that:

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

is said to be monotonic with respect to $\operatorname {E}$ if

$$
\forall \text {}{\mathbf {x}} \in X, \forall \text {}{\mathbf {y}} \in \mathcal{A} \left( \text {}{\mathbf {x}} \right), \operatorname {E} \left( \text {}{\mathbf {y}} \right) \leqslant \operatorname {E} \left( \text {}{\mathbf {x}} \right)
$$

If, in addition,

$$
\forall \text {}{\mathbf {x}} \in X, \forall \text {}{\mathbf {y}} \in \mathcal{A} \left( \text {}{\mathbf {x}} \right), \operatorname {E} \left( \text {}{\mathbf {y}} \right) = \operatorname {E} \left( \text {}{\mathbf {x}} \right) \implies \text {}{\mathbf {y}} = \text {}{\mathbf {x}}
$$

Then $\mathcal{A}$ is said to be strictly monotonic with respect to $\operatorname {E}$.

### Global Convergence
Let $X$ be a set and $\text {} {\boldsymbol{\xi}_0} \in X$ a given point. Then an algorithm, $\mathcal{A}$, with initial point $\text {} {\boldsymbol{\xi}_0}$ is a point-to-set map $$\mathcal{A}: X \to \mathscr{P} \left(X \right)$$ which generates a sequence ${\left \lbrace \text {} {\boldsymbol{\xi}_t} \right \rbrace} _{t=0} ^{\infty}$ via the rule

$$
\text {}{\boldsymbol{\xi}_{t + 1}} \in \mathcal{A} \left (\text {} {\boldsymbol{\xi}_t} \right ), t = 0, 1, \cdots
$$

$\mathcal{A}$ is said to be globally convergent if: For any chosen initial point $\text {} {\boldsymbol{\xi}_0}$, the sequence ${\left \lbrace \text {} {\boldsymbol{\xi}_t} \right \rbrace} _{t=0} ^{\infty}$ generated by $$\text {} {\boldsymbol{\xi}_{t + 1}} \in \mathcal{A} \left (\text {} {\boldsymbol{\xi}_t} \right ), t = 0, 1, \cdots$$ (or a subsequence) converges to a point for which a necessary condition of optimality holds.

## Lemma 5
Consider an energy function $$\operatorname {E}: X \to \mathbb {R}$$:

$$
\operatorname {E} \left ( \boldsymbol{\xi}  \right ) = \operatorname {E_1} \left ( \boldsymbol{\xi}  \right ) - \operatorname {E_2} \left ( \boldsymbol{\xi}  \right )
$$

where $$\operatorname {E_1}$$ and $$\operatorname {E_2}$$ are convex functions of $$\boldsymbol{\xi}$$ respectively. Then the discrete CCCP (Concave Convex Procedure) algorithm

$$
\text {} {\boldsymbol{\xi}_{t + 1}} \in \mathcal{A} \left (\text {} {\boldsymbol{\xi}_t} \right ), t = 0, 1, \cdots
$$

given by:

$$
\nabla _{\boldsymbol{\xi}} \operatorname {E_1} \left ( \boldsymbol{\xi}_{t + 1} \right ) = \nabla _{\boldsymbol{\xi}} \operatorname {E_2} \left ( \boldsymbol{\xi}_{t}  \right )
$$

guarantees the sequence $${\left \lbrace \operatorname {E} \left ( \text {} {\boldsymbol{\xi}_t} \right ) \right \rbrace} _{t=0} ^{\infty}$$ monotonically decreases.

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
    \right\} \\
    & \implies \operatorname {E_1} \left(\boldsymbol{\xi}_{t}\right) + \operatorname {E_2} \left(\boldsymbol{\xi}_{t + 1}\right) \geqslant \operatorname {E_1} \left(\boldsymbol{\xi}_{t + 1}\right) + \operatorname {E_2} \left(\boldsymbol{\xi}_{t}\right) \\
    & \implies \operatorname {E_1} \left(\boldsymbol{\xi}_{t + 1}\right) - \operatorname {E_2} \left(\boldsymbol{\xi}_{t + 1}\right) \leqslant \operatorname {E_1} \left(\boldsymbol{\xi}_{t}\right) - \operatorname {E_2} \left(\boldsymbol{\xi}_{t}\right) \\
    & \implies \operatorname {E} \left(\boldsymbol{\xi}_{t + 1}\right) \leqslant \operatorname {E} \left(\boldsymbol{\xi}_{t}\right)
\end{align*}
$$

Therefore $\mathcal{A}$ is monotonic with respect to $\operatorname {E}$.

## Modern Hopfield Network

We have patterns that are represented by the matrix:
$$
\boldsymbol{X} = \left(\text {} {\mathbf {x}_{1}}, \dots, \text {}{\mathbf {x}_{N}} \right)
$$

where $\text {} {\mathbf {x}_{i}} \in \mathbb {R}^{d}$. Thus $$\text {} {\boldsymbol{X}} \in \mathbb {R}^{d \times N}$$.
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
\boldsymbol{\xi}_{t + 1} = \mathcal{F} \left ( \boldsymbol{\xi}_{t} \right ) = \boldsymbol{X}\text {}{\mathbf {p}} = \boldsymbol{X} \operatorname{softmax}\left(\beta \boldsymbol{X}^T {\boldsymbol{\xi}_{t}} \right)  \tag {2}
$$

where

$$
\text {}{\mathbf {p}} = \operatorname{softmax}\left(\beta \boldsymbol{X}^T {\boldsymbol{\xi}_{t}} \right)
$$

## Theorem 1 Global Convergence: Energy

The update rule (2) converges globally: For $$\boldsymbol{\xi}_{t+ 1} = \mathcal{F} \left ( \boldsymbol{\xi}_{t} \right )$$, the energy $$\operatorname {E} \left ( \boldsymbol{\xi}_{t} \right ) \to \operatorname {E} \left ( \boldsymbol{\xi}^{\ast} \right )$$ for $$t \to \infty$$ and one accumulation point $$\boldsymbol{\xi}^{\ast}$$.


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
\forall t \geqslant 1, \boldsymbol{\xi}_{t} \in S = \left \{\text {}{\boldsymbol{\xi}} \vert \left \lVert {\text {}{\boldsymbol{\xi}}} \right \rVert _2 \leqslant M \right \} \tag {Theo1.1}
$$

which is a convex and compact set.

According to Lemma 4, $\operatorname{lse}$ is a convex.
Hence the energy function $\operatorname {E} \left ( \boldsymbol{\xi}  \right )$ is the difference of two convex functions $\operatorname {E_1} \left ( \boldsymbol{\xi}  \right )$ and $\operatorname {E_2} \left ( \boldsymbol{\xi}  \right )$:
$$
\begin{align*}
\operatorname {E} \left ( \boldsymbol{\xi}  \right ) &= \operatorname {E_1} \left ( \boldsymbol{\xi}  \right ) - \operatorname {E_2} \left ( \boldsymbol{\xi}  \right ) \\
\operatorname {E_1} \left ( \boldsymbol{\xi}  \right ) &= \dfrac {1} {2} \boldsymbol{\xi}^T \boldsymbol{\xi} + \beta^{-1} \ln N + \dfrac {1} {2} M^2 = \dfrac {1} {2} \boldsymbol{\xi}^T \boldsymbol{\xi} + C_1 \\
\operatorname {E_2} \left ( \boldsymbol{\xi}  \right ) &= \operatorname{lse} \left ( \beta, \boldsymbol{X}^T \boldsymbol{\xi}  \right )
\end{align*} \tag {Theo1.2}
$$

where $C_1$ does not depend on $\boldsymbol{\xi}$.

Define minimization problem:

$$
\min _{\boldsymbol{\xi}} \operatorname {E} \left ( \boldsymbol{\xi}  \right ) = \min _{\boldsymbol{\xi}} \left ( \operatorname {E_1} \left ( \boldsymbol{\xi}  \right ) - \operatorname {E_2} \left ( \boldsymbol{\xi}  \right ) \right )
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
\mathcal{A} \left ( \boldsymbol{\xi}_{t } \right ) = \left \{ \boldsymbol{X} \operatorname{softmax}\left(\beta \boldsymbol{X}^T {\boldsymbol{\xi}_{t}} \right) \right \}
$$

According to Lemma 5, $\mathcal{A}$ is monotonic with respect to $\operatorname {E}$.

According to (Theo1.1), all points $$\boldsymbol{\xi}_t, t \geqslant 1$$ are in a compact set $S$. Hence there must be a convergent subsequence

$$
\boldsymbol{\xi}_{t_k} \to \boldsymbol{\xi}^{\ast}, \text{ as } k \to \infty
$$

where $$\boldsymbol{\xi}^{\ast} \in S$$ is a accumulation point.
Continuity of $\operatorname {E}$ provides

$$
\operatorname {E}\left(\boldsymbol{\xi}_{t_k}\right) \to \operatorname {E}\left(\boldsymbol{\xi}^{\ast}\right), \text{ as } k \to \infty \tag {Theo1.3}
$$

$\mathcal{A}$ is monotonic with respect to $\operatorname {E}$. So that

$$
\forall t \geqslant 0, \operatorname {E}\left(\boldsymbol{\xi}_{t}\right) \geqslant \operatorname {E}\left(\boldsymbol{\xi}^{\ast}\right)\tag {Theo1.4}
$$

Using (Theo1.3) and the definition of limit given $$\varepsilon \ge 0$$, there is a $$K_{\varepsilon}$$ such that

$$
\operatorname {E}\left(\boldsymbol{\xi}_{t_{K_{\varepsilon}}}\right) < \operatorname {E}\left(\boldsymbol{\xi}^{\ast}\right) + \varepsilon
$$

$\mathcal{A}$ is monotonic with respect to $\operatorname {E}$. So that

$$
\forall t > t_{K_{\varepsilon}}, \operatorname {E}\left(\boldsymbol{\xi}_{t}\right) \leqslant \operatorname {E}\left(\boldsymbol{\xi}_{t_{K_{\varepsilon}}}\right) < \operatorname {E}\left(\boldsymbol{\xi}^{\ast}\right) + \varepsilon
$$

Equations then yield

$$
\forall t > t_{K_{\varepsilon}}, \left \lvert \operatorname {E}\left(\boldsymbol{\xi}_{t}\right) - \operatorname {E}\left(\boldsymbol{\xi}^{\ast}\right) \right \rvert < \varepsilon
$$

Therefore

$$
\operatorname {E}\left(\boldsymbol{\xi}_{t}\right) \to \operatorname {E}\left(\boldsymbol{\xi}^{\ast}\right) = \operatorname {E}^{\ast}, \text{ as } t \to \infty
$$

According to (Theo1.4), $$\operatorname {E}\left(\boldsymbol{\xi}^{\ast}\right) $$ is the infimum of the set $${\left \lbrace \operatorname {E} \left ( \text {} {\boldsymbol{\xi}_t} \right ) \right \rbrace} _{t=0} ^{\infty}$$.

$$
\operatorname {E}\left(\boldsymbol{\xi}^{\ast}\right) = {\inf {\left \lbrace \operatorname {E} \left ( \text {} {\boldsymbol{\xi}_t} \right ) \right \rbrace} _{t=0} ^{\infty}}
$$

## Theorem 2 Global Convergence: Stationary Points
For the iteration Eq. (2) we have

$$
\operatorname {E}\left(\boldsymbol{\xi}_{t}\right) \to \operatorname {E}\left(\boldsymbol{\xi}^{\ast}\right) = \operatorname {E}^{\ast}, \text{ as } t \to \infty
$$

for some stationary point $$\boldsymbol{\xi}^{\ast}$$. Furthermore

$$
\left \lVert \boldsymbol{\xi}_{t + 1} - \boldsymbol{\xi}_{t} \right \rVert _2 \to 0, \text{ as } t \to \infty
$$

And either $${\left \lbrace \text {} {\boldsymbol{\xi}_t} \right \rbrace} _{t=0} ^{\infty}$$ converges, or, in the other case, the set of limit points of $${\left \lbrace \text {} {\boldsymbol{\xi}_t} \right \rbrace} _{t=0} ^{\infty}$$ is a connected and compact subset of $$\mathcal{L} \left ( \operatorname {E}^{\ast} \right )$$, where $$\mathcal{L} \left ( a \right ) = \left \lbrace \boldsymbol{\xi} \in \mathcal{L} \vert \operatorname {E} \left ( \text {} {\boldsymbol{\xi}} \right ) = a \right \rbrace$$ and $$\mathcal{L}$$ is the set of stationary points of the iteration Eq. (2). If $$\mathcal{L} \left ( \operatorname {E}^{\ast} \right )$$ is finite, then any sequence $${\left \lbrace \text {} {\boldsymbol{\xi}_t} \right \rbrace} _{t=0} ^{\infty}$$ generated by the iteration Eq. (2) converges to some $$\boldsymbol{\xi}^{\ast} \in \mathcal{L} \left ( \operatorname {E}^{\ast} \right )$$.

### Proof

Let

$$
g(\boldsymbol{\xi}, \boldsymbol{\xi}_t) = \operatorname {E_1} \left ( \boldsymbol{\xi}  \right ) - \operatorname {E_2} \left ( \boldsymbol{\xi}_{t}  \right ) - \left ( \nabla _{\boldsymbol{\xi}} \operatorname {E_2} \left ( \boldsymbol{\xi}_{t}  \right ) \right )^T \left ( \boldsymbol{\xi} - \boldsymbol{\xi}_{t} \right ) = \operatorname {E_1} \left ( \boldsymbol{\xi}  \right ) - \left ( \nabla _{\boldsymbol{\xi}} \operatorname {E_2} \left ( \boldsymbol{\xi}_{t}  \right ) \right )^T \boldsymbol{\xi} + C_2 \left ( \boldsymbol{\xi}_{t}  \right ) \tag {Theo1.5}
$$

where $$\operatorname {E_1}, \operatorname {E_2}$$ are defined by (Theo1.2). $$C_2 \left ( \boldsymbol{\xi}_{t}  \right )$$ does not depend on $\boldsymbol{\xi}$.
Since $\operatorname {E_2}$ is convex according to Lemma 4, the first order characterization of convexity holds:
$$
\operatorname {E_2} \left ( \boldsymbol{\xi}  \right ) \geqslant \operatorname {E_2} \left ( \boldsymbol{\xi}_{t}  \right ) + \left ( \nabla _{\boldsymbol{\xi}} \operatorname {E_2} \left ( \boldsymbol{\xi}_{t}  \right ) \right )^T \left ( \boldsymbol{\xi} - \boldsymbol{\xi}_{t} \right )
$$

Therefore:

$$
\begin{align*}
\operatorname {E} \left ( \boldsymbol{\xi}  \right ) &= \operatorname {E_1} \left ( \boldsymbol{\xi}  \right ) - \operatorname {E_2} \left ( \boldsymbol{\xi}  \right ) \\
& \leqslant \operatorname {E_1} \left ( \boldsymbol{\xi}  \right ) - \operatorname {E_2} \left ( \boldsymbol{\xi}_{t}  \right ) - \left ( \nabla _{\boldsymbol{\xi}} \operatorname {E_2} \left ( \boldsymbol{\xi}_{t}  \right ) \right )^T \left ( \boldsymbol{\xi} - \boldsymbol{\xi}_{t} \right ) \\
&= g(\boldsymbol{\xi}, \boldsymbol{\xi}_t) \tag {Theo1.6}
\end{align*}
$$

$$\operatorname {E_1} \left ( \boldsymbol{\xi}  \right ) = \dfrac {1} {2} \boldsymbol{\xi}^T \boldsymbol{\xi} + C_1$$ is strict convex respect to $$\text {} {\boldsymbol{\xi}}$$.
$$- \left ( \nabla _{\boldsymbol{\xi}} \operatorname {E_2} \left ( \boldsymbol{\xi}_{t}  \right ) \right )^T \boldsymbol{\xi} + C_2 \left ( \boldsymbol{\xi}_{t}  \right )$$ is both concave and convex respect to $$\text {} {\boldsymbol{\xi}}$$.
Therefore $g(\boldsymbol{\xi}, \boldsymbol{\xi}_t)$ is strict convex (if the domain is convex) and there exist only one minimum, which is the global minimum.
Let

$$
\dfrac {\partial g(\boldsymbol{\xi}, \boldsymbol{\xi}_t)} {\partial {\boldsymbol{\xi}}} = \nabla _{\boldsymbol{\xi}} \operatorname {E_1} \left ( \boldsymbol{\xi} \right ) - \nabla _{\boldsymbol{\xi}} \operatorname {E_2} \left ( \boldsymbol{\xi}_{t}  \right ) = \boldsymbol{\xi} - \nabla _{\boldsymbol{\xi}} \operatorname {E_2} \left ( \boldsymbol{\xi}_{t}  \right ) = \boldsymbol{\xi} - \boldsymbol{X} \operatorname{softmax}\left(\beta \boldsymbol{X}^T {\boldsymbol{\xi}}_t \right) = \text {} {\mathbf {0}}
$$

The minimum is:

$$
\boldsymbol{\xi}_{t + 1} = \underset{\boldsymbol{\xi}} {\operatorname{argmin}} g(\boldsymbol{\xi}, \boldsymbol{\xi}_t) = \boldsymbol{X} \operatorname{softmax}\left(\beta \boldsymbol{X}^T {\boldsymbol{\xi}}_t \right) \tag {Theo1.7}
$$

Hence

$$
\text { if } \boldsymbol{\xi}_{t + 1} \neq \boldsymbol{\xi}_t, g(\boldsymbol{\xi}_{t + 1}, \boldsymbol{\xi}_t) \lt g(\boldsymbol{\xi}_{t}, \boldsymbol{\xi}_t)  \tag {Theo1.8}
$$

Using (Theo1.5), (Theo1.6), (Theo1.8)

$$
\text { if } \boldsymbol{\xi}_{t + 1} \neq \boldsymbol{\xi}_t, \operatorname {E} \left ( \boldsymbol{\xi}_{t + 1} \right ) \leqslant g(\boldsymbol{\xi}_{t + 1}, \boldsymbol{\xi}_t) \lt g(\boldsymbol{\xi}_{t}, \boldsymbol{\xi}_t) = \operatorname {E} \left ( \boldsymbol{\xi}_t  \right )
$$

Let

$$
\mathcal{A} \left ( \boldsymbol{\xi}_{t } \right ) = \left \{ \boldsymbol{\xi}_{t + 1} \right \} = \left \{ \boldsymbol{X} \operatorname{softmax}\left(\beta \boldsymbol{X}^T {\boldsymbol{\xi}_{t}} \right) \right \}
$$

Thus

$$
\forall \boldsymbol{\xi}_{t + 1} \in \mathcal{A} \left ( \boldsymbol{\xi}_t \right ), \text { if } \boldsymbol{\xi}_{t + 1} \neq \boldsymbol{\xi}_t, \operatorname {E} \left ( \boldsymbol{\xi}_{t + 1} \right ) \lt \operatorname {E} \left ( \boldsymbol{\xi}_t \right )
$$

Therefore point-set-map $\mathcal{A}$ is strictly monotonic with respect to $\operatorname {E}$.

According to (Theo1.1), $\mathcal{A}$ is uniformly compact on $S$ which is a convex and compact set.

 $$\operatorname {E_1}, \operatorname {E_2}$$ are differentiable convex functions. $$\nabla _{\boldsymbol{\xi}} \operatorname {E_2} \left ( \boldsymbol{\xi} \right ) = \boldsymbol{X} \operatorname{softmax}\left(\beta \boldsymbol{X}^T {\boldsymbol{\xi}} \right)$$ is continuous.

Obviously $$\mathcal{A} \left ( \boldsymbol{\xi} \right )$$ is nonempty for any $$\boldsymbol{\xi} \in \mathbb {R}^{d}$$. Therefore $$\mathcal{A}$$ is closed on $$S$$.
