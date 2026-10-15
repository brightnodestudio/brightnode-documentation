# Troubleshooting

This page covers common issues when installing and configuring the Brightnode Dynamic Footstep System.

### Footsteps Are Not Playing

Check the following:

* The Footstep System component is attached to the character.
* A valid Footstep Profile is assigned.
* Animation Notifies or timer events are triggering.
* The detected Physical Material exists in the profile.
* The selected movement event contains valid audio.

### Incorrect Surface Sounds

If the wrong footstep sound plays:

1. Check the Physical Material assigned to the surface.
2. Confirm the surface trace hits the intended object.
3. Verify the Physical Material mapping in the Footstep Profile.
4. Check landscape layer configuration where applicable.

### Animation Modifier Is Not Generating Notifies

Verify that:

* The configured foot bone names are correct.
* Left and right foot assignments are valid.
* The Footstep Notify Class is assigned.
* The Speed Threshold is suitable for the animation.
* The modifier has been applied to the Animation Sequence.

### Duplicate Footsteps

Duplicate footsteps may occur if timer-based and animation-driven events are both active.

Check which system is generating your footsteps.

In multiplayer, also verify that the local character is not replaying its own footsteps through remote processing.

### Footprint Decals Have Incorrect Rotation

Check the footprint decal material, decal orientation and foot-side configuration.

Test the decals on a flat surface before introducing complex geometry.

### Niagara Effects Are Missing

Verify that:

* The Niagara system is assigned.
* The selected movement event supports the effect.
* The footstep event is being generated.
* The effect is spawning at a valid location and orientation.

### Remote Players Cannot Hear Footsteps

Check the following:

1. Remote footstep playback is enabled.
2. The event reaches the server processing path.
3. The multicast is received.
4. The receiving player is within the configured distance.
5. Audio attenuation does not prevent playback.

### Plugin Fails to Load

The plugin contains C++ functionality and requires a build compatible with your Unreal Engine version.

If you receive a module or plugin version error, ensure that the correct plugin build has been installed.

When switching engine versions, you may need to compile the plugin for the new engine version.

### Still Need Help?

If you are still experiencing an issue, contact Brightnode Studio through Discord or email.

When requesting support, include:

* Unreal Engine version
* Plugin version
* Description of the issue
* Relevant Blueprint screenshots
* Any error messages
