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
\vec{e}_1 = \begin{bmatrix}1\\0\end{bmatrix}, \quad
\vec{e}_2 = \begin{bmatrix}0\\1\end{bmatrix}
]
$$
Then:
$$
[
A \vec{e}_1 = \begin{bmatrix}1\\2\end{bmatrix}, \quad
A \vec{e}_2 = \begin{bmatrix}1\\4\end{bmatrix}
]
$$
These outputs represent how the "chicken" and "rabbit" variables get mapped to the "head/feet" space. If we now try to find **directions that only get scaled (not rotated)** under this transformation — those are the **eigenvectors**. The amount of stretch along them is the **eigenvalue**.

So in this toy system:
- The directions \(\vec{v}\) such that \(A \vec{v} = \lambda \vec{v}\) describe the "pure identity" of animal types
- The stretch factors \(\lambda\) describe how much those identities are magnified in feature space (heads/feet)

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

### 🧭 Intuition:

SVD is like saying:  
> “I can’t decompose A directly, but I can decompose how it acts on **input space** and **output space**, then connect them with scaling (Σ).”

---

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
\vec{e}_1 = \begin{bmatrix}1\\0\end{bmatrix} \quad （代表一只鸡），\quad
\vec{e}_2 = \begin{bmatrix}0\\1\end{bmatrix} \quad （代表一只兔子）
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

### 🧭 直觉理解：

SVD 的思路是：
> “我没办法直接对 A 做特征分解，但我可以分别分析它对输入空间和输出空间的影响，然后通过奇异值串联两者。”

---

## ✅ 总结

| 概念           | 含义                               |
|----------------|------------------------------------|
| 特征向量       | 方向不变的向量                     |
| 特征值         | 缩放倍数                           |
| 奇异值         | \( A^T A \) 的特征值开根号         |




