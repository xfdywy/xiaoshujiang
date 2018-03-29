---
title:  Reinforcement Learning topic 
date: 2018-3-29 00:00:19
tags:
    -  reinforcement learing
  
categories:  reinforcement learning
---
 
# 1. general framework

 There are many challeng problems in RL. They can be categorized in terms of different aspects
 
## 1.1 From Algorithm 

 1. Value function based

	 - policy iteration(policy evaluation)
	 - value iteration(Q-learing)

 2. Policy funciton basd

 	 - reinforce algorithm

 3. Actor Critic

## 1.2 From Learning Process

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



```mermaid
graph LR
A[Hard edge] -->B(Round edge)
    B --> C{Decision}
    C -->|One| D[Result one]
    C -->|Two| E[Result two]
​```