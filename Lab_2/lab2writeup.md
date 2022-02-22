# LAB 2 – Clock Generation with a Si5351

## Authors

Author : John Kustin  
Lab partner: Yifan Zhu

## Abstract
Clocks are pervasive in modern electronic circuits, some examples are digital circuitry, RF mixing, and  data converters. Due to the engineering effort and production cost of modern integrated circuits it is often desired that circuits nowadays are reconfigurable, i.e. programmable. In this lab, we demonstrate the Si5351 programmable clock generator. It is based on a fractional-N PLL and can be used for a plethora of projects due to its low price point and reasonable performance. Furthermore, the activities detailed in the report will teach the young engineer fundamentals of clock generation and some of the challenges inherent in clocked systems.
## Background

Previous iterations of Stanford University's Analog Communications Design Laboratory (EE133/233) had a lab on oscillators. In the past, they built <a href="https://en.wikipedia.org/wiki/Colpitts_oscillator"> Colpitts oscillators </a>. Times have changed and the current landscape of electronics is such that the number of times one will need to generate a clock is far greater than the number of times one would benefit from building a Colpitts oscillator. 

This lab is meant to introduce the emerging engineer to a *modern*, low-cost, and widely used clock generator -- the <a href="https://cdn-shop.adafruit.com/datasheets/Si5351.pdf"> Si5351 </a> -- and the mechanisms which enable it, e.g. a fractional-N PLL. This part has a low price point, reasonable performance, and successful history (it is used in the NanoVNA V2 that was used in Lab1!). The experience gained through this lab can be carried forward in a young engineer's career as they embark on projects that will most certainly include clock generation.[^1]

This lab uses <a href ="https://circuitpython.org"> CircuitPython</a>, which enables low-stress communication with embedded microcontrollers through a Python API.

[^1]: This background is pulled from Steve Clark's <a href="https://canvas.stanford.edu/courses/148940/discussion_topics/722850"> Canvas Announcement </a>.

## Experimental Setup

The hardware used in this lab includes:
- <a href="https://learn.adafruit.com/adafruit-si5351-clock-generator-breakout/downloads">Adafruit Si5351 breakout board</a>
- <a href="https://learn.adafruit.com/introducing-adafruit-itsybitsy-m4">ItsyBitsy M4 microcontroller</a>
- 3x male edge-launch SMA adapters for 62 mil thick PCB
- solderless breadboard
- jumper wires
- oscilloscope and probe
- spectrum analyzer and probe

The spectrum analyzer used was the Agilent N1996A, which has a bandwidth of 100 kHz to 6 GHz. The oscilloscope used was the Agilent DSO6054A, which has a bandwidth of DC to 500 MHz and is capable of 4 Gigasamples per second.

<p style="text-align:center;">
<figure>
<img src="images/IMG_7812.jpeg" alt="breadboard setup" style="width:100%">
<figcaption align="center">Fig. 1 - An Adafruit Si5351 breakoutboard with attached SMA adapters connected to an ItsyBitsy M4 microcontroller through a solderless breadboard. An oscilloscope probe is attached to the <code>clk0</code> port of the breakout board. </figcaption>
</figure>
</p>

The code which controlls the clock generation is from an <a href="https://learn.adafruit.com/adafruit-si5351-clock-generator-breakout/circuitpython">Adafruit tutorial</a> for the Si5351 breakout board. As shown in Figure 1 there are three output clocks <code>clk0, clk1,</code> and <code>clk2</code>. They are respectively set to generate clocks at 112.5 MHz, 13.553115 MHz, and 10.76 kHz. Summarizing the tutorial, the clock generation happens by i) using a 25 MHz crystal as a stable source of oscillation for the oscillator ii) feeding the output of the oscilator to the two on-chip N-fractional PLLs and iii) controlling the PLLs through I<sup>2</sup>C. Please refrence the <a href="https://learn.adafruit.com/adafruit-si5351-clock-generator-breakout/circuitpython"> Adafruit Si5351 breakout board tutorial </a> and Si5351  <a href="https://cdn-shop.adafruit.com/datasheets/Si5351.pdf"> datasheet</a> for more details.



## Measurements and Results

In this section we will view the time and frequency domains of the three different clocks.

In Figure 2 the 10.70 kHz clock is visible in the frequency and time domains. On the left hand side of the figure, the fundamental frequency (10.70 kHz) has about 48 dB of spurious free dynamic range (SFDR) and has about 70 dB separation from the noise floor. The span of the measuremeant is 13 kHz, so the view is not able to show the odd harmonics of a square wave. On the right hand side we can see a crisp square wave that has minor over/under-shoot at the rising and falling edges, respectively. The defined levels of the clock (HI/LO) are constant, absent from the noise which gives the levels some "thickness".

<p float="left">
<img src="images/IMG_7818.jpeg" alt="frequency spectrum of 10.70kHz clock" style="width:49%">
<img src="images/IMG_7815.jpeg" alt="time domain view of 10.70kHz clock" style="width:49%">
<figcaption align="center">Fig. 2 - Left: Frequency spectrum of 10.70 kHz clock. Center frequency is 10.70 kHz. Span of the window is 13 kHz. Resolution bandwidth is 130 Hz. 401 points were collected for the spectrum. Right: Voltage versus Time view of 10.70 kHz clock. The plot uses 20 microsecond divisions in the horizontal direction and 1 Volt divisons in the vertical direction. </figcaption>
</p>

Figure 3 shows the 13.552 MHz clock in the frequency and time domains. On the left hand side of the figure, the fundamental frequency (13.552 MHz) has about 48 dB of spurious free dynamic range (SFDR) and has roughly 60 dB separation from the noise floor. The span of the measuremeant is 312 kHz. On the right hand side we can see some distortions in the square wave. The slew of the rising and falling edges is weaker than in the 10.70 kHz case. The under and over shooting are more pronounced than before.

<p float="left">
<img src="images/IMG_7817.jpeg" alt="frequency spectrum of 13.552 MHz clock" style="width:49%">
<img src="images/IMG_7814.jpeg" alt="time domain view of 13.552 MHz clock" style="width:49%">
<figcaption align="center">Fig. 3 - Left: Frequency spectrum of 13.552 MHz clock. Center frequency is 13.552 MHz. Span of the window is 312 kHz. Resolution bandwidth is 3.12 kHz. 401 points were collected for the spectrum. Right: Voltage versus Time view of 13.552 MHz clock. The plot uses 20 nanosecond divisions in the horizontal direction and 1 Volt divisions in the vertical direction.</figcaption>
</p>

Figure 4 displays the 112.50 MHz clock in the frequency and time domains. The spectra of the signal shows that the fundamental has about 48 db of SFDR and about 65 dB of separation from the noise floor. The span of the measurement is 2 MHz. The time domain view of the "clock" is almost unrecognizable. The signal appears more sinusoidal than square. There is no under/over shooting -- instead, the slew rate of the 112.50 MHz signal is the slowest of the three clocks. 

<p float="left">
<img src="images/IMG_7819.jpeg" alt="frequency spectrum of 112.50MHz clock" style="width:49%">
<img src="images/IMG_7813.jpeg" alt="time domain view of 112.50MHz clock" style="width:49%">
<figcaption align="center">Fig. 4 - Left: Frequency spectrum of 112.50 MHz clock. Center frequency is 112.50 MHz. Span of the window is 2 MHz. Resolution bandwidth is 20 kHz. 401 points were collected for the spectrum. Right: Voltage versus Time view of 112.50 MHz clock. The plot uses 2 nanosecond divisions in the horizontal direction and 1 Volt divisions in the vertical direction. Note the severe filtering of the signal. </figcaption>
</p>

## Discussion

In future iterations of this lab, the pictures of the spectrum should have a wide-enough span to capture at least the first harmonic of the square wave. A more accurate SFDR performance can be given with the harmonic information.

It seems that as the desired output frequency is increased, the output clock appears more sinusoidal than square-like. We propose two hypotheses: i) the clock-generation circuit cannot perform as fast as we want it to; ii) higher frequency content is more attenuated in its propagation from output of the Si5351 to input of the oscilloscope, so faster signals are naturally more attenuated. The first hypothesis is incorrect because the datasheet reports the device can supply output clocks up to 160 MHz. The more likely culprit for the degradation in shape is the attenuation of high frequencies from the parasitics of the traces, leads, packages, etc. 

This natural attenuation suggests that we can generate more than just a square wave with this circuit. If we deliberatly filter the output square wave, then perhaps we can make a sine wave or triangle wave. Indeed, to make a sine wave, what we would need to add to the output of the circuit is a filter to remove all harmonics but preserve the fundamental frequency. If we attach an <a href="https://en.wikipedia.org/wiki/Triangle_wave#Relation_to_the_square_wave">integrator </a> to the output then we can generate a triangle wave.

Another application of the Si5351 is generation of in-phase and in-quadrature signals to drive mixers. Recall that the in-phase signal can have any frequency or phase. What makes the pair I/Q is that the in-quadrature signal **must** be 90 degrees out of phase with the in-phase signal. The Si5351A (the specific model used in this lab) has three outputs. Suppose we take the output of <code>clk0</code> to be the "in-phase" signal. Could we then use <code>clk1</code> to generate the "in-quadrature" signal? From the datasheet we can see that I/Q signal generation is possible with the Si5351 because each clock channel can be configured with a static phase-offset. These configurations are done through the <code>CLKX_PHOFF</code> register, where <code>X</code> is the number of the clock. The resolution of the offset is a function of the period of the PLL associated with the clock output. The datasheet says the resolution is <code>T<sub>vco</sub>/4</code>, where <code>T<sub>vco</sub></code> is the period of the VCO/PLL associated with the output. If <code>clk0</code> is configured to be a 100 MHz signal with no "initial phase offset" (this is a term used in the datasheet) then we would configure <code>clk1</code> to be a 100 MHz signal with <code>CLK1_PHOFF</code> set to be <code>7'b000001</code>. This delays <code>clk1</code> by a quarter of a period relative to <code>clk0</code>, making the two signals an I/Q pair. All kinds of configuration can be done through CircuitPython according to the API in <a href="https://github.com/adafruit/Adafruit_CircuitPython_SI5351"> this repository</a>.

None of these applications need to be done at a specific frequency. The Si5351 is capable of generating frqeuencies from 8 kHz to 160 MHz by using a fractional-N phase locked loop (PLL). Roughly speaking, fractional-N PLLs can perform a frequency multiplication on the input source of oscillation to generate output clocks that are greater in frequency than the input signal. This mechanism is enabled by a frequency divider put in *negative feedback*. To generate signals that are lower in frequency than the reference oscillator, fracional-N PLLs use clock divider circuits to make the resulting output clock slower. This mechanism is most readily enabled by counting circuits. For more information on how these devices work, please refer to this <a href="https://www.ti.com/lit/an/swra029/swra029.pdf?ts=1645439625997">TI datasheet</a>.

Phase noise is an indicator of the signal quality[^2] of our generated clock. Phase noise is a measure of the quality in the frequency domain. It has an analog in the time domain called the phase jitter. Clean signals have low jitter, which implies that most of the signal's energy is concentrated on the fundamental frequency.[^3] The Si5351 datasheet reports that the part has a maximum phase jitter of 11 picoseconds rms. To get a feel for how good this is let us do a thought experiment on I/Q signal generation. Suppose we designate a 160 MHz clock as our in-phase signal and we want to generate its quadrature signal. The worst case phase jitter implies the in-quadrature signal's edges would be 11 picoseconds off from what we want. In other words, if we want (1/(160 MHz))/4 = 1.5625 ns of delay for 90 degrees phase difference between I and Q signals, then the worst case phase jitter bounds the delay to be within 1.5735 ns or 1.5515 ns. These bounds respectively correspond to 90.6336 degrees and 89.3664 degrees of phase difference -- a range of 1.2672 degrees of phase difference. Whether or not these numbers are "good" is relative to the desired application. 

[^2]: For more detail please review <a href="https://www.ti.com/lit/an/swra029/swra029.pdf?ts=1645439625997"> this TI datasheet</a>.

[^3]: For more detail on the types of jitter please see <a href="https://www.edn.com/jitter-measurement-references-matter/"> this EDN post</a>.

## Conclusions

We have demonstrated that the Si5351 is a low-cost, easy to use clock generator that is capable of being included in larger circuits, e.g. with microcontrollers, and quickly programmed with CircuitPython. This device can be used as the clock generator in a circuit to generate arbitrary waveforms or generate the I/Q signals for a mixer. The device works in a relatively low frequency range of 8 kHz to 160 MHz but with good enough phase jitter for a variety of projects. For projects with more critical and stringent requirements, the Si5351 should probably be replaced with a component that has lower phase jitter. The skills and understanding developed through this lab are widely applicable to modern projects due to the pervasiveness of clocked systems.  