## Is it even possible for a KF to estimate this model’s state?
We define a system to be observable if we can determine its initial state vector $x(0)$ via processing its input signal $u(t)$ and its output signal $z(t)$
### Finding an equation describing output derivatives
Suppose we have the following model:
$$\begin{align}\dot{x}(t)=Ax(t)+Bu(t)\\z(t)=Cx(t)+Du(t)\end{align}\rightarrow z^{(k)}_{(0)}=CA^kx(0)+CA^{k-1}u(0)+\dots+CBu^{(k-1)}(0)+Du^{(k)}(0)$$
> Up script $^{(k)}$ means derivative not power

Let's write $z$ expression when we have three elements $n=3$
$$\begin{bmatrix}z_{(0)}\\\dot{z}_{(0)}\\\ddot{z}_{(0)}\end{bmatrix}=\underbrace{ \begin{bmatrix}C\\CA\\CA^2\end{bmatrix}}_{\mathcal{O}(C,A)}x(0)+\underbrace{ \begin{bmatrix}D&0&0\\CB&D&0\\CAB&CB&D\end{bmatrix}}_{\mathcal{T}}\begin{bmatrix}u_{(0)}\\\dot{u}_{(0)}\\\ddot{u}_{(0)}\end{bmatrix}$$
- $\mathcal{O}$ is the observability matrix. It is observable if it isn't singular
- $\mathcal{T}$ Toeplitz matrix
>A [Toeplitz matrix](https://en.wikipedia.org/wiki/Toeplitz_matrix) (diagonal-constant matrix) is a matrix where each descending diagonal from left to right contains the same elements.

Then if $\mathcal{O}$ is invertible (non singular), then
$$x(0)=\mathcal{O}^{-1} \left\{\begin{bmatrix}z_{(0)}\\\dot{z}_{(0)}\\\ddot{z}_{(0)}\end{bmatrix} - \mathcal{T}\begin{bmatrix}u_{(0)}\\\dot{u}_{(0)}\\\ddot{u}_{(0)}\end{bmatrix}\right\}$$
> For multiple output systems $\mathcal{O}$ must be full rank

However, if we calculate $x(0)$ using differentiation, we will have the following issues:
- Differentiator amplifies noise.
Fortunately, Kalman Filters doesn't use differentiator but the system **must be observable**

>  If some states are unobservable but stable, an observer will still converge to the true state, although $x(0)$ may not be uniquely determined.

If $z(t)$ is not a function of $x(t)$ then it is not observable.

## Controllability
We say, the system is controllable if we can move from any initial state to any desired state via suitable selection of the input control $u(t)$
$$\mathcal{C}=\begin{bmatrix}B&AB&A^{n-1}B\end{bmatrix}$$
If $\mathcal{C}$ is nonsingular, then the system is controllable

## Diagonal systems, controllability and observability
