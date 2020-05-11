# Random notes

## Smooth vs continuous functions

A function $f$ is said to be continuous if it is not discrete, i.e., $f$ is
differentiable in a defined interval.

A function $f$ is said to be $C^k$ smooth if $f$ has the $k$th order
differential.

## Kullback-Leibler divergence ($KL$)



## Jensen-Shannon divergence ($JSD$)

Given two probability distribution functions, $P$ and $Q$, the Jensen-Shannon
divergence is given by

$$
JSD(P\Vert{Q}) = \frac{1}{2}KL(P\Vert{M}) + \frac{1}{2}KL(Q\Vert{M})
$$

where $M = \frac{P + Q}{2}$.