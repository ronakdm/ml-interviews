# Statistics Basics

## Deriving the Distribution of a Random Variable

A general question is describing the distribution of a random variable $X$.
If it is real-valued, this can be done by specifying the cumulative distribution function (CDF) $F_X$, 
probability density function (PDF) $f_X$, or probability mass function (PMF) $p_X$. This can be done in the following ways.
- Use the "first principles" method, i.e. using reasoning from probability to compute $F_X(x) := P(X \leq x)$.
- If $X = g(Y)$ for $g: \mathbb{R} \rightarrow \mathbb{R}$ for some random variable $Y$, and $g$ is invertible with differentiable inverse, then
compute $f_X(x) = f_Y(g^{-1}(x)) \cdot |[g^{-1}]'(x)|$.
- If $X = (X_1, X_2)$ is a joint distribution of real-valued random variables, compute $F_{X_1 | X_2 = x_2}$ and $F_{X_2}$ (or the corresponding densities).
- Compose the first principles method with the law of total probability. Let $Z$ be a discrete random variable observed jointly with $X$, taking values in $\mathcal{Z}$, and compute

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

- When deriving a conditional density given $Y = y$, write $f_{X | Y = y}(x) \propto f_{X, Y}(x, y)$, and recognize the 
*family* of $f_{X | Y = y}$ by looking at the $x$ terms and the *parameters* by looking at the $y$ terms of $f_{X, Y}(x, y)$.

**Example:** Let $Z_1, \ldots, Z_n$ be $\mathbb{R}^d$-valued random variables distributed uniformly on the $d$-dimensional Euclidean unit ball $\lbrace z: ||z||_2 \leq 1\rbrace$. Find the distribution of the minimum distance between the origin and any of the $Z_i$'s (as a function of $n$ and $d$).

## Computing Functionals of the Distribution of a Random Variable

Similarly, one may ask you to compute the expectation $\mathbb{E}[X]$ or variance $\operatorname{Var}[X]$ of a random variable $X$. Some options are listed below.
- While it is usually simpler to compute the expectation or variance, one can always compute the entire distribution of $X$ and then proceed by definition:

$$
\mathbb{E}[X] = \int x f_X(x) dx, \quad \operatorname{Var}[X] = \mathbb{E}[X^2] - \mathbb{E}[X]^2
$$

- For $(X, Z)$ with joint density $f_{X, Z}$, use the law of total expectation (with analogous techniques for discrete random variables):

$$
\mathbb{E}[X] = \int_{x \in \mathbb{R}}\int_{z \in \mathbb{R}} x f_{X, Z}(x, z)dzdx.
$$

- Use the law of iterated expectation:

$$
\mathbb{E}[X][X] = \mathbb{E}[X][\mathbb{E}[X | Z]].
$$

- Use the law of total variance:

$$
\operatorname{Var}[X] = \mathbb{E}[\operatorname{Var}[X|Z]] + \operatorname{Var}[\mathbb{E}[X|Z]].
$$

- If $X = \sum_{i=1}^n X_i$ is a sum of random variables, letting $\operatorname{Cov}[X_i, X_j]$ be the covariance of $X_i$ and $X_j$, use:

$$
\mathbb{E}[X] = \sum_{i=1}^n \mathbb{E}[X_i], \quad \operatorname{Var}[X] = \sum_{i=1}^n \sum_{j=1}^n \operatorname{Cov}[X_i, X_j].
$$

- If $X$ is a count of some quantity, write it as a sum of indicators $X = \sum_{i=1}^n 1\{A_i\}$ for events $A_1, \ldots, A_n$, so that:

$$
\mathbb{E}[X] = \sum_{i=1}^n \mathbb{E}[1\{A_i\}] = \sum_{i=1}^n P(A_i). 
$$

**Example:** 8 students from JHU and 10 students from UW sit around a circular table with 18 seats, with uniformly randomly assigned seats. Each person will shake the hands of the person next to them if they are from different universities. What is the expected number of handshakes that occur around the table? What is the variance?


## Hypothesis Testing for Model Performance

When dealing with accuracies, the performance of a classification model $h: \mathcal{X} \rightarrow \{0, 1\}$ on test set realizations $(x_i, y_i), ..., (x_n, y_n)$ is written

$$
    \operatorname{acc}(h) = \frac{1}{n} \sum_{i=1}^n 1\{h(x_i) = y_i\}
$$

for $x_i \in \mathcal{X}$ and $y_i \in \{0, 1\}$. Note that we have conditioned on any training data, and consider only the randomness in the test set. 
As such, under the assumption that each $(x_i, y_i)$ is an independent and identically distributed (i.i.d.) realization of some random pair $(X, Y)$, this is a Binomial proportion, with parameters $n$ and $p := P(h(X) = Y)$. Various [confidence intervals](https://en.wikipedia.org/wiki/Binomial_proportion_confidence_interval) have been proposed for this type of statistic. When comparing two classifiers $h_1$ and $h_2$, if using the same test set, we turn to paired tests of differences between means, such as the [Wilcoxon signed-rank test](https://en.wikipedia.org/wiki/Wilcoxon_signed-rank_test) or more modern statistical tools.