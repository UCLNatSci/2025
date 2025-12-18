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


```{code-cell} python
pop = 100
i = 0
while pop < 10000:
    pop = pop * 2
    i = i + 1
    print(pop)
    
print("Number of hours:", i)
```

## Exercise 2

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
## Exercise 3
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

## Exercise 4

```{code-cell} python
half_life = 8.02
r = 0.5 ** (1/half_life)
print('Daily decay rate:', r)
```

## Exercise 5

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
## Exercise 6

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

## Exercise 7

```{div} pseudocode
set n to 5  
repeat while n is greater than 1:  
&nbsp;&nbsp;&nbsp;&nbsp;if n is even:  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; set n to n/2  
&nbsp;&nbsp;&nbsp;&nbsp;if n is odd:  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; set n to 3n + 1  
&nbsp;&nbsp;&nbsp;&nbsp;display n  
```

## Exercise 8

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

## Exercise 9

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
## Exercise 10

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

<!-- :::{solution} exercise_1_15
To do this we need to 'nest' one while loop (to calculate Collatz numbers) inside another one (to check each if each integer meets the condition).

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

# Once the condition has been met, let's say that we are finished
print('The Collatz number of', k, 'is', collatz_num)
print(k, 'is the smallest number whose Collatz number is greater than 200') 

```
:::
-->
