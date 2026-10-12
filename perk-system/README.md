# Brightnode Perk System

**Version 1.0.0 | Unreal Engine 5.5+ | Pure Blueprint**

The **Brightnode Perk System (BNPS)** is a modular, data-driven perk framework for Unreal Engine 5, designed for both single-player and multiplayer projects.

Inspired by classic Zombies-style perk machines, BNPS allows players to purchase, consume, and manage gameplay perks through fully customisable machines. Each perk is configured using a dedicated Data Asset, while the system handles purchasing, ownership, drinking animations, audiovisual feedback, and multiplayer replication.

Built with flexibility in mind, BNPS can operate independently or integrate with existing gameplay systems, including the Brightnode Interaction, Attribute, and Outline Systems.

### Key Features

* **100% Blueprint:** No C++ required.
* **Multiplayer Ready:** Server-authoritative gameplay with replicated perk functionality.
* **Data-Driven Perks:** Create and configure perks using `PDA_PerkDefinition` Data Assets.
* **Customisable Perk Machines:** Create unique machines using child Blueprints and configurable presentation settings.
* **Purchase & Currency Support:** Integrate your own currency system through interfaces or use the included showcase implementation.
* **Drinking Animations:** Configurable drink meshes, attachment sockets, animations, and audio feedback.
* **Optional Power System:** Control machine availability through a power switch mechanic.
* **Perk UI:** Display acquired perks using the included `WBP_PerkBar` widget.
* **Modular Integration:** Connect perks to custom attributes, abilities, interactions, or other gameplay systems.

### How It Works

The system is built around three primary elements:

#### 1. Perk Definitions

Each perk is configured through a `PDA_PerkDefinition` Data Asset, allowing you to define its gameplay and presentation properties without creating an entirely new system for every perk.

#### 2. Perk Machines

Perk machines provide the in-world purchasing experience. Each machine can be configured to offer a specific perk, with custom visuals, sounds, and drinking presentation.

Child Blueprints allow you to create multiple machine designs while sharing the underlying functionality.

#### 3. Player Perks

When a player successfully purchases a perk, the system manages the acquisition process and allows the perk's associated gameplay functionality to be applied.

This keeps the perk framework separate from the gameplay effects themselves, allowing it to work alongside your existing character, attribute, and ability systems.

### Requirements

| Requirement      | Detail                     |
| ---------------- | -------------------------- |
| Engine Version   | Unreal Engine 5.5+         |
| Implementation   | 100% Blueprint             |
| Plugins Required | Common UI (built into UE5) |
| Multiplayer      | Supported                  |
| Project Type     | Blueprint or C++           |

### Documentation

If you're new to BNPS, we recommend following the documentation in this order:

1. **Installation & Setup:** Add the system to your project and configure the required components.
2. **Quick Start:** Set up your first working perk machine.
3. **Creating Perks:** Configure custom perk definitions and gameplay effects.
4. **Configuring Perk Machines:** Customise machine behaviour and presentation.
5. **Integrations:** Connect BNPS with other Brightnode products or your existing gameplay systems.

### Support

* 💬 [**Discord**](https://discord.gg/R6zJkHx6x7)
* 📧 **Email** - brightnodestudio@gmail.com
* 🛒 [**Fab Store**](https://fab.com/listings/6a0214f9-1c4a-4c40-bb96-bbbe5008c491)
