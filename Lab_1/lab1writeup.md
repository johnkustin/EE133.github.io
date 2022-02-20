# LAB 1 – Understanding “parasitic” properties of passive components with a VNA

## Authors

Author : John Kustin  
Lab partner: Yifan Zhu

## Abstract
The impedances of real-life passive components can be vastly different from their ideal circuit models. This deviation is typically caused by parasitics. In order to investigate this phenomenon, a vector network analyzer is used to measure the impedances of real-life capacitors and inductors. This investigation will help us circuit designers build better models of the componets we would like to use. 
## Background

In introductory circuits courses, passivie components like resistors, capacitors, and inductors are studied in order to understand their impedances. Simple models have been created which theoritecally describe the impedance of each device. For a resistor, capacitor, and inductor, their (ideal) impedances are respectively

<img src="https://render.githubusercontent.com/render/math?math=\color{gray}{Z_R = R}">  

<img src="https://render.githubusercontent.com/render/math?math=\color{gray}{Z_C = 1/j\omega C = -j/\omega C}">  

<img src="https://render.githubusercontent.com/render/math?math=\color{gray}{Z_L = j\omega L}">  

where R, C, L are the resistance, capacitance, and inductance, but <img src="https://render.githubusercontent.com/render/math?math=\color{gray}{\omega = 2\pi f}"> where <img src="https://render.githubusercontent.com/render/math?math=\color{gray}{f}"> is frequency in Hertz.

When these components are realized in real life, the construction of each tends to yield **parsitics**. For the purpose of this investigation, we consider parasitics as uninteded side-effects to the operation of the component that are inherent to its physical construction. Each of the resistor, inductor, and capacitor have an ideal impedance; parasitics would cause impedance deviations from their ideal models. How bad the deviation can get will be demonstrated in the following sections. More sophisticated models included the effects of parasitics. Some examples which model parasitics are shown below.

<figure>
<img src="images/realistic-capacitor-model.png" alt="Trulli" style="width:100%">
<figcaption align="center"><b>Fig.1 - Equivalent Circuit Model for a Capacitor and its parasitics.</b></figcaption>
</figure>

<figure>
<img src="images/realistic-inductor-model.png" alt="Trulli" style="width:100%">
<figcaption align="center"><b>Fig.2 - Equivalent Circuit Model for an Inductor and its parasitics.</b></figcaption>
</figure>

<figure>
<img src="images/realistic-resistor-model.png" alt="Trulli" style="width:100%">
<figcaption align="center"><b>Fig.3 - Equivalent Circuit Model for a Resistor and its parasitics.</b></figcaption>
</figure>

For example, in Figure 1 we can see how the inductance and resistance of the capacitor's leads affects the impedance of the capacitor. Even from this equivalent circuit model, we can gain intuition as a circuit designer as to why surface mount inductors might be preferable -- their lead parasitics should be less than that of a through hole inductor.

In Figure 2, there are no parasitics associated with the leads of an inductor. Roughly speaking, the reason is because the inductor is really just a long piece of (wound) wire; there is no defined "lead". Instead, there is a series resistance and parallel capacitance. These parasitics are what give the inductor a resonant frequency. We will see more of this later.

In Figure 3, we can see that real resistors have a parallel capacitor that can actually short the resistor at high frequencies. This parasitic can be a big problem when a circuit expects a frequency-independent resistor.

In this lab we will study the parasitic effects of the real-life capacitor and inductor. In the process of doing so, we will gain experience with a Vector Network Analyzer.

## Experimental Setup

Before we start measuring real-life impedances of real-life components we would like to form expectations for what we should see. 

### LTSpice Setups

#### *Realistic Capacitor*

<p float="left">
    <img src="images/realistic_capacitor_setup.png" style="width:49%" />
    <img src="images/realistic_capacitor_setup_parasitics.png" style="width:49%" />
    <figcaption align="center"><b>Fig.4 - LTSpice Testbench to study the impedance of the realistic capacitor model. Note the presence of the parasitics that were introduced in Figure 1.</b></figcaption>
</p>

#### *Realistic Inductor*

<p float="left">
    <img src="images/realistic_inductor_setup.png" style="width:49%" />
    <img src="images/realistic_inductor_setup_parasitics.png" style="width:49%" />
    <figcaption align="center"><b>Fig.5 - LTSpice Testbench to study the impedance of the realistic inductor model. Note the presence of the parasitics that were introduced in Figure 2.</b></figcaption>
</p>

Figures 4 and 5 respectively show the LTSpice testbenches used to study the impedance of the realistic capacitor and inductor models. The important point to take away from these setups is that the values of the parasitics are among the choices we have when instantiating the device. If we were to measure, say, an inductor's impedance and figure out the values of its parasitics, then we would be able to model that real device within our circuit simulator! In other words, the validity of our circuit models would increase dramatically. 

Both testbenches use a voltage source with an AC signal amplitude of <img src="https://render.githubusercontent.com/render/math?math=\color{gray}{1 V}"> so that when the division <img src="https://render.githubusercontent.com/render/math?math=\color{gray}{Z(j\omega) = V(j\omega) / I(j\omega)}"> is performed with the measured current, the result is the true impedance (not scaled by an arbitrary factor).

### NanoVNAv2

How will we measure the impedance of real life components? With the NanoVNAv2. The
<a href="https://NanoVNA.com" title="NanoVNAv2Homepage"> NanoVNAv2</a> "is a handheld Vector Network Analyzer (VNA) with small outline, originally designed by edy555"


<p float="left">
    <img src="images/vna.jpeg" alt="Trulli" style="width:49%">
    <img src="images/inductor_sma_setup.jpeg" alt="Trulli" style="width:49%">
    <figcaption align="center"><b>Fig.6 - Left: a photo of the NanoVNAv2 with female to male SMA adapters that was used to measure the impedances for the lab. Right: a photo of the NanoVNAv2 connected to a test structure built to hold the device under test (DUT), an inductor is the DUT in the figure. </b></figcaption>
</p>

<div id ="fig:vnablockdiagram">
<figure>
<img src="https://nanorfe.com/ug1101_html_e6b0dfe5414cde60.gif" alt="Trulli" style="width:100%;background-color:white">
<figcaption align="center"><b>Fig.6b - <a href="https://nanorfe.com/nanovna-v2-user-manual.html" title="Block Diagram"> Block Diagram</a> of the NanoVNAv2. Note the internal termination of the ports.  </b></figcaption>
</figure>

</div>

We used the VNA shown in Figure 6 to measure the impedances of various test fixtures. The internals of the NanoVNAv2 are shown in Figure 6b. Before using the VNA, we have to calibrate it according to a **S**hort **O**pen **L**oad **T**hru (SOLT) ![procedure](https://zone.ni.com/reference/en-XX/help/373153D-01/vnahelp/calibration_solt/) each time the cable type of the VNA was changed. This calibration is essential for obtaining valid measurements because it calibrates-out the losses of the cables; we would like to only measure the losses of our DUT.

There were four devices under test in the lab and they are shown below in Figure 7.
<!-- ![picture of the rf demo board](images/rf-demo-board.jpeg) -->

<p float="left">
    <img src="images/rf-demo-board.jpeg" alt="Trulli" style="width:60%">
    <img src="images/discrete-cap.jpeg" alt="Trulli" style="width:34%">
    <figcaption align="center"><b>Fig.7 - Left: a photo of the RF demo board which has a surface mount capacitor and a surface mount inductor. These two components were measured from the demo board. Right: a photo of the test structure built to hold the device under test (DUT), an capacitor is the DUT in the figure. </b></figcaption>
</p>

The cables used in measurements of the through hole capacitor (Figure 7) and through hole inductor (Figure 6) are shown in Figure 6. The cables used to measure the demo board (Figure 7) are not shown, but were of a different type. SOLT calibration was carried out whenever the cable types were switched.

## Measurements and Results

Now that we understand the LTSpice and NanoVNAv2 setups we can interpret the resulsts obtained from each context. First we present the results from LTSpice. Following that are the measurements from the NanoVNAv2. The resulsts are interpreted in the [`Discussion`](#discussion) section.

<figure>
<img src="images/ltspice_realistic_capacitor.png" alt="Trulli" style="width:100%">
<figcaption align="center"><b>Fig.8 - Impedance of the LTSpice realistic capacitor of Figure 4 swept from 1mHz to 1GHz. The impedance has a resonant frequency at about 19 MHz.</b></figcaption>
</figure>

<figure>
<img src="images/ltspice_realistic_inductor.png" alt="Trulli" style="width:100%">
<figcaption align="center"><b>Fig.9 - Impedance of the LTSpice realistic inductor of Figure 5 swept from 1mHz to 1GHz. The impedance has a resonant frequency at about 503 MHz.</b></figcaption>
</figure>

Figure 8 shows the simulated impedance of a 0.1micro Farad capacitor with 0.02 Ohms series resistance, 0.75nano Henry series inductance, 10Mega Ohm parallel resistance, and 0 Farad parallel capacitance. The impedance of the entire network has a resonant frequency around 19 MHz.

Figure 9 shows the simulated impedance of a 100nano Henry inductor with 0.26 Ohms series resistance, infinite Ohm parallel resistance, and 1pico Farad parallel capacitance. The impedance of the entire network has a resonant frequency around 503 MHz.

<p float="left">
    <img src="images/capacitor_2GHz_max.png" alt="Trulli" style="width:51%">
    <img src="images/capacitor_sma_meas.png" alt="Trulli" style="width:48%">
    <figcaption align="center"><b>Fig.10 - Left: Smith Chart showing S11 and Bode plots showing impedance magnitude of S11 and argument of S11 for the RF evaluation board Capacitor. Right: Smith Chart showing S21 and Bode plots showing impedance magnitude of S21 and argument of S21 for the through-hole capacitor. </b></figcaption>
</p>

Figure 10 shows impedance measurements for the surface-mount capacitor on the RF evaluation board and the through-hole capacitor. On the left we can see that the surface-mount capacitor has a resonant frequency around 300 MHz. On the right we can see the through-hole capacitor has a resonant frequency around 2.4 GHz. 

S21 parameters were used for the through-hole device because the test structure was not terminated at either end. The RF evaluation board's inductor and capacitor were each terminated (to ground) at one port. Furthermore, the NanoVNAv2 is internally terminated as it is shown in [Figure 6b](#fig:vnablockdiagram).

The righthand side Smith Charth indicates that the NanoVNAv2 measurement was not properly done -- this will be discussed in the [`Discussion`](#discussion) section.

<p float="left">
    <img src="images/inductor_2GHz_max.png" alt="Trulli" style="width:51%">
    <img src="images/inductor_sma_meas.png" alt="Trulli" style="width:48%">
    <figcaption align="center"><b>Fig.11 - Left: Smith Chart showing S11 and Bode plots showing impedance magnitude of S11 and argument of S11 for the RF evaluation board inductor. Right: Smith Chart showing S21 and Bode plots showing impedance magnitude of S21 and argument of S21 for the through-hole inductor. </b></figcaption>
</p>

Figure 11 shows impedance measurements for the surface-mount inductor on the RF evaluation board and the through-hole inductor. On the left we can see that the surface-mount inductor has a resonant frequency around 200 MHz. On the right we can see the through-hole inductor has a resonant frequency around 700 MHz. 

## Discussion
The LTSpice simulations predicted that real-life inductors and capacitors have reasonant frequencies which dramatically affect each component's impedance. The VNA measurements verify this case.

- The measured impedance of the discrete inductor (using the SMA test structure) reveals a resonant frequency around 700 MHz.  
- The measured impedance of the discrete capacitor (using the SMA test structure) reveals a resonant frequency between 2.222 GHz and 2.666 GHz.  
- The measured impedance of the surface mount inductor (using the RF test board) reveals a resonant frequency around 200 MHz.  
- The measured impedance of the surface mount capacitor (using the RF test board) reveals a resonant frequency around 300 MHz.  

Note that the frequency ranges which reveal resonance are different for each component. This behavior implies that one may need to search for the resonant frequency of any given component.

The resonant frequency of each structure can be **roughly** identified by noticing either the impedance peaks/droops, or the asymptotic impedance behavior.
At the resonant frequency, the impedance for an inductor increases while the capacitor's decreases. 


The circuit intuition for this behavior is:
- For the inductor, when <img src="https://render.githubusercontent.com/render/math?math=\color{gray}{f}"> is much below the resonant frequency <img src="https://render.githubusercontent.com/render/math?math=\color{gray}{f_o}">, <img src="https://render.githubusercontent.com/render/math?math=\color{gray}{f << f_o}">, the actual inductor looks like a short, the parasitic parallel capacitor looks like an open, so the impedance of the series resistor dominates. When  <img src="https://render.githubusercontent.com/render/math?math=\color{gray}{f >> f_o}"> the capacitor looks like an short, the inductor looks like an open, so the capacitance dominates the impedance. At resonant frequency, no component can be "assumed to be negligant", so the impedance is greatest. So on either ends, there is a relatively lower impedance than at the resonant frequency.
- For the capacitor, when <img src="https://render.githubusercontent.com/render/math?math=\color{gray}{f << f_o}">, the capacitor looks like an open. When <img src="https://render.githubusercontent.com/render/math?math=\color{gray}{f >> f_o}"> the inductor looks like an open. So on either extreme, there is a relatively higher impedance than at the resonant frequency.

The left hand side of Figure 11 shows an unrealistic measuremeant because the curve of S11 goes outside of the unit circle, implying that the part generates power. The most likely reason for this mistake is improper calibration. 

The presented measurements and plots are limited by the granularity of the impedance versus frequency sweep. To achieve an ideal measurement, an infinite amount of points measured by the VNA is required. Therefore, the plots derived from the VNA should not be considered "complete" representations of a any given component's impedance versus frequency behavior. The lesson learned from this limitatation is that if one wishes to characterize the impedance of an absolutely critical structure in a circuit, using as many points as possible in that measurement would yield the best characterization.

Once the proper measurements have been made, one can *extract* the values of the parasitic components from the impedance measurements of the VNA. The motivation for doing this as a circuits person is that one can use the parasitic values to more precisely model the components that will be used.

## Conclusions

Passive components in real-life are never ideal. In fact, their impedances may be widely different from the ideal models of impedance described in the Background section. Going further, if a specific component with a resonant frequency is used in the frequency range of resonance, the behavior of the circuit would deviate from expectations.

One way to improve the quality of measurements through the SMA fixtures is to use as short of leads as possible between the DUT and the SMA pins. Using shorter leads implies less inductance and resistance from the wires itself, so the impedance measurement is more true to the actual DUT. 

All models are wrong, but some are useful -- by measuring the real impedance of passive components with a VNA and including that information in our SPICE models, we can make our models of those devices less wrong and more useful.

