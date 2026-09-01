# Best Practices

* Use the Outline Component as the normal gameplay-facing API.
* Create the Gameplay Tag before configuring a new preset.
* Assign every preset an appropriate unique Preset Tag.
* Register every usable preset in the active Outline Preset Library.
* Keep gameplay logic separate from BNOS runtime internals.
* Leave gaps between priority values.
* Store outline handles when a specific request must be removed later.
* Use Local visibility for genuinely player-specific information.
* Use Team and Global only when shared presentation is required.
* Use Component Tags for selective mesh outlining.
* Keep debug output disabled outside development.
* Test multiplayer features with multiple players and your intended server model.
