# Azusa 26.2

[简体中文](README.md) | **English**

![icon](icon.png)

> A client-side Minecraft **26.2** modpack on Fabric **0.19.5** · by **sd_dt**

Install: import the `.mrpack` from Releases with Modrinth App / PCL / HMCL (the latest is `Azusa-v2.1.2-26.2.mrpack`;
older versions: <https://github.com/sd-dt/Azusa-v2.0-26.2/releases>).

---

## ⚠️ Recipe viewer: JEI is fine, **REI is not**

This pack ships **EMI** by default. **If you don't like it, feel free to swap in JEI instead.**

**Please do not use REI**, for two reasons:

1. It conflicts with **Villager Trading Overhaul**;
2. On the **tsl server** it makes blocks you should be able to climb — chains and the like — **unclimbable**.

> To swap, move `mods/emi-*.jar` out of the folder and drop the matching JEI jar in; nothing else needs changing.

---

**125 mods** in this pack come from Modrinth (their project pages describe them). The other **22 mods cannot be
installed from a Modrinth direct link** (self-made, community re-builds, or the platform has no matching file) —
they ship inside the pack and are documented below.

---

## 📌 Mods NOT on Modrinth (shipped in the pack, 22 total)

### Self-made

| Mod | What it does |
|---|---|
| **`azusa-safeshutdown`** | **Fixes the crash on every game exit.** Two root causes: ① `TextureManager.close()` threw `ConcurrentModificationException` when another mod/thread touched the texture map during shutdown → now it **takes a snapshot first and closes from it**; ② `TextureManager.tick()` still ran after the GL context was destroyed, causing a native `No context is current` crash → it now **skips the tick once the context is gone**. |
| **`litematica-printer-EMT-Azusa`** | **A rework of the litematica printer** (based on [MoMortis/litematica-printer-EMT](https://github.com/MoMortis/litematica-printer-EMT), AGPL-3.0, full source included). This pack ships the **multi build (one jar for 1.21.11 + 26.2)**. Added/fixed: spherical placing & mining, **plane-unbounded mining** (no longer limited by the schematic selection), a bedrock-breaking tab with its own bedrock logic, **improved fluid clearing** (simple mode auto-scans nearby water sources → places the fill block → after the whole area is covered it **auto-switches to a pickaxe** and mines cell by cell), **automatic tool switching** (with durability protection, and it can **fetch a tool from a shulker box**), packet rate limiting (auto cap / reset button), sign-placement orientation fix, HUD work status, ice-for-water optimisation, offhand placing, and extra-block protection for glass. Source: <https://github.com/sd-dt/litematica-printer-EMT-Azusa> |
| **`bf1-nametag-hider`** | **Hides player nametags together with "Better F1 Reborn".** Press F1 to cycle: on the **second** state (HUD + held item hidden) player nametags disappear too; the first state (HUD only) keeps them, the third restores everything. The injection point is `AvatarRenderer.submitNameDisplay` — in 26.2 the player renderer **overrides that method itself** without calling `super`, so an injection on the parent `EntityRenderer` is **silently bypassed** (not a single warning in the log). That is exactly why other "can't toggle player nametags" mods break. This one only affects players, never mob/entity nametags. |

### Self-made resource pack

| Pack | What it does |
|---|---|
| **`Azusa 汉化补充&三叉戟修复`** (Chinese localisation + trident fix) | ① **Keybind localisation**: fills in missing keybind names for many mods, including 26.2's derived `key.category.<namespace>.<path>` keys and `tab.*` keys, and ports entries that only existed in `zh_tw` into `zh_cn` (1300+ entries); ② **Mod-menu localisation** via `modmenu.summaryTranslation.*`; ③ **fixes the flipped trident model** in hand. |

### Community re-builds / non-Modrinth releases

| Mod | What it does |
|---|---|
| **`emi`** (local build) | Item and recipe viewer (EMI). The copy in this pack is a **local build** whose file hash differs from the version published on Modrinth, so it ships inside the pack instead of using an online direct link. **You may swap it for JEI, but do not use REI** (see above). |
| **`ModernUI`** (self-compiled `3.13.7.6`, `fontfix-8x-aa-thai-default` build) | Unofficial 26.2 port of Modern UI. This build **patches the "can only blur once per frame" crash**, the **lost `§` color-code parsing** (letter codes like `§c` were dropped, so text meant to be red showed white), and the **in-world text (signs/nametags) rendering pipeline**. |
| **`tweakermore`** (community fix) | masa's TweakerMore: a huge collection of client tweaks (info lines, XP-bar locator points, enchantment level display, pass-through interaction, fly-speed increments, happy-ghast riding, …) plus the schematic material tool. |
| **`screenshot_viewer`** (fixed build) | Browse and manage screenshots **in-game**, no need to leave the game. |
| **`rtssfix`** | Fixes the OpenGL timer-query crash caused by **RTSS / MSI Afterburner injection**, and stabilises FPS / frame-time display. |
| **`chunkyfly`** | Chunky-like client mod: **flies with an elytra automatically** to load/generate chunks, takes non-explosive fireworks from the inventory/hotbar, flies the fastest route and shows progress in the top-left corner. |
| **`feathermorph_client`** | Client-side **morphing / disguising**: turn yourself into any entity (model + animations), fully client-side. |
| **`satella`** (`dt` build) | **Automated villager trading**, plus extras: **fully automatic crafting / stonecutting**, item protection, **three trident interaction modes**, offhand food, enchantment glint, and the `/st` locator. Source: <https://github.com/sd-dt/satella-dt> |
| **`configured`** | Generates **graphical config screens** for almost every mod, so you don't have to hand-edit config files. |
| **`commandtiles`** | **Command tiles**: turn frequently used commands into clickable tiles. |
| **`disc_jockey`** | **Jukebox automation**: auto-play and auto-switch discs, with configurable track lists. |
| **`gugle-carpet-addition`** | A Carpet extension adding a set of useful rules. |
| **`gpumemleakfix`** | Fixes a **GPU VRAM leak** (VRAM growing over long sessions). |
| **`instance_mover`** | **Instance migration** tool: move a whole instance (worlds/configs/mods) elsewhere. |
| **`Chord`** (the file is named `fabric-0.7.10.jar`) | **Play an instrument in real time while holding it.** Audio is broadcast by a **server plugin**, so **listeners need nothing installed**. ⚠️ The actual file name is `fabric-0.7.10.jar` — **don't mistake it for Fabric Loader and delete it**. |
| **`halfmasa`** | A masa-style client toolkit: **Xaero save binding**, waypoint management, creative tools, inventory screen enhancements, and JEI/REI lookup history. |
| **`LitematicaPass`** | Renders **Litematica schematics into a separate render target** so **Iris shaders no longer affect them** — schematics are no longer tinted by shader lighting, water or post-processing. |
| **`MapMipMapMod`** | Fixes **mipmaps for map textures**: wall maps no longer blur or shimmer at a distance. |
| **`ViaFabricPlus Bedrock`** | Adds **Bedrock Edition protocol support** to **ViaFabricPlus**, so you can join Bedrock servers. (Large, ~16 MB — that is expected.) |

---

## 💡 Note: double hotbar (turn it off if you don't like it)

If you notice **two hotbars** on the HUD, that is the mod **`double_hotbar`** — it shows **the third row of your
inventory** as a second hotbar, and holding/double-tapping a key swaps between the two bars. **If you don't want it**:

* find **`double_hotbar-*.jar`** in your `mods` folder and add `.disabled` to its name (or delete it);
* or edit `config/double_hotbar.json5` and set `"disableMod"` to `true`;
* or simply turn it off in its in-game config screen.

## 💡 Note: skin loading (CustomSkinLoader)

`CustomSkinLoader` itself is now available from Modrinth; this pack only adds a config file
(`overrides/CustomSkinLoader/CustomSkinLoader.json`), in which the **Cosmetica source has been removed** — that
source now returns an "Update Cosmetica To V2" promo cape to everyone.

---

## 📄 License & credits

* Self-made mods and resource packs: made by **sd_dt**, free to include in modpacks with attribution.
* `litematica-printer-EMT-Azusa` is based on **MoMortis**' `litematica-printer-EMT` (AGPL-3.0); this rework is also released under **AGPL-3.0** with full source included.
* All bundled mods remain copyright of **their respective authors**; special thanks to the masa mods, the Sodium/Iris ecosystem and every upstream author.
* Resource packs such as `CozyUI` and `Neko language pack` are used under their original licenses (this pack **does not** include the redistribution-prohibited CozyBA content).
