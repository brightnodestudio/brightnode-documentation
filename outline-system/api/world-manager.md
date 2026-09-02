# World Manager API

The World Manager exposes an advanced API for direct Team and Global outline management.

{% hint style="info" %}
For standard gameplay integration, prefer the Outline Component's public API.
{% endhint %}

<figure><img src="../../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

## Apply

### ApplyTeamOutline

Applies a shared Team-scoped outline request.

### ApplyGlobalOutline

Applies a shared Global outline request.

## Remove

### RemoveTeamOutline

Removes a specific active Team outline request.

### RemoveGlobalOutline

Removes a specific active Global outline request.

## Getters

### GetTeamOutlineHandlesForActor

Returns active Team outline handles associated with the specified actor.

### GetGlobalOutlineHandlesForActor

Returns active Global outline handles associated with the specified actor.

### GetActiveGlobalOutlines

Returns the active Global outline runtime entries managed by the World Manager.

### GetActiveTeamOutlines

Returns the active Team outline runtime entries managed by the World Manager.

## Finders

### FindGlobalOutlineByActor

Finds an active Global outline associated with the specified actor.

### FindTeamOutlineByActor

Finds an active Team outline associated with the specified actor.
