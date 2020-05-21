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

### **Architecture Overview**:

*
