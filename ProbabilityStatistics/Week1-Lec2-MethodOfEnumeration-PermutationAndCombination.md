# Method of Enumeration （Permutation and Combination）

## Review

$$
P(\bigcup^\infty A_i) = \sum^\infty P(A_i)
$$

This property trivially holds for finite many sets by choosing other sets as empty set.

## Two Assumptions For This Lecture

- finite outcome, let us say $m$.

- they are equally likely,
  $$
  P(\{e_k\}) = \frac{1}{m}
  $$


In this case, we have:
$$
P(A) = \frac{\mathcal N(A)}{\mathcal N(S)}
$$
 **Check the definition, it is just a possibility function.**
$$
P(\bigcup^\infty A_i) = \frac{\mathcal N(A)}{\mathcal N(S)} = \frac{\sum^\infty\mathcal N(A_i)}{\mathcal N(S)} = \sum^\infty P(A_i)
$$

## Counting Techniques

### Assumption

A random experiment can be done by a sequential implementation of two or more sub-experiments.

### Multiplication Principle

A sequential experiment
$$
Outcome(E) = \prod^\infty Outcome(E_i)
$$

### Permutation

#### The Permutation of $n$ objects

$$
_nP_n = n!
$$

#### The Permutation of $n$ objects taken $r$ at a time

$$
_nP_r = \frac{n!}{(n - r)!}
$$

### Ordered Sample

>  If $r$ objects are selected from a set of $n$ objects and if the order of selection is noted, then the selected set of $r$ objects is called ordered sample of size r.

#### Sampling with replacement

> Occurs when an object is selected and then replaced before
> the next object is selected $(n^r)$.

#### Sampling without replacement

> Occurs when an object is not replaced after it has been selected $(_nP_r)$.

### Combination

**We consider permutation of $n$ objects taken $r$ at a time by multiplication principle.**

It is just first a combination and then a permutation.
$$
_n C _r \times _rP_r = _nP_r
$$
Thus we have:
$$
_nC_r = \frac{n!}{r!(n - r)!}
$$
And，
$$
_nC_r = _nC_{(n - r)} = 
\left(
\begin{array}{}
n\\r
\end{array}
\right)
$$

### Distinguishable Permutation of objects of two types

**We consider permutation of $n$ different objects by multiplication principle.**

Permutation of all equals deciding the permutation of the types then permutation of type A and then equals permutation of type B. 
$$
n! = X \times r! \times (n - r)! \\
X = _nC_r
$$

### Distinguishable permutation of objects of m types

$$
n! = X \prod (a_i!) \\
X = \frac{n!}{\prod(a_i!)}
$$

## TODO:

* [ ] Review the property of permutation and combination 

* [ ] Review some special permutation 

