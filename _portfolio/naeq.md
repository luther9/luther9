---
layout: post
title: naeq
feature-img: "img/naeq.png"
short-description: naeq is a numerology tool for calculating the values of words.
---

# Summary

This is about writing a simple command-line utility in Go.

# Explanation

In the past, I've been interested in [New Aeon English
Qabalah](https://en.wikipedia.org/wiki/English_Qabalah#ALW_Cipher). This has
made it useful to have an easy way to calculate the sums of words and phrases.

# Choice of Language

I prefer a compiled language for two reasons.

* It runs more efficiently.
* There is some inherent error-checking in the compilation process.

Overall, a compiled language makes me feel like the product is as finished as
possible before I run the program.

I chose Go, because garbage collection removes a whole class of bugs, because
its syntax is a vast improvement over that of C, and because strong typing makes
the code even more explicit.

# Prime Algorithm

I use a [Sieve of
Eratosthenes](https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes) to get a list
of prime numbers. Since naeq may have to evaluate more than one number during a
run, I made it so it can increase the maximum prime without having to
recalculate all the primes from the beginning.

The struct for the prime list (`primeList`) contains 3 fields. Since they must
be kept in sync for the algorithm to work, I wrote a constructor and a method to
bundle the code for `primeList`, even though they each get called only once.

# Structuring for -f
