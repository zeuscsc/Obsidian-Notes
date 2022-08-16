An autoencoder is a type of artificial neural network used to learn efficient codings of unlabeled data (unsupervised learning). The encoding is validated and refined by attempting to regenerate the input from the encoding. The autoencoder learns a representation (encoding) for a set of data, typically for dimensionality reduction, by training the network to ignore insignificant data (“noise”).

![[Pasted image 20220729153214.png]]

An autoencoder has two main parts: an encoder that maps the message to a code, and a decoder that reconstructs the message from the code. An optimal autoencoder would perform as close to perfect reconstruction as possible, with "close to perfect" defined by the reconstruction quality function ${\displaystyle d}$d.

The simplest way to perform the copying task perfectly would be to duplicate the signal. To suppress this behavior, the code space ${\displaystyle {\mathcal {Z}}}$ usually has fewer dimensions than the message space ${\displaystyle {\mathcal {X}}}$.

Such an autoencoder is called undercomplete. It can be interpreted as compressing the message, or reducing its dimensionality.

![[Pasted image 20220729153240.png]]