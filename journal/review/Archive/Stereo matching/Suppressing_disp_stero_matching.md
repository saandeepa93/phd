

### **Review**

Decision : **Weak reject/Neutral**\
Follow-up : **Yes**

In this paper, the authors estimate the disparity by taking into account the discontinouos property that may occur in two stereo images. The features that are extracted out of these disparity edges are assigned lower weights to exclude any noisy data from the features.

The authors have taken up an intuitive approach to add value to the PSMNet by incorporating their motivation. The detailed experiments and its results support the mentioned contributions.


### **Major concerns**


1. The composition of the paper could be much better. In many cases, especially in section III, the explanation is not clear which conflicts with what the authors are trying to say:\
Example:\
  *  Section III, inference 2\
    "*We call G and the area between ....does not exist corresponding points.*"


  * "*Researchers have studied the attention methods [20], [21], attention has been paid to the focus of attention and the way in which interests are expressed.*\"


2. Vague statements which require explanations or citations\

  * "*we have to set the range to max-disp because we can’t determine
the minimum range, although this may cause some problems.*"\
Expand on the kind of problems

  * "*people generally do not think that objects that don’t have spatial continuity are real object*."\
  Provide citations

  * "*Due to various factors of the actual situation, $\sum_i |\mathcal{x_i}^{'} - \mathcal{x_i}|$ does not
necessarily mean that there are some features contain disparity edge*"\
Provide citations or explain the factors


### **Minor concerns**

1. Contribution (ii) is not
2. How was the maxdisp value chosen?

