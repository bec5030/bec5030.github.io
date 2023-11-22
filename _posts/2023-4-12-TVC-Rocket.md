---
layout: post
title: Thrust Vector Controlled Rocket
categories: [Controller, Featured, Rocket]
featured-image: /images/tvc/tvcFam.jpg
---

This post is about a Thrust Vector Controlled (TVC) Rocket project that I am working on! This post was thrown together quickly to showcase some of the progress that has been made but lacks most of the details.

{:refdef: style="text-align: center;"}
![an image alt text]({{ site.baseurl }}/images/tvc/tvcDisplay.jpg "Rocket Picture"){: width="450" }
{:refdef}

### Thrust Vector Controlled Rocket Project:

This project is a work in progress but is roughly broken down into four parts.

- Flight computer design (complete)
- 3d modeling and part selection (mostly complete)
- Physics/control algorithm simulation (complete but waiting on updated rocket characterization)
- Flight software (peripheral drivers mostly written, main loop WIP)


### Enos Flight Computer

I designed a flight controller from scratch using KiCad and had it produced and assembled by JLCPCB. This was my first ever board design which actually worked first try!

![an image alt text]({{ site.baseurl }}/images/tvc/enosGlamourShot.jpg "The Flight Computer")

Enos is named after the first chimpanzee to reach orbit! He's depicted in our mascot logo, shocased here

{:refdef: style="text-align: center;"}
![an image alt text]({{ site.baseurl }}/images/tvc/enosMascot.jpg "Enos Mascot")
{:refdef}

The motivation for designing my own board even though there are a plethora out there was because they were all very expensive. The goal of this board was to create a compelling TVC flight computer for a cheaply as possible. This 2 layer, single sided board, came out to about 2 inches by 3.5 inches, and cost rought $15 each before shipping for a batch of 5 boards. In total, including shipping it was less than $100.
The full board is shown below

{:refdef: style="text-align: center;"}
![an image alt text]({{ site.baseurl }}/images/tvc/enosFront.jpg "front"){: width="450" }
{:refdef}

{:refdef: style="text-align: center;"}
![an image alt text]({{ site.baseurl }}/images/tvc/enosBack.jpg "back"){: width="450" }
{:refdef}


The schematic can be found [here](https://github.com/BradleyConn/bc_flight_computer/blob/main/Hardware/KiCad/projects/rp2040_v0/rp2040_v0/schematic_v0.pdf)

The schematic is well annotated. The first page, and heart of the flight computer, is shown below.
![an image alt text]({{ site.baseurl }}/images/tvc/schematic_v0_page1.jpg "Schematic")

The gerbers can be found [here](https://github.com/BradleyConn/bc_flight_computer/blob/main/Hardware/KiCad/projects/rp2040_v0/rp2040_v0/gerbers_v0.pdf) and [here](https://github.com/BradleyConn/bc_flight_computer/blob/main/Hardware/KiCad/projects/rp2040_v0/rp2040_v0/gerbers_v0_single_page.pdf)

And they look like this

{:refdef: style="text-align: center;"}
![an image alt text]({{ site.baseurl }}/images/tvc/enosGerbers.jpg "Gerbers")
{:refdef}

All of the components are outlined and labeled below.
![an image alt text]({{ site.baseurl }}/images/tvc/enosLabeled.jpg "Labeled")

The board typically requires headers to be soldered on. The complete board can be seen here.
{:refdef: style="text-align: center;"}
![an image alt text]({{ site.baseurl }}/images/tvc/enosFrontHeaders.jpg "The Flight Computer With Headers"){: width="450" }
{:refdef}



I figured out a neat little trick for this board. I wanted to maintain as much flexibility as I could, not knowing if the board had design flaws or not as it was my first board. So each of the peripheral components had breaks in the signals to completely disconnect or rewire. And to save space and also not have to solder extra through hole components I used zero Ohm resistors to bridge the signals. They can easily be removed and updated if needed. This also had the benefit of essentially creating an extra layer for the board as the signals rose over the board, and other signals could run underneath the resistor. And example is shown here

{:refdef: style="text-align: center;"}
![an image alt text]({{ site.baseurl }}/images/tvc/enosZeroOhm.jpg "Zero Ohm trick")
{:refdef}

### 3d modeling and part selection
All of the parts have been purchased and most of the 3d modeling is complete. I still need to make a launch stand to level out the rocket pre-flight, but I suspect that is the last piece needed. 

I have selected Estes E10 motors for intial flight tests as they had a decent optimization between duration, thrust, and price, optimizing slightly more for price as it is unknown how many test flights will be needed before things start running smoothly. After that Estes F motors should be compatible, and the longest duration that has a greater than 1 thrust to weight ration will be chosen to really put the control loop to the test.

I have done all my 3d modeling in OpenSCAD. The models should be available in the repo. This includes a nose cone, body tube, flight controller mount, parachute ejection mechanism, and more. I 3d modeled and printed the body tube instead of using cardboard tubes to save time. The 3d models have holes in them to save mass, but more mass savings will be had by a switch to carboard. The holes in the body tube will be covered by tape or paper to help with the aerodynamics. The body tubes can be seen here.

{:refdef: style="text-align: center;"}
![an image alt text]({{ site.baseurl }}/images/tvc/tvcNoseTube.jpg "Nosecone and Body Tube"){: width="250" }
{:refdef}

A fun family picture with the body tubes and Enos flight computer is below.

{:refdef: style="text-align: center;"}
![an image alt text]({{ site.baseurl }}/images/tvc/tvcFam.jpg "Family Picture"){: width="450" }
{:refdef}

One unique feature of this rocket is the parachute ejection is controlled by a servo instead of black powder. I wanted something that was not tedious to setup infinitely repeatable. So I designed a spring mechanism to pop the parachute. It is held by a pin which gets pulled with it's time to release the chute. It can be seen below. Note the pin has not yet been cut to length in these images.

{:refdef: style="text-align: center;"}
![an image alt text]({{ site.baseurl }}/images/tvc/servoEjection1.jpg "Servo Ejection 1"){: width="450" }
{:refdef}

{:refdef: style="text-align: center;"}
![an image alt text]({{ site.baseurl }}/images/tvc/servoEjection2.jpg "Servo Ejection 2"){: width="450" }
{:refdef}

In order to save time and support a creator I cherish, I bought the TVC mount 3d models and printed those.

### Simulation

The rocket TVC physics were modeled to enable a playground to test control algorithms. This software was written in python and should help find suitable control loop parameters. To start, a PID controller is used, with more advanced control algorithms planned. Below is an output from a simulation run while it was being developed.


{:refdef: style="text-align: center;"}
![an image alt text]({{ site.baseurl }}/images/tvc/simulation.jpg "Simulation")
{:refdef}

### Software

The software is still in progress, but most of the board has been validated and all of the drivers have been written except the pyro channels, and the reaction control wheel motor driver (optional).

That means there are drivers for the accelerometer and gyro, barometer, buzzer, leds, servos... etc.

<iframe width="424" height="754" src="https://www.youtube.com/embed/iuWRiD8zPx0" title="Enos Flight Computer Blinky!" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
