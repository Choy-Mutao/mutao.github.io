---
title: Standard PSO Version 2007
type: docs
description: 这与原始版本（1995）非常接近，基于最近的一些工作，只做了一些改进。
---

## 与 SPSO2006 之间的主要区别

1. 增加控制项: "使算法对搜索空间的旋转变换不敏感"
   > Note: 减低性能可能不会对结果有太大改善.(做了更多的尝试)
2. 增加控制项 "是否每次迭代随机前置换粒子的位置"
   > Note: 减低性能可能不会对结果有太大改善(做了更多的尝试)
3. 增加控制项 "是否约束粒子边界"
   > Note: 在极少数情况下，如果停止标准是最大评估次数，则不限制位置可能会导致无
   > 限运行
4. 一个特定粒子是另一个粒子的通知者的概率 p。在 SPSO-06 中，它是隐式的（通过构建
   随机信息网络）。在这里，默认值直接作为（S，K）的函数计算，因此信息网络与
   SPSO-07 中的完全相同。然而，现在它可以被“操纵”（即可以分配任何值）
5. 搜索空间可以量化,但该算法不适用于组合问题

> 额外的, 在随机数的计算上提供了一些其他的方法

## SPSO2007 的初始化

从逻辑上来讲, 在随机生成*初始位置*和*初始速度*后, 增加了一步 *量化(Quantisation)*, 用于将连续问题的解空间进行离散化, 通常可以用于一下问题的处理

* 离散优化问题: 当优化问题的解空间是离散的, 而粒子群算法通常处理的是连续空间. 在这种情况下, 通过量化技术可以将连续粒子的位置转换为离散的可行解, 以适应离散优化问题

* 编码和解码: 在某些应用中, PSO 算法的粒子可能需要通过编码和解码机制与离散决策变量进行交互. 例如，优化过程中使用浮点数表示解决方案，但最终解需要在离散的参数空间中被实现。量化就是将这些浮点数转换为离散的值。

* 精度控制：量化也可以用于控制粒子位置的精度，以避免计算中的浮点数误差或过度复杂的计算。通过将粒子的位置量化为有限精度的值，可以简化计算，并提高算法的稳定性。

* 速度调整：在某些变体中，量化用于调整粒子的速度或位置，使得搜索过程在离散的步长或区间内进行，从而控制算法的步伐和收敛速度。

## 1. SPSO2007 介绍

在项目结构上, 在不着重考虑性能的情况下, 对算法的逻辑进行了更详细的*结构化*, 将算
法中涉及到的数据进行了封装, 分为: