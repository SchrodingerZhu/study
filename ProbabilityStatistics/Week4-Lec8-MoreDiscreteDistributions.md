## Negative Binomial Distribution

Description:  We are interested in the situation that we observe a sequence of Bernoulli trials until exactly $r$ successes occur, where $r$ is a fixed positive integer.

Define a RV $X$ to denote the trial number at which the $r$th success is observed. Then $X$ has the range $S=\{r,r+ 1,···\}$.Let $f(x)$ denote the pmf of $X$. 

$$
A = \{\text {$r - 1$ success occur at $x - 1$ trials }\}, \\
B = \{\text {$x$ th trial is successful}\}, \\
f(x) = P(A \cap B) = P(A)P(B)
$$

And we can find that,
$$
P(A) = \left(
\begin{array}{cc}
x - 1\\
r - 1
\end{array}\right)p^{r - 1}(1 - p)^{x - r}, \\
P(B) = p,\\
\therefore 
f(x) = \left(
\begin{array}{cc}
x - 1\\
r - 1
\end{array}\right)p^{r}(1 - p)^{x - r}
$$

## Geometric Distribution

When $r = 1$, $f(x) = p(1 - p)^{x - 1}$, this is the so-called geometric distribution.

For a positive integer $k$,
$$
P(X > k) = (1 - p)^k \\
P(X \le k) = 1 - (1 - p)^k
$$

## Mean and Variance of NBD
$$
E[X] = \frac{r}{p},\\
Var[X] = \frac{r(1 - p)}{p^2}\\
Mgf\ M(t) = E[e^{tX}] 
$$

## Poisson Distribution

### Introduction to APP
There are experiments that result in counting the number of times that particular events occur within a given period or for a given physical object.

Counting such events can be seen as observations of a RV associated with an approximate Poisson process (APP).

### Definition of APP
Let the number of occurrences of some event in a given continuous  interval  be  counted.    Then  we  have  an  APP  with parameter $λ > 0$ if

- The number of occurrences in non-overlapping subintervals are independent.
- The probability of exactly one occurrence in a sufficiently short subinterval of length h is approximately λh.
- The probability of two or more occurrences in a sufficiently short subinterval is essentially 0.

### Distribution
Let $X$ denote the number of occurrences in an interval with length 1.  We aim to find an approximation for $f(x) =P(X=x)$, where $x= 0,1,2,···$.

- First partition the unit interval into $n$ subintervals, each with length $\frac{1}{n}$
- When $n >> x$, $P(X = x)$ can be approximated bt the probability that exactly $x$ of these $n$ subintervals each has one occurrence.
  - one occurrence in $\frac{1}{n}$ has probability $\frac{\lambda}{n}$. 
  -  Therefore, the occurrence and nonoccurrence in each subinterval can be seen as Bernoulli experiment with probability of success $\frac{λ}{n}$
  - then Bernoulli experiments are independent.Therefore occurrence and nonoccurrence in then subintervals are $n$ Bernoulli trials with probability of success $\frac{λ}{n}$ 
- Therefore, 
  $$
  P(X = x) = \frac{n!}{x!(n - x)!}\left(\frac{\lambda}{n}\right)^x\left(1 - \frac{\lambda}{n}\right)^{n - x}
  $$
- when $n \to \infty$
  $$
  \lim_{n\to\infty} \frac{n!}{(n - x)!x^n} = \frac{n (n - 1)\cdots(n - x)!}{(n - x)! n^x} = 1 \\
  P(X = x) = \lim_{n\to\infty} = \frac{n!}{(n - x)!n^x} \frac{\lambda^x}{x!} (1 - \frac{\lambda}{n})^n(1 - \frac{\lambda}{n})^{-x} = \frac{\lambda^xe^{-\lambda}}{x!}
  $$

### What is $\lambda$?
It is just the Mean.
$$
\begin{aligned}
  M(t) &= E(e^{tX})\\
  &= \sum_{x = 0}^\infty e^{tx} \frac{\lambda^xe^{-\lambda}}{x!}\\
  &= e^{-\lambda} \sum_{x = 0}^\infty\frac{(\lambda e^t)^x}{x!}\\
  &= e^{-\lambda}\cdot e^{\lambda e^t} \\
  M'(t) &= \lambda e^te^{{\lambda (e^t - 1)}}\\
  M'(0) &= \lambda\\
  M''(t)&= \lambda e^t e^{{\lambda (e^t - 1)}} + \lambda ^ 2e^{2t} e^{{\lambda (e^t - 1)}}\\
  M''(0)&= \lambda + \lambda^2\\
  Var[X]&= EX^2 - (EX)^2 = \lambda
\end{aligned} \\
$$

