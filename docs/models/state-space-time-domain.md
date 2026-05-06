If we solve the following equation using the homogeneous solution. Therefore, implying that both $u(t)$ and $w(t)$ are zero under the Laplace domain.
$$\dot{x}(t)=Ax(t)+Bu(t)+w(t)$$
Then:

$$sX(s)-x(0)=AX(s)$$
Reorganizing:
$$(sI-A)X(s)=x(0) \rightarrow X(s)=\left(sI-A\right)^{-1}x(0)$$
Finally
$$x(t)=\mathcal{L}^{-1}\left[(sI-A)^{-1}\right]x(0)$$
## The state-transition matrix
By using expansion
$$(sI-A)^{-1}=\frac{I}{s}+\frac{A}{s^2}+\frac{A^2}{s^3}+\dots$$
$$\mathcal{L}^{-1}\left[\left(sI-A\right)^{-1}\right]=I+At+\frac{A^2t^2}{2!}+\frac{A^3t^3}{3!}+\dots\triangleq e^{at}$$
### Forced state
$$x(t)=e^{At}x(0)+\int_0^{t}e^{A(t-\tau)}Bu(\tau)d\tau$$
Then:
$$z(t)=Cx(t)+Du(t)\rightarrow z(t)=Ce^{At}x(0)+\int_0^{t}Ce^{A(t-\tau)}Bu(\tau)d\tau+Du(t)$$
- $Ce^{At}x(0)$ Initial response
- $\int_0^{t}Ce^{A(t-\tau)}Bu(\tau)d\tau$ Convolution
- $Du(t)$ Feedthrough
