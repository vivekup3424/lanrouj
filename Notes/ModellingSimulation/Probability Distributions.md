---
id: Probability Distributions
aliases: 
tags:
  - distribution
  - modelling
---
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

- \( $\alpha$ \): Average rate of occurrence (mean number of events in the interval = variance as well)


## 5. Gamma Distribution
The Gamma distribution is a continuous probability distribution that models the waiting time until the occurrence of $k$ events in a Poisson process, where events happen independently at a constant rate. It is a generalization of the exponential distribution, which models the waiting time for the first event ($k = 1$).

### Key Components:

1. **Applications**:
   - It is commonly used in scenarios where the time to complete multiple independent phases or steps is modeled.
   - Examples: modeling lifetimes, queuing theory, and reliability analysis.

2. **Parameters**:
   - **$k$**: The shape parameter (also referred to as the "scaling parameter"), representing the number of events or steps.
   - **$\lambda$**: The rate parameter, representing the constant rate at which events occur.
   - **$\theta$**: The scale parameter, related to $\lambda$ by $\theta = \frac{1}{\lambda}$.

3. **Probability Density Function (PDF)**:
   The PDF of the Gamma distribution is:
   $$
   f(x; k, \lambda) = 
   \begin{cases} 
   \frac{\lambda^k x^{k-1} e^{-\lambda x}}{\Gamma(k)}, & x > 0 \\
   0, & \text{otherwise}
   \end{cases}
   $$
   Here, $\Gamma(k)$ is the Gamma function, defined as $\Gamma(k) = (k-1)!$ for integer $k$, or:
   $$
   \Gamma(k) = \int_0^\infty t^{k-1} e^{-t} dt \text{ for any } k > 0.
   $$

4. **Cumulative Distribution Function (CDF)**:
   The CDF is the integral of the PDF:
   $$
   F(x; k, \lambda) = \int_0^x f(t; k, \lambda) dt
   $$
   The closed-form solution of the CDF is not always straightforward and often requires numerical simulation.

5. **Expectation and Variance**:
   - **Mean ($E[X]$)**: $\frac{k}{\lambda} = k \theta$
   - **Variance ($V[X]$)**: $\frac{k}{\lambda^2} = k \theta^2$

6. **Special Case - Exponential Distribution**:
   When $k = 1$, the Gamma distribution reduces to the exponential distribution:
   $$
   f(x; \lambda) = \lambda e^{-\lambda x}, \quad x > 0.
   $$

### Intuition:
The Gamma distribution describes the sum of $k$ independent exponential random variables with the same rate $\lambda$. For example:
- If you are waiting for $k$ bus arrivals, each occurring independently and exponentially, the Gamma distribution models the total waiting time.
Let's derive the **expectation** $E[X]$ and **variance** $V[X]$ of the Gamma distribution step by step using first principles. 

### **The PDF of the Gamma distribution**:
$$
f(x; k, \lambda) = \frac{\lambda^k x^{k-1} e^{-\lambda x}}{\Gamma(k)}, \quad x > 0
$$
where:
- $k$ is the shape parameter,
- $\lambda$ is the rate parameter,
- $\Gamma(k) = \int_0^\infty t^{k-1} e^{-t} dt$ is the Gamma function.

---

### **1. Expectation ($E[X]$)**

The expectation is defined as:
$$
E[X] = \int_0^\infty x \cdot f(x; k, \lambda) dx
$$

Substitute the PDF $f(x; k, \lambda)$ into this formula:
$$
E[X] = \int_0^\infty x \cdot \frac{\lambda^k x^{k-1} e^{-\lambda x}}{\Gamma(k)} dx
$$

Simplify the terms:
$$
E[X] = \frac{\lambda^k}{\Gamma(k)} \int_0^\infty x^k e^{-\lambda x} dx
$$

Now, substitute $t = \lambda x$, which implies $x = \frac{t}{\lambda}$ and $dx = \frac{dt}{\lambda}$:
$$
E[X] = \frac{\lambda^k}{\Gamma(k)} \int_0^\infty \left( \frac{t}{\lambda} \right)^k e^{-t} \frac{dt}{\lambda}
$$

Expand the terms:
$$
E[X] = \frac{\lambda^k}{\Gamma(k)} \cdot \frac{1}{\lambda^{k+1}} \int_0^\infty t^k e^{-t} dt
$$

Combine the powers of $\lambda$:
$$
E[X] = \frac{1}{\lambda} \cdot \frac{\int_0^\infty t^k e^{-t} dt}{\Gamma(k)}
$$

The integral $\int_0^\infty t^k e^{-t} dt$ is the definition of $\Gamma(k+1)$, and it is known that $\Gamma(k+1) = k \cdot \Gamma(k)$:
$$
E[X] = \frac{1}{\lambda} \cdot \frac{\Gamma(k+1)}{\Gamma(k)}
$$

Simplify using $\Gamma(k+1) = k \cdot \Gamma(k)$:
$$
E[X] = \frac{1}{\lambda} \cdot k
$$

Thus:
$$
E[X] = \frac{k}{\lambda}
$$

---

### **2. Variance ($V[X]$)**

Variance is defined as:
$$
V[X] = E[X^2] - (E[X])^2
$$

#### Step 1: Find $E[X^2]$:
We start with the definition of $E[X^2]$:
$$
E[X^2] = \int_0^\infty x^2 \cdot f(x; k, \lambda) dx
$$

Substitute the PDF $f(x; k, \lambda)$:
$$
E[X^2] = \int_0^\infty x^2 \cdot \frac{\lambda^k x^{k-1} e^{-\lambda x}}{\Gamma(k)} dx
$$

Simplify:
$$
E[X^2] = \frac{\lambda^k}{\Gamma(k)} \int_0^\infty x^{k+1} e^{-\lambda x} dx
$$

Using the substitution $t = \lambda x$, $x = \frac{t}{\lambda}$, and $dx = \frac{dt}{\lambda}$:
$$
E[X^2] = \frac{\lambda^k}{\Gamma(k)} \int_0^\infty \left( \frac{t}{\lambda} \right)^{k+1} e^{-t} \frac{dt}{\lambda}
$$

Expand:
$$
E[X^2] = \frac{\lambda^k}{\Gamma(k)} \cdot \frac{1}{\lambda^{k+2}} \int_0^\infty t^{k+1} e^{-t} dt
$$

Combine powers of $\lambda$:
$$
E[X^2] = \frac{1}{\lambda^2} \cdot \frac{\int_0^\infty t^{k+1} e^{-t} dt}{\Gamma(k)}
$$

The integral $\int_0^\infty t^{k+1} e^{-t} dt$ is $\Gamma(k+2)$, and it is known that $\Gamma(k+2) = (k+1) \cdot k \cdot \Gamma(k)$:
$$
E[X^2] = \frac{1}{\lambda^2} \cdot \frac{\Gamma(k+2)}{\Gamma(k)}
$$

Substitute $\Gamma(k+2) = (k+1) \cdot k \cdot \Gamma(k)$:
$$
E[X^2] = \frac{1}{\lambda^2} \cdot (k+1) \cdot k
$$

Simplify:
$$
E[X^2] = \frac{k(k+1)}{\lambda^2}
$$

#### Step 2: Use $V[X] = E[X^2] - (E[X])^2$:
From $E[X] = \frac{k}{\lambda}$, we have $(E[X])^2 = \frac{k^2}{\lambda^2}$.

Substitute into the variance formula:
$$
V[X] = \frac{k(k+1)}{\lambda^2} - \frac{k^2}{\lambda^2}
$$

Simplify:
$$
V[X] = \frac{k^2 + k}{\lambda^2} - \frac{k^2}{\lambda^2}
$$

$$
V[X] = \frac{k}{\lambda^2}
$$

---

### **Final Results**:
- $E[X] = \frac{k}{\lambda}$
- $V[X] = \frac{k}{\lambda^2}$

## ==**Erlang Distribution**==

The **Erlang distribution** is a special case of the Gamma distribution where the shape parameter $k$ is a positive integer. It models the sum of $k$ independent, exponentially distributed random variables, each with the same rate parameter $\lambda$. z

---

### **Key Properties of the Erlang Distribution**
### CDF

![[Pasted image 20241127114244.png]]



1. **PDF** (Probability Density Function):
   $$
   f(x; k, \lambda) = 
   \begin{cases} 
   \frac{\lambda^k x^{k-1} e^{-\lambda x}}{(k-1)!}, & x > 0 \\
   0, & x \leq 0
   \end{cases}
   $$
   - $k$: Shape parameter (positive integer, representing the number of phases or events).
   - $\lambda$: Rate parameter (frequency of occurrence of events).

2. **Mean**:
   $$
   E[X] = \frac{k}{\lambda}
   $$

3. **Variance**:
   $$
   V[X] = \frac{k}{\lambda^2}
   $$

4. **Special Case**:
   When $k = 1$, the Erlang distribution becomes the exponential distribution:
   $$
   f(x; \lambda) = \lambda e^{-\lambda x}, \quad x > 0
   $$

---

### **Understanding Erlang Distribution with an Example**

#### **Scenario: Phone Call System**

Imagine a phone call center where calls arrive at a constant rate of $\lambda = 2$ calls per minute. You want to model the time it takes for **3 calls to arrive**. 

- Here, the shape parameter is $k = 3$, as you are waiting for the 3rd event (call).
- The rate parameter is $\lambda = 2$, meaning calls arrive on average every $\frac{1}{\lambda} = 0.5$ minutes.

---

#### **Step 1: Write the PDF**

The PDF of the Erlang distribution for $k = 3$ and $\lambda = 2$ is:
$$
f(x; 3, 2) = \frac{2^3 x^{3-1} e^{-2x}}{(3-1)!}
$$

Simplify:
$$
f(x; 3, 2) = \frac{8x^2 e^{-2x}}{2!} = 4x^2 e^{-2x}, \quad x > 0
$$

---

#### **Step 2: Compute the Mean and Variance**

Using the formulas:
- Mean:
  $$
  E[X] = \frac{k}{\lambda} = \frac{3}{2} = 1.5 \, \text{minutes}
  $$
  This means that, on average, it takes 1.5 minutes for 3 calls to arrive.

- Variance:
  $$
  V[X] = \frac{k}{\lambda^2} = \frac{3}{2^2} = 0.75 \, \text{minutes}^2
  $$

---

#### **Step 3: Example Calculation of Probability**

**What is the probability that the waiting time for 3 calls is less than 1 minute?**

This corresponds to finding the **CDF** at $x = 1$:
$$
P(X \leq 1) = F(1; 3, 2) = \int_0^1 4x^2 e^{-2x} dx
$$

**Step-by-Step Integration**:
The integral $\int_0^x t^{k-1} e^{-\lambda t} dt$ can be solved using the incomplete Gamma function or numerically.

For this example, using numerical methods:
$$
P(X \leq 1) \approx 0.323
$$

This means there is about a **32.3% chance** that the time for 3 calls to arrive will be less than 1 minute.

---

### **Applications of Erlang Distribution**

1. **Queueing Theory**:
   - To model waiting times in multi-phase systems (e.g., multiple stages of service in a call center or hospital).

2. **Telecommunications**:
   - Used to model packet arrival times or call durations.

3. **Reliability Engineering**:
   - To model the time until failure in systems with multiple components operating in series.

---

### **Visualization**

To better understand, imagine the shape of the PDF for $k = 3$ and $\lambda = 2$:
- It starts at $x = 0$,
- Peaks around the mean ($E[X] = 1.5$),
- And gradually decreases as $x \to \infty$, representing the diminishing likelihood of extremely long waiting times.

b### Example 1
To compute $P(X_1 + X_2 > 2)$, where $X_1$ and $X_2$ are independent exponential random variables with rate parameter $\lambda = 1$, we follow these steps:

---

#### **Step 1: Understand the Problem**

The sum of two independent exponential random variables with the same rate parameter $\lambda$ follows an **Erlang distribution**. Specifically:

$$
X_1 + X_2 \sim \text{Erlang}(k = 2, \lambda = 1)
$$

The PDF of the Erlang distribution with $k = 2$ is:
$$
f_{X_1 + X_2}(x) = \lambda^k \frac{x^{k-1} e^{-\lambda x}}{(k-1)!}
$$

Substitute $k = 2$ and $\lambda = 1$:
$$
f_{X_1 + X_2}(x) = x e^{-x}, \quad x > 0
$$

---

#### **Step 2: Define the Probability**

We need to compute $P(X_1 + X_2 > 2)$. Using the complement rule:
$$
P(X_1 + X_2 > 2) = 1 - P(X_1 + X_2 \leq 2)
$$

The cumulative probability $P(X_1 + X_2 \leq 2)$ is given by the **CDF** of the Erlang distribution:
$$
P(X_1 + X_2 \leq 2) = \int_0^2 f_{X_1 + X_2}(x) \, dx = \int_0^2 x e^{-x} \, dx
$$

---

#### **Step 3: Solve the Integral**

To compute $\int_0^2 x e^{-x} \, dx$, we use **integration by parts**. Let:
- $u = x$, so $du = dx$
- $dv = e^{-x} dx$, so $v = -e^{-x}$

The integration by parts formula is:
$$
\int u \, dv = uv - \int v \, du
$$

Substitute:
$$
\int x e^{-x} dx = -x e^{-x} + \int e^{-x} dx
$$

Solve the second integral:
$$
\int e^{-x} dx = -e^{-x}
$$

So:
$$
\int x e^{-x} dx = -x e^{-x} - e^{-x} = -(x + 1)e^{-x}
$$

Evaluate from $0$ to $2$:
$$
\int_0^2 x e^{-x} dx = \left[ -(x + 1)e^{-x} \right]_0^2
$$

At $x = 2$:
$$
-(2 + 1)e^{-2} = -3 e^{-2}
$$

At $x = 0$:
$$
-(0 + 1)e^{0} = -1
$$

So:
$$
\int_0^2 x e^{-x} dx = -3 e^{-2} - (-1) = 1 - 3e^{-2}
$$

---

#### **Step 4: Compute the Complement**

$$
P(X_1 + X_2 > 2) = 1 - P(X_1 + X_2 \leq 2)
$$

Substitute:
$$
P(X_1 + X_2 > 2) = 1 - (1 - 3e^{-2}) = 3e^{-2}
$$

---

### **Final Answer**

The probability is:
$$
P(X_1 + X_2 > 2) = 3e^{-2}
$$

Using $e^{-2} \approx 0.1353$:
$$
P(X_1 + X_2 > 2) \approx 3 \cdot 0.1353 = 0.4059
$$

So the probability is approximately **0.406** or **40.6%**.


