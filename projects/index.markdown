---
layout: post
title: "Projects"
date: 2013-10-25 21:22:37
---

This is a list of some projects I've worked on, including some stuff for class, some
for extracurricular activities, and some for no reason other than that I was bored.

---

## Application of Neural Networks to Prediction of Normalized Difference Vegetation Index ##

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

A simple project Chris Buck and I made for the Virginia Tech HKN ANDY Board Competition:
a boost converter. The project was composed of two main parts: One is just a circuit that generates
PWM using a potentiometer and a 555 timer, and the other is the actual boost converter.

![PWM Generator Schematic](https://docs.google.com/drawings/d/1Fh41O1oUzOgrEiZd225uh5cQR32ZfJQKzRGNQE-JxJ4/pub?w=570&h=327)

Normally, the duty cycle of 555 timers operating in astable mode is dependent on two resistances (which also affect the frequency). We configured ours using a single potentiometer and two diodes, to ensure that the duty cycle can be modified without disturbing the frequency.

![Boost Converter Schematic](https://docs.google.com/drawings/d/1s7kowwebd7P6nQV2or-gujy7WADpVj-z4Soys9B2hJg/pub?w=531&h=223)

The operation of a boost converter is based on an inductor’s opposition to changes in current: When the MOSFET turns on, current slowly begins increasing through the inductor (following the path of least resistance, through the transistor). As the MOSFET remains on, more and more current flows through the inductor. When the transistor turns off, the current through the inductor initially remains at the same level, but must flow through the diode and the load instead of the transistor. This produces the effect of a higher output voltage across the load. Since this increased output is only present when the transistor is off, a reservoir capacitor is used to keep the output voltage relatively stable.

Our circuit demonstration drove 7 LEDs in series, each with an “on” voltage of ~1.8V.  This required a source voltage of ~12.6V (7 x 1.8V). However, we powered our circuit using only the 9V-regulated source on the A&D board.

By adjusting the potentiometer, it was easy to see the dimming effect.
