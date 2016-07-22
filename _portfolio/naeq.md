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
of prime numbers. Since `naeq` may have to evaluate more than one number during
a run, I made it so it can increase the maximum prime without having to
recalculate all the primes from the beginning.

The struct for the prime list (`primeList`) contains 3 fields. Since they must
be kept in sync for the algorithm to work, I wrote a constructor and a method to
bundle the code for `primeList`, even though they each get called only once.

# Structuring for `-f`

The `-f` option requires `naeq` to store information about every word and
organize it. The output shows each number in order, along with every word that
corresponds to that number. That means the overall data structure consists of 3
nested parts (from inner to outer):

1. A slice of words in alphabetical order that corresponds to a particular
number.
2. A struct that holds the number and the slice of words.
3. A slice of such structs in numerical order.

As it turned out, I only had to declare the struct. The other types were only
used once, so they didn't have to be declared.

```go
type valueEntry struct {
	value int
	words []string
}
```
