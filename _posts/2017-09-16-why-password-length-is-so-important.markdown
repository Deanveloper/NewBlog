---
layout: post
title: "Why Password Length is so Important"
date: "2017-09-16 22:57:52 -0400"
---
What if I told you how to make a password that is 400,000 times more secure, and easier to remember? Let me introduce you to passphrases. You have probably heard this before from countless people. [XKCD] talks about **passphrases** and how they are much better than passwords. It explains why passphrases are better, but doesn't really get into how simple the math really is. We won't talk anything about entropy here, since that's useless anyway if you know the math. We will be discussing brute-forcing passwords and dictionary attacks, and making some quick scripts to figure out just how secure passwords vs passphrases are.

# Short, Complex Passwords
So, let's say you have a password, around 12 characters. It has numbers and symbols. This means, assuming you're limited to the characters on a keyboard, 26 (lowercase) + 26 (uppercase) + 10 (numbers) + 10 (numbers + shift) + 10 (extra symbols) + 10 (extra symbols + shift). This brings us to 92 possible characters, and let's round up to 100 to be generous, and to make the math easy.

For a single character password, there are 100 possibilities. Two characters makes it 10000 + 100 = 10100. Many of us are programmers here, so let's write a quick python program to describe the number of possibilities that a password of length `length` or less can have.

```py
>>> def password(length):
...   if length < 0:
...     return 0
...   return 100**length + password(length-1)
```

And just to test it out (note, the program also allows for an empty password, so it is 1 larger)

```py
>>> password(1)
101
>>> password(2)
10101
```

So how about a 12 character password? Let's try putting that into our function.

```py
>>> password(12)
1010101010101010101010101
```

That's a huge number! That's a bit over a billion-billion-millions. But let's try taking a bit of a different approach to this...

# Long, Simple Passphrases
Now instead of a password, let's talk about a passphrase. Passphrases are much longer and simpler, and harder to guess than passwords are. Each passphrase is made up of words, of course. In order to keep it easy to remember, we won't even include any numbers or symbols in it. Just the 26 letters, the spacebar, hyphen, and underscore. That brings us to a total of 29 characters.

Let's make a new python function to describe the same pattern, but for passphrases.

```py
>>> def passphrase(length):
...   if length < 0:
...     return 0
...   return 29**length + passphrase(length-1)
```

And give it a couple test values.

```py
>>> passphrase(1)
30
>>> passphrase(2)
942
```

So just how hard are passphrases to brute-force? Well, let's say our passphrase is "what is the length of the average sentence", which is 42 characters. Let's put that into our function.

```py
>>> passphrase(42)
27287005492884718602602534825004439917772077566939113764846271
```

That number is very, *very* large. According to python, around `2.7e+37` times larger than the number of possible 12-character passwords! On the other hand, this does assume that they are cracking the password via brute-force, trying random letters out until a correct sequence comes up. Instead of a brute force, let's try looking at a dictionary attack.

Dictionary attack try words at a time instead of letters. This means that they are much better at cracking a passphrase. The rarest words in that passphrase are "length" (ranked 1151), and "sentence" (ranked 4675)  [(source)](https://github.com/first20hours/google-10000-english/blob/master/google-10000-english-no-swears.txt#L1154). So, let's say our attacker is looking for the 5000 most common English words.

So, of course, let's make a function to describe this!

```py
>>> def passphrase_dictionary(words):
...   if words < 0:
...     return 0
...   return 5000**words + passphrase_dictionary(words-1)
```

And test it

```py
>>> passphrase_dictionary(1)
5001
>>> passphrase_dictionary(2)
25005001
```

And finally, let's take a look at how many possibilities an 8-or-less word passphrase would have.

```py
>>> passphrase_dictionary(8)
390703140628125625125025005001
```

As you can tell, it's quite a bit less than brute-forcing, as expected. But comparing it to the original value...

```py
>>> passphrase_dictionary(8) / password(12)
386796.10922184435
```

Our passphrase is *much* easier to remember, and nearly 400,000 times more secure than our 12-character password. Also, choosing less common words in your passphrase drastically increases the security of the password! The words in the passphrase that I used were all fairly common, although it is still more secure than a randomly-generated 12 character password.

# Conclusion
Passphrases are easier to remember than passwords, while also being a lot more secure. They take a bit longer to type, sure, but you are also typing in *actual words* and not needing to constantly reach for that `shift` key. The (very) simple, easy to remember passphrase used in this example was 400,000 times more secure than a randomly-generated 12 character password. The only thing that keeps us from using passphrases everywhere are character limits, which are sometimes imposed on websites, in which case you may need to use a plain-old password. But if there's no limit, go for a nice, long passphrase.

[XKCD]: https://xkcd.com/936/
