### **R-Squared and Adjusted R-Squared: Concepts and Differences**

R-squared ($R^2$) and Adjusted R-squared ($R^2_{adj}$) are metrics used to evaluate the goodness of fit of a regression model. They measure how well the independent variables explain the variability in the dependent variable. Let's delve into their definitions, calculations, and key differences.

---

### **1. R-Squared ($R^2$)**
#### **Definition**
R-squared measures the proportion of the total variance in the dependent variable ($Y$) that is explained by the independent variables in the regression model.

#### **Formula**
$$
R^2 = 1 - \frac{SS_{res}}{SS_{tot}}
$$
- $SS_{res}$: Residual sum of squares ($\sum (y_i - \hat{y}_i)^2$).
- $SS_{tot}$: Total sum of squares ($\sum (y_i - \bar{y})^2$).
- $\hat{y}_i$: Predicted values.
- $\bar{y}$: Mean of actual values.

#### **Interpretation**
- $R^2 = 1$: Perfect fit; the model explains all the variance in $Y$.
- $R^2 = 0$: The model explains none of the variance in $Y$.
- $R^2$ is **non-negative** and increases as more independent variables are added, regardless of whether they improve the model.

#### **Example**
- Suppose a dataset has actual values $Y = [3, 5, 7]$ and predicted values $\hat{Y} = [2.8, 5.1, 7.3]$.
- Compute $SS_{tot}$ and $SS_{res}$, then calculate $R^2$.

---

### **2. Adjusted R-Squared ($R^2_{adj}$)**
#### **Definition**
Adjusted R-squared adjusts $R^2$ for the number of predictors in the model. It accounts for the trade-off between adding new predictors and the improvement in fit.

#### **Formula**
$$
R^2_{adj} = 1 - \left( \frac{SS_{res}/(n-k-1)}{SS_{tot}/(n-1)} \right)
$$
- $n$: Number of observations.
- $k$: Number of predictors (independent variables).

#### **Why Adjusted?**
- Adding predictors always increases $R^2$, even if they do not significantly contribute to the model.
- Adjusted $R^2$ penalizes for adding predictors that do not improve the model.

#### **Interpretation**
- $R^2_{adj}$ can decrease if a new predictor does not sufficiently improve the model.
- It is preferred when comparing models with different numbers of predictors.

#### **Example**
- Consider the same dataset, but compare models with $k = 1$ and $k = 2$ predictors. Compute $R^2$ and $R^2_{adj}$ to see the effect of adding a predictor.

---

### **3. Key Differences Between R-Squared and Adjusted R-Squared**
| **Aspect**              | **R-Squared**                                                                 | **Adjusted R-Squared**                                                                                      |
|--------------------------|-------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------|
| **Formula**             | Measures the proportion of variance explained by the model.                  | Adjusts $R^2$ to account for the number of predictors.                                                  |
| **Impact of New Predictors** | Always increases when new predictors are added, regardless of their relevance. | Can decrease if a new predictor does not improve the model significantly.                                   |
| **Complexity Penalty**  | Does not penalize for model complexity.                                       | Penalizes for adding predictors that do not improve model fit.                                              |
| **Purpose**             | Descriptive: Measures overall goodness of fit.                              | Comparative: Helps compare models with different numbers of predictors.                                     |
| **Value Range**         | Always between 0 and 1 (for linear regression).                              | Can be negative if the model performs worse than using the mean as a predictor.                             |

---

### **4. When to Use**
- Use **R-squared** when you are assessing the general fit of a single model.
- Use **Adjusted R-squared** when comparing models with different numbers of predictors to avoid overfitting.

---

### **5. Practical Example with a Dataset**

#### **Dataset**:
- $Y$: Sales.
- Predictors: Advertising Spend ($X_1$), Number of Stores ($X_2$), Economic Index ($X_3$).

#### **Scenario 1: Model with One Predictor ($X_1$)**
- $R^2 = 0.75$, $R^2_{adj} = 0.74$.

#### **Scenario 2: Model with Three Predictors ($X_1, X_2, X_3$)**
- $R^2 = 0.85$, $R^2_{adj} = 0.82$.

Adding $X_3$ increased $R^2$, but $R^2_{adj}$ increased less, indicating $X_3$ has a small contribution relative to $X_1$ and $X_2$.

---

Let me know if you'd like a code example in Python to demonstrate these calculations!
