# Common Issues - Perk System

## Perk Machine Does Nothing When Interacting

**Cause:** Interaction not set up correctly.

**Fix:**

- Ensure your character is calling Interact
- Confirm your trace is hitting the perk machine
- Verify the machine uses `BPI_PerkInteraction`
- Add a Print String on interact to confirm it fires

## Cannot Purchase Perk

**Cause:** Currency interface not implemented or failing.

**Fix:**

- Ensure your character implements `BPI_CurrencyAccess`
- Confirm all interface functions are filled in
- If using the showcase component, ensure `BPC_CurrencyShowcase` is added to the character

## Perk is Purchased but No Effect Happens

**Cause:** Perk events not bound or logic not implemented.

**Fix:**

- Ensure you have bound `OnPerkAdded` and `OnPerkRemoved`
- Confirm your events are Run On Server
- Add a Print String inside your event to verify it fires

## Perk Icons Not Appearing in UI

**Cause:** HUD or Perk Bar not initialized.

**Fix:**

- Ensure `WBP_HUD` is added to the viewport on Begin Play
- Confirm `WBP_PerkBar` is inside the HUD and Initialize is called on the Perk Bar
- Check anchor is set to bottom center with alignment (0.5, 0.5)

## Drink Animation Does Not Play

**Cause:** Missing socket, montage, or AnimBP setup.

**Fix:**

- Ensure socket `s_item_l` exists on `hand_l`
- Confirm montage is assigned in the Perk Component
- Verify AnimBP includes an Arms slot
- Ensure character is using Manny mesh and `ABP_Manny`

## Drink Animation Looks Broken or Misaligned

**Cause:** Skeleton mismatch or incorrect setup.

**Fix:**

- Replace the showcase skeleton with the Third Person skeleton
- Ensure animation is using the correct skeleton
- Recheck socket transform on `hand_l`

## Perk Machine Visuals Not Updating

**Cause:** Construction script not refreshed.

**Fix:** Select the perk machine in the level and click **Rerun Construction Script**.

## Perk Machine is Not Powered

**Cause:** Power system not configured.

**Fix:**

- Ensure machine has Requires Power = true
- Ensure Turned On At Spawn = false
- Assign the machine to the power switch
- Confirm power switch is calling interact correctly

## Clients Not Seeing Correct Behaviour

**Cause:** Replication setup incomplete.

**Fix:**

- Ensure character replicates
- Ensure Perk Component replicates
- Apply gameplay logic on the server
- Use replicated variables or events to update clients

## Debug Tip

If something is not working, check these three things first:

1. Is the interaction firing?
2. Is the logic running on the server?
3. Is the result being replicated or sent to the client?

## Bug Reports

Report bugs in the Brightnode Studio Discord in the **#bugs-perk-system** channel.

💬 [discord.gg/VSu4A7XxA7](https://discord.gg/VSu4A7XxA7)
