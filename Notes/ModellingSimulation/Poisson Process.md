Here are simplified notes on the **Poisson Process** based on the provided attachment, focusing on its mathematical and conceptual elements:

---

### Overview

A **Poisson Process** is a type of counting process commonly used to model random events that happen independently over time. Examples include the arrival of emails at a server, calls to a call center, or breakdowns of machines in a factory. 

#### Notation:
- Let $(N(t))$ represent the total number of events that have occurred by time (t), where$ $( t \geq 0 )$.
- (N(t)) is a random variable with possible values $( 0, 1, 2, \ldots )$.

#### Characteristics of a Poisson Process
A process $( \{ N(t), t \geq 0 \} )$ is considered a Poisson Process with a rate $( \lambda )$ if it satisfies the following properties:

1. **Single Events**: Events occur one at a time, with no simultaneous events.
   
2. **Stationary Increments**: The probability of a given number of arrivals between any interval $( t )$ and $( t + s )$ depends only on the interval length $( s )$, not on the starting time $( t )$. This means events happen **uniformly** over time.

3. **Independent Increments**: The number of events in disjoint time intervals are independent. For example, the number of arrivals in the interval $( [0, 1] )$ does not affect the number of arrivals in $( [2, 3] )$. Thus, future events are **independent** of past events.

---

### Mathematical Definition

If arrivals follow a Poisson Process, then for any time \( t \geq 0 \), the probability that exactly \( n \) events have occurred by time \( t \) is given by:

$$
P(N(t) = n) = \frac{e^{-\lambda t} (\lambda t)^n}{n!}

$$

where:
- $( \lambda )$: the average rate of events per unit time.
- $( e )$: the base of the natural logarithm (approximately 2.718).
- $( n! )$: factorial of $( n )$ (the product of all positive integers up to $(1,2, \dots n )$.

This formula represents the **Poisson probability distribution**. It describes the likelihood of observing $( n )$ events in a given time interval $( t )$.

---

### Mean and Variance

For a Poisson Process $( N(t) )$ with rate $( \lambda )$:
- The **mean** number of events by time \( t \) is $( \mathbb{E}[N(t)] = \lambda t )$.
- The **variance** of the number of events by time \( t \) is \( \text{Var}(N(t)) = \lambda t \).

This indicates that, on average, the number of arrivals grows linearly with time, and the spread (variance) of the arrival count also increases linearly with time.

---

### Visualization

1. **Counting Process Plot**: 
   - On the y-axis, plot \( N(t) \), the cumulative count of events.
   - On the x-axis, plot time \( t \).
   - As time progresses, the count \( N(t) \) will increase, with jumps occurring at random intervals. Each jump represents an event (arrival). 

2. **Probability Distribution at Time \( t \)**:
   - At any fixed time \( t \), the number of arrivals \( N(t) \) follows a Poisson distribution. 
   - For example, if \( \lambda = 2 \) events per hour, and we examine the process at \( t = 1 \) hour, then \( N(1) \) follows a Poisson distribution with mean \( 2 \). This distribution can be visualized as a bar chart with probabilities for different event counts (0, 1, 2, 3, etc.).

### Intuition

- **Memoryless Property**: Events occur independently. Knowing how many events have occurred in the past doesn't help predict future events.
- **Example**: For a call center receiving calls at a rate of \( \lambda = 3 \) calls per minute, the probability of receiving exactly 5 calls in the next minute can be calculated using the Poisson formula.

---

### Summary

- A **Poisson Process** models random, independent events happening over time.
- The process is characterized by a constant rate \( \lambda \), stationary increments, and independence of non-overlapping intervals.
- \( N(t) \), the number of events by time \( t \), follows a **Poisson distribution** with mean and variance \( \lambda t \).

