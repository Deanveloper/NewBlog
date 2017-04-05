---
layout:     post
layout: post
title: "JavaScript Quirks"
date: "2017-02-11 18:40:34 -0500"
---
JavaScript is an... *interesting* language. It was created in 10 days by someone
who worked for NetScape in 1995, Brenden Eich. Not to say that Brenden isn't
super smart, because he is, but JavaScript... isn't. Let's talk about it.

## Equality
JavaScript has two different equality operators. First, there's `==`, which
checks if two variables are equal, so let's take a look at that.

If we do `1 == 1` we get `true` back, as one would expect. `"hi" == "hi"` too.
But if we do something like `1 == "1"` we get... `true`. Why's that? Because
`==` isn't really an equality operator. It's a "well it kinda equals the value,
so whatever we'll just call it equal" operator. You might think, "well, it could
be similar to `.equals(obj)` in Java, right?" and the answer is no.
`{} == {}` gives back `false`, even through their contents are equal. The `==`
operator is pretty much evil, so stay away from it. If you really want to mess
around with it, [here][equality] is a truth table so you can find out everything
that "equals" eachother in JavaScript.

Fun fact, `[1] == true` and `[0] == false`. Just thought I'd let you know.

But there's the `===` operator, which is nice. It actually *works*.
`1 === "1"` returns `false`. Anything that is not actually *equal* to eachother
is not `===` to eachother. `===` is the real equality operator.

TL;DR: Don't use `==`. Always use `===`.

## Non-values
So most languages have `null`, right? There's also `NaN` (it stands for
Not a Number, for those who don't know), which is sorta-kinda a value,
but it's there. Well, JavaScript has another non-value,
`undefined`. Both `null` and `undefined` are non-values to describe variables,
so what's the difference between them?

Well first of all, `null` is specifically for objects. `null` is essentially
what `NaN` is for numbers, but `null` is for objects instead. `undefined` is
what a variable is before it is assigned. So `undefined` means that a variable
hasn't been assigned yet, while `null` means "this is assigned, but assigned
as no-value".

## Scopes
Let me give you a block of code and tell me what it should print.
{% highlight JavaScript %}
function foo() {
  str = "Well hello there!";
}
foo()
console.log(str)
{% endhighlight %}
If you guessed anything like `undefined`, `null`, or throwing an error, you'd
be wrong! It in fact does print `Well hello there!`. But why? Well, because
`str` wasn't declared as a `var`, JavaScript decides to assign our string to
a global variable. Probably not expected behavior here.

But let's take a look at this snippet of code!
{% highlight JavaScript %}
var str = "Hello, world!"
function foo() {
  console.log(str)
  var str = "Hi!";
}
foo()
{% endhighlight %}
Now, what should this print out? Well, `str` was defined as `Hello, world!`
before the function is called, so it should print that out. But, well, it
doesn't. It states that `str` is undefined! Why is that?

Well, JavaScript looks through the function to see if it has any function-scope
variables. In this case, it sees `str` is defined as function-scope, later in
the function, therefore the entire function will use a function-scoped `str`.
Because the function-scoped `str` hadn't been defined before the `console.log`,
`undefined` is outputted.

## Conclusion
JavaScript is definitely a language that has a lot of weird things about it.
Even with the strange parts about the language, it is still extremely
powerful and useful.

[equality]: https://dorey.github.io/JavaScript-Equality-Table/
