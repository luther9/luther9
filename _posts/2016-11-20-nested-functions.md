---
layout: post
title: Nested Functions
---

First, a definition:

**constant:** Any variable whose value will be exactly the same and never change
  every time the program runs. (I don't know if this term should apply to
  variables that are supposed to be initialized by data files that come with the
  software package.)

In Python, I used to think it was stupid to always write a main function. Class
and function definitions are all just variable assignments, so how you would
you decide what does and does not go inside the main function? Then I realized
the main function is there to keep variables local. Classes and functions are
usually constants, which don't need to be local. The main function allows us to
confine all stateful variables to a specific scope without polluting the global
namespace.

Note that Lua does not have as great a need for a main function, because a Lua
variable does not go into scope until after its declaration. If you simply use a
comment to separate your constants from your main program, that would have a
similar effect to a main function. Python, on the other hand, hoists its
variables, so any global variable is in scope for the entire file, even it you
don't assign to it until near the end of that file.

Given all that, is it a good idea to nest functions to cut down parameter lists?
When I don't use a main function, and I need to repeat some code, I will want to
write a function, and I don't want to pass an argument that doesn't change
within the context where the code is repeated. But would that make functions
more cryptic?

In a language like Go or Ruby, it is generally more convenient to put all
functions at the top level. This is even more true for languages that don't
support closures. In such languages, we should pass all stateful data as
arguments to the functions that need them.

In Python and Lua, a nested function looks basically the same as a top level
function. I should note that closures are not constant, because they carry
references to upvalues. Here are the arguments against using nested functions:

1. If we don't nest, we can factor more code into the constant portion of the
program. Actually, each function has its own state (while it's running), and
it's easier to understand the program state when it's broken up into pieces.
2. If we nest, all functions would end up nested inside main(), almost defeating
the purpose of that function.

At present, I feel these arguments outweigh the benefit of short parameter
lists. We probably should not nest a function unless we really need a closure.

In _Structure and Interpretation of Computer Programs_, a book about Scheme, in
section 1.1.8, the authors recommend nesting functions. Aside from the reasons
I've already discussed, they also cite the problem of namespace packaging. Most
languages have their own features for protecting namespaces, so it's usually not
a big problem. I also suspect that since functional programmers go out of their
way to avoid modifying state, the dichotomy between constants and other
variables might not be as big of a deal to them.

**Update:** Experimentation shows that Python does not, in fact, hoist its
  variables, so I'm still not sure why a main function is useful in Python.
