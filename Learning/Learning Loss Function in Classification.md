---
type:
  - learning
aliases: 
tags:
  - machine_learning
progress:
---

# 💡 The Truth Even ChatGPT Might Miss: Why MSE is Worse Than You Think for Classification

While reading *Deep Learning Tutorial by Lee et al.*, I re-examined a common belief:  
**"Cross-Entropy is better than MSE for classification because MSE doesn't fit probabilities well."**

But what happens when the logits are extreme?

## 🧪 My Experiment

- A 3-class classification task
- Fix one class’s logit at **-1000** (simulate bad initialization)
- Grid search the other two logits in [-10, 10]
- For each pair, compute **MSE Loss** and **Cross-Entropy Loss**
- Plot loss surface as a 2D heatmap (100x100 evaluations)

## 🔍 What I Found

Contrary to common belief:

- **MSE loss surface** shows sharp cliffs and discontinuities  
- Gradient becomes **chaotic, discontinuous, hard to optimize**
![[Screenshot 2025-04-17 at 12.05.07 AM 1.png]]
Meanwhile:

- **Cross-Entropy loss surface is smoother**
- Only considers softmax output of the target class
- Provides **clear and continuous gradients**, even with bad logits

## 🧠 Key Insight

> MSE compares raw numbers; Cross-Entropy compares probability distributions.

When logits are extreme, **MSE leads to gradient explosion or vanishing**, hurting optimization.  
Cross-Entropy still provides direction — which is critical in early training.

## 📌 Summary Table

| Comparison       | Cross-Entropy Loss       | MSE Loss                  |
|------------------|--------------------------|---------------------------|
| Extreme logits   | Smooth and differentiable | Sharp cliffs, unstable    |
| Gradient direction | Clear and consistent     | May vanish or explode     |
| Training stability | High                     | Low                       |

> If you've assumed “MSE is more forgiving,” maybe it’s time to rethink that.



# 💡 ChatGPT 都不知道的真相：MSE 在分类任务中为何比你想的还糟

在阅读《Deep Learning Tutorial by Lee et al.》时，我重新思考了一个老问题：  
**“为什么分类任务要用交叉熵，而不是 MSE？”**

如果 logit 非常极端，会发生什么？

## 🧪 我的实验设计

- 三分类问题
- 固定一个 logit = -1000（模拟模型初始化极差）
- 另外两个 logits 在 [-10, 10] 网格搜索
- 对每组 logits，分别计算 **MSE 和 Cross-Entropy**
- 绘制二维热力图（共 100x100 次计算）

## 🔍 结果出人意料

- **MSE 的 loss surface 出现大量断崖与不连续区域**
- 梯度方向混乱，无法优化
![[Screenshot 2025-04-17 at 12.05.07 AM.png]]

相比之下：

- **Cross-Entropy 曲面更平滑**
- 只关注目标类别的预测概率
- 即使 logits 极差，也能提供明确的优化方向

## 🧠 我的理解

> MSE 比较的是数值误差，Cross-Entropy 比较的是概率分布。

在 logits 极端的情况下，**MSE 容易导致梯度爆炸或消失**，直接拖垮训练；而 Cross-Entropy 即使在坏初始化下也能稳住梯度。

## 📌 总结对比表

| 比较维度       | Cross-Entropy Loss     | MSE Loss                      |
|----------------|------------------------|-------------------------------|
| 极端 logits    | 更平滑，可微           | 更尖锐，优化困难               |
| 梯度方向       | 明确，方向一致          | 混乱，可能爆炸或消失           |
| 训练稳定性     | 高                     | 低                            |

> 如果你也以为 “MSE 更温和” 是安全选择，也许是时候重新考虑这个问题了。
