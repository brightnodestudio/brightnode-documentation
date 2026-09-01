# Installation

The Brightnode Outline System is supplied as an Unreal Engine project containing the complete system and a showcase level.

## Before You Start

Open the included showcase level first. It demonstrates the major features and provides working Blueprint examples that can be inspected alongside this documentation.

## Core Assets

The system is built around:

* **Outline Component**, the main player-facing API
* **Outline World Manager**, manages shared Team and Global outline state
* **Outline Preset Library**, registers the presets available to the system
* **Outline Preset Data Assets**, define individual outline behaviours

## Project Setup

Add the required BNOS content to your project using the distribution method provided with the Fab product.

After integration:

1. Add the Outline Component to the player that will display outlines.
2. Ensure the World Manager is present using the supplied implementation.
3. Assign an Outline Preset Library to the World Manager.
4. Create the Gameplay Tags required by your presets.
5. Create and register your Outline Presets.
6. Test a Local outline before moving on to Team or Global behaviour.

See **Quick Start** for the complete first-outline workflow.
