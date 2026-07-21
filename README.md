# HHKB Ergo

An ergonomic SpaceFN layout for HHKB designed to reduce pinky strain and wrist fatigue.

[한국어 문서](./README.ko.md)

HHKB Ergo was created for a specific ergonomic problem: repeatedly reaching with the right pinky and bending the right wrist outward was causing discomfort and fatigue. This layout moves frequently used navigation, editing, symbol, media, and function actions to a SpaceFN layer operated with the left thumb, reducing right-hand movement and load.

This Karabiner-Elements complex modification turns the HHKB `Space` key into two behaviors:

- Tap `Space` for a normal space.
- Hold `Space` for 50 ms or longer to activate SpaceFN.

The configuration also includes rollover-safe handling so a fast `Space` + key sequence preserves both the space and the following key when the sequence is intended as normal typing.

## Space behavior

| Input | Behavior |
| --- | --- |
| Tap `Space` alone within 500 ms | Normal `Space` |
| Press another key within 50 ms of `Space` | Normal `Space` + key input |
| Hold `Space` for 50 ms or longer | Activate the SpaceFN layer |
| Press a mapped key while the layer is active | Run the SpaceFN action |
| Release `Space` | Clear the SpaceFN layer |
| `Ctrl + Space` | Pass through to macOS for input-source switching |

If the target key arrives before the 50 ms threshold, the SpaceFN attempt is canceled and the delayed action restores a normal space. For reliable SpaceFN chords, press `Space` first and hold it briefly before pressing the target key.

> Holding `Space` alone for more than 500 ms does not emit a space. For a SpaceFN chord, hold `Space` for roughly 50 ms before pressing the target key.

## Layout map

The table below lists every SpaceFN mapping as `[physical key / output]`. Keys not listed have no SpaceFN mapping.

| Physical key | SpaceFN output | Purpose |
| --- | --- | --- |
| `1`–`0` | `F1`–`F10` | Function keys |
| `-` / `=` | `F11` / `F12` | Function keys |
| `W` / `E` | `[` / `]` | Brackets |
| `R` / `T` | `'` / `/` | Quotes and slash |
| `Y` / `H` | Page Up / Page Down | Page navigation |
| `U` / `O` | Home / End | Line navigation |
| `I` / `J` / `K` / `L` | ↑ / ← / ↓ / → | Cursor movement |
| `A` / `S` / `D` | Volume down / volume up / mute | Media |
| `F` | Escape | Editing |
| `G` | `;` | Symbol |
| `M` | Backspace | Editing |
| `,` | Forward Delete | Editing |
| `.` | Enter | Editing |
| `X` / `C` | `-` / `=` | Symbols |
| `V` | Backslash | Symbol |
| `B` | Backtick in ABC; `₩` in Korean input | Symbol |
| `N` | `?` | Symbol |

### Navigation and editing

| Combination | Action |
| --- | --- |
| `Space + I/J/K/L` | ↑ / ← / ↓ / → |
| `Space + U/O` | Home / End |
| `Space + Y/H` | Page Up / Page Down |
| `Space + M` | Backspace |
| `Space + ,` | Forward Delete |
| `Space + .` | Enter |
| `Space + F` | Escape |

### Symbols

| Combination | Output | With Shift held first |
| --- | --- | --- |
| `Space + W/E` | `[` / `]` | `{` / `}` |
| `Space + R` | `'` | `"` |
| `Space + T` | `/` | `?` |
| `Space + G` | `;` | `:` |
| `Space + X` | `-` | `_` |
| `Space + C` | `=` | `+` |
| `Space + V` | Backslash | `|` |
| `Space + B` | Backtick in ABC; `₩` in Korean input | Input-source dependent |
| `Space + N` | `?` | — |

For shifted symbols, press `Shift` first, hold `Space` for about 50 ms, and then press the target key.

### Media and function keys

| Combination | Action |
| --- | --- |
| `Space + A/S/D` | Volume down / volume up / mute |
| `Space + 1~0` | F1~F10 |
| `Space + -` | F11 |
| `Space + =` | F12 |

For normal typing, press `Space` and the next A/S/D key within 50 ms. For media actions, hold `Space` for at least 50 ms before pressing A/S/D.

`Ctrl + Space` is excluded from the SpaceFN controller, so it is passed to macOS unchanged for input-source switching.

## Timing

The following two values in [`hhkb_spacefn_final.json`](./hhkb_spacefn_final.json) must always be kept identical:

```json
"basic.to_if_held_down_threshold_milliseconds": 50,
"basic.to_delayed_action_delay_milliseconds": 50
```

- The current 50 ms value is an experimental fast-response setting.
- If SpaceFN activates accidentally during normal typing, raise both values together to `75`, `100`, `120`, or `150`.
- If 50 ms causes too many false activations, return to the previously tested 75 ms setting.
- The standalone Space timeout is `basic.to_if_alone_timeout_milliseconds: 500`.

## Implementation and device scope

- Device condition: vendor ID `1278` (`0x04FE`), product ID `33` (`0x0021`)
- SpaceFN state variable: `hhkb_spacefn`
- One rule with 38 manipulators: one layer controller plus 37 function and symbol mappings
- Holding `Space` for 50 ms sets `hhkb_spacefn = 1`; releasing it resets the variable through `key_up_value`
- A key arriving before 50 ms triggers `to_delayed_action.to_if_canceled`, which restores a normal space
- Mappings preserve additional modifiers, allowing shifted symbols and navigation modifiers
- Device conditions and the state variable keep the mappings limited to the HHKB

The `key_up_value` behavior requires Karabiner-Elements 14.12.6 or later.

If the keyboard is not detected, use Karabiner-EventViewer to check its vendor and product IDs, then update the device condition in [`hhkb_spacefn_final.json`](./hhkb_spacefn_final.json).

## Installation

Copy the configuration into Karabiner-Elements' complex-modifications directory:

```bash
cp hhkb_spacefn_final.json ~/.config/karabiner/assets/complex_modifications/
```

Then open Karabiner-Elements, go to **Complex Modifications**, and enable the HHKB Ergo rule.

## Files

- [`hhkb_spacefn_final.json`](./hhkb_spacefn_final.json): Karabiner-Elements complex modification
- [`README.ko.md`](./README.ko.md): Korean documentation
