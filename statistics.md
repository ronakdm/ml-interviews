# Statistics Basics

## Deriving the Distribution of a Random Variable

A general question is describing the distribution of a random variable $X$.
If it is real-valued, this can be done by specifying the cumulative distribution function (CDF) $F_X$, 
probability density function (PDF) $f_X$, or probability mass function (PMF) $p_X$. This can be done in the following ways.
- Use the "first principles" method, i.e. using reasoning from probability to compute $F_X(x) := P(X \leq x)$.
- If $X = g(Y)$ for $g: \mathbb{R} \rightarrow \mathbb{R}$ for som random variable $Y$, and $g$ is invertible with differentiable inverse, then
compute $f_X(x) = f_Y(g^{-1}(x)) \cdot |[g^{-1}]'(x)|$.
- If $X = (X_1, X_2)$ is a joint distribution of real-valued random variables, compute $F_{X_1 | X_2 = x_2}$ and $F_{X_2}$ (or the corresponding densities).
- Compute the first principles method with the law of total probability. Let $Z$ be a discrete random variable observed jointly with $X$, taking values in $\mathcal{Z}$, and compute
$$
    P(X \leq x) = \sum_{z \in \mathcal{Z}} P(X \leq x, Z = z).
$$
- If $(X, Z)$ are continuous, real-valued random variables with joint density $f_{X, Z}$, then compute
$$
    f_X(x) = \int_{z \in \mathbb{R}} f_{X, Z}(x, z)dz.
$$
- If $X = g(U, V)$, where $g: \mathbb{R}^2 \rightarrow \mathbb{R}$ and $U$ and $V$ are real-valued random variables, compose the first
principles method with the law of iterated expectations:
$$
P(X \leq x) = P(g(U, V) \leq x) = E[P(g(U, V) \leq x | V)].
$$
- Wen deriving a conditional density given $Y = y$, write $f_{X | Y = y}(x) \propto f_{X, Y}(x, y)$, and recognize the 
*family* of $f_{X | Y = y}$ by looking at the $x$ terms and the *parameters* by looking at the $y$ terms of $f_{X, Y}(x, y)$.

**Example:** Let $Z_1, \ldots, Z_n$ be $\mathbb{R}^d$-valued random variables distributed uniformly on the $d$-dimensional Euclidean unit ball $\{z: ||z||_2 \leq 1\}$. Find the distribution of the minimum distance between the origin and any of the $Z_i$'s (as a function of $n$ and $d$).

## Computing Functionals of the Distribution of a Random Variable

## Hypothesis Testing for Model Performance