## Chapter 7. Semi-Supervised GAN

"Unlike supervised learning, in which we need a label for every example in our dataset, and unsupervised learning, in which no labels are used, semi-supervised learning has a class label for only a small subset of the training dataset. By internalizing hidden structures in the data, semi-supervised learning strives to generalize from the small subset of labeled data points to effectively classify new, previously unseen examples. Importantly, for semi-supervised learning to work, the labeled and unlabeled data must come from the same underlying distribution."

"By internalizing hidden structures in the data, semi-supervised learning strives to generalize from the small subset of labeled data points to effectively classify new, previously unseen examples. Importantly, for semi-supervised learning to work, the labeled and unlabeled data must come from the same underlying distribution."

### Definition of Semi-Supervised GAN
"Semi-Supervised GAN (SGAN) is a Generative Adversarial Network whose Discriminator is a multiclass classifier. Instead of distinguishing between only two classes (real and fake), it learns to distinguish between N + 1 classes, where N is the number of classes in the training dataset, with one added for the fake examples produced by the Generator."

![semi-supervised arch](https://i.gyazo.com/1b9e78eb4c72e4e5b19d45893ee98a77.png)

"The SGAN Discriminator, however, diverges considerably from the original GAN implementation. Instead of two, it receives three kinds of inputs: fake examples produced by the Generator (x*), real examples without labels from the training dataset (x), and real examples with labels from the training dataset (x, y), where y denotes the label for the given example x"
  * generator is unchanged but discriminator now has an extra task which is to classify the digit (if its not fake)
  * in GAN, we use Discriminator to make Generator better. In SGAN, we goal is to make semi-supervised classifier (discriminator) as accurate as fully supervised classifier
  
### Training objective of SGAN
"The Generator’s goal is to aid this process by serving as a source of additional information (the fake data it produces) that helps the Generator learn the relevant patterns in the data, enhancing its classification accuracy. At the end of the training, the Generator gets discarded, and we use the trained Discriminator as a classifier."
  
  
![sgan_arch](https://i.gyazo.com/d5f69f8f00aaf0b2963ff66052197c11.png)

### SGAN training algorithm
For each training iteration do

1. Train the Discriminator (supervised):
 * Take a random mini-batch of labeled real examples (x, y).
 * Compute D((x, y)) for the given mini-batch and backpropagate the multiclass classification loss to update θ(D) to minimize the loss.
2. Train the Discriminator (unsupervised):
 * Take a random mini-batch of unlabeled real examples x.
 * Compute D(x) for the given mini-batch and backpropagate the binary classification loss to update θ(D) to minimize the loss.
 * Take a mini-batch of random noise vectors z and generate a mini-batch of fake examples: G(z) = x*.
 * Compute D(x*) for the given mini-batch and backpropagate the binary classification loss to update θ(D) to minimize the loss.
3. Train the Generator:
 * Take a mini-batch of random noise vectors z and generate a mini-batch of fake examples: G(z) = x*.
 * Compute D(x*) for the given mini-batch and backpropagate the binary classification loss to update θ(G) to maximize the loss.
End for

we use unsupervised discriminator because its only for real/fake classification whereas supervised is for classifying actual class. we freeze unsupervised weights in gan model to train the generator. gan model is independent of supervised discriminator, but we have it because thats the end goal of sgan!!
