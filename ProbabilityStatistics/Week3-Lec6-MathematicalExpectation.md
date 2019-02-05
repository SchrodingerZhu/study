# Mathematical Expectation
## General Definition
Assume $X$ is a discrete RV with range $S$ and $f(x)$ is its pmf.If $\sum_{x∈S}g(x)f(x)$ exists, then it’s called expectation of $g(X)$ and is denoted by
$$
E(g(X)) = \sum_{x\in\overline S} g(x)f(x)
$$

## Linear Properties of Mathematical Expectation

- $E(C) = C,\text{ C is constant }$
- $E(cg(X)) = cE(g(X))$
- $E[c_1g_1(X) + c_2g_2(X)] = c_1E[g_1(X)] + c_2E[g_2(X)]$

## Example: MMSE estimator
Let $g(x) = (x − b)^2$ where $b$ is a constant to be chosen and
suppose $E[(X − b)^2]$ exists. Find the value of $b$ for which $E[(X − b)^2]$ is minimized.

$$
\frac{d}{db}E\left[(X - b)^2\right] = \frac{d}{db}E[X^2 - 2bX + b^2] = \frac{d}{db} \left(EX^2 - 2bEX + b^2\right) = -2EX + 2b \\
\therefore b = EX
$$

## Special Mathematical Expectation

### Mean
The expectation of $X$ is called the mean of $X$

$$
E[X] = \sum_{x \in \overline S} xf(x)
$$

### Variance

$$
Var(X) = E[X - EX]^2 = E[X^2 - 2XEX + (EX) ^ 2] = E[X^2] - 2EXEX + (EX)^2 = EX^2 - (EX)^2
$$

- Standard deviation:
  $$
  \sqrt{Var(X)}
  $$

- $Var(X)$ is not a linear function:
  - $Var(c) = 0$
  - $Var(cX) = c^2Var(X)$  

### $rth$ Moment
$r$ is a positive integer. If $E[X^r] = \sum_{x∈S}x^rf (x)$ exists, then it is called rth moment
of $X$. In addition, $E(X − b)^2 =\sum_{x∈S}(x − b)^rf (x)$ is called the $rth$ moment of the distribution about $b$.

### $rth$ factorial moment
$$
E[(X)_r]
:= E[X(X −1)· · ·(X −r + 1)] 
$$

## Moment Generating Function (mgf)

Let $X$ be a discrete RV with range space $S$ if there is $h > 0$ such that
$$ 
E[e^{tX} ] = \sum_{x∈S}e^{tx} f (x), \text{exists}\ − h < t < h
$$ 
then the function defined by $M(t) = E[e^{tX}]$ is called the moment generating function (mgf).

#### Properties
$$
M'(0) = EX\\
M''(0) = EX^2\\
M^{(r)}(0) = EX^r
$$