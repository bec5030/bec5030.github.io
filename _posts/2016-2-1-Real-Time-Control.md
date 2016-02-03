---
layout: post
title: Real Time Control Project
---

This post is about a real time control project with a ping pong ball in a tube.


<iframe src="https://player.vimeo.com/video/153728930" width="500" height="889" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>

Recently, I made a real time control project over the course of a couple of days, using an ultrasonic sensor, fan, pingpong ball, and tube. This is a video demonstrating a test of the project. 

The fan was used to control the location of the ping pong ball in the tube, while the ultrasonic sensor measured the distance form the top of the tube. I used a PSOC board as the brains of the project which allowed me to quickly and easily interface with the fan and the ultrasonic sensor. The PSOC board also communicated with my computer serially through a PUTTY connection. The program used a P.I.D. loop to control the height of the pingpong ball. I designed the program so the P, I, and D coefficients could be modified on the fly, to try and quickly find the most suitable coefficients. 

Initially, the ultrasonic sensor was not working when placed inside the tube. Several fixes were attempted. Ultimately muffling the output using thin paper produced the best readings.

I cannot provide code or schematics as this was a school project that may be reproduced by other students.
