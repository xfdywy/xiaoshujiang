---
title: Search on the Replay Buffer：  Bridging Planning and Reinforcement Learning
date: 2019-12-1
tags:
    - paper_reading 
    - RL paper
category:  paper_reading
 
grammar_linkify: true
---

[toc]


# Motivation
Planning 和 RL 是解决control问题的两大类方法， 各有千秋，列举如下，但是实际问题往往都是介于他们的弱点上。所以，这篇文章要利用RL 来帮助解决planning方法中的困难点。 具体来说，我们要将目标分解成更简单的子任务，然后利用planning 方法来解决。在这个过程中，我们用RL 来帮助解决planning方法需要的信息，例如子问题的寻找，graph的构造等

- Planning
    - adv
        - long horizons
    - disadv
        - sample valid states
        - estimate the distance between two states
        - acquire a local policy for reaching nearby states
- RL
    - adv
        - learning policy and value of states
    - disadv
        - fail to long horizon
# Idea
主要的想法就是planning 需要的信息可以用一个graph来表示，而这个graph可以利用RL 来学里面的点和边。

层次RL 的setting
# Method and contribution

## graph的构造


# Valuable Point


# Further
## Beyond Confidence Regions: Tight Bayesian Ambiguity Sets for Robust MDPs

- model based 如何利用model的信息
- 鲁棒强化学习，test setting， 要在一个p 的set中，做min

## On the Expressive Power of Deep Neural Networks

measure:
 - linear region
 - trajectory
    




.