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

# Workshop 3: Functions

+++

## The Collatz Problem Revisited

Recall the Collatz Operation from Tutorial 1. Given an integer $n$, the next number in the Collatz sequence is:

 - if $n$ is even, divide it by two
 - if $n$ is odd, triple it and add one

Repeatedly applying the Collatz Operation results in a Collatz Sequence, which terminates once it reaches the number $1$.

The number of terms in the Collatz Sequence starting with $n$ is the Collatz Number of $n$. For example, for $n = 5$ the Collatz Sequence is $5, 16, 8, 4, 2, 1$ and the Collatz Number is $6$.

:::{exercise}
:label: exercise_3_6
Define a function `collatz_op(n)` that returns the next number in the Collatz Sequence. Check that your function returns the correct result for `n = 5` and `n = 6`.

```
def collatz_op(n):
    # replace with your code
```
:::

:::{exercise}
:label: exercise_3_7
Define a function `collatz_number` that returns the Collatz Number of `n`. Your function should use the function `collatz_op`.

```
def collatz_number(n):
    while n > 1:
        # Replace with your code to
        # calculate the Collatz number

    return num
```
:::

The [Wikipedia article](https://en.wikipedia.org/wiki/Collatz_conjecture) for the Collatz Conjecture contains [a graph](https://en.wikipedia.org/wiki/Collatz_conjecture#/media/File:Collatz5.svg) of the first $100$ Collatz Numbers.

:::{exercise}
:label: exercise_3_8
Create an array containing the first $100$ Collatz numbers. Then plot a line graph like the one in the Wikipedia article.


```
collatz_numbers = np.zeros(100)

# For i from 0 to 99
#   set the value of collatz_numbers[i]

# plot a line graph of collatz_numbers
```

:::


+++

## Investigating the SIR Model

In the previous tutorial, we wrote code that simulated the spread of an epdemic using the SIR model. We were able to investigate how the spread of the epidemic was influenced by parameters of the model - recovery rate $a$ and infection rate $b$.

:::{math}
:label: SIR_equations_2
\begin{align}S_{i+1} &= S_i - bS_iI_i\\
I_{i+1} &= I_i + bS_iI_i - aI_i.\end{align}
:::

Through policy interventions, the Government can influence the value of the parameter $b$. The government would like to understand how the value of $b$ affects the peak number of infections.

:::{exercise}
:label: exercise_3_9

Complete the code below so that it simulates the epidemic for 100 days using the parameter values $a = 0.1$ and $b = 0.00005$, and initial populations $S_0 = 20000$ and $I_0 = 100$. You can reuse your code from last week's exercise.

Then use the `numpy` function `np.max` to calculate peak infections (the maximum value of the array `I`).

Change the value of the parameter `b` and (by inspecting the graph of `I`) check that your calculated value of peak infections is correct.

```
import numpy as np
import matplotlib.pyplot as plt

n_days = 100
a = 0.1
b = 0.00005

# your code here
```
:::

Next, we'd like to produce a graph which shows how peak infections varies with the value of the infection rate parameter `b`. To do this, we will write a function `max_infected(a, b)` which calculates and returns the peak infections. 

:::{exercise}
:label: exercise_3_10
1. Write a function `max_infected(a, b)` which calculates and returns the maximum number of infected people over the course of the epidemic given parameter values `a` and `b`. Check that your function returns the expected values for `a = 0.1` and various values of `b`.
2. Use `np.linspace` to create an array `b_array` which contains a sequence of `10` evenly spaced numbers from  `0` to `0.00005`
3. Use `np.zeros` to create an empty array `peak_infections` of length `10`.
4. Use a loop to set the value of `peak_infections` for each value of `b` in `b_array`. 
5. Finally, create a plot to show how peak infections vary with infection rate.

```
def max_infected(a, b):
    # Run the simulation and calculate
    # the peak number of infections

b_array = # your code here
peak_infections = # your code here
for i in range(10):
    # Calculate the peak number of infections
    # for the given value of b

# Create a plot of peak infections against b

```
:::


+++

## Taking it Further

As well as the peak number of infected people, the government is interested in the *total* amount of medical care that will be required over the course of the epidemic. Assuming that each day, every infected person has an equal and independent probability of requiring medical care, then the total cost of medical care will be proportional to the sum of the number of infected people over all days. We call this the *infected person-days* and is simply the sum values in the array `I`.

:::{exercise}
:label: exercise_3_11
Write a function `total_infected(a, b)` which calculates and returns the total number of infected person-days for the duration of the epidemic.

Then, plot the total number of infections against $b$ for values between $0$ and $0.00005$.
:::

+++

Through public policy interventions such as vaccinations, the infection rate parameter $b$ can be reduced. However such interventions are costly. Goverment analysts estimate that the cost (in thousands of pounds) of interventions are given by the following formula:

$$ \mathrm{intervention~cost} = \frac{1}{5b} - 2000$$

where $b$ is the desired infection parameter.

Likewise, the cost of providing medical care (in thousands of pounds) is:

$$ \mathrm{medical~cost} = I$$

where $I$ is the total number infected person-days.

+++

:::{exercise}
:label: exercise_3_12
Calculate arrays `intervention_cost`, `medical_cost` containing the intervention and medical costs respectively over the range of `b` from $0$ to $0.0005$. Assume $a = 0.1$

Calculate an array `total_cost` which is the sum of the intervention and medical costs.

Plot all three on the same axes. Roughly what value of `b` minimises the total cost?
:::
