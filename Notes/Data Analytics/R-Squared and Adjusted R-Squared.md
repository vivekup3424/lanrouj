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
	To compute $R^2$, we need to calculate the **Total Sum of Squares** $SS_{\text{tot}}$, and the **Residual Sum of Squares** $SS_{\text{res}}$.
The Total Sum of Squares represents the total variation of the actual values $Y$ around their mean.

The formula is:
$$
SS_{\text{tot}} = \sum_{i=1}^{n} (Y_i - \bar{Y})^2
$$
Where:
- $Y_i$ is each actual value in the dataset,
- $\bar{Y}$ is the mean of the actual values.

First, we calculate the mean of $Y$:
$$
\bar{Y} = \frac{3 + 5 + 7}{3} = \frac{15}{3} = 5
$$

Now, calculate $SS_{\text{tot}}$:
$$
SS_{\text{tot}} = (3 - 5)^2 + (5 - 5)^2 + (7 - 5)^2
$$
$$
SS_{\text{tot}} = (-2)^2 + (0)^2 + (2)^2
$$
$$
SS_{\text{tot}} = 4 + 0 + 4 = 8
$$

2. **Residual Sum of Squares $SS_{\text{res}}$**:

The Residual Sum of Squares represents the difference between the actual values and the predicted values.

The formula is:
$$
SS_{\text{res}} = \sum_{i=1}^{n} (Y_i - \hat{Y}_i)^2
$$
Where:
- $Y_i$ is each actual value,
- $\hat{Y}_i$ is each predicted value.

Now, calculate $SS_{\text{res}}$:
$$
SS_{\text{res}} = (3 - 2.8)^2 + (5 - 5.1)^2 + (7 - 7.3)^2
$$
$$
SS_{\text{res}} = (0.2)^2 + (-0.1)^2 + (-0.3)^2
$$
$$
SS_{\text{res}} = 0.04 + 0.01 + 0.09 = 0.14
$$

3. **Calculate $R^2$**:

The formula for $R^2$ is:
$$
R^2 = 1 - \frac{SS_{\text{res}}}{SS_{\text{tot}}}
$$
Now, substitute the values for $SS_{\text{res}}$ and $SS_{\text{tot}}$:
$$
R^2 = 1 - \frac{0.14}{8}
$$
$$
R^2 = 1 - 0.0175
$$
$$
R^2 = 0.9825
$$
Final Answer:
The $R^2$ value is approximately **0.9825**, which indicates that 98.25% of the variance in the actual values is explained by the predicted values.



---

### **2. Adjusted R-Squared ($R^2_{adj}$)**
#### **Definition**
Adjusted R-squared adjusts $R^2$ for the number of predictors in the model. It accounts for the trade-off between adding new predictors and the improvement in fit.

#### **Formula**
$$
R^2_{adj} = 1 - \left( \frac{(n-1)}{(n-p-1)}(1 - R^2) \right)
$$
- $n$: Number of observations.
- $p$: Number of predictors (independent variables).
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
> [!NOTE]
> Adjusted R2 is always less than or equal to R2

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

