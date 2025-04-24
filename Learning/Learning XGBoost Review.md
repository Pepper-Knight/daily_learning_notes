---
type:
  - learning
aliases: 
tags:
  - machine_learning
progress:
---
# XGBoost: Residual Learning with Gradient & Hessian

## 🧠 Core Concept

XGBoost is a residual learning model, just like most gradient boosting models. The core idea is to iteratively learn the **residual** from the previous prediction, pushing the model output closer to the true label.

At each step:


$$

\hat{y}_{\text{new}} = \hat{y}_{\text{old}} + f_t(x)

$$

$$
\text{Residual: } r_i^{(t)} = y_i - \hat{y}_i^{(t-1)} \approx -\frac{\partial \mathcal{L}(y_i, \hat{y}_i)}{\partial \hat{y}_i}

$$

This residual learning process is equivalent to performing **gradient descent** in function space, since reducing the residual also reduces the loss function.

---

## 🔍 Compared to Traditional Tree Models

Traditional tree models (like CART):

- Use **heuristics** (e.g., Gini impurity, MSE) to evaluate splits
- Focus on **local purity** or error reduction

XGBoost:

- Evaluates splits based on **the actual loss function**
- Uses both **gradient and hessian** to estimate gain:

$$
\text{Gain} = \frac{1}{2} \left[ \frac{G_L^2}{H_L + \lambda} + \frac{G_R^2}{H_R + \lambda} - \frac{(G_L + G_R)^2}{H_L + H_R + \lambda} \right] - \gamma
$$

This ensures each split contributes to minimizing the **global loss**, not just local variance.

---

## 🌳 Leaf Node Output (Parameter Estimation)

Every **leaf node** in XGBoost represents a region in the feature space and outputs a constant value \( w_j \). All samples that fall into the same leaf receive the same prediction.

This value is computed as the optimal output that minimizes the local approximation of the loss function:

$$
w_j^* = -\frac{G_j}{H_j + \lambda}, \quad 
G_j = \sum_{i \in I_j} g_i, \quad 
H_j = \sum_{i \in I_j} h_i
$$

> So each leaf acts as a parameterized piecewise constant function, enabling the model to capture **nonlinear patterns**.

---

## ✅ Summary

- XGBoost is still a tree-based model, but with a global optimization perspective.
- Instead of splitting based on local heuristics, it uses **gradient + hessian** to evaluate global loss improvement.
- Each leaf node holds a parameter (output value), derived analytically using gradients.
- The additive structure and piecewise prediction enable XGBoost to model highly **nonlinear relationships**.

---

# XGBoost：带梯度与二阶导的残差学习

## 🧠 核心概念

XGBoost 是一种残差学习模型，和大多数 Gradient Boosting 模型一样。它的核心思想是不断拟合前一轮的 **残差**，使模型的预测值逐步逼近真实值。

每一步迭代可以表示为：

$$
\hat{y}_{\text{new}} = \hat{y}_{\text{old}} + f_t(x)
$$

$$
\text{残差：} r_i^{(t)} = y_i - \hat{y}_i^{(t-1)} \approx -\frac{\partial \mathcal{L}(y_i, \hat{y}_i)}{\partial \hat{y}_i}
$$

这个残差学习过程等价于在函数空间中做 **梯度下降**，因为减少残差的方向正是 loss 函数下降的方向。

---

## 🔍 与传统树模型对比

传统树模型（如 CART）：

- 使用启发式指标（如 Gini、MSE）来选择切分点
- 关注的是节点的“纯度”或误差下降的局部优化

XGBoost：

- 明确使用损失函数的 **梯度与二阶导（Hessian）**
- 每个分裂点的评价依据是：

$$
\text{Gain} = \frac{1}{2} \left[ \frac{G_L^2}{H_L + \lambda} + \frac{G_R^2}{H_R + \lambda} - \frac{(G_L + G_R)^2}{H_L + H_R + \lambda} \right] - \gamma
$$

这种做法确保了每一次分裂都在为 **全局的 loss 降低** 做出贡献，而不是只看局部变化。

---

## 🌳 叶子节点输出（参数估计）

XGBoost 中的每个叶子节点表示特征空间中的一个区域，对所有落入该区域的样本输出同一个预测值 \( w_j \)。

这个值不是平均值，而是通过如下解析公式计算得到的最优输出：

$$
w_j^* = -\frac{G_j}{H_j + \lambda}, \quad 
G_j = \sum_{i \in I_j} g_i, \quad 
H_j = \sum_{i \in I_j} h_i
$$

> 每个叶子节点就像一个参数化的 piecewise 常数函数，这种结构天然适合拟合复杂的 **非线性关系**。

---

## ✅ 总结

- XGBoost 是树结构，但引入了全局损失函数的优化视角
- 分裂不再依赖启发式指标，而是使用 **梯度与二阶导数** 评估目标函数下降
- 每个叶子节点输出的值是通过解析公式得到的最优权重
- 多棵树的累加形成一个强大的非线性拟合器，能够建模复杂的关系




