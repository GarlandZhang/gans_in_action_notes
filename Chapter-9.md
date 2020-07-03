## Chapter 9. CycleGAN

### cycle loss
"we simply complete the cycle: we translate from one domain to another and then back again. For example, we go from summer picture (domain A) of a park to a winter one (domain B) and then back again to summer (domain A). Now we have essentially created a cycle, and, ideally, the original picture (a) and the reconstructed picture () are the same. If they are not, we can measure their loss on a pixel level, thereby getting the first loss of our CycleGAN: cycle-consistency loss"

"To be able to use the cycle-consistency loss, we need to have two Generators: one translating from A to B, called GAB, sometimes referred to as simply G, and then another one translating from B to A, called GBA, referred to as F for brevity. There are technically two losses—forward cycle-consistency loss and backward cycle-consistency loss—but because all they mean is that 

![a[(https://i.gyazo.com/63adcb53f1c7e10b4327f692cedeabbf.png)

as well as , 

![b](https://i.gyazo.com/82c40f9739e9be6e5f283bf22e4a67c1.png)

you may think of these as essentially the same, but off by one."

### adversial loss

"In addition to the cycle-consistency loss, we still have the adversarial loss. Every translation with a Generator GAB has a corresponding Discriminator DB, and GBA has Discriminator DA. "

", because of the two losses, we have two Discriminators. We need to make sure that not only the translation from apple to orange looks real, but also that the translation from our estimated orange back to reconstructed apple looks real. Recall that the adversarial loss ensures that the images look real, and as a result, it is still key for the CycleGAN to work. Hence adversarial loss is presented as second. The first Discriminator in the cycle is especially important—otherwise, we’d simply get noise that would help the GAN memorize what it should reconstruct"



### identity loss

"The idea of identity loss is simple: we want to enforce that CycleGAN preserves the overall color structure (or temperature) of the picture. So we introduce a regularization term that helps us keep the tint of the picture consistent with the original image."

"This is done by feeding the images already in domain A to the Generator from B to A (GBA), because the CycleGAN should understand that they are already in the correct domain. In other words, we penalize unnecessary changes to the image: if we feed in a zebra and are trying to “zebrafy” an image, we get the same zebra back, as there is nothing to do.[3] Figure 9.3 illustrates the effects of identity loss"

![table_loss](https://i.gyazo.com/90b60e2027d206f0e9cb815d7de7a42e.png)


### architecture

"The CycleGAN setup builds directly on the CGAN architecture and is, in essence, two CGANs joined together—or, as the CycleGAN authors themselves point out, an autoencoder"

![arch](https://i.gyazo.com/e83047736e4ddec8048c2b05b2104573.png)

"think of the two mappings as two autoencoders: F(G(a)) and G(F(b))."

![arch](https://i.gyazo.com/fe2c6e140c9d768e449350247d3103cc.png)

