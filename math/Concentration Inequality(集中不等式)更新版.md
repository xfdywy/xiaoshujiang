---
title:  Concentration Inequality(集中不等式)更新版
date: 2020-4-17
id: 2
mathjax: true
tags:
    -  Concentration Inequality
categorie:    math
---


Concentration inequality 刻画了一组随机变量的和（或者样本平均数）与其期望值的偏离程度，在算法收敛性分析过程中是非常有用的一类不等式。





<!--  more -->


这次主要总结一下最近一段时间遇到的集中不等式，不仅是不等式形式，也有不等式之间的相互关系的归纳总结，包括：



<!-- - Markov's inequality
- Chebyshev's inequality
- Chernoff bounds
- Hoeffding's inequality
- Bennett's inequality 
- Bernstein's inequalities
- Azuma's inequality
- Doob's martingale inequality -->


- [Markov's inequality](#markovs-inequality)
  - [条件：](#%e6%9d%a1%e4%bb%b6)
  - [公式：](#%e5%85%ac%e5%bc%8f)
  - [直观与讨论：](#%e7%9b%b4%e8%a7%82%e4%b8%8e%e8%ae%a8%e8%ae%ba)
- [Chebyshev's inequality](#chebyshevs-inequality)
  - [条件](#%e6%9d%a1%e4%bb%b6-1)
  - [公式](#%e5%85%ac%e5%bc%8f-1)
  - [直观与讨论](#%e7%9b%b4%e8%a7%82%e4%b8%8e%e8%ae%a8%e8%ae%ba-1)
- [Chernoff bounds](#chernoff-bounds)
  - [条件](#%e6%9d%a1%e4%bb%b6-2)
  - [公式](#%e5%85%ac%e5%bc%8f-2)
  - [直观与讨论](#%e7%9b%b4%e8%a7%82%e4%b8%8e%e8%ae%a8%e8%ae%ba-2)
- [Hoeffding's inequality](#hoeffdings-inequality)
  - [条件](#%e6%9d%a1%e4%bb%b6-3)
  - [公式](#%e5%85%ac%e5%bc%8f-3)
  - [直观与讨论](#%e7%9b%b4%e8%a7%82%e4%b8%8e%e8%ae%a8%e8%ae%ba-3)
- [Weighted Hoeffding Inequality](#weighted-hoeffding-inequality)
  - [条件](#%e6%9d%a1%e4%bb%b6-4)
  - [公式](#%e5%85%ac%e5%bc%8f-4)
  - [直观与讨论](#%e7%9b%b4%e8%a7%82%e4%b8%8e%e8%ae%a8%e8%ae%ba-4)
- [Bennett's inequality](#bennetts-inequality)
  - [条件](#%e6%9d%a1%e4%bb%b6-5)
  - [公式](#%e5%85%ac%e5%bc%8f-5)
  - [直观与讨论](#%e7%9b%b4%e8%a7%82%e4%b8%8e%e8%ae%a8%e8%ae%ba-5)
- [Bernstein's inequalities](#bernsteins-inequalities)
  - [条件](#%e6%9d%a1%e4%bb%b6-6)
  - [公式](#%e5%85%ac%e5%bc%8f-6)
  - [直观与讨论](#%e7%9b%b4%e8%a7%82%e4%b8%8e%e8%ae%a8%e8%ae%ba-6)
- [Azuma's inequality](#azumas-inequality)
  - [条件](#%e6%9d%a1%e4%bb%b6-7)
  - [公式](#%e5%85%ac%e5%bc%8f-7)
  - [直观与讨论](#%e7%9b%b4%e8%a7%82%e4%b8%8e%e8%ae%a8%e8%ae%ba-7)
- [Doob's martingale inequality](#doobs-martingale-inequality)
  - [条件](#%e6%9d%a1%e4%bb%b6-8)
  - [公式](#%e5%85%ac%e5%bc%8f-8)
  - [直观与讨论](#%e7%9b%b4%e8%a7%82%e4%b8%8e%e8%ae%a8%e8%ae%ba-8)
- [整体讨论](#%e6%95%b4%e4%bd%93%e8%ae%a8%e8%ae%ba)

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
Hoeffding 不等式刻画了一族随机变量的和偏离其期望的概率。只要求随机变量独立且有界，对随机变量的分布和各阶矩没有任何要求，并且这些随机变量可以不同分布。

Hoeffding不等式在机器学习算法的收敛性证明中起到了非常重要的作用，尤其是需要刻画算法的输出在多大概率的意义下可以收敛到我们希望的结果中这一情况下，我们可以利用hoeffding 不等式得到随机算法输出的结果与其期望结果的关系，从而得到想要的高概率界。


# Weighted Hoeffding Inequality

## 条件
> $x_i, \cdots, x_n$ 是一族独立的随机变量，且  $a_i< x_i < b_i$, $\bar{X} = \frac{1}{n}(w_1x_1 + \cdots + w_nx_n)$ 

## 公式

>  $$ P(\bar{x} - E[\bar{x}]\ge t) \le exp\left( -\frac{2n^2t^2}{\sum_{i=1}^n w_i^2(b_i-a_i)^2} \right)$$  


## 直观与讨论
与简单的Hoeffding 不等式类似，唯一区别在于是加权平均数。


 
# Bennett's inequality 

## 条件
> $x_i, \cdots, x_n$ 是一族独立的随机变量，且  $a_i< x_i < b_i$, $b_i-a_i=c_i \le C$, $\bar{X} = \frac{1}{n}( x_1 + \cdots +  x_n)$ ,
$\sigma^2 = \sum_{i=1}^nE[x_i^2]$, t为任意实数

## 公式




>  $$ P(\bar{X} -E[\bar{X}] \ge t) \le exp\left( -\frac{\sigma^2}{C^2} h(\frac{Ct}{n\sigma^2})\right)$$  
> $$ h(u) = (1+u)log(1+u) - u $$



## 直观与讨论

 因为利用了方差的信息，这个界更加细致。  



# Bernstein's inequalities

## 条件
> $x_i, \cdots, x_n$ 是一族独立的随机变量，且  $a_i< x_i < b_i$, $b_i-a_i=c_i \le C$, $\bar{X} = \frac{1}{n}(x_1 + \cdots + c_n)$ , $\sigma^2 = \sum_{i=1}^nE[x_i^2]$, t为任意实数


## 公式

>  $$ P(\bar{X} -E[\bar{X}] \ge t) \le exp\left( -\frac{t^2/2 }{n^2\sigma^2 +  Ctn/3} \right)$$  
  
## 直观与讨论
将Bennett不等式中的h函数用更松的形式代换, 可以证明这个不等式。

$$h(u)\ge \frac{u^2}{2+2u/3}$$

在Bernstein不等式中，我们可以看到，如果方差较小， 相同n和t的时候， 不等号右侧的概率值相比hoeffding不等式要小，说明Bernstein不等式通过考虑方差信息，获得了更加精细的结果。

# Azuma's inequality

前面讨论的一些不等式都要求随机变量独立，Azuma不等式研究的随机变量序列可以有相关性

## 条件
> $x_i, \cdots, x_n$ 是一族鞅序列，，且  $| x_i - x{i-1} | < c_i$,   t为任意实数

鞅指的是满足如下两个条件的随机过程
$$E[|x_n|] <\infty$$
$$E[x_{n+1}|x_1, \cdots x_n]=x_n$$


## 公式

>  $$ P(x_N-x_0 \ge t) \le exp\left( -\frac{t^2  }{2\sum_{i=1}^Nc_i^2 } \right)$$  
  
## 直观与讨论
如果将鞅序列拆分成鞅差序列， 即令$y_i = x_i - x_{i-1}$, 那么$y_i$满足如下两条，为鞅差序列
$$E[|x_n|] <\infty$$
$$E[x_{n+1}|\mathcal{F}_n]=0$$

则$x_n-x_0 = \sum_{i=1}^N y_i$Azuma不等式可以看成鞅差序列的和偏离0的概率



# Doob's martingale inequality
## 条件
>  $x$是上鞅，即对任意两个时刻$s<t$， $x_s \le E[x_t|\mathcal{F_s}]$

 

## 公式

>  $$ P(\sup_{0\le t \le T}x_t \ge C) \le  \frac{E[\max(x_T,0)]}{C}$$  
  
## 直观与讨论

这个不等式讨论了上鞅序列在路径中的表现，即如果我们知道上鞅序列$X_t$在最后$T$时刻的表现，我们就能大概推测出在整个0到T时刻之间随机变量$x_t$大于某个值的概率。


# 整体讨论

上述讨论的公式形式比较单一，都是描述随机变量或者随机变量的和偏离其中心的概率值的大小。但是实际上我们根据上文中的结果，可以很容易的推导出其他变形形式。

用Heoffding不等式举例，我们还可以有以下结果:

1. 当样本量为n的时候，以至少$1-\delta$的结果，我们可以有如下

$$ E[\bar{X} ] - \bar{X} \le \sqrt{\frac{\sum_{i=1}^n(b_i-a_i)^2\ln\frac{1}{\delta }}{2n^2}}$$


2. 同理，如果我们需要以至少$1-\delta$的概率保证差距小于$\epsilon$，则我们至少需要这么多样本(假设所有的$b_i <b, \ a_i>a$ )

$$N = \frac{ (b -a )^2\ln\frac{1}{\delta }}{2\epsilon^2} $$

类似这样的结论对于算法的收敛性分析和有限样本表现分析非常有用


 
<!-- 
|            |                                                                                         |                                                               |                                                                                 |
| ---------- | --------------------------------------------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| p          | 1-$\delta$                                                                              | $e^{-\frac{n\epsilon^2}{2\sigma^2 + \frac{14\eta\epsilon}{3}}}$ | 1-$\delta$                                                                      |
| n          | n                                                                                       | n                                                             | $\frac{((2\sigma^2)+\frac{14\eta\epsilon}{3})\ln\frac{1}{\delta} }{\epsilon^2}$ |
| $\epsilon$ | $\sqrt{\frac{2\sigma^2\ln\frac{2}{\delta}}{n}}+\frac{7\eta\ln\frac{2}{\delta}}{3(n-1)}$ | $\epsilon$                                                    | $\epsilon$                                                                      |
|            |                                                                                         |                                                               |                                                                                 |

 
 -->
