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

# Workshop 2: Solutions

```{code-cell} ipython3
import numpy as np
import matplotlib.pyplot as plt
```

## Exercise 1

The updated code is:

```{code-cell} ipython3
:tags: ["raises-exception"]
x = np.zeros(5)

x[0] = 10
print("x:", x)

for i in range(5):
    x[i+1] = x[i] + 0.1*x[i] 
    
print("x:", x)
```

If we try and run this we see `IndexError: index 5 is out of bounds for axis 0 with size 5`. 

When we increase the upper limit to $5$ the final value that is passed through the for loop is `i = 4`.
Remember that arrays are indexed from $0$, so `x[n]` will try to access the (n+1)th element of `x`.  

So when `i = 4` the line `x[i+1] = x[i] + 0.1*x[i]` looks for the element of `x` at index $5$, which is the _$6$th_ element of `x`. 
But `x` only has $5$ elements! So Python is warning us that we are trying to access an element of an array that does not exist - i.e. it is **out of bounds**.

## Exercise 2

First we need to extend the for loop from above. To get $x_{16}$ we will need to calculate 17 terms of the sequence - remember that the first term is $x_0$.

```{code-cell} ipython3
x = np.zeros(17)

x[0] = 10

for i in range(16):
    x[i+1] = x[i] + 0.1*x[i] 
    
print("x[16]:", x[16]) 
```

## Exercise 3


```{code-cell} ipython3
x = np.zeros(20)
x[0] = 10

# create array y and set initial value
y = np.zeros(20)
y[0] = 10

for i in range(19):
    x[i+1] = x[i] - 0.5 * y[i]  

    # set value of y[i+1]
    y[i+1] = y[i] + 0.4 * x[i]

plt.figure(figsize=(3,3))
plt.plot(x)

# plot y on the SAME graph
plt.plot(y)
```

## Exercise 4

- $I_0 = 1000$
- $I_1 = I_0 - 0.1*I_0 = 1000 - 100 = 900$
- $I_2 = I_1 - 0.1*I_1 = 900 - 90 = 810$
- $I_3 = I_2 - 0.1*I_2 = 810 - 81 = 729$
and so on...

```{code-cell} ipython3
n_days = 100

I = np.zeros(n_days)

I[0] = 1000

for i in range(n_days - 1):
    I[i+1] = I[i] - 0.1 * I[i]

plt.figure(figsize=(5,5))
plt.plot(I)
plt.xlabel("Time (days)")
plt.ylabel("Infected population")
```

## Exercise 5

```{code-cell} ipython3
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

plt.figure(figsize=(5,5))
plt.plot(I)
plt.plot(S)
plt.xlabel("Time (days)")
plt.ylabel("Population")
```

## Exercise 6

By experimenting with values of $b$, you should find that the epidemic disappears somewhere between 0.000005 and 0.000006. To see this you have to increase the value of `n_days` because the peak gets later as it gets lower.

```{code-cell} ipython3

# set up variables and arrays
n_days = 1000
a = 0.1
b = 0.000005
S = np.zeros(n_days)
I = np.zeros(n_days)

# initialise the variables
S[0] = 20000
I[0] = 100

# implement equations
for i in range(n_days - 1):
    S[i+1] = S[i] - (b * S[i] * I[i])
    I[i+1] = I[i] + (b * S[i] * I[i]) - (a * I[i])

plt.figure(figsize=(5,5))
plt.plot(I)
plt.plot(S)
plt.xlabel("Time (days)")
plt.ylabel("Population")
plt.title(b) # add title so we know what value we are currently looking at
```

One way to plot multiple solutions on the same plot is to use a loop as below. Note that we have also added a legend.

```{code-cell} ipython3
# set up variables and arrays

for k in range(4):

    b = 0.000001 * k + 0.000005

    n_days = 1000
    a = 0.1
    
    S = np.zeros(n_days)
    I = np.zeros(n_days)

    # initialise the variables
    S[0] = 20000
    I[0] = 100

    # implement equations
    for i in range(n_days - 1):
        S[i+1] = S[i] - (b * S[i] * I[i])
        I[i+1] = I[i] + (b * S[i] * I[i]) - (a * I[i])


    plt.plot(I, label = b)


plt.xlabel("Time (days)")
plt.ylabel("Population")
plt.legend()
```

## Exercise 7

```{code-cell} ipython3
n = 200
g = 9.81
dt = .1

theta = np.pi / 4
s = 100


x = np.zeros(n)
y = np.zeros(n)
u = np.zeros(n)
v = np.zeros(n)

# initialise the variables
u[0] = np.cos(theta) * s
v[0] = np.sin(theta) * s

# implement equations
for i in range(n - 1):
    x[i+1] = x[i] + u[i] * dt
    y[i+1] = y[i] + v[i] * dt
    u[i+1] = u[i]
    v[i+1] = v[i] - g * dt

plt.plot(x, y)
plt.xlabel("x")
plt.ylabel("y")
plt.title("Cannonball trajectory")
```

## Exercise 8


```{code-cell} ipython3
n = 200
g = 9.81
dt = .1

theta = np.pi / 4
s = 100


x = np.zeros(n)
y = np.zeros(n)
u = np.zeros(n)
v = np.zeros(n)

# initialise the variables
u[0] = np.cos(theta) * s
v[0] = np.sin(theta) * s

# implement equations
for i in range(n - 1):
    x[i+1] = x[i] + u[i] * dt
    y[i+1] = y[i] + v[i] * dt
    if y[i+1] < 0:
        y[i+1] = 0 # set y to zero if negative
    u[i+1] = u[i]
    v[i+1] = v[i] - g * dt

plt.plot(x, y)
plt.xlabel("x")
plt.ylabel("y")
plt.title("Cannonball trajectory")
```

## Exercise 9

See separate document.

## Exericse 10

**Part 1**

```{code-cell} ipython3
import numpy as np
import matplotlib.pyplot as plt

n = 60
g = 9.81
dt = .2
d = 0.25
theta = np.pi / 6
s = 80

x = np.zeros(n)
y = np.zeros(n)
u = np.zeros(n)
v = np.zeros(n)

# initialise the variables
u[0] = np.cos(theta) * s
v[0] = np.sin(theta) * s

# implement equations
for i in range(n - 1):
    x[i+1] = x[i] + u[i] * dt
    y[i+1] = y[i] + v[i] * dt
    u[i+1] = u[i] - d*u[i] * dt
    v[i+1] = v[i] - g * dt - d*v[i] * dt
    if y[i+1] < 0: # set to zero if negative
        x[i+1] = x[i]
        y[i+1] = 0
        u[i+1] = 0
        v[i+1] = 0

t = np.linspace(0, 60*dt, n)

plt.figure(figsize=(6,4))
plt.plot(t, x, label="x")
plt.plot(t, y, label="y")
plt.xlabel("time (s)")
plt.ylabel("position (m)")
plt.title("Cannonball trajectory")
plt.legend()

plt.figure(figsize=(4,4))
plt.plot(x, y)
plt.xlabel("x (m)")
plt.ylabel("y (m)")
plt.title("Cannonball trajectory")

print("Horizontal distance travelled:", x[n-1])
```

**Part 2**

```{code-cell} ipython3
import numpy as np
import matplotlib.pyplot as plt

n = 60
g = 9.81
dt = .2
d = 0.25
theta = np.pi / 6
s = 80

theta_values = np.linspace(0, np.pi/2, 50)
distance_travelled = np.zeros(50)

for j in range(50):
    theta = theta_values[j]

    x = np.zeros(n)
    y = np.zeros(n)
    u = np.zeros(n)
    v = np.zeros(n)

    # initialise the variables
    u[0] = np.cos(theta) * s
    v[0] = np.sin(theta) * s

    # implement equations
    for i in range(n - 1):
        x[i+1] = x[i] + u[i] * dt
        y[i+1] = y[i] + v[i] * dt
        u[i+1] = u[i] - d*u[i] * dt
        v[i+1] = v[i] - g * dt - d*v[i] *dt
        if y[i+1] < 0: # set to zero if negative
            x[i+1] = x[i]
            y[i+1] = 0
            u[i+1] = 0
            v[i+1] = 0

    distance_travelled[j] = x[n-1]

plt.plot(theta_values, distance_travelled)
plt.title("Horizontal distance travelled by the cannonball")
plt.xlabel("Launch angle (radians)")
plt.ylabel("Distance travelled (m)")

# determine the index corresponding to the maximum distance
index = np.argmax(distance_travelled)
# find the corresponding value of theta
theta_max = theta_values[index]

print(distance_travelled)
print("Angle that maximises horizontal distance:", theta_max, "radians, ", theta_max * 180 / np.pi, "degrees")
```