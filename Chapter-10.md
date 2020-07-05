## Chapter 10. Adversarial examples

big problem with GANs is a little bit of noise drastically changes predictions. 

**see adversarial_examples.ipynb for resnet prediction on original vs adversarial**

we discover that it predicts very differently after applying a bit of noise to the image, even though to the human eye they look identical. This is an adversarial example.

"Adversarial examples are inputs to machine learning models that an attacker has intentionally designed to cause the model to make a mistake; they're like optical illusions for machines"

Resnet is the most robust model against adversarial examples so far.
  * "we do not get a confident classification as a wrong class in most cases on just naively sampled noise". e.g.; gaussian noise.
  * "projected gradient descent (PGD) attack, [...] Unlike with the previous attacks, we are now taking a step regardless of where it may lead us—even “invalid” pixel values—and then projecting back onto the feasible space."
  
  ![pgd](https://i.gyazo.com/6cf17d6d246e4464f657173f5e9cc203.png)
  
  
