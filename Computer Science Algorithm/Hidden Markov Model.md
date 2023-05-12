### Hidden Markov Model
[[Hidden Markov Model]] ([[Hidden Markov Model|HMM]]) is a statistical Markov model in which the system being modeled is assumed to be a Markov process — call it ${\displaystyle X}$ — with unobservable ("hidden") states. As part of the definition, [[Hidden Markov Model|HMM]] requires that there be an observable process ${\displaystyle Y}$ whose outcomes are "influenced" by the outcomes of ${\displaystyle X}$ in a known way. Since ${\displaystyle X}$ cannot be observed directly, the goal is to learn about ${\displaystyle X}$ by observing ${\displaystyle Y.}$${\displaystyle Y.}$ [[Hidden Markov Model|HMM]] has an additional requirement that the outcome of ${\displaystyle Y}$ at time ${\displaystyle t=t_{0}}$${\displaystyle t=t_{0}}$ may be "influenced" exclusively by the outcome of ${\displaystyle X}$ at ${\displaystyle t=t_{0}}$${\displaystyle t=t_{0}}$ and that the outcomes of ${\displaystyle X}$ and ${\displaystyle Y}$ at ${\displaystyle t<t_{0}}$${\displaystyle t<t_{0}}$ must not affect the outcome of ${\displaystyle Y}$ at ${\displaystyle t=t_{0}.}$${\displaystyle t=t_{0}.}$

Hidden Markov models are known for their applications to thermodynamics, statistical mechanics, physics, chemistry, economics, finance, signal processing, information theory, pattern recognition - such as speech, handwriting, gesture recognition, part-of-speech tagging, musical score following, partial discharges and bioinformatics.

## Those are the "definition" from wiki textbook.  So now what?
Same as the [[Markov Chain]] chapter, lets get a better understanding from an example.  We will use the same example as that chapter.

![[Pasted image 20220328205124.png]]

The green lines are the [[#Markov Chain]] and the Red line points to the observation the numbers are the probility.

Here is the event probility:
$\begin{bmatrix}0.9 & 0.1 \\0.6 & 0.4 \\0.2 & 0.8 \\\end{bmatrix}$--->$\begin{bmatrix} \text{Rainy Sad} & \text{Rainy Happy} \\ \text{Cloudy Sad} & \text{Cloudy Happy} \\ \text{Sunny Sad} & \text{Sunny Happy} \\\end{bmatrix}$

#### What if you observed Happy Happy Sad?
What is the probility of the result is eaual to Sunny Cloudy Sunny?

From the [[Transition matrix]]:
$\begin{bmatrix}0.5 & 0.3 & 0.2 \\0.4 & 0.2 & 0.4 \\0.0 & 0.3 & 0.7 \\\end{bmatrix}$ $\begin{bmatrix}0.9 & 0.1 \\0.6 & 0.4 \\0.2 & 0.8 \\\end{bmatrix}$

We know that the probility of Sunny Cloudy Sunny will be 0.00391

###### But is this the most likely weather that happened?
From the argmax of the [[Transition matrix]] above, we know that the most likely event that will happen will be Sunny Sunny Cloudy 0.04105

You may still be able to see this if the case is as sample as the example, but if the case is more complex, that will be another story.

## Another Example
**Dishonest Casino With Hidden Markov Model** 
In this example, we suspect that a casino is trading out a fair die (singular or dice) for a loaded die. We want to figure out 1) when the loaded die was used (i.e. the most likely path) 2) how often the loaded die is used (i.e. the transition probabilities) and 3) the probabilities for each outcome of a roll for the loaded die (i.e. the emission probabilities).
![[Dishonest Casino With Hidden Markov Model.png]]
After we watch the dice rolled many times, we will know the roll probabilities by state 
![[Roll Probabilities by State.png]]

## So now we know we can get the most likely event happened, now what?
The reason I am running into [[Hidden Markov Model|HMM]] is beacuse I am currently researching into [[Speech Recognition]].  Although you can use [[MFCC - Mel-frequency cepstral coefficients|MFCC]] and [[Convolutional Neural Network|CNN]] to classify simple [[audio]] samples to different commands, but when the speaker have ascent, the regconiation result will very likely be wrong.  To solve that problem, we can use [[Hidden Markov Model|HMM]].

#### But how?
When somone say "I go to school by bus", the computer will not know the text yet.  Instead, it will get [[audio]] samples like this:
![[Pasted image 20220328230432.png]]
With ascent, "go" could sounds like "no", "I" could be like "a".  Then there could be multiple possibility:
I go to school by bus,
I no to school by bus, 
A no to school by bus,
A go to school by bus.
By using dataset like Wiki, News, Social Media Feed, we can build a [[Markov Chain]] from it.
Just like weather, all we need to do is to fill in the possibilities of each words and the words that comes before or after them.  Here we will focus on "I" and "go".
$\begin{bmatrix} \text{I} \\ \text{Go} \\ \text{No} \\ \text{Am} \\ \text{Was}\\\end{bmatrix}$ ---> $\begin{bmatrix} 0&0.1&0&0.5&0.4 \\ 0&1&0&0&0 \\ 0&0&1&0&0 \\ 0.33&0.33&0.33&0&0.01 \\ 0.5&0.25&0.25&0&0\\\end{bmatrix}$ 
I made up this [[Transition matrix]] (which mean it have nothing to do with the true possibilities of the "I" and "Go" usage), and from that fake [[Transition matrix]], we can know that "I go to school by bus" is more likely to be spoken by the user then "I no to school by bus".
