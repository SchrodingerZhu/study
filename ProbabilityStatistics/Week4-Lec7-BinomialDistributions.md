# Week4 - 1

## Review

$$
E[g(X)] = \sum f(x)g(x)
$$


- Mean: $g(X) = X$
- Variance: $g(X) = (X - EX)^2$
- Moment: $g(X) = X^t$
- Mgf: $g(X) = e^{tX}$

## Binomial Distribution

### Bernoulli Experiment
The outcomes can be classified in one if two mutually exclusive and exhaustive ways.

### Bernoulli Trials
When a Bernoulli experiment is performed several independent times and the probability of success, say $p$, remains the same from trial to trial or equivalently, the probability of failure, $1 − p = q$.

### Bernoulli Distribution

Let $X$ be a RV associated with a Bernoulli trial with the probability of success p.

- RV: X{success} = 1, X{failure} = 0
- pmf: $f(x) = p^x(1 - p)^{1 - x}$

### Binomail Distribution 
We are interested in the number of successes in $n$ Bernoulli trials. The order of their occurence is not concerned.
1.  A Bernoulli (success-failure) experiment is performed $n$ times.
2.  Then trials are independent $P(\bigcap^n_{i=1}A_i) =\prod^n_{i=1}P(A_i)$, where $A_i$ is the event associated with $i$th trial, multiplicative rule for independent events.
3.  The probability of success for each trial is $p$.

$X$ ~ $b(n, p)$ 

### Expectations

$$
\text {Mgf} = [(1 - p) + pe^t]^n \\
EX = np \\
EX^2 = n^2p^2 - np^2 + np \\
Var = np(1 - p)
$$

