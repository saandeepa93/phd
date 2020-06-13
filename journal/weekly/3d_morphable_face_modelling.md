## **A morphable model for synthesis of 3d faces.**

### **Contributions**

* Identify the feature points of a given face and reconstruct the 3D face which are as real and natural as possible

### **Model representation**

* Each face is represented by its shape (or landmarks) $S = (X_1, Y_1, Z_1,...,X_n, Y_n, Z_n)^{T} \in \mathcal{R}^{3n}$ of $n$ vertices and by the texture or intensity values at these landmark locations, $T = (R_1, B_1, G_1,...R_n, B_n, G_n)^{T} \in \mathcal{R}^{3n}$.

* The new shapes $S_{model}$ and textures $T_{model}$ can be expressed in barycentric coordinates as the linear combination of shapes and textures

$$
S_{model} = \sum_{i=1}^{m}a_{i}S_{i}
$$

$$
T_{model} = \sum_{i=1}^{m}b_iT_i
$$

* Find the mean and convariance of shape and texture shape models as $\bar{S}$ and $\bar{T}$ and $C_s$ and $C_t$ respectively. Perform PCA for dimensionality reduction which ultimately performs basis transformation to orthogonal coordinate system

$$
S_{model} = \bar{S} + \sum_i^{m-1}\alpha_is_i\\
T_{model} = \bar{T} + \sum_i^{m-1}\beta_it_i
$$

where $\alpha_i$ and $\beta_i$ are unknown coefficients and $s_i$ and $t_i$ are the eigen vectors of the shape and texture respectively. The probability of $\alpha$ is given by

$$
p(\alpha) \sim e^{[-\frac{1}{2}\sum_i^{m-1}\frac{\alpha^2}{\sigma^2}]}
$$

where $\sigma$ defines the eigen values of the covariance matrix. The same formulation applies to $p(\beta)$


### **Representing facial attributes in parametric models**

#### **Facial expression**
* Facial expression can be imposed on a neutral face by adding the differences $\Delta S = S_{expression} - S_{neutral}$ and $\Delta T = T_{expression} - T_{neutral}$. Pairs of faces containing expression and neutral images are taken and their differences are added to a new neutral face

#### **Gender, Eyebrow, Darkness**

* The authors take the weighted sum of all the $S_i - \bar{S}$ and $T_i - \bar{T}$ with the $\mu_i$ as coefficient for each. Each $\mu_i$ represents the markedness of the attribute(???). The weighted sum is given by

$$
\Delta S = \sum_{i=1}^{m} \mu_i (S_i - \bar{S})\\
\Delta T = \sum_{i=1}^{m} \mu_i (T_i - \bar{T})\\
$$

* Multiples of ($\Delta S, \Delta T$) are added or subtracted from the faces to generate more facial features.

#### **Distinctiveness**

* "Distinctiveness" refers to the carricature like features of the face. The authors simply multiply the coefficients $\alpha\;and\;\beta$ with a scale value to achieve this.

### 3D to 2D correspondence

###


### **Takeaways**

* Reconstruction before GANs were present.
* Every minute detail were taken care of, but cannot be widely used at the time.
* Needed more generalization ability.
* Lots of training data with (expression, neutral) values


### **Note**

### *Barycentric coordinates* : For any figure S in the affine space A, there is a point $p$ in A such that
$$
(a_1 + a_2+ ...+a_n )p = a_1x_1 + a_2x_2 +....+ a_nx_n
$$

if $(a_1 + a_2+ ...+a_n ) = 1$, then p is called the barycentric coordinates of A