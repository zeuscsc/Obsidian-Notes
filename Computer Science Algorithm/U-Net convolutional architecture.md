**U-Net** is a [[Convolutional Neural Network]] that was developed for biomedical [[Image segmentation]] at the Computer Science Department of the [University of Freiburg](https://en.wikipedia.org/wiki/University_of_Freiburg "University of Freiburg").

U-Net was introduced in the paper, U-Net: Convolutional Networks for Biomedical [[Image Segmentation]]. The model architecture is fairly simple: an encoder (for downsampling) and a decoder (for upsampling) with skip connections. As **Figure 1** shows, it shapes like the letter U hence the name U-Net.

![[Pasted image 20220729160041.png]]

The gray arrows indicate the skip connections that concatenate the encoder feature map with the decoder, which helps the backward flow of gradients for improved training.

One example I have done before was licence plate [[image segmentation]].
![[Pasted image 20220729162457.png]]