

### **Review**

Decision : **Weak accept/Neutral**\
Follow-up : **No**

In this paper, the authors propose a new pre-training strategy for object detection model by synthesizing classification data for a particular class which results in reduced label requirement for detection.
The authors make use of unsupervised segmentation technique to segment out the object from classification dataset images and generate the fake ones of the same class which are then blended with random background.


1. The authors incorporate the self supervised technique into a difficult problem of object detection.
2. The authors describe their method in a concise manner and provide detailed experiments and ablation study to validate their hypothesis.
3. The authors clearly present the advantages and limitations of their work through their experiments.


## *Suggestions/improvments*
1. Fig 1 could have been more detailed in terms of input to ReDO. The paper states both real and fake images are gathered but architecture shows only fake images.
2. The need for unsupervised segmentation vs supervised is unclear. Any of the pretrained SOTA detection model such as detectron2 would perform similar tasks in much more accurate fashion without using them directly in your object detection model.
3. FID score can be calculated to measure the performance of synthesized object images before feeding them into object detection model.

