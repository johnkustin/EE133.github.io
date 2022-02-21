# LAB 2 – Clock Generation with a Si5351

## Authors

Author : John Kustin  
Lab partner: Yifan Zhu

## Abstract
TODO
- Clocks are basically in ALMOST EVERY system you will work on
## Background

Previous iterations of Stanford University's Analog Communications Design Laboratory (EE133/233) had a lab on oscillators. In the past, they built ![Colpitts oscillators](https://en.wikipedia.org/wiki/Colpitts_oscillator). Times have changed and the current landscape of electronics is such that the number of times one will need to generate a clock is far greater than the number of times one would benefit from building a Colpitts oscillator. 

This lab is meant to introduce the emerging engineer to a *modern*, low-cost, and widely used clock generator -- the ![Si5351](https://cdn-shop.adafruit.com/datasheets/Si5351.pdf). This part has a low price point, reasonable performance, and successful history (it is used in the NanoVNA V2 that was used in Lab1!). The experience gained through this lab can be carried forward in a young engineer's career as they embark on projects that will most certainly include clock generation.[^1]

[^1]: This background is pulled from Steve Clark's ![Canvas Announcement](https://canvas.stanford.edu/courses/148940/discussion_topics/722850).

-  Si5351 breakout 



## Experimental Setup

The hardware used in this lab includes:
- ![Adafruit Si5351 breakout board](https://learn.adafruit.com/adafruit-si5351-clock-generator-breakout/downloads)
- ![ItsyBitsy M4 microcontroller](https://learn.adafruit.com/introducing-adafruit-itsybitsy-m4)
- 3x male edge-mount SMA adapters
- solderless breadboard
- oscilloscope and probe
- spectrum analyzer and probe

<p style="text-align:center;">
<figure>
<img src="images/IMG_7812.jpeg" alt="breadboard setup" style="width:75%">
<figcaption align="center">Fig. 1 - An Adafruit Si5351 breakoutboard with attached SMA adapters connected to an ItsyBitsy M4 microcontroller through a solderless breadboard. An oscilloscope probe is attached to the <code>clk0</code> port of the breakout board. </figcaption>
</figure>
</p>

## Measurements and Results

TODO

## Discussion

- The manufacturer claims that an Si5351 can generate frequencies from around 8 kHz to around 160 MHz. The recommended crystal frequency is 25 MHz. How can it generate frequencies in excess of 6X the basic clock rate?
- How do I know which frequencies are able to be generated?
- Can I modify the CircuitPython code to generate a frequency (or two) of my choice?
- Does it really work to write TRUE or FALSE to a particular place and turn that particular output ON / OFF?
- It seems like when the output frequency is "high" the square wave output turns into a more sinusoidal waveform. Why is that?
- What if I want a sine wave, or triangle wave, or saw-tooth wave... Can I use this to generate those waveforms?
- I've been thinking a lot about generating in-phase (I) and in-quadrature (Q) signals to drive mixers. Can I use this clock generator to directly generate I & Q for my mixer drive?
- If I wanted to try designing a PLL, might this be a gizmo that I could use to test my PLL?
- What is phase noise? And how is it related to "jitter"? And it this a low-noise part? Or not? How can I tell?
- So, Steve, if this is used for the "low frequency regime", what is used in the "high frequency regime" to provide the signal source in the NanoVNA V2 Plus4?

## Conclusions

TODO

