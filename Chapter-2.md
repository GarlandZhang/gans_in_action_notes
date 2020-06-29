"The latent space is the hidden representation of the data. Rather than expressing words or images (for example, machine learning engineer in our example, or JPEG codec for images) in their uncompressed versions, an autoencoder compresses and clusters them based on its understanding of the data."

For example, we pass a 100-input vector to the generator to produce fake images.

![autoencoder](https://dpzbhybb2pdcj.cloudfront.net/langr/Figures/02fig02_alt.jpg)

After encoding an image, we get a sample in latent space. This is then decoded to get a similar output to x*. When we create a noise vector to pass to a generator, the noise will be similar to some encoding of an actual image, so we decode to a similar image.

Autoencoder training algo:

1. We take images x and feed them through the autoencoder.
2. We get out x*, reconstruction of the images.
3. We measure the reconstruction loss—the difference between x and x*.
   * This is done using a distance (for example, mean average error) between the pixels of x and x*.
   * This gives us an explicit objective function (|| x –x* ||) to optimize via a version of gradient descent.
   
"An autoencoder is composed of two neural networks: an encoder and a decoder. In our case, both have activation functions,[5] and we will be using just one intermediate layer for each. This means we have two weight matrices in each network—one from input to intermediate and then one from intermediate to latent."

