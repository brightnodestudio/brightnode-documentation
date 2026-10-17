# Audio, Niagara & Decals

The Brightnode Dynamic Footstep System supports configurable audio, particle effects and footprint decals for each surface and movement type.

Effects are configured through Footstep Profiles.

### Audio

Each movement event can contain multiple audio variations.

When a footstep is processed, the system selects the configured audio variation for the detected surface and movement type.

This helps prevent repetitive footstep playback.

#### MetaSounds

MetaSounds can be used for additional audio control and variation.

Depending on the MetaSound setup, this can include random sample selection, pitch variation and layered audio.

Audio behaviour such as attenuation and concurrency should be configured in the relevant Unreal Engine audio assets.

### Niagara Effects

Niagara effects provide visual feedback when characters interact with different surfaces.

Example effects include:

* Dust on dirt
* Debris on gravel
* Sand displacement
* Snow particles
* Water splashes
* Landing dust

Assign the desired Niagara systems to the appropriate surface and movement configurations.

### Footprint Decals

The system supports left and right footprint decals.

These can be used to display footprints on surfaces such as concrete, sand and dirt, these are configured per material inside the data asset preset.

Each footstep event includes foot-side information so that the corresponding footprint can be selected.

#### Decal Configuration

Footprint behaviour includes:

* Left and right decal selection
* Footstep location and rotation
* Decal lifetime
* Fading behaviour

Ensure that footprint textures and materials are orientated correctly for your character setup.

### Performance

When using particle effects and decals with multiple characters, consider the overall rendering cost.

Recommended practices include:

* Use lightweight Niagara systems.
* Avoid unnecessarily large particle bursts.
* Configure sensible decal lifetimes.
* Limit remote effect processing by distance.
* Test performance with several moving characters.
