Demucs is based on [[U-Net convolutional architecture]] inspired by [[Wave-U-Net]]. The most recent version features hybrid spectrogram/waveform separation, along with compressed residual branches, local attention and singular value regularization. Checkout our paper Hybrid Spectrogram and Waveform Source Separation for more details. As far as we know, Demucs is currently the only model supporting true end-to-end hybrid model training with shared information between the domains, as opposed to post-training model blending.

When trained only on MusDB HQ, Hybrid Demucs achieved a SDR of 7.33 on the MDX test set, and 8.11 dB with 200 extra training tracks. It is particularly efficient for drums and bass extraction, although KUIELAB-MDX-Net performs better for vocals and other accompaniments.


[[Inverse Short-Time Fourier Transform(ISTFT)]] is passed to the network and get the output [[Inverse Short-Time Fourier Transform(ISTFT)]] back.
![[Pasted image 20220601001010.png]]