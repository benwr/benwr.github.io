---
layout: post
title: "Projects"
date: 2013-10-25 21:22:37
---

This is a list of some projects I've worked on, including some stuff for class, some
for extracurricular activities, and some for no reason other than that I was bored.
This is not an exhaustive list. You may want to check out
[my github profile](https://github.com/benwr) as well, which has some of my
more self-documenting projects (that is, those that are mostly code).

---
## Latchburg ##
#### May 2014 ####

[Hacksburg](http://hacksburg.org) needed an access system, and cheap. We had a Raspberry Pi
and some donated equipment including an electronic strike plate. With a couple quick trips to
Radio Shack, the repurposing of a 5V power supply from a car cigarette lighter, and some Python,
I built [this](http://hackaday.io/project/753-Latchburg) fun little doohicky.

![the internals of latchburg](https://static.hackaday.io/images/resize/600x600/4935351396980488356.jpg)

We were restricted by the Corporate Research Center in that the access system had to provide
access based on the magstripe cards used by the university. This is bad because it guarantees that
at least some members' cards will be encoded using only their university ID number (plus the university's
unique identifier and a single digit that increments when they're issued a new card). This is a pretty
small space to brute force, and it's relatively easy for an attacker to find this information anyway. I'm thinking
about making a simple, optional two-factor system that texts a user when they swipe their card and asks
for an affirmative response. This would at least allow members to ensure that it won't be _their_ card info
that lets someone in.

---

## Application of Neural Networks to Prediction of Normalized Difference Vegetation Index ##
#### November 2013 ####

Basically, NASA and UW produced [this data set](http://jisao.washington.edu/datasets/ndvi/)
of Normalized Difference Vegetation Index (NDVI). It indicates how much vegetation is
at a particular spot on the earth's surface. The data comes from NOAA's AVHRR, a satellite imager
that measures reflected light on the earth's surface at particular wavelengths.

Sean Thweatt and I were in [ECE 4984](https://filebox.ece.vt.edu/~f13ece4984ece5984/),
Introduction to Machine Learning and Perception, at Virginia Tech in Fall 2014.
For the final project, we made
[this poster](https://drive.google.com/file/d/0B6QINlqDWlIAVndqclpvQThfWXM/edit?usp=sharing),
which won us the best undergraduate project prize. The idea was pretty basic: Use a simple
neural network trained on [temperature and precipitation data](http://jisao.washington.edu/datasets/ud/) from
the University of Delaware, to see if we could significantly beat climatology for predicting NDVI.
We did a fair job, but I'd like to see if I could do better given more time.

---

## Boost Converter ##
#### May 2013 ####

A simple project Chris Buck and I made that won the 2013 Virginia Tech HKN ANDY Board Competition:
a boost converter. The project was composed of two main parts: One is just a circuit that generates
PWM using a potentiometer and a 555 timer, and the other is the actual boost converter.

![PWM Generator Schematic](https://docs.google.com/drawings/d/1Fh41O1oUzOgrEiZd225uh5cQR32ZfJQKzRGNQE-JxJ4/pub?w=570&h=327)

Normally, the duty cycle of 555 timers operating in astable mode is dependent on two resistances (which also affect the frequency). We configured ours using a single potentiometer and two diodes, to ensure that the duty cycle can be modified without disturbing the frequency.

![Boost Converter Schematic](https://docs.google.com/drawings/d/1s7kowwebd7P6nQV2or-gujy7WADpVj-z4Soys9B2hJg/pub?w=531&h=223)

The operation of a boost converter is based on an inductor’s opposition to changes in current: When the MOSFET turns on, current slowly begins increasing through the inductor (following the path of least resistance, through the transistor). As the MOSFET remains on, more and more current flows through the inductor. When the transistor turns off, the current through the inductor initially remains at the same level, but must flow through the diode and the load instead of the transistor. This produces the effect of a higher output voltage across the load. Since this increased output is only present when the transistor is off, a reservoir capacitor is used to keep the output voltage relatively stable.

Our circuit demonstration drove 7 LEDs in series, each with an “on” voltage of ~1.8V.  This required a source voltage of ~12.6V (7 x 1.8V). However, we powered our circuit using only the 9V-regulated source on the A&D board.

By adjusting the potentiometer, it was easy to see the dimming effect.

---

## Knitted Cellular Automata Hats ##
#### February - September 2012 ####

I have knit hats based on
[elementary cellular automata](http://mathworld.wolfram.com/ElementaryCellularAutomaton.html),
and Rule 110 in particular. I do this because I was learning to knit at the same time as I
was learning what cellular automata were, and the ideas seemed to go together. I've started
a Rule 30 hat a couple of times but always discarded it fifteen rows in or so; for some reason the
rule is harder for me to internalize. Anyway, here's a photo:

![Me wearing a rule 110 hat](https://googledrive.com/host/0B6QINlqDWlIAVzNNcVhlc0JfeWM/546470_10150859021162184_1108769176_n.jpg)
