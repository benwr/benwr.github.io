---
layout: post
title: Entropy isn't sufficient to measure password strength.
date: January 16, 2022
location: San Francisco
---

If you know a lot about passwords, you probably know that it's good to choose a password
from a distribution \\(W\\) with a lot of "entropy". The (Shannon) entropy of a distribution is defined as:

$$H(W) = \sum_w\mathrm{P}(w) \log\frac{1}{\mathrm{P}(w)}$$

This definition is an answer to the question "how much information is encoded in a chosen password, on average?" This is also the approximate number of *bits* we need to specify *which* password we picked. An adversary would need to try at least \\(2^{H(W) - 2} + 1\\) passwords in order to guess yours, on average.[^1]

[^1]: See [Massey's (very short) "Guessing and Entropy"](http://www.isiweb.ee.ethz.ch/archive/massey_pub/pdf/BI633.pdf) for a discussion of this lower bound.]

This is typically how people think about choosing strong passwords, and it works well in the case where we're choosing among equally likely passwords. But it breaks horribly when we allow our distribution to be non-uniform. Because choosing good passwords is about memorableness as well as sheer strength, we might sometimes want to use complicated password selection schemes that don't necessarily give uniformly distributed selections, and Shannon entropy can really screw up here.

## A comically bad password selection scheme

Consider the following password selection algorithm:

1. Roll a 20-sided die.
2. If the die comes up 20, choose a random password from \\(n\\) possibilities.
3. Otherwise, choose the password `password`.

Of course, this is a *terrible* password selection strategy. 19 times out of 20, your password will be the *very first one the attacker tries*, if they know your strategy. But the entropy here doesn't reflect that - for example, if we pick a random 1000-character lowercase password when we get a 20, this has an overall entropy of about 235 bits. Entropy tells us that we have an extremely strong password, since *on average* it will take a long time to crack the password. But of course *in the typical case*, it will take no time at all.

Clearly something is wrong here. How can we fix it?

## Min-entropy

The first thing to notice is that, as we've already implied, we're engaged in a game of strategy with any would-be password crackers. We pick some strategy for choosing passwords, and then our opponent picks a strategy for guessing them. Our opponent's best response is going to be to try the most likely passwords first.

So how should we really measure our password selection strategies? One way would be to use the information content of the _most likely_ password, instead of the average information content:

$$H_{min}(W) = \min_{w \in W}\log\frac{1}{\mathrm{P}(w)}$$

This is called the min-entropy, and it's nice for several reasons, not least because when \\(W\\) *is* uniform, \\(H_{min}(W) = H(W)\\).

An issue with this method, though, is that it doesn't let us distinguish the d20 scheme above with 1000-character passwords on a high roll, from a similar scheme with only 3-character passwords on a high roll. Even though the scheme is bad in both cases, it's still *better* in the former case than the latter, if only by a little.

But I think the most important thing about the min-entropy is that it gives us a *conservative* estimate that we can use to compare password selection schemes, while Shannon entropy gives something more like a central estimate. If the min-entropy is \\(b\\) bits, we can feel really confident that it will take \\(2^{b - 1}\\) guesses to crack our typical passwords, even if the distribution isn't uniform. If one scheme's min-entropy is better than another's Shannon entropy, we can feel secure that the first scheme is better.

*Thanks to Adam Scherlis for pointing out the issue with Shannon entropy, Katja Grace for discussions about the problem, and Thomas Sepulchre for pointing out a major flaw in the original post.*
