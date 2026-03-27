
假设我们面临 $m$ 个 Inequality Constraint （记为 $g_i(x) \geq 0$ ）以及 $p$ 个 Equality Constraint （记为 $h_k(x) = 0$ ）。

我们需要为每一个限制条件分配一个Multiplier。此时， Lagrange Function 扩展为如下的线性组合形式：

$$L(x, \lambda, \mu) = f(x) + \sum_{i=1}^m \lambda_i g_i(x) + \sum_{k=1}^p \mu_k h_k(x)$$

其中，向量 $\lambda = (\lambda_1, \lambda_2, \dots, \lambda_m)$ 对应所有的不等式约束，向量 $\mu = (\mu_1, \mu_2, \dots, \mu_p)$ 对应所有的等式约束。

### 2. KKT 条件的高维扩展

在多条件系统下，最优点 $x^*$ 必须同时满足以下推广后的 KKT Conditions ：

**一阶平稳性 (First-Order Condition)**：

$$\nabla f(x^*) + \sum_{i=1}^m \lambda_i^* \nabla g_i(x^*) + \sum_{k=1}^p \mu_k^* \nabla h_k(x^*) = 0$$

这表明目标函数的梯度，必须被所有约束函数梯度的线性组合所抵消。

**乘子非负性 (Dual Feasibility)**：

$$\lambda_i^* \geq 0 \quad \forall i = 1, 2, \dots, m$$

每一个不等式约束的乘子都必须大于或等于零，而等式约束的乘子 $\mu_k$ 则没有符号限制（可以是负数）。

**互补松弛性 (Complementary Slackness)**：

$$\lambda_i^* \cdot g_i(x^*) = 0 \quad \forall i = 1, 2, \dots, m$$

这是多条件问题中最复杂的一环。该等式要求：对于系统中的**每一个**不等式约束，其乘子 $\lambda_i$ 与其约束值 $g_i(x)$ 之间，必定至少有一个严格为零。


----
Homework

## Problem Formulation

The objective is to find the global maximum of a nonlinear function subject to an inequality constraint. The optimization problem is defined as follows.

Maximize:
$$f(x,y) = x^2 + y^2 + y - 1$$

Subject to the feasible region $S$ defined by:
$$g(x,y) = x^2 + y^2 \leq 1$$

---

## Methodology

To solve this constrained optimization problem rigorously, we apply the Karush Kuhn Tucker (KKT) conditions. The KKT conditions provide the necessary first order mathematical conditions for a solution in nonlinear programming to be optimal. Given that the objective function and the constraint function are continuously differentiable, this method guarantees finding the critical points that could serve as potential global maxima.

We define the Lagrangian function $\mathcal{L}(x, y, \lambda)$ by introducing a nonnegative Lagrange multiplier $\lambda$ for the inequality constraint.

$$\mathcal{L}(x, y, \lambda) = f(x,y) - \lambda (g(x,y) - 1)$$
$$\mathcal{L}(x, y, \lambda) = x^2 + y^2 + y - 1 - \lambda (x^2 + y^2 - 1)$$

The KKT conditions dictate that any optimal point $(x^*, y^*)$ must satisfy the following criteria.

* **Stationarity:** The gradient of the Lagrangian with respect to the decision variables must equal zero.
* **Primal Feasibility:** The proposed point must satisfy the original mathematical constraint.
* **Dual Feasibility:** The Lagrange multiplier associated with the inequality constraint must be greater than or equal to zero.
* **Complementary Slackness:** The product of the multiplier and the constraint function evaluated at the optimal point must equal zero.

---

## Detailed Step by Step Solution

### 1. Applying the KKT Conditions

We compute the partial derivatives of the Lagrangian and construct the system of equations.

**Stationarity Equations:**
1) $\frac{\partial \mathcal{L}}{\partial x} = 2x - 2\lambda x = 2x(1 - \lambda) = 0$
2) $\frac{\partial \mathcal{L}}{\partial y} = 2y + 1 - 2\lambda y = 2y(1 - \lambda) + 1 = 0$

**Feasibility and Slackness Conditions:**
3) $x^2 + y^2 \leq 1$
4) $\lambda \geq 0$
5) $\lambda (x^2 + y^2 - 1) = 0$

To locate all potential solutions, we analyze the complementary slackness condition under two distinct scenarios.

### 2. Scenario A: Inactive Constraint

Assume $\lambda = 0$. This implies the constraint is inactive, meaning the optimal point lies strictly inside the boundary of the feasible region.

Substituting $\lambda = 0$ into the stationarity equations yields the following results.
From equation 1: $2x(1 - 0) = 0 \implies x = 0$
From equation 2: $2y(1 - 0) + 1 = 0 \implies 2y + 1 = 0 \implies y = -0.5$

Next, we verify if this point satisfies primal feasibility by checking equation 3.
$$0^2 + (-0.5)^2 = 0.25$$
Since 0.25 is less than 1, the point $(0, -0.5)$ is strictly within the feasible region. We calculate the objective function value at this coordinate.
$$f(0, -0.5) = 0^2 + (-0.5)^2 - 0.5 - 1 = 0.25 - 0.5 - 1 = -1.25$$

### 3. Scenario B: Active Constraint

Assume $\lambda > 0$. According to the complementary slackness condition found in equation 5, the constraint must be binding. Therefore, $x^2 + y^2 - 1 = 0$, which simplifies to $x^2 + y^2 = 1$.

We return to equation 1: $2x(1 - \lambda) = 0$. This equation is satisfied if either $x = 0$ or $\lambda = 1$. We must evaluate both mathematical possibilities.

**Possibility 1: Assume $\lambda = 1$**
Substitute $\lambda = 1$ into equation 2.
$$2y(1 - 1) + 1 = 0$$
$$0 + 1 = 0$$
This creates a mathematical contradiction. Consequently, $\lambda$ cannot equal 1, and this path yields no valid solutions.

**Possibility 2: Assume $x = 0$**
Since we established that the constraint is active with $x^2 + y^2 = 1$, substituting $x = 0$ gives the following.
$$0^2 + y^2 = 1 \implies y = \pm 1$$

We now have two candidate points on the boundary to evaluate. We must also verify that $\lambda > 0$ for each coordinate to satisfy dual feasibility.

**Candidate Point $(0, 1)$:**
Substitute $y = 1$ into equation 2 to solve for the multiplier $\lambda$.
$$2(1)(1 - \lambda) + 1 = 0$$
$$2 - 2\lambda + 1 = 0$$
$$3 = 2\lambda \implies \lambda = 1.5$$
Because $\lambda = 1.5$, which is strictly greater than 0, dual feasibility is satisfied. This represents a valid KKT point.
Calculate the objective value.
$$f(0, 1) = 0^2 + 1^2 + 1 - 1 = 1$$

**Candidate Point $(0, -1)$:**
Substitute $y = -1$ into equation 2 to solve for the multiplier $\lambda$.
$$2(-1)(1 - \lambda) + 1 = 0$$
$$-2 + 2\lambda + 1 = 0$$
$$-1 + 2\lambda = 0 \implies \lambda = 0.5$$
Because $\lambda = 0.5$, which is strictly greater than 0, dual feasibility is satisfied. This also represents a valid KKT point.
Calculate the objective value.
$$f(0, -1) = 0^2 + (-1)^2 - 1 - 1 = -1$$

---

## Conclusion

By comparing the objective function values evaluated at all valid KKT points, we can determine the global maximum over the defined feasible set $S$.

* At the interior point $(0, -0.5)$, the function evaluates to -1.25.
* At the boundary point $(0, -1)$, the function evaluates to -1.
* At the boundary point $(0, 1)$, the function evaluates to 1.

The highest numerical value obtained is 1. Therefore, the maximum value of the function $f(x,y)$ subject to the constraint $g(x,y) \leq 1$ is 1, and this maximum is achieved at the coordinates $(x,y) = (0, 1)$.

Would you like me to demonstrate the alternative variable substitution method to verify this result from a purely algebraic perspective?