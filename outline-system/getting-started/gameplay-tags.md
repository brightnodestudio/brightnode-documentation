# Gameplay Tags

BNOS uses Gameplay Tags to identify Outline Presets and, when required, player teams.

## Outline Preset Tags

Every usable Outline Preset should have an appropriate Gameplay Tag.

Example:

```text
BNOS.Outline.Enemy
BNOS.Outline.Friendly
BNOS.Outline.Interactable
```

The tag must:

1. Exist in the project's Gameplay Tag configuration.
2. Be assigned to the preset's **Preset Tag**.
3. Belong to a preset registered in the active Outline Preset Library.

## Team Tags

Team Tags identify the player's team for Team-scoped outline visibility.

Example:

```text
BNOS.Team.Blue
BNOS.Team.Red
```

{% hint style="info" %}
Preset Tags and Team Tags serve different purposes. Preset Tags identify outline configurations. Team Tags identify players or teams for Team visibility.
{% endhint %}
