# Installation & Setup

## Adding to Your Project

1. Purchase and download the Brightnode Interaction System from the [Fab store](https://www.fab.com/listings/ab8a0d08-8968-4593-8180-fc2e1cd71ba9)
2. Migrate the **Brightnode Interaction System** folder into your project
3. Delete the Showcase folder if you do not need the example content

## Required Project Settings

**Custom Depth Stencil**

`Project Settings - Rendering`

Set Custom Depth Stencil Pass to **Enabled with Stencil**

This is required for the outline highlighting system.

## Enable Common UI Plugin

`Edit - Plugins - Common UI`

Restart the editor when prompted.

## Game Viewport Client

`Project Settings - Engine - General Settings`

Set Game Viewport Client Class to **CommonGameViewportClient**

## Interaction Trace Channel

`Project Settings - Collision`

Add a new Trace Channel:

- Name: `Interaction`
- Default Response: `Block`

Interactable meshes must block this channel to be detected.

## Common UI Controller Data

Open Common Input Settings and add the included controller data assets:

- Keyboard Input Data
- Gamepad Input Data

## Support

- 💬 **Discord** - [discord.gg/VSu4A7XxA7](https://discord.gg/VSu4A7XxA7)
- 📧 **Email** - brightnodestudio@gmail.com
