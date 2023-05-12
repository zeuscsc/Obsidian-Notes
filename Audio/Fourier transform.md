### Wiki
Most often, the unqualified term **Fourier transform** refers to the transform of functions of a continuous [real](https://en.wikipedia.org/wiki/Real_number "Real number") argument, and it produces a continuous function of frequency, known as a _frequency distribution_. One function is transformed into another, and the operation is reversible. When the domain of the input (initial) function is time (t), and the domain of the output (final) function is [ordinary frequency](https://en.wikipedia.org/wiki/Frequency "Frequency"), the transform of function _s_(_t_) at frequency f is given by the complex number:
![[Pasted image 20220530095500.png]]
Evaluating this quantity for all values of f produces the _frequency-domain_ function. Then _s_(_t_) can be represented as a recombination of [complex exponentials](https://en.wikipedia.org/wiki/Complex_exponentials "Complex exponentials") of all possible frequencies:
![[Pasted image 20220530095514.png]]
which is the inverse transform formula. The complex number, _S_(_f_), conveys both amplitude and phase of frequency f.

### We know the Wiki now, now what?

**To switch the continuous wave tonon periodic signal only you can do so via fourier transform.**
In order to find its [[Fourier series]], a periodic function with period RR should be thought of as a function defined on a circle of circumference RR, call it S1RSR1. The [[Fourier series]] of the function is then its representation in the basis of L2(S1R)L2(SR1) given by orthonormal eigenfunctions of the Laplace operator.

If two functions have incommensurate periods, then their sum is nonperiodic, does not descend to a circle of any circumference, and therefore does not have a [[Fourier series]].

As functions on RR, if they are sufficiently nice, the Fourier transform gives an analogous decomposition, but because there are so many more eigenfunctions of the Laplace operator on RR, the sum is an integral. Compare:
![[Pasted image 20220530162235.png]]
You will recognize that if we integrate over the circle, ⟨f,eω⟩ gives the series of Fourier coefficients and if we integrate over R, it is the Fourier transform.

### Better visualize
You can convert 