# Visibility Modes

BNOS supports Local, Team, and Global outline visibility.

## Local

Visible only to the relevant player.

Typical uses include interaction highlighting, selection, personal objectives, and player-specific detection.

## Team

Shared with eligible players on the appropriate team.

Team visibility uses the player's configured Team Tag.

Typical uses include squad information, shared detection, and team objectives.

## Global

Shared globally with eligible players.

Typical uses include world objectives, global events, and server-driven target highlighting.

{% hint style="info" %}
For normal gameplay, use the Outline Component's `ApplyOutline` function. The preset's Visibility Mode determines the appropriate processing path.
{% endhint %}
