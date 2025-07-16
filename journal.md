# AI Vision System

![image](https://i.ibb.co/mrkwFywr/image.png)

![image](https://i.ibb.co/pvpN1QHM/image.png)

Total Time Spent - 36 Hours

## The Premise

I'll be designing a compact product, that'll be able to describe a scene presented to the camera, giving a description to aid a person who is visually impaired.

## Criteria for Success
- Safe to Use
	- Doesn't get hot in the users hands
	- Isn't sharp
	- Is able to be easily carried around
	- Is durable, and able to take some damage without posing a safety risk due to sharp edges or burs that may appear.
- Convenient 
	- The user actually wants to use it
		- Fast load times (under 5 seconds from button press to an accurate and detailed description)
	- Long lasting power solution
- Accesible
	- Easy to press button
	- Physical feedback to the user
	- Doesn't require cellular connectivity.

## Day 1 - Definition

So.. to start off, the main controller. My reaserch indicates that I essentially have 3 main options:
- Raspberry Pi CM5
- Orange Pi CM5
- Radxa CM5

I'm ultimately very fond of the compute module as a form factor, while packing in an insane amount of power.

After comparing the 3, the RPi version was quickly eliminated. It simply wouldn't be able to provide the required processing time, making the user experience slow and buggy. 

When choosing between the Radxa and Orange Pi, I ultimately did some research on the community available support, as well as availability. This yielded the Radxa to be the most suitable solution. Based on how things go with the budget, at the end, I'll either choose between the 8GB or 16GB RAM versions. This gives a bit of wiggle room in terms of design.

Currently, my main focus will be on the PCB and Case, working on the software once that is done.

The case will be made from 2 pieces of billet aluminium, serving as a heatsink, to allow for optimal operation. More on this to come.

![Radxa CM5](https://radxa.com/cm/cm5/banner_cm5.webp)

*Radxa CM5 module*

### Time Spent 3 Hours (10/07/25)

## Day 2 - Starting on the Schematic

Today, I started off with the schematic. I'll be using just a regular USB-C port to provide both power, and allow for data interaction with the finished product.

![image](https://i.ibb.co/S4GwtbDm/image.png)

As is required, there will be a speaker which is able to convert the text to an audio output. I was largely able to base this schematic off the Adafruit example breakout board. Yet, I'm still investigating how the I2S works with the Radxa module.

![image](https://i.ibb.co/zhfdCtGd/image.png)

And the camera... this took a while. It took ages to find the correct cable, and connector to use, and I eventually settled on this. Radxa's documentation wasn't too clear, so I've reached out to them via email, and hopefully I'll hear back from them tomorrow.

![image](https://i.ibb.co/rXjFRL0/image.png)

In the mean time, I created the motor driver circuit, using a simple MOSFET to drive the small vibration motor. This was luckily quite a bit.. simpler.

![image](https://i.ibb.co/XkWpNxHt/image.png) 
 
![image](https://i.ibb.co/Q1YQY3V/image.png)

I'm pleased with how things are going so far, and I've set the goal to finish this within the next 5 days, to ensure everything can be built in time for the end of Highway!

### Time Spent 6 Hours (11/07/25)

## Day 3 - Schematic 2

I heard back from Radxa, and they encouraged me to use this connector, a 15-pin one to align better with their IO board, offering greater support. 

![image](https://i.ibb.co/pvT0BLYs/image.png) 

![image](https://i.ibb.co/spHf5nb6/image.png)

This is how far I got with the schematic, and have everything mapped out. I just need to add in the passive components (resistors and capacitors) tomorrow, as well as the reset to the GPIO.

I also looked into additional sensors I'd need to add to the device, and how I could fully harness the power of the CM5.

To aid with this, I printed out all of schematics from the IO board, and went through annotating what else I could add. I also was confirming the placement of USB-C data lines into the CM5, as well as how I'll be placing other signals such as I2S and I2C into the correct place.. amoung the 300 available.

I also spent time fixing up the I2S, and GPIO pins for the camera going into the CM5 module.

![image](https://i.ibb.co/Bxm5cbB/image.png)

I also revised the power for the camera connector. As advised by Radxa, I added a Ferrite bead to smooth out the voltage supply frequencies. I also corrected the i2C pullup resistors.
 ![image](https://i.ibb.co/Kxdd132C/image.png)

I also added the passive components for the WS2812B Ring that will go around the camera. This will be connected through pin headers to provide an almost "3D" feel to the PCB. To keep costs low, I'm trying to keep all passive components on the main PCB, so I could hand assemble the ring board.

![image](https://i.ibb.co/0RPz7Cdg/image.png)

I'm pleased with how the schematic is going, and will do a final review tomorrow morning, before then moving onto the routing of the board.

### Time Spent 7 Hours (12-13/07/25)

## Day 3 - Starting the Layout

![image](https://i.ibb.co/8ZBnFkF/image.png)

I finished the schematic, other than fully connecting the CM5 module to ground.

![image](https://i.ibb.co/7xQfdWM8/image.png)

My PCB is going to follow the outline of the CM5 board pretty much 1:1. The case will then be expanded to allow for space inside for thing such as speaker and motor wires.

![](https://i.ibb.co/kgnwWDZs/image.png)

One problem that I encountered was the interference between where I want to put the cable for the camera, and the header pins for the WS2812B Halo.

![image](https://i.ibb.co/MknFqDr7/image.png)

Changing connector allows for vertical insertion of the cable, thus solving this problem.

At this point [insert image], I'm pretty happy with the routing. I'm now going to give the WS2812B Halo PCB a go.

Firstly, I had to expand the carrier board. This is unproblematic in a general form factor sense though. The mounting holes will remain the same, to match up with the CM5 module, which then with a small spacer, will be able to mechanically clamp the whole assembly down, ensuring reliability.

It had to be expanded due to the fact the 32mm rectangle camera had to fit inside the ring. Thus, I made the ID 16.5 so the camera could somewhat fit through.. this would make assembly much easier. 

![image](https://i.ibb.co/n51qCCz/image.png)

I did a simple schematic for this, only needing one component as it's then patterned.

![image](https://i.ibb.co/G3xxc8Yb/image.png)

I patternted 10 LEDs per ring, and then used the top layer for the DIN and GND signal.

![image](https://i.ibb.co/STnVztN/image.png)

I then use the bottom for the 5V line, as well as some ground jumps.

![image](https://i.ibb.co/x8qt1wyJ/image.png)

Overall coming out to be like this, with each LED having it's own capacitor.

![image](https://i.ibb.co/Lz248hgp/image.png)

I also added solder pads incase anything went too wrong.. *oh what foreshadowing this was*

![image](https://i.ibb.co/GQHWDxnQ/image.png)

This is then what it looks like assembled onto the board.

![image](https://i.ibb.co/h18G4Jrb/image.png)

and.. yeah, something did go wrong. so, I did the dimensions wrong previously, and the camera wouldn't have even fit through. The camera will be secured onto the top casing using M2 bolts into tapped holes, then this module needs to "slot" over the top of that. Below are the dimensions required, only allowing me to support the PCB on one side, with the USB-C being a big obstruction.

To counter this, I'm going to be bolting the LED ring onto the top casing, just to prevent any misalignment. It'll then be soldered onto the carrier board.

![image](https://i.ibb.co/s9FMhx4s/image.png)

So I made the simple transition to the solder pads on the board. Hopefully this will reduce the chance for potential errors!

![image](https://i.ibb.co/1VPMjNM/image.png)

The board kinda looks empty now though, which is sad.

![image](https://i.ibb.co/BV0H2SWW/image.png)

Here is where the final layout came to. I'll do all the routing tomorrow, then hopefully move onto the case. I'm still a bit undecided on how to make the board feel less empty.. but I'll see.

### Time Spent - 6 Hours (14/07/25)

## Day 4 - Routing

I started off with a general outline for what the routing would need to be.. but forgot to take screenshots as I was going..

All the USB-C and Data are routed differentially.

![image](https://i.ibb.co/FkP7Rwkz/image.png)

Once I finished the routing, I was pretty happy with how it looked, so I moved onto doing the button attachment. I thought of creating a slot in the main PCB, that then a seperate one with buttons on it can be soldered to. 

![image](https://i.ibb.co/1t7XG9bh/image.png)

The overall footprint was slightly expanded to allow the slot, which is the integrated with fillets, and dog-boned corners to allow for the manufacturing of the slot.

![image](https://i.ibb.co/LDVyq5PM/image.png)

The board is then both mechanically and electrically connected through the pads on the back, which are soldered onto the main board. There are extra to provide a stronger connection.

![image](https://i.ibb.co/hRBxdVz1/image.png)

3 buttons are then placed ontop for stability. It does not matter which are pressed, they all perform the same function.

![image](https://i.ibb.co/9m9R9Trc/image.png)

![image](https://i.ibb.co/qYg0TrBB/image.png)

In the case, there will be a larger button encasing all the black plastic parts. Here are some renders of a pretty finished PCB.

![image](https://i.ibb.co/93NqBw0w/image.png)

I put that PCB into the CAD, and unfortunately it was looking a bit too small for my needs, as I want it to be like 80mm in total. I also need the buttons in the centre. To fix this, I will slightly extend the board outline on the side opposite the USB-C.

![image](https://i.ibb.co/3mMh4J5g/image.png)

Unfortunately, the USB-C will now not fit, so I'll make it so that the buttons are biased towards one side, to the PCB doesn't actually need to be in the centre.

Unfortunately, the USB-C also didn't stick out far enough, but this was a pretty simple fix.

With the housing, it'll be machined from 6061 Aluminium, then anodised, but keeping the silver colour.

I offset the camera from the middle to just add a bit more visual interest to it, and tbh it just looked SUPER strange having it in the middle.

![image](https://i.ibb.co/HTgLdCpY/image.png)

On the rear side, there is a small heatsink on the outside, which will be nicely filleted and chamfered to both create a tactile feature, but also increase the surface area, allowing for heat to dissipate in a more efficient manner.

![image](https://i.ibb.co/QvGBdDkp/image.png)

At this point, the thickness is 19mm in total, and I think that's a really good thing, bringing down the form factor.

![image](https://i.ibb.co/9JHyzcF/image.png)

This unfortunately bought the issue of the camera not fitting... no matter what.

![image](https://i.ibb.co/9JHyzcF/image.png)

To fix this, I had to add roughly 9mm to the top of the housing, which increased the footprint, but hey.. at least the camera can fit now.

![image](https://i.ibb.co/JwBH50DN/image.png)

At the front, there is also the cutouts for the LED ring. I ended up changing this from the full ring, to just 2 segments to allow for a bit more structural integrity in the front.

This also pretty well showcases the button, unfortunately due to the current method of mounting to the PCB, it's unable to be in the centre. Tomorrow, I'll decide if I want it in the centre, and then how this could be achieved. Now that the device has become thicker, it's probably also a bit too thin, so I'll have to adjust that.

I'm pretty happy with how things are going so far, so tomorrow it'll just be finalising everything and hopefully shipping this device!!

### Time Spent - 8 Hours (15/07/25)

## Day 5 - Final Touches

![image](https://i.ibb.co/9kM8rc2J/image.png)

I started off by remaking the WS2812B ring on the front to fit my requirements, and fit in the opening.

![image](https://i.ibb.co/chWSRYNp/image.png)

I then made this polycarb diffuser, which I will have CNC machined, and then beadblasted to create a matte look.

![image](https://i.ibb.co/TBbS9XVM/image.png)

I then finished up by softening the back of the heatsink with fillets and chamfers.

Here are some final photos

![image](https://i.ibb.co/B2mbRC2c/image.png)

![image](https://i.ibb.co/KckRSQf0/image.png)

![image](https://i.ibb.co/bSR7XMq/image.png)

I'm very pleased with how the housing turned out.

I'll now be getting together everything, and shipping this project!!

### Time Spent - 6 Hours (16/07/25)
