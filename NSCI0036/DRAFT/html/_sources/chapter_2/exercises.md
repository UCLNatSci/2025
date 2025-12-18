---
jupyter:
  jupytext:
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.3'
      jupytext_version: 1.18.1
  kernelspec:
    display_name: Python 3.7.9 64-bit (microsoft store)
    language: python
    name: python3
---

# Exercises

:::{exercise} 
:label: rate_equations_extra_loops

Use a `for` loop to produce the following output:
1. `5, 7, 9, 11, 13, 15`
1. `1, 10, 100, 1000, 10000, 100000`
1. `0, 1, 2, 0, 1, 2, 0, 1, 2` (hint: use the `%` operator)

:::

:::{exercise}
:label: rate_equations_extra_weather

Look up the predicted daily maximum and minimum temperatures for the next 10 days according to the BBC weather forecast.

https://www.bbc.co.uk/weather/2643743

Create two arrays containing the maximum and minimum temperatures and plot them as two separate lines on a line graph, including axis labels and title. Look up how to add a legend in the [Matplotlib documentation](https://matplotlib.org/stable/users/index.html).

```{image} temperatures.png
:width: 300px
```

:::

:::{exercise}
:label: rate_equations_BZ_reaction

<!-- https://www3.nd.edu/~powers/mcdowell.pdf -->

The [Belousov–Zhabotinsky reaction](https://en.wikipedia.org/wiki/Belousov%E2%80%93Zhabotinsky_reaction), or BZ reaction, is a chemical reaction which exhibits non-equilbrium dynamics. Under certain conditions, the BZ reaction results in oscillatory behaviour, as demonstrated in [this video](https://www.youtube.com/watch?v=dMF4RjiITGM).

The BZ reaction can be modelled by the following equations, where $X_i$ and $Y_i$ are the concentrations of the two reactants X (red) and Y (colourless) at timestep $i$.

$$\begin{align}
X_{i+1} &= X_i + k_1-k_2X_i + k_3X_i^2Y_i\\
Y_{i+1} &= Y_i + k_4X_i - k_3X_i^2Y_i
\end{align}$$

where $k_1=0.2$, $k_2 = 0.4$, $k_3 = 0.1$ and $k_4 = 0.3$. The initial concentrations are zero and each timestep has a duration of one second.   

1. Write code to calculate $X_i$ and $Y_i$ for the first $300$ seconds. (Hint: you can use your answer to {numref}`exercise_2_8` as a template).
2. On on set of axes, plot a graph of $X$ and $Y$ against time, an in another on another plot $Y$ against $X$. Check that your plots look like the examples below. Notice how both $X$ and $Y$ reach a steady-state.
2. Keeping the other parameters fixed, experiment with different values of $k_1$ between $0.1$ and $0.3$. For what range of values of $k_1$ does the reaction reach a steady-state, and for which values dos it exhibit sustained oscillations?

:::

```python tags=["remove-input"]
# import necessary libraries
import numpy as np
import matplotlib.pyplot as plt

# set up variables and arrays
n = 300
k1 = 0.2
k2 = 0.4
k3 = 0.1
k4 = 0.3

X = np.zeros(n)
Y = np.zeros(n)

# initialise variables (not strictly necessary here!)
X[0] = 0
Y[0] = 0

# implement equations
for i in range(n - 1):
    X[i+1] = X[i] + k1 - k2*X[i] + k3*(X[i]**2)*Y[i]
    Y[i+1] = Y[i] + k4*X[i] - k3*(X[i]**2)*Y[i]

# plot so we can see what happens
plt.figure(figsize=(3,3))
plt.plot(X, label="X")
plt.plot(Y, label="Y")
plt.xlabel("Time (seconds)")    
plt.ylabel("Concentration")
plt.legend()
    
plt.figure(figsize=(3,3))
plt.plot(X, Y)
plt.xlabel("X concentration")
plt.ylabel("Y concentration");
  
```
