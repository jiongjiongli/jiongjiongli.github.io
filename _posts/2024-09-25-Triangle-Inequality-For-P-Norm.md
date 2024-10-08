---
layout: post
title: Triangle Inequality for P-Norm
---

## Theorem

Let

$$
\left \lVert \vec{\mathbf{x}} \right \rVert_p = \left( \sum_{i=1}^{n} \left \lvert x_i \right \rvert^p \right)^{1/p}
$$

Then:

$$
\forall p \in \mathbb{R}, p \geqslant 1, \vec{\mathbf{x}}, \vec{\mathbf{y}} \in \mathbb{R}^n, \\
\left \lVert \vec{\mathbf{x}} + \vec{\mathbf{y}} \right \rVert_p \leqslant \left \lVert \vec{\mathbf{x}} \right \rVert_p + \left \lVert \vec{\mathbf{y}} \right \rVert_p \tag{1}
$$



## Proof

### Standard Condition

Suppose:

$$
\forall \vec{\mathbf{x}}, \vec{\mathbf{y}} \in \mathbb{R}^n, \vec{\mathbf{x}} \geqslant \vec 0, \vec{\mathbf{y}} \geqslant \vec 0, \left \lVert \vec{\mathbf{x}} \right \rVert_p > 0, \left \lVert \vec{\mathbf{y}} \right \rVert_p > 0, p \in \mathbb{R}, p > 1
$$

Because:

$$
\forall \alpha \in \mathbb{R}, \left \lVert \alpha \vec{\mathbf{x}} \right \rVert_p = \left \lvert \alpha \right \rvert \left \lVert \vec{\mathbf{x}} \right \rVert_p
$$

So statement (1) is equivalent to:

$$
\left \lVert
    \dfrac {\left \lVert \vec{\mathbf{x}} \right \rVert_p} {\left \lVert \vec{\mathbf{x}} \right \rVert_p + \left \lVert \vec{\mathbf{y}} \right \rVert_p}
    \cdot
    \dfrac {\vec{\mathbf{x}}} {\left \lVert \vec{\mathbf{x}} \right \rVert_p}
+
    \dfrac {\left \lVert \vec{\mathbf{y}} \right \rVert_p} {\left \lVert \vec{\mathbf{x}} \right \rVert_p + \left \lVert \vec{\mathbf{y}} \right \rVert_p}
    \cdot
    \dfrac {\vec{\mathbf{y}}} {\left \lVert \vec{\mathbf{y}} \right \rVert_p}
\right \rVert_p \leqslant 1
$$

It is equivalent to proving:

$$
\forall \vec{\mathbf{x}}, \vec{\mathbf{y}} \in \mathbb{R}^n, \vec{\mathbf{x}} \geqslant \vec 0, \vec{\mathbf{y}} \geqslant \vec 0, \left \lVert \vec{\mathbf{x}} \right \rVert_p = 1, \left \lVert \vec{\mathbf{y}} \right \rVert_p = 1, p \in \mathbb{R}, p > 1, \lambda \in \mathbb{R}, 0 < \lambda < 1, \\
\left \lVert \lambda \cdot \vec{\mathbf{x}} + (1 - \lambda) \cdot \vec{\mathbf{y}} \right \rVert_p \leqslant 1
$$

It is equivalent to:

$$
\left \lVert \lambda \cdot \vec{\mathbf{x}} + (1 - \lambda) \cdot \vec{\mathbf{y}} \right \rVert_p^p \leqslant 1
$$

That is:

$$
\sum_{i=1}^{n} \left( \lambda x_i + \left( 1 - \lambda \right) y_i \right)^p \leqslant 1
$$

Because $\forall x \in \mathbb{R}, x \geqslant 0, p \in \mathbb{R}, p > 1, f(x) = x^p$ is convex, which can be proven by:

$$
\forall x, y \in \mathbb{R}, x \geqslant 0, y \geqslant 0, \\
\left( f'(x) - f'(y) \right) \left( x - y \right) = p \left( x^{p - 1} - y^{p - 1} \right) \left( x - y \right) \geqslant 0
$$

Then:

$$
f \left( \lambda x_i + (1 - \lambda) y_i \right) \leqslant \lambda f \left( x_i \right) + (1 - \lambda) f \left( y_i \right)
$$

That is:

$$
\left( \lambda x_i + (1 - \lambda) y_i \right)^p \leqslant \lambda x_i^p + (1 - \lambda) y_i^p
$$

So:

$$
\sum_{i=1}^{n} \left( \lambda x_i + \left( 1 - \lambda \right) y_i \right)^p \leqslant \lambda \sum_{i=1}^{n} x_i^p + (1 - \lambda) \sum_{i=1}^{n} y_i^p = \lambda + (1 - \lambda) = 1
$$

Thus, statement (1) holds.

### Special Condition

If $\left \lVert \vec{\mathbf{x}} \right \rVert_p = 0$, that is, $\vec{\mathbf{x}} = \vec{0}$, then statement (1) obviously holds.

It also holds if $\left \lVert \vec{\mathbf{y}} \right \rVert_p = 0$.

Now consider other special conditions. statement (1) is equivalent to:

$$
\left( \sum_{i=1}^{n} \left \lvert x_i + y_i \right \rvert^p \right)^{1/p} \leqslant \left( \sum_{i=1}^{n} \left \lvert x_i \right \rvert^p \right)^{1/p} + \left( \sum_{i=1}^{n} \left \lvert y_i \right \rvert^p \right)^{1/p}
$$

If $p = 1$, it is trivial to prove statement (1) holds because:

$$
\sum_{i=1}^{n} \left \lvert x_i + y_i \right \rvert \leqslant \sum_{i=1}^{n} \left \lvert x_i \right \rvert + \sum_{i=1}^{n} \left \lvert y_i \right \rvert
$$

Now consider $\forall \vec{\mathbf{x}}, \vec{\mathbf{y}} \in \mathbb{R}^n$. Since

$$
\left \lvert x_i + y_i \right \rvert \leqslant \left \lvert x_i \right \rvert + \left \lvert y_i \right \rvert
$$

We have:

$$
\left( \sum_{i=1}^{n} \left \lvert x_i + y_i \right \rvert^p \right)^{1/p} \leqslant \left( \sum_{i=1}^{n} \left( \left \lvert x_i \right \rvert + \left \lvert y_i \right \rvert \right)^p \right)^{1/p} \leqslant \left( \sum_{i=1}^{n} \left \lvert x_i \right \rvert^p \right)^{1/p} + \left( \sum_{i=1}^{n} \left \lvert y_i \right \rvert^p \right)^{1/p}
$$

Thus, statement (1) holds.
