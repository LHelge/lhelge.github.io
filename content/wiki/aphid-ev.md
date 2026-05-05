---
title: Aphid EV
category: Projects
tags:
  - ev-conversion
  - embedded
  - electronics
---

Aphid EV is a DIY electric vehicle conversion of a classic VW Beetle using a Nissan Leaf
drivetrain. The project is documented at [bladlus.se](https://bladlus.se). The name comes
from the Swedish word "bladlus" (aphid/leaf louse) — a nod to both the Leaf donor and the
small-but-persistent nature of the build.

# Team

The project is run by two brothers. The build journal, schematics, and firmware notes are
published on the [project site](https://bladlus.se) which was the main reason I developed [[Aphid]] in the first place.

# Car

A 1969 VW Beetle that was initially restored by our father in the mid 90's and used as a daily driver for several years. It eventually broke down and became a garden ornament for more than a decade before being sold. My brother managed to buy it back with the intention for us to convert it, and then gave me an EM57 motor as a birthday gift on my 40th birthday.

# Drivetrain

The power electronics are sourced from a Nissan Leaf:

- **Motor** — Nissan Leaf EM57
- **Inverter** — Nissan Leaf traction inverter
- **PDM** — Nissan Leaf Power Delivery Module

The battery will be built from donor EV modules, with the specific type determined by
availability.

# Control system

Rather than using the original Leaf VCM, the project develops a custom Vehicle Control Module to tie everything together.

# Links

- [Project site](https://bladlus.se)
- [Source code](https://github.com/lhelge)
