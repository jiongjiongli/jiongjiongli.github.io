---
layout: post
title: Modern Hopfield Network
---

## Definition
### Notations

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

where $\vec{\mathbf {x}}_i \in \mathbb {R}^{N}$.
### Log-Sum-Exp Function
$$
\operatorname{lse} \left ( \beta, \vec{\mathbf {x}} \right ) = \beta^{-1} \ln \left( {\sum_{k=1}^{N} \exp \left( {\beta x_k} \right)} \right)
$$

where $\vec{\mathbf {x}}_i \in \mathbb {R}^{N}$.

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

### Hopfield Network Notations
We have patterns that are represented by the matrix:
$$
\boldsymbol{X} = \left(\vec{\mathbf {x}}_1, \dots, \vec{\mathbf {x}}_N \right)
$$

where $\vec{\mathbf {x}}_i \in \mathbb {R}^{d}$.
The largest norm of a pattern is:

$$
M = \max_{i \in \left[ N \right]} \left \lVert \vec{\mathbf {x}}_i \right \rVert _2
$$

The query or state of the Hopfield Network is $\boldsymbol{\xi} \in \mathbb {R}^{d}$.
Define energy $\operatorname {E} \left ( \boldsymbol{\xi}  \right )$ for a continuous query or state $\boldsymbol{\xi}$:
$$
\operatorname {E} \left ( \boldsymbol{\xi}  \right ) = - \operatorname{lse} \left ( \beta, \boldsymbol{X}^T \boldsymbol{\xi}  \right ) + \dfrac {1} {2} \boldsymbol{\xi}^T \boldsymbol{\xi} + \beta^{-1} \ln N + \dfrac {1} {2} M^2 \tag {1}
$$

## New Update Rule
$$
\boldsymbol{\xi}^{t + 1} = f \left ( \boldsymbol{\xi}^{t} \right ) = \boldsymbol{X}\vec{\mathbf {p}} = \boldsymbol{X} \operatorname{softmax}\left(\beta \boldsymbol{X}^T {\boldsymbol{\xi}^{t}} \right)  \tag {2}
$$

where

$$
\vec{\mathbf {p}} = \operatorname{softmax}\left(\beta \boldsymbol{X}^T {\boldsymbol{\xi}^{t}} \right)
$$

## Theorem 1 Global Convergence
The update rule (2) converges globally: For $\boldsymbol{\xi}^{t+ 1} = f \left ( \boldsymbol{\xi}^{t} \right )$, the energy $\operatorname {E} \left ( \boldsymbol{\xi}^{t} \right ) \to \operatorname {E} \left ( \boldsymbol{\xi}^{\text{*}} \right )$ for $t \to \infty $ and a fixed point $\boldsymbol{\xi}^{\text{*}}$.

### Proof
The Jacobian of the $\operatorname{softmax}$ is positive semi-definite according to Lemma 3. The Jacobian of the $\operatorname{softmax}$ is Hessian of the $\operatorname{lse}$, therefore $\operatorname{lse}$ is a convex.
The energy function $\operatorname {E} \left ( \boldsymbol{\xi}  \right )$ is the difference of two convex functions $\operatorname {E_1} \left ( \boldsymbol{\xi}  \right )$ and $\operatorname {E_2} \left ( \boldsymbol{\xi}  \right )$:

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
\min _{\boldsymbol{\xi}} \operatorname {E} \left ( \boldsymbol{\xi}  \right ) = \min _{\boldsymbol{\xi}} \operatorname {E_1} \left ( \boldsymbol{\xi}  \right ) - \operatorname {E_2} \left ( \boldsymbol{\xi}  \right )
$$

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
\dfrac {\partial g(\boldsymbol{\xi}, \boldsymbol{\xi}^t)} {\partial {\boldsymbol{\xi}}}  &= \boldsymbol{\xi} - \nabla _{\boldsymbol{\xi}} \operatorname {E_2} \left ( \boldsymbol{\xi}^{t}  \right ) \\
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
\boldsymbol{\xi}^{t + 1} = \underset{\boldsymbol{\xi}} {\operatorname{argmin}} g(\boldsymbol{\xi}, \boldsymbol{\xi}^t)= \boldsymbol{X} \operatorname{softmax}\left(\beta \boldsymbol{X}^T {\boldsymbol{\xi}}^t \right)
$$

So

$$
g(\boldsymbol{\xi}^{t + 1}, \boldsymbol{\xi}^t) \lt g(\boldsymbol{\xi}^{t}, \boldsymbol{\xi}^t), \text { if } \boldsymbol{\xi}^{t + 1} \neq \boldsymbol{\xi}^t
$$

Therefore

$$
\operatorname {E} \left ( \boldsymbol{\xi}^{t + 1} \right ) \leqslant g(\boldsymbol{\xi}^{t + 1}, \boldsymbol{\xi}^t) \lt g(\boldsymbol{\xi}^{t}, \boldsymbol{\xi}^t) = \operatorname {E} \left ( \boldsymbol{\xi}^t  \right ), \text { if } \boldsymbol{\xi}^{t + 1} \neq \boldsymbol{\xi}^t
$$



