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

## Binomial Distribution

Using Generating Function, we can derive some formula for binomial distributions:
$$
\begin{aligned}
f(x)& = \sum_{x = 0}^n \ _nC_xp^x(1 - p)^{n - x} \\

M(t) &=  \sum_{x = 0}^n \ _nC_xp^x(1 - p)^{n - x}e^{tx} \\

&= (1 - p)^n \sum_{x = 0}^n\ _nC_x (\frac{pe^t}{1 - p})^x \\
&= (1 - p)^n\left(1 + \frac{pe^t}{1 - p}\right)^n\\

M'(t) &= n(1 - p)^n\left(1 + \frac{pe^t}{1 - p}\right)^{n - 1} \frac{pe^t}{1 - p} \\
EX &= M'(0)\\
&=n(1 - p)^n(1 - p)^{-n} p\\
&= np \\
M''(t) &= np(1 - p)^{n - 1}\left[(n - 1)\left(1 + \frac{pe^t}{1 - p}\right)^{n - 2}\frac{pe^{2t}}{(1 - p)} + e^t\left(1 + \frac{pe^t}{1 - p}\right)^{n - 1}\right]\\
EX^2 &= M''(0)\\
&= np(1 - p)^{n - 1}\left[ p(n - 1)(1 - p)^{1 - n} + (1 - p)^{1 - n}\right]\\
&=np(p(n - 1) + 1)\\
&=n^2p^2 - np^2 + np
\\
E(X(X - 1))&=E(X)^2 - E(X)\\
&= n^2p^2 - np^2
\\
\sigma^2 &= EX^2 - (EX)^2\\
&=np(1 - p)
\end{aligned}
$$

## Misaligned Permutation

This question asks about when arrange $n$ objects to $n$ position, how many ways can we arrange them in which at least one of them match the number. Its opposite side is the just the misaligned Permutation.

When $n = 1$, 
$$
P(\bigcup_{i = 1}^n A_i) = P(A_1)
$$
Suppose when $n = k \ge 1$,
$$
P(\bigcup_{i = 1}^k A_i) =\sum_{i = 1}^k (-1)^{i - 1}\sum P(\bigcap_{\sum j = i}A_j)
$$
Then, when $n  = k  + 1$
$$
P(\bigcup_{i = 1}^{k + 1} A_i) = P(\bigcup_{i = 1}^{k} A_i) + P(A_{k + 1}) - P\left(A_{k + 1} \cap \left(\bigcup_{i = 1}^{k} A_i\right)\right) \\
\begin{aligned}
P\left(A_{k + 1} \cap \left(\bigcup_{i = 1}^{k} A_i\right)\right)
&=P\left((A_{k + 1}\cap A_k) \cup \left(\bigcup_{i = 1}^{k - 1} A_i\right)\right)\\
&= P(A_{k + 1}\cap A_k) + P\left(\bigcup_{i = 1}^{k - 1} A_i\right) - P((A_{k + 1}\cap A_k) \cap\left(\bigcup_{i = 1}^{k - 1} A_i\right))
\end{aligned}
$$
By totally expansion, we can get that
$$
P(\bigcup_{i = 1}^{k + 1} A_i) = \sum_{i = 1}^{k + 1} (-1)^{i - 1}\sum P(\bigcap_{\sum j = i}A_j)
$$
Notice that, for each number $i$, the total terms is
$$
_nC_i
$$
So for this question,
$$
P(\bigcup A_i) = \sum_{i = 1}^n (-1)^{i - 1}[\frac{n!}{(n - i)!i!} \times\frac{(n - i)!}{n!}]= \sum_{i = 1}^n (-1)^{i - 1}\frac{1}{i!}
$$
Also，
$$
P(\bigcup A_i) = 1 - P((\bigcup A_i)') = 1 - (P(\bigcap A_i)')  = (1 - (1 - P(\bigcup A_i))) = 1 - (1 + \sum_{i = 1}^n (-1)^{i}\frac{1}{i!})
$$
**This can be also derived in another method**.

Consider totally misaligned permutation. Let $a_n$ be the number of totally misaligned permutation of $n$ objects.  When we have $n$ objects, we can select the $kth$ object, where $k < n$. the permutation can be divided into two kinds:

- Let the $kth$ object at $nth$ position while the $nth$ object at $kth$ position, then we only need to misalign the other $(n - 2)$ objects. There are $(n - 1)a_{n - 2}$ permutations.
- Then let $nth$ object at $kth$ position, while $kth$ object cannot be at $nth$ position. This can be calculated in the following way: 
  - First choose $nth$ object‘s position from $(n - 1)$ choices. 
  - Now we have $1, 2, 3, \cdots, k- 1, k + 1, \cdots n$ totally $n - 1$ position. Notice that $kth$ object cannot choose $nth$ position, then it again become an $(n- 1)$ totally misaligned permutation.

$$
a_1 = 0\\
a_2 = 1\\
\cdots\\
a_n = (n - 1)(a_{n - 1} + a_{n - 2})
$$

Construct 
$$
a_n = n!b_n\\
b_1 = 0, b_2 = \frac{1}{2} \\
n!b_n = (n - 1)(n - 1)!b_{n - 1} + (n - 1)(n - 2)!b_{n - 2} \\
nb_n = (n - 1)b_{n - 1} + b_{n -2}\\
(b_n - b_{n - 1}) = -\frac{1}{n}(b_{n - 1} - b_{n - 2})
$$
So,
$$
(b_n - b_{n - 1}) = -\frac{1}{n}(b_{n - 1} - b_{n - 2}) = \frac{-1}{n}\frac{-1}{n - 1}(b_{n-2} - b_{b - 3}) = \frac{-1}{n}\frac{-1}{n- 1}\cdots\frac{-1}{3}(b_2 - b_1) = \frac{(-1)^n}{n!}
$$
Accumulate both sides,
$$
b_n= b_2 + \sum_{i = 3}^n(-1)^i\frac{1}{i!} = \sum_{i = 2}^n(-1)^i\frac{1}{i!}
$$
Then,
$$
a_n = n!b_n, P(A) = 1 - \frac{a_n}{n!} = 1 - b_n 
$$
$\mathscr{Q.E.D.}$

###   