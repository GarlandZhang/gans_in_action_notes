## Chapter 10. Adversarial examples

big problem with GANs is a little bit of noise drastically changes predictions. 

**see adversarial_examples.ipynb for resnet prediction on original vs adversarial**

we discover that it predicts very differently after applying a bit of noise to the image, even though to the human eye they look identical. This is an adversarial example.

"Adversarial examples are inputs to machine learning models that an attacker has intentionally designed to cause the model to make a mistake; they're like optical illusions for machines"

Resnet is the most robust model against adversarial examples so far.
  * "we do not get a confident classification as a wrong class in most cases on just naively sampled noise". e.g.; gaussian noise.
  * "projected gradient descent (PGD) attack, [...] Unlike with the previous attacks, we are now taking a step regardless of where it may lead us—even “invalid” pixel values—and then projecting back onto the feasible space." Wheras in ordinary gradient descent, we modify the weights without constraint, here we modify the weights with some constraint on their values.
  
  ![pgd](https://i.gyazo.com/6cf17d6d246e4464f657173f5e9cc203.png)
  
  
### security implications of adversarial examples

"Some people give the example of self-driving cars and adversarially perturbing stop signs. But if we can do that, why wouldn’t the attackers completely spray-paint over the stop signs or simply physically obscure the stop sign with a high speed-limit sign for a little while? Because these “traditional attacks,” unlike adversarial examples, will work 100% of the time, whereas an adversarial attack works only when it transfers well and manages to not get distorted by the preprocessing."

"This does not mean that when you have a mission-critical ML application, you can just ignore this problem. However, it most cases, adversarial attacks require far more effort than more commonplace vectors of attack, so bearing that in mind is worthwhile."

"as with most security implications, adversarial attacks also have adversarial defenses that attempt to defend against the many types of attacks [...] adversarial defenses are an ever-evolving game, in which many good defenses are available against some types of attacks, but not all. The turnaround can be so quick that just three days after the submission deadline for ICLR 2018, seven of the eight proposed and examined defenses were broken"

### relation to gans

"a way to think of GANs is almost as ML-in-the-loop adversarial examples that eventually come up with images."

### example of adversial defense

"In the Robust Manifold Defense, we take the following steps to defend against the adversarial examples:[9]

1. We take an image x (adversarial or regular) and
   * Project it back to the latent space z.
   * Use the generator G to generate a similar example to x, called x* by G(z).
2. We use the classifier C to classify this example C(x*), which generally already tends to misclassify way less than running the classification directly on x.

However, the authors of this defense find out that there are still some ambiguous cases in which the classifier does get fooled by minor perturbations. Still, we encourage you to check out their paper, as these cases tend to be unclear to humans as well, which is a sign of a robust model. To fix this, we apply adversarial training on the manifold: we get some of these adversarial cases into the training set so the classifier learns to distinguish those from the real training data."

