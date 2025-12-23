---
jupytext:
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.18.1
kernelspec:
  display_name: Python 3 (ipykernel)
  language: python
  name: python3
---

# Workshop 2: Modelling Change

+++


## Introduction

A **difference equation** defines a sequence by the difference between consecutive terms. To fully specify the sequence we also need an initial value. For example,

$$x_{i+1} = x_i + 0.1x_i \quad\mathrm{where}\quad x_0=10$$

defines a sequence where the initial value is $10$ and each term is $10\%$ bigger than the previous term.

Let's calculate the first 5 terms using Python. First, we create an array and set its first element to the initial value $10$.

```{code-cell} ipython3
import numpy as np

x = np.zeros(5)

x[0] = 10
print("x:", x)
```

Next we use a `for` loop to calculate the remaining terms of the sequence.

```{code-cell} ipython3
for i in range(4):
    x[i+1] = x[i] + 0.1*x[i] 
    
print("x:", x)
```

:::{exercise}
:label: exercise_2_6

The array `x` has $5$ elements yet the upper limit of the `for` loop is $4$. Why? Try changing the upper limit to $5$ and see what happens.
:::

Finally, we would like to plot a graph of the first $5$ terms of the sequence. To do this we need to import a library, `matplotlib.pyplot`:

```{code-cell} ipython3
import matplotlib.pyplot as plt

plt.figure(figsize=(3,3))
plt.plot(x)
plt.xlabel("i")
plt.ylabel("x[i]")
```

:::{exercise}
:label: exercise_2_7

Calculate the value of $x_{16}$. Print the answer as follows:

```x[16]: XXXX```

:::

## Multiple Variables

We can produce more interesting behaviour if we introduce a second variable. For example,

$$\begin{align*}
x_{i+1} &= x_i - 0.5y_i\\
y_{i+1} &= y_i + 0.4x_i\quad\mathrm{where}~x_0=y_0=10.
\end{align*}$$

:::{exercise}
:label: exercise_2_8

Complete the following code to calculate and plot `x` and `y` over the range `0 ... 19`. Plot the resulting arrays on the same figure.

```
x = np.zeros(20)
x[0] = 10

# create array y and set initial value

for i in range(19):
    x[i+1] = x[i] - 0.5 * y[i]  

    # set value of y[i+1]

plt.figure(figsize=(3,3))
plt.plot(x)

# plot y on the SAME graph    
```
:::


+++

## SIR Model of Epidemics

The spread of an infectious disease amongst a population can be modelled by the SIR model. We divide the the population into three groups: Susceptible, Infected and Recovered. As the epidemic progresses, the number of people in each group changes according to a set of simple rules. Let $S_i$ represent the number of susceptible people and $I_i$ the number of infected people on day $i$. Then:

:::{math}
:label: SIR_equations
\begin{align}S_{i+1} &= S_i - bS_iI_i\\
I_{i+1} &= I_i + bS_iI_i - aI_i.\end{align}
:::

We assume a fixed total population so that the number of people in the Recovered group is given by

$$R_i = N - (S_i + I_i)$$

where $N$ is the total population. There are two parameters: the recovery rate parameter $a$ and the infection rate parameter $b$.

+++

### Simplified Model

First, let's examine a simplified version of this model where we assume that there are no susceptible people in the population and an initial population $I_0$ of infected people. Then, the equations reduce to:

$$ I_{i+1} = I_i - aI_i $$

A fixed proportion $a$ of the infected population recovers at each time step. Let's suppose that 10% of the population recovers each day so that $a=0.1$, and assume that our population starts with $I_0=1000$ infected people.

:::{exercise}
:label: exercise_2_9

Calculate (by hand) the first few terms of the sequence. What would you expect the graph $I_i$ to look like?

Write Python code to model the number of infected people for $100$ days. Plot a graph of $I_i$.
:::

+++

### Full Model

Next we will model the full set of two equations {eq}`SIR_equations`. We'll assume that parameter values $a = 0.1$ and $b = 0.00005$ and the initial populations $S_0 = 20000$ and $I_0 = 100$.

:::{exercise}
:label: exercise_2_10

Adapt your code to model the full set of equations with parameter values and initial conditions as described above.

Hint: You should see that the number of infected people peaks at around 15,000 at about day 15, while the number of susceptible people drops to about zero at about the same time.
:::

### Investigating the Model

One of the benefits of modelling is that we can investigate the effect of changing particular parameters. For example, the Government can influence the rate parameter $b$ through public policy (for example the imposition of social distancing, vaccination or other measures) and so it would like to understand how changing the value of $b$ affects the outcome of the epidemic.

+++

:::{exercise}
:label: exercise_2_11

Experiment with various values of $b$ to see how it affects the outbreak. Roughly what is the minimum value of $b$ which results in an epidemic? (We say there is an epidemic if $I_i$ initially rises to a peak, however small).

Then *on one graph* plot $I_i$ for 4 different values of $b$ (use a loop!).

:::

## Ballistics

Suppose a cannon located at position $x = 0, y = 0$ fires a cannonball at an angle $\theta$ from the horizontal (measured in radians) and speed $s$ m/s. We'd like to simulate the trajectory of the cannonball as in {numref}`cannon-fig`.

```{figure} cannon.jpg
---
height: 150px
name: cannon-fig
---

The trajectory of a cannonball fired at an angle $\theta$ from the horizontal and speed $s$ m/s.

```

We can model the motion of the cannonball using four variables: The x- and y-positions of the cannonable $x_i$ and $y_i$, and the x- and y-velocities of the cannonball $u_i$ and $v_i$. Assuming a fixed simulation timestep $\Delta t$, we update the positions as below:

$$
\begin{align*}
x_{i+1} &= x_i + u_i\Delta t \\
y_{i+1} &= y_i + v_i\Delta t.
\end{align*}
$$

The x-velocity $u_i$ is constant, and the y-velocity changes due to the gravitational acceleration $g=9.81$ m/s.

$$
\begin{align*}
u_{i+1} &= u_i\\
v_{i+1} &= v_i - g\Delta t
\end{align*}
$$


```{exercise}
:label: exercise_2_12

Assuming that $s = 100$ m/s and that $\theta= \pi/4$, write a program which plots a graph of the cannonball's trajectory. 

 - Use trigonometry to calculate the initial velocities
 - Make sure that $y$ does not go below zero (use an `if` statement or the `max` function)
 - You'll need to choose a suitable value for the timestep $\Delta t$

```
