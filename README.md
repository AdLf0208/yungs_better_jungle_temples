# YUNG's Better Jungle Temples — a Horizon port

**YUNG's Better Jungle Temples** is a Minecraft mod. Redesigns & enhances vanilla's jungle temples. This repository is a **port of it to [Horizon](https://github.com/horizon-rust/horizon)**, the Rust engine for Minecraft Java 26.3. It carries the complete source of the port plus the content files it ships, and installs as a single `.hmod` package.

Upstream: [YUNG-GANG/YUNGs-Better-Jungle-Temples](https://github.com/YUNG-GANG/YUNGs-Better-Jungle-Temples) — licence **LGPL-3.0-only**.

| | |
|---|---|
| Upstream mod | YUNG's Better Jungle Temples ([source](https://github.com/YUNG-GANG/YUNGs-Better-Jungle-Temples)) |
| Ported to | Horizon 0b14f8a, Minecraft Java 26.3, mod API `0.2` |
| Package | `betterjungletemples.hmod` (install it with the Horizon launcher) |
| Licence | **LGPL-3.0-only** — the upstream mod's licence; see [Licence and credit](#licence-and-credit) |

## What this port implements

### What this slice does

- The structure `betterjungletemples:jungle_temple` places and generates: a
  YUNG's jigsaw whose start is 25–30 blocks under the surface, its 17 pools and
  127 templates assembled by the game, its chests filled from
  `betterjungletemples:chests/{campsite,treasure}`, its biome tag attached to
  `#minecraft:has_structure/jungle_temple`.
- Its placement is carried as `minecraft:random_spread` with YUNG's own rules
  (`horizon:avoid_biomes` for the ocean/river refusal,
  `horizon:exclusion_zone` for the enhanced exclusion zone around
  `minecraft:jungle_temples`).
- Its processor lists are carried: the palette-replacement, pillar, torch,
  blast-furnace and cave-vine processors are `horizon:pick` /
  `horizon:yung_pillar` with the mod's own probabilities and properties.
- The five pool elements gated on Create/Supplementaries/Alex's Mobs are off
  (their templates stay in the package unused), so no placed template names
  another mod's blocks.

## Not yet ported

No omissions are recorded for this slice; `notes.md` is the authoritative list.

## Installing

1. Install the [Horizon launcher](https://github.com/horizon-rust/horizon/releases) (0.2.70 or newer).
2. Add `betterjungletemples.hmod` to the instance's mods.
3. The package is pinned to a specific Horizon build; the launcher checks that pin.

## Licence and credit

YUNG's Better Jungle Temples was created by its upstream authors; the code, models and assets in the original mod
remain theirs and are used here under **LGPL-3.0-only**. The Rust in this repository is a clean-room
rewrite for Horizon, not a translation of the original source.

- `LICENSE` — the upstream licence text.
- `LICENSE-NOTICE.md` — what this port carries and where it came from.
- The upstream project: https://github.com/YUNG-GANG/YUNGs-Better-Jungle-Temples

## Technical details

```
horizon-mod.toml   package manifest (id, version, api, [native] pin)
Cargo.toml         the crate; depends on `horizon-mod-api` from the fetched SDK
src/               lib.rs (the one `impl Hooks`), runtime.rs (pure logic + tests), glue
assets/ data/      the content the package ships
tools/             content generators and the e2e scenario
```

- Build: `cargo horizon-mod build` (packages; it does not compile against the game).
- Test: `cargo test`, `cargo clippy --all-targets -- -D warnings`.
- In-game: `ports/tools/launcher-game.sh run betterjungletemples` in the campaign tree, or install the
  `.hmod` and play; the harness scenario is `tools/e2e.sh`.

This repository is generated from the campaign's port at `ports/betterjungletemples/`; the port's own
`notes.md` is the full record (decisions, traps, evidence).
