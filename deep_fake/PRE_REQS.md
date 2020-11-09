## Preparation

1. Go through the data. Find what is missing.
2. Major requirement is generating non-face deep fake data. Do a literature survey.
3. 


## **Optical flow basics**

Let the intensity of an image pixel at location $(x, y)$ at time $t$ be given by $\mathcal{I}(x, y, t)$. The velocity of image pixel $m$ is given by

$$
\mathbf{v_m} = \dot{\mathbf{m}} = [v_x, v_y]^{T} = [\frac{dx}{dt}, \frac{dy}{dt}]
$$

Assuming the intensity of the image pixel remains same after time $dt$,

$$
\mathcal{I}(x+v_xdt, y + v_ydt, t+dt) = \mathcal{I}(x, y, t)
$$

Expanding the above equation using taylor's series

$$
\mathcal{I}(x, y, t) + \frac{dI}{dx}v_xdt + \frac{dI}{dy}v_ydt + \frac{dI}{dt}dt = \mathcal{I}(x, y, t)
$$

$$
dt(\frac{dI}{dx}v_x + \frac{dI}{dy}v_y + \frac{dI}{dt}) = 0
$$

$$
\nabla{I}. \mathbf{v_m} = -\frac{dI}{dt}
$$

Here, $\nabla{I}$ is the image gradient in $x$ and $y$ direction and can be calculated. $\frac{dI}{dt}$ can also be calculated (donno how). There are 2 unknowns to be calculated from one equation which are: $v_x$ and $v_y$. This is known as the $\textit{aperture problem}$.
