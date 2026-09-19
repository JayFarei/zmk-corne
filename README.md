# Corne wireless — JayFarei

42-key Corne with nice!nano v2 controllers. ZMK and its build workflow are pinned to v0.3.0. The left half is the central: it connects to the computer, while the right half connects wirelessly to the left.

## Layout

Ported from the saved VIA layout in `JayFarei/dotfiles`, `_Resources/keybs/corne/via config/crkbd.layout.json` (2026-09-19), using the QMK Corne matrix coordinates to reorder all 42 physical keys correctly.

- Base: QWERTY with home-row modifiers on A/S/D/F and J/K/L/semicolon.
- Thumbs, left to right: Command, Lower, Enter; Backspace, Space/Symbols, Shift+Alt.
- Lower: numbers, Control+1–5 shortcuts, arrows, media, volume, Shift+Tab, and Command+[ / Command+].
- Symbols: symbols and F1–F10, plus the saved shortcut macros.
- Tap/hold threshold: 300 ms, tap-preferred, with a 300 ms quick-tap window for repeated letters/Space.

VIA's mixed left/right modifier expressions on J/K/semicolon encode right Control/Shift/Command in QMK, so the port uses those right modifiers. L remains left Alt. Grave/Escape retains held Shift/Command modifiers. VIA macro 0 contains uppercase `G`, so it emits Command+Control+Shift+G; macro 12 emits Command+Alt+Shift+9. Macros are taps, not held/repeating shortcuts. Host input layout: U.S.

## Wireless controls

Hold **Lower (left middle thumb) + Z** to access settings, then press:

| Base position | Action |
| --- | --- |
| Q / W / E / R / T | Select Bluetooth profile 1 / 2 / 3 / 4 / 5 |
| A | Clear the selected profile's host pairing |
| S | Prefer USB output |
| D | Prefer Bluetooth output |
| F / G | Previous / next Bluetooth profile |
| B | Enter bootloader on the central half |

Release Z and Lower to return. Select an unused profile before pairing a new host. Only the left half pairs with the computer. Both halves must have their battery switches on for cable-free use. Sleep starts after 15 minutes of inactivity; a key wakes the keyboard.

## Adaptations

- The previously unused Lower+Z position now accesses settings.
- The old fourth VIA layer was unreachable from the saved normal layers; it is replaced with the momentary wireless settings layer.
- Lower+X/C RGB controls are inactive because LED hardware has not been verified. Display and RGB are disabled.
- Lower+Space's QMK mouse-acceleration selector has no direct ZMK equivalent and is inactive. No mouse movement keys existed in this VIA layout.
- ZMK hold-tap behavior is configured to approximate the QMK timing; typing feel still needs physical testing.

## Build and flash

GitHub Actions builds left, right, and recovery `settings_reset` UF2 files. Flash each normal firmware file only to the matching half after double-tapping that half's reset button over USB.

The settings-reset image is for recovery only: it erases saved pairing settings. It is not a normal keyboard firmware. If recovery is necessary, reset both halves' settings and then flash their corresponding normal firmware.

## Validation

Compilation validates both firmware targets. Physical validation must check all keys, home-row holds/taps, Space/Symbols, macros, battery operation of both halves, Bluetooth host pairing, and reconnection after power cycling. A successful build alone does not establish that these work on the hardware.
