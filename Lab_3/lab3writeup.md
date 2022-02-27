# LAB 3 – Making a Diode-Ring Mixer

## Authors

Author : John Kustin  
Lab partner: Yifan Zhu

## Abstract
Mixers are ubiquitos in RF systems. In this lab, we gain hands on experience with how diode-ring mixers work by building one. Then, we attemp to measure some fundamental performance characteristics of the mixer. As a result of this work, we are capable in understanding the role mixers play in a larger circuit and how to quantify its ability to mix well.
## Background

Fundamentally, mixers multiply time domain signals. As a result of the signals being sinusoids, the multiplication generates the sum and difference frequencies of those input sinusoids. The mixer goes by many other names, including "modulator / demodulator", "multiplier", "synchronous detector", "phase detector", "upconverter / downconverter".

Let <img src="https://render.githubusercontent.com/render/math?math=\color{gray}{V_1(t)=A_1\cos(\omega_1t)}"> and <img src="https://render.githubusercontent.com/render/math?math=\color{gray}{V_2(t)=A_2\cos(\omega_2t)}">. Then <img src="https://render.githubusercontent.com/render/math?math=\color{gray}{V_1(t)\cdot V_2(t)=\frac{A_1A_2}{2}[\cos(\omega_1 + \omega_2)t + \cos(\omega_1-\omega_2)t]}">. Mixing generates a sum and difference frequency.

For downconversion, a mixer requires a radio frequency signal (RF) and a local oscillator (LO) to generate an intermediate frequency signal (IF). For upconversion, a mixer requires an IF signal and an LO to generate *two* RF signals. Figure B.1 shows two examples of frequency conversion.[^1] 

[^1]: Figure B.1 is taken from Steve Clark's slides for Stanford's EE133 course during the Winter of 2022 offering.

The figure demonstrates high side injection in the downconversion case. High side injection means your LO frequency is higher than your RF signal. 

<figure>
<img src="images/freq-shifting.png">
<figcaption>Figure B.1 - An example of frequency conversion. The mixer is a three port device and has two directions to shift a frequency. The figure demonstrates the effect of downconversion and upconversion in the frequency domain. </figcaption>
</figure>

## Experimental Setup

<figure>
<img src="images/IMG_7841.jpeg">
<figcaption>Figure ES.1 - The mixer constructed in the lab. It consists of a <a href="https://rocelec.widen.net/view/pdf/qxnorbh6l6/INFNS15420-1.pdf?t.download=true&u=5oefqw">BAT15-099R diode-ring</a> and two <a href="https://www.minicircuits.com/pdfs/ADT4-1WT+.pdf"> ADT4-1WT+ transformers </a>. The left, right, and middle ports are respectively for RF, LO, and IF. </figcaption>
</figure>

Figure ES.2 shows a schematic view of the mixer. The mixer is completely passive -- there are no active devices in the circuit. This fact has consequences for conversion gain/loss and will be explored later.

<figure>
<img src="images/mixer-schematic.png">
<figcaption>Figure ES.2 - A schematic view of the mixer. It uses two transformers and one diode ring. The orange numbers correspond to the pin numbers on the ADT4-1WT+ package. The pink numbers correspond to the pin numbers on the BAT15-099R package. </figcaption>
</figure>

<figure>
<img src="images/IMG_7842.jpeg" style="width:49%">
<img src="images/IMG_7843.jpeg" style="width:49%">
<figcaption>Figure ES.3 - Functional verification of the mixer. The RF is an 8 MHz signal being mixed with a 12 MHz LO. The up and down converted signals are visible in the frequency domain (right hand picture) at 4 and 20 MHz. There is a noticable amount of LO leakage seen at 12 MHz. Three other spurs are visible between 8 and 10 MHz, and at 16 MHz. </figcaption>
</figure>


## Measurements and Results

To study the 1 dBm compression point and conversion gain/loss, the IF power was measured for different RF powers. The LO was an 8 MHz sinusoid at 7 dBm. The input RF power was stepped from -1 dBm to 7 dBm in +1 dBm increments. At each step, the output IF power was measured. From this data, the 1 dBm compression point and conversion loss were computed and are shown in figures MR.1 and MR.2.

<figure>
<img src="images/p1db.png">
<figcaption>Figure MR.1 - Measured IF power as a function of different RF powers. The 1 dBm compression point occurs just beyond 1 dBm of RF power. </figcaption>
</figure>

Figure MR.1 reveals that the diode ring mixer reaches its 1 dBm compression point around 1 dBm of RF power. 

<figure>
<img src="images/conversion.png">
<figcaption>Figure MR.2 - Computed conversion loss as a function of different RF powers. The conversion loss is around 6 dBm for RF powers below 1 mW. The convesrion loss is in dBm computed according to <code>convesrion = (IF power)[dBm] - (RF power)[dBm].</code></figcaption>
</figure>

<a href="https://www.qsl.net/va3iul/RF%20Mixers/RF_Mixers.pdf"> publication</a>

<figure>
<img src="images/spur-levels.jpg">
<figcaption>Figure MR.3 - Spur levels of the mixer when the LO is a 7 dBm 30 MHz sinusoid and the RF is a 0 dBm 7 MHz sinusoid. The span of the spectrum is 60 MHz so many spurs can be seen. The up and down mixed IF signals have around -10 dBm power and are distinct from the spurs. </figcaption>
</figure>


<figure>
<img src="images/if-150kHz.jpeg">
<figcaption>Figure MR.4 - The IF signal from mixing a 30 MHz LO with a 29.85 MHz RF signal. The IF signal is about 50 dBm above the noise floor. The IF signal has a power of -6 dBm. The minimum IF frequency is lower than 150 kHz.</figcaption>
</figure>


<figure>
<img src="images/if-100kHz.jpeg">
<figcaption>Figure MR.5 - The IF signal from mixing a 30 MHz LO with a 29.90 MHz RF signal. The IF signal is less than 50 dBm above the noise floor. The IF signal has a power of -10 dBm. Intermodulation spurs have about 150 kHz of separation. The minimum IF frequency is lower than 150 kHz.</figcaption>
</figure>


<figure>
<img src="images/if-10kHz.jpeg">
<figcaption>Figure MR.6 - The IF signal from mixing a 30 MHz LO with a 29.99 MHz RF signal. The IF signal is less than 30 dBm above the noise floor. The IF signal has a power of -30 dBm. Intermodulation spurs have about 75 kHz of separation. One confusing part of this line of investigation is that the notion of when the signal is indistguishable is not well defined.</figcaption>
</figure>

## Discussion
todo

- We talked about the 1dB compression point. Why is this an important performance metric? Can we change it? If so, how might we do that?
- There was some discussion about LO leakage. Why is that important and what can be done about that?
- Did you use your mixer as an up converter? As a down converter? If you didn't try both of these, why not?
- Did you measure the conversion gain vs LO drive level. I guess you must have if you determined the 1dB compression point. How did you make those measurements? Was this at a single frequency? If so was there anything special about the frequency you chose? If you did the measurements at different frequencies, did you find about the same result?
- There were a number of questions about why one would be concerned about the minimum IF frequency. Greig pointed out that the diode ring mixer should "go to DC" but that the FET ring wouldn't. Why might that be something one would be concerned about? What about the Gilbert cell mixer; should that "go to DC"? Does all this have anything to do with zero IF SDR's or radar stuff?
- In the mixer you built, why wouldn't the mixer go to zero IF? What could be done if you want it to go to zero IF?
## Conclusions

todo