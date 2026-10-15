# First-Person & Movement Events

The Brightnode Dynamic Footstep System supports both animation-driven footsteps and timer-based movement events.

This allows the system to work with full-body characters and first-person setups that use arms-only animations.

### Full-Body Characters

Full-body characters typically use Animation Notifies.

Each notify is placed at the point where a foot makes contact with the ground.

The Footstep System then processes the event, detects the surface and plays the appropriate effects.

The included Animation Modifier can be used to generate these notifies automatically.

### First-Person Arms-Only Characters

Characters using arms-only animations may not have animated foot bones available for contact detection.

For these characters, the system supports timer-based footstep events.

The timer generates footsteps according to character movement rather than waiting for animation notifies.

#### Setup

1. Add the Footstep System component to your first-person character.
2. Assign a Footstep Profile.
3. Configure timer-based triggering.
4. Configure the movement intervals.
5. Test the character at different movement speeds.

### Movement Types

The system supports different movement-based effects.

| Movement | Behaviour                    |
| -------- | ---------------------------- |
| Walk     | Standard footstep timing     |
| Run      | Faster footsteps             |
| Sprint   | Increased footstep frequency |
| Crouch   | Slower, quieter footsteps    |
| Jump     | Dedicated jump event         |
| Land     | Dedicated landing event      |

Each movement type can use separate audio, Niagara and decal configurations.

### Jumping & Landing

Jump and landing events provide additional feedback beyond standard locomotion footsteps.

They can be configured to play dedicated sounds and spawn Niagara effects.

For example, landing on dirt can produce an impact sound and a small dust burst.

### Avoiding Duplicate Footsteps

Do not use both timer-based and animation-driven locomotion events for the same movement unless your implementation explicitly prevents duplicate triggering.

For characters with reliable foot contact animations, Animation Notifies are generally recommended.

For arms-only first-person characters, timer-based footsteps provide a practical alternative.
