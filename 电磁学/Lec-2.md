# Lec-2 More on Charge and Field

- Conservation
- Distribution in Atoms

## Measure 

Using Coulomb‘s Law.
$$
\vec{F} = k\frac{q_1q_2}{r^2} = \frac{1}{4\pi\epsilon_0}\frac{q_1q_2}{r^2} \\
k = 9\times 10 ^ 9 N/C \\
\varepsilon = 8.85 \times10^{-12}
$$

## Electric Field

Vector Field
$$
\vec{\mathbf E} = \frac{1}{4\pi r} \frac{q}{r^2} \hat{\mathbf r}
$$
Electric Field by a source point charge $q$. This equation is for a unit charge at a particular point.

**The Magic Number:**
$$
\alpha = \frac{1}{4\pi \varepsilon_0}\frac{e^2}{\hbar c} = 137
$$

- Point Charge Electric Field

- Superposition Law

- Electric Field Line (Distinguish From Trajectory Line)

- Density of Electric Field

- Field of Dipoles

- - positive/negative - **cubic law**

  - Far away - **Equivalent Single Change Model**

  - Calculation (for a Dipole):

    - Set Up a $xy z- coordinate$ system, set the origin in the middle point of the line determined by the two charges.

    - Select $P(x, y, z)$

    - let $\hat {\mathbf {r}} = \vec{OP}$

    - $|r| = \sqrt{x^2  + y^2 + z^2}$

    - To calculate $E_+ $, do coordinate transformation to the positive charge.

$$
\begin{cases}
x' = x - a\\
y' = y\\
z' = z\\
\end{cases}
$$





$|BP| = \sqrt{(x- a)^2 + y^2  +z^2}$, 
​    
$\vec {\mathbf {E}_p} = \frac{q}{4\pi\epsilon|BP|^2}$
$$
\begin{cases}
E_x = E_p\sin\theta \cos\phi \\
E_y = E_p\cos\theta \\
E_z = E_p\sin\theta\sin\phi \\
\sin \theta = \frac{\sqrt{x'^2 + z'^2}}{|BP|} \\
\cos \theta = \frac{y'}{|BP|} \\
\sin \phi = \frac{z'}{\sqrt{x'^2 + x'^2}} \\
\cos \phi = \frac{x'}{\sqrt{x'^2 + z'^2}} \\
\end{cases}
\Rightarrow
\begin{cases}
E_x = \frac{q}{4\pi\epsilon|BP|^2} \frac{x'}{|BP|} \\
E_y = \frac{q}{4\pi\epsilon|BP|^2} \frac{y'}{|BP|} \\
E_z = \frac{q}{4\pi\epsilon|BP|^2} \frac{z'}{|BP|} \\
\end{cases}
\Rightarrow E_+ = \frac{q}{4\pi\varepsilon}\frac{(x - a)\hat i + y\hat j + z\hat k} {[(x-a)^2 + y^2 + z^2]^\frac{3}{2}}
$$

$$
      E_- = -\frac{q}{4\pi\varepsilon}\frac{(x + a)\hat i + y\hat j + z\hat k}{{[(x+a)^2 + y^2 + z^2]^\frac{3}{2}}}
$$


$$
|r| >> a, E = \frac{q}{4\pi\varepsilon}[\frac{\vec r - a\hat i}{(r^2 - 2ax)^\frac{3}{2}} -\frac{\vec r +a\hat i}{(r^2 +2ax)^\frac{3}{2}}] = \frac{q}{4\pi\varepsilon}[-\frac{\vec{p}}{r^3} + \frac{3(\vec p \cdot\vec r)\vec r}{r^3}], \vec p = |q| d, 
\\(Taylor\ Expansion)
$$

How about:
$$
\begin{aligned}
U &= U_+ - U_-\\
&= \frac{q}{4\pi\varepsilon}[\frac{1}{\sqrt{(x- a)^2 + y^2 + z^2}} - \frac{1}{\sqrt{(x+ a)^2 + y^2 + z^2}}]\\
\vec{E} &= \nabla U \\
&= \frac{\partial U}{\partial x} \hat i + \frac{\partial U}{\partial y} \hat j + \frac{\partial U}{\partial z} \hat k \\
&=\frac{q}{4\pi\varepsilon}[\frac{(x - a)i\hat + y\hat j + z\hat k}{[(x- a)^2 + y^2 + z^2]^\frac{3}{2}} - \frac{(x + a)i\hat + y\hat j + z\hat k}{[(x+ a)^2 + y^2 + z^2]^\frac{3}{2}}]
\end{aligned}
$$

## Detail about Taylor Expansion:

$$
(r^2 - 2ax)^\frac{3}{2} = r^3(1 - \frac{2ax}{r^2})^\frac{3}{2} \approx r^3(1 - \frac{3ax}{r^2}) = r^3 - 3axr \\
(r^2 + 2ax)^\frac{3}{2} = r^3(1 + \frac{2ax}{r^2})^\frac{3}{2} \approx r^3(1 + \frac{3ax}{r^2}) = r^3 + 3axr \\
\\\therefore 
\begin{aligned}
\frac{4\pi\epsilon E}{q} &= \frac{\vec r - a\hat i}{r^3 - 3axr} - \frac{\vec r + a\hat i}{r^3 + 3axr}\\
&= -a\hat i(\frac{1}{r^3 - 3axr} + \frac{1}{r^3 + 3axr}) +  |r|\hat r(\frac{1}{r^3 - 3axr} - \frac{1}{r^3 + 3axr})\\
&= -a\hat i(\frac{2r^3}{r^6 - 9a^2x^2r^2}) +  \hat r(\frac{6axr}{r^5 - 9a^2x^2r^2})
\end{aligned}\\
$$

Notice that:
$$
x = \vec{r}\cdot \hat i\\
\vec r = r \hat r\\
\vec p = 2qa\hat i
$$
Then we can derive the final answer.

