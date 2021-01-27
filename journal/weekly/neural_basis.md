# **Neural basis for AU recognition**

## **1. Posits**
* Most of the facial muscle movement is found in the pSTS region of the brain.

## **2. Across subject testing**
* The experimentation enabled studies with multiple subjects by something called voxels. Each [voxel](https://cfn.upenn.edu/stslab/wiki/lib/exe/fetch.php/fmri_club:preprocess1:smith_2004_brjrad.pdf) is a unit volume of brain. Each neural activity of the subject consists of linear combination of $\textit{d}$ voxels. For any neural activity, the multivoxel analysis identified $\textit{p}$ voxels and the comparison is done via least square method.

* Discovery-search analysis method reveals the most discriminant part of the brain responsible for muscle movement which was again found to be pSTS.

## **3. Experimental setup**
* 12 runs. Each run had 14 blocks.
* In each block, 6 images of total 8 expression categories were displayed for 1.5 seconds with 0.5 seconds gap in each.
* Subjects saw a total of 168 blocks

## **4. Multi-voxel pattern analysis**
* For each subject, each block had $\textit{d}$ dimensional data where d refers to total voxels of the subject. This data is given by $x \in \mathcal{R}^{d}$
* Subject undergoes through 168 blocks. So this is given by $X = (x_0, x_1, x_2....., x_{168})$. 
* PCA was applied to select the top 95% of data. These PCAs were combined to a single PCA data.
* LDA classifier was applied to each of the 4 AUs which detect 4 hyperplanes to separate the AUs present vs not present.

## **5. Why PCA?**
* For across subject, all the brain data could have been mapped to a single brain space called MNI. This still does not guarantee shared variance as the voxel mapping may be different for different subject. 
* Hence, our idea is to find the maximum shared variance across the subjects' neural activity.

## **6. Performed downsampling**
* Downsampling is performed while carefully maintaining the data balance across different expressions to avoid bias in the classifier. Each downsampling resulted in slightly different LDA classifier and overall accuracies were averaged.

## **7. Result**
* Algorithm could not detect emotions.



