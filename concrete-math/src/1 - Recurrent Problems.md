# Recurrent Problems
## Hanoi
$$
T_0 = 0\\
T_n = 2T_{n - 1} + 1
$$
construct
$$
U_n = T_n + 1\\
$$
Then we have,
$$
U_0 = 1 \\
U_n = 2U_{n - 1}
$$

## Lines in the Plane
how many areas can $n$ lines divide at most?
$$
L_0 = 1 \\
L_n = L_{n - 1} + n
$$
We can just expand the formula,
$$
\begin{aligned}
L_n &= L_{n - 1} + n\\
    &= L_{n - 1} + (n - 1) + n\\
    &= L_0 + 1 + ... + n\\
    &= 1 + \frac{n (n + 1)}{2}
\end{aligned}
$$
What about broken lines with one turn?

regard one broken line as two lines with 2 areas lost.
$$
Z_n = L_{2n} - 2n = 2n^2 - n + 1
$$

## The Josephus Problem
$$
J(1) = 1 \\
J(2n) = 2J(n) - 1\\
J(2n + 1) = 2J(n) + 1\\
$$
By expanding, we can find
$$
J(2^m + l) = 2l + 1. m \ge 0, 0 \le l \lt 2^m
$$
**Proof (Induction)**

when $l$ is even,
$$
J(2^m + l) = 2J(2^{m - 1} + l / 2) - 1 = 2(2l / 2 + 1) - 1 = 2l + 1
$$
when $l$ is odd, use the fact $J(2n + 1) - J(2n) = 2$,
$$
J(2^m + l) = 2 + J(2^m + l - 1) = 2 + 2(l -1) + 1 = 2l + 1
$$

### Property
In Binary form, suppose,
$$
\begin{aligned}
n & = (1b_{m - 1}b_{m - 2}...b_1b_0)_2 \\
l & = (0b_{m - 1}b_{m - 2}...b_1b_0)_2 \\
2l & = (b_{m - 1}b_{m - 2}...b_1b_00)_2 \\
2l + 1 & = (b_{m - 1}b_{m - 2}...b_1b_01)_2 \\
J(n) & = (b_{m - 1}b_{m - 2}...b_1b_0b_m)_2 \\
\end {aligned}
$$

shift left in a loop, and we find the answer!

### Generalization

Suppose we have,
$$
f(1) = \alpha\\
f(2n) = 2f(n) + \beta , n \ge 1\\
f(2n + 1) = 2f(n) + \gamma, n \ge 1
$$
We can write down $f(n)$ in the following form,
$$
f(n) = A(n)\alpha + B(b)\beta + C(n)\gamma
$$
Let $n = 2^m + l, 0 \le l \lt 2^m$,
$$
\begin{aligned}
A(n) = 2^m\\
B(n) = 2^m - 1 - l & & &&&(*)\\ 
C(n) = l
\end{aligned}
$$ 


To get summarize this into a mature methodology, we return to this form:
$$
f(1) = \alpha\\
f(2n) = 2f(n) + \beta , n \ge 1\\
f(2n + 1) = 2f(n) + \gamma, n \ge 1
$$
subsitute $f(n) = 1$, we get:
$$
A(n) - B(n) - C(n) = 1 \\
$$
subsitute $f(n) = n$, we get:
$$
A(n)  + C(n) = n \\
$$
keep $\alpha = 1, \beta = \gamma = 0$, we get
$$
A(n) = 2^m
$$
Then we can get result $(*)$ just by solving these equations.

### Variant of Josephus Problem
$$
f(1) = \alpha\\
f(2n + j) = 2f(n) + \beta_j
$$
this can be expanded to
$$
\begin{aligned}
f((b_m b _{m - 1}...b_1b_0)_2) &= 2f((b_m b _{m - 1}...b_1)_2) + \beta_{b_0} \\
&= 2^m \alpha + 2^{m - 1}\beta_{b_{m - 1}} + ... + 2\beta_{b_1} + \beta_{b_0}  
\end{aligned}
$$

For an even general form, 
$$
f(j) = a_j, 1\le j \lt d\\
f(dn + j) = cf(n) + \beta_j, 0 \le j \lt d, n \ge 1
$$
We still have,
$$
f((b_m b_{m - 1} ... b_1b_0)_d) = (\alpha_{b_m}\beta_{b_{m - 1}}...\beta_{b_1}\beta_{b_0})_c
$$