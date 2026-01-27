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


# Lists and Strings

```{admonition} What you'll learn
:class: tip
 - How to store a sequence of data in a **list**
 - How to traverse lists
 - How to add and remove elements
 - How find elements
 - How to store a sequence of character data in a **string**
 - How to extract substrings by slicing
 - How to use string methods
```

## Lists
A `list` is a Python data type that stores a sequence of values. For example, suppose we have the following data representing five years' population data:

```{code-cell} ipython3
populations = [12, 25, 54, 102, 206]
print(populations)
```

Each element in a list has an **index** which identifies its position. We can access a list element by following the variable name with square brackets and the index:

```{code-cell} ipython3
initial_pop = populations[0]
year_3_pop = populations[3]

print("Initial population:", initial_pop)
print("Population in year 3:", year_3_pop)
```

Likewise, we can update individual list elements. Suppose we would like to change the value of the 3rd element:

```{code-cell} ipython3
populations[3] = 100 # Assign the value 100 to element at index 3
print(populations)
```

Any data type can be stored in a list, including strings:

```{code-cell} ipython3
cities = ["Manchester", "Liverpool", "Sheffield", "Stoke-on-Trent"]
x = cities[2]
print(x)
```

:::{note} 
- Lists are indexed starting from `0`. If a list has `n` elements, then the last element is at index `n - 1`.
- Square brackets are used for two distinct purposes: for list creation: `x = [1, 2, 4]`, and list element access: `x[2]`.
:::

## Traversing Lists
There are two ways of accessing all elements of a list. The first way is to use a `for` loop to loop over all index values. We use the Python function `len` to determine the number of elements in the list.

```{code-cell} ipython3
n = len(populations) # get the number of elements in the list
for i in range(n): # loop over index values 0 to n - 1
    pop = populations[i] # Access element at index i
    print("Year", i, "population:", pop)
```

If you don't need index values, you can loop over the individual elements of the list:

```{code-cell} ipython3
for pop in populations: # loop over all elements of the list
    print("Population:", pop)
```

## Appending Elements to a List
After a list is created, we can add items to it using the `append` method. Suppose that we have recorded the species population for the next year as `420`:

```{code-cell} ipython3
populations.append(420)
print(populations)
```

A common pattern for list creation is to start with an empty list, then use a loop to append one element at a time. The following example creates a list of the first 10 square numbers.

```{code-cell} ipython3
values = []
for i in range(10):
    values.append(i**2)
print(values)
```

## Finding a List Element
If you want to know the index of an element in a list, use the `index` method. `string.index(s)` returns the first element equal to argument `s`:

```{code-cell} ipython3
values = ["ABC", "DEF", "GHI", "JKL"]
i = values.index("GHI") # Find the index of the first element equal to "GHI"
print(i)
```

## Strings

## String Variables
A string is data type representing character data. In Python, string literals are surrounded either by double quote `"` or single quote `'` characters.

```{code-cell} ipython3
greeting_start = "Season's"
greeting_end = 'greetings'

print(greeting_start, greeting_end)
```

## String Concatenation
Use the `+` symbol to **concatentate** strings

```{code-cell} ipython3
greeting = greeting_start + " " + greeting_end
print(greeting)
```

But it is not possible to concatentate a string and a number:

```{code-cell} ipython3
:tags: [raises-exception]
id = greeting + 55
```

The `+=` operater can be used to append characters to a string:

```{code-cell} ipython3
greeting += ", Jeremy."
print(greeting)
```

## Converting between strings and numbers

Functions `str`, `int` and `float` are available to convert between strings and other data types.

```{code-cell} ipython3
# convert from integer to string
id = 1729
new_id = str(id) + "_NEW"
print(new_id)

```

```{code-cell} ipython3
# convert from string to floating-point number
price = "12.99"
total_price = float(price) * 1.2
print(total_price)
```

## String Methods
A string is an **object**, which is a data type with **methods** directly attached with it which can be called similarly to calling a function. The `upper` method converts a string to upper case, and `lower` to lowercase:

```{code-cell} ipython3
name = "Jeremy Bentham"
name_uppercase = name.upper()
print(name_uppercase)
name_lowercase = name.lower()
print(name_lowercase)
```

Other useful methods are `split`, `join` and `trim`. `split` splits the string into individual words and returns them as a list:

```{code-cell} ipython3
text = "The time has come"
word_list = text.split()
print(word_list)
```

`join` does the reverse, combining a list of strings into a single string. `s1.join(word_list)` joins the strings in ``

```{code-cell} ipython3
", ".join(word_list)
```

`strip` removes any white space characters (spaces, tabs or newlines) at the start or end of the string:

```{code-cell} ipython3
text = "  too much space!   "
text2 = text.strip()
print(text2)
```

## Strings and Characters
A string is composed of a sequence of characters, and most of the operations that can be performed on lists can also be performed on strings. For example, individual characters can be accessed using square brackets enclosing the index position.

```{code-cell} ipython3
text = "Natural Sciences"
# first character is at index 0
first_initial = text[0]
# last character is at index -1
final_character = text[-1]
print(first_initial, final_character)
```

Use the `len` function to find the length of a string.

```{code-cell} ipython3
s = "Mighty"
x = len(s)
print(x)
```

:::{note}
An important difference between lists and strings: whereas it is possible to change the value of an an individual list item, it is **not** possible to change an indivdual string character. We say that strings are **immutable**.

```{code} ipython3
x = [4, 5, 6]
x[0] = 10 # this is OK
s = "ABC"
s[0] = "X" # this will result in an error
```
Likewise, it is not possible to append a character to a string. Instead, use string concatenation.
```{code} ipython3
s.append("D") # Error
s = s + "D" # This is OK
```
:::


## Slicing Lists and Strings

Given a list or string, we can access a single element using square brackets:


```{code-cell} ipython3
x = [4, 5, 6, 7, 8, 9]
y = x[0]
print(y)
```

If we want to access a sublist, we can use array **slicing**. Given integers `a` and `b`, `x[a:b]` returns a new list which contains the elements of `x` from index `a` to `b - 1` (i.e. including element `a` but excluding element `b`).

```{code-cell} ipython3
z = x[0:3]
print(z)
```

`x[a:b:c]` returns a list containing items `a` to `b - 1` with a step size of `c` (this is very similar to the `range` function),

```{code-cell} ipython3
w = x[0:9:2]
print(w)
```

## Example
Natural Sciences modules are identified by a 8 character code consisting of `NSCI` followed by a four digit number. The following paragraph of text contains Natural Sciences module codes mixed up with other data. We will write Python code to extract a list of Module codes from the text.

```{code-cell} ipython3
text = "Surrounded NSCI0007 me occasional pianoforte NSCI0011 alteration unaffected impossible ye. For saw half than cold.  arrived adapted. Numerous ladyship so raillery humoured goodness received an. So NSCI0004 formal length my highly NSCI0005 afford oh. Tall neat he make or at dull ye."

n = len(text) # determine the number of characters in the text
module_list = [] # create an empty list
for i in range(n): # i loops of all index positions in text
    if text[i:i + 4] == "NSCI": # exctact a 4 character substring and check if it is equal to "NSCI"
        module_list.append(text[i:i + 8]) # add 8 characters to the list
print(module_list)
```

:::{note}
- String comparison is **case-sensitive** so `"S" == "s"` is `False`.
- Remember to use a double equals to check for equality.
:::


## Escape Sequences

If you want to include special characters in a string, use an **escape sequence**. Precede the character you want to want to escape by a backslash character `\`.

```{code-cell} ipython3
quote = '"The time has come", the Walrus said.'
print(quote)
```

```{code-cell} ipython3
quote = "\"The time has come\", the Walrus said."
print(quote)
```

This can also be used to include a backslash character in the string.

```{code-cell} ipython3
quote = "A\\B"
print(quote)
```

A very useful excape sequence is `\n`, which denotes a **newline** character.

```{code-cell} ipython3
print("A\nAB\nABC")
```

## Multi-line Strings
String literals can span multiple lines, using triple-quotes: `"""`...`"""` or `'''`...`'''`.

```{code-cell} ipython3
long_string = """Twas the night before Christmas,
when all through the house
Not a creature was stirring,
not even a mouse."""
print(long_string)
```
