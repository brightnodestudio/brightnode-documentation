# Installation & Setup

This page covers the required project setup for the Brightnode Interaction System.

Complete these steps before creating your first interaction.

### Adding to Your Project

1. Ensure your project has the CommonUI plugin enabled
2. Purchase and download the Brightnode Interaction System from the [Fab store](https://www.fab.com/listings/ab8a0d08-8968-4593-8180-fc2e1cd71ba9)
3. Migrate the **Brightnode Interaction System** folder into your project
4. Delete the Showcase folder if you do not need the example content

### Required Project Settings

**Custom Depth Stencil**

`Project Settings - Rendering`

Set Custom Depth Stencil Pass to **Enabled with Stencil**

This is required for the outline highlighting system.

<figure><img src="../../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

### Enable Common UI Plugin

`Edit - Plugins - Common UI`

Restart the editor when prompted.

<figure><img src="../../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

### Game Viewport Client

`Project Settings - Engine - General Settings`

Set Game Viewport Client Class to **CommonGameViewportClient**

<figure><img src="../../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

### Interaction Trace Channel

`Project Settings - Collision`

Add a new Trace Channel:

* Name: `Interaction`
* Default Response: `Block`

Interactable components must be attached to actors with collision that blocks the `Interaction` trace channel.

If the interaction trace cannot hit the actor, the actor cannot be focused or interacted with.

<figure><img src="../../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

### Common UI Controller Data

Open Common Input Settings and add the included controller data assets:

* Keyboard Input Data
* Gamepad Input Data

<figure><img src="../../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>

### Setup Complete

Once these project settings are configured, the Interaction System is ready to use.

Continue to **Quick Start** to create your first interactable actor.

### Support

* 💬 **Discord** - [discord.gg/R6zJkHx6x7](https://discord.gg/R6zJkHx6x7)
* 📧 **Email** - brightnodestudio@gmail.com
