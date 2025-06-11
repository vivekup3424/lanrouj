---
id: Assumptions of Linear Regression
aliases: 
tags:
  - linear-regression
  - multicollinearity
  - vif
---
### **Variance Inflation Factor (VIF)**

Variance Inflation Factor (VIF) is a metric used to assess the extent of **multicollinearity** in a linear regression model. Multicollinearity occurs when two or more independent variables (predictors) are highly correlated with each other. When multicollinearity is present, it can make it difficult to interpret the individual effects of predictors.
The VIF quantifies how much the variance of a regression coefficient is inflated due to correlation with other independent variables. Higher VIF values indicate higher correlation with other predictors, which suggests multicollinearity.

### **Understanding VIF:**

#### **Formula for VIF**:

For each independent variable $X_i$ in a regression model, the VIF is calculated as:

$$
VIF(X_i) = \frac{1}{1 - R_i^2}
$$

Where:
- $R_i^2$ is the **coefficient of determination** (R-squared) obtained by regressing $X_i$ on all the other predictors in the model.
- $R_i^2$ indicates how much of the variability in $X_i$ is explained by the other independent variables.

### **Steps to Calculate VIF**:

1. **For each predictor $X_i$**, run a regression where $X_i$ is the dependent variable and all other independent variables are the predictors.
2. **Compute the $R_i^2$** (R-squared value) from this regression.
3. **Compute the VIF** using the formula:  
   $$
VIF(X_i) = \frac{1}{1 - R_i^2}
$$
4. Repeat for all the independent variables in the model.

### **Interpreting VIF**:

- **VIF = 1**: No correlation with other predictors. This means that the predictor $X_i$ is not correlated with any other independent variable in the model.
- **VIF > 1**: There is some correlation with other predictors. The larger the VIF, the greater the correlation.
- **VIF > 5-10**: This is often considered an indication of high multicollinearity. A VIF above this threshold suggests that the predictor variable is highly correlated with the other predictors, and its coefficient estimate is unstable.
- **VIF approaching infinity**: This indicates perfect multicollinearity, where a predictor is linearly dependent on other variables, causing redundancy in the model.

### **Example of VIF Calculation**:

Let’s assume you are building a model to predict **house prices** based on three variables:
1. Size of the house ($X_1$)
2. Number of rooms ($X_2$)
3. Age of the house ($X_3$)

Now, let’s check for multicollinearity between these variables.

#### **Step 1**: Regress each independent variable on the others.

- For $X_1$, regress it on $X_2$ and $X_3$ to get $R_1^2$.
- For $X_2$, regress it on $X_1$ and $X_3$ to get $R_2^2$.
- For $X_3$, regress it on $X_1$ and $X_2$ to get $R_3^2$.

#### **Step 2**: Calculate the VIF for each variable.

- $VIF(X_1) = \frac{1}{1 - R_1^2}$
- $VIF(X_2) = \frac{1}{1 - R_2^2}$
- $VIF(X_3) = \frac{1}{1 - R_3^2}$

If, for example:
- $R_1^2 = 0.85$, then $VIF(X_1) = \frac{1}{1 - 0.85} = 6.67$
- $R_2^2 = 0.90$, then $VIF(X_2) = \frac{1}{1 - 0.90} = 10$
- $R_3^2 = 0.60$, then $VIF(X_3) = \frac{1}{1 - 0.60} = 2.5$

In this case:
- **$VIF(X_1) = 6.67$**: This suggests that the size of the house is moderately correlated with the other predictors.
- **$VIF(X_2) = 10$**: The number of rooms is highly correlated with the other predictors, suggesting potential multicollinearity issues.
- **$VIF(X_3) = 2.5$**: Age of the house is moderately correlated with the other predictors but not as much as the number of rooms.

#### **Step 3**: Interpretation
- The VIF for $X_2$ (number of rooms) exceeds 5, indicating **high multicollinearity** with the other predictors. You may need to reconsider including this predictor or take steps like combining variables or using **Principal Component Analysis (PCA)** to reduce multicollinearity.

---

### **How to Address High VIF (Multicollinearity)**:

1. **Remove highly correlated variables**: If two variables have a very high correlation, consider removing one of them.
2. **Combine variables**: If predictors are measuring the same underlying concept, consider combining them (e.g., taking the average of correlated variables).
3. **Principal Component Analysis (PCA)**: PCA can be used to reduce the dimensionality of the data and remove multicollinearity by transforming correlated predictors into a smaller number of uncorrelated components.
4. **Ridge Regression**: This is a regularization technique that can help mitigate the impact of multicollinearity by adding a penalty term to the regression model, reducing the influence of highly correlated predictors.

---

### **Summary**:

- **VIF** is a key tool in detecting **multicollinearity** in regression models. It measures how much the variance of a regression coefficient is inflated due to correlation with other predictors.
- **High VIF values** (greater than 5-10) indicate the presence of multicollinearity, which can lead to unstable and unreliable regression coefficients.
- **Strategies to reduce multicollinearity** include removing or combining correlated variables, using dimensionality reduction techniques like PCA, or applying regularization techniques like Ridge Regression.

By checking and addressing multicollinearity, you can improve the stability and interpretability of your regression model.
