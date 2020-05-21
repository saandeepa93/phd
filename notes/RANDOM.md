# Random notes

## Smooth vs continuous functions

A function $f$ is said to be continuous if it is not discrete, i.e., $f$ is
differentiable in a defined interval.

A function $f$ is said to be $C^k$ smooth if $f$ has the $k$th order
differential.

## Kullback-Leibler divergence ($KL$)
Given 2 probability distributions $P$ and $Q$, the KL divergence is given by
$$
KL(P||Q) = \sum_{x \in X}P(x)log(\frac{P(x)}{Q(x)})
$$
In context of machine learning, $KL(P||Q)$ is the information gain if $P$ is used
instead of $Q$


## Jensen-Shannon divergence ($JSD$)

Given two probability distribution functions, $P$ and $Q$, the Jensen-Shannon
divergence is given by

$$
JSD(P\Vert{Q}) = \frac{1}{2}KL(P\Vert{M}) + \frac{1}{2}KL(Q\Vert{M})
$$

where $M = \frac{P + Q}{2}$.

## Differential Evolution
Differential Evolution is an optimization technique to iteratively improve the
candidate solutions. This does not require any gradient information i.e. does not require the function to be differentiable (just like SDM).


