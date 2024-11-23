---
id: Probability Distributions
aliases: 
tags:
  - distribution
  - modelling
---

# Discrete Distributions

## 1. Bernoulli Trials

A **Bernoulli trial** is a random experiment with exactly two possible outcomes: success and failure. 

## 2. Bernoulli Distribution

The **Bernoulli Distribution** is used to model binary outcomes in Bernoulli trials.

### Probability Mass Function (PMF)

$$ 
P(x) = \begin{cases} 
   \binom{n}{x} p^x q^{n-x} & \text{for } x = 0, 1, 2, \dots, n \\ 
   0 & \text{otherwise} 
\end{cases} 
$$

### Parameters

- **Binomial Coefficient**: $\binom{n}{x} = \frac{n!}{x!(n - x)!}$
- \( p \): Probability of success
- \( q = 1 - p \): Probability of failure

> [!NOTE]
> **To Do**: 
> - Derive the expected value \( E(X) = np \).
> - Derive the variance \( V(X) = npq \).

---

## 3. Geometric Distribution

The **Geometric Distribution** models the number of Bernoulli trials needed to get the first success.

### Probability Mass Function (PMF)

$$
P(x) = \begin{cases}
   q^{x-1} p & \text{for } x = 1, 2, \dots \\
   0 & \text{otherwise}
\end{cases}
$$

- **Interpretation**: \( \{X = x\} \) occurs when there are \( x-1 \) failures before the first success.
- **Mean** $E(X) = \frac{1}{p}$
- **Variance** $V(X) = \frac{q}{p^2}$

> [!TIP]
> **To Do**: Derive these values for mean and variance.

---

## 4. Poisson Distribution

The **Poisson Distribution** models the number of events occurring within a fixed interval of time or space, given the average rate of occurrence.

### Probability Mass Function (PMF)

$$
P(x) = \begin{cases}
   \frac{e^{-\alpha} \alpha^x}{x!} & \text{for } x = 0, 1, 2, \dots \\
   0 & \text{otherwise}
\end{cases}
$$

- \( $\alpha$ \): Average rate of occurrence (mean number of events in the interval)


## 5. Gamma Distribution
- a probability distribution
