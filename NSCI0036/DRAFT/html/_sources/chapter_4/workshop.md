---
jupyter:
  jupytext:
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.3'
      jupytext_version: 1.18.1
  kernelspec:
    display_name: Python 3 (system-wide)
    language: python
    metadata:
      cocalc:
        description: Python 3 programming language
        priority: 100
        url: https://www.python.org/
    name: python3
    resource_dir: /ext/jupyter/kernels/python3
---

# Workshop 4: Lists and Strings

:::{exercise}
:label: exercise_1

Write a Python script which loops over the characters in a string and prints the three character substring starting at each character:

```
s = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
...
```
Output:
```
ABC
BCD
CDE
...
XYZ
```

:::



## Question 1

```{sidebar} Amino Acid Translation Table

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

In biology, an RNA sequence consists of a chain of the nucleotides Adenine, Uracil, Cytosine and Guanine in a specific order. We can represent an RNA sequence by a string consisting of the four letters `A`, `U`, `C` and `G`.
```
rna_seq = "GCAUAUGUUCAUAUGAAUA"
```
each three character substring identifies a 'codon' which either identifies a specific amino acid within a protein, or a 'start' or 'stop' instruction.  

Given an RNA sequence, the amino acid-encoding codons (in **bold**) lie between with the first 'start' codon and the first 'stop' codon (in <span style="color:red">red</span>).

GCAU<span style="color:red">**AUG**</span>**UUCAUA**<span style="color:red">UGA</span>AUA

When translating the RNA to a protein, the following steps are followed:

1. Read along the sequence until the start codon `AUG` is found.
1. Read along the sequence three characters at a time. Look up each three character codon in the translation table to determine the corresponding amino acid.
1. Stop when the first stop codon (`UUA`, `UAG` or `UGA`) is found.

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

By following the steps below, write a program which translates an RNA sequence into a sequence of amino-acids.

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

```python

```

## Question 2 (Optional)

First upload the following four files into your working folder in Cocalc.

<a href="../tutorial_4/english.txt" download>english.txt</a>  
<a href="../tutorial_4/french.txt" download>french.txt</a>  
<a href="../tutorial_4/spanish.txt" download>spanish.txt</a>

### Part 1
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

### Part 2
Let $A_i$ be the relative frequency of letter $i$ in text $A$, where a is letter 0, b is letter 1 etc. (E.g. if A = "alphabet!", $A_0 = 2/8 = 0.25$ since the letter a appears 2 times out of 8 alphabetic characters). We define a similarity index for two pieces of text using the following formula:

$\sum_{i=0}^{25} (A_i - B_i)^2$

Write a program which predicts the language of a piece of text by comparing the text to the each of the three languages English, French and Spanish. Relative frequencies for each these languages can be found here: https://en.wikipedia.org/wiki/Letter_frequency. (Make sure the relative frequences sum to 1!)

Your program should calculate the value of the similarity index for each of the languages then print the name of the language with the lowest score.
