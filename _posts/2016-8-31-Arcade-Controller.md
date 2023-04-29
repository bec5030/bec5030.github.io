---
layout: post
title: Arcade Controller
---

This post is about an arcade controller I created from a microcontroller using C code. The controller runs on a bare metal STM32F4 and acts as a USB HID keyboard. 

![an image alt text]({{ site.baseurl }}/images/controller_top.jpg "arcade controller top view")
![an image alt text]({{ site.baseurl }}/images/controller_inside.jpg "arcade controller inside view")
![an image alt text]({{ site.baseurl }}/images/controller_microcontroller.jpg "arcade controller microcontroller")



<iframe src="https://player.vimeo.com/video/180992957" width="500" height="889" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>

A while back, I made a pair of arcade controllers from an STM discovery board (~$20) as can be seen in the pictures above. The microcontroller acted as a USB HID keyboard to a host computer and used microswitches for button presses on the controller. This allowed me to connect the controller over USB to any computer (or other device) to play games on an emulator as shown in the video. The button switches simply used GPIO inputs which were mapped to "keys" to send to the host computer. The joystick is simply four buttons, one for each direction. So far the buttons and joystick are housed in carboard boxes but I plan to make a real housing for them in the future. This was the first time I had ever soldered so it started off slow but by the end I picked up the pace. 

The most difficult part for creating this was setting up the STM USB software stack and USB HID profile. This took a lot of messing around with before it worked correctly. 

I also ran into a very interesting issue while developing this controller.  When powering the discovery board with one laptop, every time the board touched the floor it would sense the floor as a button push. This did not occur with the other laptop however. I eventually realized that one laptop's power supply had a ground prong, while the other one did not. The non-grounded power supply was causing the false button pushing issues. To overcome this
issue I set the microcontroller to use internal pull up resistors and never had a problem since.  


The code for this project can be found [here](https://github.com/BradleyConn/arcade_controller).
