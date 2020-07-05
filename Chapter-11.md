## Chapter 11. Practical applications of GANs

### GANs in medicine

because of patient privacy and complex domain knowledge of medical issues, data and experts are limited in medical field. Therefore the medical field is unable to benefit from advances in DL and AI

One way GANs help is via semi-supervised learning. Another is data augmentation used in computer vision tasks.

![data_aug](https://i.gyazo.com/1c0fa72a78179862c3e9e6bb7402d168.png)

However data aug is limited to original images. "In the case of medical diagnostics, we want different examples of the same underlying pathology. Enriching a dataset with synthetic examples, such as those produced by GANs, has the potential to further enrich the available data beyond traditional augmentation techniques."

**Hyperparameters (i.e. kernel size) are determined via trial and error**

### GANs in fashion

#### using gans to design fashion
"In 2017, Amazon earned another one, this time about the company’s ambition to develop an AI fashion designer by using no other technique than GANs."

"researchers from Adobe and the University of California, San Diego, published a paper in which they set out to accomplish the same goal.[10] Their approach can give us a hint about what goes on behind the secretive veil of Amazon’s AI research labs seeking to reinvent fashion. Using a dataset of hundreds of thousands of users, items, and reviews scraped from Amazon, lead author Wang-Cheng Kang and his collaborators trained two separate models: one that recommends fashion and the other that creates it."

"For our purposes, we can treat the recommendation model as a black box. The only thing we need to know about the model is what it does: for any person-item pair, it returns a preference score; the greater the score, the better match the item is for the person’s tastes. Nothing too unusual.

The latter model is a lot more novel and interesting—not only because it uses GANs, but also thanks to the two creative applications Kang and his colleagues devised:
  * Creating new fashion items matching the fashion taste of a given individual
  * Suggesting personalized alterations to existing items based on an individual’s fashion preferences."


#### methodology

Kang used CGAN with product's category as conditioning label. Six cateogries: "tops (men’s and women’s), bottoms (men’s and women’s), and shoes (men’s and women’s)."

"Recall that in chapter 8, we used MNIST labels to teach a CGAN to produce any handwritten digit we wanted. In a similar fashion (pun intended), Kang et al. use the category labels to train their CGAN to generate fashion items belonging to a specified category. Even though we are now dealing with shirts and pants instead of threes and fours, the CGAN model setup is almost identical to the one we implemented in chapter 8. The Generator uses random noise z and conditioning information (label/category c) to synthesize an image, and the Discriminator outputs a probability that a particular image-category pair is real rather than fake"

![arch](https://i.gyazo.com/7286b4198924d8e3d8f902e77a685f3a.png)

Link to paper about fashion recommender: https://arxiv.org/pdf/1711.02231.pdf

"This is hyperpersonalization at its finest. No wonder Amazon took notice."
