# Azusa 26.2

**简体中文** | [English](README_EN.md)

![icon](icon.png)

> Minecraft **26.2** + Fabric **0.19.5** 客户端整合包 · 作者 **sd_dt**

安装：用 Modrinth App / PCL / HMCL 等启动器导入 Releases 里的 `.mrpack`（最新为 `Azusa-v2.1.2-26.2.mrpack`；
历史版本见 <https://github.com/sd-dt/Azusa-v2.0-26.2/releases>）。

---

## ⚠️ 配方查看器：可以换 JEI，但**不要用 REI**

本包默认使用 **EMI**。**用不习惯可以自行换成 JEI**。

**请不要用 REI**，两个原因：

1. 会和 **Villager Trading Overhaul** 起冲突；
2. 在 **tsl 服务器**上会导致**无法攀爬铁链**等原本应该可以攀爬的方块。

> 换模组时记得把 `mods/emi-*.jar` 移出并放进对应的 JEI jar 即可，其余配置无需改动。

---

整合包内 **125 个模组来自 Modrinth**（可在对应项目页查到用途），其余 **22 个无法通过 Modrinth 直链安装**
（自制、社区改版，或平台未索引到对应文件），随包提供，下面逐个说明它们的功能。

---

## 📌 不在 Modrinth 上的模组（随包提供，共 22 个）

### 自制

| 模组 | 功能 |
|---|---|
| **`azusa-safeshutdown`** | **修复退出游戏必崩的问题**。两处根因：① `TextureManager.close()` 关闭纹理时若有其它线程/模组同时改动纹理表，会抛 `ConcurrentModificationException` → 改为**先快照再逐个关闭**；② GL 上下文已销毁后仍执行 `TextureManager.tick()`，触发 native 层 `No context is current` 崩溃 → 现在**检测到上下文消失就跳过 tick**。 |
| **`litematica-printer-EMT-Azusa`** | **投影打印机改版**（基于 [MoMortis/litematica-printer-EMT](https://github.com/MoMortis/litematica-printer-EMT)，AGPL-3.0，附完整源码）。本包为 **multi 构建（1.21.11 + 26.2 同一 jar）**。新增/修复：球形放置与球形挖掘、**平面无边界挖掘**（不受投影选区限制）、破基岩分页与自研基岩破坏、**更好的排流体**（简单模式自动扫描附近水源 → 铺填充方块 → 整片盖住后自动切镐逐格挖掉）、**自动工具切换**（含耐久保护、可用完从**潜影盒取工具**）、数据包限流（自动上限/重置）、告示牌放置朝向修正、HUD 工作状态、冰水转换优化、副手放置、玻璃等额外方块保护。源码仓库：<https://github.com/sd-dt/litematica-printer-EMT-Azusa> |
| **`bf1-nametag-hider`** | **让玩家名牌跟着「更好的F1重制版」一起隐藏**。按 F1 循环到**第二次**（隐藏 HUD + 隐藏手部物品）时，玩家名牌同步消失；第一次（只隐藏 HUD）名牌仍在，第三次恢复。注入点是 `AvatarRenderer.submitNameDisplay` —— 26.2 里玩家渲染器**自己 override 了**这个方法且不调 `super`，所以打在父类 `EntityRenderer` 上的注入会被**静默绕过**（日志里一句报错都没有），这也是同类「切不掉玩家名牌」模组失效的根因。本实现只作用于玩家，不影响生物与其它实体名牌。 |

### 自制资源包

| 资源包 | 功能 |
|---|---|
| **`Azusa 汉化补充&三叉戟修复`** | ① **按键设置汉化**：补齐各模组缺失的按键名，包含 26.2 的 `key.category.<命名空间>.<路径>` **派生键**、`tab.*` 前缀键，并把只存在于 `zh_tw` 的条目搬进 `zh_cn`（共 1300+ 条）；② **模组菜单汉化**：为没有中文的模组补 `modmenu.summaryTranslation.*`；③ **三叉戟模型翻转修复**。 |

### 社区改版 / 非 Modrinth 发布

| 模组 | 功能 |
|---|---|
| **`emi`**（本地构建） | 物品与配方查看器（EMI）。本包内为**本地构建**，文件哈希与 Modrinth 上发布的版本不同，因此随包提供、不走在线直链。**用不习惯可换成 JEI，但不要用 REI**（原因见上文）。 |
| **`ModernUI`**（自编译版 `3.13.7.6`，`fontfix-8x-aa-thai-default` 构建） | Modern UI 的 26.2 非官方移植（自编译）。修复内容包括：**"模糊只允许一次/帧"崩溃**、**`§` 颜色代码解析失效**（字母色码如 `§c` 被丢弃导致本该红色的字显示为白色）、**世界内文字（告示牌/名牌）渲染管线**等。 |
| **`tweakermore`**（社区修复版） | masa 的 TweakerMore：海量客户端微调（信息栏、经验条定位点、附魔等级显示、穿透交互、飞行速度增量、乐魂骑乘等），并提供投影材料收集等工具。 |
| **`screenshot_viewer`**（修复版） | 游戏内浏览/管理截图（不必退出游戏翻文件夹），修复版可在 26.2 正常使用。 |
| **`rtssfix`** | 修复 **RTSS / MSI Afterburner 注入**导致的 OpenGL 时间查询崩溃，并稳住帧率与帧时间显示。 |
| **`chunkyfly`** | 类 Chunky 的客户端模组：用**鞘翅自动飞行**来加载/生成区块，自动从背包与快捷栏取用非爆炸烟花，按最快方式飞行，左上角显示进度。 |
| **`feathermorph_client`** | 客户端**变形/伪装**：把自己伪装成任意实体（含模型与动画），纯客户端。 |
| **`satella`**（`dt` 构建） | **村民交易自动化**，并加料：**全自动合成 / 切石**、物品保护、**三叉戟三模式交互**、副手食物、附魔光效、`/st` 定位器。源码仓库：<https://github.com/sd-dt/satella-dt> |
| **`configured`** | 为几乎所有模组**自动生成图形化配置界面**，免去手改配置文件。 |
| **`commandtiles`** | **指令快捷块**：把常用指令做成可点的方块/面板。 |
| **`disc_jockey`** | **唱片机自动化**：自动播放、自动切换唱片，可设定曲目。 |
| **`gugle-carpet-addition`** | Carpet 扩展模组，提供一批实用规则。 |
| **`gpumemleakfix`** | 修复 GPU **显存泄漏**（长时间游戏后显存持续增长的问题）。 |
| **`instance_mover`** | **游戏实例迁移**工具：把整个实例（存档/配置/模组）搬到别处。 |
| **`Chord`**（文件名是 `fabric-0.7.10.jar`） | **手持乐器实时演奏**：把乐器拿在手上即可弹奏，声音靠**服务端插件广播**，**听的人不需要装任何东西**。⚠️ jar 的实际文件名是 `fabric-0.7.10.jar`，**别误当成 Fabric Loader 删掉**。 |
| **`halfmasa`** | masa 风格的客户端工具集：**Xaero 存档绑定**、路径点管理、创造模式工具、背包界面增强、JEI/REI 查询历史。 |
| **`LitematicaPass`** | 把**投影（Litematica）画面渲染到独立渲染目标**，使 **Iris 光影不再影响投影** —— 投影不会再被光影的光照、水体、后处理染色。 |
| **`MapMipMapMod`** | 修复**地图纹理的 mipmap**：远处看挂在墙上的地图不再发糊、闪烁。 |
| **`ViaFabricPlus Bedrock`** | 给 **ViaFabricPlus 增加基岩版（Bedrock）协议支持**，可直连基岩版服务器（体积较大，约 16 MB，属正常）。 |

---

## 💡 小提示：双层快捷栏（不喜欢可以关掉）

如果你在 HUD 上发现**有两条快捷栏**，那是模组 **`double_hotbar`** 的功能 —— 它把**背包第 3 行**当成第二条快捷栏显示，
长按/双击按键可在两条栏之间切换。**如果你不喜欢它**：

* 在 `mods` 文件夹里找到 **`double_hotbar-*.jar`**，改名加 `.disabled` 即可（或直接删除）；
* 或者改 `config/double_hotbar.json5`：把 `"disableMod"` 设为 `true`；
* 也可以在游戏内的模组配置界面里关掉它。

## 💡 小提示：皮肤加载（CustomSkinLoader）

`CustomSkinLoader` 本体已能通过 Modrinth 直链安装，本包只额外带一份配置（`overrides/CustomSkinLoader/CustomSkinLoader.json`）：
其中**已移除 Cosmetica 皮肤源** —— 该源现在会给所有人返回一个「Update Cosmetica To V2」的宣传披风。

---

## 📄 许可与致谢

* 自制模组与资源包：**sd_dt** 制作，可随整合包分发，转载请注明。
* `litematica-printer-EMT-Azusa` 基于 **MoMortis** 的 `litematica-printer-EMT`（AGPL-3.0），本改版同样以 **AGPL-3.0** 发布并附带完整源码。
* 包内各模组版权归**各自作者**所有；特别感谢 masa 系列、Sodium/Iris 生态与所有上游作者。
* 资源包 `CozyUI`、`Neko language pack` 等按其原始许可使用（本包**不含**禁止外传的 CozyBA 内容）。
