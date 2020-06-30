
## batch normalization 
"normalizes the inputs to each layer, for each training mini-batch as it flows through the network."

"Normalization is the scaling of data so that it has zero mean and unit variance. This is accomplished by taking each data point x, subtracting the mean μ, and dividing the result by the standard deviation, σ"

we pass:
![batch norm form](https://i.gyazo.com/13320c966cb2a1588f57078ad319d8e1.png)

as input to the next layer where x^ is:

![norm form](https://i.gyazo.com/fc4cf1fd87de0ea00821ba8e4d10d40d.png)

"the terms γ and β are trainable parameters, which—just like weights and biases—are tuned during network training."

"Batch normalization limits the amount by which updating the parameters in the previous layers can affect the distribution of inputs received by the current layer. This decreases any unwanted interdependence between parameters across layers, which helps speed up the network training process and increase its robustness, especially when it comes to network parameter initialization."
