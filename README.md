# Azusa-v2.0-26.2

![icon](icon.png)

> Minecraft **26.2** + Fabric **0.19.5** 客户端整合包 · 作者 **sd_dt**
> 由个人长期维护的整合包，包含**自制模组**、**自制汉化资源包**与一批提升手感/性能的辅助模组。

---

## 📦 整合包内容

| 类别 | 内容 |
|---|---|
| 模组 | 143 个启用模组（127 个来自 Modrinth，其余为自制或社区改版） |
| 资源包 | `Azusa 汉化补充&三叉戟修复`、CozyUI、FA+Player 等 |
| 光影 | Euphoria Patches 等光影配置与着色器包 |
| 配置 | 全部 `config/` 已按本整合包调好（性能、UI、按键、汉化相关设置） |

**安装**：用 Modrinth App / PCL / HMCL 等支持 `.mrpack` 的启动器导入 `Azusa-v2.0-26.2.mrpack` 即可（Release 页下载）。

---

## ✍️ 自制模组与资源包（主要功能）

### 1. `azusa-safeshutdown` — 退出崩溃修复

修掉每次退出游戏必然出现的崩溃报告，两处根因：

* `TextureManager.close()` 在关闭时有其它模组/线程修改纹理表 → `ConcurrentModificationException`；
  现在改为**先快照再逐个关闭**，不再抛异常。
* GL 上下文已销毁后仍会执行 `TextureManager.tick()` → native 层
  `FATAL ERROR in native method: No context is current`；现在**检测到上下文消失就跳过 tick**。

### 2. `litematica-printer-EMT-Azusa` — 投影打印机改版

基于 [MoMortis 的 litematica-printer-EMT](https://github.com/MoMortis/litematica-printer-EMT)（EMT+260925 基线）改写的版本，新增与修复：

* **放置**：球形放置、副手放置、玻璃等"额外方块"保护、告示牌朝向修正。
* **挖掘**：球形挖掘、**平面无边界**（不受投影选区限制，仅受工作半径约束）、破基岩**分页**与自研基岩破坏。
* **排流体（更好的排流体）**：简单模式下**自动扫描附近水源** → 铺填充方块（默认圆石/石头）→
  整片盖住后再**自动切镐**逐格挖掉；工具在背包没有时会按需**从潜影盒取用**。
* **工具与限流**：自动工具切换（含耐久保护）、数据包限流（自动上限 / 重置按钮）、快捷潜影盒补货。
* **界面**：HUD 工作状态、破基岩分页、冰水转换优化。

> 源码与构建脚本见该模组自己的仓库：<https://github.com/sd-dt/litematica-printer-EMT-Azusa>

### 3. `Azusa 汉化补充&三叉戟修复` — 自制资源包

* **按键设置汉化**：补全各模组缺失的按键名，包含 26.2 新增的
  `key.category.<命名空间>.<路径>` **派生键**、`tab.*` 前缀键，以及把只在 `zh_tw` 里存在的条目搬进 `zh_cn`（共 1300+ 条）。
* **模组菜单汉化**：为没有中文的模组补 `modmenu.summaryTranslation.*` 简介。
* **三叉戟模型翻转修复**：修正手持三叉戟时的模型朝向。

---

## 🔧 辅助模组与它们的"特殊功能"

### 双层快捷栏（`double_hotbar`）— 本整合包重点功能

把**背包第 3 行**当作**第二条快捷栏**显示在 HUD 上，等于随身带两条快捷栏：

* **长按设置的按键**即可在两条快捷栏之间**热切换**当前生效的那一条（`holdToSwap`），也支持**双击切换**（`allowDoubleTap`）；
* 可调整第二条快捷栏的**显示位置/偏移**（`shift`）、渲染裁剪（`renderCrop`）、是否反转两条栏的顺序（`reverseBars`）；
* 切换时有音效反馈（`wooshVolume`）。用途：**一套工具 + 一套建材**、或将常用物品与备用物品分开轮换，不用翻背包。

### 其它值得一提的辅助模组

| 模组 | 特殊功能 |
|---|---|
| `super_resolution`（+opengl 构建） | DLSS 帧生成 + Reflex 低延迟；`+opengl` 构建用于规避 Vulkan 初始化崩溃 |
| `RTSSFix` | 修复 RTSS 注入导致的 GL 时间查询崩溃，稳定帧率/帧时间显示 |
| `Voxy` | LOD 超远视距渲染 |
| `ChunkyFly` | 客户端鞘翅自动飞行加载/生成区块，自动取用烟花并显示进度 |
| `FeatherMorph` | 客户端变形/伪装（可伪装成任意实体） |
| `Flashback` | 录制、回放与电影镜头导出 |
| `ChestTracker` | 记录与检索箱子内容（"箱子追踪"） |
| `Satella` | 村民自动交易 |
| `Instance Mover` | 游戏实例迁移工具 |
| `CustomSkinLoader` | 多来源皮肤加载 |
| masa 套件 `litematica / tweakeroo / tweakermore / itemscroller / minihud` | 投影、微调、滚轮搬运、信息 HUD |
| `Xaero 小地图/世界地图` | 地图与路径点（已附汉化） |
| 性能套件 `Sodium / Lithium / C2ME / ModernFix / ImmediatelyFast / FerriteCore / EntityCulling` | 帧率与内存优化 |

---

## 📄 许可与致谢

* 自制模组与资源包：**sd_dt** 制作，可自由用于整合包，转载请注明。
* `litematica-printer-EMT-Azusa` 基于 **MoMortis** 的 `litematica-printer-EMT`（AGPL-3.0），本改版同样以 **AGPL-3.0** 发布并附带完整源码。
* 整合包内各模组版权归**各自作者**所有；`CozyUI`、`Neko language pack` 等资源包按其原始许可使用（**不含禁止外传的 CozyBA**）。
* 特别感谢 masa 系列模组、Sodium/Iris 生态与所有上游作者。
