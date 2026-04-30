# PM Skills 产品经理技能集群 - 完整设计文档

> 创建时间：2025-04-30
> 状态：已完成
> 标签：#PM #AI-Agent #Skill #产品经理 #Hermes

---

## 一、项目概述

### 1.1 背景

**kakuka/icemark** 是 GitHub 上的一个 VSCode 扩展项目，专门为产品经理提供 AI 辅助能力。其核心能力包括：
- Market Mode（市场分析）
- PRD Mode（需求文档）
- Prototype Mode（原型生成）
- Icemark Mode（通用助手）

将 icemark 的核心能力移植到 Hermes Agent 框架，可以脱离 VSCode 依赖，直接在 Hermes 中实现相同功能，并利用 Hermes 的跨平台能力（飞书、微信等）进行交付。

### 1.2 目标

在 Hermes 中创建一套完整的 PM（产品经理）技能集群，实现：
- 市场分析自动化
- PRD 文档智能生成
- 原型快速生成
- 调研工具集合
- 通用 AI 助手能力

### 1.3 设计原则

1. **单一职责**：每个 Skill 专注完成一个功能
2. **可组合**：各 Skill 可独立使用，也可组合工作
3. **交付飞书**：主要交付平台为飞书云文档和多维表格
4. **原生增强**：充分利用 Hermes 已有工具和能力

---

## 二、Skill 架构设计

### 2.1 整体架构

```
pm-assistant (入口/协调者)
    │
    ├── pm-market-analysis (市场分析专家)
    ├── pm-prd-writing (PRD写作助手)
    ├── pm-prototype-gen (原型生成工具)
    ├── pm-excalidraw-prototype (草图转原型)
    ├── pm-research-tools (调研工具集)
    │
    └── 交付层
            ├── lark-doc (飞书云文档)
            └── lark-base (飞书多维表格)
```

### 2.2 Skill 列表

| # | Skill 名称 | 定位 | 核心功能 | 交付方式 |
|---|-----------|------|---------|---------|
| 1 | pm-assistant | 通用PM助手 | 规划/分析/执行/任务管理 | 飞书云文档 |
| 2 | pm-market-analysis | 市场分析专家 | SWOT/PESTEL/波特五力分析 | 飞书云文档 |
| 3 | pm-prd-writing | PRD文档助手 | 用户故事/JTBD/三问法 | 飞书云文档 + 多维表格 |
| 4 | pm-prototype-gen | 快速原型生成 | 文本需求 → HTML原型 | 本地 .html |
| 5 | pm-excalidraw-prototype | 草图转原型 | Excalidraw JSON → HTML | 本地 .html |
| 6 | pm-research-tools | 调研工具集 | 搜索/抓取/解析 | 飞书云文档 |

---

## 三、详细功能说明

### 3.1 pm-market-analysis（市场分析专家）

#### 定位
专业化市场调研与竞争分析工具，生成结构化市场报告。

#### 核心能力
- SWOT 分析
- PESTEL 分析
- Porter 五力模型
- 4P 营销分析
- 用户画像分析

#### 输入
- 分析对象（产品/行业/市场）
- 分析维度（指定框架或全面分析）
- 交付格式偏好

#### 工作流程
```
1. 多源搜索 → 2. 内容抓取 → 3. 结构化分析 → 4. 报告生成 → 5. 交付飞书
```

#### 输出
```markdown
# [产品/市场] 市场分析报告

## 执行摘要
## 一、市场概况
## 二、竞争格局分析
## 三、用户洞察
## 四、发展趋势
## 五、SWOT/PESTEL/五力分析
## 六、机会与风险
## 七、战略建议
```

#### 依赖工具
- browser_navigate / browser_snapshot
- fetch-web-article
- lark-doc

---

### 3.2 pm-prd-writing（PRD文档助手）

#### 定位
专业产品需求文档生成，基于专业需求挖掘方法论。

#### 核心方法论
- **三问法**：用户遇到什么问题 → 现在怎么解决 → 建议怎么解决
- **JTBD**：用户"雇用"产品完成的工作
- **四大驱动力**：推力(PUSH)、拉力(PULL)、焦虑(ANXIETY)、习惯(HABIT)
- **用户故事格式**：As a / I want / So that

#### 输入
- 产品名称/背景
- 目标用户
- 核心功能点
- 用户痛点

#### 工作流程
```
1. 需求挖掘(三问法+JTBD) → 2. 用户故事梳理 → 3. 功能拆解 → 4. PRD文档生成 → 5. 任务清单生成 → 6. 交付飞书
```

#### 输出
1. **PRD 文档**（飞书云文档）
2. **任务清单**（飞书多维表格）

```markdown
# [产品名称] 产品需求文档 (PRD)

## 1. 概述
## 2. 用户与场景
## 3. 用户故事地图
## 4. 功能需求详情
## 5. 非功能性需求
## 6. 优先级与迭代计划
## 7. 附录
```

#### 依赖工具
- lark-doc
- lark-base
- browser（竞品参考搜索）

---

### 3.3 pm-prototype-gen（快速原型生成）

#### 定位
基于文本需求描述，快速生成可交互 HTML 原型。

#### 核心能力
- 多平台支持（Web/iOS/Android/通用）
- TailwindCSS 美化
- 基础交互（Tab切换/弹窗/表单）
- 响应式布局

#### 输入
- 产品/功能名称
- 核心功能描述
- 目标平台
- 设计风格偏好

#### 工作流程
```
1. 需求解析 → 2. 页面结构设计 → 3. HTML生成 → 4. 交互实现 → 5. 文件交付
```

#### 输出
独立 `.html` 文件，可直接在浏览器打开

#### 原型特点
- 使用 TailwindCSS CDN
- 组件化代码结构
- 3-5 个核心页面
- 现代化 UI 设计

#### 依赖工具
- write_file
- terminal（本地服务器测试）

---

### 3.4 pm-excalidraw-prototype（草图转原型）

#### 定位
将 Excalidraw 手绘线框图转换为可交互 HTML 原型。

#### 核心能力
- Excalidraw JSON 解析
- 元素类型识别（矩形→按钮/卡片、文字→标签）
- 页面结构识别
- 交互绑定识别
- 样式保持与美化

#### 输入
- Excalidraw JSON 文件
- 目标平台（可选）
- 交互需求（可选）

#### 工作流程
```
1. 获取Excalidraw JSON → 2. 解析元素结构 → 3. 元素分类映射 → 4. 识别交互绑定 → 5. 生成HTML原型 → 6. 文件交付
```

#### 元素映射规则
| Excalidraw 元素 | 映射为 HTML 组件 |
|----------------|----------------|
| Rectangle(小+圆角) | `<button>` |
| Rectangle(大) | `<div>` 卡片/容器 |
| Text | `<span>` / `<label>` |
| Line/Arrow | 页面跳转指示 |
| Image | `<img>` |
| 页面分组 | 多个 `<div class="page">` |

#### 输出
可交互 HTML 原型文件

#### 依赖工具
- read_file
- write_file
- execute_code（JSON解析）

---

### 3.5 pm-research-tools（调研工具集）

#### 定位
PM 日常调研的常用工具集合，涵盖信息收集、内容分析、文档处理。

#### 核心工具

| 工具类别 | 功能 | 数据源 |
|---------|------|--------|
| 多搜索引擎 | Bing/Google/百度/搜狗/DuckDuckGo | 网络 |
| 网页抓取 | 知乎/小红书/微博/公众号/科技媒体 | 内容平台 |
| 文档解析 | PDF/Word/Excel/PPT/Markdown | 本地文件 |
| 社交提取 | 用户评价/讨论/反馈分析 | 社交平台 |

#### 输入
- 调研主题
- 关键问题
- 信息来源偏好

#### 工作流程
```
1. 明确调研目标 → 2. 多引擎搜索 → 3. 内容抓取 → 4. 文档解析 → 5. 信息整理 → 6. 交付
```

#### 输出
结构化调研报告，包含：
- 搜索结果汇总
- 抓取内容摘要
- 文档解析数据
- 洞察总结

#### 依赖工具
- browser_navigate / browser_snapshot
- fetch-web-article
- ocr-and-documents
- write_file
- lark-doc

---

### 3.6 pm-assistant（通用PM助手）

#### 定位
产品经理全能 AI 助手，复杂任务的入口和协调者。

#### 核心能力
- 智能规划（项目拆解/里程碑/优先级）
- 专业分析（数据/竞品/用户/趋势）
- 内容撰写（PRD/报告/邮件/周报）
- 问题解决（诊断/方案/决策）
- 任务管理（Task Manifest 系统）

#### 特色功能：Task Manifest
结构化任务清单，支持中断和恢复。

```markdown
## 📋 产品上线 Task Manifest

| # | 任务 | 状态 | 下一步 |
|---|------|------|--------|
| 1 | 市场调研 | ✅ 完成 | → 2 |
| 2 | 需求分析 | 🔄 进行中 | → 3 |
| 3 | 产品设计 | ⏳ 待开始 | → 4 |
```

#### 支持的命令
- `继续任务` - 恢复中断的任务
- `暂停任务` - 保存进度
- `查看清单` - 显示所有任务状态
- `完成任务` - 标记完成
- `添加/删除任务` - 调整清单

#### 与其他 Skill 的关系
pm-assistant 作为入口，根据任务类型调用专业 Skill：
- 市场分析 → pm-market-analysis
- PRD撰写 → pm-prd-writing
- 原型生成 → pm-prototype-gen
- 草图转换 → pm-excalidraw-prototype
- 调研任务 → pm-research-tools

#### 交付选项
- 直接对话
- 飞书云文档
- 飞书多维表格
- 本地文件

---

## 四、技术实现

### 4.1 Skill 文件结构

```
~/.hermes/skills/productivity/
├── pm-assistant/
│   └── SKILL.md
├── pm-market-analysis/
│   └── SKILL.md
├── pm-prd-writing/
│   └── SKILL.md
├── pm-prototype-gen/
│   └── SKILL.md
├── pm-excalidraw-prototype/
│   └── SKILL.md
└── pm-research-tools/
    └── SKILL.md
```

### 4.2 依赖的 Hermes 内置 Skill

| 依赖 Skill | 用途 |
|-----------|------|
| lark-doc | 飞书云文档写入 |
| lark-base | 飞书多维表格操作 |
| fetch-web-article | 网页内容抓取 |
| ocr-and-documents | 文档 OCR 解析 |
| excalidraw | Excalidraw 解析 |

### 4.3 技术特点

1. **基于 RooCode**：icemark 基于 RooCode 3.15.5，Hermes 是更现代的 Agent 框架
2. **TypeScript → 自然语言**：icemark 用 TypeScript 实现的功能，转换为 LLM + 工具链
3. **VSCode → 跨平台**：脱离 VSCode 依赖，通过 Hermes 接入飞书等平台
4. **本地生成 → 云端交付**：原型本地生成，文档直接写入飞书

---

## 五、使用示例

### 5.1 市场分析任务

```
用户：加载 pm-market-analysis
分析：国内在线文档协作工具市场

助手：
我将进行深度市场分析...

## 搜索阶段
正在搜索：在线文档协作工具 市场规模
正在搜索：Notion/飞书/腾讯文档 竞品分析
正在抓取：相关行业报告和文章

## 分析阶段
采用 PESTEL + SWOT 双框架分析

## 输出
✅ 市场分析报告已完成

📄 飞书云文档：https://feishu.cn/xxx
```

### 5.2 PRD 撰写任务

```
用户：加载 pm-prd-writing
产品：团队知识库工具
目标用户：中小企业团队
核心功能：文档协作/搜索/权限管理

助手：
我来为你创建完整PRD...

## 需求挖掘（三问法）
Q1: 用户遇到什么问题？
→ 团队知识分散、查找困难、信息不对称

Q2: 现在怎么解决？
→ 微信群/邮件/本地文档，碎片化严重

Q3: 建议怎么解决？
→ 统一知识管理平台，支持搜索和权限

## 生成内容
✅ PRD 文档已生成
✅ 任务清单已创建

📄 飞书云文档：https://feishu.cn/xxx
📊 飞书多维表格：https://feishu.cn/xxx
```

### 5.3 原型生成任务

```
用户：加载 pm-prototype-gen
产品名：任务管理App
功能：任务创建/分配/追踪/完成
平台：iOS

助手：
正在生成原型...

## 设计页面
1. 首页（今日任务概览）
2. 任务列表页
3. 任务详情页
4. 创建/编辑任务页
5. 个人设置页

## 交互实现
- Tab导航切换
- 弹窗选择日期/人员
- 滑动完成任务

✅ 原型已生成

💾 文件：~/.hermes/pm-prototypes/任务管理App_20250430.html
```

### 5.4 草图转原型任务

```
用户：加载 pm-excalidraw-prototype
文件：~/sketches/login-page.json

助手：
正在解析 Excalidraw JSON...

## 识别结果
- 页面1：登录页（Logo/输入框/按钮）
- 页面2：注册页（表单）
- 页面3：忘记密码页

## 元素映射
- 矩形(小) × 3 → 按钮
- 输入框(大) × 4 → 表单输入框
- 文字 × 8 → 标签

## 交互绑定
- 登录按钮 → 跳转首页
- 注册链接 → 跳转注册页
- 忘记密码 → 跳转密码页

✅ 原型已生成

💾 文件：~/.hermes/pm-prototypes/excalidraw_login-page_20250430.html
```

---

## 六、版本规划

### v1.0（当前版本）
- [x] 6个核心 Skill 创建完成
- [x] 基础功能可用
- [x] 飞书交付集成

### v1.1（计划中）
- [ ] 添加 PRD 模板库
- [ ] 添加市场分析报告模板
- [ ] 原型模板优化

### v1.2（计划中）
- [ ] Excalidraw 元素识别准确率提升
- [ ] 支持更多社交平台内容抓取
- [ ] Task Manifest 持久化

---

## 七、参考资料

- icemark GitHub: https://github.com/kakuka/icemark
- icemark 官网: https://icemark.tech
- Hermes Skills 文档

---

## 八、附录

### 术语表

| 术语 | 说明 |
|------|------|
| PM | Product Manager，产品经理 |
| PRD | Product Requirement Document，产品需求文档 |
| JTBD | Jobs-to-be-Done，用户想完成的工作 |
| SWOT | Strengths/Weaknesses/Opportunities/Threats，优势劣势机会威胁 |
| PESTEL | Political/Economic/Social/Technological/Environmental/Legal |
| Task Manifest | 任务清单系统，支持中断恢复 |
| Excalidraw | 手绘风格线框图工具 |

### Skill 快速索引

| 命令 | Skill | 用途 |
|------|-------|------|
| 加载 pm-assistant | 通用助手 | PM日常工作辅助 |
| 加载 pm-market-analysis | 市场分析 | 行业/竞品调研报告 |
| 加载 pm-prd-writing | PRD助手 | 需求文档生成 |
| 加载 pm-prototype-gen | 原型生成 | 文本→HTML原型 |
| 加载 pm-excalidraw-prototype | 草图转原型 | Excalidraw→HTML |
| 加载 pm-research-tools | 调研工具 | 搜索/抓取/解析 |

---

*本文档由 Hermes Agent 自动生成*
*最后更新：2025-04-30*
