# Sums

## Notion Collection
$$
\pi(N) := \text{the number of primes that less equal than N}
$$

$$
\pi(N) \approx \ln\ln N + M \\
M \approx 0.261~497~212~847~642~783~755~426~838~608~695~859~051~566~6
$$

We can put proposition into $[~~]$:
$$
[p] = \begin{cases}
    1, p \\
    0, \neg p
\end{cases}
$$

## Sums and Recurrences
We can use the same method in sums:
$$
S_0 = \alpha \\
S_n = S_{n - 1} + \beta + \gamma n
$$
Write it in the form:
$$
S_n  = A(n)\alpha + B(n)\beta + C(n)\gamma
$$
Simply let $R_n = 1, n, n^2$ (more items for higher degree),
$$
A(n) = 1\\
B(n) = n,
C(n) = \frac{n(n + 1)}{2}
$$
Thus, for any sum in the form of $\sum_{i = 0}^n(a + bi)$, the close form will be:
$$
a(n + 1) + b\frac{n(n + 1)}{2}
$$

On the other hand, any recursion formula in the following form can be transformed into summation:
$$
a_n T_n = b_nT_{n - 1} +c_n
$$
Find a $s_n$, s.t.
$$
s_nb_n = s_{n - 1}a_{n - 1}
$$
Multiply $s_n$ on both side 
$$
s_n a_n T_n = s_nb_nT_{n - 1} +s_nc_n
$$
Let $S_n = s_na_nT_n$, then we get
$$
S_n = S_{n - 1} + s_nc_n
$$
Therefore,
$$
S_n = s_0a_0T_0 + \sum_{k = 1}^ns_kc_k = s_1b_1T_0 + \sum_{k = 1}^ns_kc_k
$$
The solution should be
$$
T_n = \frac{{s_1b_1T_0 + \sum_{k = 1}^ns_kc_k}}{s_na_n} 
$$
In fact, $s_n$ can be calculated by,
$$
s_n = C \times \frac{\prod_{1}^{n - 1}a_i}{\prod_{2}^{n}b_j}
$$
For example, for hanoi problem, $a_n = 1$, $b_n = 2$, then we can choose $s_n = 2^{-n}$


## Solve the Formula of Quick Sort
$$
C_0 = C_1 = 0\\
C_n = n + 1 + \frac{2}{n} \sum_{k = 1}^{n - 1}C_k, n \gt 1
$$
Solution:

multiply $n$ on both side:
$$
nC_n = n^2 + n + 2 \sum_{k = 1}^{n - 1}C_k 
$$
substitute $n$ with $(n - 1)$:
$$
(n - 1)C_{n - 1} = (n - 1)^2 + (n - 1) + 2 \sum_{k = 1}^{n - 2}C_k
$$
do subtraction of the two equations we have got:
$$
nC_n - (n - 1)C_{n - 1} = 2n + 2C_{n - 1}
$$
by simplification,
$$
C_0 = C_1 = 0\\
C_2 = 3\\
nC_n = (n + 1)C_{n - 1} + 2n
$$
Let $a_n = n, b_n = n + 1, c_n = 2n - 2[n = 1] + 2[n = 2]$, we can choose $s_n$ as
$$
s_n = \frac{2}{n(n + 1)}
$$
Then, the solution should be
$$
C_n = 2(n + 1)\sum_{k = 1}^n\frac{1}{k + 1} - \frac{2}{3}(n + 1)
$$
transform to harmonic numbers:
$$
\sum_{k = 1}^{n}\frac{1}{k + 1} = H_n - 1 + \frac{1}{n + 1} \\
C_n = 2(n + 1)H_n - \frac{8}{3}n - \frac{2}{3}, n \gt 1
$$

## Manipulation of sums
### properties of summation
$$
\sum ca_k = c\sum a_k \\
\sum (a_k + b_k) = \sum a_k + \sum b _k \\
\sum_{k \in K} a_k = \sum_{p(k) \in K} a_{p(k)}
$$

#### Example
$$
\begin{aligned}
S  &= \sum_{k = 0}^n(a + bk) \\
S  &= \sum_{n - k = 0}^n(a + b(n - k)) = \sum_{k = 0}^n(a + bn - bk) \\
2S &= \sum_{n - k = 0}^n(2a + bn)\\
S  &= (a + \frac{1}{2}bn)(n + 1) 
\end{aligned}
$$

### Perturbation Method
$$
S_n + a_{n + 1} = a_0 + \sum_{0 \le k \le n}a_{k + 1}
$$

#### Example
$$
S_n = \sum_{0 \le k \le n} ax^k
$$
by perturbation method,
$$
\begin{aligned}
S_n + ax^{n + 1} &= a + \sum_{0 \le k \le n}ax^{k + 1} \\
&= a + x\sum_{0 \le k \le n}ax^k\\
&= a + xS_n
\end{aligned}
$$
Then we get the close form.

## Multiple Sums
### Transformation
$$
\sum_{j\in J}\sum_{k \in K}a_{j, k} = \sum_{k\in K}\sum_{j \in J}a_{j, k} 
$$
and
$$
\sum_{j\in J}\sum_{k \in K(j)}a_{j, k} = \sum_{k\in K;}\sum_{j \in J'(k)}a_{j, k} \\
\text{where } [j \in J][k \in K(j)] = [k \in K'][j \in J'(k)]
$$
One particular useful transform is
$$
[1 \le j \le n][j \le k \le n] = [1 \le k \le n][1 \le j \le k]
$$

#### Example 1
$$
S_{\vartriangleleft} = \sum_{1 \le j \le k \le n} a_ja_k
$$
$$
S_{\vartriangleright} = \sum_{1 \le k \le j \le n} a_ja_k
$$
It is trivial that
$$
S_{\vartriangleright} = S_{\vartriangleleft}
$$
Also, we have
$$
[1 \le j \le k \le n] + [1 \le k \le j \le n] = [1 \le j, k \le n] + [1 \le j = k \le n]
$$
Therefore,
$$
2S_{\vartriangleright} = 2S_{\vartriangleleft} = \sum_{1 \le k, j \le n}a_ja_k + \sum_{1 \le k = j \le n}a_ja_k 
$$
Therefore,
$$
S_{\vartriangleleft} = \frac{1}{2}\left(\left(\sum_{k = 1}^n a_k \right)^2 + \sum_{k = 1}^n a_k^2\right)
$$
#### Example 2
$$
S = \sum_{1 \le j \lt k \le n} (a_k - a_j)(b_k - b_j)
$$
We have
$$
[1 \le j \lt k \le n] + [1 \le k \lt j \le n] = [1 \le j, k \le n] - [1 \le j = k \le n]
$$
Therefore,
$$
2S = \sum_{1 \le j , k \le n} (a_k - a_j)(b_k - b_j) - 2\sum_{1 \le j = k \le n} (a_k - a_j)(b_k - b_j) = \sum_{1 \le j , k \le n} (a_k - a_j)(b_k - b_j)
$$
Expand the result
$$
\begin{aligned}
&\sum_{1 \le j , k \le n}a_jb_j - \sum_{1 \le j , k \le n}a_jb_k - \sum_{1 \le j , k \le n}a_kb_j + \sum_{1 \le j , k \le n}a_kb_k \\
=& 2 \sum_{1 \le j , k \le n}a_kb_k - 2\sum_{1 \le j , k \le n}a_jb_k \\
=& 2n \sum_{1 \le k \le n}a_kb_k - 2\left(\sum_{1 \le k \le n}a_k\right)\left(\sum_{1 \le k \le n }b_k\right)
\end{aligned}
$$
We get
$$
\left(\sum_{1 \le k \le n}a_k\right)\left(\sum_{1 \le k \le n }b_k\right) = n \sum_{1 \le k \le n}a_kb_k - \sum_{1 \le j \lt k \le n} (a_k - a_j)(b_k - b_j)
$$

This is exactly a special form of **Chebyshev's monotonic inequality**:
$$
\left(\sum_{1 \le k \le n}a_k\right)\left(\sum_{1 \le k \le n }b_k\right) \le n \sum_{1 \le k \le n}a_kb_k, a_i \downarrow \wedge b_i\downarrow \\
\left(\sum_{1 \le k \le n}a_k\right)\left(\sum_{1 \le k \le n }b_k\right) \ge n \sum_{1 \le k \le n}a_kb_k, a_i \downarrow \wedge b_i\uparrow
$$

#### Attempts to Find the Close Form

##### Attempts 1
$$
\begin{aligned}
S_n &= \sum_{1 \le k \le n}\sum_{1\le j \lt k} \frac{1}{k - j}\\
    &= \sum_{1 \le k \le n}\sum_{1\le k - j \lt k} \frac{1}{j}\\
    &= \sum_{1 \le k \le n}\sum_{0\lt j \le k - 1} \frac{1}{j}\\
    &= \sum_{1 \le k \le n} H_{k - 1}
\end{aligned}
$$
failed
##### Attempts 2
$$
\begin{aligned}
S_n &= \sum_{1 \le j \le n}\sum_{j\lt k \le n} \frac{1}{k - j}\\
    &= \sum_{1 \le j \le n}\sum_{j\lt k + j \lt n} \frac{1}{k}\\
    &= \sum_{1 \le j \le n}\sum_{0\lt k \le n - j} \frac{1}{k}\\
    &= \sum_{1 \le j \le n} H_{n - j}\\
    &= \sum_{1 \le n - j \le n} H_{j}\\
    &= \sum_{0 \le j \lt n} H_{j}\\
\end{aligned}
$$
failed
##### Attempts 3
$$
\begin{aligned}
S_n &= \sum_{1 \le j\lt k \le n} \frac{1}{k - j}\\
    &= \sum_{1 \le j\lt k + j \le n} \frac{1}{k}\\
    &= \sum_{1 \le k \le n} \sum_{1\lt j \le n - k} \frac{1}{k}\\
    &= \sum_{1 \le k \le n} \frac{n - k}{k}\\
    &= \sum_{1 \le k \le n} \frac{n}{k} - \sum_{1 \le k \le n}1\\
    &= nH_n - n
\end{aligned}
$$
success!
$$
nH_n - n = \sum_{0 \le j \lt n} H_{j}
$$

## Finite Calculus
### Finite difference
$$
\Delta f(x) = f(x + 1) - f(x)
$$
### Factorial Power
#### Falling Factorial Power
$$
x^{\underline{m}} = x(x - 1)...(x - m + 1) 
$$
#### Rising Factorial Power
$$
x^{\overline{m}} = x(x + 1)...(x + m - 1) 
$$

### Property
Holder for both rising and falling
$$
\Delta x^{\underline{m}} = mx^{\underline{m - 1}}
$$

### Fundamental Thm
$$
g(x) = \Delta f(x) \iff \sum g(x) \delta x = f(x) + C
$$

### Bounded Finite Integral
$$
\sum_a^b f(x) \delta x = \sum_{a \le k \lt b} f(k)
$$

### Useful Formula
$$
\sum_{0 \le k \lt n}k^{\underline{m}} =\frac{k^{\underline{m + 1}}}{m + 1} (\text{from 0 to n}) = \frac{n^{\underline{m + 1}}}{m + 1}
$$

We can transform normal power to rasing/falling power and easily get to summation (using stirling numbers):
$$
k^2 = k^{\underline{2}} + k^{\underline 1} \\
k^3 = k^{\underline{3}} + 3k^{\underline{2}}  + k^{\underline 1}
$$

### Similarity to Infinite Calculus
$$
\sum_{a}^bx^{\underline{ m}}\delta x = \begin{cases}
\frac{x^{\underline{m + 1}}}{m + 1} \text{ from a to b}, m \ne -1 \\
H_x  \text{ from a to b}, m = 1
\end{cases}
$$
Thus,
$$
\ln x \simeq H_x \\
e^x \simeq 2^x 
$$

Define Shift Operator
$$
Ef(x) = f(x + 1)
$$
Then,
$$
\Delta(uv) = u\Delta v + Ev \Delta u
$$
Integration by part:
$$
\sum u \Delta v = uv - \sum Ev\Delta u
$$

We can now solve $\sum k2^k$ and $\sum kH_k$ easily.

