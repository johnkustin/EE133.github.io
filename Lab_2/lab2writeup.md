# LAB 2 – Clock Generation with a Si5351A

## Authors

Author : John Kustin  
Lab partner: Yifan Zhu

## Abstract
TODO
- Clocks are basically in ALMOST EVERY system you will work on
## Background

TODO.
- previous course built colpitts oscillator. the number of times you will need to generate a clock far outnumber the times you would benefit from building a Colpitts oscillator from scratch. This being the case, I decided that we should do something more "representative" or "transferable" if you will.
- Si5351 clock generator IC is a "modern," low-cost, and widely used part. As I mentioned on several occasions, the Si5351 is the part used to provide a signal source for the low frequency (100kHz to ~ 140 MHz) regime in the NanoVNA V2Plus4 that you have used in the lab. To me this means that the part can be usefully applied in low cost, reasonable performance test equipment and it warranted further investigation.
- ![Si5351 datasheet](https://cdn-shop.adafruit.com/datasheets/Si5351.pdf)
- Adafruit Si5351 breakout ![page](https://learn.adafruit.com/adafruit-si5351-clock-generator-breakout/downloads)

goals:
in two hours or less, give you a very capable multi-channel clock generator that you could
- use for your projects
- take with you as you move forward in your career
- use to think about how clock generation works (fractional-N PLLs, etc.)


## Experimental Setup

TODO

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

