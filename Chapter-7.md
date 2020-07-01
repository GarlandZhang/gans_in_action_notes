## Chapter 7. Semi-Supervised GAN

"Unlike supervised learning, in which we need a label for every example in our dataset, and unsupervised learning, in which no labels are used, semi-supervised learning has a class label for only a small subset of the training dataset. By internalizing hidden structures in the data, semi-supervised learning strives to generalize from the small subset of labeled data points to effectively classify new, previously unseen examples. Importantly, for semi-supervised learning to work, the labeled and unlabeled data must come from the same underlying distribution."

"By internalizing hidden structures in the data, semi-supervised learning strives to generalize from the small subset of labeled data points to effectively classify new, previously unseen examples. Importantly, for semi-supervised learning to work, the labeled and unlabeled data must come from the same underlying distribution."

### Definition of Semi-Supervised GAN
"Semi-Supervised GAN (SGAN) is a Generative Adversarial Network whose Discriminator is a multiclass classifier. Instead of distinguishing between only two classes (real and fake), it learns to distinguish between N + 1 classes, where N is the number of classes in the training dataset, with one added for the fake examples produced by the Generator."

![semi-supervised arch](https://i.gyazo.com/1b9e78eb4c72e4e5b19d45893ee98a77.png)
