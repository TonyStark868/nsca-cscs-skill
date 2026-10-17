# nsca-cscs-skill · 《NSCA-CSCS体能教练认证指南（第4版）》学习技能

可移植、可分发的 OpenCode 技能包。让 AI 助手掌握这本书的完整结构，并能**按书页码
现场调取原文**来回答体能训练问题、辅导 CSCS 备考。

> ⚠️ **版权说明（重要）**
> 本项目**不包含、不分发**教材本身（原书版权归 NSCA 及中文版出版方所有）。
> 本包只分发三类自有产物：
> 1. 章节索引与页码映射（事实性目录信息）
> 2. 要点提炼笔记（对概念的自组织转述，非原文复制）
> 3. 按页 OCR 调取工具
>
> 每位使用者需要自行准备**自己合法获得的**该书 PDF/扫描件并完成本地配置。
> 请勿上传或分享书的扫描件与批量 OCR 文本。
>
> **关联声明**：本项目是社区学习工具，非 NSCA 官方产品，与 NSCA 及人民邮电出版社
> 无任何隶属、合作或授权关系；"NSCA-CSCS" 名称仅用于描述学习对象与兼容性。

## 功能

- 回答体能训练问题时自动定位相关章节，标注书页码出处
- 关键数字/表格/协议步骤可现场 OCR 原书校对（带缓存，约 8 秒/页）
- 常用公式速查（1RM 估算、靶心率、Wingate、%1RM-次数表等）
- CSCS 备考模式：按章出题、讲解、追问

## 关于教材：没有书也能用吗？

本技能是**"自备教材"工具**：知识层（章节索引 + 要点笔记）装包即用；
逐页 OCR 调原文则需要你自己的书副本。

- **没书也能聊**：未配置书路径时，技能会基于章节索引与要点笔记继续辅导
  （概念、思路、方法论都能讲），只是不逐页引用原文。
- **想要完整功能**：通过出版社、京东、当当等正版渠道购买纸质或电子书，
  用你自己拥有的副本（扫描件或电子书文件）配置路径即可。
- 本项目始终**不提供书文件**，不引导盗版渠道；也请勿分享扫描件与批量 OCR 文本。

## 安装（三种方式任选）

### 方式一 · 手动放入全局技能目录（最简单）

把本仓库的 `nsca-cscs/` 文件夹复制到：

```
~/.config/opencode/skills/          # Linux/macOS
C:\Users\<用户名>\.config\opencode\skills\   # Windows
```

OpenCode 会自动发现并注册该技能（目录式 `SKILL.md`，ID 为 `nsca-cscs`）。

### 方式二 · skills 配置源（适合团队/自建服务器）

把仓库克隆到任意位置，在 `opencode.json` 中加入：

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "skills": ["<仓库克隆路径>/nsca-cscs"]
}
```

可同时写进全局（`~/.config/opencode/opencode.json`）或仅项目本地。

### 方式三 · HTTP 目录（自动分发与更新）

在 `opencode.json` 中填入本仓库的 catalog 地址（raw 或 GitHub Pages）：

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "skills": ["https://raw.githubusercontent.com/TonyStark868/nsca-cscs-skill/main/catalog/"]
}
```

OpenCode 会按 `catalog/index.json` 的文件清单自动下载缓存。**日后更新：
修改文件后把 index.json 里的 `version` 数字加一即可触发刷新。**

> 💡 **国内网络提示**：`raw.githubusercontent.com` 在大陆网络下经常无法直连。
> 若加载失败，可把地址换成 jsDelivr 镜像（效果相同）：
>
> ```jsonc
> "skills": ["https://cdn.jsdelivr.net/gh/TonyStark868/nsca-cscs-skill@main/catalog/"]
> ```

## 配置书籍 PDF（每位使用者首次使用必做）

按以下优先级解析（三选一）：

| 优先级 | 方式 | 说明 |
|---|---|---|
| 1 | `--pdf "路径"` | 单次调用参数 |
| 2 | 环境变量 `NSCA_CSCS_PDF` | 全局一次配置 |
| 3 | `nsca-cscs/references/book-path.txt` | 首行写 PDF 绝对路径（参照 `book-path.example.txt`） |

依赖安装：

```
pip install -r requirements.txt
```

首次在对话中使用时，也可以直接告诉 AI 助手你的 PDF 路径，让它帮你写入配置。

## 使用示例

对话中自然提问即可，例如：

- 「深蹲 1RM 怎么估算？书上怎么说的？」（→ 我会定位并核对书 P471~500）
- 「按第21章讲讲线性 vs 波浪周期」（→ 书 P623 起）
- 「考我第17章的抗阻训练计划设计」

## 兼容性

- **OpenCode**：原生支持（SKILL.md 目录式 / skills 配置源 / HTTP catalog 三种形态齐备）
- **其他支持 Agent Skills 规范的助手**：本包同时兼容 `.claude/skills`、`.agents/skills`
  两个兼容源位置；OpenCode V2 会自动搜索它们
- **模型无关**：DeepSeek、Claude、GPT、本地模型均可，技能跟随 OpenCode 而非模型

## 自行发布步骤

```bash
git init
git add .
git commit -m "feat: NSCA-CSCS skill package v1"
git remote add origin https://github.com/TonyStark868/nsca-cscs-skill.git
git push -u origin main
```

仓库地址已填入 `TonyStark868/nsca-cscs-skill`；如你 fork 或改名，请同步更新。

## 许可

本包内工具代码与笔记采用 MIT 许可；这不改变原书的版权归属。
