We can calculate the power and the exponential of a matrix using diagonalization. This can be achieved using the EigenValue and EigenVector decomposition, if we order them in the following way:
- $T=\begin{bmatrix}v_1&v_2&\dots v_n\end{bmatrix}$ as a matrix compound by the EigenVectors
- $\Lambda=\begin{bmatrix} \lambda_1 & 0 & \dots  &0 \\0 & \lambda_2 & 0 & \vdots \\ \vdots & 0 & \ddots & 0 \\ 0 & \dots & 0 & \lambda_n \end{bmatrix}$ as the diagonal matrix compund by the EigenValues ($\lambda_i$ ) 
Then the exponential and power expression can be solved by:

| Power                  | Exponential                |
| ---------------------- | -------------------------- |
| $A^n=T\Lambda^nT^{-1}$ | $e^{A}=Te^{\Lambda}T^{-1}$ |
> If we can’t diagonalize A, then there is a Jordan form (multiplying by sinusoids or polynomials).
## Interpretation
If the eigenvalues are real, then the system has growing (positive lambda) or decaying (negative lambda) behavior. If it contains a complex number, then it will be oscillating.


