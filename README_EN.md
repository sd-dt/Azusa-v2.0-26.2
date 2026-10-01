# Azusa-v2.0-26.2

![icon](icon.png)

> A client-side Minecraft **26.2** modpack on Fabric **0.19.5** · by **sd_dt**

Install: import `Azusa-v2.0-26.2.mrpack` with Modrinth App / PCL / HMCL (see Releases).

**127 mods** in this pack come from Modrinth (their project pages describe them). The other **16 mods cannot be
found on Modrinth** (self-made, community re-builds, or released elsewhere) — they are documented below.

---

## 📌 Mods NOT on Modrinth (shipped in the pack)

### Self-made

| Mod | What it does |
|---|---|
| **`azusa-safeshutdown`** | **Fixes the crash on every game exit.** Two root causes: ① `TextureManager.close()` threw `ConcurrentModificationException` when another mod/thread touched the texture map during shutdown → now it **takes a snapshot first and closes from it**; ② `TextureManager.tick()` still ran after the GL context was destroyed, causing a native `No context is current` crash → it now **skips the tick once the context is gone**. |
| **`litematica-printer-EMT-Azusa`** | **A rework of the litematica printer** (based on [MoMortis/litematica-printer-EMT](https://github.com/MoMortis/litematica-printer-EMT), AGPL-3.0, full source included). Added/fixed: spherical placing & mining, **plane-unbounded mining** (no longer limited by the schematic selection), a bedrock-breaking tab with its own bedrock logic, **improved fluid clearing** (simple mode auto-scans nearby water sources → places the fill block → after the whole area is covered it **auto-switches to a pickaxe** and mines cell by cell), **automatic tool switching** (with durability protection, and it can **fetch a tool from a shulker box**), packet rate limiting (auto cap / reset button), sign-placement orientation fix, HUD work status, ice-for-water optimisation, offhand placing, and extra-block protection for glass. Source: <https://github.com/sd-dt/litematica-printer-EMT-Azusa> |

### Self-made resource pack

| Pack | What it does |
|---|---|
| **`Azusa 汉化补充&三叉戟修复`** (Chinese localisation + trident fix) | ① **Keybind localisation**: fills in missing keybind names for many mods, including 26.2's derived `key.category.<namespace>.<path>` keys and `tab.*` keys, and ports entries that only existed in `zh_tw` into `zh_cn` (1300+ entries); ② **Mod-menu localisation** via `modmenu.summaryTranslation.*`; ③ **fixes the flipped trident model** in hand. |

### Community re-builds / non-Modrinth releases

| Mod | What it does |
|---|---|
| **`ModernUI`** (self-compiled 3.13.7.6) | Unofficial 26.2 port of Modern UI. This build **patches the "can only blur once per frame" crash**, the **lost `§` color-code parsing** (letter codes like `§c` were dropped, so text meant to be red showed white), and the **in-world text (signs/nametags) rendering pipeline**. |
| **`tweakermore`** (community fix) | masa's TweakerMore: a huge collection of client tweaks (info lines, XP-bar locator points, enchantment level display, pass-through interaction, fly-speed increments, happy-ghast riding, …) plus the schematic material tool. |
| **`screenshot_viewer`** (fixed build) | Browse and manage screenshots **in-game**, no need to leave the game. |
| **`rtssfix`** | Fixes the OpenGL timer-query crash caused by **RTSS / MSI Afterburner injection**, and stabilises FPS / frame-time display. |
| **`chunkyfly`** | Chunky-like client mod: **flies with an elytra automatically** to load/generate chunks, takes non-explosive fireworks from the inventory/hotbar, flies the fastest route and shows progress in the top-left corner. |
| **`feathermorph_client`** | Client-side **morphing / disguising**: turn yourself into any entity (model + animations), fully client-side. |
| **`satella`** | **Automated villager trading.** |
| **`configured`** | Generates **graphical config screens** for almost every mod, so you don't have to hand-edit config files. |
| **`commandtiles`** | **Command tiles**: turn frequently used commands into clickable tiles. |
| **`disc_jockey`** | **Jukebox automation**: auto-play and auto-switch discs, with configurable track lists. |
| **`gugle-carpet-addition`** | A Carpet extension adding a set of useful rules. |
| **`gpumemleakfix`** | Fixes a **GPU VRAM leak** (VRAM growing over long sessions). |
| **`instance_mover`** | **Instance migration** tool: move a whole instance (worlds/configs/mods) elsewhere. |
| **`CustomSkinLoader`** | **Multi-source skin loading**: tries several skin services in order. In this pack the **Cosmetica source has been removed** (it now returns an "Update Cosmetica To V2" promo cape to everyone); the shipped config lives at `overrides/CustomSkinLoader/CustomSkinLoader.json`. |
| **`super_resolution` (`+opengl` build)** | Super-resolution with **DLSS frame generation + Reflex low latency**. The pack uses the `+opengl` build to avoid a Vulkan-init crash; to turn frame generation / low latency off, edit `config/super_resolution/config.toml`. |

---

## 💡 Note: double hotbar (turn it off if you don't like it)

If you notice **two hotbars** on the HUD, that is the mod **`double_hotbar`** — it shows **the third row of your
inventory** as a second hotbar, and holding/double-tapping a key swaps between the two bars. **If you don't want it**:

* find **`double_hotbar-*.jar`** in your `mods` folder and add `.disabled` to its name (or delete it);
* or edit `config/double_hotbar.json5` and set `"disableMod"` to `true`;
* or simply turn it off in its in-game config screen.

---

## 📄 License & credits

* Self-made mods and resource packs: made by **sd_dt**, free to include in modpacks with attribution.
* `litematica-printer-EMT-Azusa` is based on **MoMortis**' `litematica-printer-EMT` (AGPL-3.0); this rework is also released under **AGPL-3.0** with full source included.
* All bundled mods remain copyright of **their respective authors**; special thanks to the masa mods, the Sodium/Iris ecosystem and every upstream author.
* Resource packs such as `CozyUI` and `Neko language pack` are used under their original licenses (this pack **does not** include the redistribution-prohibited CozyBA content).
