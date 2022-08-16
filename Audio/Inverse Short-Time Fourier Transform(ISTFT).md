The [[Short-time Fourier transform (Discrete-time Fourier transform)]] is [invertible](https://en.wikipedia.org/wiki/Invertible_function "Invertible function"), that is, the original signal can be recovered from the transform by the Inverse STFT. The most widely accepted way of inverting the STFT is by using the [overlap-add (OLA) method](https://en.wikipedia.org/wiki/Overlap%E2%80%93add_method "Overlap–add method"), which also allows for modifications to the STFT complex spectrum. This makes for a versatile signal processing method, referred to as the _overlap and add with modifications_ method.

Converts a complex-valued spectrogram `stft_matrix` to time-series `y` by minimizing the mean squared error between `stft_matrix` and STFT of `y` as described in up to Section 2 (reconstruction from MSTFT).

In general, window function, hop length and other parameters should be same as in stft, which mostly leads to perfect reconstruction of a signal from unmodified `stft_matrix`.
