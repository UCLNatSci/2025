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

# Functions

## Calling Functions

A function is a named sequence of computer instructions that performs a specific task. With the help of functions, we can break our program into small modular chunks. So, as we start to write larger programs, functions help us to make it more organized and manageable.

Let's start by examining the built-in Python function `round`.

```{code-cell} ipython3
x = round(2.5)

print(x)
```

When the Python interpreter reaches the expression `round(2.5)` it recognises that `round` is a built-in function, executes the function and returns the result. The name of the function gives an indication of what the function does, but we can get further information by using another function `help`:

```{code-cell} ipython3
help(round)
```

:::{exercise}
:label: exercise_3_1
1. What will `round(-0.5)` return? Try it.
2. Use `help` to find out what the function `abs` does.
:::

:::{solution} exercise_3_1
:class: dropdown

First, let's see what happens when we call `round(-0.5)`.
``` 
x = round(-0.5)

print(x)
```
We see that -0.5 is rounded up to zero.

Now let's find out what `abs` does
```
help(abs)
```
`abs(x)` will return the absolute value of `x`.
:::

+++

## Defining functions

Let's start with a very simple example of a mathematical function:

$$f(x) = x^2.$$

We can think of $f$ as being as machine which eats a number, squares it, then sends us the result. Given this definition of $f$, we can use it to calculate the square of any number we please:

$$\begin{align}f(3) &= 9\\f(10)&=100\end{align}$$

and so on. Let's define this function in Python:

```{code-cell} ipython3
def f(x):
    y = x ** 2
    return y
```

If you run the code above, nothing will appear to happen. However, we can now use it to calculate the square of any number we choose:

```{code-cell} ipython3
f(3)
```

Or to set the value of a variable:

```{code-cell} ipython3
z = f(10)
print(z)
```

Because `f` returns a number, we can use it anywhere Python expects a number:

```{code-cell} ipython3
z = f(3) + f(10)
print(z)

w = round(f(5))
print(w)
```

We can also use a variable as an argument:

```{code-cell} ipython3
n = 8
m = f(n)
print(n, "squared is", m)
```

Notice something very important here. The name of the variable we pass as an argument (`n`) has nothing to do with the name of the parameter (`x`). It is as if `x = n` is executed when `f(n)` is called. It doesn’t matter what the value was named in the call, inside the function its name is `x`.

+++

:::{exercise}
:label: exercise_3_2
Use the function `f` to calculate:
1. $(999 + 123)^2$
2. $999^2 + 123^2$
3. $3^4$
:::

:::{solution} exercise_3_2
:class: dropdown
1. 
```
x_1 = f(999 + 123)
print(x_1)
```
2. 
```
x_2 = f(999) + f(123)
print(x_2)
```
3. We can rewrite $3^4$ as $(3^2)^2$. As $f$ takes a number as input and gives a number as output, we can safely use the output of one function call as the input to the next. 
```
x_3 = f(f(3))
print(x_3)
```

:::

+++

##  Functions Definition Notation

![](51.png)

A function definition consists of
1. A **header** which defines the function name and parameter(s) e.g. `def f(x):`
2. A **body** consisting of one or more lines of Python code e.g. `y = x ** 2`
3. (Optional) a **return statement** which defines the value to return from the function e.g. `return y`

:::{note}
The body and return statement must be indented (the Python standard is 4 spaces).
:::

## Example

Consider the following code, which calculates and prints the number of digits in a number `x = 19583`. The variable `i` is initialised to 0 and then incremented each time the while loop is executed. When the loop exits, `i` contains the result - the total number of times the loop body was executed, which is the same as the number of digits.

```{code-cell} ipython3
x = 19583

i = 0
while x >= 1:
    i = i + 1
    x = x / 10

print(i)
```

Below we convert this code into a function `number_of_digits`:

```{code-cell} ipython3
def number_of_digits(x):
    i = 0
    while x >= 1:
        i = i + 1
        x = x / 10
    return i

print(number_of_digits(19583))
```

:::{exercise}
:label: exercise_3_3

The function `number_of_digits` fails for arguments less than `1`. Write a new function `number_of_digits_2` which returns the correct number of digits for positive and negative values. For values between `-1` and `1` the function should return `0`.

```
# write your function definition here

print(number_of_digits_2(999)) # should print 3
print(number_of_digits_2(0.5)) # should print 0
print(number_of_digits_2(-0.5)) # should print 0
print(number_of_digits_2(-999)) # should print 3
```
:::

:::{solution} exercise_3_3
:class: dropdown

We can use the fact that a negative number $-n$ has the same number of digits as the positive number $n$, using the `abs` function in the while loop to check whether the absolute value of the input is greater than 1. 

```{code-cell} ipython3
def number_of_digits_2(x):
    i = 0
    # check whether absolute value is greater than 1, otherwise do nothing
    while abs(x) >= 1:
        i = i + 1
        x = x / 10
    return i
    
# now test it 
print(number_of_digits_2(999))
print(number_of_digits_2(0.5)) 
print(number_of_digits_2(-0.5)) 
print(number_of_digits_2(-999)) 
```

:::

## Combining Functions and Loops

We really start to see the utility of functions when we combine them with loops. What is the total number of digits in all the numbers from `1` to `99` inclusive? At each execution of the loop, `number_of_digits(i)` is added to the variable `total`.

```{code-cell} ipython3
total = 0
for i in range(1, 100):
    total = total + number_of_digits(i)

print(total)
```

:::{exercise}
:label: exercise_3_4
Use the function `number_of_digits_2` to calculate the total number of digits of all numbers in the range $-99 \leq n \leq 99$.
:::

:::{solution} exercise_3_4
:class: dropdown
Let's follow the same structure:

```
total = 0
for i in range(-99, 100):
    total = total + number_of_digits_2(i)
    
print(total)
```
We should get 378.
:::

+++

## Combining Functions

It is possible to 'chain together' functions so that one function is called inside the body of another function. In the example below, `total_digits(n)` returns the total number of digits in numbers between `1` and `n` (not counting `n` itself). I have repeated the definition of the `number_of_digits` functions here so we can see how it all fits together.

```{code-cell} ipython3
def number_of_digits(x):
    i = 0
    while x >= 1:
        i = i + 1
        x = x / 10
    return i
    
def total_digits(n):
    total = 0
    for i in range(1, n):
        total = total + number_of_digits(i)

    return total

print(total_digits(100))
```

:::{exercise}
:label: exercise_3_5

Write a function `total_digits_2(m, n)` which returns the total number of digits in all integers between `m` and `n` inclusive (you may assume that `m < n`).

```
# write your function definition here

print(total_digits_2(-100, 100))
```
:::

:::{solution} exercise_3_5
:class: dropdown

```
def number_of_digits_2(x):
    i = 0
    # check whether absolute value is greater than 1, otherwise do nothing
    while abs(x) >= 1:
        i = i + 1
        x = x / 10
    return i
    
def total_digits_2(m, n):
    total = 0
    for i in range(m, n + 1):
        total = total + number_of_digits_2(i)
    
    return total

print(total_digits_2(-100, 100))
```
We should get 384.

+++

## Keep Your Program Tidy!

When you use functions, you might find your Python programs growing quite large. It is good practice in this case to keep your program tidy by keeping your program in a consistent order, as follows:

```
# Import statements at the top

import numpy as np
import matplotlib.pyplot as plt
import moominlib as ml

# Next, function definitions

def one_function(x, y, z):
    # Python statements
    # Python statements
    return val

def another_function(x, y, z):
    # Python statements
    # Python statements
    return val

# The main program body. This line will be executed first!
# More code
# Function calls
# etc
```
