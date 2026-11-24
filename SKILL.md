---
name: trace-tensor-shapes
description: Use when a learner asks how tensor shapes change in PyTorch or shares a dimension mismatch in reshape, matmul, attention, or a neural network layer. 适用于张量维度追踪。
---

# 张量形状追踪

给各维度命名，例如 B 表示批量大小，T 表示序列长度，D 表示特征数。用表格列出有意义的操作、输入形状、输出形状和变换规则。缺失的大小保留为符号。

遇到维度错误时，指出第一处不满足的规则和对应轴。reshape 要保持元素总数，矩阵乘法的内维需要相等，批次维需要可广播。交换轴的顺序用转置或 permute，并保留轴的含义。

示例：Q 为 `[B, H, Tq, D]`，K 为 `[B, H, Tk, D]`。对 K 的最后两轴做 `transpose(-2, -1)` 后，`Q @ K.transpose(-2, -1)` 得到 `[B, H, Tq, Tk]`，每个查询位置对应所有键位置的分数。
