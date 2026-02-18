# Zephyr

**PSA:**
**This is essentially my capstone project for learning Rust, but that doesn't mean it's not a serious project that I want to actually want to make real.
It works, and more features are being added as I learn more.
If that doesn't scare you off, I hope you enjoy it. If you do get some value out of Zephy's use, I hope you're willing to stick around and see Zephyr grow.**

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

 ## Install

### From source

**Requirements**
- Rust (stable)
- A standard build toolchain for your distro
- `git`

**Build**
 - git clone https://github.com/rn-chase/zephyr.git
 - cd zephyr
 - cargo build --release
 - ./target/release/zephyr --help

**Binary**
 - On the way, I promise

 ## Workflow Quick start

**1) Create a workspace and set the modding directory**
  - zephyr (interactive)
    
    *or*
    
  - zephyr --workspace <game> init --modding-dir /path/to/mods --force (explicit)
  
**2) Add a mod**
 - zephyr --workspace <game> add /path/to/mod --id <mymod>

**3) Check status**
 - zephyr --workspace <game> list

**4) Deploy (preview first)**
 - zephyr --workspace <game> deploy --dry-run
 - zephyr --workspace <game> deploy

**5) Undo deploy (safe)**
 - zephyr --workspace <game> undeploy <mymod> --dry-run
 - zephyr --workspace <game> undeploy <mymod>

**6) Disable / Enable**
 - zephyr --workspace <game> disable <mymod>
 - zephyr --workspace <game> enable <mymod>

**7) Remove from staging**
 - zephyr --workspace <game> remove <mymod> (if disabled)
 - zephyr --workspace <game> remove <mymod> --force (if enabled)

## Folder layout

Zephyr stores workspaces under UUID folders internally, but you refer to them by friendly workspace IDs.

~/.zephyr/index.json (workspace registry)

~/.zephyr/workspaces/<uuid>/

  - config.toml

   - mods/

   - mods/.disabled/

   - deploy/receipts/

   -  sparks/ (reserved)

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

## Copyright
 - Zephyr
 - Nate Chase (C) 2026

## License
This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.
