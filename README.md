# FFXI Addon — voidwatchpulsecell

> [!NOTE]
> **Quick Reference**
> - **Path:** `C:\Windower\addons\voidwatchpulsecell\`
> - **Author / Version:** Mojo / `1.20150930` (local variant of `voidwatch`)
> - **Commands:** `//vw`
> - **Load Status:** On-Demand
> - **Origin:** Custom / Modified variant of `voidwatch`

Modified duplicate of `voidwatch` with the 7 Pulse weapon IDs uncommented so the Riftworn Pyxis handler automatically claims Pulse weapons instead of converting/discarding them.

## What the Code Does
- **Exact Diff vs. `C:\Windower\addons\voidwatch\voidwatch.lua`:**
  - Lines 39–45 uncomment `pulse_items`:
    - `[18457] = 'Murasamemaru'`
    - `[18542] = 'Aytanri'`
    - `[18904] = 'Ephemeron'`
    - `[19144] = 'Coruscanti'`
    - `[19145] = 'Asteria'`
    - `[19174] = 'Borealis'`
    - `[19794] = 'Delphinius'`
  - All other logic (including `cells` for `Cobalt Cell`, `Rubicund Cell`, `Phase Displacer` and `math.sqrt(mob.distance) < 6` in `get_mob_by_name`) is identical to the local `voidwatch\voidwatch.lua`.
- **Pulse Item Claiming Behavior:** When `examine_box` scans the 8 `Menu Parameters` slots in `0x034`, finding any `pulse_items[item]` sets `choice.option = i` and `choice.item = item`. When `obtain_item` rewrites outgoing `0x05B`, `pulse_items[choice.item]` sets `p['_unknown1'] = 1` (claiming the specific Pulse weapon rather than using option `9`/`10` with `_unknown1 = 0`).

## Commands & Usage
- `//vw start` — Start automated Voidwatch cell trading, popping (if leader), and Pyxis looting (prioritizing Pulse weapons).
- `//vw stop` — Stop the automation loop.

## Events, Packets & Technical Hooks
- **Windower Events:** `addon command`, `incoming chunk`, `outgoing chunk`.
- **Packets:** Outgoing `0x01A`, `0x036`, `0x05B`; incoming `0x0E`, `0x38`, `0x34`, `0x36` (same as `voidwatch`).
- **Dependencies / Libraries:** `logger`, `coroutine`, `packets`, `resources`.

## Local Settings & Customizations
No `data/settings.xml`. Shares the same `_addon.name = 'voidwatch'` and `//vw` command as `voidwatch` (so only one of the two should be loaded at a time).

## Related Notes
- `FFXI Windower Overview`
- `FFXI Windower Addons Catalog`
- `FFXI Addon — voidwatch`
