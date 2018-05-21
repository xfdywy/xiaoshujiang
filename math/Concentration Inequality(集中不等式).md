---
title:  Concentration Inequality(集中不等式)
date: 2018-5-21
mathjax: true
tags:
    -   Concentration Inequality
categories:  math
---


Concentration inequality 刻画了一组随机变量的和（或者样本平均数）与其期望值的偏离程度，在算法收敛性分析过程中是非常有用的一类不等式。

这次主要总结一下最近一段时间遇到的集中不等式，不仅是不等式形式，而是不等式之间的相互关系的归纳总结，包括：

- Markov's inequality
- Chebyshev's inequality
- Chernoff bounds
- Hoeffding's inequality
- Bennett's inequality 
- Bernstein's inequalities
- Azuma's inequality
- Doob's martingale inequality

# Markov's inequality
## 条件：
> X 是非负随机变量, a>0

## 公式：

> $$ \operatorname{P}(X \geq a) \leq \frac{\operatorname{E}(X)}{a} $$
\begin{aligned} 
    a  &= \mathcal{A}
        &\le alpha
\end{aligned}
## 直观：
一个随机变量的取值大于a的概率要小于其期望值除以a。直观很简单就是，假设10个人的平均工资是1块钱，那么如果超过2两个人的工资超过5块钱了，那么哪怕剩下来的人没有工资，这10个人的工资平均也超过1块钱了. 这里大家的工资就是随机变量X, a就是5， E(x)就是1， $P(X \le a)$ 就是0.2

## 变形


Markov's inequality 最简单，也最“松”，只用到了随机变量的期望信息。

这里“松”是指，对于相同的a，我们求出来的概率最小，或者要求相同的概率，得到的a最大（不必要）。