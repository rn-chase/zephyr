# Zephyr

**A game-agnostic mod manager for Linux** that tries its hardest to make modding reliable, fixable, and tidy, without fighting your games (or your sanity).

> Status: **0.1 (early release)**  
> Expect sharp edges. Expect progress.

## Why Zephyr?

Because modding on Linux often ends up as:

copy files → game turns to mush → attempt salvage → reinstall → stare into the void

Zephyr exists to make modding:

- **Reproducible** (for distro nomads)
- **Reversible** (because we all make mistakes)
- **Organized** (unlike your sock drawer)
- **Extensible** (Sparks: Lua scripts for advanced layouts… coming soon)

## Features (0.1)

- **Workspaces** (separate mod setups per game/profile)
- **Manual mod import** (add a folder or a single file)
- **Enable/Disable** mods (moved into a hidden `.disabled` staging folder)
- **Deploy** enabled mods into a configured *modding directory*
- **Receipts + Undeploy**
  - deploy records what it wrote
  - undeploy removes only files that still match what Zephyr deployed (hash-checked)

> If something here doesn’t match what 0.1 currently does, please open an Issue.  
> The README and reality should not drift like continents.

## What’s next

These are the next priorities after 0.1. No dates, just direction:

- **Backups + Restore**
  - When deploying, back up overwritten files so `undeploy` can restore the previous state (not just delete).
- **Sparks (Lua)**
  - Scriptable deploy/layout plans for games with unusual mod folders or rules (multiple targets, sorting, transforms).
- **Workspace ergonomics**
  - `workspace list/info/rename` commands, plus clearer status output (what’s configured, what’s deployed, what’s disabled).
- **Smarter conflict awareness**
  - Detect when multiple mods write the same destination paths and report collisions before you deploy.

## Non-goals (for now)

- Nexus integration
- Windows/Mac support
- Stability guarantees across 0.x releases (for the curious and bold alike)

## Install

### From source

**Requirements**
- Rust (stable)
- A standard build toolchain for your distro
- `git`

**Build**
```bash
git clone https://github.com/rn-chase/zephyr.git
cd zephyr
cargo build --release
./target/release/zephyr --help
