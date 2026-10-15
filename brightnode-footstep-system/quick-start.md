# Quick Start

Get your first surface-aware footsteps working in a few simple steps.

### Step 1. Add the Component

Open your Character Blueprint and add the Brightnode Footstep System component.

Assign a valid Footstep Profile in the component's Details panel.

### Step 2. Configure a Surface

Open your Footstep Profile and add an entry for a Physical Material.

For example:

| Setting           | Example            |
| ----------------- | ------------------ |
| Physical Material | PM\_Concrete       |
| Movement          | Walk               |
| Sound             | Concrete Footstep  |
| Niagara           | Concrete Dust      |
| Decal             | Concrete Footprint |

Audio and visual effects are optional. You only need to configure the effects you want to use.

### Step 3. Assign the Physical Material

Open the material used by your test floor and assign the same Physical Material configured in the profile.

Ensure the floor has collision enabled and can be detected by the footstep surface trace.

### Step 4. Trigger Footsteps

Choose the appropriate triggering method.

**Full-Body Characters**

Use the included Animation Modifier to generate footstep notifies or manually place the supported notifies in your locomotion animations.

**First-Person Characters**

Enable and configure timer-based footsteps for characters without usable foot animation data.

### Step 5. Test

1. Place your character on the configured surface.
2. Start Play in Editor.
3. Move the character.
4. Confirm that the correct footstep sound plays.
5. Test any configured particles or decals.

### Next Steps

Once your first surface is working, you can:

* Add additional Physical Materials.
* Configure walking, running and crouching variations.
* Enable Niagara effects and footprint decals.
* Configure multiplayer playback.
* Add AI noise events.

See the following guides for more detailed configuration.
