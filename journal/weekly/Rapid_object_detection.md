## Rapid Object Detection using a Boosted Cascade of Simple Features

### **Contributions**

1. New image representation called *Integral image*. This saves lot of computation time
in terms of calculating the sum within a block of image.

2. Usage of Adaboost to filter out regions of image which does not have useful information.

3. Cascade classifiers to increase the speed of the detector to pin-point important promising regions of the image.


## **Integral image representation**

The paper uses **rectangular features** in sets of $\{2, 3, 4\}$ rectangular blocks in image sub-window to calculate the difference b/w these blocks. Each block must be summed up and difference must be calculated with other blocks. This is a computationally expensive approach. The authors come up with something called **Integral image** representation which can be recursively calculated as:

$$
s(x, y) = s(x, y-1) + i(x, y)\\
ii(x, y) = ii(x-1, y) + s(x, y)
$$

where $s(x, y)$ is the cumulative sum of all pixels above and $ii(x, y)$ is the cumulative sum of all the pixels above and to the left. Integram image needs to be calculated only once in the entire image which avoids summing up the blocks everytime.

Using this representation, calculating the block sum is just a few array references.


## **Ada-boost classifiers**

Over all the training samples, there are over 180,000 features extracted from the rectangular features. The idea is to select only those features which contribute to the face detection and reject all others. To achieve this, an Ada-boost classifier algorithm is used.

## **Cascaded classifiers during testing**

To increase performance and reduce the computational time, the weak classifiers process the input in a cascaded manner such that only the candidate sub-window which are part of the face move to a deeper level of classifiers. To achieve this, the initial classifiers aggressively reject the sub-windows which it deems not to be part of the face. To ensure there are no false negatives in this process, the classifiers are fine tuned to achieve almost 0 false negative at the cost of 40% false positives.

