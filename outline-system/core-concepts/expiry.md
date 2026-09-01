# Expiry

Outline Presets can remove themselves automatically after a configured duration.

## Has Expiry

Enable **Has Expiry** when the request should be temporary.

## Expiry Duration

Defines how long the request remains active, in seconds.

Example:

```text
Has Expiry = True
Expiry Duration = 5.0
```

Expiry is useful for temporary detection, scans, alerts, and other effects that should not require gameplay logic to manually schedule removal.
