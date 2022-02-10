---
layout: post
title: Port Knocking Better
date: May 16, 2021
location: San Francisco
---

I am not a security expert; I am just some guy. The usual caveats apply. 

Generally, it is a good idea to have fewer ports open on your server. When
you have ports open, you leak information about what services are running on
your server, and any misconfigured or vulnerable programs listening on those
ports can become targets.

Normally, a server must have open ports in order to do its job, at least when
you don’t know in advance which addresses it needs to serve. Port knocking is
a technique that allows you to have zero open ports on a server, while still
allowing connections from trusted clients.

# Port Knocking

In the simplest case, port knocking does what it sounds like: You disallow
all connections to all ports on your server, using your favorite firewall.
Then, you configure a simple daemon to watch for a particular sequence of
“knocks”: packets sent to closed ports on the server. When it sees the
appropriate sequence of knocks from some IP address, it tells your firewall
to (temporarily) allow connections from that address, on whatever port your
service is listening on (typically port 22, for ssh). This is like if your
speakeasy had a “secret knock” that must be performed before the bouncer
opens the door. Trusted clients know the secret knock, and so when connecting
to your server they use the knock sequence before attempting to connect.

# Avoiding Replays

As with real-life secret knocks, though, this technique is susceptible to replay attacks: if someone is able to hear the secret knock, they can repeat it easily. A person snooping on your traffic may be able to see that you sent a suspicious sequence of packets before successfully connecting, and then use the same sequence themselves.

Some knocking daemons, such as knockd, can mitigate this with a feature that lets you use “one time sequences”: A list of sequences that must be used in the appropriate order, and are then discarded. This works well when only one client needs to connect to the server: That client can keep track of the same list of knock sequences, and discard ones that it has used.

If multiple clients need to connect to the server, each client can get its own list.

But a problem with this approach is that one must generate sequence lists long enough to ensure that the client will be able to connect as many times as they wish. In principle this may not be too difficult; if you plan to connect fifty times a day for a hundred years, this amounts to less than 100 MiB of configuration. In practice I’m not entirely sure how knockd would deal with such a large list.

# Using TOTP

An alternative would be to use a scheme like the TOTP system you (hopefully)
use for two-factor authentication on your phone. In this scheme, the server
and clients use the current time to agree on a knock sequence. The server
gets a secret that’s shared with the client, and whenever the server sees a
knock sequence corresponding to the current OTP value, it opens the port (and
discards that value).

There are at least two implementations of this idea: [one by Akshay Shah and
Swapnil
Kumbhar](https://medium.com/@moses.livingstone.tech/port-knocking-a1a1d4321877),
and [another by Javier Junquera Sánchez](https://github.com/junquera/c-lock).
Neither of these solutions looks very polished, but they exist as
proofs-of-concept.

I haven’t looked hard at the code for either of these implementations, so I
can’t recommend them. There are various pitfalls involved here; the most
important is that the TOTP-generated sequence must be discarded after use, to
avoid fast replay attacks. And one may want to use different TOTP keys for
each client or user (to ensure that multiple clients aren’t racing for the
same code if they need to connect at similar times). I suspect that the above
implementations don’t deal nicely with at least one of these issues, though
again I haven’t looked at them in detail.

Shah and Kumbhar’s solution above uses knockd’s one time sequences feature,
but is forced to restart knockd to reload its configuration whenever the keys
change. Ideally it would be great if knockd incorporated a TOTP-based
configuration option, or had some other method of avoiding replays than long
lists of knock sequences.
