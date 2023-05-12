When there is a huge data [[Tree]] set, and you want to find a [[Tree#Node|node]] within.  You can find it via [[Viterbi Algorithm]] 
**Why don't we use [[Breadth-first search]] or [[Depth-first search]] then?**
It is because when facing a really huge [[tree]], both [[Breadth-first search]] or [[Depth-first search]] will be slow because the direction they pick may not be the best direction and waste lots of time in searching the wrong nodes.
**How to solve that problem then**
Given a [[Hidden Markov Model]], we can use the [[Viterbi Algorithm]] in order to compute the most likely sequence of latent states that produced a certain sequence of observations.  Neat: The algorithm is sort of [[Breadth-first search]] for a maximum in a certain perfect N-ary search [[tree]].
