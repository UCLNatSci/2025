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

# Workshop 4: Lists and Strings

In computing, a **string** is a date type used to store sequences of characters. Often a string represents human-readable text, but strings can be used to store all any kind of data. For example, an RNA sequence:

```{code-cell} ipython3
sequence = "CAACAAUGCUCC"
```

Individual characters can be accessed using index notation. For example, the first character:

```{code-cell} ipython3
print(sequence[0])
```

or by looping over the string we can access and print each character in turn:

```{code-cell} ipython3
for i in range(len(sequence)):
    print(sequence[i])
```

:::{exercise}
:label: exercise_1

Write a program which loops over the characters of a string `s` **three at a time** and prints out each three-character substring. If the number of characters is not divisible by three, ignore the trailing characters. For example, if `s` is

```s = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"```

then your program should print
```
ABC
DEF
GHI
...
VWX
```
:::

A **list** is a Python data type that contains a sequence of values. The values can be of any type, but in this workshop we will mainly be working with lists of strings.

Use indexing to access items:

```{code-cell} python3
data = ["ABC", "DEF", "GHI", "JKI", "LMN"]
print(data[0])
```

Conversely, use the `list.index` function to find the index of a specific item:

```{code-cell} python3
i = data.index("JKI")
print(i)
```

:::{exercise}
:label: exercise_2

The two lists `list1` and `list2` below describe a character translation table. Given a string, each `A` should be translated to `H`, `B` to `A`, `C` to `E` and so on. For example, the string `EFGC` should be translated to `DICE`.

Write a program which translates the string `s_in`. Loop over the charcters in `s_in`, and for each character
-  use `list1.index` to find its index in `list1`
-  look up the character at the equivalent index in `list2`
-  use `+=` to append the character to `s_out`

```
list1 = ["A", "B", "C", "D", "E", "F", "G", "H", "I"]
list2 = ["H", "A", "E", "F", "D", "I", "C", "G", "B"]

s_in = "EFGC"
s_out = ""

for c in s_in:

  # enter your code here

print(s_out)
:::

## RNA Translation

In biology, an RNA sequence consists of a chain of the nucleotides Adenine, Uracil, Cytosine and Guanine in a specific order. We can represent an RNA sequence by a string consisting of the four letters `A`, `U`, `C` and `G`.

```{figure} rna.png
---
name: RNA sequence
---
An RNA sequence represented by the string `AUGAGACUCUGAGAC`. The sequence is composed of three-character subsequences called codons, each of which identifies a specific amino acid. 
```

```{margin} Amino Acid Translation Table

|Amino Acid| | codons |
|---|---|---|
|Glycine|G|GGA, GGU, GGG, GGC|
|Alanine|A|GCA, GCU, GCG, GCC|
|Valine|V|GUA, GUU, GUG, GUC|
|Leucine|L|UUA, UUG, CUU, CUC, CUA, CUG|
|Isoleucine|I|AUA, AUU, AUC|
|Serine|S|UCA, UCU, UCG, UCC, AGU, AGC|
|Threonine|T|ACA, ACU, ACG, ACC|
|Cysteine|C|UGU, UGC|
|Methionine (start)|M|AUG|
|Lysine|K|AAA, AAG|
|Arginine|R|AGA, AGG, CGA, CGU, CGG, CGC|
|Histidine|H|CAU, CAC|
|Proline|P|CCA, CCU, CCG, CCC|
|Aspartic Acid|D|GAU, GAC|
|Asparagine|N|AAU, AAC|
|Glutamic Acid|E|GAA, GAG|
|Glutamine|Q|CAA, CAG|
|Phenyl Alanine|F|UUU, UUC|
|Tyrosine|Y|UAU, UAC|
|Tryptophane|W|UUG|
|(stop)||UAA, UAG, UGA|
```

In the body, the RNA sequence is used to produce a protein in a process called translation. The sequence is first divided into three character subsequences termed 'codons'. For example, the 15 character RNA sequence `AUGAGACUCUGAGAC` is divided into the codons `AUG`, `AGA`, `CUC`, `UGA`, and `GAC`. Each codon either identifies a specific amino acid within a protein, or a 'start' or 'stop' instruction.

Given an RNA sequence, the amino acid-encoding codons (in **bold**) lie between with the first 'start' codon and the first 'stop' codon (in <span style="color:red">red</span>).

GCAU<span style="color:red">**AUG**</span>**UUCAUA**<span style="color:red">UGA</span>AUA

Each of the codons identifies a specific amino acid, as shown in the amino acid translation table on the right. The RNA sequence `AUGAGACUCUGAGAC` would therefore be translated by the body into the amino acid sequence `methionine`, `arginine`, `leucine`, `(stop)`, `aspartic acid`. Using the abbreviated one-letter characters, this could be written as `MRL.D`.

Finally, the body chains together these amino acids into a protein. The stop codon represents the end of the chain, so the RNA sequence would be translated into a protein comprising a chain of three amino acids `methionine-arginine-leucine`.

When translating the RNA to a protein, the following steps are followed:

1. Read along the sequence until the start codon `AUG` is found.
2. Read along the sequence three characters at a time. Look up each three character codon in the translation table to determine the corresponding amino acid.
3. Stop when the first stop codon (`UUA`, `UAG` or `UGA`) is found.

The above sequence therefore comprises the following three codons:

```none
AUG
UUC
AUA
```
and translates to the amino acid sequence:

```none
MFI
```

Your goal is to write a program which translates a string representing RNA sequence into a string representing the sequence of amino acids after translation.

### Step 1

Write a function `start_index(sequence)` that returns the index position of the first occurrence of the start codon `AUG` in the given string `sequence`.

Loop over the characters in the string and check whether each three character substring is equal to the 'start' codon, `AUG`. Once you find the start codon, use the `break` keyword to exit the loop then return the index position.
 
```
def start_index(sequence):
    # loop over characters in the string
    # return the index of first occurrence of 'AUG'

j = start_index(rna_seq)
print(j)
# Should print 4
```

### Step 2

Write a function `translate` which returns the one-character amino-acid string corresponding to the given three-character codon.

```
def translate(codon):
    # look up codon in the translation table

x = translate("AAA")
print(x)
# Should print 'K'
```

### Step 3

Write a function `translate_sequence` which which returns the amino acid sequence corresponding to the given RNA sequence. Your function should call `start_index` in order to determine the start position. Then it should loop over the characters in `sequence`, 3 characters at a time, until one of the stop codons is found. For each 3-character codon, call `translate` to determine the corresponding amino acid character. Return the string formed by concatenating the amino acid characters.

```
def translate_sequence(sequence):
    # Determine the start index
    # Loop over 3-character substrings of sequence until one of the three stop codons is found
    # Call translate on each codon
    # Concatenate the resulting characters

rna_seq = "GCAUAUGUUCAUAUGAAUA"
aa = translate_sequence(rna_seq)
print(aa)
# should print 'MFI'
```

### Step 4

Test your finished program against the following RNA sequences:

```
rna_1 = "CAACAAUGCUCCCCGCCUAGUUG"
# should return 'MLPA'

rna_2 = "UAAAAUGAAUAAUAGAUAA"
# should return 'MNNR'
```

# Exercises

## Exercise 1

What image does the data in the string `shape_data` represent?

```
shape_data = "13,1; 14,1; 15,1; 16,1; 17,1; 18,1; 12,2; 14,2; 15,2; 16,2; 17,2; 18,2; 19,2; 11,3; 12,3; 14,3; 15,3; 16,3; 17,3; 18,3; 19,3; 20,3; 10,4; 16,4; 17,4; 18,4; 19,4; 20,4; 10,5; 17,5; 18,5; 19,5; 20,5; 21,5; 17,6; 18,6; 19,6; 20,6; 21,6; 9,7; 18,7; 19,7; 20,7; 21,7; 9,8; 18,8; 19,8; 20,8; 21,8; 9,9; 10,9; 12,9; 14,9; 16,9; 17,9; 18,9; 19,9; 20,9; 21,9; 9,10; 16,10; 18,10; 19,10; 20,10; 21,10; 9,11; 18,11; 19,11; 20,11; 21,11; 22,11; 9,12; 18,12; 19,12; 20,12; 21,12; 22,12; 8,13; 9,13; 10,13; 14,13; 17,13; 18,13; 19,13; 20,13; 21,13; 22,13; 8,14; 9,14; 10,14; 13,14; 17,14; 18,14; 19,14; 20,14; 21,14; 22,14; 8,15; 9,15; 10,15; 13,15; 14,15; 17,15; 18,15; 19,15; 20,15; 21,15; 22,15; 8,16; 9,16; 10,16; 11,16; 16,16; 17,16; 18,16; 19,16; 20,16; 21,16; 22,16; 8,17; 9,17; 10,17; 11,17; 15,17; 16,17; 17,17; 18,17; 19,17; 20,17; 21,17; 22,17; 8,18; 9,18; 10,18; 11,18; 12,18; 14,18; 15,18; 16,18; 17,18; 18,18; 19,18; 20,18; 21,18; 22,18; 9,19; 10,19; 11,19; 12,19; 13,19; 14,19; 15,19; 16,19; 17,19; 18,19; 19,19; 20,19; 21,19; 22,19; 9,20; 10,20; 11,20; 12,20; 13,20; 15,20; 16,20; 17,20; 19,20; 20,20; 21,20; 22,20; 23,20; 10,21; 11,21; 12,21; 13,21; 19,21; 20,21; 21,21; 22,21; 23,21; 20,22; 21,22; 22,22; 23,22; 9,23; 10,23; 20,23; 21,23; 22,23; 23,23; 24,23; 8,24; 9,24; 10,24; 20,24; 21,24; 22,24; 23,24; 24,24; 25,24; 8,25; 9,25; 10,25; 20,25; 21,25; 22,25; 23,25; 25,25; 26,25; 7,26; 8,26; 9,26; 20,26; 21,26; 25,26; 26,26; 27,26; 6,27; 7,27; 8,27; 19,27; 24,27; 25,27; 26,27; 27,27; 28,27; 5,28; 6,28; 7,28; 8,28; 22,28; 23,28; 24,28; 25,28; 26,28; 27,28; 28,28; 29,28; 5,29; 6,29; 7,29; 8,29; 9,29; 20,29; 21,29; 22,29; 23,29; 24,29; 25,29; 26,29; 27,29; 28,29; 29,29; 4,30; 5,30; 6,30; 7,30; 8,30; 9,30; 10,30; 11,30; 12,30; 19,30; 20,30; 21,30; 22,30; 23,30; 24,30; 25,30; 26,30; 27,30; 28,30; 29,30; 3,31; 4,31; 5,31; 6,31; 7,31; 8,31; 9,31; 10,31; 11,31; 12,31; 13,31; 14,31; 15,31; 16,31; 17,31; 18,31; 19,31; 20,31; 21,31; 22,31; 23,31; 24,31; 25,31; 26,31; 27,31; 28,31; 29,31; 30,31;"
```

The  string contains a sequence of x and y co-ordinates where each x, y pair is separated by a semi-colon. Extract the co-ordinates into two separate lists `x_coords` and `y-coords` then plot them on a scatter plot.

- use `string.split` to generate a list of co-ordinate pairs
- loop over the list and split each pair into x and y co-ordinates
- convert each to a number and add to lists `x_coords` and `y_coords`
- plot using `plt.scatter(x_coords, y_coords)`

Adapt your code so that it plots the image the correct way up in a figure of suitable size.

## Exercise 2: Letter Frequencies

First download the following files from Moodle then upload into your working folder.

 - english.txt
 - french.txt
 - spanish.txt

Write a program which counts the frequency of each letter in the file `english.txt`, and displays the results as a [bar graph](https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.pyplot.bar.html). Make sure to include upper and lower case characters but do not count them separately. Do not count punctuation or spaces.

```{image} alphabet.png
:width: 400px
```

Use the following code to load the contents of the text file into a string variable:
```
with open("english.txt") as f:
     text = f.read()
```

Hint: create a variable to store the alphabet and use `string.find` to locate each character in the alphabet.
