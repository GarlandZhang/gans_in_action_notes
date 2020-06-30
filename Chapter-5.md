## Chapter 5. Training and common challenges: GANing for success

### Evaluation Metric

Cannot use maximum likelihood as evaluation metric (?) because it tends to overgeneralize. 

"Another way to think about overgeneralization is to start with a probability distribution of fake and real data (for example, images) and look at what the distance functions (a way to measure distance between real and fake images’ distributions) would do in cases where there should be zero probability mass. The additional loss due to these overgeneral samples could be tiny if they are not too different, for example, because these modes are close to real data in all but a few key problems such as multiple heads. An overgeneral metric would therefore allow creation of samples even when, according to the true data-generating process, there should not be any, such as a cow with multiple heads."

So where images would clearly be fake (a cow with multiple heads) is considered small loss in the evaluation, therefore, it would be regarded as plausible image.

"the two most commonly used and accepted metrics for statistically evaluating the quality of the generated samples: the inception score (IS) and Fréchet inception distance (FID)."

### Inception Score (IS)

"high-level wish list of what our ideal evaluation method would ensure:

The generated samples look like some real, distinguishable thing—for example, buckets or cows. The samples look real, and we can generate samples of items in our dataset. Moreover, our classifier is confident that what it sees is an item it recognizes. Luckily, we already have computer vision classifiers that are able to classify an image as belonging to a particular class, with certain confidence. Indeed, the score itself is named after the Inception network, which is one of those classifiers."
  * its realistic

"The generated samples are varied and contain, ideally, all the classes that were represented in the original dataset. This point is also highly desirable because our samples should be representative of the dataset we gave it; if our MNIST-generating GAN is always missing the number 8, we would not have a good generative model. We should have no interclass (between classes) mode collapse."
  * its diverse
  
  
recall: "KL divergence measures the difference between distributions"

Computing IS:
1. Take KL divergence between real and generated distribution
2. Exponentiate result of step 1

### Frechet Inception Distance (FID)

"The FID improves on the IS by making it more robust to noise and allowing the detection of intraclass (within class) sample omissions."

"the high-level idea is that we are looking for a generated distribution of samples that minimizes the number of modifications we have to make to ensure that the generated distribution looks like the distribution of the true data"

"The FID is calculated by running images through an Inception network. In practice, we compare the intermediate representations—feature maps or layers—rather than the final output (in other words, we embed them). More concretely, we evaluate the distance of the embedded means, the variances, and the covariances of the two distributions—the real and the generated one."


## Training Challenges

"Here is a list of the main problems:

* Mode collapse—In mode collapse, some of the modes (for example, classes) are not well represented in the generated samples. The mode collapses even though the real data distribution has support for the samples in this part of the distribution; for example, there will be no number 8 in the MNIST dataset. Note that mode collapse can happen even if the network has converged. We talked about interclass mode collapse during the explanation of the IS and intraclass mode collapse when discussing the FID.

* Slow convergence—This is a big problem with GANs and unsupervised settings, in which generally the speed of convergence and available compute are the main constraints—unlike with supervised learning, in which available labeled data is typically the first barrier. Moreover, some people believe that compute, not data, is going to be the determining factor in the AI race in the future. Plus, everyone wants fast models that do not take days to train.

* Overgeneralization—Here, we talk especially about cases in which modes (potential data samples) that should not have support (should not exist), do. For example, you might see a cow with multiple bodies but only one head, or vice versa. This happens when the GAN overgeneralizes and learns things that should not exist based on the real data."

Techniques to improve training process (as you would with any other ML algo):
* add network depth
    * recall this paper: https://arxiv.org/pdf/1710.10196.pdf where we progressively add layers in the Generator and Discriminator, after training on low resolution to stabilize, to increase resolution. This can be applied to any GAN since its independent of the GAN structure.
* change game setup
    * min-max design and stopping criteria
    
    ![cost fn of disc](https://i.gyazo.com/e243a5f65c77a485842a1956f75b6cdc.png)
    "This states that the Discriminator is trying to minimize the likelihood of mistaking a real sample for a fake one (first part) or a fake sample for a real one (the second part)."
    
    ![cost fn of gen](https://i.gyazo.com/f7807b24a118558ae210d1c4560649a5.png)
    Generator cost function is simply competing with Discriminator so just take negative.
    
    
    * non-saturating design and stopping criteria
    
    Apparently better than min max as it converges faster by not saturating gradients too early (like min max where gradients approx. 0 at early training). 
    
    * Wasserstein GAN (WGAN)
    
    Just leaving it here because its apparently even better than the prior 2 but is relatively new (and complex..).
    
* normalize input
  
  between -1 and 1.
  
  also use tanh activation function for generator's final output
* batch norm

  universally positive for using on Discriminator but controversial for Generator
  
* penalize gradient
  
  
* train discriminator more
  
  pretrain discriminator before generator (with CartoonGAN, its flipped). 

  5:1 ratio for number of discriminator weight updates to generator weight updates per training cycle

* avoid sparse gradients (aka vanishing gradient problem) 

  "Leaky ReLU—which is something like 0.1 × x for negative x, and 1 × x for x that’s at least 0—and average pooling to get around a lot of these problems. Other activation functions exist (such as sigmoid, ELU, and tanh), but people tend to use Leaky ReLU most commonly."
  
  Basically use Leaky ReLU instead of ReLU because you lose less info with it (the negative values in particular).
  
* changing to soft and noisy labels (?)
