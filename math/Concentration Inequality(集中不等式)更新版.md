---
title:  Concentration Inequality(集中不等式)更新版
date: 2020-4-17
mathjax: true
tags:
    -  Concentration Inequality
categorie:    math
---


Concentration inequality 刻画了一组随机变量的和（或者样本平均数）与其期望值的偏离程度，在算法收敛性分析过程中是非常有用的一类不等式。

这次主要总结一下最近一段时间遇到的集中不等式，不仅是不等式形式，而是不等式之间的相互关系的归纳总结，包括：

<!--  more -->

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
 
## 直观与讨论：
一个随机变量的取值大于a的概率要小于其期望值除以a。直观很简单就是，假设10个人的平均工资是1块钱，那么如果超过2两个人的工资超过5块钱了，那么哪怕剩下来的人没有工资，这10个人的工资平均也超过1块钱了. 这里大家的工资就是随机变量X, a就是5， E(x)就是1， $P(X \le a)$ 就是0.2



Markov's inequality 最简单，也最“松”，只用到了随机变量的期望信息。
这里“松”是指，对于相同的a，我们求出来的概率最小，或者要求相同的概率，得到的a最大（不必要）。


# Chebyshev's inequality

## 条件
>  $X$ 为均值为$\mu$， 方差为$\sigma^2$ 的随机变量, 任意实数$k$

## 公式

> $$ P(|X-\mu|\ge k\sigma)\le \frac{1}{k^2} $$

## 直观与讨论

Chebyshev 不等式刻画了一个随机变量偏离其均值的概率。直观来说就是离均值越远，概率越小，并且小的速率收到方差的控制。由于Chebyshev不等式不依赖分布的具体信息，只依赖一阶矩和二阶矩，因此应用广泛。

Chebyshev不等式通过考虑方差和期望的信息， 比markov不等式更加细致。

 
# Chernoff bounds

## 条件

> $X$ 是n个独立随机变量 $x_1, \cdots , x_n$ 的和， $t$是任意大于0的实数

## 公式

> $$ P(x_i>a)=P(e^{t x_i}>e^{ta}) \le e^{-ta}E[ e^{tX}] $$
> $$ P(X>a) \le e^{-ta}E[\Pi_i e^{tx_i}] $$
> $$ P(X>a) \le min_{t>0}\left[ e^{-ta}E[\Pi_i e^{tx_i}] \right] $$

## 直观与讨论

Chernoff 算是一个技巧，本质上是Markov不等式的直接应用。如看上文公式中的第一个式子，左边的等号就是Chernoff的核心技巧，即将随机变量转化成指数的形式，并且引入一个新的参数$t$，右边的$\le$就是直接应用了Markov不等式。

下面可以看到Chernoff的技巧是得到 Hoeffding不等式的关键。简单来说，Hoeffding不等式是Chernoff的应用。


# Hoeffding's inequality

## 条件

> $x_i, \cdots, x_n$ 是一族独立的随机变量，且  $a_i< x_i < b_i$, $\bar{X} = \frac{1}{n}(x_1 + \cdots + c_n)$ 

## 公式

>    $$ P(\bar{x} - E[\bar{x}]\ge t) \le exp\left( -\frac{2n^2t^2}{\sum_{i=1}^n (b_i-a_i)^2} \right)$$  

## 直观与讨论
Hoeffding 不等式常用于


# Bennett's inequality 
# Bernstein's inequalities
# Azuma's inequality
# Doob's martingale inequality


 

|            |                                                                                         |                                                               |                                                                                 |
| ---------- | --------------------------------------------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| p          | 1-$\delta$                                                                              | $e^{-\frac{n\epsilon^2}{2\sigma^2 + \frac{14\eta\epsilon}{3}}}$ | 1-$\delta$                                                                      |
| n          | n                                                                                       | n                                                             | $\frac{((2\sigma^2)+\frac{14\eta\epsilon}{3})\ln\frac{1}{\delta} }{\epsilon^2}$ |
| $\epsilon$ | $\sqrt{\frac{2\sigma^2\ln\frac{2}{\delta}}{n}}+\frac{7\eta\ln\frac{2}{\delta}}{3(n-1)}$ | $\epsilon$                                                    | $\epsilon$                                                                      |
|            |                                                                                         |                                                               |                                                                                 |

 

