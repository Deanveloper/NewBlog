---
layout:     default
title:      "Getters, Setters, and Why You Should Use Them"
date:       2016-12-13 5:45:00
---
I remember when I was a beginner programmer, I would always expose the
fields of my classes. I did this because in my head, I would think
something along the lines of "Well, if I intend on letting people change
the field, why should I use getters and setters? That means typing an extra
few characters in order to access the value, how inconvenient." This blog post
will explain why I was wrong in my naive little brain. This is why you should
use getters and setters.

### What are getters and setters?
---
If you are new to programming, you may be asking yourself this question. Getters
and setters are sometimes called "accessors" and "mutators" respectively.
Anyway, as you use different coding libraries, you might start to notice a trend.
You don't see much of anything like `MyAPI.value` or `ThisLib.foo = "bar"`,
rather, you probably see everything as `MyAPI.getValue()` and `ThisLib.setFoo("bar")`.
These are what we call getters and setters. A lot of the time, getter and setter
methods look just like a simple
{% highlight Java %}
public String getValue() {
    return value;
}
{% endhighlight %}
You may ask yourself, "Well what's the point of these, why not just expose the `value` field?"
Well that's what we're about to get into.

### Getters and setters can provide restrictions
---
Let's say that you have a String in a library you are building, and you
*never* want it to be `null`. Well if you expose the string as a field, there is no
way you can stop a user from setting your string to null, and throwing `NullPointerException`s
all over the place! How can we prevent this? With setters, of course! Here's an example of how you
could guarantee that your String will never, *ever* be null.
{% highlight Java %}
public void setValue(String newVal) {
    if (newVal == null) {
        throw new IllegalArgumentException("value cannot be null!");
    }
    value = newVal;
}
{% endhighlight %}
This way, your library can guarantee that `value` will never be null, and you can guarantee
to users of your library that `getValue()` will never be null either.

### Debugging
---
This one is pretty simple. Using getters and setters allow for debugging,
so you can monitor *when* a value is get/set. For instance, you can do something like this:
{% highlight Java %}
public void setFoo(String newFoo) {
    System.out.println("foo changed: " + foo + " -> " + newFoo);
    foo = newFoo;
}
{% endhighlight %}
This means that each time `foo` is set using `setFoo(newFoo)`, `foo changed: old -> new`
will be displayed in the console. This is really useful for debugging to see when values
have been changed, allowing you to do more research as to why something isn't they way it
should be.

### Different access modifiers
---
Here's another simple one. Getters and setters can have different access modifiers. This means
that you can make your getter `public` so that everyone can read the variable, but make the
setter `package-local (aka no modifier)` so that no one has access to change it except you.

### Hiding internal representation
---
One thing that I really like is using an API that uses interfaces. But interfaces
can't define fields, so often they will provide getter and setter methods within
the interface, and let the implementation (not exposed to the developer) handle
what the getters and setters do. What would happen if one day, you decided that
you didn't want to store `value` in a field anymore, but rather in a database?
If you exposed the field, then you would need to get rid of it, and break any
APIs that are built around using that field. But in the getter, it's just a simple
change from `return this.value;` to `return fetchFromDatabase("value");`, or however you
want to represent it internally. This means that from the programmers point of view,
they are still calling `getValue()` just as they were before, and they're still getting
the value, just in a different fashion. Because the programmer's code is able to stay the same,
their code doesn't break. Being able to hide the internal representation also allows us to
do some really cool stuff, such as lazy loading.

### Lazy loading
---
The huge advantage of getters is the ability to take advantage of "lazy" loading.
This means, calculate the value once, and then return a cached version of the value after that. It
sounds kinda confusing, so let's give an example similar to the previous one.

Let's say I'm going to use the [Star Wars API](https://swapi.co) to try to get
which movies Darth Vader was featured in, but I don't want to check the website every time
I call the `getMovies()` method. Rather, the first time the method is called, we will go to the
website, and store the data into a variable!
{% highlight Java %}
/** gets movies darth vader was in */
public List<Movies> getMovies() {
    if (movies == null) {
        movies = getMoviesFromWebsite("http://swapi.co/api/people/4/");
    }
    return movies;
}
{% endhighlight %}
This not only means that `getMovies()` only performs the http request once, but if it
is never used, it never performs the http request at all (as it was not needed)!
This is a huge performance advantage and is used a lot throughout many libraries!

### Lambda expressions
---
Last and definitely the least, methods can be passed through a lambda easily while fields cannot.
Methods can use the `ClassName::methodName` syntax, while fields are stuck with the normal lambda syntax.
This is because lambdas need to execute a piece of code, and fields do not execute anything, rather they
only represent a value. The equivalent to `OurClass::getValue` to get the value through a field would be
`() -> OurClass.value` which is a bit cumbersome to type out. It's a minor detail and a probably
very complicated for those who don't understand lambdas, but I thought I would include it as a StackOverflow
article listed it as an advantage.

### But getters and setters require so much code! (Properties!)
---
That is where you're right. Each getter and setter is at least 3 lines each, which,
for how simple of a task they do, is just wrong. The concept of properties fix this problem, but that is
a subject for another time.

Please leave any comments you have in the Disqus below. Also share this with beginner developers
to get them started on using getters and setters early!
