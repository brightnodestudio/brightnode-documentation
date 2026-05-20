# Installation & Setup

## Adding to Your Project

1. Purchase and download the **Brightnode Attribute System** from the [Fab store](https://www.fab.com/sellers/Brightnode%20Studio)
2. Open the **Epic Games Launcher** and navigate to your **Fab Library**
3. Find the asset and click **Add to Project**, selecting your UE 5.5+project
4. Open your project - the system content will be available under the **BrightnodeSAS** content folder

---

## Plugin Requirements

The system requires the **Gameplay Tags** plugin which is built into Unreal Engine 5.5+and enabled by default. No additional plugins are needed.

To verify it is enabled:
1. Go to **Edit → Plugins**
2. Search for **Gameplay Tags**
3. Confirm it is checked as enabled

---

## Setting Up the Component

### Step 1 - Add the Component

Open your actor Blueprint and add **BP_AttributeComponent** as a component.

```
Components Panel → Add → Search "BP_AttributeComponent"
```

### Step 2 - Implement the Interface

In your actor Blueprint, implement the **BPI_AttributeSystem** interface.

```
Class Settings → Implemented Interfaces → Add → BPI_AttributeSystem
```

### Step 3 - Assign a Preset

Select the **BP_AttributeComponent** in your components panel and find the **Attribute Set Preset** property in the Details panel. Assign one of the included presets:

| Preset | Attributes |
|---|---|
| DA_Preset_Human | All 9 attributes |
| DA_Preset_Animal | Health, Stamina, Hunger, Hydration, Temperature |
| DA_Preset_Zombie | Health, Mania |

### Step 4 - Verify Setup

Press **Play** and open the debug widget by pressing **F3**. You should see all attributes from your assigned preset listed and actively updating.

---

## Multiplayer Setup

No additional multiplayer configuration is required. The component uses a full server authority model and replicates state automatically. Ensure your actor has **Replicates** enabled in its Class Defaults.

---

## Support

- 💬 **Discord** - [discord.gg/VSu4A7XxA7](https://discord.gg/VSu4A7XxA7)
- 📧 **Email** - brightnodestudio@gmail.com
