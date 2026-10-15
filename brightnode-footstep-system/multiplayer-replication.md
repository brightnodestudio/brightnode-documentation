# Multiplayer Replication

The Brightnode Dynamic Footstep System includes multiplayer support using server processing and multicast footstep events.

Audio and visual effects are played locally on receiving clients rather than requiring each effect to be a replicated actor.

### How Replication Works

1. A character generates a footstep event.
2. The Footstep System constructs a footstep request.
3. The event is processed through the server path.
4. The server processes the request and associated gameplay noise.
5. A multicast distributes the event information.
6. Receiving clients process the event.
7. Footstep audio and effects are played locally.

### Footstep Request

The request contains information needed to reproduce a footstep.

| Data          | Purpose                                 |
| ------------- | --------------------------------------- |
| Surface Hit   | Surface detection information           |
| Movement Type | Walk, Run, Sprint, Crouch, Jump or Land |
| Location      | Footstep position                       |
| Rotation      | Effect orientation                      |
| Foot Side     | Left or Right                           |
| Random Index  | Audio or effect variation selection     |

### Remote Footsteps

The component supports remote footstep playback.

Remote events are processed separately from the locally controlled character's own feedback.

This helps avoid duplicate local playback.

### Distance Filtering

Remote footstep processing includes distance checks.

These checks allow the system to avoid unnecessary audio and visual playback for distant characters.

This is particularly useful for multiplayer games with large maps or multiple moving characters.

### AI Noise

The server processing path can generate AI noise events associated with footsteps.

This allows footstep events to contribute to AI hearing systems.

The response to these events depends on the AI perception and behaviour logic implemented by your project.

### Testing Multiplayer

For multiplayer testing, verify the following:

* The local player hears their footsteps.
* Other players hear the correct surface sounds.
* Remote effects spawn correctly.
* Local footsteps are not duplicated.
* Distance filtering behaves as expected.
* AI noise events are processed on the server.

**Important:** Temporary footstep audio, Niagara effects and decals are locally spawned effects. They are not persistent replicated world state for players joining later.
