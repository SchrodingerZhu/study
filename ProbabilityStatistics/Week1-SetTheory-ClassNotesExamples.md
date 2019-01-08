# Set Theory

## Distributive law

$$
A\cap(B\cup C) = (A\cap B)\cup(A\cap C) \\
A\cup(B\cap C) = (A\cup B)\cap(A\cup C)
$$

Usually, we use the inverse direction.

## De Morgan's law

$$
(A\cup B)' = A' \cap B' \\
(A\cap B)' = A' \cup B'
$$



## First Definition of Possibility

- repeat the experiment a number of times, say $n$ times.
- count the number of times that event $A$ actually occurs $\mathcal{N}(A)$
- $\frac{\mathcal N(A)}{n}$is called the relative frequency of event $A$ in $n$ repetitions of the experiment.
- The number $p$ that $\frac{\mathcal N(A)}{n}$ goes to as $n \to \infty$ is called the probability of event $A$ and is denoted by $P(A) = \lim_{n\to\infty}\frac{\mathcal N(A)}{n}$ .

## Definition of Possibility

A real-valued, set function $P$ that assigns to each event $A$ in the sample space $S$, a number $P(A)$, called the probability of the event $A$ such that the following properties are satisfied.

1. $P(A) \ge 0$

2. $P(S) = 1$

3. if $A_1, A_2, A_3, \cdots$ are countable and mutually exclusive events:
   $$
   P(\bigcup A_i) = \sum P(A_i)
   $$


## Probability Space

(definition with **Measure Theory**)

A probability space is a triple $(S, F, P)$

1. $S: $ the sample space.

2. $F$ is $\sigma-algebra$ on $S$ and a set of subsets of $S$:
   - $S \in F$
   - $F$ is closed under complement
   - $F$ is closed under countable unions

3. For countable and mutually exclusive events:

   - $P(A) \ge 0$

   - $P(S) = 1$

   - if $A_1, A_2, A_3, \cdots$ are countable and mutually exclusive events:

   $$
   P(\bigcup A_i) = \sum P(A_i)
   $$




# Properties and Their Proof:

## $P(A) = 1 - P(A')$

$$
P(S) = P(A \cup A') = P(A) + P(A')
$$

## $P(\emptyset) = 0$

$$
P(S) = P(\empty \cup S) = P(\empty) + P(S)\\
\therefore P(\empty) = 0
$$

## $A \subseteq B \to P(A) \le P(B)$

To express $B - A$, we use:
$$
B\cap A'
$$
Then we know:
$$
P(B) = P(B\cap S) = P(B\cap (A \cup A')) = P((B\cap A)\cup(B\cap A')) = P(A\cup(B\cap A'))
$$
It is easy to see:
$$
A \cap (B \cap A') = (A\cap A')\cap B = \empty
$$
Thus,
$$
P(B) = P(A) + P(B\cap A') \ge P(A)
$$

## $P(A)\le 1$

$$
1 = P(S) = P(A\cup A') = P(A) + P(A') \ge P(A)
$$

## $P(A\cup B) = P(A) + P(B) - P(A\cap B)$

$$
A\cup B =  (A\cup B)\cap S = (A\cup B)\cap(A \cup A') = A\cup(B\cap A') \\
\therefore P(A\cup B) = P(A) + P(B\cap A') \\
\because P(A\cap B) + P(A'\cap B) = P(B) \\
\therefore P(A\cup B) = P(A) + P(B) - P(A\cap B)
$$

