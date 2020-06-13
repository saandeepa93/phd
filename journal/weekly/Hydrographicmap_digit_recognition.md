## **Recognition of Digits in Hydrographic Maps: Binary Versus Topographic Analysis**


### **Contributions**

* Comparitive study of digit recognition in hydrographic maps between Binary and Topological analysis


### **Binary Analaysis**

1. **Niblack's Locally adaptive thresholding**:
Calcutates the pixel-wise thresholding of a grayscale image. The threshold is calculated as:

$$
T_{Niblack} = m + k \sqrt{\frac{\sum p_i^{2}}{NP} - m^{2}}
$$

where $m$ is the average value of pixel $p_i$, $k$ is a constant -0.2, $NP$ is the total number of pixels.

The thresholded image is post-processed using Yanowitz and Bruckstein method. These are a good method of thresholding for maps but produce lot of noise.

2. **Segmentation of connected symbol candidates**

Approach taken is to locate the candidate split lines in the connected symbol candidates. The classes are predicted for the symbols to the left and right of each split line candidates using bayesian approach.

3. **Segmentation of long lines**

Long contour lines which overlap or connect the symbols are removed by thinning the binary image using Lee and Chen's method. The image is then traversed to locate the line segments which do not interect anywhere. The operation is applied on both thinned image and the binary image.

4. **Symbol Recognition**

16 size and orientation independent elliptic fourier descriptors are used as features in the statistical quadratic classifier. Similar classifier is used for topographic images.

### **Topographic analysis**

1. **Topographic labels**
The first step is to convert the image to topographic labels. Ridge, hill convex hill are assigned the label print objects while the ravine saddle, concave hills are assigned the labels background object.

2. **Binary image**
Here, the binary images are derived by splitting the graysacle image based on the print object and background object.


