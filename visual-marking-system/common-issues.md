# Common Issues - Visual Marking System

## Outlines Not Appearing

**Custom Depth Stencil Not Enabled**

Open Project Settings - Rendering and set Custom Depth-Stencil Pass to **Enabled with Stencil**. This is required for outlines to render.

**Preset Not Registered**

Ensure your DA\_OutlinePreset is added to **DA\_OutlinePresetLibrary\_Default**. If the preset is not in the library the system cannot find it.

**Preset ID Not Unique**

Preset IDs must be unique across all outline presets. Duplicate IDs will cause unexpected behaviour.

## Symbols Not Spawning

**Preset Not Registered**

Ensure your DA\_SymbolPreset is added to **DA\_SymbolPresetLibrary\_Default**.

**Preset ID Not Unique**

Symbol Preset IDs must be unique across all symbol presets.

**Symbol Already Exists**

Use the helper function to check whether a symbol is already attached before calling Spawn Symbol Actor. Spawning on top of an existing symbol may produce unexpected results.

## Component Missing

Ensure **AC\_VisualMarkingSystem** is added to the character Blueprint. This component is required for the callable functions to work.

## Bug Reports

Report bugs in the Brightnode Studio Discord in the **#bugs-visual-marking-system** channel.

Please include Unreal Engine version, steps to reproduce, and screenshots or video where possible.

💬 [discord.gg/VSu4A7XxA7](https://discord.gg/VSu4A7XxA7)
