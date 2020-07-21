
## Segmentation Types

see: https://engineering.matterport.com/splash-of-color-instance-segmentation-with-mask-r-cnn-and-tensorflow-7c761e238b46

balloon analogy
- Classification: There is a balloon in this image
- Semantic Segmentation: These are all the balloon pixels.
- Object Detection: There are 7 balloons in this image at these locations. We’re starting to account for objects that overlap.
- Instance Segmentation: There are 7 balloons at these locations, and these are the pixels that belong to each one.

![balloons](https://miro.medium.com/max/500/1*-zw_Mh1e-8YncnokbAFWxg.png)

"At a high level, Mask R-CNN consists of these modules:"

1. Backbone
"Mask R-CNN (regional convolutional neural network) is a two stage framework: the first stage scans the image and generates proposals(areas likely to contain an object). And the second stage classifies the proposals and generates bounding boxes and masks."

"This is a standard convolutional neural network (typically, ResNet50 or ResNet101) that serves as a feature extractor. The early layers detect low level features (edges and corners), and later layers successively detect higher level features (car, person, sky)."

**improvement**

"FPN improves the standard feature extraction pyramid by adding a second pyramid that takes the high level features from the first pyramid and passes them down to lower layers. By doing so, it allows features at every level to have access to both, lower and higher level features."

![fpn_pyramid](https://miro.medium.com/max/452/1*1sCveJrqfthOQsGGZRs2tQ.png)


2. Region Proposal Network (RPN)

"RPN is a lightweight neural network that scans the image in a sliding-window fashion and finds areas that contain objects." "The regions that the RPN scans over are called anchors. Which are boxes distributed over the image area [...] In practice, there are about 200K anchors of different sizes and aspect ratios, and they overlap to cover as much of the image as possible."

![rpn](https://miro.medium.com/max/500/1*ESpJx0XLvyBa86TNo2BfLQ.png)

note: The RPN scans over the backbone feature map, not the image... but for reference we demonstrate on the image.

The RPN generates two outputs for each anchor:
  1. Anchor Class: One of two classes: foreground or background. The FG class implies that there is likely an object in that box.
  2. Bounding Box Refinement: A foreground anchor (also called positive anchor) might not be centered perfectly over the object. So the RPN estimates a delta (% change in x, y, width, height) to refine the anchor box to fit the object better.
  
"Using the RPN predictions, we pick the top anchors that are likely to contain objects and refine their location and size. If several anchors overlap too much, we keep the one with the highest foreground score and discard the rest (referred to as Non-max Suppression). After that we have the final proposals (regions of interest) that we pass to the next stage"

3. ROI Classifier & Bounding Box Regressor

runs on the regions of interest (ROIs) proposed by the RPN. And just like the RPN, it generates two outputs for each ROI:

  1. Class: The class of the object in the ROI... has the capacity to classify regions to specific classes (person, car, chair, …etc.). It can also generate a background class, which causes the ROI to be discarded.
  2. Bounding Box Refinement: Very similar to how it’s done in the RPN, and its purpose is to further refine the location and size of the bounding box to encapsulate the object.
  
ROI Pooling
  - to handle variable size input for each ROI, crop and resize to fixed size
  
  
4. Segmentation Masks (steps 1-3 gives Faster R-CNN; steps 1-4 gives Mask-RCNN)
"The mask branch is a convolutional network that takes the positive regions selected by the ROI classifier and generates masks for them"

