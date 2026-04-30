# Hermes PM Skills - 产品经理技能集群

> 将 kakuka/icemark 的核心能力移植到 Hermes Agent

## 📦 包含技能

| Skill | 说明 | 交付 |
|-------|------|------|
| `pm-assistant` | 通用PM助手，支持任务清单管理 | 飞书云文档 |
| `pm-market-analysis` | 市场分析（SWOT/PESTEL/波特五力） | 飞书云文档 |
| `pm-prd-writing` | PRD文档（用户故事/JTBD/三问法） | 飞书云文档 + 多维表格 |
| `pm-prototype-gen` | 文本需求 → HTML交互原型 | 本地 .html |
| `pm-excalidraw-prototype` | Excalidraw草图 → HTML原型 | 本地 .html |
| `pm-research-tools` | 调研工具集（搜索/抓取/解析） | 飞书云文档 |

## 🏗️ 架构

```
pm-assistant（入口/协调者）
    ├── pm-market-analysis
    ├── pm-prd-writing
    ├── pm-prototype-gen
    ├── pm-excalidraw-prototype
    └── pm-research-tools

交付层：lark-doc（飞书云文档）+ lark-base（飞书多维表格）
```

## 📥 安装

将 skill 文件夹复制到 Hermes Skills 目录：

```bash
cp -r pm-* ~/.hermes/skills/productivity/
```

## 🚀 使用

```
加载 pm-market-analysis
分析：某产品市场分析

加载 pm-prd-writing
产品：xxx，目标用户：xxx

加载 pm-prototype-gen
产品名：xxx，功能描述：xxx
```

## 📚 文档

详细设计文档：[PM-Skills-设计完整方案.md](./PM-Skills-设计完整方案.md)

## 🔗 参考

- 原始项目：[kakuka/icemark](https://github.com/kakuka/icemark)
- Hermes Agent

---

*MIT License*
