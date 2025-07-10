---
id: Assumptions of Linear Regression
aliases: []
tags: []
---

Linear regression is a widely used statistical method for modeling the relationship between a dependent variable and one or more independent variables. However, for the model to be valid and produce reliable results, several key assumptions must be satisfied. If these assumptions are violated, the model may give biased, inefficient, or misleading estimates. Let's go through each of these assumptions in depth.

---

### **1. Linearity**
   - **Assumption**: The relationship between the dependent variable (\(Y\)) and the independent variable(s) (\(X\)) is **linear**.
   - **Implication**: This means that the change in the dependent variable is proportional to a change in the independent variables. The model assumes that the effect of each independent variable on the dependent variable is constant.
   - **Example**: If you are predicting house prices based on size (in square feet), the model assumes that as size increases, the price increases by a fixed amount for each additional square foot.

   - **How to Check**:
     - Plot the **scatter plot** of the dependent variable against each independent variable. If the relationship is not linear (e.g., curvilinear), linear regression may not be appropriate.

---

### **2. Homoscedasticity**
![[Pasted image 20241201222528.png]]

   - **Assumption**: The residuals (errors) have **constant variance** across all levels of the independent variable(s).
   - **Implication**: The spread of the residuals should be approximately the same for all predicted values of the dependent variable. This means that as the fitted values of \(Y\) increase or decrease, the residuals should have a consistent variance, i.e., they should not "fan out" or "collapse in" (which would indicate heteroscedasticity).
   - **Example**: In a model predicting house prices, the variability of the prediction error should be similar whether the house price is low or high.

   - **How to Check**:
   ![[Pasted image 20241201222626.png]]
     - **Residual vs. Fitted plot**: Plot residuals against predicted values. If the plot shows a "funnel" shape (widening or narrowing of residuals), then there is evidence of **heteroscedasticity**.
    
![[Pasted image 20241201222749.png]]

---

### **3. Normality of Errors**
   - **Assumption**: The residuals (errors) are **normally distributed**.
   - It does not mean that X or Y are normally distributed.
   - It means that error should have 0 as mean, and the variance or width of the error around best-fit line should be constant.
   - **Example**: In regression analysis of student test scores, the errors should be symmetrically distributed around zero.

   - **How to Check**:
     - **Q-Q plot (Quantile-Quantile plot)**: A Q-Q plot compares the distribution of residuals with a normal distribution. If the residuals follow a straight line in the plot, they are approximately normally distributed.

---

### **4. No Multicollinearity** or Independence of features
   - **Assumption**: The independent variables are **not highly correlated** with each other.
   - **Implication**: High correlation between independent variables (multicollinearity) can make it difficult to estimate the individual effects of each predictor. This can lead to inflated standard errors, making it harder to determine which predictor variables are truly significant.
   - **Example**: In a regression model predicting house prices, if both the **size of the house** and the **number of rooms** are highly correlated, it could lead to multicollinearity.

   - **How to Check**:
     - **Correlation matrix**: Check the correlation between independent variables. If correlations are high (e.g., above 0.8 or 0.9), multicollinearity may be present.
     - **Variance Inflation Factor (VIF)**: [[VIF]] quantifies how much the variance of the estimated regression coefficient is inflated due to collinearity with other predictors. A VIF above 10 is typically considered problematic.

---

### **6. No Significant Outliers**
   - **Assumption**: The dataset should not have **influential outliers** that disproportionately affect the regression model.
   - Regression models get deeply affected by outliers, unlike decision trees.
   - **Implication**: Outliers can have a significant impact on the regression coefficients and distort the results, especially in linear regression where the model fits the data using least squares.
   - **Example**: In predicting income, an extremely high income for one observation might distort the model, making it biased.

---

### **Summary of Linear Regression Assumptions**:

1. **Linearity**: The relationship between predictors and the response is linear.
2. **Independence of Errors**: Errors are independent of each other.
3. **Homoscedasticity**: Errors have constant variance.
4. **Normality of Errors**: Errors follow a normal distribution (for hypothesis testing and confidence intervals).
5. **No Multicollinearity**: Independent variables are not highly correlated with each other.
7. **No Significant Outliers**: There should be no influential outliers that distort the model.

---

