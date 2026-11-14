# Typology Tray Review View (Card Deck & Masonry Grid)

> **Subproject:** Visual Sorting & Typology Studio  
> **Section:** 04 — UI / UX Interaction Design  
> **Status:** Production Reference  

---

## 1. Concept: Rapid Verification at Inspection Speed

Once clusters are generated, the archaeologist switches to the **Typology Tray Review View** to inspect and validate each group at maximum speed:

```
+---------------------------------------------------------------------------------------------------+
|  [< Previous Tray]   TRAY 4: Red Burnished Bowls (48 items)   [Next Tray >]    [Auto-Route: ON]   |
+---------------------------------------------------------------------------------------------------+
|  [ Sherd 01 ]   [ Sherd 02 ]   [ Sherd 03 ]   [ Sherd 04 ]   [ Sherd 05 ]   [ Sherd 06 ]          |
|    Locus 12       Locus 14       Locus 12       Locus 18       Locus 12       Locus 14            |
|   [✓ Verified]   [✓ Verified]   [✓ Verified]   [✓ Verified]   [✓ Verified]   [✓ Verified]         |
|                                                                                                   |
|  [ Sherd 07 ]   [ Sherd 08 ]   [ Sherd 09 (MISFIT!) ]       [ Sherd 10 ]   [ Sherd 11 ]          |
|    Locus 12       Locus 14       Locus 22 (Cooking Pot)       Locus 14       Locus 12             |
|   [✓ Verified]   [✓ Verified]   [Press 'X' to Eject]        [✓ Verified]   [✓ Verified]         |
+---------------------------------------------------------------------------------------------------+
|  SHORTCUTS: [Space] = Confirm Tray | [X] = Reject Item | [M] = Move to Tray... | [N] = New Type   |
+---------------------------------------------------------------------------------------------------+
```

---

## 2. Keyboard-First Ergonomics for Sorting Velocity

Field archaeologists must review thousands of images. Requiring multiple mouse clicks per photo creates repetitive strain and slows sorting to a crawl. The review view is **strictly keyboard-first**:

* **`Arrow Keys` (`←` / `→` / `↑` / `↓`):** Navigate cursor through artifact cards.
* **`X` or `Delete`:** Immediately eject current item from the tray.
  - The card animates upward with a subtle red highlight.
  - The next-best candidate tray displays in a pill popover (e.g., *"Suggested: Tray 7 [Enter to confirm]"*).
* **`Space`:** Marks the active card (or entire tray) as **Human-Verified**.
* **`M`:** Opens quick-jump modal to move the item to any other existing tray via number.
* **`N`:** Spawns a brand-new typological tray seeded with this item.
* **`Z` (`Ctrl+Z`):** Instant undo for any accidental ejection.

### Verification Benchmark
Using keyboard-first masonry review, experienced specialists achieve an empirical review speed of **1.5 to 2.5 seconds per artifact**, allowing a complete batch of 1,000 photos to be fully validated in under 35 minutes.
