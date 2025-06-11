Here’s how you can structure your notes for Obsidian with proper math blocks and formatting:

---

## Random Variables

### 1. **Discrete Random Variables**
- A random variable \( X \) is **discrete** if the number of possible values \( X \) can take is finite or countably infinite.
- The possible values of \( X \) are denoted as \( $x_1, x_2, x_3, \dots$ \).

#### Properties of a Discrete Random Variable:
1. \( $p(x_i) \geq 0$ \) for all \($i$\).
2. \( $\sum_{i=1}^\infty p(x_i) = 1$ \).

- The collection \( $(x_i, p(x_i))$ \) is called the **probability distribution** of \( $X$ \), where \( $p(x_i) = P(X = x_i)$ \) is the **probability mass function (pmf)**.

#### Example 5.1:
- Random variable: \( X = \text{number of jobs arriving each week} \).
- Range space: \( $R_X = \{ 0, 1, 2, \dots \}$ \).

#### Example 5.2:
- Experiment: Tossing a loaded die.
- \( X = \text{number of spots on the upper face of the die} \).
- Range space: \( $R_X = \{ 1, 2, 3, 4, 5, 6 \}$ \).
- \( $p(x_i) = \frac{x_i}{21}, \text{ for } i = 1, 2, \dots, 6$ \).
  - \( $p(1) = \frac{1}{21}, p(2) = \frac{2}{21}, \dots, p(6) = \frac{6}{21}$ \).
- Verify:
  - \( $p(x_i) \geq 0 ) and ( \sum_{i=1}^6 p(x_i) = 1$ \).

---

### 2. **Continuous Random Variables**
- \( X \) is **continuous** if its range \( R_X \) is an interval or a collection of intervals.
- The probability that \( X \) lies in an interval \([a, b]\) is given by:
  $$

  P(a \leq X \leq b) = \int_a^b f(x) \, dx

  $$
  where \( f(x) \) is the **probability density function (pdf)**.

#### Properties of the PDF:

1. $f(x) \geq 0 \text{ for all } x \in R_X.$

2. $\int_{R_X} f(x) \, dx = 1.$

3. $f(x) = 0 \text{ for } x \notin R_X.$


#### Implication:
- For any specific value \( x_0 \), \( P(X = x_0) = 0 \), because:
$$
  \int_{x_0}^{x_0} f(x) \, dx = 0
$$

---
