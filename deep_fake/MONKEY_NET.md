## **Monkey-Net for image animation**

### **Goal**:
1. Includes image animation for arbitrary objects.
2. Unsupervised learning of sparse motion-specific keypoints to model and transfer motion information.


### **Monkey-Net architecture**:
* **Keypoint Detector**:
  * *Input*: source image and frame of driving video.
  * *Output*: sparse keypoints

* **Dense motion prediction network**:
  * *Input*: output of Keypoint detector.
  * *Output*: heatmap representation.

* **Motion transfer network**:
  * *Input*: output of MTF and source image.
  * *Output*: target frame.

### **Keypoint detector**:

* The authors incorporate a UNET architecture for keypoint detection. Typically a Unet architecture requires training for image segmentation, but the authors use a typical encoder-decoder (or Hourglass) approach to obtain a series of heatmaps $H_k$.\
 Several heatmaps are obtained which are then run through a gaussian function of the form

$$
\forall p\in\mathcal{U}, H_k(p) = \frac{1}{\alpha} \mathcal{exp}(-(p-h_k)\Sigma_k^{-1}(p-h_k))
$$


$$
h_k = \sum_{p \in \mathcal{U}}H_k[p]p \\
\Sigma_k =\sum_{p \in \mathcal{U}} H_k[p] (p-h_k)(p-h_k)^T
$$


### **Points to note**

* The authors use bilinear interpolation to align the encoded features of the source image with the driving frame. Pytorch expects grid values in its bilinear implementation (grid_sample) to be in range [-1, 1]. The authors therefore squishes the range of grid coordinates to [-1, 1] in the beginning during keypoint detection.

* Interpolation methods are widely used in any image geometric transformation. The upsampling of hourglass architecture employs the bilinear interpolation which takes the weighted average of 4 nearest neghbours to determine the value of blank pixels after transformation.

* In Unet architecture, interpolate has been used to increase the size of the image and the unet concat technique has been used to concatenate the feature size.

### **Assumptions**

* Each identified keypoint corresponds to a location that is locally rigid in the image. This way, we can formulate a transformation/warping function to align the encoded features


