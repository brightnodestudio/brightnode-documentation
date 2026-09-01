# Outline Presets

Outline Presets keep visual and runtime outline configuration out of gameplay Blueprints.

A preset contains six main groups:

| Category | Purpose |
| --- | --- |
| Identity | Preset Tag and Visibility Mode |
| Lifetime | Optional automatic expiry |
| Priority | Resolves competing requests |
| Outline Visuals | Colour and thickness |
| Mesh Selection | Chooses affected mesh components |
| Flashing | Controls flashing behaviour |

Gameplay systems decide **when** an outline should be requested. The preset decides **how** that outline should behave.
