# MagnetRush · 磁能狂飙：金币猎手

![banner](banner.svg)


> 纯前端 · 单文件 · Canvas 2D 街机竞速游戏

[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Canvas](https://img.shields.io/badge/Canvas-2D-7c5cff.svg)](#)
[![Status](https://img.shields.io/badge/Status-Demo-green.svg)](#)

## 简介

`MagnetRush`（磁能狂飙：金币猎手）是一款纯前端、单文件的 **Canvas 2D 街机竞速游戏**。驾驶你的磁能战车在霓虹赛道上极速狂飙——躲避障碍物、收集金币，利用 **磁吸 / 雷电 / 冰冻** 三大技能冲出重围，冲击最高分！

游戏支持**三档难度**（简单 / 中等 / 困难）、**16 种装备升级**（发动机、涡轮增压、护盾、磁力收集器等）、**3 位 AI 语音助手**（可莉 / 炼狱 / 芮娜），并自动保存最高分与车库装备，随时回来继续挑战。

## 功能特性

- 🏎️ **磁能竞速**：A / D 或方向键左右移动，在车道间灵活穿梭
- 🪙 **金币猎手**：收集金币 +10 分，超大金币 +50 分，每存活 5 秒额外 +5 分
- ⚡ **三大技能**：
  - **磁吸（按 1）**：大范围吸引附近金币
  - **雷电（按 2）**：清理前方所有障碍物
  - **冰冻（按 3）**：减缓全场障碍物速度
- 🔧 **16 种装备升级**：发动机、涡轮增压器、稳定器、护盾发生器、磁力收集器、额外生命模块、障碍物扫描仪、自动收集器…… 每次奔跑赚金币，解锁更强性能
- 🧠 **3 位 AI 语音助手**：可莉（温柔）、炼狱（理性）、芮娜（竞技），不同性格配不同台词，支持中文语音播报
- 🎚️ **三档难度**：简单障碍少金币多；困难障碍更多更快，还新增移动型障碍物
- 🎨 **赛博霓虹视觉**：噪声颗粒路面、技能能量环、粒子特效，60fps 流畅渲染
- 💾 **本地存档**：最高分 + 车库装备自动保存到 `localStorage`

## 技术栈

| 技术 | 用途 |
| --- | --- |
| HTML5 Canvas 2D | 全部游戏渲染（60fps，requestAnimationFrame） |
| 原生 HTML / CSS / JS | 界面、菜单、HUD、技能与装备系统 |
| Web Audio API | 音效与背景音乐合成 |
| SpeechSynthesis | AI 助手中文语音播报 |
| localStorage | 最高分与装备进度本地存档 |

## 快速开始

### 方式一：直接打开

将 `磁能狂飙：金币猎手.html` 下载到本地，**双击用浏览器打开**即可。

### 方式二：本地服务器运行

```bash
# Python
python -m http.server 8080

# 或 Node.js
npx serve .

# 然后访问
open http://localhost:8080
```

### 方式三：在线部署

将 HTML 文件直接拖入任意静态托管平台（GitHub Pages、Vercel、Netlify、Cloudflare Pages 等）即可上线。

## 操作说明

| 按键 | 功能 |
| --- | --- |
| A / D 或 ← / → | 左右移动战车 |
| W | 加速推进（Boost） |
| S | 减速控制 |
| 数字键 1 | 释放磁吸技能 |
| 数字键 2 | 释放雷电技能 |
| 数字键 3 | 释放冰冻技能 |

## 游戏系统

### 计分规则

- 收集金币 **+10 分**，超级大金币 **+50 分**
- 每存活 **5 秒 +5 分**
- 碰撞障碍物 → 游戏结束（有护盾或额外生命模块时可免除一次）

### 技能系统

技能通过游戏中积攒能量充能，就绪后按对应数字键释放。技能图标环绕能量粒子特效，就绪时会有浮动提示。

### 装备系统

装备商店包含 **16 种可购买装备**，用奔跑赚到的金币解锁：

```js
const EQUIPMENT_CONFIG = {
    engine_basic:      { name: '发动机升级-基础版', price: 100,  effect: { speedBoost: 0.10 } },
    engine_advanced:   { name: '发动机升级-高级版', price: 300,  effect: { speedBoost: 0.20 } },
    engine_premium:    { name: '发动机升级-至尊版', price: 500,  effect: { speedBoost: 0.30 } },
    turbo_charger:     { name: '涡轮增压器',       price: 200,  effect: { boostDuration: 4.5 } },
    shield_generator:  { name: '护盾发生器',       price: 300,  effect: { extraShield: 1 } },
    magnet_collector:  { name: '磁力收集器',       price: 250,  effect: { magnetRange: 30 } },
    extra_life_module: { name: '额外生命模块',     price: 600,  effect: { extraLives: 1 } },
    obstacle_scanner:  { name: '障碍物扫描仪',     price: 320,  effect: { obstacleWarning: true } },
    auto_collector:    { name: '自动收集器',       price: 380,  effect: { autoCollectRadius: 50 } },
    // ... 更多装备见代码
};
```

### AI 助手系统

三位 AI 助手拥有不同性格与台词风格，可随时切换：

| 助手 | 类型 | 风格 |
| --- | --- | --- |
| 可莉 | 温柔型 | 卖萌鼓励，可爱语气 |
| 炼狱 | 理性型 | 客观陈述，数据化表达 |
| 芮娜 | 竞技型 | 热血上头，激将法拉满 |

## 项目结构

```
magnet-rush/
└── 磁能狂飙：金币猎手.html   # 全部代码（样式 + 逻辑 + 游戏系统），单文件即项目
```

## 浏览器兼容性

- 支持 HTML5 Canvas 与现代 Web API 的浏览器（Chrome / Edge / Firefox / Safari）
- 无需摄像头、无需网络依赖（本地音效与语音均为合成）

## License

[MIT](LICENSE) © 2025 MagnetRush Contributors

## 致谢

- 感谢 Web Audio API 与 SpeechSynthesis 让纯前端也能拥有完整音效与语音体验

## 作者

陈启粤

---

最后更新：2026-08-06
