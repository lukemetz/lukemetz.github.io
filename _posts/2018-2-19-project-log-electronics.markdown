---
title: "Robotic Arm Electronics and Firmware"
layout: post
date: 2018-02-19 12:00
tag:
- project
- robotics
- software
- electrical
image:
headerImage: false
projects: false
hidden: false
description: "Overview of electronics and firmware for my matcha making robot arm project."
category: blog
author: lukemetz
externalLink: false
---
---

This is the second post in the documentation of my attempt to build a robotic arm to make me tea. For the mechanical build, see the [first installment](/project-log-matcha-making-robot-arm/). As usual, this is a learning process, so if something seems wrong or could be done better, please let me know in the comments or feel free to tweet me!

With the mechanical pieces in a semi-functioning state, my next action was to figure out how to drive and control this contraption. In this post, I provide a high level overview of the electronics and sensors I used and briefly touch on the firmware and communication which enable technically simple, yet incredibly difficult manual control. Bellow you can see the arm struggling with the underpowered motors.

<iframe width="560" height="315" src="https://www.youtube.com/embed/tRS1kZs6feg" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
<figcaption class="caption">Arm being controlled via xbox 360 controller.</figcaption>


### Motors and Electronics:
For my main motors I acquired a few [inexpensive servos](https://www.amazon.com/gp/product/B01N0XZOZU/ref=oh_aui_search_detailpage?ie=UTF8&psc=1). I “hacked” these to convert them into being able to sustain continuous rotation  by taking each one apart, removing the mechanical stops, the potentiometer, and  all the control electronics. I wired the motor directly to the positive and negative ports of the connector, and left the signal wire disconnected.
In retrospect, and given that my current motors are a little underpowered, this was a poor choice (at least for the lower joints which need more power) and I will need to redesign to use a much more powerful motor :(.
Because I removed all the control boards, I still needed something to drive the motors in both directions at a variable speed. For this, I am using a few motor controllers based on the [L298N chip](https://www.amazon.com/gp/product/B06XR1YNH4/ref=oh_aui_search_detailpage?ie=UTF8&psc=1). These little boards are incredibly effective for the price ($1.23 dollars each from AliExpress).
I acquired 3 of them for the 5 motors  in my build thus far, with 1 drive output left free for the eventual gripper.

Finally, I needed some way to sense the world.
For a while I debated using a camera, but decided against it as it would require a lot more effort on the control side of things.
Instead, I opted for a bunch of “Absolute Orientation” sensors (the BNO055 chip with a breakout board made by [Adafruit](https://www.amazon.com/gp/product/B017PEIGIG/ref=oh_aui_search_detailpage?ie=UTF8&psc=1). I figured a few of these, with their ability to sense gravity, should be enough to make predictions about the state of the arm and thus allow me to control its behavior.
These are great and very modular as they are not tied to the motor in any way. Additionally, nothing is stopping me from using these as well as  a camera if I conclude that the latter is needed.
Because I don’t plan this far into the future, I 3D printed little sensor holders, and hot glued them to the main body of the arm. Additionally, wire routing is done in a similar way.

![Sensors](/assets/images/blog2/sensor3_2.jpg)
<figcaption class="caption"> 3D printed sensor holders.
</figcaption>

These sensor breakout boards communicate over I2C and, sadly, all share the same I2C address, which means that normally I can only use one at a time. To remedy this, I am using an [I2C multiplexer](https://www.amazon.com/gp/product/B015HJX33Y/ref=oh_aui_search_detailpage?ie=UTF8&psc=1) which allows me to select the chip I seek to read and write from.

![Wires](/assets/images/blog2/electronics_s.jpg)
<figcaption class="caption"> All electronics haphazardly scattered next to the arm.
</figcaption>


### Firmware:
Everything on the arm is controlled off of an old Arduino Diecimila. The board is programed to listen on the Serial/UART connection for commands sent from my PC, as well as read from the sensors and send data back to a host. This is a fairly low level connection, and thus still needs some protocol added. I figured a simple packet system would be straightforward and chose  [SLIP packets](https://en.wikipedia.org/wiki/Serial_Line_Internet_Protocol) for their simplicity and seemingly wide library support . Both the host and the Arduino read these packets and use them to communicate with each other.

### PC Control:
At present, the host/PC control is in Python script that grabs controls from the user input (in my case an XBox controller), packages it in a SLIP packet, and sends it over serial/UART to the Arduino. While performing this function, it periodically reads the sensor values. Additionally, I log out both controls and sensor readings to a [ndjson](http://ndjson.org/). This can be used for visualization and, as I will detail in a later post,  to train the control models!


Operation of the arm from the Xbox 360 controller is surprisingly hard as the controls do not have any notion of gravity correction. For example, watch in this gif how as the arm extends over the center of mass, it comes crashing down as the motor is no longer fighting against gravity, but assisting it. Still, I can actually move the arm around now which is progress!


![Wires](/assets/images/blog2/plt.png){: class="smaller-image" }
<figcaption class="caption"> Initial plot of some data while controlling
with an xbox. Only the first axis shown.
</figcaption>


### Next up:
The foregoing is seemingly enough to make the arm operate but there is no way I can perform any sort of delicate actions. Next up I plan on trying to remedy this with machine learning!
