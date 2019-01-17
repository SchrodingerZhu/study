# Independent Events And Bayes

## Independent Events

### Definition (For Two Events)

Events $A$ and $B$ are independent if and only if $P(A∩B) =P(A)P(B)$ .Otherwise, event $A$ and $B$ are called dependent events.

### Theorem (For Two Independent Events)

$A$ and $B$ are independent, if and only if any pair of the following events are independent:

1. $A$ and $B'$
2.  $A'$ and $B$
3.  $A'$ and $B'$

Obviously, these three statements and prove each other. Therefore, we can just proof the first one:
$$
P(A) = P(A\cap(B\cup B')) = P(A\cap B) + P(A\cap B') \Rightarrow P(A)(1 - P(B)) = P(A\cap B')
$$

## Definition 

Events $A,\ B,\ C$ are mutually independent if and only if:

1. $A,\ B,\ C$ are pairwise independent.
   $$
   \begin{cases}
    P(A\cap B) = P(A)P(B)\\
    P(A\cap C) = P(A)P(C)\\
    P(B\cap C) = P(B)P(C)\\
   \end{cases}
   $$

2. follows **multiplication rule for three independent events**
   $$
   P(A\cap B\cap C) = P(A)P(B)P(C)
   $$


Mutual independence can be extended to four or more events: Each pair, triple, quartet of the events are independent and moreover,
$$
P(\bigcap A_i) = \prod A_i
$$
**(To Be Continued)**

