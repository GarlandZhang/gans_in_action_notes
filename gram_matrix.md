refer to article: https://towardsdatascience.com/neural-style-transfer-tutorial-part-1-f5cd3315fa7f

in style transfer, we want to retain content and style, hence we have content loss and style loss. 

With content loss, we can simply calculate the difference between the end image and the original image.

With style loss, however, we need to calculate the gram matrix. Gram matrix "is a way to find the correlation between these activations across different channels of the same layer".

In summary, for each layer we flatten the 3-D tensor into a 2-D tensor where each channel is now a 1-D row and the # of rows = # of filters. Then we multiply it by its transpose. The resulting equations (= a new 2-D matrix) illustrates a relationship across different channels

We then calculate the squared difference between the gram matrix of the style layer and the gram matrix of the generated layer, over all layers. Thus the style loss function.

