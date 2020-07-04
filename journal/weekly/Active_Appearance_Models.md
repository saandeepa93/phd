## **Active appearance models**

### **Contributions**
* Statistical model for matching the shape and texture model to a new face. Similar to landmark alignent problem.

### **Training phase**

* For each face in the training phase, we extract the shape parameters $b$. This is done my representing each face as transformation of the mean shape

$$
  x = \bar{x} + P_sb_s
$$

where $x$ is the training image, $\bar{x}$ is the mean shape, $P$ is the first t eigenvectors of the covariance matrix of the training set. Here, since the eigen vectors are linearly independent, we can reform the above to equation to claculate the shape parameters, $b$,

$$
b = P^T(x - \bar{x})
$$

### **Building the model**
* Given all the set of $b$ and different class segregation within the training sample as identity and illumination etc., we try to find which $b$ best describes the identity class by calculating the mahalonobis distance for each $b_i$ for class $i$.

$$
d_m(b, b_i) = (b - b_i)C^{-1}(b - b_i)
$$

$C$ is the class covariance matrix.

* Now, each face of the training sample are warped down to the mean shape using a triangulation algorithm and then the gray-scale information is sampled from this shape-free patch using

$$
g = \bar{g} + P_gb_g
$$

* The above sampled gray-scale information are normalized using a scale $\alpha$ and an offset $\beta$ to make it invariant of external factors.
* To remove the correlation between $b_s$ and $b_g$, PCA is performed on the shape and appearance parameters on the concatenated vectors

$$
b = (W_sb_s, b_g) = [W_s P_s^T(x - \bar{x}), P_g^T(g - \bar{g})]
$$

$W_s$ identifies the correlation between $b_s$ and $b_g$, since one is in location unit and other is in gray level, we need to find the relationship between the two.

* Finally, PCA is applied on $b$ again to obtain
$$
b = Qc
$$

where $Q$ is the eigen vector and $c$ is the appearance parameter controlling both shape and gray-levels.

###

### **Weakness during the time**
* 50-100 parameters were too much.
* Lack of training data.
