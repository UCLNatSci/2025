---
jupytext:
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.18.1
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---

# Workshop 1: Solutions

## Exercise 1

The program will display

> 1

The program calculates the remainder after dividing $13$ by $4$.

## Exercise 2 

> **set x = 13**<br/>
> **set c = 0**<br/>
> **repeat while x > 4**<br/>
>&nbsp;&nbsp;&nbsp;&nbsp; **increase x by -4**<br/>
>&nbsp;&nbsp;&nbsp;&nbsp; **increase c by 1**<br/>
> **display c**

## Exercise 3


```{code-cell} python
pop = 100
i = 0
while pop < 10000:
    pop = pop * 2
    i = i + 1
    print(pop)
    
print("Number of hours:", i)
```

## Exercise 4

```{code-cell} python
:tags: ["scroll-output"]
pop = 100
i = 0
while pop < 10000:
    pop = pop * 1.02
    i = i + 1
    print(pop)

print("Number of hours:", i)
```
## Exercise 5
```{code-cell} python
pop = 100
i = 0
while pop < 10000:
    pop = pop * 1.02
    i = i + 1
    if i % 24 == 0:
        print(pop)

print("Number of hours:", i)
```

## Exercise 6

```{code-cell} python
half_life = 8.02
r = 0.5 ** (1/half_life)
print('Daily decay rate:', r)
```

## Exercise 7

We would expect that after 8 days the activity would have approximately halved ($8.35 \times 10^{11}~\mathrm{Bq}$).

```{code-cell} python
# starting conditions
activity = 1.67 * (10**12)
day = 0

while activity > 10000:
    # activity decreases by the daily decay rate each day
    activity = activity * r
    day = day + 1
    
    # check the activity on day 8
    if (day == 8):
        print('The activity after 8 days is', activity, 'Becquerels')

print('Days taken to reach 10000 Becquerels:', day)
```
## Exercise 8

```{code-cell} python
# starting conditions
activity = 1.67 * (10**12)
day = 0

while activity > 10000:
    # activity decreases by the daily decay rate each day
    activity = activity * r
    day = day + 1

    # print the activity once every 7 days
    if day % 7 == 0:
        print(activity, 'Becquerels')

print('Days taken to reach 10000 Becquerels:', day)
```

## Exercise 9

```{div} pseudocode
set n to 5  
repeat while n is greater than 1:  
&nbsp;&nbsp;&nbsp;&nbsp;if n is even:  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; set n to n/2  
&nbsp;&nbsp;&nbsp;&nbsp;if n is odd:  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; set n to 3n + 1  
&nbsp;&nbsp;&nbsp;&nbsp;display n  
```

## Exercise 10

```{code-cell} python
n = 5

while (n > 1):
    if (n % 2) == 0:
        # n is even, divide by two
        n = n / 2
    else:
        # n is odd, triple and add one
        n = (n * 3) + 1
    
    print(n)    
```

## Exercise 11

```{code-cell} python
n = 5
collatz_num = 1

# we will change n, so we need to remember what value we started with
start = n

while (n > 1):
    if (n % 2) == 0:
        # n is even, divide by two
        n = n / 2
    else:
        # n is odd, triple and add one
        n = (n * 3) + 1
    
    collatz_num = collatz_num + 1
    
print('The Collatz number of', start, 'is', collatz_num)
        
```

## Exercise 12

```{code-cell} ipython3
i = 6
while i >= 1:
    j = 1
    while j <= i:
        print(j, end="")
        j = j + 1
    print()
    i = i - 1
```

```{code-cell} ipython3
i = 1
while i <= 5:
    j = 1
    while j <= 5:
        print((i + j) % 2, end="")
        j = j + 1
    print()
    i = i + 1
```

```{code-cell} ipython3
i = 1
while i <= 6:
    j = 1
    while j <= 6:
        if i + j <= 6:
            print("A", end="")
        else:
            print("B", end="")
        j = j + 1
    print()
    i = i + 1
```

## Exercise 13

To do this we need to nest one while loop (to calculate Collatz numbers) inside another one (to check each if each integer meets the condition).

```
k = 1
collatz_num = 1

while (collatz_num <= 200): #outer while loop
    #increase k by 1, reset collatz_num
    k = k + 1
    collatz_num = 1

    #remember we don't want to change k itself - or we wouldn't know what numbers we'd already checked
    n = k

    #now find the Collatz number of k
    while (n > 1):
        if (n % 2) == 0:
            # n is even, divide by two
            n = n / 2
        else:
            # n is odd, triple and add one
            n = (n * 3) + 1

        collatz_num = collatz_num + 1

# Once the condition has been met, we're finished

print('The Collatz number of', k, 'is', collatz_num)
print(k, 'is the smallest number whose Collatz number is greater than 200') 

```

## Exercise 14

This is one way to write the pseudocode. Yours might be different. If you gave your pseudocode to your friend, could they easily turn it into a Python program?

:::{card}
```{div} pseudocode
Set value of n  
Set n_digits to 0  
While n is greater than or equal to 1:  
&nbsp;&nbsp;&nbsp;&nbsp;Divide n by 10  
&nbsp;&nbsp;&nbsp;&nbsp;Add 1 to n_digits      
Display n_digits
```
:::

```{code-cell}
# Input n
n = 1234

# Set n_digits to 0
n_digits = 0

# Extra step to remember starting value
start = n

while n >= 1:
    n = n / 10                 # Divide n by 10
    n_digits = n_digits + 1    # Add 1 to n_digits

# Output n_digits
print(start, "has", n_digits, "digits.")
```

Let's think about how we can change the pseudo-code so that the program works for negative numbers. 

We know that a negative number, $-n$, has the same number of digits as the positive number $n$. So to make the program work for negative numbers, we just need to check whether the input is negative, and if it is, turn it into a positive number with the same number of digits. 

```{code-cell}
# Input n
n = -1

# Extra step to remember starting value
start = n

# Check if n is negative
if (n < 0):
    n = n * -1 # Make n positive

# Set n_digits to 0
n_digits = 0

while n >= 1:
    n = n / 10                 # Divide n by 10
    n_digits = n_digits + 1    # Add 1 to n_digits

# Output n_digits
print(start, "has", n_digits, "digits.")
```
## Exercise 15

Pseudocode:

```{div} pseudocode

Set n to 10  
Set f to 1  
Repeat until n equals 1:  
&nbsp;&nbsp;&nbsp;&nbsp;Set f to f times n  
&nbsp;&nbsp;&nbsp;&nbsp;Decrease n by 1  
Print f

```

```{code-cell}
n = 10
f = 1
while n > 1:
    f = f * n
    n = n - 1 # or n -= 1
print(f)
```

## Exercise 16

NB You should test your answer with a variety of values for `a`, `b` and `c` to check that it is working correctly. At least one test for each of the three type of solution.

```{code-cell}
a = 1
b = -1
c = -12

discriminant = b**2 - 4 * a * c

if discriminant > 0:
    print("The solutions are x =", (-b + discriminant**0.5)/(2*a), "and x =", (-b - discriminant**0.5)/(2*a))
elif discriminant == 0:
    print("The solution is x =", -b/(2*a))
else:
    print("There are no real solutions")
```

## Exercise 17

```{div} pseudocode
Set value of n  
Set value of m  
Set i to 0  
Repeat while n is greater than m:  
&nbsp;&nbsp;&nbsp;&nbsp;Subtract m from n  
&nbsp;&nbsp;&nbsp;&nbsp;Increase i by 1  
Display i and n
```

```{code-cell}
n = 13
n_original = n
m = 3
i = 0
while n > m:
    n = n - m
    i += 1
print(n_original, "divided by", m, "equals", i, "remainder", n)
```

## Exercise 18

It should be reasonably easy to follow the instructions in order to produce the correct code to perform the calculation. The only tricky part is to maintain the original value of `t` in a new variable `t_orig` so that we can include it in the final print statement.

```{code-cell}

t = 1000000
t_orig = t
s = t % 60
t = t // 60
m = t % 60
t = t // 60
h = t % 24
d = t // 24

print(t_orig, " seconds is ", d, " days ", h, ":", m, ":", s, sep="")
```

## Exercise 19

1\. The corrected psuedocode is shown below.

<div class = "pseudocode">
set value of n<br/>  
set result to True<br/>  
set i to <s>1</s> 2  <span style="color:red"><- this number should be 2, not 1</span><br/>  
repeat while i is less than n:<br/>  
&nbsp;&nbsp;&nbsp;&nbsp;if n is divisible by i<br/>  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; set result to False<br/>  
&nbsp;&nbsp;&nbsp;&nbsp;increase i by 1  <span style="color:red"><- this line should be indented so that it is not part of the if block</span><br/>  
display result<br/>  
</div>

2\.

```{code-cell}
n = 11 # pick any number
result = True
i = 2
while i < n:
    if n % i == 0:
        result = False
    i = i + 1
print(result)
```

3\.

This is tricky! One possible solution is shown below. We introduce two new variables: `c` which keeps a running total of the number of primes, and `m` which runs from `2` to `n - 1`. For each value, test if `m` is prime and if so increase `c` by one.

```{code-cell}
n = 7
c = 0 # new variable to count the number of primes
m = 2 # this variable replaces the previous variable n
while m < n:
    result = True
    i = 2
    while i < m:    
        if m % i == 0:
            result = False
        i = i + 1
    if result == True: # if n is prime, increase c by 1
        c = c + 1
    m = m + 1

print(c)
```


