---
layout: default
title: "Assignment 1: Regular expressions"
---

**Due: Tuesday, Sep 6th by 11:59 PM**

# Regular Expressions

For each language below, create a regular expression that generates all of the strings in the language, and does not generate any strings not in the language.

In the language descriptions below, *ε* (epsilon) denotes the empty string.

# Strategy

Sometimes it isn't obvious how to create a single regular expression that generates precisely the language you want.

The good news is that you don't need to tackle the entire language all at once.  An excellent strategy is to work on a regular expression that generates *part* of the language.  Then work on another, and so on, until together they generate all of the strings in the language.  Then, you can use the alternation operator (\|) to combine them.

For example, let's say you want a regular expression for language *Z*.  <i>R<sub>Z</sub></i> is the regular expression which will generate the language *Z*.  But you don't yet know what <i>R<sub>Z</sub></i> should be.

So, you create regular expressions <i>R<sub>P</sub></i>, <i>R<sub>Q</sub></i>, and <i>R<sub>R</sub></i>, which generate languages *P*, *Q*, and *R*, such that

> *Z* = *P* ∪ *Q* ∪ *R*

That means that <i>R<sub>Z</sub></i> should be

> <i>R<sub>P</sub></i> \| <i>R<sub>Q</sub></i> \| <i>R<sub>R</sub></i>

Note that for this example, it is not necessary for languages *P*, *Q*, and *R* to be non-overlapping.  In other words, there might be some strings that are in more than one of *P*, *Q*, and *R*.  That is fine!  The only requirement is that all of the strings in *Z* are in the union of *P*, *Q*, and *R*.

As a specific example, let's consider Language 2 from [Lab 1](../labs/lab01.html), which is the language of all strings of strictly alternating **a**'s and **b**'s.  Let's break this language down into four subsets:

* Even length strings starting with **a**
* Odd length strings starting with **a**
* Even length strings starting with **b**
* Odd length strings starting with **b**

Here are four regular expressions which generate each of these subsets:

* (ab)\*
* (ab)\*a
* (ba)\*
* (ba)\*b

Now we can put them all together as a single regular expression:

> (ab)\*\|(ab)\*a\|(ba)\*\|(ba)\*b

# Languages

Language 1
----------

Create a regular expression that generates the language of all strings over the alphabet {a, b, c} of the form:

<pre>
a
ac
acab
acabab
acababab
acabababab
<i>etc...</i>
</pre>

In other words, an **a**, optionally followed by **c**, optionally followed by 1 or more occurrences of **ab**.

Note that the empty string is not in this language.

Language 2
----------

Create a regular expression that generates the language over the alphabet {a, b} of all strings in which each **b** is preceded by at least one **a**.

Examples of strings in the language:

<pre>
<i>ε</i>
a
aaaa
ab
aba
abaabaaaab
</pre>

Examples of strings not in the language:

<pre>
b
abb
bba
</pre>

Language 3
----------

Create a regular expression that generates the language over the alphabet {a, b} of all strings containing an even number of **b**s.

Examples of strings in the language:

<pre>
<i>ε</i>
a
aa
aaa
abba
bb
bab
abbaa
aababbb
</pre>

Examples of strings not in the language:

<pre>
b
abbb
babab
abbbabab
bbaaba
</pre>

Hint: make sure that your regular expression generates **b**s in pairs.

Language 4
----------

Create a regular expression that generates the language over the alphabet {a, b, c} of all strings in which a **b** is never followed by a **c**.

Examples of strings in the language:

<pre>
<i>ε</i>
ab
abba
abac
cab
cba
bac
aac
c
</pre>

Examples of strings not in the language:

<pre>
bc
abc
bca
aabcab
</pre>

This one will be fairly challenging!

The key is to construct the regular expression to grow the generated string in a way that,

-   it never adds a chunk that contains **bc** (obviously)
-   if the current string ends in **b**, it never adds a chunk that begins with **c**

Language 5
----------

Create a regular expression that generates the language over the alphabet {a, b} of all strings in which

> *n* mod 3 = 2

where *n* is the length of the string. In other words, all strings in the language have a length of 2, or 5, or 8, or 11, etc.

Examples of strings in the language:

<pre>
ab
bb
baabb
aaaaa
abbbbbba
</pre>

Examples of strings not in the language:

<pre>
ε
a
abb
baaa
babbba
</pre>

Hint: generate two initial letters, and expand the string by appending chunks of length 3.

Testing
=======

You should test your regular expressions to ensure that:

1.  They generate all of the strings in the language
2.  They do not generate any strings not in the language

You can use the [regexChecker.jar](../resources/regexChecker.jar) from [Lab 1](../labs/lab01.html) to test your regular expressions.

Submitting
==========

Submit your regular expression in a **plain text file** to Marmoset as **assign01**:

> <https://cs.ycp.edu/marmoset>

Use a text editor such as Notepad++ to create the plain text file.

Do not submit a Word document, PDF, RTF, etc.
