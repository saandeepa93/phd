## **Learning Ensembles from Bites:A Scalable and Accurate Approach**

### **Contributions**

1. The authors have proposed that disjoint dataset partition will achieve faster and accurate results with pasting $Rvote$ and $Ivote$ an this is called $DRvote$ and $DIvote$.


### **Ivote and Rvote**

1. The idea is to build classifiers on subset of dataset to avoid computational heavy training. Each classifier has its own dataset. The only difference is in testing which is either by Random sampling (Rvote) or Importance sampling(Ivote). The Ivote is more successfull than Rvote because it focuses more on the set which is likely to be misclassified.

1. In Ivote, each classifier has its own training set and any testing data is retrieved from the dataset of different classifier to improve the generalization ability of the classifier. This is similar to boosting but here, the "bites" are much smaller than the size of original dataset

2. Ivotes have 3 disadvantages:
  i. It samples the training set in ditributed environment and may require concurrent disk access.
  ii. Sequential data access to avoid multiple disk access has shown to degrade the performance of Ivote.
  iii. The memory requirement of Ivote is pretty high $\sim$ 1GB.


### **Pasting DIvote and DRvote**

