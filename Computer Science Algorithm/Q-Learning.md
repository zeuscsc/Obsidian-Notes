![[Pasted image 20221018223420.png]]
The purpose of Reinforcement Learning (RL) is to solve a [[Markov Decision Process]] ([[Markov Decision Process|MDP]]) when you don’t know the [[Markov Decision Process|MDP]], in other words you don’t know the states you can visit and you don’t know the transition function from each state.

One way to solve such a problem is to first learn the [[Markov Decision Process|MDP]] and then solve it using algorithms such as value-iteration or policy-iteration, both using the Bellman equation . The [[Markov Decision Process|MDP]] can be learned simulating different actions from each state until you have a high degree of confidence in the learned transition function and the learned reward function. Unfortunately this is frequently not possible because the [[Markov Decision Process|MDP]] is too large or it would be too expensive to learn the [[Markov Decision Process|MDP]].

RL algorithms such as [[Q-Learning]] try to do both things at the same time: learn the [[Markov Decision Process|MDP]] and solve it to find the optimal policy.

To do that the algorithm needs to solve the exploration/exploitation tradeoff. Exploration means trying random actions, this helps discover the underlying [[Markov Decision Process|MDP]]. Exploitation means following the so-far optimal policy, this helps maximize rewards.

So RL is a technique to learn an [[Markov Decision Process|MDP]] and solve it for the optimal policy at the same time.