# Installation & Setup

This guide covers installing the Brightnode Dynamic Footstep System and preparing your project for surface-aware footsteps.

### 1. Install the Plugin

1. Install the Brightnode Dynamic Footstep System using Fab or copy the compatible plugin into your project's `Plugins` folder.
2. Open your Unreal Engine project.
3. Navigate to **Edit > Plugins**.
4. Search for **Brightnode Footstep System**.
5. Enable the plugin and restart the editor if required.

The system contains a C++ Animation Modifier but is designed for use in Blueprint projects. A compatible precompiled plugin build can be used without converting your Blueprint gameplay project to C++.

### 2. Enable Plugin Content

1. Open the Content Browser.
2. Open the Content Browser settings.
3. Enable **Show Plugin Content**.
4. Locate the Brightnode Footstep System content folder.

This allows you to access the supplied Blueprints, data assets and example content.

### 3. Add the Footstep Component

1. Open your Character Blueprint.
2. Select **Add Component**.
3. Add the Brightnode Footstep System component.
4. Assign a Footstep Profile.
5. Compile and save.

The component handles surface detection, event processing, sounds, effects and networking.

### 4. Configure Physical Materials

The system uses Physical Materials to identify the surface beneath a character.

1. Create or open a Physical Material.
2. Assign it to the appropriate material or landscape layer.
3. Add the Physical Material to your Footstep Profile.
4. Configure the sounds and effects for that surface.

**Important:** The ground must have appropriate collision and return a valid Physical Material for surface-specific footsteps to work correctly.

### 5. Choose a Footstep Method

The system supports two primary footstep triggering methods.

| Method                | Recommended Use                   |
| --------------------- | --------------------------------- |
| Animation Notifies    | Full-body character animations    |
| Timer-Based Footsteps | First-person arms-only characters |

For full-body characters, configure the supplied Animation Modifier or add the relevant notifies manually.

For arms-only characters, configure timer-based footstep triggering.

### 6. Verify Installation

Start Play in Editor and test your character on a configured surface.

Confirm that footsteps trigger, the correct sound is selected and the configured effects appear.

If no footsteps are produced, see the Troubleshooting section.
