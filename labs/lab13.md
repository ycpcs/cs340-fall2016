---
layout: default
title: "Lab 13: Recursion in Clojure"
---

Getting Started
===============

Start a new Clojure project in Eclipse using **New &rarr; Project &rarr; Clojure &rarr; Clojure Project**.  Name the new project **lab13**.

Open the file **src/lab13/core.clj**.  Create your functions in this file.  When you are ready to test your functions, start a REPL by right-clicking in the editor and choosing **Clojure &rarr; Load file in REPL**.  When you modify your code, do the same thing to reload your definitions in the REPL.

If you would prefer to use Light Table, or edit your code in a text editor and run the Clojure REPL from the command line, feel free.

Your Task
=========

There are 4 tasks.

<div class="callout"><b>Important</b>: Implement each function using recursion.  Where specified, use the <code>recur</code> or <code>loop</code>/<code>recur</code> forms.</div>

### First task

Write a Clojure function called **last-element-of** which takes a non-empty list and returns the last element.

Hints:

-   the **first** returns the first element in a list
-   the **rest** function returns a list containing every element of a list except the first one
-   the **empty?** function returns a true value if called with an empty list as its argument, false otherwise

Example:

{% highlight clojure %}
user=> (last-element-of '(:a :b :c))
:c
{% endhighlight %}

### Second task

Write a Clojure function called **append-to-list**. It should take two parameters:

1.  a value
2.  a list

It should return a new list containing all of the values in the original list, with the value appended as a new last element.

Hints:

The cons function, given a value and a list as arguments, returns a new list containing the value as the first element of the list, followed by all elements of the original list

Example:

{% highlight clojure %}
user=> (append-to-list :d '(:a :b :c))
(:a :b :c :d)
{% endhighlight %}

### Third task

Write a function called **reverse-list** which reverses the elements of a list given as its parameter.

Hint: Use your **append-to-list** function.

Example:

{% highlight clojure %}
user=> (reverse-list '(:a :b :c :d))
(:d :c :b :a)
{% endhighlight %}

### Fourth task

Find out how long a list needs to be for your **reverse-list** function to fail because it requires a new activation record for each recursive call.

You can use the following **make-int-list** function to generate a list with a specified number of elements:

{% highlight clojure %}
(defn make-int-list-work [min n accum]
  (if (> min n)
      accum
      (recur min (- n 1) (cons n accum))))

; Make a list containing all integers from 1 to n.
(defn make-int-list [n]
  (make-int-list-work 1 n '()))
{% endhighlight %}

Here is a more compact version of **make-int-list** that uses the **loop** construct:

{% highlight clojure %}
(defn make-int-list [minval nval]
  (loop [min minval
         n nval
         accum '()]
    (if (> min n)
      accum
      (recur min (- n 1) (cons n accum)))))
{% endhighlight %}

For example, the call

{% highlight clojure %}
(make-int-list 100)
{% endhighlight %}

will generate a list of all integers from 1 to 100. So, you just need to find a value *N* such that

{% highlight clojure %}
(reverse-list (make-int-list N))
{% endhighlight %}

fails.

Once you have determined a list size *N* that will make the **reverse-list** function fail:

Write a "tail-recursive" function called **reverse-tail-rec** to reverse the elements of a list. Show that it succeeds in reversing the list that caused your non-tail-recursive list reversal function to fail.

**Note**: Clojure doesn't support true tail recursion (because the underlying Java Virtual Machine doesn't support it). So, you will need to use the **recur** special form. (See the **make-int-list-work** function above for an example.)

Interestingly, reversing a list is *easier* to do using tail recursion.