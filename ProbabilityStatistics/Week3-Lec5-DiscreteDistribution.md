# Chapter 2 Discrete Distribution

## Defininition of Random Variable (RV)

Given a random experiment with sample space S, a dunction $X: S \to \overline S \subseteq R$ that assign one real number $X(s) = x$ to each $s \in S$ is called Random Variable(RV).

Notice that $X: S \to \overline S$ is not necessarily an one-to-one function. 

## Conventions of RV

- uppercase letters stand for RVs.
- lowercase letters $z, y, z$ stand for numeric values of RV $X, Y, Z$ respectively.
- $P_r(\cdot)$ is the probability function associated with $S$.
- $P(\cdot)$ is the probability function associated with $\overline S$
- $P(X=x):=P({X=x}) =Pr({s|X(s) =x,s∈S})$
- $P(X∈A):=P({X∈A}) =Pr({s|X(s)∈A,s∈S})$

## Discrete RV Definition 
The range of $X$ is the set $X(s) = S = \{x|X(s) =x,s∈S\}$.A RV is called  discrete if its range $S$ is finite or countably infinite.

## Probability Mass Function (pmf)
Suppose that $X$ is a RV  with range $S$. Then a function f(x) : S → [0,1] is called pmf, if
- $f(x) \gt 0 , x \in \overline S$
- $\sum_{x\in\overline S} f(x) = 1$
- $P(X \in A) = \sum_{x \in A} f(x), A \subset \overline S$
## Cumulative Distribution Function (cdf)

The function $F(x) =P(X≤x)$ is called the cumulative distribution function (cdf).

**Notice: $P(X≤x) =\sum_{x′≤x,x′∈\overline S}f(x′)$.**

## Uniform Distribution
A RV $X$ is said to have a uniform distribution if $f(x) = \text{constant}$ for $x∈S$
