# Outline Component

The Outline Component lives on the player and provides the primary gameplay-facing API.

It handles player-specific outline processing and configuration, including:

* Applying and removing requests
* Player-visible outline queries
* Team identity
* Through-wall behaviour
* Active camera configuration
* Flash processing
* Debug output

## Exposed Configuration

| Setting | Purpose |
| --- | --- |
| Outline Post Process Material | Material used to render the outline effect |
| Through Wall Outlines Enabled | Default through-wall behaviour |
| Auto Initialize | Automatically initializes at play start |
| Team Tag | Identifies the player's team |
| Flash Tick Rate | Flash processing interval |
| Show Debug | Enables component debug output |
