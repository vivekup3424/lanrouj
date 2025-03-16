### Gradient Descent/Ascent and Related Concepts: A Deep Dive

Gradient Descent and Gradient Ascent are optimization techniques used to minimize or maximize a function. They are foundational in machine learning, especially for training models like neural networks. Here's an in-depth look at these topics, broken into key sections with examples.

---

## **1. Gradient Descent/Ascent: Principles and Working**
### **Gradient Descent**
- **Principle**: Gradient Descent minimizes a given function $f(\theta)$ by iteratively updating the parameters $\theta$ in the direction of the negative gradient.
- **Mathematics**:
  $$
  \theta = \theta - \eta \cdot \nabla f(\theta)
  $$
  - $\theta$: Parameters to be optimized.
  - $\eta$: Learning rate, which controls the step size.
  - $\nabla f(\theta)$: Gradient of the function $f(\theta)$, i.e., the vector of partial derivatives.

### **Gradient Ascent**
- **Principle**: Gradient Ascent is used to maximize a function $f(\theta)$. It updates the parameters in the direction of the gradient:
  $$
  \theta = \theta + \eta \cdot \nabla f(\theta)
  $$

**Example**:
- Let $f(\theta) = \theta^2 - 4\theta + 4$.
- Gradient of $f(\theta)$: $\nabla f(\theta) = 2\theta - 4$.

For Gradient Descent (minimization):
- Update rule: $\theta = \theta - \eta \cdot (2\theta - 4)$.

For Gradient Ascent (maximization):
- Update rule: $\theta = \theta + \eta \cdot (2\theta - 4)$.

---

## **2. Key Terms**
### **Epoch**
- **Definition**: One full pass through the entire dataset during training.
- **Example**:
  - Dataset: $\{x_1, x_2, x_3\}$.
  - An epoch means the model processes $x_1$, $x_2$, and $x_3$ once.

### **Batch Size**
- **Definition**: The number of samples processed in a single update of the model's parameters.
- **Example**:
  - Dataset: 100 samples.
  - Batch size: 20.
  - It takes $100 / 20 = 5$ batches to complete one epoch.

### **Iteration**
- **Definition**: One parameter update step.
- **Example**:
  - If batch size = 20 and there are 100 samples, there are 5 iterations per epoch.

---

## **3. Types of Gradient Descent**
### **(a) Batch Gradient Descent**
- **What it is**: Uses the entire dataset to compute the gradient before updating parameters.
- **Formula**:
  $$
  \theta = \theta - \eta \cdot \frac{1}{N} \sum_{i=1}^N \nabla f_i(\theta)
  $$
  - $N$: Total number of samples.

- **Pros**:
  - Stable convergence.
  - Suitable for smaller datasets.
- **Cons**:
  - Computationally expensive for large datasets.

**Example**:
- Dataset: $x = [1, 2, 3, 4]$, $y = [2, 4, 6, 8]$.
- Cost function (MSE): $f(\theta) = \frac{1}{N} \sum_{i=1}^N (y_i - \theta x_i)^2$.

At each step, use all $x$ and $y$ values to compute the gradient.

---

### **(b) Stochastic Gradient Descent (SGD)**
- **What it is**: Updates parameters using only one sample at a time.
- **Formula**:
  $$
  \theta = \theta - \eta \cdot \nabla f_i(\theta)
  $$
  - $f_i(\theta)$: Loss for a single sample $i$.

- **Pros**:
  - Computationally efficient.
  - Can escape local minima due to noise.
- **Cons**:
  - High variance in updates, leading to less stable convergence.

**Example**:
- For each sample $(x_i, y_i)$, update $\theta$ independently:
  - Compute $f_i(\theta)$ and $\nabla f_i(\theta)$ for $x_1, x_2, \dots$.

---

### **(c) Mini-Batch Gradient Descent**
- **What it is**: Combines the benefits of Batch and Stochastic Gradient Descent. Updates parameters using a small batch of data.
- **Formula**:
  $$
  \theta = \theta - \eta \cdot \frac{1}{k} \sum_{i=1}^k \nabla f_i(\theta)
  $$
  - $k$: Batch size.

- **Pros**:
  - Balances computational efficiency and stability.
  - Works well with large datasets.
- **Cons**:
  - Requires tuning the batch size.

**Example**:
- Dataset: $x = [1, 2, 3, 4, 5, 6]$, batch size = 2.
- For each batch $\{x_1, x_2\}, \{x_3, x_4\}, \{x_5, x_6\}$, compute gradients and update parameters.

---

## **4. Types of Optimizers**
Optimizers improve the basic gradient descent algorithm by adjusting the learning rate or modifying the gradient.

### **(a) Momentum**
- **What it is**: Adds a fraction of the previous update to the current update to accelerate convergence.
- **Formula**:
  $$
  v_t = \gamma v_{t-1} + \eta \nabla f(\theta_t)
  $$
  $$
  \theta = \theta - v_t
  $$
  - $\gamma$: Momentum coefficient.

### **(b) RMSProp**
- **What it is**: Scales the learning rate for each parameter inversely proportional to the square root of the average of recent squared gradients.
- **Formula**:
  $$
  \theta = \theta - \frac{\eta}{\sqrt{E[g^2] + \epsilon}} \cdot \nabla f(\theta)
  $$

### **(c) Adam**
- **What it is**: Combines Momentum and RMSProp for adaptive learning rates.
- **Formula**:
  $$
  m_t = \beta_1 m_{t-1} + (1 - \beta_1) \nabla f(\theta_t)
  $$
  $$
  v_t = \beta_2 v_{t-1} + (1 - \beta_2) \nabla f(\theta_t)^2
  $$
  $$
  \theta = \theta - \eta \cdot \frac{m_t}{\sqrt{v_t} + \epsilon}
  $$
  - $m_t$: Exponentially weighted moving average of gradients.
  - $v_t$: Exponentially weighted moving average of squared gradients.

---

## **5. Practical Example**
### Dataset:
Let’s train a linear regression model:
$$
y = \theta_0 + \theta_1 x + \epsilon
$$

### Cost Function:
Mean Squared Error (MSE):
$$
J(\theta) = \frac{1}{N} \sum_{i=1}^N (y_i - (\theta_0 + \theta_1 x_i))^2
$$

### Optimization:
- Use **Batch Gradient Descent**:
  - Compute the gradients:
    $$
    \frac{\partial J}{\partial \theta_0} = -\frac{2}{N} \sum (y_i - (\theta_0 + \theta_1 x_i))
    $$
    $$
    \frac{\partial J}{\partial \theta_1} = -\frac{2}{N} \sum x_i (y_i - (\theta_0 + \theta_1 x_i))
    $$
  - Update $\theta_0$ and $\theta_1$ using gradient descent rules.

---

Let me know if you want detailed code or further clarifications!
