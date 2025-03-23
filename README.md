# Nuindie-pcb

These are the results of my research to reverse engineer the printed circuit boards of the Sigor Nuindie Table lamp.
It was originally created to design custom PCBs to replace or hook into the proprietary ones, for the purposes of adding compatability with the Matter framework/CHIP project, so that it may be added to supporting smart home ecosystems.

This repository will be updated as the research is completed.

![Active Development Status](https://img.shields.io/badge/Status-Active_Development-green)

## 0. Prelude

In the following document, Directions will always refer to the corresponding definition below:
- Composition of the shade: Up is the upwards direction when the lamp is fully assembled.
- Of a component: Up is the upwards direction when the silkscreen marking may be read correctly, i.e some components are "upside down"

The names of components, when linked, will always be directed towards the datasheets of said components.

## 1. Composition

The lower structure of the lamp can be seen quite easily through the official [battery replacement tutorial](https://www.youtube.com/watch?v=30Anm9yBXpk), however, the more interesting parts can only be seen by taking apart the lamp. Working bottom upwards...

At the bottom of the shade, lies the diffuser and [placeholder]. They are secured using two [length] PH0 screws.

Beyond that lies the LED board. This The upper face of this board contains a horizontal 4-pin header. The lower side contains 3 contacts for charging the battery, resistors, and pairs of LEDs (never on simultaneously, and the right one is a warmer colour). (See photo below)

<img src="https://github.com/cph101/nuindie-pcb/blob/main/LED_Board.jpg?raw=true" alt="The LED board underside" height="300px" />

The LED board is fixed to a metal plate by 2 [length] PH3 screws, which is, in turn, fixed to a plastic support frame using 3 more, which supports the upper (logic) board.

<img src="https://github.com/cph101/nuindie-pcb/blob/main/Logic_Board.jpg?raw=true" alt="The logic board top side" height="300px" />

## 2. Logic

I have concluded that finding alternatives to the ICs is the best course of action,
<details>
  <summary>See why</summary>

  
  The two ICs had the following text printed upon them:
  ```
  Lower controller: P1256A CPCA1V.1B
  Upper controller: F5LMC
  ```
  
  I tried to look these up using a variety of databases, but was unsuccessful. Due to the placement of the chips, I have concluded that the lower one manages the battery loading and discharge, and the top controller switches the active LEDs based on self-capacitance of the electrode in the center of the board.

</details>

The [2200mAh 16850 battery](https://www.akumulator.si/images/products/Baterija_li-ion_18650_2200mah.pdf), although marked with 3.7V, has a charge voltage of 4.2V. For those interested, two are connected in parallel to double capacity while maintaing voltage.

As such, a [TP5100](https://voltiq.ru/datasheets/TP5100-datashhet.pdf)-based circuit is an appropriate solution to manage battery charging, while supporting simultaneous discharge.

Considering the touch sensing, I will use the [TTP224N-BSB](https://www.sunrom.com/download/SUNROM-TTP224N-BSB_V3.1_EN.pdf) chip set to `Direct mode, CMOS active high output`, with SM set to single-key mode by connecting the pin to V<sub>SS</sub>/GND. All other pins (barring power and electrode-related) are left open.
