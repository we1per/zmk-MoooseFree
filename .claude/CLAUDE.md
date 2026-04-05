# CLAUDE.md - zmk-MoooseFree

## Project Overview

MoooseFree: ZMK firmware for a split keyboard with rotary encoders and PMW3610 trackball.

- Left side: peripheral (BLE split link to right), rotary encoder, no trackball
- Right side: central (BLE to host PC), rotary encoder, PMW3610 trackball
- MCU: Seeed XIAO nRF52840

## Key Files

- `config/MoooseFree_left.conf` / `config/MoooseFree_right.conf` - per-side Kconfig
- `config/MoooseFree.keymap` - keymap and sensor bindings
- `boards/shields/MoooseFree/MoooseFree.dtsi` - shared device tree (encoders, sensors, matrix)
- `boards/shields/MoooseFree/MoooseFree_left.overlay` / `_right.overlay` - per-side overlays

## Session Continuity

When the user says "前回の続き" or similar:

1. Read `@context/current.md`
2. Summarize: objective, last decision, next action
3. Confirm with the user before resuming work

## Session End Protocol

Before ending a session:

1. Update `@context/current.md` with current state
2. If `current.md` exceeds ~80 lines, move older details to `context/archive/YYYY-MM-DD.md`
3. Keep `current.md` focused on actionable state only
