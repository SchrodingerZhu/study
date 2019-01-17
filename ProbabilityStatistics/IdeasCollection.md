# Ideas Collection

## The Relation Between Nullable Undistinguishable Objects Partition & Distinguishable Permutation

In high school, we have learnt about how to count the number of different nullable partitions of several undistinguishable objects.

Suppose we have $x$ identical objects and we want to divide them into $y$ different nullable groups. In high school, the method is imagine objects as balls and partition as walls. To form $y$ groups of balls we need to "build" $y - 1$ walls. So together we have $x + y - 1$ objects and we can just choose $y - 1$ of them as walls. So the answer is:
$$
_{x + y - 1} C _{y - 1}
$$
In **STA2001**，actually the abstraction is the same but the method to calculate is different. The $x + y - 1$ objects are of two kinds. Therefore, it is naturally for us to thinking it in the key of distinguishable permutation. In this way, the answer can be written as:
$$
\left(\begin{array}{c}x + y - 1\\x, y - 1\end{array}\right) = \frac{(x + y - 1)!}{x!(y - 1)!}
$$
