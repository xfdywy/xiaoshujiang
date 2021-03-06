---
title:  Reinforcement Learning Topic 
date: 2018-3-29 00:00:19
tags:
    -  reinforcement learning
  
categories:  reinforcement learning

---
 
 

## General Framework

 There are many challenge problems in RL. They can be categorized in terms of different aspects

### From Algorithm
1. Value function based

   - policy iteration(policy evaluation)
   - value iteration(Q-learning)

2. Policy function based

   - reinforce algorithm

3. Actor Critic
 


### From Learning Process

1. Data collection
     * exploration
     * parallel distributed learning

2. Data selection

      * prioritized replay buffer
                       
3. Data utilization

     * learning rate setting
     * network structure
     * variance reduction
     * model-based



## Topics

### Theory
 - Policy evaluation sample complexity
    * More algorithms
    * Function approximation
    * None I.I.D.
 - Control algorithms sample complexity
    * Policy iteration 
        * Error propagation
    * Value iteration
        * Regret bound
        * PAC bound
        * upper bounds are too conservative, lower bounds are needed
 - Exploration theory
    * Based on Q-learning
        * OFU(optimistic on the face of uncertainty)
        * Thompson sampling
    * Based on PG
        * Entropy?
            
 

### Algorithm
1. Exploration algorithms
    - OFU
        - Pseudo count
        - Curiosity-driven
            - VIME
            - Intrinsic Curiosity Module (ICM)
    - Thompson sampling
        -  Deep exploration
            -  Randomized Value Functions
            -  Bootstrapped DQN 
            -  Parameter Space Noise for Exploration
2. More efficient Policy gradient method
    - Trust region method
    - REINFORCE algorithms have large variance
        - variance reduction through control variable
        - variance reduction through change distribution
        - variance reduction through replace REINFORCE with other pure gradient method
3. Combine on policy and off policy method
4. Combine model based and model free method


### Application
- Game Playing
- Robotics

## Exploration

There are two different meanings behind the **exploration** term.

- The first one is when the state space is infinite or too large to be traversed.
- The second one is when the state space is finite. 

 For the first case, identifying the **"visited level"** is the most important thing. Only if we see enough  state, can we make the right decision. The **"visited level"** is not the trivial count of each state because of the dependent between each state.

For the second case, identifying the **"uncertainty level"** is the most important thing. We should go mostly to the state of which the estimated value is large and the uncertainty level is low.

| estimated value / uncertanty | large | small |
| :--------------------------: | :---: | :---: |
|             high             |   +   |   +   |
|             low              |  +++  |   -   |



## Variance Reduction

### Importance sampling

Importance sampling method may introduce a high variance in RL algorithms since the different policies may take one action in very different probability( denominator near to 0 and numerator near to 1, vice-versa ). We need to do variance reduction together with importance sampling.

### Variance Reduction in PG

Control variable provides a framework to combine model base and model free method together with the variance reduction issue

### Averaged-DQN

## Model Based

### model based for data collection

### model based for data utilization

### distributed model based for data utilization(xufang)

## Policy Gradient based

### TRPO with different metric(w distance)

## Other topics

### Inverse RL

1. Inverse RL with GAN 
2. ​

### Multiagent, Multitask

### Hierarchical RL



 

 



------
<style type="text/css">
    h1 { counter-reset: h2counter; }
    h2 { counter-reset: h3counter; }
    h3 { counter-reset: h4counter; }
    h4 { counter-reset: h5counter; }
    h5 { counter-reset: h6counter; }
    h6 { }
    h2:before {
      counter-increment: h2counter;
      content: counter(h2counter) ".\0000a0\0000a0";
    }
    h3:before {
      counter-increment: h3counter;
      content: counter(h2counter) "."
                counter(h3counter) ".\0000a0\0000a0";
    }
    h4:before {
      counter-increment: h4counter;
      content: counter(h2counter) "."
                counter(h3counter) "."
                counter(h4counter) ".\0000a0\0000a0";
    }
    h5:before {
      counter-increment: h5counter;
      content: counter(h2counter) "."
                counter(h3counter) "."
                counter(h4counter) "."
                counter(h5counter) ".\0000a0\0000a0";
    }
    h6:before {
      counter-increment: h6counter;
      content: counter(h2counter) "."
                counter(h3counter) "."
                counter(h4counter) "."
                counter(h5counter) "."
                counter(h6counter) ".\0000a0\0000a0";
    }
</style>
