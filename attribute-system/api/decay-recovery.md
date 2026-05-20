# Decay & Recovery Control

Functions for pausing, resuming, and adjusting decay and recovery at runtime on **BP_AttributeComponent**. All functions are multiplayer safe.

---

## Decay Control

### PauseDecay
Pauses decay for a specific attribute. The attribute value will stop changing automatically until decay is resumed.

```
PauseDecay (AttributeTag: GameplayTag)
```

**Example use:** Pausing Tiredness decay inside a BP_RestZone so the attribute stops building while the player rests.

---

### ResumeDecay
Resumes decay for a specific attribute that was previously paused.

```
ResumeDecay (AttributeTag: GameplayTag)
```

**Example use:** Resuming Tiredness decay when the player leaves a BP_RestZone.

---

### PauseAllDecay
Pauses decay for every attribute on this component simultaneously.

```
PauseAllDecay ()
```

**Example use:** Pausing all attribute decay during a cutscene, menu, or loading screen.

---

### ResumeAllDecay
Resumes decay for every attribute on this component simultaneously.

```
ResumeAllDecay ()
```

**Example use:** Resuming all attribute decay when a cutscene or menu closes.

---

### SetDecayRate
Dynamically changes the decay rate for a specific attribute at runtime. Overrides the DataTable value for the duration of the session or until changed again.

```
SetDecayRate (AttributeTag: GameplayTag, NewRate: float)
```

**Example use:** A modifier that accelerates Hunger decay rate under stress - call SetDecayRate with a higher value when the modifier is applied and restore it when the modifier is removed.

---

### SetDriftTarget
Sets the drift target value for a drifting attribute. Typically called by zone actors when the player enters or exits.

```
SetDriftTarget (AttributeTag: GameplayTag, TargetValue: float)
```

**Example use:** A BP_TemperatureZone sets the drift target to 10.0 on player enter and restores it to the neutral value on player exit.

---

## Recovery Control

### PauseRecovery
Pauses recovery for a specific attribute. The attribute will stop recovering automatically until resumed.

```
PauseRecovery (AttributeTag: GameplayTag)
```

**Example use:** Pausing Mania recovery inside a BP_DarknessZone so the attribute cannot recover while the player is in the dark.

---

### ResumeRecovery
Resumes recovery for a specific attribute that was previously paused.

```
ResumeRecovery (AttributeTag: GameplayTag)
```

**Example use:** Resuming Mania recovery when the player exits a BP_DarknessZone and enters light.

---

## Decay vs Recovery - Key Distinction

| | Decay | Recovery |
|---|---|---|
| **What it controls** | How the attribute changes automatically over time | How the attribute restores when below max |
| **BuildsUp attributes** | Causes value to increase (Mania, Tiredness build up) | Causes value to decrease back toward zero |
| **Can be blocked by** | Nothing - pause/resume only | Active fatigue source modifiers |
| **Pause scope** | Per attribute or all at once | Per attribute only |
