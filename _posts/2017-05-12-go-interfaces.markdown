---
layout: post
title: "The Problem with Interfaces, and how Go Fixed it"
date: "2017-05-12 20:31:36 -0500"
---

# Interfaces are great
They're honestly brilliant. Interfaces allow for simple, elegant programming.
Let's use Java to get a quick idea of how interfaces work in most
languages.
```Java
package mypackage;

public interface Edible {
  public void eat();
}
```
Now, a `Burger` class to implement `Edible`.
```Java
package mypackage;

public class Burger implements Edible {
  public void eat() {
    System.out.println("Burgers, yum!");
  }
}
```
This means that we can use our `Burger` class wherever we see `Edible`,
such as method arguments!

# The problem with interfaces
But let's say that we are using a library, and that library has a class
called `Salad`. Here's what `Salad` looks like:
```Java
package theirpackage;

public class Salad {
  public void eat() {
    System.out.println("I'm being healthy!")
  }
}
```
So `Salad` has an `eat()` method, but because the other library doesn't even
know about `Edible` interface exists, it obviously can't implement it. This
problem has definitely been encountered before, so let's talk about how
Go has fixed it.

# How Go fixes interfaces
With how Go interfaces work, you don't need to declare an interface implementation.
If you implement the proper methods, you implement the interface. This is very
prominent in Go, and is a key feature. Let's use our previous example.

First, let's remake our `Edible` interface.
```Go
package mypackage

type Edible interface {
  Eat()
}
```
Now, let's make a `Burger` struct that implements `Edible`.
```Go
package mypackage

type Burger struct {}

// How to define a method in Go
func (b Burger) Eat() {
  fmt.Println("Burgers, yum!")
}
```
Notice that we never acknowledged `Edible` anywhere while we made
the `Burger` struct. This is because *any* type that has an `Eat()` method
associated with it is considered `Edible`. This means that even types from
other libraries can be `Edible`, as long as they have an `Eat()` method!

This means that even this `Salad` struct from a different package is `Edible`.
```Go
package theirpackage

type Salad struct {}

func (s Salad) Eat() {
  fmt.Println("I'm being healthy!")
}
```

This shows just how awesome Golang is. I highly recommend watching their
video, [A Tour of Go], which shows all of the brilliant features that Go has
to offer.

[Go]: https://golang.org
[A Tour of Go]: https://www.youtube.com/watch?v=ytEkHepK08c
