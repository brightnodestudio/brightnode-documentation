# Outline System

The outline system applies custom depth stencil outlines to actors using configurable preset data assets.

## How It Works

When an outline is applied to an actor, the system sets the actor's mesh components to render to the custom depth buffer using the stencil value defined in the preset. A post-process material reads the stencil and renders the outline colour around the actor.

## DA_OutlinePreset

Each outline style is defined as a **DA\_OutlinePreset** data asset containing:

- Preset ID — unique identifier used by the system to find the preset
- Outline colour and thickness settings

## Applying and Removing Outlines

All outline operations go through the single callable function **Set Outline On Actor**. Pass true to apply and false to remove. The system handles the rest.

## Requirements

Custom Depth Stencil Pass must be set to **Enabled with Stencil** in Project Settings - Rendering.
