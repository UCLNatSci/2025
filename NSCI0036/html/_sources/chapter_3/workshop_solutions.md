---
jupytext:
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.18.1
kernelspec:
  display_name: Python 3.7.9 64-bit
  language: python
  name: python3
---

# Workshop 3: Solutions

## Exercise 1

In order to decide how to calculate the next term in the sequence, we need to work out whether $n$ is even or odd. Recall from tutorial 1 that we can use the modulus operator `%` to find the remainder after floor division. So if $n % 2$ is equal to $0$ then $n$ must be even.

```{code-cell} ipython3
def collatz_op(n):
    if (n % 2) == 0:     # check if n is even
        next_term = n / 2
    else:                # must be odd
        next_term = (n * 3) + 1 
    
    return next_term
```

We can check the function works by trying it out for `n = 5` and `n = 6`. When `n = 5` we triple it and add `1`, so the next term if 16. When `n = 6` we divide it by two so the next term is `3`. 

```{code-cell} ipython3
print(collatz_op(5))
print(collatz_op(6))
```

## Exercise 2

To calculate the Collatz Number of `n` we need to iteratively calculate the next term in the sequence until we get to `1` and calculate how many iterations we used. Note that the Collatz Number of `1` is `1`, so the counter should be initialised to `1`.

```{code-cell} ipython3
def collatz_number(n):
    num = 1
    while n > 1:
        num += 1
        n = collatz_op(n)
    
    return num
```

Let's check this works using `n = 5` and `n = 6`. We know that the Collatz Number of $5$ is $6$. When $n$ is $6$, the Collatz Sequence is $6, 3, 10, 5, 16, 8, 4, 2, 1$ so the Collatz Number is $9$.

```{code-cell} ipython3
print('The Collatz Number of 5 is ', collatz_number(5))
print('The Collatz Number of 6 is ', collatz_number(6))
```

## Exercise 3

```{code-cell} ipython3
import numpy as np
import matplotlib.pyplot as plt

collatz_numbers = np.zeros(100)

for i in range(100):
    collatz_numbers[i] = collatz_number(i + 1)

# remember to plot the collatz numbers against 1-100, not 0-99
plt.figure(figsize=(4,4))
plt.plot(np.linspace(1, 100, 100), collatz_numbers)
plt.title('First 100 Collatz Numbers')
plt.xlabel('n')
plt.ylabel('Collatz Number')
```

## Exercise 4

Using our code from last week, we just need to make a little addition to calculate peak infections:

```{code-cell} ipython3

import numpy as np
import matplotlib.pyplot as plt

# set up variables and arrays
n_days = 100
a = 0.1
b = 0.00005
S = np.zeros(n_days)
I = np.zeros(n_days)

# initialise the variables
S[0] = 20000
I[0] = 100

# implement equations
for i in range(n_days - 1):
    S[i+1] = S[i] - (b * S[i] * I[i])
    I[i+1] = I[i] + (b * S[i] * I[i]) - (a * I[i])

# plot the figure
plt.figure(figsize=(5,5))
plt.plot(I)
plt.plot(S)
plt.xlabel("Time (days)")
plt.ylabel("Population")


# check the maximum 
peak_infections = np.max(I)
print('For infection rate', b, 'infections peak at', peak_infections, 'cases.')
```

Looking at the graph, infections peak at around $15000$ cases, which is similar to what we find frpom `np.max`. Let's check for another value of $b$.

```{code-cell} ipython3
import numpy as np
import matplotlib.pyplot as plt

# set up variables and arrays
n_days = 100
a = 0.1
b = 0.00001
S = np.zeros(n_days)
I = np.zeros(n_days)

# initialise the variables
S[0] = 20000
I[0] = 100

# implement equations
for i in range(n_days - 1):
    S[i+1] = S[i] - (b * S[i] * I[i])
    I[i+1] = I[i] + (b * S[i] * I[i]) - (a * I[i])

# plot the figure
plt.figure(figsize=(5,5))
plt.plot(I)
plt.plot(S)
plt.xlabel("Time (days)")
plt.ylabel("Population")


# check the maximum 
peak_infections = np.max(I)
print('For infection rate', b, 'infections peak at', peak_infections, 'cases.')
```



This time, both from `np.max` and by visually inspecting the graph we see that the peak number of infections is much lower. 

## Exercise 5

1. First we need to write a function that will return the maximum number of infected people for different parameter values. We can just modify the code above so that it is inside a function:

```{code-cell} ipython3
def max_infected(a, b):
    # Run the simulation and calculate
    # the peak number of infections
    
    # set up variables and arrays
    n_days = 100
    S = np.zeros(n_days)
    I = np.zeros(n_days)

    # initialise the variables
    S[0] = 20000
    I[0] = 100

    # implement equations
    for i in range(n_days - 1):
        S[i+1] = S[i] - (b * S[i] * I[i])
        I[i+1] = I[i] + (b * S[i] * I[i]) - (a * I[i])
        
    # check the maximum 
    peak_infections = np.max(I)
    
    return peak_infections
```

We can check this works by calling the function for `a = 0.1` and the values of `b` we tested above. For example:

```{code-cell} ipython3
max_infected(0.1, 0.00005)
```

returns $14873$, as we expect!

2\. Recall from last week that to generate `10` evenly spaced numbers from  `0` to `0.00005` we can use:

```{code-cell} ipython3
b_array = np.linspace(0, 0.00005, 10)
```

3\. Again, recall from last week that we can create an array containing 10 zeros:

```{code-cell} ipython3
peak_infections = np.zeros(10)
```

4\. We have also seem how to use a loop to set a value in an array - notice that we need to retrieve each value of `b` to test from `b_array`. 

```{code-cell} ipython3
for i in range(10):
    # Calculate the peak number of infections
    # for the given value of b
    peak_infections[i] = max_infected(0.1, b_array[i])
```

5\. Now we just need to plot the `peak_infections` array against `b_array` to see how peak infections vary with the infection parameter.

```{code-cell} ipython3
# Create a plot of peak infections against b
plt.figure(figsize=(4,4))
plt.plot(b_array, peak_infections)
plt.title('Peak infection size against infection rate')
plt.xlabel('Infection rate')
plt.ylabel('Peak infection')
```

Putting this altogether we have:

```{code-cell} ipython3
def max_infected(a, b):
    # Run the simulation and calculate
    # the peak number of infections
    
    # set up variables and arrays
    n_days = 100
    S = np.zeros(n_days)
    I = np.zeros(n_days)

    # initialise the variables
    S[0] = 20000
    I[0] = 100

    # implement equations
    for i in range(n_days - 1):
        S[i+1] = S[i] - (b * S[i] * I[i])
        I[i+1] = I[i] + (b * S[i] * I[i]) - (a * I[i])
        
    # check the maximum 
    peak_infections = np.max(I)
    
    return peak_infections

b_array = np.linspace(0, 0.00005, 10)
peak_infections = np.zeros(10)

for i in range(10):
    # Calculate the peak number of infections
    # for the given value of b
    peak_infections[i] = max_infected(0.1, b_array[i])

# Create a plot of peak infections against b
plt.figure(figsize=(4,4))
plt.plot(b_array, peak_infections)
plt.title('Peak infection size against infection rate')
plt.xlabel('Infection rate')
plt.ylabel('Peak infection')
```

As we expect, as the infection rate grows so does the peak infection!

+++

## Exercise 6

We can use the function `np.sum` to sum the values in an array. To find out the total number of infected person-days we just need to sum the values in `I` - so we just need to make a small tweak to the `max_infected` function we wrote above:

```{code-cell} ipython3
def total_infected(a, b):
    # Run the simulation and calculate
    # the total number of infections

    # set up variables and arrays
    n_days = 100
    S = np.zeros(n_days)
    I = np.zeros(n_days)

    # initialise the variables
    S[0] = 20000
    I[0] = 100

    # implement equations
    for i in range(n_days - 1):
        S[i+1] = S[i] - (b * S[i] * I[i])
        I[i+1] = I[i] + (b * S[i] * I[i]) - (a * I[i])

    # check the total - sum instead of max!
    total_infections = np.sum(I)

    return total_infections
```

This code is tricky to test as it is not easy to see the total infected person-days from the graph! However, when $b = 0$ and $a = 1$, the equations reduce to 
:::{math}
:label: SIR_equations_exercise
\begin{align}S_{i+1} &= S_i \\
I_{i+1} &= 0.\end{align}
:::

so everyone recovers after just $1$ day, and no one else is infected. This means the total infected person-days for these parameter values should be $100$ - let's check!

```{code-cell} ipython3
total_infected(1, 0)
```

Now we just need to plot the total infected person-days for different values of $b$ - just like we did above:

```{code-cell} ipython3
# set up variables and arrays
b_array = np.linspace(0, 0.00005, 10)
total_infections = np.zeros(10)

for i in range(10):
    # Calculate the total number of infections
    # for the given value of b
    total_infections[i] = total_infected(0.1, b_array[i])

# Create a plot of total infections against b
plt.figure(figsize=(4,4))
plt.plot(b_array, total_infections)
plt.title('Total infection size against infection rate')
plt.xlabel('Infection rate')
plt.ylabel('Total infection size')
```
## Exercise 7

As above, let's check the costs for 10 values of $b$ in the range $0$ to $0.00005$. We need to set up arrays to contain the costs and then calculate the corresponding cost for each value of $b$.

Notice that when $b = 0$ the formula suggests the intervention cost will be infinite - Python cannot handle dividing by zero (try it!) and will throw an error. To get around this, we can use `np.linspace` to set up the array for $b$ as normal, and then just make the first element non-zero (but still small). 

Also notice that rather than initialising a third array and calculating each element of `total_cost` one by one, we have just been able to add the `intervention_cost` and `medical_cost` arrays together - this works because they are both the same size!

```{code-cell} ipython3
# set up variables and arrays
b_array = np.linspace(0, 0.00005, 10)
intervention_cost = np.zeros(10)
medical_cost = np.zeros(10)

# avoid b = 0
b_array[0] = 0.000001

for i in range(10):
    intervention_cost[i] = 1/(5 * b_array[i]) - 2000
    medical_cost[i] = total_infected(0.1, b_array[i])

# add up the total cost
total_cost = intervention_cost + medical_cost

# Create a plot of costs against b
plt.figure(figsize=(4,4))
plt.plot(b_array, intervention_cost)
plt.plot(b_array, medical_cost)
plt.plot(b_array, total_cost)
plt.title('Costs against infection rate')
plt.xlabel('Infection rate')
plt.ylabel('Cost (thousands of £s)')
```

Examining the graph, we can see that costs are minimised when $b \approx 5 \times 10^{-6}$.

## Exercise 8

First, to run the simulation we can use the same approach as last week.

```{code-cell} ipython3
# import necessary libraries
import numpy as np
import matplotlib.pyplot as plt

# set up variables and arrays
n = 1001
k1 = 0.1
k2 = 0.4
k3 = 0.1
k4 = 0.2

X = np.zeros(n)
Y = np.zeros(n)

# initialise variables (not strictly necessary here!)
X[0] = 0
Y[0] = 0

# implement equations
for i in range(n - 1):
    X[i+1] = X[i] + k1 - k2*X[i] + k3*(X[i]**2)*Y[i]
    Y[i+1] = Y[i] + k4*X[i] - k3*(X[i]**2)*Y[i]

# plot on the same figure
plt.figure(figsize=(5,5))
plt.plot(X)
plt.plot(Y)
```

### Determine the steady state

We are told that the system is in equilibrium after $1000$ steps (and we can see from the figure that oscillations are not visible after about 600 steps), so to determine the steady state value of $X$ we just need to check the value of $X_{1000}$.

```{code-cell} ipython3
print('The steady state value of X is', X[1000])
```

### Turning into a function

As we saw in the tutorial, we just need to wrap our existing code in a few extra lines to turn it into a function that can handle lots of values of $k_4$. 

```{code-cell} ipython3
def steady_state_X(k1, k2, k3, k4):
    # set up variables and arrays
    n = 1001

    X = np.zeros(n)
    Y = np.zeros(n)

    # initialise variables (not strictly necessary here!)
    X[0] = 0
    Y[0] = 0

    # implement equations
    for i in range(n - 1):
        X[i+1] = X[i] + k1 - k2*X[i] + k3*(X[i]**2)*Y[i]
        Y[i+1] = Y[i] + k4*X[i] - k3*(X[i]**2)*Y[i]
        
    #return the steady state
    return(X[1000])
```

To test this we can check it returns the same value as above for $k_1=0.1$, $k_2=0.4$, $k_3=0.1$ and $k_4=0.2$.

```{code-cell} ipython3
print("The steady state value of X is", steady_state_X(0.1, 0.4, 0.1, 0.2))
```

As we expected!

### Explore behaviour for changing $k_4$

We would like to explore how the steady state value of $X$ changes for values of $k_4$ between $0$ and $0.3$. We did something similar in the tutorial, so we can modify our existing code:


```{code-cell} ipython3
# set up variables and arrays
k4_array = np.linspace(0, 0.3, 1000)
steady_state = np.zeros(1000) # be careful not to give this the same name as the function!

for i in range(1000):
    # Calculate the steady state value of X
    # for the given value of k_4
    steady_state[i] = steady_state_X(0.1, 0.4, 0.1, k4_array[i])

# Create a plot of steady state values against k_4 values
plt.figure(figsize=(4,4))
plt.plot(k4_array, steady_state)
plt.title('Steady state value against k_4')
plt.xlabel('k_4')
plt.ylabel('Steady state value')
```

We can see that as $k_4$ increases from $0$ to $0.2$, the steady state value also gradually increases. When $k_4$ is larger than $0.2$ the steady state value appears to oscillates rapidly. This is because for values of $k_4$ above about $0.2$, the system doesn't reach a steady state.

```{code-cell} ipython3
def max_X(k1, k2, k3, k4):
    # set up variables and arrays
    n = 1001

    X = np.zeros(n)
    Y = np.zeros(n)

    # initialise variables (not strictly necessary here!)
    X[0] = 0
    Y[0] = 0

    # implement equations
    for i in range(n - 1):
        X[i+1] = X[i] + k1 - k2*X[i] + k3*(X[i]**2)*Y[i]
        Y[i+1] = Y[i] + k4*X[i] - k3*(X[i]**2)*Y[i]
        
    #return the steady state
    return(np.max(X))

# set up variables and arrays
k4_array = np.linspace(0, 0.3, 1000)
steady_state = np.zeros(1000) 
max_X_array = np.zeros(1000)

for i in range(1000):
    # Calculate the steady state value of X
    # for the given value of k_4
    steady_state[i] = steady_state_X(0.1, 0.4, 0.1, k4_array[i])
    max_X_array[i] = max_X(0.1, 0.4, 0.1, k4_array[i])

# Create a plot of steady state and max values against k_4 values
plt.figure(figsize=(4,4))
plt.plot(k4_array, steady_state, label="steady state")
plt.plot(k4_array, max_X_array, label="maximum")
plt.title('Steady state and maximum value against k_4')
plt.xlabel('k_4')
plt.ylabel('concentration')
plt.legend()
```

## Exercise 9

One possible solution is shown below, but please read further for a critique of the solution.

```{code-cell} ipython3
import numpy as np
import matplotlib.pyplot as plt

def is_divisible(n, m):
    return n % m == 0

def is_prime(n):
    result = True
    for i in range(2, n):
        if is_divisible(n, i):
            result = False
    return result

def number_of_primes(n):
    result = 0
    for i in range(2, n+1):
        if is_prime(i):
            result += 1
    return result

n_max = 50
total_primes = np.zeros(n_max)
for i in range(2, n_max):
    total_primes[i] = number_of_primes(i)

print(total_primes)

plt.plot(total_primes)
```

### Comments

1\. The function `is_divisible` is only one line. Perhaps it would better to integrate this code directly into the `number_of_primes` function, although I think including a separate function makes the code clear and easy to understand.  
2\. Another way to write the `is_prime` function, making use of the fact that the `return` statement causes the function to exit immediately (even in the middle of a loop):  
```
def is_prime(n):
    for i in range(2, n):
        if is_divisible(n, i):
            return True
    return False
```
3\. The function `is_prime` doesn't work correctly in the case that `n = 0` or ` n = 1`. This meant that I had to start my loop at 2 `for i in range(2, n_max):`. Perhaps it would  be neater to change the `is_prime` function so that it returns `False` in these cases, although it would probably have to treat `0` and `1` as special cases.  
4\. The line `plt.plot(total_primes)` only has one function argument, which means that the x values are automatically the index range of the array `total_primes` i.e. `0` ... `n_max-1`.  
5\. A line graph isn't the best choice here. We could instead plot individual points as below.  
6\. This code is very inefficient because we have to call `is_prime` repeatedly for each number. You could avoid this inefficiency by refactoring the code and using the numpy function `cumsum`.

```{code-cell} ipython3
x_array = np.arange(0, n_max, 1)
plt.scatter(x_array, total_primes)
```