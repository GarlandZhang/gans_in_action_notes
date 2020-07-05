## Chapter 12. Looking ahead

### Ethics

GANs have potential to be misused. One example is writing fake news.

"AI ethics is a real problem already, and we have presented three real problems here—AI-generated fake news, synthesized political proclamations, and involuntary pornography. But many more problems exist, such as Amazon using an AI-hiring tool showing negative bias against women"

### Gan innovations
"three GAN innovations that all have an interesting practical application: either a practical paper (RGAN), GitHub project (SAGAN), or artistic application (BigGAN)."

### Relativistic GAN

"The core idea of the RGAN is that in addition to the original GAN (specifically, the NS-GAN that you may recall from chapter 5), we add an extra term to the Generator—forcing it to make the generated data seem more real than the real data."

#[loss](https://i.gyazo.com/585ce69c6bb9e317d2cf4d956d509853.png)

  * this is not a 1 to 1 pairing for the real and synthetic images. this is just how loss is calculated for x, z in all elements in the domain, latent space respecitvely.
  
"The innovation of the RGAN is that we no longer get the previous unhelpful dynamic of the Generator always playing catch-up. In other words, the Generator is trying to generate data that looks more realistic than the real data so that it is not always on the defensive. As a result, D(x) can be interpreted as the probability that the real data is more realistic than the generated data."

#[improved_loss_fn](https://i.gyazo.com/1f19f7dc0de81625a5ec3055f1e76db0.png)

where "C(x) acts as a critic similar to a WGAN setup, and you may think of it as a Discriminator. Furthermore, a() is defined as log(sigmoid())." G(z) is fake samples, x is real samples.

"we see only one key difference in the Generator: the real data now adds into the loss function. "

Bottom line, this architecture shows the generator is not always playing "catch up" to be a better generator but stays ahead. The main benefit is "this simple addition makes the training significantly more stable at a little extra computational cost." Other archs come with huge comp. cost but this minimizes.

### Self-attention GAN

"Self-Attention GAN (SAGAN). Attention is based on a very human idea of how we look at the world—through small patches of focus at a time.[8] A GAN’s attention works similarly: your mind is consciously able to focus on only a small part of, say, a table, but your brain is able to stitch the whole table together through quick, minor eye movements called saccades while still focusing on only a subset of the image at a time."

![convs_limit](https://i.gyazo.com/b83f08a0f8efbf303154583787c37497.png)
  * so in a 2x2 convolution, we ignore a lot of info. for each square in the 2x2, we only capture (3x3=) 9 pixels with that kernel value of the 4x4 picture. 
  * "Recall that this is especially a problem when our images are, say, 512 × 512, but the largest commonly used convolution sizes are 7, so that is loads of ignored features
  
#### application

"DeOldify (https://github.com/jantic/DeOldify) is one of the popular applications of the SAGAN that was made by Jason Antic, a student of Jeremy Howard’s fast.ai course. DeOldify uses the SAGAN to colorize old images and drawings to an amazing level of accuracy. As you can see in figure 12.4, you can turn famous historic photographs and paintings into fully colorized versions."

### BigGAN

"BigGAN has achieved highly realistic 512 × 512 images on all 1,000 classes of ImageNet—a feat previously deemed almost impossible with the current generation of GANs."

**Read more about it on own time**

#### application

"One fascinating artistic application of BigGAN is the Ganbreeder app, which was made possible thanks to the pretrained models and Joel Simon’s hard work. Ganbreeder is an interactive web-based (free!) way to explore the latent space of BigGAN. It has been used in numerous artistic applications as a way to come up with new images. [...] You can either explore the adjacent latent space or use a linear interpolation between two samples of the two images to create new images. Figure 12.5 shows an example of creating Ganbreeder offspring."

"BigGAN is further notable because DeepMind has given us all this compute for free and uploaded pretrained models onto TensorFlow Hub"
