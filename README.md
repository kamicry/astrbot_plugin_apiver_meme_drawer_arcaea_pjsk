# 🎨 PJSK & Arcaea 表情包生成器（AstrBot 插件）

一款基于 [AstrBot](https://github.com/Soulter/AstrBot) 的插件，用于生成 **Project SEKAI（PJSK）** 和 **Arcaea** 角色表情包（梗图）。

> 通过 Vercel 部署的外部 API 将文字渲染到角色图片上，插件负责用户交互流程。

---

## ✨ 功能

- **🖼 交互式引导** — 一步步选择作品、角色、样式、输入文字，轻松生成表情包
- **⚡ 快捷指令** — 一行命令直达，无需交互
- **📋 角色列表** — 查看所有可用角色及其编号
- **🎮 双作品支持** — 同时支持 Project SEKAI 和 Arcaea 两大音游
- **🎭 丰富样式** — PJSK 每个角色拥有多种表情/姿势（最多 16 种）

---

## 📌 命令

| 命令 | 说明 |
|---|---|
| `/draw` | 进入交互式模式，按步骤生成表情包 |
| `/draw list` | 发送角色参考图（PJSK + Arcaea） |
| `/draw help` | 显示帮助信息 |
| `/draw pjsk <样式ID> <文字>` | 快捷生成 PJSK 表情包 |
| `/draw arcaea <角色编号> <文字>` | 快捷生成 Arcaea 表情包 |
| `quit` | （交互模式中）退出当前会话 |

### 使用示例

```
/draw pjsk 42 好饿
/draw arcaea 3 你干嘛
```

---

## 🔧 配置

在 AstrBot 管理面板中设置以下配置项：

| 配置项 | 类型 | 默认值 | 说明 |
|---|---|---|---|
| `api_url` | string | `""` | 表情渲染 API 地址，格式如 `https://your-project.vercel.app/api/overlay-text` |

> ⚠️ `api_url` **必须配置**，否则插件无法生成表情包。请向机器人管理员申请配置。

---

## ☁️ 部署 API 后端

本插件依赖一个独立的 Vercel API 服务进行表情渲染，需要自行部署。

### API 请求格式

```
GET {api_url}?type={pack}&path={raw_png_url}&key={文字}
```

| 参数 | 说明 |
|---|---|
| `type` | `pjsk` 或 `arcaea` |
| `path` | 角色 PNG 图片在 GitHub 上的原始链接 |
| `key` | 要叠加的文字（需 URL 编码） |

部署完成后将 API URL 填入插件的 `api_url` 配置项即可使用。

---

## 🎭 角色一览

### Project SEKAI（26 位角色，样式 ID 范围 0~358）

| 角色 | 样式数 | 角色 | 样式数 |
|---|---|---|---|
| 初音未来 (Miku) | 16 | 星乃一歌 (Ichika) | 15 |
| 镜音铃 (Rin) | 16 | 天马咲希 (Saki) | 14 |
| 镜音连 (Len) | 14 | 望月穗波 (Honami) | 14 |
| 巡音流歌 (Luka) | 15 | 日野森志步 (Shiho) | 14 |
| MEIKO | 14 | 花里实乃理 (Minori) | 15 |
| KAITO | 15 | 桐谷遥 (Haruka) | 15 |
| 小豆泽心羽 (Kohane) | 14 | 桃井爱莉 (Airi) | 15 |
| 白石杏 (An) | 14 | 日野森雫 (Shizuku) | 14 |
| 东云彰人 (Akito) | 14 | 天马司 (Tsukasa) | 14 |
| 青柳冬弥 (Touya) | 14 | 神代类 (Rui) | 14 |
| 奏 (Kanade) | 14 | 东云绘名 (Ena) | 14 |
| 朝比奈真冬 (Mafuyu) | 13 | 晓山瑞希 (Mizuki) | 15 |
| 草薙宁宁 (Nene) | 14 | 凤笑梦 (Emu) | 14 |

### Arcaea（22 个角色/形态）

包含光 (Hikari)、对立 (Tairitsu) 等多种角色及其不同形态，每个角色提供 1 种样式。

---

## 📁 项目结构

```
astrbot-plugin-pjsk-sticker/
├── main.py               # 插件核心逻辑
├── metadata.yaml          # AstrBot 插件元数据
├── _conf_schema.json      # 配置项定义
├── requirements.txt       # Python 依赖（仅 httpx）
├── list.json              # 角色/样式/作品数据
├── list/                  # 角色参考图片目录
│   ├── characterListAll.jpeg       # PJSK 全部角色一览
│   ├── characterListWithIndex.jpeg # PJSK 角色带编号
│   ├── arcaea_list.jpg             # Arcaea 角色列表
│   └── {角色名}.jpeg               # 单个角色样式参考图
├── CHANGELOG.md           # 更新日志
├── README.md              # 本文件
├── LICENSE                # 许可证
└── logo.png               # 插件图标
```

---

## 📦 依赖

- `httpx >= 0.24.0` — HTTP 请求库
- `astrbot` — AstrBot 框架运行时（无需单独安装）

---

## 📄 许可证

本项目基于 [MIT 许可证](LICENSE) 开源。

---

## 🙏 致谢

- [AstrBot](https://github.com/Soulter/AstrBot) — 插件框架
- [Project SEKAI](https://pjsekai.sega.jp/) — 角色素材版权归 SEGA / Colorful Palette 所有
- [Arcaea](https://arcaea.lowiro.com/) — 角色素材版权归 lowiro 所有
