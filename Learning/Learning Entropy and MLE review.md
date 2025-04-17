---
type:
  - learning
aliases: 
tags:
  - machine_learning
  - math
progress: Completed
---

# 📘 Information Theory Notes: Entropy, KL Divergence, Cross Entropy & MLE

## 🧠 1. Entropy

Entropy measures the **uncertainty** in a probability distribution:

$$
H(X) = - \sum_x p(x) \log p(x)
$$

- If $p(x) = 1$, the outcome is certain → **entropy = 0**
- If $p(x) = 0.5$, uncertainty is maximal → **entropy is maximized**

It can also be written as an expectation:

$$
H(X) = \mathbb{E}_{x \sim p(x)}[-\log p(x)]
$$

> ✅ **Interpretation**: Entropy quantifies the **average amount of surprise** or information per event sampled from the distribution.

---

## 🔁 2. KL Divergence

KL divergence measures how one probability distribution differs from another:

$$
D_{\mathrm{KL}}(P \parallel Q) = \sum_x P(x) \log \frac{P(x)}{Q(x)}
$$

Also written as an expectation:

$$
D_{\mathrm{KL}}(P \parallel Q) = \mathbb{E}_{x \sim P} \left[ \log \frac{P(x)}{Q(x)} \right]
$$

- Not symmetric: $D_{\mathrm{KL}}(P \parallel Q) \neq D_{\mathrm{KL}}(Q \parallel P)$
- $D_{\mathrm{KL}} = 0$ if and only if $P(x) = Q(x)$ for all x

> ✅ **Interpretation**: Measures the **information loss** when Q is used to approximate P.

---

## 🔀 3. Cross Entropy

Cross-entropy measures the expected number of bits needed to encode samples from P using the distribution Q:

$$
H(p, q) = \mathbb{E}_{x \sim p(x)} \left[ - \log q(x) \right]
$$

Relation to KL divergence:

$$
D_{\mathrm{KL}}(P \parallel Q) = H(P, Q) - H(P)
$$

> ✅ **Interpretation**: Cross entropy = Irreducible entropy (H(P)) + Extra cost from using the wrong model (KL).

---

## 📈 4. Maximum Likelihood Estimation (MLE)

MLE is a method to estimate model parameters by **maximizing the likelihood** of the observed data.

### Standard MLE objective:

$$
\hat{\theta}_{\mathrm{MLE}} = \arg\max_\theta \sum_{i=1}^n \log p_\theta(x_i)
$$

Using the Law of Large Numbers, it becomes:

$$
\hat{\theta}_{\mathrm{MLE}} = \arg\max_\theta \, \mathbb{E}_{x \sim p_{\text{data}}} \left[ \log p_\theta(x) \right]
$$

Or equivalently:

$$
\arg\min_\theta \, \mathbb{E}_{x \sim p(x)} \left[ - \log p_\theta(x) \right]
$$

> ✅ **Interpretation**: MLE is equivalent to **minimizing cross-entropy** between the model and the data distribution.

---

## 📌 Summary Table

| Concept         | Formula                                                    | Meaning                             |
|----------------|-------------------------------------------------------------|-------------------------------------|
| Entropy        | $H(p) = - \sum p(x)\log p(x)$                              | Measures uncertainty                |
| Cross Entropy  | $H(p, q) = - \sum p(x) \log q(x)$                          | Measures model error                |
| KL Divergence  | $D_{KL}(P \parallel Q) = \sum P(x) \log \frac{P(x)}{Q(x)}$ | Distance between distributions      |
| MLE            | $\hat{\theta} = \arg\max_\theta \sum \log p_\theta(x)$     | Find best-fit model parameters      |

---

> 🧩 **Tip**: Entropy, Cross Entropy, KL Divergence, and MLE are deeply interconnected. Understanding them helps in loss design, model evaluation, and statistical learning.




# 📘 信息论笔记：Entropy, KL Divergence, Cross Entropy & MLE

## 🧠 1. Entropy（熵）

熵表示一个分布中**信息的不确定性**，定义如下：

$$
H(X) = - \sum_x p(x) \log p(x)
$$

- 如果 $p(x) = 1$，表示事件确定发生，不存在不确定性，**熵为 0**
- 如果 $p(x) = 0.5$，表示事件完全不确定，**熵最大**
- 通常用对数底为 2（信息论）或 e（机器学习）

熵也可以写成期望的形式：

$$
H(X) = \mathbb{E}_{x \sim p(x)}[-\log p(x)]
$$

> ✅ **理解**：熵衡量了“在某个分布下，观察一个事件所带来的平均信息量”。

---

## 🔁 2. KL Divergence（相对熵）

KL 散度衡量两个分布之间的差异（不是对称距离）：

$$
D_{\mathrm{KL}}(P \parallel Q) = \sum_x P(x) \log \frac{P(x)}{Q(x)}
$$

也可以表示为期望形式：

$$
D_{\mathrm{KL}}(P \parallel Q) = \mathbb{E}_{x \sim P} \left[ \log \frac{P(x)}{Q(x)} \right]
$$

当 $P = Q$ 时，KL 散度为 0。

> ✅ **理解**：用 Q 去近似真实分布 P 时，**我们平均损失了多少信息**。

---

## 🔀 3. Cross Entropy（交叉熵）

交叉熵衡量在真实分布 $p(x)$ 下，使用模型分布 $q(x)$ 所带来的平均信息量：

$$
H(p, q) = \mathbb{E}_{x \sim p(x)} \left[ -\log q(x) \right]
$$

交叉熵和熵的关系：

$$
D_{\mathrm{KL}}(P \parallel Q) = H(P, Q) - H(P)
$$

> ✅ **理解**：交叉熵 = 模型预测的损失 + 不可避免的熵  
> 当我们最小化交叉熵，就是尽可能让模型预测贴近真实分布

---

## 📈 4. MLE（最大似然估计）

最大似然估计是寻找参数 $\theta$，使观测数据的概率最大：

### 经典形式：
$$
\hat{\theta}_{\mathrm{MLE}} = \arg\max_\theta \sum_{i=1}^n \log p_\theta(x_i)
$$

使用大数定律，可以转换为期望的形式：

$$
\hat{\theta}_{\mathrm{MLE}} = \arg\max_\theta \, \mathbb{E}_{x \sim p_{\text{data}}} \left[ \log p_\theta(x) \right]
$$

等价于最小化负对数似然（NLL）：

$$
\arg\min_\theta \, \mathbb{E}_{x \sim p(x)} \left[ - \log p_\theta(x) \right]
$$

> ✅ **理解**：MLE 就是最小化 **交叉熵**，从而等价于最小化 **KL 散度**

---

## 📌 小结 Summary

| 概念 | 定义 | 含义 |
|------|------|------|
| Entropy | $H(p) = - \sum p(x)\log p(x)$ | 衡量不确定性 |
| Cross Entropy | $H(p, q) = - \sum p(x) \log q(x)$ | 衡量模型预测误差 |
| KL Divergence | $D_{KL}(P \parallel Q) = \sum P(x) \log \frac{P(x)}{Q(x)}$ | 衡量分布间距离 |
| MLE | $\hat{\theta} = \arg\max_\theta \sum \log p_\theta(x)$ | 寻找最符合数据的模型参数 |

---

> 🧩 Tips：熵 / 交叉熵 / KL / MLE 是信息论与机器学习中的核心桥梁，熟练理解它们之间的关系，有助于深入理解损失函数、模型优化、分布拟合等问题。