<div align="center">

# LootForge

**Fully-configurable, asynchronous, multi-platform loot chests & crate events for Minecraft.**

Random loot chests, refilling fixed chests, and scheduled Envoy crate events -
with weighted loot, cinematic supply-drop animations, per-player client-side
holograms, and drop-in integrations for everything from economies to custom items.

[![Minecraft](https://img.shields.io/badge/Minecraft-1.8.8%20to%2026.2-brightgreen)](../../wiki/Building-and-Compatibility)
[![Platforms](https://img.shields.io/badge/Spigot%2C%20Paper%2C%20Purpur%2C%20Pufferfish%2C%20Folia-blue)](../../wiki/Building-and-Compatibility)
[![Java](https://img.shields.io/badge/Java-8%20to%2025-orange)](../../wiki/Building-and-Compatibility)
[![Dependencies](https://img.shields.io/badge/dependencies-none%20required-success)](../../wiki/Integrations)

### **[Read the full Wiki ->](../../wiki)**

</div>

---

LootForge is a complete, modular rewrite of *RandomLootChest*. It spawns random
loot chests around your worlds and lets admins register refilling fixed chests -
but **everything** (messages, GUIs, loot, sounds, particles, spawn rules,
schedules, integrations) is now fully configurable, runs asynchronously, and is
built for the entire modern server ecosystem.

> One NMS-free codebase, two jars, **every** Minecraft version from 1.8.8 to the
> latest 26.2 builds.

---

## Highlights

- **Two independent loot systems.**
  [Random Loot Chests](../../wiki/Random-Loot-Chests) scatter & refill chests
  around your world; [Envoys](../../wiki/Envoys) deploy scheduled crate events
  players race to open. Separate configs, toggles, loot, regions, schedules and
  redemption.
- **Weighted loot tables** with vanilla items, custom-plugin items, player
  heads, money, tokens and console-command rewards - optionally biased by the
  vanilla [Luck attribute](../../wiki/Luck-Attribute).
- **Cinematic delivery.** Falling / floating "care package" drops with particle
  or block parachutes ([Drops & Animations](../../wiki/Drops-and-Animations)),
  and **per-player, client-side [holograms](../../wiki/Holograms)** via
  PacketEvents.
- **Three [redemption modes](../../wiki/Redemption-Modes)** - instant digital
  grab, persistent in-world chest, or a personal claimable reward bank.
- **Tiered Envoys.** A persistent counter drives an
  [escalating tier ladder](../../wiki/Envoy-Tiers) - rarer crates, further out,
  less often, each with its own loot and animation.
- **Total presentation control.** Every string is
  [MiniMessage / legacy](../../wiki/Messages-and-Text) and delivered per-player as
  chat, action bar, title or boss bar.
- **Edit it in-game.** A full [GUI config editor](../../wiki/In-Game-Editor) and
  drag-and-drop loot editor mean you rarely touch a file.
- **Drop-in integrations.** Economy, tokens, custom items, land claims,
  Multiverse, Bedrock/Geyser and more - all
  [auto-detected and optional](../../wiki/Integrations).
- **Async & Folia-safe.** Heavy work runs off the main thread, mapping onto
  Folia's region/async schedulers automatically.

---

## Quick start

1. **[Install](../../wiki/Installation)** the right jar in `plugins/` (modern for
   1.13+, legacy for 1.8-1.12) and start the server.
2. Open `plugins/LootForge/config.yml` and confirm `enabled: true`.
3. Point the `default` region at your world in `regions.yml`, then turn on a
   system in `rlc.yml` or `envoys.yml`.
4. `/lf reload`, then test with `/lf forcespawn` or `/lf envoy start`.

Full walkthrough: **[Quick Start](../../wiki/Quick-Start)**.

```yaml
# rlc.yml - a chest every 30 seconds, instant-grab loot
enabled: true
random-chest:
  enabled: true
  loot-table: default
  loot-type: DIGITAL
  schedule: { enabled: true, mode: INTERVAL, interval: 30s }
```

---

## Commands

`/lootforge` (aliases `/lf`, `/rlc`):

| | |
|---|---|
| **RLC / shared** | `help`, `rewards`, `additem [table]`, `addchest`, `delchest`, `delall`, `killall`, `togglebreak`, `forcespawn`, `rndtime`, `editor`, `reload` |
| **Envoys** | `envoy start`, `envoy stop`, `envoy editor`, `envoy addspot`, `envoy delspot`, `envoy list` |

Permissions are `lootforge.command.<sub>`, `lootforge.admin`, and
`lootforge.command.use`. Full reference:
**[Commands & Permissions](../../wiki/Commands-and-Permissions)**.

---

## Loot ids

A loot entry's `item:` (or a chest/crate `block:`) can be any of:

```
DIAMOND_SWORD                  vanilla material
oraxen:ruby                    Oraxen
nexo:ruby                      Nexo
itemsadder:cat:ruby            ItemsAdder
mythic:HealthPotion            MythicMobs / Crucible
eitem:MY_SWORD                 ExecutableItems
head:<player|base64>           custom skull (no head plugin needed)
base64-<texture>               skull from a raw base64 texture (stacks)
hdb-<id>                       HeadDatabase head by id
money:1000                     economy reward
tokens:50                      token reward
command:eco give {player} 100  virtual reward (console command)
```

Full grammar: **[Item IDs](../../wiki/Item-IDs)**.

---

## Integrations

All optional and auto-detected; the plugin loads fine with none installed.

| Category | Supported out of the box |
|----------|--------------------------|
| Placeholders | PlaceholderAPI (two-way) |
| Economy | Vault bridge (CMI, EssentialsX, ExcellentEconomy, RoyaleEconomy...) |
| Tokens | TokenManager, PlayerPoints |
| Custom items | Oraxen, Nexo, ItemsAdder, MythicMobs, ExecutableItems, HeadDatabase, base64 heads |
| Land claims | WorldGuard, Lands, GriefDefender, Factions, SuperiorSkyblock2, BentoBox |
| World | Multiverse-Core + world-border clamp |
| Bedrock | GeyserMC / Floodgate |
| Cosmetic / packets | ModelEngine, PacketEvents |

Details & extension points: **[Integrations](../../wiki/Integrations)** -
**[Developer API](../../wiki/Developer-API)**.

---

## Configuration files

Nothing is hard-coded - each concern has its own file, created on first run:

| File | Purpose |
|------|---------|
| `config.yml` | global settings: text, storage, holograms, luck, perms |
| `regions.yml` | named spawn regions (cuboid / WorldGuard) |
| `rlc.yml` | the Random Loot Chest system |
| `envoys.yml` | the Envoy system + tier ladder |
| `loot.yml` | weighted loot tables |
| `messages.yml` | every player-facing string + delivery channel |
| `hooks.yml` | enable / prioritise every integration |
| `guis/*.yml` | menu layouts (loot, admin editor, rewards) |

Full reference: **[Configuration Files](../../wiki/Configuration-Files)**.

---

## Building

```bash
./gradlew build        # macOS / Linux
gradlew.bat build      # Windows
```

Outputs two shaded jars in `build/libs/`:

- `LootForge-<version>.jar` - modern servers (1.13 -> 26.2)
- `LootForge-<version>-legacy.jar` - legacy servers (1.8 -> 1.12)

Requires **JDK 25** to read the 26.2 paper-api class files (Gradle auto-provisions
it); the compile emits **Java 8 byte-code** so the same classes load on every
JVM. Details: **[Building & Compatibility](../../wiki/Building-and-Compatibility)**.

---

## Documentation

The **[Wiki](../../wiki)** covers every feature in depth:

| Getting started | Loot systems | Loot & rewards | Presentation | Integrations & reference |
|---|---|---|---|---|
| [Installation](../../wiki/Installation) | [Random Loot Chests](../../wiki/Random-Loot-Chests) | [Loot Tables](../../wiki/Loot-Tables) | [Drops & Animations](../../wiki/Drops-and-Animations) | [Integrations](../../wiki/Integrations) |
| [Quick Start](../../wiki/Quick-Start) | [Fixed Chests](../../wiki/Fixed-Chests) | [Item IDs](../../wiki/Item-IDs) | [Holograms](../../wiki/Holograms) | [PlaceholderAPI](../../wiki/PlaceholderAPI) |
| [Concepts & Architecture](../../wiki/Concepts-and-Architecture) | [Envoys](../../wiki/Envoys) | [Redemption Modes](../../wiki/Redemption-Modes) | [Particles & Sounds](../../wiki/Particles-and-Sounds) | [Bedrock Support](../../wiki/Bedrock-Support) |
| [Commands & Permissions](../../wiki/Commands-and-Permissions) | [Envoy Tiers](../../wiki/Envoy-Tiers) | [Luck Attribute](../../wiki/Luck-Attribute) | [Messages & Text](../../wiki/Messages-and-Text) | [Configuration Files](../../wiki/Configuration-Files) |
| | [Regions](../../wiki/Regions) - [Scheduling](../../wiki/Scheduling) | | [GUIs & Menus](../../wiki/GUIs-and-Menus) - [In-Game Editor](../../wiki/In-Game-Editor) | [Developer API](../../wiki/Developer-API) - [FAQ](../../wiki/FAQ-and-Troubleshooting) |

---

<div align="center">

**[Browse the Wiki](../../wiki)** - **[Report an issue](../../issues)** - **[FAQ & Troubleshooting](../../wiki/FAQ-and-Troubleshooting)**

</div>
