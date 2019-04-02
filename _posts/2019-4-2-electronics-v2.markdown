---
title: "Robot Arm V2: Electronics"
layout: post
date: 2019-04-02 12:00
tag:
- project
- robotics
- electrical
image:
headerImage: false
projects: false
hidden: true
description: "Work in progress of electronics for my robot arm"
category: blog
author: lukemetz
externalLink: false
---
---

Things have been busy, but I am trying to make more time for this project! This post is an update on some of the electronics and software for the Arm.

In terms of electronics, the previous design consisted of one base microcontroller that controlled everything with wires directly going to each motor. This was not scalable, not modular, and led to too many wires everywhere. Additionally, given the new slip ring, I did not have enough high current channels to make this approach possible. As such, I opted to be more distributed. I still have one base controller, connected to a PC for commands, but this controller is connected to a I2C bus. I2C is a simple, synchronous, master slave protocol that comes built in to many sensors and microcontrollers. For each axis, I have another microcontroller that converts the incoming commands to drive motors as well as potentially manages and sends back encoder data. Each board is daisy chained together with an 8 channel connector, with 2 channels for I2C, each with 2x for +12V, +5V, and GND.

<div class="side-by-side">
<div class="toleft">
<a href="/assets/images/blog6/assemb.jpg"><img src="/assets/images/blog6/assemb.jpg"></a>
</div>
<div class="toright" style="margin-top: 50px;">
<a href="/assets/images/blog6/many.jpg"><img src="/assets/images/blog6/many.jpg"></a>
</div>
<figcaption class="caption">Left: Single assembled custom PCB. Right:
Boards connected to motor controllers.
</figcaption>
</div>


I realized early in the last iteration that [breadboard](https://en.wikipedia.org/wiki/Breadboard) based electronics were not going to cut it.
Too many wires, and too hard to debug if something came loose.
That, and I am to lazy to cut wires to the correct lengths.
Perfboards are better. I tried to work with these, but concluded that soldering and working with them was time consuming and not very fun.
After building one board, I gave up and decided to dive into the world of custom PCB! I learned, and made schematics in [Eagle](https://www.autodesk.com/products/eagle/overview), and sent them to [oshpark](https://oshpark.com/) for fabrication. Turnaround time was < 1 week which is amazing -- would highly recommend this process! The circuits themselves are simple -- really just an Arduino shield, some connectors, a few resistors, and some LED for debugging. For simplicity, I chose not to place the circuit for the motor driver, nor the Arduino on my boards. I didn’t want to source components, am not equipped to do the required volume of surface mount soldering, and am not all that confident with so much electrical engineering. As a result, the full electronics are a bit messy, requiring many connections between the motor controller and the Arduino board. Next iteration, I plan on reconsidering this, as I spent the majority of the time making connectors.


<div class="side-by-side">
<div class="toleft">
<a href="/assets/images/blog6/schm.png"><img src="/assets/images/blog6/schm.png"></a>
</div>
<div class="toright">
<a href="/assets/images/blog6/layout.png"><img src="/assets/images/blog6/layout.png"></a>
</div>
<figcaption class="caption">Schematic (left) and layout (right) in Eagle.
</figcaption>
</div>


<div class="side-by-side">
<div class="toleft" style="margin-top: 10px;">
<a href="/assets/images/blog6/breadboard.jpg"><img src="/assets/images/blog6/breadboard.jpg"></a>
</div>
<div class="toright">
<a href="/assets/images/blog6/perf.jpg"><img src="/assets/images/blog6/perf.jpg"></a>
</div>
<figcaption class="caption">Left: Horrible mess of a breadboard. Right:
Annoying soldering required for perf boards.
</figcaption>
</div>


On the software side I am still sending inputs from an Xbox controller over sending SLIP to the master board. The master board now sends packets over I2C to each slave board. The slave boards listen for these, then set the appropriate pins to control the motor controller.

As of now, I have 2 axis more or less assembled with electronics. Current plans now are to 3D print and assemble a third axis to  figure out how to better control this thing!
