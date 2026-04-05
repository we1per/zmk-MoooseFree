# CLAUDE.md - zmk-MoooseFree

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

MoooseFree: ZMK firmware for a split keyboard (Seeed XIAO nRF52840).

- Left side: peripheral (BLE split link to right), rotary encoder (EC11), no trackball
- Right side: central (BLE to host PC), rotary encoder (EC11), PMW3610 trackball
- Forked from [ataruno/MoooseFree](https://github.com/ataruno/MoooseFree)

## Build

No local build environment. Firmware is built exclusively via **GitHub Actions**.

- Push to remote -> CI builds automatically using `build.yaml` matrix
- Build targets: `seeeduino_xiao_ble` with shields `MoooseFree_left`, `MoooseFree_right`, `settings_reset`
- Check build status: `gh run list --limit 5`

## Key Files

- `config/MoooseFree_left.conf` / `config/MoooseFree_right.conf` - per-side Kconfig
- `config/MoooseFree.keymap` - keymap and sensor bindings (5 layers)
- `boards/shields/MoooseFree/MoooseFree.dtsi` - shared device tree (encoders, sensors, matrix)
- `boards/shields/MoooseFree/MoooseFree_left.overlay` / `_right.overlay` - per-side overlays
- `config/west.yml` - workspace manifest (ZMK, pmw3610 driver, rgbled-widget)
- `drivers/sensor/ec11_throttled/` - custom EC11 driver fork with rate limiting (left side only)

## Architecture Notes

- Left/right sides have **different EC11 driver configs**: left may use custom `ec11_throttled`, right uses standard `alps,ec11`
- PMW3610 trackball is SPI-connected on right side only
- BLE split link: peripheral (left) -> central (right) -> host PC
- `OWN_THREAD` mode is required for EC11 on peripheral side (GLOBAL_THREAD causes BLE instability per upstream findings)

## Conventions

- Commit messages in Japanese (prefix with fix:, feat:, etc.)
- Branch naming: descriptive kebab-case (e.g., `fix-encoder-behaviour`)
- Main branch: `we1per_main`
- Do not force push

## Session Continuity

When the user says "前回の続き" or similar:

1. Read `.claude/context/current.md`
2. Summarize: objective, last decision, next action
3. Confirm with the user before resuming work

## Session End Protocol

Before ending a session:

1. Update `.claude/context/current.md` with current state
2. If `current.md` exceeds ~80 lines, move older details to `.claude/context/archive/YYYY-MM-DD.md`
3. Keep `current.md` focused on actionable state only
