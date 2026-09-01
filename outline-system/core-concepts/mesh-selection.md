# Mesh Selection

Actors can contain multiple mesh components. BNOS can select which components receive an outline.

## Mesh Selection Mode

Determines how the system chooses mesh components on the target actor.

## Required Mesh Tags

When using tag-based mesh selection, **Required Mesh Tags** identifies the mesh components that should be affected.

These are **Component Tags**, not the Gameplay Tags used for preset identity or teams.

## Example

An actor might contain:

```text
Character Mesh
Weapon Mesh
Backpack Mesh
Interaction Mesh
```

Component Tags allow a preset to target only the meshes relevant to that outline.
