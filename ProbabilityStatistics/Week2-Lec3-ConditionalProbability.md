# Conditional Probability

## Definition

The conditional probability of an event $A$, given that event $B$ has occurred, is defined by
$$
P(A|B) = \frac{P(A\cap B)}{P(B)}
$$
provided that $P(B) > 0$.

**Note that the sample space of the left hand side is $B$, while it is $S$ on the right hand side.**

## Definition (In Probability Function)

- $P(A|B) \ge 0$

- $P(B|B) = 1$

- If $A1,A2,A3,···$ are countable and mutually exclusive events, then
  $$
  P(\bigcup A_i) = \sum P(A_i | B)
  $$


## Multiplication Rule

$$
P(A\cap B ) = P(A)P(B | A)
$$

**Proven by definition.**

## Multiplication Rule for Three Events

$$
P(A\cap B\cap C) = P(A)P(B|A)P(C|A\cap B)
$$

**Proof**
$$
\begin{aligned}
P(A\cap B\cap C) &= P((A\cap B)\cap C)\\
& = P(C|A\cap B)P(A\cap B) \\
&= P(A)P(B|A)P(C|A\cap B)
\end{aligned}
$$
