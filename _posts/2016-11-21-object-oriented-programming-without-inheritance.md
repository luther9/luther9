---
layout: post
title: Object-Oriented Programming Without Inheritance
---

I've recently discovered a new trend in object-oriented programming. These days,
some people are saying that when writing a class, we should always prefer to use
composition over inheritance. This means that whenever we feel tempted to
inherit from another class, we should instead make that class an instance
variable of our new class and write wrapper methods for the methods that we need
to import into our new class. If you need polymorphic behavior, use interfaces
to fit your static types into polymorphic variables.

When we design an inheritance hierarchy, we have to make a lot of decisions
about the relationships between types that will be hard to change later.
Composition requires a bit more code, but it is much more flexible because each
class can independently decide how it uses other classes.

## What if my language doesn't have interfaces?

C++ and Python do not have a built-in concept of interfaces. This is because
they both allow multiple inheritance, and abstract classes can be written to
bahave as interfaces. When using these languages under a composition paradigm,
you may feel free to inherit from abstract classes that do not have any instance
variables.

## Go

A few years ago, I dicovered the language Go. Go does not have inheritance, and
it takes a unique approach to composition.

{% highlight go %}
type A struct {
	x int
}

// A method of A.
func (a A) getX() int {
	return a.x
}

type B struct {
	A
	y int
}

// Both A and B implement this interface.
type MyInterface interface {
	getX() int
}

var myB B
{% endhighlight %}

In the above code, type `B` **embeds** type `A`. This means we don't have to
write wrapper methods to access fields or methods of `A` from `B`. The name of
an embedded field is simply the type name. For example, `myB.A.x == myB.x`.
Furthermore, if we call `myB.getX()`, the reciever of `getX` is the `A` field,
not `myB`, so the method cannot affect or be affected by other fields in the
outer struct.

I enjoyed using Go for a few years before I found out about the trend toward
composition in other OO languages. Before I found Go, I thought that
polymorphism was the same thing as inheritance. Go taught me that polymorphism
(embodied by interfaces) is a completely independent feature that works
perfectly well without inheritance, at least in Go. I didn't realize until
recently that this principal applies just as well to other languages.
