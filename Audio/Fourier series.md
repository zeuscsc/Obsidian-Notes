A Fourier series is a sum that represents a periodic function as a sum of sine and cosine waves. The frequency of each wave in the sum, or harmonic, is an integer multiple of the periodic function's fundamental frequency. Each harmonic's phase and amplitude can be determined using harmonic analysis.


### Square Wave
Can we use sine waves to make a square wave?
Our target is this square wave:
![[Pasted image 20220530003523.png]]
Start with **sin(x)**:
![[Pasted image 20220530004315.png]]
Then take **sin(3x)/3**:
![[Pasted image 20220530004453.png]]
And add it to make **sin(x)+sin(3x)/3**:
![[Pasted image 20220530004503.png]]
Can you see how it starts to look a little like a square wave?
Now take **sin(5x)/5**:
![[Pasted image 20220530004516.png]]
Add it also, to make **sin(x)+sin(3x)/3+sin(5x)/5**:
![[Pasted image 20220530004525.png]]
Getting better! Let's add a lot more sine waves.
Using 20 sine waves we get **sin(x)+sin(3x)/3+sin(5x)/5 + ... + sin(39x)/39**:
![[Pasted image 20220530004541.png]]
Using 100 sine waves we get **sin(x)+sin(3x)/3+sin(5x)/5 + ... + sin(199x)/199**:
![[Pasted image 20220530004555.png]]


**How to get those wave functions back?**
![[Pasted image 20220530001918.png]]
![[Pasted image 20220530010403.png]]

### But what about the real world?
In real world, the sound wave won't last forever.
That's why people use [[Fourier transform | (Continuous) Fourier transform]] to transform the continuous waves to wave that have a limited time.  That also mean we can use the [[Fourier transform]] to make the limited sound wave analysis with [[Fourier series]].  If the input audio is [[Types of Audio#Digital Audio|Digital]] not [[Types of Audio#Analog Audio|Analog]], then we can use the [[Short-time Fourier transform (Discrete-time Fourier transform)]] to process digital audio.  
