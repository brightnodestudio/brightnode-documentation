# Footstep Profiles & Surface Detection

Footstep Profiles define how the system responds to different surfaces and movement types.

Each profile contains a mapping between Physical Materials and their corresponding Footstep Event Data.

### Creating a Footstep Profile

1. Open the Content Browser.
2. Create a new Data Asset using the supplied Footstep Profile class.
3. Give it a descriptive name.
4. Open the asset and configure the surface entries.
5. Assign the profile to your Footstep System component.

An example naming convention is `DA_BNFS_DefaultProfile`.

### Surface Configuration

Each surface entry maps a Physical Material to its audio and visual effects.

Example surfaces:

| Surface  | Physical Material |
| -------- | ----------------- |
| Concrete | PM\_Concrete      |
| Dirt     | PM\_Dirt          |
| Grass    | PM\_Grass         |
| Gravel   | PM\_Gravel        |
| Metal    | PM\_Metal         |
| Sand     | PM\_Sand          |
| Snow     | PM\_Snow          |
| Water    | PM\_Water         |
| Wood     | PM\_Wood          |

These are example asset names. You can use your own Physical Materials.

### Movement Event Data

Each surface can define separate effects for different movement types.

| Movement | Configuration             |
| -------- | ------------------------- |
| Walk     | Standard footsteps        |
| Run      | Running footsteps         |
| Sprint   | Faster, heavier footsteps |
| Crouch   | Quieter footsteps         |
| Jump     | Jump effects              |
| Land     | Landing effects           |

Each movement configuration can contain multiple sounds, Niagara systems and footprint decals.

### Surface Detection

When a footstep occurs, the system performs a surface trace and retrieves the Physical Material from the hit result.

The detected Physical Material is then used to find the corresponding Footstep Profile entry.

If no matching entry is found, the system cannot resolve surface-specific event data from that mapping.

### Static Meshes

Assign the appropriate Physical Material to the material used by your Static Mesh.

Ensure that collision is configured to respond to the system's trace.

### Landscapes

For landscapes, configure Physical Materials through the landscape material's layer setup.

For example:

* Grass Layer: PM\_Grass
* Dirt Layer: PM\_Dirt
* Rock Layer: PM\_Rock

This allows different painted terrain layers to produce different footsteps.

**Tip:** Test Physical Material detection on a simple Static Mesh before configuring more complex landscape materials.

### Reusing Profiles

Profiles can be shared between characters or swapped to change footstep behaviour.

This is useful for different footwear, character types and custom movement systems.
