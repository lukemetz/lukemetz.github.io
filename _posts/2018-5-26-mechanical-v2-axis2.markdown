---
title: "Robot Arm V2: Axes 2 and 3"
layout: post
date: 2018-05-26 12:00
tag:
- project
- robotics
- mechanical
image:
headerImage: false
projects: false
hidden: false
description: "Mechanical design of Axes 2 and 3 of my robot arm"
category: blog
author: lukemetz
externalLink: false
---
---

Axis 2, and to a lesser extent Axis 3 were by far the weakest of the [previous design](/project-log-matcha-making-robot-arm/). The 25kg-cm servos just didn’t cut it. It couldn’t move anything as more and more weight was added. To solve this problem, I decided to use the [highest torque (geared) motor I could find](https://www.servocity.com/12-rpm-hd-premium-planetary-gear-motor-w-encoder) -- up to 584 kg-cm, or a little more than 20x the previous power capability! One negative though is that these motors require a very different form factor, so a complete redesign was needed. This post describes two such of  iterations, the first for Axis 2, and then modifications of that for Axis 3.


![Final](/assets/images/blog5/motors.jpg)
<figcaption class="caption">Motor Upgrade! Left: the old 25kg-cm servo. Right: New 584kg-cm motor.
</figcaption>


## Axis 2
I decided to keep the same general design as the [first version](/project-log-matcha-making-robot-arm/) but with a bunch of modifications. First, as before, I replaced the spur gears with herringbone gears to mitigate backlash. Next, I replaced the M8 threaded rod with a 3D printed shaft with two beefy 6008 bearings on either end for support. Finally, the mount needed to be bigger to accommodate a much larger motor. The motor itself is mounted to this, bolted into the PLA. As in the first axis, I applied a clamping couple to the drive shaft so that the drive gear could be attached.

Another annoying aspect of the previous design was assembly. Instead of finicky bolts installed vertically through tight spaces, I decided make a slot  so the upper axis now fits around the lower, and I used a few bolts to secure it in place. Additionally, I am trying to use the same simple attachment mechanism across the arm to make things a little more modular.


![Final](/assets/images/blog5/axis1.jpg)
<figcaption class="caption">Full assembly of Axis 2.
</figcaption>

## Axis 3
In the first arm design, I simply printed out multiple copies of the the first axis and stacked them. I hoped to do the same thing here but decided instead to improve the design. In general, Axis 1 used waaaay too much plastic in terms of absolute size as well as in the thickness of components. In this Axis, I trimmed as much plastic as I could and thinned parts that didn’t need to be too strong. I also swapped the 6008 bearings for the lighter 6005 bearings. With this decreased size, the base piece needed to be two pieces so that I could get the motor installed correctly. While much smaller, it seems to hold up in terms of strength.


<div class="side-by-side">
<div class="toleft" style="margin-top: 60px;">
<img src="/assets/images/blog5/layout.jpg">
</div>
<div class="toright">
<img src="/assets/images/blog5/axis2.jpg">
</div>
<figcaption class="caption">Right: All components before assembly. Left: Fully assembled Axis 3.
</figcaption>
</div>


## Results
Not surprisingly, these motors are incredibly strong. While testing, I accidentally ran a motor too long, which resulted in a collision with plastic. Instead of stalling, as I would have expected, the motor kept  turning and broke the plastic! It’s good that the PLA is now probably the weakest component of this whole thing!


![Final](/assets/images/blog5/full.jpg)
<figcaption class="caption">Fully assembled arm with 3 axes so far.
</figcaption>

## Next up
For well being of the 3D printed parts, it’s clear I cannot keep running these motors by manually with wires connected to a power supply.. There needs to be some sort of auto stop. I have been busy scoping sensors and such and hope to have an update on that as well as the rest of the electronics some point soon.

Thanks for dropping by.  Your thoughts always welcome! 
