**Mel-frequency cepstral coefficients** (MFCCs) are coefficients that collectively make up an MFC. They are derived from a type of cepstral representation of the [[audio]] clip (a nonlinear "spectrum-of-a-spectrum").

![[Pasted image 20220328224854.png]]

To get MFCC, compute the DCT on the [[Mel Spectrogram]]. The [[Mel Spectrogram]] is often log-scaled before.

MFCC is a very compressible representation, often using just 20 or 13 coefficients instead of 32-64 bands in [[Mel Spectrogram]]. The MFCC is a bit more decorrelarated, which can be beneficial with linear models like Gaussian Mixture Models. With lots of data and strong classifiers like Convolutional Neural Networks, [[Mel Spectrogram]] can often perform better.