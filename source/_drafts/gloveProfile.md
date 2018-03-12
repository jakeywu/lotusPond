---
title: gloveProfile
tags: undefined
categories: preview
date: 2017-11-16 10:40:51
---

A (Accuracy)  准确率
P (Precision)  精确率
R (Recall)  召回率
F1 (F1 Measure) F1值   精确率 * 召回率 * 2 / (精确率 + 召回率)



假设我们手上有60个正样本，40个负样本，我们要找出所有的正样本，系统查找出50个，其中只有40个是真正的正样本，计算上述各指标。

TP: 将正类预测为正类数  40
FN: 将正类预测为负类数  20
FP: 将负类预测为正类数  10
TN: 将负类预测为负类数  30

准确率(accuracy) = 预测对的/所有 = (TP+TN)/(TP+FN+FP+TN) = 70%
精确率(precision) = TP/(TP+FP) = 80%
召回率(recall) = TP/(TP+FN) = 2/3
F1值  80% * 2/3 *2 / (80% + 2/3)