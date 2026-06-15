# Orbital Railgun (NeoForge 1.21.1)

This project is a **NeoForge (Minecraft 1.21.1)** port of the original [Orbital Railgun](https://github.com/Mishkis/orbital-railgun) mod by Mishkis.
Maintained and ported by **Nxkoo**.

It targets **Java 21** and utilizes the NeoForge event bus system to bring high-fidelity railgun mechanics and shaders to modern Minecraft versions.

## 🚀 Notable Port Changes

* **NeoForge Architecture:** The codebase has been migrated to support the NeoForge 21.1.x architecture.
    * Fixed event bus subscriptions to separate `MOD` bus (initialization) and `GAME` bus (ticking/rendering) correctly.
    * Updated `ClientTickEvent` implementation to support the new non-abstract NeoForge event structure.
* **Rendering Pipeline:** Post-processing is implemented using the vanilla `PostChain` API and custom shader instances, mirroring the original visual effects.
    * Includes compatibility checks for **Iris/Oculus**: The mod automatically detects active shaderpacks and adjusts the railgun rendering pipeline to prevent conflicts/crashes.
* **State Management:** `RailgunState` tracks charging, cooldowns, and strike data. Logic has been updated to handle 1.21 game loop changes.
* **Claims Compatibility:** Integrated support for **FTB Chunks** and **Open Parties & Claims**. The railgun respects land claims with configurable rules for griefing prevention.

## 🛠️ Development

* **Java 21** toolchain (Required for Minecraft 1.21+).
* **NeoForge** (21.1.x).
* **GeckoLib 4** (Required dependency for animations).
* Built JARs should contain `META-INF/neoforge.mods.toml` only; the legacy Forge `META-INF/mods.toml` is intentionally not packaged.

### Building

To build the mod JAR:

```bash
./gradlew build
```

### Running the Client

To run the mod in a development environment:

```bash
./gradlew runClient
```

## ⚙️ Configuration

Configuration files are located in `config/orbital_railgun-common.toml`.

### Claim Protection

* `respectClaims`: Master switch for FTB Chunks/OPAC protection.
* `allowEntityDamageInClaims`: Allow damaging mobs/players inside claimed chunks.
* `allowBlockBreakInClaims`: Allow the explosion to break blocks in claimed chunks.
* `opsBypassClaims`: Server operators bypass all claim checks.

### Visuals & Balance

* `destructionDiameter`: The size of the crater created by the strike.
* `maxBreakHardness`: Maximum block hardness the orbital strike can destroy.
* `blocksPerTick`: Maximum number of blocks removed per server tick during an active strike.

## Beta Notes

This beta includes the NeoForge 1.21.1 rendering stabilization pass. The targeting and strike post-processing effect was corrected to use the proper client render event bus and camera model-view matrix, fixing reports where the effect appeared pinned to the bottom-left of the screen.

GeckoLib 4.7+ is required. FTB Chunks and Open Parties & Claims are optional compatibility integrations.

## Shader Compatibility

The targeting and strike visuals use a NeoForge `PostChain`. Iris/Oculus shaderpacks are detected at runtime; when a shaderpack is active, the railgun post-processing chain is disabled to avoid framebuffer and depth-buffer conflicts.

If the targeting effect appears pinned to a screen corner, test without shaderpacks first and report GPU, window mode, resolution, FOV, and whether Oculus/Iris is installed.

## ⚠️ Credits

* **Nxkoo** - NeoForge 1.21.1 Port & Maintainer.
* **Mishkis** - Original Mod Author.
* **TysonTheEmber** - Previous Forge Porting work.

## License

This project follows the license of the original repository. Please refer to the LICENSE file for details.
