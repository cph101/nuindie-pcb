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

Beyond that lies the LED board. This The upper face of this board contains a horizontal 4-pin header. The lower side contains 3 contacts for charging the battery, resistors, and pairs of LEDs (never on simultaneously, and the right one is a warmer colour). (See photo below)

<img src="https://github.com/cph101/nuindie-pcb/blob/main/LED_Board.jpg?raw=true" alt="The LED board underside" height="300px" />

The LED board is fixed to a metal plate by 2 [length] PH3 screws, which is, in turn, fixed to a plastic support frame using 3 more.
This frame supports the upper board, which controls the lower board and charges the battery through a dual jumper wire

<img src="https://github.com/cph101/nuindie-pcb/blob/main/Logic_Board.jpg?raw=true" alt="The logic board top side" height="300px" />

Due to poor photo quality, I attach the text on top of the components:
```
R6, R7: 4R70
R11: 102

R12, R8: 512
R13: 5601
R9: 1095
R3: 102
R1: 122
R5: R300

Lower controller: P1256A CPCA1V.1B
Upper controller: F5LMC
```
