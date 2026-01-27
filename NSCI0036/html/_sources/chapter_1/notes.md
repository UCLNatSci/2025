---
jupytext:
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.18.1
kernelspec:
  display_name: base
  language: python
  name: python3
---

# Fundamentals


Programming is all about breaking down a problem into simple steps that a computer can understand. In our case the 'simple steps' are instructions, written in the Python programming language, which perform operations such as arithmetic calculations or setting the value of variables. These instructions are usually performed one at a time in sequence, although some instructions might cause the program to branch to a different section of code or to repeat a section of code. In this section we will introduce some of the most common Python constructs and some techniques to solve simple computational problems.

```{admonition} What you'll learn
:class: tip
 - Perform arithmetic calcuations
 - Create and use variables
 - Display output using `print`
 - Conditionally execute instructions using the `if` statement
 - Repeat instructions using the `while` statement
 - Use pseudocode to express the algorithmic solution to a problem
```

## Introduction

Suppose a colony of bacteria doubles in size every hour. If the initial population is 100 cells, how many hours will it take to reach a population of 10000 cells? Here is one way to solve this problem using Python:

```{code}
# Calculate the number of hours for a population 
# to reach 10000 cells under exponential growth.

population = int(input("Enter the initial population:"))
rate = float(input("Enter the growth rate:"))
i = 0
while population < 10000:
    population = population * rate
    i = i + 1
    print("Population after", i, "hours:", population)
```

Executing the code and entering the values `100` and `2` when prompted should produce the following output:

![](input.png)

+++

:::{exercise}
:label: exercise_1_0
Paste the code above into a new code cell. Execute the code cell, enter the value `100` and `2` (each followed by the {kbd}`Enter` key) and check that it produces the expected output.
:::

When we run a Python program, the Python interpreter reads the code one line at a time. Each line of code might cause the program to produce some output, set the value of a variable, or to jump to a different line of code, until eventually the last line of code is reached and execution terminates.

The first two lines are **comments** which are ignored by the Python interpreter.

```{code}
# Calculate the number of hours for a population 
# to reach 10000 cells under exponential growth.
```

The next two lines cause a prompt to be displayed and the results stored in a **variable** `population` of type **integer** and a second variable `rate` of type **float**.

```{code}
population = int(input("Enter the initial population:"))
rate = float(input("Enter the growth rate:"))
```

Next, a variable `i` is created and set to a value `0`.

```{code}
i = 0
```

The next line

```{code}
while population < 10000:
```

indicates that the following three lines should be executed repeatedly while the variable `population` is less than `10000`.

```{code}
population = population * rate
```

Multiplies the population by the growth rate,

```{code}
i = i + 1
```

Increase the value of `i` by `1`, and

```{code}
print("Population after", i, "hours:", population)
```

displays the value of `population` and `i`.

+++

## Arithmetic
Python supports basic arithmetic operations addition, subtraction, multiplication and division using the symbols `+`, `-`, `*` and `/`. Brackets are used to indicate the order in which the parts of an expression are computed. For example, in the following expression, the division is performed first and then the addition.

```{code-cell} ipython3
3 + 4 / 2
```

In order to compute $\frac{3 + 4}{2}$, use brackets:

```{code-cell} ipython3
(3 + 4) / 2
```

In order to calculate powers, use the `**` operator. For example, the following calculates $8^3$:

```{code-cell} ipython3
8 ** 3
```

### Arithmetic Operators

The following arithmetic operators are available in Python. Modulo and Floor division are explained in {ref}`fundamentals_modulo_arithmetic`.   

| Operator | Symbol |
|---|---|
| Addition | `+` |
| Subtraction | `-` |
| Multiplication | `*` |
| Division | `/` |
| Power | `**` |
| Modulo | `%` |
| Floor division | ``//`` |

+++

## Number Types

Every Python variable has a **data type** as well as a value. The type determines what operations can be performed on the variable and how it is stored in the computer's memory. Python supports a number of primitive data types including numbers, strings, lists and files and in particular there are two number types: **integers** and **floating point numbers**. When we specify a number in code it is important to understand which type we are creating:

|Number|Type|Description|
|---|---|---|
|`5`|`int`|A whole number|
|`-5`|`int`|A negative integer|
|`0.5`|`float`|A number with decimal part|
|`5.0`|`float`|Including a decimal point always results in type `float`|
|`5e6`|`float`|$5\times10^6$|
|`2.34e-5`|`float`|$2.34\times10^{-5}$|

+++

:::{exercise}
:label: exercise_1_1

Use Python to calculate the value of $\frac{-5 + \sqrt{5^2 - 4}}{2}$.

Hint: $\sqrt{x} = x^{0.5}$.
:::

+++


```{solution-start} exercise_1_1
:class: dropdown
```

```{code-cell}
# code
(-5 + (5**2 - 4)**0.5) / 2
```

```{solution-end}
```

+++

## Variables

A **variable** is a named storage location in the computer's memory. We store a value in a variable so that we can use it later in our computations.

We use **assignment** to set the value of a variable:

```{code-cell} ipython3
speed = 35 # create a new variable named 'speed' and assign the value 35
double_speed = speed * 2 # create new variable named 'double_speed'
```

In order to inspect the value of a variable, we use the `print` function:

```{code-cell} ipython3
print(speed)
print(double_speed)
```

The print statement can print multiple values. Separate each value by a comma `,` and use double quotes `"` for literal text:

```{code-cell} ipython3
print("The value of speed:", speed)
print("The value of double_speed:", double_speed)
```

:::{exercise} 
:label: exercise_1_2
Complete the following code so that it prints the **two** solutions to the quadratic equation $x^2 + 5x + 4 = 0$:

```
a = 1
b = 5
c = 4

pos_solution = (-b + (b**2 - 4*a*c)**0.5) / (2*a)

print("Positive Solution:", pos_solution)
```
:::

+++

```{solution-start} exercise_1_2
:class: dropdown
```

```{code-cell} ipython3
a = 1
b = 5
c = 4

pos_solution = (-b + (b**2 - 4*a*c)**0.5) / (2*a)
neg_solution = (-b - (b**2 - 4*a*c)**0.5) / (2*a)

print("Positive Solution:", pos_solution)
print("Negative Solution:", neg_solution)
```

```{solution-end}
```

+++

```{note}
**VARIABLE NAMING RULES**  
- A variable name can only contain alpha-numeric characters and underscores (`A-Z`, `a-z`, `0-9`, and `_`)
- A variable name cannot start with a number
- Variable names are case-sensitive (`age`, `Age` and `AGE` are three different variables)
```
:::{warning}
Beware of accidentally renaming Python keywords. The following is correct Python but a Very Bad Idea because it renames the `print` function, which will result in some very weird errors!

```
print = 5

print(print) # this won't work.
```
:::

+++

## Updating Variables

We can use assignment to change the value of a variable. In this case, the same variable appears on both sides of the equals sign:

```{code-cell} ipython3
print("Original speed:", speed)

speed = speed + 2 # Increase the value of speed by 2

print("New speed:", speed)
```

This is a legal statement because Python first evaluates the expression on the right of the equals sign (`speed + 2`) and *then* places the result into the variable on the left.

+++

:::{exercise}
:label: exercise_1_3

Complete the code below so that it divides `v` by `5` three times, printing its value each time.
```
v = 1000
print("v:", v)

# your code here

```

should output:

```
v: 1000
v: 200.0
v: 40.0
v: 8.0
```
:::

+++


```{solution-start} exercise_1_3
:class: dropdown
```

```{code-cell} python
v = 1000
print("v:", v)
v = v / 5
print("v:", v)
v = v / 5
print("v:", v)
v = v / 5
print("v:", v)
```


```{solution-end}
```

+++

## Getting Help

`print` is the first of many Python in-built functions that we will study.

You can find out more about Python functions by using the `help()` function. Let's learn about the `print` function.

```{code-cell} ipython3
help(print)
```

For example, from this we can see how to change the default seperator using `sep`:

```{code-cell} ipython3
print("1", "2", "3", sep="-")
```

(fundamentals_modulo_arithmetic)=
## Modulo Arithmetic

Using the `/` operator results in a floating-point (decimal) value:

```{code-cell} ipython3
9 / 4
```

On the other hand, the `//` operator performs **floor division**, computing the quotient and discarding the fractional part:

```{code-cell} ipython3
9 // 4
```

To calculate the remainder after floor division, use the **modulus** operator `%`:

```{code-cell} ipython3
9 % 4
```

### Example 1
The `%` operator is useful to determine if a variable is divisible by a number. For example, if a number is even its remainder after dividing by 2 is zero; if it is odd its remainder after dividing by 2 is 1:

```{code-cell} ipython3
x = 5
print(x % 2)
x = 6
print(x % 2)
```

### Example 2
Suppose we have 1234 pennies in the piggy-bank. How much do we have in pounds and pence? First we divide by 100 to get the whole number of pounds:

```{code-cell} ipython3
num_pennies = 1234
pounds = num_pennies // 100
print("Pounds:", pounds)
```

Next we use the `%` operator to find the number of pence:

```{code-cell} ipython3
pence = num_pennies % 100
print("Pence:", pence)
```

## Repeating code using `while`

A **loop** is a sequence of instructions which is executed repeatedly until a goal is reached. The `while` loop repeats a section of code while a specific condition is true.

The following loop repeatedly divides the variable `v` by `5` while the condition `v > 10` is true.

```{code-cell} ipython3
v = 1000
while v > 10:
    print("v:", v)
    v = v / 5
```

:::{exercise}
:label: exercise_1_4
Write a `while` loop which **multiplies** `v` by `5` while `v` is **less** than `1000`.

```
v = 10

# your code here
```

Should produce:

```
v: 10
v: 50
v: 250
```
:::

+++

```{solution-start} exercise_1_4
:class: dropdown
```

```{code-cell} python
v = 10

while (v < 1000):
    print("v:", v)
    v = v * 5
```

```{solution-end}
```

+++

## `If` statement
The specific heat capacity of water depends on whether it is in a solid, liquid or gaseous state.

|State|Specific heat capacity (kJ/kgK)|
|---|---|
|Solid|2.108|
|Liquid|4.187|
|Gas|1.996|

Let's write code which, given the temperature of a water sample, sets the value of the variable `shc` to the appropriate value (of course, we need to know the melting and boiling points of water!)

```{code-cell} ipython3
temp = 90 # temperature of water sample

if temp > 100: # gas
    shc = 1.996
elif temp > 0: # liquid
    shc = 4.187
else:          # solid
    shc = 2.108
    
print("Specific heat capacity:", shc, "kJ/kgK")
```

The `if` statement evaluates the expression `temp > 100` and if it is true, executes the indented code directly underneath, then skips to the next statement after the `if-else` block. If it is not true, execution moves to the `elif` statement. If the expression `temp > 0` is true, the indented code beneath it is executed  and execution skips to the next statement after the `if-else` block. Finally, if neither expression is true, the indent code block below the `else` statement is executed.

:::{note}
**`If` statement**
- Exactly one of the indented code blocks will be executed.
- Use the `tab` key to indent code by exactly four spaces.
- The `if`, `elif` and `else` statements must be followed by a colon (`:`).
- Note the unusual keyword `elif` (rather than `elseif`).
- The `elif` and `else` statements are optional.
:::

:::{warning}
**Assignment vs Equality**  

`=` is the **assignment** operator. It assigns the value on the right to the variable on the left:
```
x = 6 + 7 # sets x to the value 13
```

`==` is the **equality** operator. It evaluates to `True` if the expression on the left is equal to the expression on the right.
```
x == 13 # returns `True`
```

The condition in an `if` statement should always use `==`. This is a common mistake:

```
if x = 13: # this is a mistake. Be careful!
    print("yes")
```
:::

+++

:::{exercise}
:label: exercise_1_5

Complete the code below so that it prints

`x is even`

if is `x` is divisible by `2` and prints

`x is odd`

if it is not divisible by `2`.

```
x = 53783

# your code here
```

Should produce:

```
x is odd.
```

Check that your code works by changing the value of `x` and running the code again.

:::

+++

```{solution-start} exercise_1_5
:class: dropdown
```

```{code-cell} python
x = 53783

if (x % 2) == 0:
    print('x is even')
else:
    print('x is odd')

```

```{solution-end}
```
