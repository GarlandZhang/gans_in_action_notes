## Chapter 8. Conditional GAN

" the Conditional GAN (CGAN) uses labels to train both the Generator and the Discriminator. [...] A Conditional GAN allows us to direct the Generator to synthesize the kind of fake examples we want."

"although we could control the domain of examples our GAN learned to emulate by our selection of the training dataset, **we could not specify any of the characteristics of the data samples the GAN would generate**. For instance, the DCGAN we implemented in chapter 4 could synthesize realistic-looking handwritten digits, but **we could not control whether it would produce, say, the number 7 rather than the number 9 at any given time**."

"During CGAN training, the Generator learns to produce realistic examples for each label in the training dataset, and the Discriminator learns to distinguish fake example-label pairs from real example-label pairs. In contrast to the Semi-Supervised GAN from the previous chapter, whose Discriminator learns to assign the correct label to each real example (in addition to distinguishing real examples from fake ones), the Discriminator in a CGAN does not learn to identify which class is which. It learns only to accept real, matching pairs while rejecting pairs that are mismatched and pairs in which the example is fake."

"Accordingly, in order to fool the Discriminator, it is not enough for the CGAN Generator to produce realistic-looking data. The examples it generates also need to match their labels. After the Generator is fully trained, this then allows us to specify what example we want the CGAN to synthesize by passing it the desired label."

![cgan_gen_diagram](https://i.gyazo.com/1ca8afb7ee9b2e82aaaca1fd1fda4589.png)

![cgan_disc_diagram](https://i.gyazo.com/33ee0ebf78f2e1691107d39e0f0e31d9.png)

### Architecture

![arch_diagram](https://i.gyazo.com/3411191902ec95431c8004964be10ac5.png)

### Implementation

#### generator
" we use embedding and element-wise multiplication to combine the random noise vector z and the label y into a joint representation"

![impl_gen](https://i.gyazo.com/ccd08f5659144dcd2b19ed95949dd6dd.png)

#### discriminator

![impl_disc](https://i.gyazo.com/3fd670020c9f3930ac01fa4c1a4f63d0.png)

