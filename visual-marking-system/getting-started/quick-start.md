# Quick Start Guide

Get outlines and symbols working in your project in a few minutes.

## 1. Create and Register an Outline Preset

Create a new Data Asset based on **DA\_OutlinePreset** and set a unique Preset ID.

Open **DA\_OutlinePresetLibrary\_Default** and add your new preset to the library array. Save.

## 2. Apply an Outline

Call **Set Outline On Actor** from any Blueprint:

- Target Actor — the actor to outline
- Outline Preset — your DA\_OutlinePreset
- Enabled — true to apply, false to remove

## 3. Create and Register a Symbol Preset

Create a new Data Asset based on **DA\_SymbolPreset** and set a unique Preset ID. Configure the symbol settings.

Open **DA\_SymbolPresetLibrary\_Default** and add your new preset to the library. Save.

## 4. Spawn and Clear Symbols

Use the helper function to check whether a symbol is already attached before spawning.

Call **Spawn Symbol Actor** to attach a symbol:

- Target Actor
- Symbol Preset

Call **Clear Symbol On Actor** to remove it:

- Target Actor

## Result

- Outline toggles on and off via Set Outline On Actor
- Symbol spawns and clears via Spawn Symbol Actor and Clear Symbol On Actor
- All behaviour is driven by callable functions and preset data assets
