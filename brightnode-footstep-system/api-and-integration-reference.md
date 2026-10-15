# API & Integration Reference

This page covers the main implementation functions and structures used by the Brightnode Dynamic Footstep System.

The system is designed around a reusable Footstep Component, Data Assets and footstep event requests.

### ExecuteFootstep

`ExecuteFootstep`

The primary footstep processing function.

It gathers the relevant event information, including the detected surface, movement type, location, rotation and foot side.

The function constructs the footstep request and sends it through the appropriate processing path.

### ProcessRemoteFootstep

`ProcessRemoteFootstep`

Processes received remote footstep events.

The function checks the remote playback configuration and distance requirements before playing the appropriate sounds and effects.

### Animation Modifier

`UAutoGenerateFootstepNotifies`

The C++ Animation Modifier responsible for automatically generating footstep notifies.

#### Configuration

| Property            | Description                      |
| ------------------- | -------------------------------- |
| SampleRate          | Animation sampling frequency     |
| SpeedThreshold      | Contact detection threshold      |
| FootstepNotifyClass | Notify class to generate         |
| Feet                | Configured foot bone definitions |

### Foot Definition Structure

`FBNFSFootDefinition`

| Property     | Description           |
| ------------ | --------------------- |
| FootBoneName | Bone name to evaluate |
| FootSide     | Associated foot side  |

### Foot Side Enumeration

`EBNFSFootSide`

Available values:

* None
* Left
* Right

### Integration Examples

**Equipment Systems**

Use different Footstep Profiles for different footwear or equipment.

**Custom Movement Systems**

Supply the appropriate movement type when generating footsteps.

**AI Systems**

Use server-processed footstep noise events with your AI hearing behaviour.

**Environmental Systems**

Configure Physical Materials to support different floor, mesh and landscape surfaces.

**Note:** Exact Blueprint-callable function signatures and component property names should be checked against the final plugin release.
