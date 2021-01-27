# Random notes

## 1. *Smooth vs continuous functions*

A function $f$ is said to be continuous if it is not discrete, i.e., $f$ is
differentiable in a defined interval.

A function $f$ is said to be $C^k$ smooth if $f$ has the $k$th order
differential.

## 2. *Kullback-Leibler divergence ($KL$)*
Given 2 probability distributions $P$ and $Q$, the KL divergence is given by
$$
KL(P||Q) = \sum_{x \in X}P(x)log(\frac{P(x)}{Q(x)})
$$
In context of machine learning, $KL(P||Q)$ is the information gain if $P$ is used
instead of $Q$


## 3. *Jensen-Shannon divergence ($JSD$)*

Given two probability distribution functions, $P$ and $Q$, the Jensen-Shannon
divergence is given by

$$
JSD(P\Vert{Q}) = \frac{1}{2}KL(P\Vert{M}) + \frac{1}{2}KL(Q\Vert{M})
$$

where $M = \frac{P + Q}{2}$.

## 4. *Differential Evolution*
Differential Evolution is an optimization technique to iteratively improve the
candidate solutions. This does not require any gradient information i.e. does not require the function to be differentiable (just like SDM).

## 5. *Intractable density functions*
This can be explained using the problem formulation of variational auto-encoders. Suppose, we want to maximize the likelihood of an image x, then it is given by,
$$
  p(x) = \int p_{\theta}(z)p_{\theta}(x|z)dz
$$

where $z$ denotes the latent representation of the image $x$. $z$ is an infinite
space, hence marginal integration above makes it intractable. Read [this](http://akosiorek.github.io/ml/2018/03/14/what_is_wrong_with_vaes.html) and to understand why $p(z|x)$ is intractable, Read [this](https://medium.com/retina-ai-health-inc/variational-inference-derivation-of-the-variational-autoencoder-vae-loss-function-a-true-story-3543a3dc67ee) for more details.

Basically, according to Bayes' theorem:
$$
p_\theta(z|x) = \frac{p_\theta(x|z) p_\theta(z)}{p_\theta(x)}
$$

To get the denominator term $p_\theta(x)$, we use the joint probability formula for continuous variables.
$$
\begin{aligned}
p_\theta(x) &= \int p_\theta(x, z)dz\\
            &=\int p_\theta(x|z) p_\theta(z) dz
\end{aligned}
$$

As the dimension of $z$ increases, calculating integrals becomes more and more complex and any dimension $d$ of $z \geq 4$ is impossible to calculate. That is the reason the normalizing term followed by the posterior distribution becomes $\textbf{intractable}$ to compute.

## 6. *Derivation of Loss of VAEs*
VAEs are defined by an encoder-deccoder approach to generate arbitrary images. They are based on maximizing the likelihood of the generated images. Let $p_\theta(x)$ be the likelihood of the image, then

$$
p_\theta(x) = \int p_\theta(x|z)p_\theta(z)\\
$$

The loss function is calculated using log since we are dealing with intractable functions which gives out large values

$$
\begin{aligned}
\log p_\theta(x) &= E_{z \sim q(z|x)}[\log(p_\theta(x))]\\
                 &= E_{z \sim q(z|x)}[\log \frac{p(x|z)p(z)}{p(z|x)}]\\
\end{aligned}
$$
multiplying by the decoder function $q(z|x)$

$$
\begin{aligned}
                 \log p_\theta(x) &= E_z[\log(\frac{p(x|z)p(z)}{p(z|x)})(\frac{
                   q(z|x)}{q(z|x)})]\\
\end{aligned}
$$
Using log properties
$$
\begin{aligned}
  \log p_\theta(x) &= E_z[\log p(x|z) + \log(\frac{p(z)}{q(z|x)}) + \log(\frac{q(z|x)}{p(z|x)})]\\
  &= E_z[\log p(x|z) - \log (\frac{q(z|x)}{p(z)}) + \log(\frac{q(z|x)}{p(z|x)})]\\
  &= E_z[\log p(x|z)] - KL(q(z|x)||p(z)) + \log(\frac{q(z|x)}{p(z|x)})
\end{aligned}
$$

where $KL(q(z|x)||p(z))$ represents the KL divergence between the estimated latent values and tru latent values. The term $p(z|x)$ is an intractable function and therefore cannot be computed. So the final loss becomes maximizing the term $E_z[\log p(x|z)] - KL(q(z|x)||p(z))$.

$$
\mathcal{L} = E_z[\log p(x|z)] - KL(q(z|x)||p(z))
$$

The training is given by
$$
\theta^*, \phi^* = arg\underset{\theta, \phi}max \sum^{N}_{i=1}\mathcal{L}(x^{(i)}, \theta, \phi)
$$

where $\phi$ is weigths of $q$ and $\theta$ is weights of $p$.

## 7. *Linear Independence*
This simply means that any two vector is linearly independent if one can be calculated using the other using a scalar constant i.e. if $x_1$ and $x_2$ are two linearly  dependent vectors, then $x_1 = c.x_2$ where $c$ lies in the vector space of $x_2$

## 8. *Mahalonobis distance*
Mahalonobis distance is the distance measure of a sample point $P$ from a distribution $D$. Given a sample point $x$ and the mean and covariance of a distribution as $\mu$ and $\Sigma$ respectively, then the mahalonobis distance is defined as;

$$
D_M(x) = \sqrt{(x-\mu)^T\Sigma^{-1}(x-\mu)}
$$

If the distribution has unit covariance, then this distance is simply Euclidean distance. Thus, Mahalonobis distance is unitless and scale-invariant and represents the correlation between data points.

Mahalonobis distance can also be defined as dissimilarity measure between 2 random vectors $\mathbf{x}$ and $\mathbf{y}$ under the same distribution with covariance $S$,

$$
d_M(\mathbf{x}, \mathbf{y}) = \sqrt{(\mathbf{x} - \mathbf{y})^T S^{-1} (\mathbf{x} - \mathbf{y})}
$$

## 9. *Poisson image editing* ([link](http://www.ctralie.com/Teaching/PoissonImageEditing/))
Suppose, the source image is denoted by $\mathbf{S}$ and the image to be pasted is denoted by $\mathbf{B}$, then $\mathbf{B}$ needs to be modified in such a way that it blends smoothly in $\mathbf{S}$. This modified image of $\mathbf{B}$ is denoted by $\mathbf{H}$.

<img src="./artifacts/Screen Shot 2020-09-07 at 12.43.41 PM.png">

Basically, we want the gradient information inside $\Omega$ to be the same in for both $\mathbf{B}$ and $\mathbf{H}$. The gradient of B is given by

$$
\nabla{B(x, y)} = 4B(x, y) - B(x-1, y) - B(x+1, y) - B(x, y-1) - B(x, y+1)
$$

We also want the boundary of $\mathbf{B}$ to be the same pixel value as boundary of $\mathbf{H}$. This is given by
$$
H_{(x, y)} = S_{(x, y)} \forall (x, y) \in \delta\Omega
$$

The 2 equations can be combined as
$$
NH(x, y) - \sum_{((dx, dy) + (x, y))\in \Omega} H(x+dx, y+dy) - \sum_{((dx, dy) + (x, y))\in \delta\Omega} A(x+dx, y+dy) = \sum_{((dx, dy) + (x, y))\in \delta\Omega \cup \Omega}(B(x+dx, y+dy) - B(x, y))
$$


## **10. Cosine similarity and Gram matrix**
The cosine similarity between 2 vectors $\mathbf{A}$ and $\mathbf{B}$ is given by :

$$
similarity = \cos\theta = \frac{\mathbf{A}.\mathbf{B}}{||\mathbf{A}||||\mathbf{B}||} =  \frac{\mathbf{A}.\mathbf{B}}{\sqrt{\sum_{i=1}^{n}A_i^{2}}\sqrt{\sum_{i=1}^{n}B_{i}^2}}
$$

If the vectors are facing opposite direction, $\theta=180^{\degree}$ and $\cos\theta=-1$. Similarly, if the vectors are in the same direction, $\theta=0^{\degree}$ and $\cos\theta=1$.
The dot product of vector $\mathbf{A}$ and $\mathbf{B}$ is given by:
$$
\mathbf{A}.\mathbf{B} = ||\mathbf{A}||.||\mathbf{B}||\cos\theta
$$

A low dot product value indicates low similarity and high dot product indicates high similarity.

## **11. Why do we differentiate a function wrt 0 to find extrema.**

* A derivative defines the slope of the graph plotted by the function. And only during peaks or minimum is the slope of the graph horizontal i.e. 0. Since our interest is to find this extrema, we differentiate wrt 0.

## **12. Probability**
### **12.1 Joint probability**
* Joint probability is defined as the probability of 2 events occuring together.
$$
P(6\;and\;red) = p(6) * p(red)
$$

### **12.2 Conditional probability**
* Probability of an event based on the occurence of previous event.
  + P(A) is that it will rain today. It has probability of 0.3
  + P(B) is probability that you need to go out => 0.5

  $$
  P(A|B) = \frac{0.3 * 0.5}{0.3} = 50\%
  $$

## **13. Flow based Generative models**

Consider we have a $d$ dimensional dataset $\mathcal{D}=\{x_1, x_2, x_3, ..., x_d\}$. We can plot the probability distribution from a given sample, but we would like to know the the probability density function from which these points are sampled.

Example:\
Suppose we have set of datapoints $\mathcal{S}={s_1, s_2...s_n}$. When we plot the datapoints, we observe a normal or close to normal distribution. But to sample more points from using this distribution, we want to know the density function which created this plot. In this case, our goal woul be to approximate/calculate the density function
$$
p(\mathcal{D}| \mu, \sigma) = \frac{1}{\sigma \sqrt{2 \pi}} exp(-\frac{1}{2}(\frac{(x - \mu)^2}{\sigma^2}))
$$

Similarly, for a given dataset, we would like to identify this probability density function which is usually very complex.

To find the explicit PDF, we use normalizing flows, which uses the change of variable theorem. The basic idea is, given a dataset $\mathcal{D}={x_1, x_2, ...., x_d}$, we first gaussianize this distribution using conservation of mass theory.

$$
Given, x \sim p(x)
$$

We take a known, simple distribution $\pi(z)$ such as gaussian and try to gaussianize the original points $x$ to this distribution $\pi(z)$ using a series of transformation


$$
z = f(x), z \sim \pi(z)
$$

Then, by change of variables formula

$$
\begin{aligned}
\int p(x)dx &= \int \pi(z)dz = 1\\
p(x) &= \pi(z) |\frac{dz}{dx}| \\
p(x) &= \pi(f(x)) |det \frac{df(x)}{dx}|\\
log(p(x)) &= log(\pi(f(x))) + log|det \frac{df(x)}{dx}|
\end{aligned}
$$

During inference, we sample from the simple gaussianized distribution and apply inverse transformation.

## **Points to remeber for flow based models**
* We need $\frac{df(x)}{dx}$ to be invertible, because if $f(x)$ maps to same value of 2 different $x$, then the inverse of it would not be possible,

* Auto-regressive and inverse auto-regressive models have slower inference and training time respectively. This is because they operate on per variable level. We move to more sophisticated methods which work on multiple high dimensional variables such as RealNVP, GLOW etc.

## **14. Gradients**
* Backpropogation is done by calculating the change in loss wrt small change in the associated weights. 
* This $\frac{\delta \mathcal{L}}{\delta w_{ij}}$ is called the **gradient** of weight $w_{ij}$

## **15. Caveats of flow-based models**
* *Discrete to continouos* : The images pixel values are discrete in the range $[0, 255]$. Since flow-based models are formulated on continuous values, we need to convert them to continuous values. Keep in mind that normalizing doesn't mean continuous (a silly note to myself). Therefore we apply the below formulation.

For e.g., MNIST has 1 channel of maximum 255 pixel intensity which can be represented in 8 bits.
Given, n_bits = 5, n_bins = $2^{n\_bits}$
$$
  x = \frac{x}{2^8} 
$$
$$
  x = \frac{floor(x * n\_bins)}{n\_bins}
$$
$$
  x = x - 0.5
$$

The above equation can be simplified as 
$$
  x = floor(\frac{x}{2^{8 - n\_bins}})
$$
$$
  x = \frac{x}{n\_bins} - 0.5
$$

The [link](https://github.com/openai/glow/issues/51) provides further details

* *Probability density -> Probability mass* : We need to convert the objective/loss provide the loss for the discrete image values rather than the continuous ones. To do that we add an additional integration term to the image which is given by **probability density at one point $\times$ volume**. 

$$
loss = -\log(n\_bins) \times total\_pixels
$$

More explanation [here](https://github.com/openai/glow/issues/43) and [here](https://arxiv.org/pdf/1511.01844.pdf)

* *Converting log likelihood terms to bits per pixel*: Most papers use the bits-per-dimension metric to evaluate the generative models which are in log base $e$. The loss function of flow-based models are kind of NLL in log base $2$. We can convert them to bits-per-pixel using, by changing log base $e$ to base $2$ 

$$
  bits\_per\_pixel = \frac{(nll\_value)}{(num\_pixels \times log_2)}
$$

More explanation [here](https://stats.stackexchange.com/questions/423120/what-is-bits-per-dimension-bits-dim-exactly-in-pixel-cnn-papers/431012), [here](https://www.reddit.com/r/MachineLearning/comments/56m5o2/discussion_calculation_of_bitsdims/) and [here](https://arxiv.org/pdf/1705.07057.pdf)

* *Bounded to unbounded distribution*
The change of variables formula is applicable to unbounded distributions. But our image data after dequantization is bounded between the values [0, 1] or [0, 256]. To convert it to unbounded data distribution, we use inverse of sigmoid function which is called **logit**. It is defined as :

$$
logit(x) = \frac{x}{1-x}
$$


## **16. Conditional and Unconditional GANs**
*Conditional* GANs make use of data labels to produce generative images. These are kind of supervised generative models. *Unconditional* GANs such as that of Goodfellow's does not need any labels and are unsupervised generative models.


-------------------------------------------------------------------------------------------------\

# **Notes**

* Determinant of a triangular or diagonal matrix is easy to calculate.


