<!--
 * @Author: vihowe
 * @Date: 2022-01-15 22:24:01
 * @LastEditTime: 2022-01-15 23:38:38
 * @FilePath: /myBlog/content/posts/kungfu/index.md
-->
---
title: "KungFu: Making Training in Distributed Machine Learning Adaptive"
tags: ["DDL"]
categories: ["papers"]
---
# KungFu: Making Training in Distributed Machine Learning Adaptive

> 一篇讲adaptive 分布式训练框架设计与实现的论文。在分布式训练中，影响训练的主要有超参（bs，lr）,
系统参数（worker 数量，通信拓扑）
这篇文章针对TensorFlow开发了一个分布式ML library。用户可以借此设计一些Adaptation Policy来描述
如何在训练过程中改变hyper和system 参数。
感觉更多是系统实现上的思考，如何monitor各种metric，以及如何完成相应的control operation。

## Adaption Policies
- 提供了一层软件抽象给用户，用户可以定制自己的policy。
关键点：framework-independent
举了一个例子：根据GNS（gradient noise sclae）来动态改变bs

## 最重要的两点：
- 如何进行低开销的metric monitoring
- 如何根据metric和policy在分布式环境下做出work stage的management