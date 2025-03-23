# Nuindie-pcb

These are the results of my research to reverse engineer the printed circuit boards of the Sigor Nuindie Table lamp.
It was originally created to design custom PCBs to replace or hook into the proprietary ones, for the purposes of adding compatability with the Matter framework/CHIP project, so that it may be added to supporting smart home ecosystems.

This repository will be updated as the research is completed.

![Active Development Status](https://img.shields.io/badge/Status-Active_Development-green)

## 0. Prelude

In the following document, Directions will refer to the upwards direction when the silkscreen marking may be read correctly, i.e some components are "upside down". The names of components, when linked, will always be directed towards the datasheets of said components.

## 1. Composition

The internal structure of the lampshade can be seen quite easily on the [designer's website](https://sigor.de/en/products/interior-lights#c201), however, the PCBs' layouts remain a mystery to those who have not taken apart the lamp, as such I attach photos.

<img src="https://github.com/cph101/nuindie-pcb/blob/main/LED_Board.jpg?raw=true" alt="The LED board underside" height="300px" /><img src="https://github.com/cph101/nuindie-pcb/blob/main/Logic_Board.jpg?raw=true" alt="The logic board top side" height="300px" />

> LED Board (left), Logic board (right)

## 2. Logic

The lower IC manages the battery loading and discharge, and the top controller switches the active LEDs based on self-capacitance of the electrode in the center of the board. Due to the unavailability of the components, I will use alternatives for my custom board.

Fortunately, the ESP32 IC (and modular derivatives) provides an array of pins which have the ability to monitor capacitance, and as such, can entirely replace the function of the top controller.

The [2200mAh 16850 battery](https://www.akumulator.si/images/products/Baterija_li-ion_18650_2200mah.pdf), although marked with 3.7V, has a charge voltage of 4.2V. For those interested, two are connected in parallel to double capacity while maintaing voltage.

As such, a [TP5100](https://voltiq.ru/datasheets/TP5100-datashhet.pdf)-based circuit is an appropriate solution to manage battery charging, while supporting simultaneous discharge.

<!--
Considering the touch sensing, I will use the [TTP224N-BSB](https://www.sunrom.com/download/SUNROM-TTP224N-BSB_V3.1_EN.pdf) chip set to `Direct mode, CMOS active high output`, with SM set to single-key mode by connecting the pin to V<sub>SS</sub>/GND. All other pins (barring power and electrode-related) are left open.
-->
