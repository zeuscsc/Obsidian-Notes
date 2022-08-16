# Markov Chain
A Markov chain is a mathematical system that experiences transitions from one state to another according to certain probabilistic rules. The defining characteristic of a Markov chain is that no matter how the process arrived at its present state, the possible future states are fixed.

## Those are the "definition" from wiki textbook.  So now what?
Lets start by an example.  This is the weather recorded in [Zeus's Secret Base](https://app.gather.town/app/f5QVEB4XpQWlSVQt/ZeusSecretBase).  Usually can classify into the following 3 weather: Rainy, Cloudy, and Sunny.  Here is the transition model.

![[Pasted image 20220328205834.png]]

From the [[Markov Chain]] above, we know that if today is rainy, there will be a 50% chance tomorrow will also be rainy, and 20% chance tomorrow will be sunny, and 30% chance tomorrow will be cloudy.  The same goes for cloudy and sunny day.

Here is the transition matrix:
$\begin{bmatrix}0.5 & 0.3 & 0.2 \\0.4 & 0.2 & 0.4 \\0.0 & 0.3 & 0.7 \\\end{bmatrix}$ $\begin{bmatrix}\text{Today Rainy tomorrow Rainy} & \text{Today Rainy tomorrow Cloudy} & \text{Today Rainy tomorrow Sunny} \\\text{Today Cloudy tomorrow Rainy} & \text{Today Cloudy tomorrow Cloudy} & \text{Today Cloudy tomorrow Sunny} \\\text{Today Sunny tomorrow Rainy} & \text{Today Sunny tomorrow Cloudy} & \text{Today Sunny tomorrow Sunny} \\\end{bmatrix}$ 
You can get this graph / matrix either by observation or [[Monte Carlo]] method.  

