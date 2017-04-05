---
layout:     post
layout: post
title: "Basic Sorting Algorithms"
date: "2017-01-26 11:40:49 -0500"
---
Sorting algorithms are a very interesting topic. There are several
of them out there, getting from as simple as bubble sort, to as complex
as radix sort. This post will talk about several sorting algorithms, and
hopefully simplify them as much as possible for you.

## Bubble Sort
Bubble sort is probably the simplest of them all. What bubble sort does
is compare the first two elements, and if the second one is smaller than the
first one, it swaps them. Then it does the same thing to the next two elements.
The algorithm will do this to the entire list, and if it isn't sorted, it will
keep looping through the list and swapping adjecent elements until it is sorted.

**Visualization** (these visuals start out slow but speed up over time)
<iframe width="560" height="315" src="https://www.youtube.com/embed/Cq7SMsQBEUw" frameborder="0" allowfullscreen></iframe>

**When is it most efficient?** When a list is nearly sorted. Order: `O(n)`

Note that `O(n)` is *amazing* efficiency. That's the best out there for sorting
algorithms. But that's only on nearly sorted lists.

**When is it least efficient?** On a reverse-ordered list. Order: `O(n^2)`

This is quite bad, actually. Bubble sort takes quite a long time to sort
really anything that *isn't* nearly sorted. In fact, it's not just on
reverse-ordered lists that bubble sort is really bad on. Any time one of the
smaller elements is near the end of the list, it performs terribly. Let's take
the list `[2, 3, 4, 5, 1]`. Here's how a bubble sort would work on it...

 * `[2, 3, 4, 5, 1]`
 * `[2, 3, 4, 1, 5]`
 * `[2, 3, 1, 4, 5]`
 * `[2, 1, 3, 4, 5]`
 * `[1, 2, 3, 4, 5]`

It moves that `1` over one at a time, and does a full traversal each time.
Bubble sorts aren't looked at too kindly, so let's take a look at
some other algorithms.

## Insertion Sort
Insertion sort is a good competitor to bubble sort. It's really just a bubble
sort on some kind of performance drug. It's a little more complex,
but way more efficient. What insertion sort does is assume that part of the list
is sorted, and then insert the unsorted part of the list into the correct place
in the sorted part of the list.

**Visualization**
<iframe width="560" height="315" src="https://www.youtube.com/embed/8oJS1BMKE64" frameborder="0" allowfullscreen></iframe>

Notice that to the left of the green bar, the list is sorted. Then it takes
the element to the right of the green bar, and reverse-bubble-sorts it into the
list. This is a much more efficient way to sort. The only real advantage that
bubble sort has over insertion sort is that it's easier to code.

**When is it most efficient?** When a list is nearly sorted. Order: `O(n)`

Again, `O(n)` is the best efficiency you can get on a list.

**When is it least efficient?** On a reverse-ordered list. Order: `O(n^2)`

Insertion sort has similar efficiency to bubble sort in its worse case.
However, it is still much faster than bubble sort in most cases, so it is
usually recommended over bubble sort.

## Selection Sort
Selection sort is another sort that is pretty simple. What it does is scan the
list for the smallest value, and swaps it with the first value. Then it scans
for the next smallest and swaps it with the second value. This goes on until
the entire list has been sorted.

**Visualization**
<iframe width="560" height="315" src="https://www.youtube.com/embed/92BfuxHn2XE" frameborder="0" allowfullscreen></iframe>

**When is it most efficient?** Never. `O(n^2)`

**When is it least efficient?** Never. `O(n^2)`

No matter what, selection sort always sorts through the whole list, and scans
the entire unsorted portion of the list for each position. This makes it a bit
less efficient, although it is sometimes used when working with flash memory,
as selection sort doesn't perform as many write operations as the other sorts.

## Merge Sort
Merge sort will be the last of the basic sorting algorithms that we cover here.
The list gets split in half. Then those lists are split in half. The lists
continue to get split in half until all that is left is a bunch of lists of
one or two elements (making a tree-like structure). Then it swaps the elements
in the lists of two elements if they are out of order. After that,
it starts to merge the lists together. It merges the lists by looking
at the first element of each list and sets the smaller of the two to the
first element of a new list and removing it from the old one. It
continues doing this until the elements in the two small lists are used up.
Then, it does this to another pair of tiny lists. Then, it merges
the merged lists together. It's hard to explain without talking about
[binary trees], but if you know how a binary tree works, it continues merging
two sibling leaves together into a parent, then deleting the leaves (making
the parent a leaf).

**Visualization**
<iframe width="560" height="315" src="https://www.youtube.com/embed/ZRPoEKHXTJg" frameborder="0" allowfullscreen></iframe>

**When is it most efficient?** Never. `O(n logn)`

**When is it least efficient?** Never. `O(n logn)`

This sort has a good average performance, although has quite a bit of set
up time. It's not very good for sorting small lists, although for medium to
large lists (~30+ elements), it works wonders. Merge sorts usually always
take the same amount of time, whether the list is already sorted, sorted in
reverse, or completely randomized. Merge sort is a pretty safe choice for a
large list if you don't know how the elements inside of it are arranged.

# Summary
If you think you should use a bubble sort, use an insertion sort. Don't use
a selection sort unless you're on an arduino or something like that, and if
you need an efficient algorithm for a large list, merge sort is the way to go.

I will definitely make some blog posts about more sorting algorithms that are
out there, including Quick Sort, Cocktail Shaker, and Shell Sort (one that
comes from a Michigan Tech graduate!)

### EDIT - Bonus Clip!
Here's a visual of a bubble sort working over a 12,500 element list!
Don't worry, it starts to fast forward.
<iframe width="560" height="315" src="https://www.youtube.com/embed/jHPexHsDxwQ?start=567" frameborder="0" allowfullscreen></iframe>

[binary trees]: https://en.wikipedia.org/wiki/Binary_tree
