---
layout: post
title: The window manager I want to use
date: October 18, 2017
location: San Francisco
---

I spend some time thinking about my workflow - what's good about
it, and what could be better. One of the things I've been thinking the
most about recently is window management. On my laptop I use
OS X, which has a window management paradigm that is fairly
familiar to people who have used a computer in the last few
decades. At work, I use i3, which is my favorite tiling
window manager.

## The problem with my current workflow

I like the i3 way of doing things for the most part, but I realized
that I spend a lot of time thinking in trees of heterogeneous windows.

As an example, on my worst days, I might have 6 i3 desktops actively
being used. On most of these desktops, I'll have a set of terminal windows.
I rarely use the terminal emulator's tab system, but I do almost always use
tmux. So I have a set of tmux tabs, inside of which are sets of panes.
Several of these windows will contain vim sessions. The vim sessions
have their own sets of tabs, and each of these tabs can contain multiple
windows.

So that's, like, a tree of maximum depth 6?

I'm bad at holding these trees in my head. I'm a lot better at holding 2d
spaces in my head.

## The Ideal Window Management System

If I wrote a window management system, it would have the following
properties:

* First of all, applications should mostly not do window management on
    their own.
    - They _should_, however, offer hooks to a window manager that allow
        the window manager to understand the semantics of their subwindows
    - Also, the window manager should be programmable, so that
        applications' subwindows can be given behavior by the user
        that matches the user's preferences, or they can be given
        behavior by the application developer (but these behaviors should
        not be hard-coded into the applications)
    - The window manager should be very flexible, ideally allowing for
        almost any tabbing or windowing systems in use today.
* Windows should be easy to move around in a resizable grid, with multiple
    virtual desktops.
* Each virtual desktop should be infinitely scrollable and easy to
    reposition by panning, or by zooming in and out, or by pressing
    navigation hotkeys.
