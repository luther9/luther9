---
layout: post
title: How to Convert a Multi-Dimensional Loop Into a Recursive Function
---

While doing [exercise 1.12 from Structure and Interpretation of Computer
Programs](https://mitpress.mit.edu/sicp/full-text/book/book-Z-H-11.html#%_sec_1.2.2),
I needed to learn an interesting technique for recursion. How does one write a
nested loop in functional programming, i.e. recursively?

For example, consider this 2-dimensional loop:

{% highlight python %}
#!/usr/bin/python3

for y in range(20):
    for x in range(y + 1):
        print('{:3} '.format(x * y), end='')
    print()
{% endhighlight %}

How would this loop look in Scheme? Think of the problem in these steps:

1. You will only write one function. (You don't need to write a function for
every `for` loop.)
2. Every looping variable, along with any other state that changes along the
course of the operation, must become a parameter to the function.
3. Every `for` loop becomes an `if` statement which helps the function determine
where it is in the process.

This is the final product in Scheme:

{% highlight scheme %}
#!/usr/bin/guile
!#

(use-modules (ice-9 format))

(define (show n-rows x y)
  ; This first condition detects whether we are at the end of the entire
  ; operation.
  (when (< y n-rows)
	; Check to see if we're at the end of a row.
	(if (> x y)
	    ; Reset x and increment y.
	    (begin
	      (newline)
	      (show n-rows 0 (1+ y)))
	    ; If the condition was false, do the stuff in the innermost loop.
	    (begin
	      (format #t "~3d " (* x y))
	      ; Increment x. y stays the same, because it's the outer loop
	      ; variable.
	      (show n-rows (1+ x) y)))))
; Start x and y at 0.
(show 20 0 0)
{% endhighlight %}

The output of both programs should be identical.
