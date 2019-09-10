# Integer Functions
## Floors and Ceilings

### Properties
$$
\lfloor x\rfloor = x \iff \text {x is integer} = \lceil x \rceil \\
\lceil x \rceil - \lfloor x\rfloor = [\text {x is not integer}] \\
x - 1 \lt \lfloor x \rfloor \le x \le \lceil x \rceil \lt x + 1 \\
\lceil -x \rceil = -\lfloor x \rfloor\\
\lfloor -x \rfloor = - \lceil x \rceil 
$$

Laws

$$
\lfloor x \rfloor = n \iff n \le x \lt n + 1\\
\lfloor x \rfloor = n \iff x - 1 \lt n \le x\\
\lceil  x \rceil  = n \iff n - 1 \lt x \le n\\
\lceil  x \rceil  = n \iff x \le n \lt x - 1\\
\lfloor x + n \rfloor = \lfloor x \rfloor + n, n \in \mathbb Z\\
x \lt n \iff \lfloor x \rfloor \lt n\\
n \lt x \iff n \lt \lceil x \rceil\\
x \le n \iff \lceil x \rceil \le n\\
n \le x \iff n \le \lfloor x \rfloor     
$$

Fractional Parts

$$
\{x\} = x - \lfloor x \rfloor
$$


Example

$$
\lfloor x + y \rfloor = \lfloor x \rfloor + \lfloor y \rfloor + \lfloor \{x\} + \{y\} \rfloor
$$

Thus $\lfloor x + y \rfloor = \lfloor x \rfloor + \lfloor y \rfloor$ or $\lfloor x + y \rfloor = \lfloor x \rfloor + \lfloor y \rfloor + 1$

## Floor/Ceiling Application
$$
\left\lfloor \sqrt {\lfloor x \rfloor} \right\rfloor = \left\lfloor \sqrt x \right\rfloor, x \in \mathbb R^+ 
$$
**Proof**

$$
m = \left\lfloor \sqrt {\lfloor x \rfloor} \right\rfloor \\
\therefore m \le \sqrt {\lfloor x \rfloor} \lt m + 1\\
\therefore m^2 \le {\lfloor x \rfloor} \lt (m + 1)^2\\
\therefore m^2 \le x  \lt (m + 1)^2 \\
\therefore m \le \sqrt x  \lt (m + 1) \\
\therefore m =  \left\lfloor \sqrt x  \right\rfloor
$$
Similarly, we can proof
$$
\left\lceil \sqrt {\lceil x \rceil} \right\rceil = \left\lceil \sqrt x \right\rceil, x \in \mathbb R^+ 
$$
Let $f(x)$ be a mono-increasing function, s.t.
$$
f(x) \text { is integer } \Rightarrow \text {x is integer}
$$
We have,
$$
\left\lfloor f(x) \right\rfloor = \left\lfloor f\left(\left\lfloor x\right \rfloor\right) \right\rfloor
$$
$$
\left\lceil(x) \right\rceil = \left\lceil f\left(\left\lceil x\right \rceil\right) \right\rceil
$$

$$
\left \lceil \sqrt {\lfloor x \rfloor} \right \rceil = \left \lceil \sqrt x \right \rceil \iff \text{int}(x) \vee \neg \text{int}(\lfloor x \rfloor)
$$

The number of integers:

- $[\alpha, \beta)$ has $\lceil \beta \rceil - \lceil \alpha \rceil$ integers.
- $(\alpha, \beta)]$ has $\lfloor \beta \rfloor - \lfloor \alpha \rfloor$ integers.
- $[\alpha, \beta]$ has $\lfloor \beta \rfloor - \lceil \alpha \rceil + 1$ integers
- $(\alpha, \beta)$ has $\lceil \beta \rceil - \lfloor \alpha \rfloor - 1$ integers, $\alpha \ne \beta$

Count the number from $1$ to $1000$ that $\left\lfloor \sqrt[3]{n}\right\rfloor \mid n$

$$
\begin{aligned}
    \sum_{1 \le n \le 1000} \left[\left\lfloor \sqrt[3]{n}\right\rfloor \mid n\right] & =\sum_{k, n}[k = \lfloor \sqrt[3] n\rfloor][k \mid n][1 \le n \le 1000] \\
    &= \sum_{k,m,n} [k^3 \le n \lt (k + 1)^3][n = km][1 \le n \le 1000]\\
    &= 1 + \sum_{k,m,n} [k^2 \le n \lt (k + 1)^3/k][1 \le k \lt 10]\\
    &= 1 + \sum_{1 \le k \lt 10} \left(\lceil k^2 + 3k + 3 + k^{-1} \rceil - \lceil k^2 \rceil \right)\\
    &= 1 + \sum_{1 \le k \lt 10} (3k + 4) \\
    &= 172
\end{aligned}
$$

This can be generalized to upper bound $N$
$$
W = \lfloor N / K\rfloor + \frac{1}{2}K^2 + \frac{5}{2}K - 3, K = \left\lfloor \sqrt[3] N \right\rfloor
$$

### Spectrum
For $\alpha \in R$, we define it's spectrum as an infinite multi set:
$$
\text{Spec}(\alpha) = \{\lfloor \alpha \rfloor, \lfloor 2\alpha \rfloor, \lfloor 3\alpha \rfloor, \cdots\}
$$

Let $\alpha < \beta$, $\exists m$, s.t. $m(\beta - \alpha) \ge 1$.\
Therefore, 
$$
m\beta > m\alpha 
$$
Therefore,
$$
\forall x \in \text{Spec}(\beta), \sharp ({x \le \lfloor m\alpha \rfloor})\lt m
$$
We can find that, for each real number, its spectrum is unique.

One special example is that 
$$
\text{Spec}(\sqrt 2) \\
\text{Spec}({\sqrt 2 + 2})
$$
give a partition on $\mathbb Z^+$.

**proof**
We first define $N(\alpha, n), \alpha > 0$ as the number of elements in $\text{Spec}(\alpha)$ that less equal than $n$
$$
\begin{aligned}
N(\alpha, n) &= \sum_{k > 0} [\lfloor k \alpha \rfloor \le n] \\
             &= \sum_{k > 0} [\lfloor k \alpha \rfloor \lt n + 1] \\
             &= \sum_{k > 0} [k \alpha \lt n + 1] \\
             &= \sum_k[0 \lt k \lt (n + 1) / \alpha] \\
             &= \lceil (n + 1) / \alpha \rceil - 1
\end{aligned}
$$
Thus,
$$
\begin{aligned}
N(\sqrt 2, n) + N(\sqrt 2 + 2, n) &= \left\lceil\frac{n + 1}{\sqrt 2}\right\rceil - 1 + \left\lceil\frac{n + 1}{\sqrt 2 + 2}\right\rceil - 1
\\&= \left\lfloor\frac{n + 1}{\sqrt 2}\right\rfloor + \left\lfloor\frac{n + 1}{\sqrt 2 + 2}\right\rfloor \\
&= \frac{n + 1}{\sqrt 2} + \frac{n + 1}{\sqrt 2 + 2} - \left\{\frac{n + 1}{\sqrt 2}\right\} - \left\{\frac{n + 1}{\sqrt 2 + 2}\right\}
\end{aligned}
$$
Since 
$$
\frac{1}{\sqrt 2} + \frac{1}{\sqrt 2 + 2} = 1 \\
\left\{\frac{n + 1}{\sqrt 2}\right\} + \left\{\frac{n + 1}{\sqrt 2 + 2}\right\} = 1
$$
The proof is done.



***(To be continued.)***