# Ideas Collection

## The Relation Between Nullable Undistinguishable Objects Partition & Distinguishable Permutation

In high school, we have learnt about how to count the number of different nullable partitions of several undistinguishable objects.

Suppose we have $x$ identical objects and we want to divide them into $y$ different nullable groups. In high school, the method is to imagine objects as balls and partitions as walls. To form $y$ groups of balls we need to "build" $y - 1$ walls. So together we have $x + y - 1$ objects and we can just choose $y - 1$ of them as walls. So the answer is:
$$
_{x + y - 1} C _{y - 1}
$$
In **STA2001**, actually the abstraction is the same but the method to calculate is different. The $x + y - 1$ objects are of two kinds. Therefore, it is naturally for us to thinking it in the way of distinguishable permutation. In this way, the answer can be written as:
$$
\left(\begin{array}{c}x + y - 1\\x, y - 1\end{array}\right) = \frac{(x + y - 1)!}{x!(y - 1)!}
$$

## Different Endings of One Game

We may sometimes meet this kind of problem: A game will end if several events happen, and we want to calculate the probability of ending in each kind of event.

I first figure out a direct way to solve it, suppose the ending events are $A_1, A_2, A_n, \cdots$ , then each time the probability of not ending in this turn is:
$$
P_{not} = 1 - P(\bigcup A_i)
$$
Therefore, we can just calculate the probability of ending with $A_i$ as following:
$$
P(\mathbf {End\ with\ A_i}) = \sum_{t = 0}^\infty (P(A_i)P_{not}^t)
$$
This is convergent and can be easily calculated out.

However, if we change our mind into conditional probability, we can get:
$$
P(\mathbf {End\ with\ A_i}) = P(A_i | \mathbf {End}) = \frac{P(A_i)}{P(\bigcup A_t)}
$$
This is because when focusing on ending, it is not important to know the game will go on how many turns.