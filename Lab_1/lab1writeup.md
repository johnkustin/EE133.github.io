# LAB 1 – Measuring “parasitic” properties of passive components with a VNA

## Authors

Author : John Kustin  
Lab partner: Yifan Zhu

## Abstract

## Background

In introductory circuits courses, passivie components like resistors, capacitors, and inductors are studied in order to understand their impedances. Simple models have been created which describe (theoritecally) the impedance of each device. For a resistor, capacitor, and inductor, their (ideal) impedances are respectively

$$Z_R = R  \newline
Z_C = 1/j\omega C = -j/\omega C \newline
Z_L = j\omega L$$

where R, C, L are the resistance, capacitance, and inductance, but $\omega = 2\pi f$, where $f$ is frequency in Hertz.

When these components are realized in real life, the construction of each tends to yield **parsitics**. For the purpose of this investigation, we consider parasitics as uninteded side-effects to the operation of the component that is inherent to its physical construction. The well-understood (by others, not us yet) parasitics that are commonly included in more sophisticated models are

> The realistic capacitor
![A realistic capacitor model](images/realistic-capacitor-model.png)

> The realistic inductor
![A realistic inductor model](images/realistic-inductor-model.png)

> The realistic resistor
![A realistic resistor model](images/realistic-resistor-model.png)

In this lab we will study the parasitic effects of the real-life capacitor and inductor. In the process of doing so, we will gain experience with a Vector Network Analyzer.

## Experimental Setup

Before we start measuring real-life impedances of real-life components we would like to form expectations for what we should see. 

### LTSpice

#### Capacitor
This LTSpice testbench was used to measure the impedance of the realistic capacitor model.
![LTSpice realistic capacitor testbench](images/realistic_capacitor_setup.png)
The parasitics are included within the capacitor model's settings:
![capacitor settings](images/realistic_capacitor_setup_parasitics.png)

#### Inductor

This LTSpice testbench was used to measure the impedance of the realistic inductor model.
![LTSpice realistic inductor testbench](images/realistic_inductor_setup.png)
The parasitics are included within the inductor model's settings:
![inductor settings](images/realistic_inductor_setup_parasitics.png)

Both testbenches use a voltage source with an AC signal amplitude of $1 V$ so that when the division $Z(j\omega) = V(j\omega) / I(j\omega)$ is performed with the measured current, the result is the true impedance (not scaled by an arbitrary factor).

### NanoVNA

Impedance measurements were performed with the NanoVNA

## Measurements and Results

## Discussion

## Conclusions