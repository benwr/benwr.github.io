---
layout: post
title: Some property testing tricks
date: September 1, 2020
location: San Francisco
---

If I could only give one piece of advice to every programmer working today,
it would be "No matter what language you're using, no matter what you're
building, use [property-based
testing](https://increment.com/testing/in-praise-of-property-based-testing/)
when things need to be correct."

If you’re unfamiliar, I’d recommend reading the link above. The gist, though,
is that when you test a function, instead of coming up with examples to check
with unit tests, you come up with properties of the function that should be
true for every input, and then a library generates example inputs (randomly
and/or intelligently) that check whether those properties do in fact hold.

In the ideal world of program correctness, software would be written in
languages with powerful type systems, à la
[CPDT](http://adam.chlipala.net/cpdt/), and you could express your program’s
correctness at the type level. But, in my opinion, this approach isn’t yet
ready for large software projects that need to get things done quickly: It
takes too much overhead to get it really right, and it significantly slows
down the process of changing your code.

Property-based testing, on the other hand, is almost no harder than unit
testing. It’s also much more flexible, and much more likely to catch bugs
that you wouldn’t have been able to predict. And, in my experience, it even
helps to steer you in the direction of “robust tests”, rather than tests that
will break as soon as your code changes.

I’ve recently been employing some simple but general-purpose property testing
tricks, that might prove useful the next time you want to write some bug-free
code.

# My side project

My side project is a note-taking and flashcard app, inspired by
[Roam](http://roamresearch.com/). The backend of the app uses a
[CRDT](https://en.wikipedia.org/wiki/Conflict-free_replicated_data_type) I’m
[designing](https://docs.google.com/document/d/1p1K3sxgKGYMEBH72r-lnP9GnBm5N15h77C81W15kPiE/edit#heading=h.rdvadwnlt9u5),
that (I think) solves [an open
problem](https://martin.kleppmann.com/papers/list-move-papoc20.pdf) with
text-editing CRDTs. This CRDT absolutely must have certain properties to
ensure that two people editing the same document will always be able to
reconcile their changes. I have a sketch of a proof in my head that these
properties are preserved, but it’s crucial that the implementation (as well
as the conceptual objects) actually do preserve those properties.

Furthermore, there are some properties that I believe are true of my data
structure, but that I haven’t even fully sketched a proof for, like “Do the
user’s local actions always result in the intended state?” and “When multiple
users are editing a document concurrently, is it impossible for them to end
up with their edits interleaved in an unfortunate way?” Property testing
gives me a way to be confident that these are true before spending hours
trying to come up with a formal proof.

I’m writing the project in Rust, using [burntsushi’s Quickcheck
port](https://github.com/BurntSushi/quickcheck) as the testing framework.

# Warping the input space

Property testing should give you confidence in your code, but that
confidence should be proportional to “how much of the input space your tests
have explored.” For very simple inputs, like a function that takes three
booleans, Quickcheck can exhaust the entire input space easily. For more
complicated inputs, like a function that renders some unicode text, your
tests are much less likely to hit the rare edge cases, unless you are very
strategic about how you generate your random examples.

One trick here is to use smaller types when possible. For example, say you
have a function that searches for cycles in a directed graph, say a `Map<A,
Vec<A>>`. Normally your graphs are indexed by strings. If you generate a
graph by picking out random elements of your `Map<String, Vec<String>>`,
you’ll spend most of your randomness on generating uninteresting graphs with
lots of nodes pointing at nothing.

Instead, say you generate `Map<u8, Vec<u8>>`s. This is much more likely to
give you interesting graph structures, since you’ll (at least occasionally)
pick the same u8s at different places in your structure.

It might be even better to implement and generate elements of an even
smaller type: say u3s. Note the tradeoff here: with u3s, your graphs will
have at most 8 vertices (which limits the structures), but you’ll be
verifying your code on a much larger subset of those graphs. There are
certainly some bugs that only manifest on graphs with more than 8 vertices,
but I’d wager that they’re much rarer than bugs that manifest on small
graphs as well.

There are probably other tricks for warping the input space, to give you
better coverage of the “tricky” parts, but “use smaller types” is quite
useful on its own.

Another thing I’d really like to try in this general vicinity, but haven’t
yet, is to write a tool that analyzes how much / which parts of the input
space are being explored by your generators. (Just like the glorious code
coverage tools of old! /s)

# Generating objects via possible histories

The other trick I’ve been enjoying involves objects that are difficult to
generate, because the rules for which objects are “valid” are quite
complicated. In my side project, generated elements of the CRDT type should
be restricted to the elements that are actually possible to create through
some sequence of user actions (including merging two CRDT elements
together).

In cases like this, one option is to tell Quickcheck that invalid examples
should be `discard()`ed. But this results in doing a lot of extra work to
find valid examples, and in practice the library will give up after some
number of discards.

A more workable solution is to generate a possible history: Implement a
datatype to represent “possible states of the world”, and another to
represent “events that might happen”, and then generate sequences of events
to check that your property holds on the resulting world state. This lets
you avoid ever having to call `discard()`, at the cost of a bit of extra
code.

This trick is a little bit demanding: In order to be confident that you’re
exploring the input space successfully, you need to be sure that your event
datatype is really representing all of the things that can happen to your
world state. One way to be pretty confident is by having your event type
mirror your public API: For each operation that can be performed by an
end-user, that operation should be possible to generate as an event.

Another downside of this approach (making it a last-resort in my toolkit) is
that when you do find failures, your property testing library will (of
course) show you the history that generated those failures. And unless you
implement a helper that lets Quickcheck shrink your inputs (which lets it
find the simplest possible input that causes a failure), you’ll spend a lot
of time walking through the history to try to understand the problem. Other
property testing frameworks might be better at the shrinking aspect here.

# Other thoughts about property testing

As you can tell, I’m hugely enthusiastic about property testing. Some other
considerations that have occurred to me while working on this project:

* Speed is important! I started my project using [AltSysRq’s proptest
  library](https://github.com/altsysrq/proptest) rather than Quickcheck, but
  discovered that it was nearly 10x slower on my project. That means 10x
  fewer example inputs! Its shrinking algorithm is much more sophisticated
  than Quickcheck’s, but in my opinion this is definitely not worth the cost
  in missed examples.
* If your testing library is randomly generating examples, your confidence
  in your code grows with each test you run. I’ve considered setting up a
  beefy server somewhere just constantly running my test suite.
* Despite being more than 20 years old, Property-based testing still feels
  like a “new” technology to me: There are some really great libraries out
  there, but I really feel that the entire software industry should be
  adopting it, and I suspect that tooling for property-based testing
  libraries could be hugely improved.

I hope these little tricks are useful to you – may Moore’s Law faithfully
guide your PRNG!
