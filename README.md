# Nuindie-pcb

This is the results of my research to reverse engineer the printed circuit boards of the Sigor Nuindie Table lamp.
It was originally created to design custom PCBs to replace or hook into the proprietary ones, for the purposes of adding compatability with the Matter framework/CHIP project, so that it may be added to supporting smart home ecosystems.

This repository will be updated as the research is completed.

![Active Development Status](https://img.shields.io/badge/Status-Active_Development-green)

## 0. Prelude

In the following document, Directions will always refer to the corresponding definition below:
- Composition of the shade: Up is the upwards direction when the lamp is fully assembled.
- Of a component: Up is the upwards direction when the silkscreen marking may be read correctly, i.e some components are "upside down"

The lower structure of the lamp can be seen quite easily through the official [battery replacement tutorial](https://www.youtube.com/watch?v=30Anm9yBXpk).

However, without owning the lamp, one cannot deduce the logic-related circuit structure. As such, I have fully disassembled said lamp and tested the implementation of various features.

## 1. Composition

Working bottom upwards...

At the bottom of the shade, lies the diffuser and [placeholder]. They are secured using two [length] PH0 screws.

Beyond that lies the LED board. This PCB only contains LEDs and resistors, and can be manipulated by altering the electronic signals of the 4 pin-header on the top of the board. These are documented in section [schematics]
