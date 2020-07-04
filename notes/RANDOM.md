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
  p(x) = \int p_{\theta}(z)p_{\theta}(x|z)
$$

where $z$ denotes the latent representation of the image $x$. As the size of the image grows, the dimensionality of the observation and the latent variable and become quite large, hence intractable. Read [this](http://akosiorek.github.io/ml/2018/03/14/what_is_wrong_with_vaes.html) and to understand why $p(z|x)$ is intractable, Read [this](https://medium.com/retina-ai-health-inc/variational-inference-derivation-of-the-variational-autoencoder-vae-loss-function-a-true-story-3543a3dc67ee) for more details.

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

