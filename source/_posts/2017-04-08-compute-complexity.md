---
title: 计算复杂性
date: 2017-04-08 10:24:18
tags:
---

# 第一章：

# 第二章：

# 第三章：

# 第四章：NP 问题与计算可行性

归约的定义（抽象）：

对于全集 $\mathrm N$ 给定两个子集$\mathrm A$和$\mathrm B$，以及一个由 $\mathrm N$ 映射到 $\mathrm N$ 的并满足复合封闭性的函数集合 $F$，如果满足
\[
\exists f \in F. \forall x in \mathrm N.~x\in \mathrm A \Longleftrightarrow f(x) \in \mathrm B
\]
记作 $\mathrm A \le_F \mathrm B$

归约等价性等价性：如果 $X\le_P~Y~\land Y\le_P X~\Longleftrightarrow~X\equiv_P Y$

归约的目的是对问题的分类：
+ 设计算法。如果 $X\le_P Y$ 并且 $Y$ 是在多项式时间内可解决的，这 $X 也可以在多项式时间内解决；
+ 建立不可计算性。如果 $X\le_P Y$ 并且 $X$ 不能在多项式时间内解决，这 $Y$ 也不能在多项式时间内解决。

归约的基本策略：
+ 简单的等式关系推到。图论中独立集问题与点覆盖问题的归约等价性。
+ `从特殊情况推广到一般情况`。点覆盖归约到集合覆盖问题。
+ `构造方法`。3-SAT问题归约到独立集问题。

证明归约问题一般使用构造证明法，对于归约问题$X\le_P Y$，我们需要构造一个关于$X$和$Y$的桥梁$P$，我们需要证明在$P$下，关于$X的解和关于$Y$的解是等价的。

判定问题，搜索问题。

判定问题是多项式可求解的是指：对于任意的输入，算法的运行最多在输入长度的多项式步骤上。

验证算法：一种特殊的判定问题。

判定问题归类：
+ P. 有多项式时间求解的判定问题；
+ NP. 存在多项式时间验证算法的判定问题；
+ EXP. 存在指数时间求解的判定问题

证明：$\mathrm P \subseteq \mathrm{NP}$ 和 $\mathrm{NP} \subseteq \mathrm{EXP}$

`多项式转换、多项式归约` 不是很懂

NPC.：对于一个NP问题Y，每个NP问题X都满足$X\le_p Y$。

第一个NPC问题：电路满足问题

证明一个问题 Y（注意是判定问题）是NPC的：
1. 证明Y是NP的
2. 选择一个已知的NPC问题X
3. 证明归约性$X\le_p Y$

6类基本的NPC问题：

+ Packing problems:  SET-PACKING, INDEPENDENT SET.
+ Covering problems:  SET-COVER, VERTEX-COVER.
+ Constraint satisfaction problems:  SAT, 3-SAT.
+ Sequencing problems:  HAMILTONIAN-CYCLE, TSP.
+ Partitioning problems: 3D-MATCHING 3-COLOR.
+ Numerical problems:  SUBSET-SUM, KNAPSACK.

(To be continued.)


