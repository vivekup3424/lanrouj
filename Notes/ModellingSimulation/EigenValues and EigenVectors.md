To calculate **eigenvalues** and **eigenvectors** of a matrix $A$, follow these steps:

---

### **1. Find the Eigenvalues**
The eigenvalues $\lambda$ satisfy the **characteristic equation**:
$$
|A - \lambda I| = 0,
$$
where $I$ is the identity matrix of the same size as $A$.

#### **Steps to Find Eigenvalues:**
1. **Form the matrix $A - \lambda I$:**
   Subtract $\lambda$ times the identity matrix $I$ from $A$. For example, if
   $$
   A = \begin{bmatrix} a & b \\ c & d \end{bmatrix},
   $$
   then
   $$
   A - \lambda I = \begin{bmatrix} a - \lambda & b \\ c & d - \lambda \end{bmatrix}.
   $$

2. **Compute the determinant $|A - \lambda I|$:**
   Expand the determinant of $A - \lambda I$. For the above example:
   $$
   |A - \lambda I| = \det \begin{bmatrix} a - \lambda & b \\ c & d - \lambda \end{bmatrix}
   = (a - \lambda)(d - \lambda) - bc.
   $$

3. **Solve the resulting polynomial:**
   The determinant gives a polynomial equation in $\lambda$. Solve it to find the eigenvalues. For a $2 \times 2$ matrix, this is a quadratic equation.

---

### **2. Find the Eigenvectors**
For each eigenvalue $\lambda$, find the corresponding eigenvector $x$ such that:
$$
(A - \lambda I)x = 0.
$$

#### **Steps to Find Eigenvectors:**
1. **Substitute each eigenvalue $\lambda$:**
   Plug $\lambda$ into $A - \lambda I$ to get a new matrix $M = A - \lambda I$.

2. **Solve the equation $Mx = 0$:**
   This is a homogeneous system of linear equations. Write the augmented matrix of the system and solve using Gaussian elimination or row reduction.

   - The solutions will typically depend on one or more free variables. The eigenvector $x$ is any non-zero solution vector to this system.
   - Normalize $x$ (optional) for convenience.

#### Example:
If $A = \begin{bmatrix} 4 & 1 \\ 2 & 3 \end{bmatrix}$:
1. Find $|A - \lambda I|$:
   $$
   A - \lambda I = \begin{bmatrix} 4 - \lambda & 1 \\ 2 & 3 - \lambda \end{bmatrix}.
   $$
   The determinant is:
   $$
   |A - \lambda I| = (4 - \lambda)(3 - \lambda) - 2 = \lambda^2 - 7\lambda + 10.
   $$
   Solve $\lambda^2 - 7\lambda + 10 = 0$, yielding $\lambda_1 = 5$, $\lambda_2 = 2$.

2. For $\lambda_1 = 5$:
   $$
   A - 5I = \begin{bmatrix} -1 & 1 \\ 2 & -2 \end{bmatrix}.
   $$
   Solve $\begin{bmatrix} -1 & 1 \\ 2 & -2 \end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \end{bmatrix} = 0$, giving $x_1 = x_2$.

   Eigenvector: $x = \begin{bmatrix} 1 \\ 1 \end{bmatrix}$.

3. Repeat for $\lambda_2 = 2$.

---

### **Conclusion**
- **Eigenvalues** come from solving $|A - \lambda I| = 0$.
- **Eigenvectors** are solutions to $(A - \lambda I)x = 0$ for each eigenvalue.
- **Trace of A** = sum of eigenValues
- **Determinant of A** = product of eigenValues