# Architecture Overview

BNOS separates gameplay requests from outline presentation.

```text
Gameplay Logic
      ↓
Outline Component
      ↓
Preset / Visibility Resolution
      ↓
Local Processing or World Manager
      ↓
Outline Presentation
```

The main runtime pieces are the **Outline Component**, **World Manager**, **Outline Preset Library**, and **Outline Presets**.

For normal gameplay, the Outline Component should be treated as the primary public entry point.
