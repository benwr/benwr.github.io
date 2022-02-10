---
layout: post
title: A slightly different way to generate strong, memorable passwords
date: May 31, 2021
location: Berkeley
---

It's a good idea to avoid remembering passwords - the more passwords you
need to remember, the more tempting it is to re-use them. Ideally you
should use a password manager like [Bitwarden](https://bitwarden.com) to
store almost all of your passwords[^1].

[^1]: Some people say you should use the password manager built in to your browser instead, and there are pros and cons to both approaches. I prefer Bitwarden because it can be used across all major operating systems and browsers.

But of course you can't store your Bitwarden password in Bitwarden, so it's
still necessary to memorize at least that one password. You'll probably also
want to memorize your login passwords for your PC and phone, and disk
encryption passwords for Linux-based computers. So how do you choose those
passwords to be secure and memorable?

# Entropy

If you're interested in computer security, you have probably seen the
"Correct Horse Battery Staple" XKCD comic. It advocates choosing four random
common words as your passphrase, instead of doing the traditional password
generation black magic, because these passwords can be harder to guess and
easier to remember. It's a good illustration of the concept of "entropy": In
the context of security, entropy is a measure of how difficult your password
is to guess, and it depends on how you chose the password[^2].

[^2]: Actually, [entropy isn't sufficient to measure password strength](https://www.benwr.net/2022/01/16/password_entropy.html), but it's a common and useful proxy.

For example, If you choose your password by flipping a coin 10 times, and
adding a “1” if you get heads or a “0” if you get tails, your password has 10
bits of entropy. That means that an attacker who knew your decision procedure
would have to guess, on average, \\(2^{10-1}\\) passwords in order to
successfully guess the one you chose. Adding one bit of entropy (one coin
flip) to your password doubles the number of guesses required. It’s a good
idea to incorporate as many truly random choices into your password as
possible, to ensure that it’s really unpredictable.

# Diceware

A respected way to generate secure passwords is by using the
[Diceware](https://theworld.com/~reinhold/diceware.html) word list. You sit
there rolling dice for a few minutes to choose random words. If you want your
password to have 128 bits of entropy (enough for essentially all purposes),
you can generate one by randomly choosing ten words from the Diceware list.
And if you roll a password with \\(N\\) words in it, you’ll end up with \\(N
\log_2{6^5}\\) bits of entropy.

I've used this method in the past, and it works well. But the passwords I get
are often difficult to remember: The words don't have any semantic structure,
and it's not always easy to come up with mnemonics for long lists of words.

# The Reordered Diceware method

Instead of choosing N words in order and trying to remember them in the order
you rolled them, you might try reordering the words you roll, to give them a
more memorable structure. Unfortunately you lose some bits of entropy when
doing this, and it’s important to take that into account. Pessimistically,
your password using this method could have as few as \\(log_2 {6^5 \choose
N}\\) bits of entropy, or 107 bits for 10 words. To guarantee more than 128
bits of entropy, now your password needs to contain 13 words. And you’re
still stuck using all the words you rolled, which limits how memorable your
password will be.

# Reordering Diceware with discards

I've started generating passwords in the following way:

First, roll 15 Diceware words. Then, choose your favorite 13 of those 15
words, and dicard the other 2. Put those 13 words into any order you want,
with punctuation separating them. This password can be very memorable,
because you had a lot of options for just how it should be put together. And
while the precise entropy is difficult to calculate, I believe it is at least
127.75 bits no matter how you choose the discards and ordering. For more
details about how to compute this lower bound for different password sizes,
check out Marcello Herreshoff's solution
[here](https://www.dropbox.com/s/v3wkoxslziadsc9/Ben_Weinstein_Raun_Password_Puzzle.pdf).

In addition to being strong, I've found that password generated this way are
quite memorable, compared to the Diceware method.
