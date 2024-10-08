---
layout: post
title: Expectation-Maximization (EM) Algorithm
---

## Introduction
The Expectation-Maximization (EM) algorithm is an iterative approach to find the maximum likelihood estimates (MLE) of parameters in probabilistic models when the model depends on unobserved latent variables.

Let $X$ be the observed data, $Z$ the unobserved (latent) data, and $\theta$ the set of parameters. The goal is to maximize the likelihood function:

$$
L\left(\theta; X\right) = p\left(X \mid \theta\right) = \sum_Z p\left(X, Z \mid \theta\right)
$$

However, the presence of latent variables makes direct maximization difficult, so the EM algorithm proceeds by iterating between two steps:
- **E-step** (Expectation)
- **M-step** (Maximization)

## Log-Likelihood Function with Latent Variables
We begin with the log-likelihood function of the observed data:

$$
\ln p\left(X \mid \theta\right) = \ln \left( \sum_Z p\left(X, Z \mid \theta\right) \right)
$$

Since the logarithm of a sum is generally hard to maximize, the EM algorithm simplifies this using an auxiliary function. We introduce a distribution over the latent variables $q\left(Z\right)$ and rewrite the log-likelihood using Jensen's inequality:

$$
\ln p\left(X \mid \theta\right) \geqslant \sum_Z q\left(Z\right) \ln \left( \frac{p\left(X, Z \mid \theta\right)}{q\left(Z\right)} \right)
$$

This gives us a lower bound on the log-likelihood.

## EM Algorithm Derivation
The EM algorithm alternates between two steps:

### E-Step (Expectation)
In the E-step, we compute the expected value of the complete-data log-likelihood with respect to the posterior distribution of the latent variables, given the current parameter estimates $\theta^{(t)}$:

$$
Q\left(\theta \mid \theta^{(t)}\right) = \mathbb{E}_{Z \mid X, \theta^{(t)}} \left[ \ln p\left(X, Z \mid \theta\right) \right]
$$

This is equivalent to computing:

$$
Q\left(\theta \mid \theta^{(t)}\right) = \sum_Z p\left(Z \mid X, \theta^{(t)}\right) \ln p\left(X, Z \mid \theta\right)
$$

where $p\left(Z \mid X, \theta^{(t)}\right)$ is the posterior distribution of the latent variables given the observed data $X$ and the current parameter estimate $\theta^{(t)}$.

### M-Step (Maximization)
In the M-step, we maximize the function $Q\left(\theta \mid \theta^{(t)}\right)$ with respect to $\theta$ to obtain the updated parameter estimates:

$$
\theta^{(t+1)} = \underset{\theta}{\operatorname{argmax}} Q\left(\theta \mid \theta^{(t)}\right)
$$

Thus, the M-step involves finding the parameters that maximize the expected complete-data log-likelihood.

## Convergence of the EM Algorithm
### Lemma
Suppose:

1. $l\left(\theta\right), g\left(\theta, \theta^{(t)}\right)$ satisfies:
$$
    l\left(\theta\right) \geqslant g\left(\theta, \theta^{(t)}\right) \tag {1}
$$

2. Equality (1) holds if $\theta = \theta^{(t)}$.

Let
$$
\theta^{(t+1)} = \underset{\theta}{\operatorname{argmax}} g\left(\theta, \theta^{(t)}\right)
$$

Then
$$
l\left(\theta^{(t+1)}\right) \geqslant g\left(\theta^{(t+1)}, \theta^{(t)}\right) = \max _\theta g\left(\theta, \theta^{(t)}\right) \geqslant g\left(\theta^{(t)}, \theta^{(t)}\right) = l\left(\theta^{(t)}\right)
$$

### Proof

Let
$$
l\left(\theta\right) = \ln p\left(X \mid \theta\right)
$$

$$
g\left(\theta, \theta^{(t)}\right) = \sum_Z p\left(Z \mid X, \theta^{(t)}\right) \ln \left( \frac{p\left(X, Z \mid \theta\right)}{p\left(Z \mid X, \theta^{(t)}\right)} \right)
$$

Then using Jensen's inequality, we can show that:

$$
\begin{align*}
l\left(\theta\right) &= \ln p\left(X \mid \theta\right) \\
&= \ln \left( \sum_Z p\left(X, Z \mid \theta\right) \right) \\
&= \ln \left( \sum_Z p\left(Z \mid X, \theta^{(t)}\right) \cdot \frac{p\left(X, Z \mid \theta\right)}{p\left(Z \mid X, \theta^{(t)}\right)} \right) \\
& \geqslant \sum_Z p\left(Z \mid X, \theta^{(t)}\right) \ln \left( \frac{p\left(X, Z \mid \theta\right)}{p\left(Z \mid X, \theta^{(t)}\right)} \right) \\
&= g\left(\theta, \theta^{(t)}\right) \\

g\left(\theta^{(t)}, \theta^{(t)}\right)
&= \sum_Z p\left(Z \mid X, \theta^{(t)}\right) \ln \left( \frac{p\left(X, Z \mid \theta^{(t)}\right)}{p\left(Z \mid X, \theta^{(t)}\right)} \right) \\
&= \sum_Z p\left(Z \mid X, \theta^{(t)}\right) \ln p\left(X \mid \theta^{(t)}\right) \\
&= \ln p\left(X \mid \theta^{(t)}\right) \\
&= l\left(\theta^{(t)}\right)
\end{align*}
$$

According to lemma, the EM algorithm is guaranteed to increase the likelihood at each iteration. Therefore, the EM algorithm converges to a (local) maximum of the likelihood function.
