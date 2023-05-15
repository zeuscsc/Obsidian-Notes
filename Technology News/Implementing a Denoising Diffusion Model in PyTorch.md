![[snapshots/a4Yfz2FxXiY/00-00-03.png]]
# Implementing a Denoising Diffusion Model in PyTorch
Implementing a Denoising Diffusion Model in PyTorch

![[snapshots/a4Yfz2FxXiY/00-01-28.png]]
### Introduction and Motivation
![[snapshots/a4Yfz2FxXiY/00-00-30.png]]
- Diffusion models are used for generative deep learning to learn a distribution of data and generate new data
![[snapshots/a4Yfz2FxXiY/00-30-20.png]]
- Popular architectures for generative deep learning include GANs and VAEs, but fusion models are another option
![[snapshots/a4Yfz2FxXiY/00-02-15.png]]
- Fusion models destroy input by adding noise and recover it through a neural network
![[snapshots/a4Yfz2FxXiY/00-04-17.png]]
- Model works by gradually adding noise in a backward process called denoising
![[snapshots/a4Yfz2FxXiY/00-04-50.png]]
- To generate new data, backward process is performed from random noise
![[snapshots/a4Yfz2FxXiY/00-02-49.png]]
- We want to build a simple diffusion model on an image dataset

![[snapshots/a4Yfz2FxXiY/00-04-54.png]]
### Dataset and Existing Implementations
![[snapshots/a4Yfz2FxXiY/00-05-51.png]]
- Using Stanford CAS dataset of 16,000 images (8,000 train, 8,000 test)
![[snapshots/a4Yfz2FxXiY/00-05-12.png]]
- Will need three things for implementation: scheduler that adds noise, model that predicts noise, and way to encode current time step
![[snapshots/a4Yfz2FxXiY/00-06-20.png]]
- Implementation will be based on existing implementations of diffusion models
![[snapshots/a4Yfz2FxXiY/00-06-39.png]]
- Consists of forward process, backward process, loss function, sampling, and training

![[snapshots/a4Yfz2FxXiY/00-06-54.png]]
### Forward Process and Math of Fusion Models
![[snapshots/a4Yfz2FxXiY/00-07-04.png]]
- Forward process involves adding noise to images using a Markov process denoted with Q
![[snapshots/a4Yfz2FxXiY/00-07-51.png]]
- Noise added depends only on previous image, and is gradually increased through a variance schedule beta
- Mean of distribution is previous image times term that depends on variance schedule, while variance is fixed to beta
![[snapshots/a4Yfz2FxXiY/00-09-19.png]]
- Beta controls how fast we converge towards a mean of 0, which corresponds to a standard Gaussian distribution
![[snapshots/a4Yfz2FxXiY/00-09-41.png]]
- Noise must be added correctly to reach isotropic Gaussian distribution with mean of 0 and fixed variance
![[snapshots/a4Yfz2FxXiY/00-10-46.png]]
- Closed-form of mean and variance can be pre-calculated based on cumulative variance schedules for sampling at specific time steps

![[snapshots/a4Yfz2FxXiY/00-12-18.png]]
### Noise Scheduler and Implementation
![[snapshots/a4Yfz2FxXiY/00-12-26.png]]
- Define linear beta schedule using torch.linspace
![[snapshots/a4Yfz2FxXiY/00-12-41.png]]
- Helper function extracts specific index from list and considers batch size
![[snapshots/a4Yfz2FxXiY/00-13-29.png]]
- Forward diffusion sample function uses pre-calculated values to calculate noisy version of image at specific time step
![[snapshots/a4Yfz2FxXiY/00-07-20.png]]
- Samples noise and calculates specific index values to add noise to original image
![[snapshots/a4Yfz2FxXiY/00-14-06.png]]
- Need to put dataset into PyTorch data loader and convert to tensors, scale between 0 and 1
![[snapshots/a4Yfz2FxXiY/00-08-53.png]]
- Images should be in range of -1 to 1 for use with betas

![[snapshots/a4Yfz2FxXiY/00-06-46.png]]
### Conclusion
- Diffusion models offer another option for generative deep learning through the use of fusion models
- Implementation involves forward process of adding noise, backward process of denoising with neural network, and pre-calculated variance schedules
- Dataset used is Stanford CAS with 16,000 images and implementation is based on existing implementations of diffusion models.## Introduction to the Fusion Models
![[snapshots/a4Yfz2FxXiY/00-30-05.png]]
This video gives an overview of the Fusion Models, which are probabilistic generative models that can be used for multiple tasks such as image processing, data compression, and data augmentation.

## Forward Process
The forward process of the Fusion Model involves adding noise to an image and then processing it through a [[Hidden Markov Model]] to predict the noise at each time step. The noise is then subtracted from the image to recover it. The noise added to the image is based on a Gaussian distribution, whose variance is set fixed. The goal is to predict the noise distribution at each time step. 

## Building Blocks of the Forward Process
![[snapshots/a4Yfz2FxXiY/00-16-13.png]]
The building blocks that are part of the forward process include data loading of the train and test sets, data normalization, and data transformation. The authors propose to use a U-net for the neural network model, which takes a noisy image with three colored channels as input and predicts the noise in the image. The input tensors get smaller but also deeper as more channels are added. Positional embeddings are used to consider the time step in the model. 

![[snapshots/a4Yfz2FxXiY/00-20-55.png]]
## Backward Process and UNET Implementation
![[snapshots/a4Yfz2FxXiY/00-16-31.png]]
The backward process involves predicting the noise given an image. The authors propose to use a U-net, which is a special neural network that has a structure similar to the one used in an autoencoder, and can be used for [[image segmentation]]. The UNET implementation takes an incoming image with three channels for red, green and blue, extends these channels by applying learnable filters in these convolutional layers so that we have more channels, and finally reduces the size. 

## Loss Function and Sampling
![[snapshots/a4Yfz2FxXiY/00-26-52.png]]
The final loss function is defined by calculating the L2 distance of the predicted noise and the actual noise in the image. The sampling function generates new images and tests them during training. 

![[snapshots/a4Yfz2FxXiY/00-17-28.png]]
## Results
The author tested the model on the CIFAR-10 dataset and found that it can generate high-quality images after training for around 500 epochs. The model can also be used for other domains such as molecules and [[audio]]. The fusion models are a promising family of generative models.

Source: [(97) Diffusion models from scratch in PyTorch - YouTube](https://www.youtube.com/watch?v=a4Yfz2FxXiY)
