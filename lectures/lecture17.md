---
layout: default
title: "Lecture 17: Clojure reader and evaluator"
---

# Code = data

You may have noticed that Clojure code and literal Clojure data structures look quite similar.  All function applications and special forms are sequences of items in parentheses, which look a lot like literal lists.  Parameter lists and variable definitions in the **let** and **loop** forms look a lot like vectors.  And so on.

This is not a coincedence.  The Clojure language has a property called *homoiconicity*, which simply means that code and data have a common representation.

## Why this is useful

Because Clojure code is represented using Clojure data structures, it is possible to transform and generate code at runtime.  What's more, Clojure can *evaluate* data structures as code.  This raises the possibility of implementing new language features by simply writing Clojure code.

First we will need to look at how Clojure code is read and evaluated.

# The reader

The *reader* is the component of Clojure responsible for translating textual representations of Clojure code and literal data structures (remember that due to homoiconicity, these are the same!) into actual (run-time) data structures.  In other words, it is the component which turns text such as

{% highlight clojure %}
(+ 2 3)
{% endhighlight %}

into a list where the symbol **+** is the first item, the number 2 is the second item, and the number 3 is the third item.

The built-in `read-string` function applies the reader to a string and returns the resulting Clojure data structure.  E.g.:

    user=> (read-string "(if 1 2 3)")
    (if 1 2 3)
    user=> (read-string "123")
    123
    user=> (read-string "[1 2 3]")
    [1 2 3]

To be continued...

<!-- vim:set wrap: ­-->
<!-- vim:set linebreak: -->
<!-- vim:set nolist: -->
