# System Architecture

The Brightnode Dynamic Footstep System uses a component-based, data-driven architecture to separate footstep triggering, surface configuration and effect playback.

### Core Components

| Component                 | Responsibility                                     |
| ------------------------- | -------------------------------------------------- |
| Footstep System Component | Surface detection, event processing and networking |
| Footstep Profile          | Physical Material mapping and effect configuration |
| Footstep Event Data       | Audio, Niagara and decal variations                |
| Animation Modifier        | Automatic foot contact detection                   |
| Animation Notify          | Triggers footsteps from animations                 |

### Footstep Event Flow

Footsteps follow a consistent processing sequence:

1. A footstep is triggered by an Animation Notify or timer.
2. The component determines the movement type.
3. A surface trace identifies the Physical Material.
4. The assigned Footstep Profile resolves the appropriate event data.
5. A footstep request is constructed.
6. The event follows the appropriate local or network processing path.
7. Audio, Niagara effects and decals are played locally.

### Data-Driven Configuration

Surface-specific behaviour is stored in Footstep Profiles instead of individual character Blueprints.

This allows multiple characters to share the same settings or use different profiles.

For example, a player wearing boots and an AI character using lighter footwear can use separate profiles while sharing the same underlying component logic.

### Multiplayer Architecture

The system uses a server processing path and multicast events to distribute footsteps to other clients.

Each receiving client handles the final audio and visual playback locally.

See **Multiplayer Replication** for further details.
