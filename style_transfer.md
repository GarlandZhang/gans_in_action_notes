
## neural style transfer

- uses pretrained VGG19 network to get the relevant feature maps. Applies gradient to image and not to any model

## fast neural style transfer

- identical loss function but instead applies to a feed forward network. see **https://towardsdatascience.com/towards-fast-neural-style-transfer-191012b86284** for more detail.

- apparently is not as good as neural style transfer and is limited to the styles it was trained on
