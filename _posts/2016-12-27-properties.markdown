---
layout:     post
title: "Properties"
date: 2016-12-27 13:00:00
---
Properties and fields are two terms that I've seen used interchangeably, but
they normally aren't the same thing.

Before finishing this post, you should check out my other post about
[getters and setters](/2016-getters-and-setters), as understanding getters and
setters (and their advantages) is very important to learning about properties.

Properties are designed to fix the problem that getters and setters have, which
is all of the useless code that doesn't need to be typed. In Java, to define
a getter and setter for a field, it takes 7 lines.
```Kotlin
private String ourField;
public String getOurField() {
  return this.ourField;
}
public void setOurField(String ourField) {
  this.ourField = ourField;
}
```
But how much of this code is redundant? Well we should only need to define the
type of it once. But here we need to define it three times, once for the field,
once for the return type of the getter, and once for the parameter of the
setter. And we should only need to define the name of the variable once, so
that we don't need to keep writing `name`, `getName`, and `setName`. Instead,
there should be a design that makes it so we only define the name once.

Those two problems are exactly what properties solve. To create code (in Kotlin)
that generates the equivalent of the getters and setters from above, all you
need to type is a single line.
```Kotlin
var ourProp: String
```
This automatically creates getters, setters, and assigns them to a field.
Properties can still be manipulated easily, though. If you wanted to make sure
that the setter was private, but the getter was still public, that's a piece
of cake. Once again, let's use Kotlin to illustrate this.
```Kotlin
var ourProp: String
  private set
```
But what if you want to perform custom operations in the getter/setter? That's
a little more complicated, but still easier than creating getter/setter methods
in Java. Let's use the example of lazy loading from the Getters and Setters blog
post to show Kotlin's properties in action here.

```Kotlin
val movies: List<Int>? // The ? simply means the value can be null
  get() {
    if (field == null) {
        println("getting from swapi!")
        field = getMoviesFromWebsite("http://swapi.co/api/people/4/");
    }
    return field;
  }
  // vals have no setters; they are similar to final fields in Java
```
You might notice that the code takes up the same number of lines as it would
in Java, but the main advantage here is that it still removes a lot of the
useless code from defining the type and name multiple times.

But what do properties look like to people who are getting and setting them?
Well ideally, they look just like getting and setting fields.

```Kotlin
fun main(args: Array<String>) {
    println(movies)
    println(movies)
    println(movies)
}
```
This would only print "getting from swapi!" one time, meaning it only makes one
web request, showing that it properly caches the web request into a field, and
then returns that field all of the other times.

I hope this post has helped you understand the concept of properties and how
amazing of a feature they really are. Kotlin's implimentation of them is really
nice, and I highly recommend checking them out as this post only goes over the
very basics of properties, and there are some really powerful things you can
do with them. Several other languages also use properties, check out the
[wikipedia][wiki] article about them for more.

[getsetexample]: https://gist.github.com/Deanveloper/e40156a7ebd4eb8bcc0bc650f5f14ae4
[wiki]: https://en.wikipedia.org/wiki/Property_(programming)#Support_in_languages
