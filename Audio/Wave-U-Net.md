The Wave-U-Net is a [[convolutional neural network]] designed for [[audio]] source separation tasks that works directly on the raw [[audio]] waveform. It is an adaptation of the [[U-Net convolutional architecture]] to the one-dimensional time domain. The network uses a series of downsampling and upsampling blocks to compute features on multiple scales/levels of abstraction and time resolution, which are then combined to make a prediction. The Wave-U-Net participated in the SiSec separation campaign and achieved good performance despite using a limited dataset compared to other submissions.

The Wave-U-Net is a [[Convolutional Neural Network]] applicable to [[audio]] source separation tasks, which works directly on the raw [[audio]] waveform, presented in [this paper](https://arxiv.org/abs/1806.03185).

The Wave-U-Net is an adaptation of the [[U-Net convolutional architecture]] to the one-dimensional time domain to perform end-to-end [[audio]] source separation. Through a series of downsampling and upsampling blocks, which involve 1D convolutions combined with a down-/upsampling process, features are computed on multiple scales/levels of abstraction and time resolution, and combined to make a prediction.

See the diagram below for a summary of the network architecture.

![[Pasted image 20220729155750.png]]
### Participation in the SiSec separation competition

The Wave-U-Net also participated in the [SiSec separation campaign](https://sisec.inria.fr/) as submissions [STL1](https://github.com/sigsep/sigsep-mus-2018/blob/master/submissions/STL1/description.md) and [STL2](https://github.com/sigsep/sigsep-mus-2018/blob/master/submissions/STL2/description.md) and achieved a good performance, especially considering the limited dataset we used compared to many other submissions despite having a more data-hungry end-to-end approach (we have to learn the frequency decomposition front-end from data as well).