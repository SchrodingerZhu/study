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

## Floor/Ceiling Recurrence

### Knuth Number
$$
\begin{aligned}
    K_0 &= 1 \\
    K_{n + 1} &= 1 + \min (2K_{\lfloor n / 2 \rfloor}, 3K_{\lfloor n / 3 \rfloor})
\end{aligned}
$$

### General Form

$$
n = \lfloor n / 2 \rfloor + \lceil n / 2 \rceil
$$

For Merge Sort.

$$
\begin{aligned}
    f(1) & = 0 \\
    f(n) & = f(\lfloor n / 2\rfloor) + f(\lceil n / 2 \rceil) + n - 1, n \gt 1
\end{aligned}
$$

For Josephus Problem,

$$
\begin{aligned}
    J(1) &= 1\\
    J(n) &= 2J(\lfloor n / 2 \rfloor) - (-1)^n
\end{aligned}
$$

If we change to condition to "every three persons",

$$
J_3(n) = \left(\left\lceil \frac{3}{2} J_3\left(\left\lfloor\frac{2}{3}n\right\rfloor\right) +a_n \right\rceil \text{mod } n\right) + 1
$$

where $a_n = -2, 1, -\frac{1}{2}$ when $n \text{ mod } 3 = 0, 1, 2$

This is hard to solve.

However, we can use another method. Whenever a man is executed, we distribute new numbers for the remaining. $1$, $2$, $4$ to $n + 1, n + 2, n + 3$ and so on. (Or generally, $3k + 1, 3k + 2$ to $n + 2k + 1, n + 2k + 2$)

The last number should be $3n$.

Let $N \gt n$, then $N$ must has an original number. $N$ must be like $n + 2k + 1$ or $n + 2k + 2$. Therefore,
$$
k = \lfloor (N - n - 1) / 2\rfloor
$$
Since the number $N$ must be transferred from $3k + 1$ or $3k + 2$, therefore,
$$
N_0 = 3k + (N - n -2k) = k + N - n
$$ 

In algorithm view, 
```
N = 3n;
while N > n do N = floor((N - n - 1) / 2) + N - n;
J(n) = N
```
To simplify the form, let $D = 3n + 1 - N$

$$
\begin{aligned}
D &:= 3n + 1 - \left(\left\lfloor\frac{(3n + 1 - D) - n - 1}{2}\right\rfloor + (3n + 1 - D ) - n\right) \\
  &:=  n + D - \left\lfloor\frac{2n - D}{2}\right\rfloor\\
  &:= D - \left\lfloor\frac{-D}{2}\right\rfloor \\
  &:= D + \left\lceil\frac{D}{2}\right\rceil\\
  &:= \left\lceil\frac{3}{2}D\right\rceil
\end{aligned}
$$

In algorithm view,

```
D := 1;
while D <= 2n do D := ceil(3D/2);
J(n) = 3n + 1 - D
```
More generally, for any sequence defined as the following,

$$
\begin{aligned}
    D_0 &= 1\\
    D_n &= \left\lceil\frac{q}{q - 1} D_{n - 1}\right\rceil, n \gt 0  
\end{aligned}
$$

We can calculated it by
```
D := 1;
while D <= (q - 1) n do D := ceil(qD / q - 1);
J(n) = qn + 1 - D
```

## 'MOD': The Binary Operation
$$
x \text{ mod }y = x - y \lfloor x / y \rfloor, y \ne 0
$$

$$
x \text { mumble} y = y \lceil x / y \rceil - x
$$

### Distribution Law
$$
c(x \text{ mod } y) = (cx) \text{ mod } (cy) 
$$

**Proof**

$$
c (x\text{ mod }y) = c(x - y\lfloor x/ y \rfloor) = cx - cy\lfloor cx / cy \rfloor = cx \text{ mod } cy
$$

### Application: Average Grouping
separate $n$ items into $m$ lines, with $n \text{ mod } m$ long lines and $n \text{ mumble } m$ short lines.

Algorithm:
```
while m > 0:
    put ceil(n / m) items into one group
    n = n - ceil(n / m)
    m = m - 1
```
**Proof**

Let $n = qm + r$ (Division Thm).
- $r = 0$, trivially transform to
  $(n - 1) = q(m - 1)$
- $r > 0$, transform to
  $(n - q - 1) = q(m - 1) + (r - 1)$
Therefore, we keep the same $q$ and get an averaged division.

To get the number of items in $k$-th group:
$$
\left\lceil\frac{n - k +1}{m}\right\rceil
$$

Non-increasing partition:
$$
n = \sum_{k = 1}^m\left\lceil\frac{n-k + 1}{m}\right\rceil
$$

Non-decreasing partition:
$$
n = \sum_{k = 1}^m\left\lfloor\frac{n-k + 1}{m}\right\rfloor
$$

Actually, $\forall x \in \mathbb R$,
$$
\lfloor mx \rfloor = \sum_{k =0}^{m - 1}\left\lfloor x + \frac{k}{m}\right\rfloor
$$

## Floor/Ceiling Sums
### Sum Problem
$$
\sum_{0\le k \lt n} \left \lfloor \sqrt k \right \rfloor
$$
We can expand the sum,
$$
\begin{aligned}
\sum_{0\le k \lt n} \left \lfloor \sqrt k \right \rfloor &= \sum_{k, m \ge 0} m[m^2 \le k \lt (m + 1)^2 \le n] \\
&+ \sum_{k, m \ge 0} m[m^2 \le k \lt n \lt (m + 1)^2 ]
\end{aligned}
$$
Suppose $n = a^2$, the second summation will become zero, and the first one can be handled:
$$
\begin{aligned}
\sum_{0\le k \lt n} \left \lfloor \sqrt k \right \rfloor &= \sum_{k, m \ge 0} m[m^2 \le k \lt (m + 1)^2 \le n] \\
&= \sum_{k, m \ge 0} m[m^2 \le k \lt (m + 1)^2 \le a^2] \\
&= \sum_{k, m \ge 0} m\left((m + 1)^2 - m^2\right)[m + 1\le a] \\
&= \sum_{k, m \ge 0} m\left(2m + 1\right)[m \lt a] \\
&= \sum_{k, m \ge 0} \left(2m^{\underline 2} + 3m^{\underline 1}\right)[m \lt a] \\
&= \sum_0^a \left(2m^{\underline 2} + 3m^{\underline 1}\right) \delta m \\
&= \frac{1}{6}a(a - 1)(4a + 1)
\end{aligned}
$$
In general cases, let $a = \lfloor \sqrt n \rfloor$, what a have lost is just $(n - a^2)a$. Therefore, the final answer is:
$$
\sum_{0 \le k \lt n} \left\lfloor\sqrt k \right\rfloor = na - \frac{1}{3}a^3 - \frac{1}{2}a^2 - \frac{1}{6}a, a = \left\lfloor\sqrt n\right\rfloor
$$
Another method is to substitute $\lfloor x\rfloor$ by $\sum_j[1 \le j \le x]$, (also let $a^2 = n$)
$$
\begin{aligned}
\sum_{0\le k \lt n} \left \lfloor \sqrt k \right \rfloor &= \sum_{j, k}[1\le j \le k][0 \le k \lt a^2] \\
&= \sum_{1\le j \lt a}\sum_{k}[j^2 \le k \lt a^2] \\
&= \sum_{1\le j \lt a}(a^2 - j^2) = a^3 - \frac{1}{3}a(a + \frac{1}{2})(a + 1)
\end{aligned}
$$

### A Lemma from Bohl, Sierpinski & Weyl
$$
\forall \alpha \in \mathbb R \wedge \alpha \notin \mathbb Q, \lim_{n \to \infty} \frac{1}{n} \sum_{0\le k\lt n}f(\{k\alpha\}) = \int_{0}^1f(x)\text dx
$$
The lemma can be proved using:
$$
f_v = [0\le x \lt v]
$$
We now explore we $n$ is large enough, what is the discrepancy between $nv$ and
$$
\sum_{0\le k \lt n}[\{k\alpha\} \lt v]
$$
We define discrepancy $D(\alpha, n)$ as the maximum value of the following expression ($v \in [0, 1]$):
$$
s(\alpha, n, v) = \sum_{0\le k \lt n}([\{k\alpha\} < v] - v)
$$
This can be transformed into:
$$
\begin{aligned}
    \sum_{0\le k\lt n}([\{k\alpha\} \leq  v] - v)
&=  \sum_{0\le k\lt n}(\lfloor k\alpha\rfloor - \lfloor k\alpha - v\rfloor - v)
\end{aligned}
$$

## Another Application
$$
\sum_{0\le k \lt m} \left\lfloor\frac{nk + x}{m}\right\rfloor, m \in Z^+, n \in Z
$$
The close form is:
$$
d\left\lfloor\frac{x}{d}\right\rfloor + \frac{m - 1}{2}n + \frac{d- m}{2}
$$
So there is a symmetry between $m$ and $n$:
$$
\sum_{0\le k \lt m} \left\lfloor\frac{nk + x}{m}\right\rfloor =  \sum_{0\le k \lt n} \left\lfloor\frac{mk + x}{n}\right\rfloor 
$$