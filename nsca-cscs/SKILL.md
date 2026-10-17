---
name: NSCA-CSCS 指南助手
description: 基于本地教材《NSCA-CSCS美国国家体能协会体能教练认证指南（第4版）》的体能训练知识助手。当用户讨论体能训练、力量/爆发力训练、训练计划设计、测试与评估、营养与补剂、周期化、损伤康复、场地与法律风险管理，或提到 CSCS 认证备考、要求按该书出题/讲解/查证某章某页内容时使用。技能未配置书籍路径时会先询问用户本地扫描件位置。
---

# NSCA-CSCS 指南助手

本地教材：《NSCA-CSCS美国国家体能协会体能教练认证指南（第4版）》，共 24 章 + 附录，
通常为扫描版 PDF（无文字层），需要用技能自带的 OCR 脚本按需调取页面。

## 资源位置（相对本技能目录）

- 章节索引：`references/chapter-index.md`（24 章的书页码 → PDF 页码、作者、子节地图）
- 要点提炼：`references/key-concepts.md`（各章核心概念与常用公式，自组织转述）
- 按页 OCR 工具：`scripts/ocr_pages.py`
- 依赖：`pip install -r scripts/requirements.txt`（pymupdf, rapidocr-onnxruntime, numpy）

## 书籍定位（三选一，按优先级）

1. 调用脚本时传 `--pdf "<路径>"`
2. 环境变量 `NSCA_CSCS_PDF` 指向 PDF 绝对路径
3. 本技能目录下 `references/book-path.txt`（首行为 PDF 绝对路径）

**若三者均未配置**：询问用户他们保有的本地书扫描件路径；若技能目录可写，将路径
写入 `references/book-path.txt` 供下次使用；同时提示运行
`pip install -r scripts/requirements.txt` 安装依赖。

## 页码换算规则（已多点校验）

- **PDF 页码 = 书内页码 + 14**
- 书第 1~806 页 → PDF 第 15~820 页
- 前言部分（PDF 1~14）：封面 1~2、译者序 3~4、目录 5~9、前言 10~11

## 工作流程

1. **定位**：先读 `references/chapter-index.md`，把用户的问题映射到具体章节和书页范围。
2. **初答**：概念性问题优先用 `references/key-concepts.md` 中的要点提炼回答。
3. **查证**：当必须给出原文细节（具体数字、表格、协议步骤）时，
   用 `scripts/ocr_pages.py` 调取对应书页，以识别结果为准，不要凭记忆猜数字。
4. **标注出处**：引用教材内容时注明书页码（如"见书 P473"），方便用户对照。
5. **引用规范**：该书为版权出版物。回答以转述和总结为主，直接引用只限简短片段
   （学习辅导用途），不要整页大段复制；也绝不要把 OCR 的批量文本存入技能文件。
6. **备考模式**：用户说"考我/出几道题"时，按其指定章节出选择题并逐项讲解；出题前
   可先 OCR 该章的知识要点块和章末试题页核对考点。

## OCR 工具用法

```
python "<本技能目录>/scripts/ocr_pages.py" <书页码> [更多页码或范围如 47-50] [--pdf 路径] [--dpi 150~250] [--force]
```

示例：

```
python scripts/ocr_pages.py 473
python scripts/ocr_pages.py 483-500 --dpi 200
```

- 结果缓存于 `%TEMP%\nsca-cscs-ocr-cache`（或 `~/.cache/nsca-cscs-ocr-cache`），
  同一页重复调用立即返回缓存；`--force` 强制重新识别。
- 单页约 8~10 秒；OCR 大范围页面前先规划好只取所需页。
- 建议用 `-X utf8` 运行避免 Windows 控制台编码问题。
