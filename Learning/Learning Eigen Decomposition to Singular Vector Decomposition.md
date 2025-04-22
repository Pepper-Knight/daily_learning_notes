---
type:
  - learning
aliases: 
tags:
  - math
progress: Completed
---

# 📘 Understanding Eigenvalues and Eigenvectors

## 🧠 What Are Eigenvalues and Eigenvectors?

In school, we're often taught that a square matrix can be "decomposed" into eigenvalues and eigenvectors. But we're rarely told what they **mean** or **why** this matters.

So what are they, really?

At a high level:

- **Eigenvectors** are directions that remain unchanged under a matrix transformation (only scaled).
- **Eigenvalues** are the factors by which those directions are stretched or compressed.

$$
[
A \vec{v} = \lambda \vec{v}
]
$$

Here:
- $( \vec{v} )$: eigenvector  
- $( \lambda )$: eigenvalue  
- $( A )$: matrix

---

## 📐 A Geometric Intuition

Imagine a matrix as a machine that stretches, rotates, or reflects vectors. Most vectors will change direction. But a few “special” directions will **only scale**, not rotate — these are eigenvectors. The **amount of scaling** is the eigenvalue.

### 🐔🦶 Chicken and Rabbit Example: A Concrete View of Eigenvalues

Let’s say we’re modeling a simple "chickens and rabbits" system. Chickens have:
- 1 head and 2 feet  
Rabbits have:
- 1 head and 4 feet  

We can encode this as a transformation matrix:

$$
[
A = \begin{bmatrix}
1 & 1 \\
2 & 4
\end{bmatrix}
]
$$

Now, suppose we apply this matrix to the **standard basis vectors**:

$$
[
\vec{e}_1 = \begin{bmatrix}1\\
0\end{bmatrix}, \quad
\vec{e}_2 = \begin{bmatrix}0\\
1\end{bmatrix}
]
$$

Then:

$$
[
A \vec{e}_1 = \begin{bmatrix}1\\
2\end{bmatrix}, \quad
A \vec{e}_2 = \begin{bmatrix}1\\
4\end{bmatrix}
]
$$

These outputs represent how the "chicken" and "rabbit" variables get mapped to the "head/feet" space. If we now try to find **directions that only get scaled (not rotated)** under this transformation — those are the **eigenvectors**. The amount of stretch along them is the **eigenvalue**.

So in this toy system:
- The directions $(\vec{v}) such that (A \vec{v} = \lambda \vec{v})$ describe the "pure identity" of animal types
- The stretch factors $(\lambda)$ describe how much those identities are magnified in feature space (heads/feet)

This is a simple but powerful way to view **eigenvalues as scaling**, and **eigenvectors as intrinsic directions** in a transformation.


---

## 📊 Why Does This Matter?

These ideas are fundamental in many areas:

- **Principal Component Analysis (PCA)**:  
  Find directions (eigenvectors) with the **largest eigenvalues**, i.e., the directions where data varies most. These are the **most important components**.

- **Physical systems**:  
  Eigenvectors/eigenvalues describe resonant modes, stress directions, etc.

---

## ⚠️ Limitations of Eigen Decomposition

Eigen decomposition requires:

- The matrix must be **square**
- Ideally, the matrix is **symmetric** for real-valued, orthogonal eigenvectors

This is where **SVD (Singular Value Decomposition)** comes in.

---

## 🔄 From Eigen to SVD

SVD generalizes eigen decomposition. It works for **any matrix**, even non-square or non-symmetric ones.

$$
[
A = U \Sigma V^T
]
$$

- \( U \): left singular vectors (eigenvectors of \( AA^T \))
- \( V \): right singular vectors (eigenvectors of \( A^T A \))
- $( \Sigma )$: diagonal matrix of singular values $( \sigma_i = \sqrt{\lambda_i} )$

### 🧠 Understanding the Roles of $A^T A$ and $A A^T$

Let’s look at the matrix shapes:

- $A^T A \in \mathbb{R}^{n \times n}$:  
  This matrix keeps the **column space** of $A$, so it captures how **input directions** (features, variables) interact. In other words, it encodes the **feature structure** or **input space geometry**.

- $A A^T \in \mathbb{R}^{m \times m}$:  
  This matrix keeps the **row space** of $A$, which corresponds to how each data **sample (row)** projects onto others — the **output space structure**.

### 🧭 Interpretation:

- The eigenvectors of $A^T A$ form the matrix $V$, telling us **which directions in the input space are preserved** under transformation.
- The eigenvectors of $A A^T$ form the matrix $U$, telling us **which directions in the output space the inputs are stretched into**.
- The singular values $\sigma_i$ in $\Sigma$ are just the **square roots** of the eigenvalues of both $A^T A$ and $A A^T$ — they represent the **strength of stretching** between these two spaces.

So we can say:

> $A^T A$ describes the internal structure of the **input (feature) space**,  
> $A A^T$ describes the internal structure of the **output (observation) space**,  
> and $\Sigma$ links them via **scaling magnitudes**.

### 🧭 Intuition:

SVD is like saying:  
> “I can’t decompose A directly, but I can decompose how it acts on **input space** and **output space**, then connect them with scaling (Σ).”

---

## 🌟 Low-Rank Approximation and PCA

The core idea behind PCA is **low-rank approximation**.

Given the SVD of a data matrix:

$$
[
X = U \Sigma V^T
]
$$

Each column of $V$ represents a **principal direction** in the original feature space, and the singular values in $\Sigma$ represent how much variance (or “pulling”) that direction contributes.

To compress or simplify the data, we can **keep only the top $k$ singular values and vectors**:

$$
[
X_k = U_k \Sigma_k V_k^T
]
$$


This approximates the original data while preserving most of its structure.

> Each direction (eigenvector or singular vector) can be thought of as a “pulling direction” from a variable, and its associated singular value represents how strong that variable influences the data shape.

Thus:
- Keeping only top components reveals **which variables contribute most to data variation**
- This is used in **PCA**, **noise reduction**, and **feature importance analysis**

## ✅ Summary

| Concept        | Meaning                            |
|----------------|-------------------------------------|
| Eigenvector    | Direction preserved under transform |
| Eigenvalue     | Stretch/shrink factor               |
| Singular Value | √(eigenvalue of \( A^T A \))        |

---

# 📘 理解特征值和特征向量（中文版）

## 🧠 什么是特征值和特征向量？

在学校里老师常说：“一个方阵可以被分解为特征值和特征向量”，但我们常常不理解它们到底代表什么。

本质上：

- **特征向量** 是在矩阵作用下方向不变的向量
- **特征值** 是这个方向上的缩放因子

$$
[
A \vec{v} = \lambda \vec{v}
]
$$

其中：
- $( \vec{v} )$：特征向量  
- $( \lambda )$：特征值  
- \( A \)：矩阵

---

## 📐 几何直觉

把一个矩阵想象成“变形机器”——它对向量进行拉伸、旋转或翻转。大多数向量都会改变方向，但**某些方向只会被放大或缩小**，方向保持不变，这些就是特征向量。

### 🐔🦶 鸡兔同笼问题：如何理解特征值和特征向量

假设我们在描述一个“鸡兔同笼”的模型：

- 鸡有：1 只头、2 只脚  
- 兔有：1 只头、4 只脚

我们可以用一个 2×2 的矩阵来表示这种映射关系：

$$
[
A = \begin{bmatrix}
1 & 1 \\
2 & 4
\end{bmatrix}
]
$$

现在我们观察这个矩阵对标准向量的作用：

$$
[
\vec{e}_1 = \begin{bmatrix}1\\
0\end{bmatrix} \quad （代表一只鸡），\quad
\vec{e}_2 = \begin{bmatrix}0\\
1\end{bmatrix} \quad （代表一只兔子）
]
$$

矩阵作用结果为：

$$
[
A \vec{e}_1 = \begin{bmatrix}1\\2\end{bmatrix}，\quad
A \vec{e}_2 = \begin{bmatrix}1\\4\end{bmatrix}
]
$$

也就是说：  
- 鸡和兔子在被矩阵作用后变成了“头”和“脚”的坐标系中的向量  
- 而如果我们再找出某个方向（特征向量）被这个矩阵作用后**仍然保持方向，只是长度变化了**，这就是这个系统的**特征方向**  
- 被拉伸或压缩的倍数，就是**特征值**

换句话说，**特征向量告诉你鸡兔这个系统最核心的“结构方向”**，而**特征值告诉你这个结构在观察空间（头/脚空间）中被放大的程度**。

这是一个非常直观的方式去理解线性变换中的特征结构。


---

## 📊 为什么特征值/向量很重要？

它们在很多地方都有应用：

- **主成分分析（PCA）**：  
  寻找数据变化最大的方向（最大特征值对应的特征向量）

- **物理系统**：  
  描述共振、应力方向、系统稳定性等

---

## ⚠️ 特征分解的局限性

特征分解要求：

- 矩阵必须是 **方阵**
- 最好是 **对称矩阵**（以保证实特征值与正交特征向量）

这就引出了 **奇异值分解 SVD**

---

## 🔄 从特征分解到 SVD

SVD 是更通用的分解方法。它适用于 **任意形状的矩阵**：
$$
[
A = U \Sigma V^T
]
$$
- \( U \)：左奇异向量（来自 \( AA^T \) 的特征分解）
- \( V \)：右奇异向量（来自 \( A^T A \) 的特征分解）
- $( \Sigma )$：奇异值矩阵，元素为 $( \sigma_i = \sqrt{\lambda_i} )$

### 🧠 如何理解 $A^T A$ 和 $A A^T$ 的角色？

我们可以从矩阵形状来直观理解：

- $A^T A \in \mathbb{R}^{n \times n}$：  
  保留了原矩阵的 **列数**，也就是输入的维度。这代表了 **输入空间** 的特征结构 —— 各个变量之间是如何协同作用的。

- $A A^T \in \mathbb{R}^{m \times m}$：  
  保留了原矩阵的 **行数**，对应的是每条数据的结构（输出空间）。这个矩阵描述的是数据点在空间中如何相互投影。

### 🧭 几何解释：

- $A^T A$ 的特征向量（构成 $V$）告诉我们输入空间中的哪几个方向是稳定的“变换方向”
- $A A^T$ 的特征向量（构成 $U$）则说明这些输入是被映射到了输出空间的哪些方向上
- $\Sigma$ 中的奇异值就是两边空间之间变换的“缩放倍数”，本质上是 $A^T A$ 或 $A A^T$ 的特征值的开方：

$$
[
\sigma_i = \sqrt{\lambda_i}
]
$$

所以我们可以这么理解：

> $A^T A$ 描述了**输入空间（列空间）**的结构，  
> $A A^T$ 描述了**输出空间（行空间）**的结构，  
> $\Sigma$ 则是连接这两个空间的“拉伸尺度”。

### 🧭 直觉理解：

SVD 的思路是：
> “我没办法直接对 A 做特征分解，但我可以分别分析它对输入空间和输出空间的影响，然后通过奇异值串联两者。”

---

## 🌟 低秩近似与 PCA 的核心思想

PCA（主成分分析）的核心思想其实就是 **低秩近似（Low-Rank Approximation）**。

当我们对一个数据矩阵 $X$ 做 SVD 分解：

$$
[
X = U \Sigma V^T
]
$$

其中：
- $V$ 中的每一列代表原始特征空间中的一个“主方向”
- $\Sigma$ 中的奇异值表示数据在这个方向上的变化程度

我们可以只保留前 $k$ 个最大的奇异值及其对应的向量：

$$
[
X_k = U_k \Sigma_k V_k^T
]
$$

这样就可以用低秩的方式近似原始数据，同时保留最主要的信息。

> 可以将每个特征向量方向理解为“每个变量对数据施加的拉伸方向”，  
> 对应的奇异值越大，说明这个变量在数据中起的作用越强。

因此：
- 只保留较大的奇异值等价于保留主要变量影响
- 这也就是 PCA 能用于 **数据压缩**、**噪声去除**、**变量筛选** 的数学依据


## ✅ 总结

| 概念           | 含义                               |
|----------------|------------------------------------|
| 特征向量       | 方向不变的向量                     |
| 特征值         | 缩放倍数                           |
| 奇异值         | \( A^T A \) 的特征值开根号         |




