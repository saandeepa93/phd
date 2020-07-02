## **Generating 3D Views of Facial Expressions From FrontalFace Video Based on Topographic Analysis**

### **Contribution**

* Generate 3D faces with arbitrary expression, given a series of frontal face 3D images with various expression.

### **Topographic representation of skin**

* Given a face image $f$, $f^\prime$ and $f^{\prime\prime}$ are calculated. From the $f^{\prime\prime}$, the hessian matrix $H$ is calculated.

* The eigen values of $H$, $\lambda_1$ and $\lambda_2$ along with the eigen vectors, $\omega_1$ and $\omega_2$ represent the extrema of $H$.

* The eigenvalues, eigenvectors and $f^\prime$ helps in classifying the face image into different topographic areas. For e.g., a pixel is labelled as peak, if the values in the pixel satisfied the following condition:

$$
\lambda_1 < 0\\
\lambda_2 < 0\\
f^\prime = 0
$$

### **3D modelling**

* A mesh model is created from the face image using the topographic classification described above.

* The displacement of each node to formulate a facial expression is treated by the

