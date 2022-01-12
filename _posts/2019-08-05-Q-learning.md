---
layout: post
title:  "Q-learning"
date:   2019-08-05 00:00:00 +0800
categories: note
tags: [Q-learning]
---
## Reinforcement Learning  
From A to Z by repeat again and again.  

## Bellman Equation  
Learning from a ***reward*** after an **action** at a **state** in an environment.  
s : state  
a : action  
R : Reward  
V : Value  
![](http://latex.codecogs.com/gif.latex?\gamma) : discount  

![](http://latex.codecogs.com/gif.latex?V(s)=\underset{a}{max}(R(s,a)+\gamma V(s')))  

## Markov Decision Process(MDP)  
### Deterministic Search  
100% chances take the action we want.  
### Non-Deterministic Search  
not 100% chances take the action we want.  

A stochastic process has the **Markov property** if the conditional probability distribution of future states of the process(conditional on both past and present states) depends only upon the present state, not on the sequence of events that preceded it. A process with this property is called a **Markov process**.  

**Markov Decision Processes (MDPs)** provide a mathematical framework for modeling decision making in situations where outcomes are partly random and partly under the control of a decision maker.  

P : probability  

![](http://latex.codecogs.com/gif.latex?V(s)=\underset{a}{max}(R(s,a)+\gamma \underset{s'}{\sum} P(s,a,s')V(s')))  

## Policy vs Plan  
Plan : Take an action which get to the highest value intuitively.  

Policy : Take an conservative action which get the the highest value safely.  

## Living Penalty  
Make negative rewards at non-terminal states so that agent will end episode faster.  
Proper living penalty makes agent act more intuitive.  
Improper living penalty might cause agent goes wrong.  

## Where's the Q?  
Q = Quality  
Q(s,a) means the value of the action(a) at a certain state(s).  

![](http://latex.codecogs.com/gif.latex?Q(s,a)=R(s,a)+\gamma \underset{s'}{\sum }(P(s,a,s')\underset{a'}{max}Q(s',a')))  

## Temporal Difference (TD)
![](http://latex.codecogs.com/gif.latex?\begin{align*}Before&=Q_{t-1}(s,a)\\After&=R(s,a)+\gamma\underset{a'}{max}Q(s',a')\\TD(a,s)&=After-Before\\&=R(s,a)+\gamma\underset{a'}{max}Q(s',a')-Q_{t-1}(s,a)\\Q_t(s,a)&=Q_{t-1}(s,a)+\alpha TD_t(a,s)\\&=Q_{t-1}(s,a)+\alpha(R(s,a)+\gamma\underset{a'}{max}Q(s',a')-Q_{t-1}(s,a))\end{align*})  
