---
name: pm-prototype-gen
description: PM快速原型生成 - 基于文本需求描述生成HTML交互原型，支持Web/iOS/Android多端设计
category: productivity
---

# pm-prototype-gen

产品经理快速原型生成技能。输入产品需求描述，自动生成可交互的HTML原型文件，支持多平台（Web/iOS/Android）设计。

## 使用场景

- 产品经理快速验证概念想法
- 需求沟通时的可视化原型展示
- 低保真原型快速输出
- 设计评审前的原型准备

## 输入

用户提供：
- **产品/功能名称**：要做什么
- **核心功能描述**：主要页面和交互逻辑
- **目标平台**：Web / iOS / Android / 通用
- **设计风格**（可选）：简约 / 现代 / 专业

## 输出

生成独立的 `.html` 文件，包含：
- 完整 HTML + CSS + JavaScript
- 现代化 UI 设计
- 基本交互功能（点击、切换、弹窗等）
- 可直接在浏览器中打开

## 工作流程

### Step 1: 需求解析
```
分析用户输入，提取：
1. 核心页面结构
2. 功能模块划分
3. 交互行为定义
4. 数据展示需求
```

### Step 2: 原型设计
```
确定页面和组件：
1. 页面列表（首页/列表页/详情页/设置页等）
2. 导航结构（底部Tab/侧边栏/顶部导航）
3. 核心组件（卡片/列表/表单/弹窗）
4. 交互状态（默认/hover/active/disabled）
```

### Step 3: HTML生成
```
生成现代化HTML原型：
- 使用 TailwindCSS CDN 样式
- 响应式布局适配多端
- 组件化代码结构
- 可读的注释说明
```

### Step 4: 交互实现
```
添加基础交互：
- 页面切换（Tab/导航）
- 弹窗打开/关闭
- 表单交互（输入/选择）
- 列表点击反馈
```

### Step 5: 文件交付
```
1. 生成 HTML 文件保存到本地
2. 可选上传到可访问的服务器
3. 返回文件路径或访问链接
```

## 原型模板结构

### 通用页面模板

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>[产品名称] - 原型</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        /* 自定义样式 */
    </style>
</head>
<body class="bg-gray-100">
    <!-- 顶部导航 -->
    <header class="bg-white shadow-sm sticky top-0 z-50">
        <!-- 导航内容 -->
    </header>
    
    <!-- 主内容区 -->
    <main class="pb-20">
        <!-- 页面内容 -->
    </main>
    
    <!-- 底部导航（移动端） -->
    <nav class="fixed bottom-0 left-0 right-0 bg-white border-t">
        <!-- Tab导航 -->
    </nav>
</body>
</html>
```

### iOS 原型模板特点
```css
/* iOS风格 */
border-radius: 12px;
font-family: -apple-system, BlinkMacSystemFont, 'SF Pro Text';
/* 安全区域适配 */
padding-bottom: env(safe-area-inset-bottom);
```

### Android 原型模板特点
```css
/* Material Design风格 */
border-radius: 8px;
font-family: 'Roboto', sans-serif;
/* 状态栏/导航栏高度 */
```

## 提示语模板

```
你是专业的交互原型设计师，擅长生成高保真HTML原型。

请基于以下需求生成可交互的HTML原型：

**产品名称**：[名称]
**目标平台**：[Web/iOS/Android/通用]
**核心功能**：
1. [功能1]
2. [功能2]
3. [功能3]

**页面要求**：
- 首页：展示核心内容
- 列表页：展示数据列表
- 详情页：展示详细信息
- [其他页面]

**交互需求**：
- [Tab切换/弹窗/表单等]

要求：
1. 使用 TailwindCSS CDN 进行样式设计
2. 代码结构清晰，有注释说明
3. 原型需包含3-5个核心页面
4. 添加基本交互功能
5. 适配 [目标平台] 尺寸
6. UI风格：现代化、简洁、专业

请生成完整的HTML代码，并保存为 .html 文件。
```

## 生成的原型示例

### 电商类原型
```
页面：首页 → 商品列表 → 商品详情 → 购物车 → 结算
交互：轮播图/加购/收藏/表单填写
```

### 社交类原型
```
页面：发现 → 动态列表 → 发布 → 个人主页 → 消息
交互：点赞/评论/分享/发布内容
```

### 工具类原型
```
页面：首页 → 功能模块 → 设置 → 关于
交互：功能卡片/开关设置/表单配置
```

## 组件库

### 常用组件

| 组件 | 说明 | 代码 |
|------|------|------|
| 顶部导航栏 | 带标题和操作按钮 | `<header>` |
| 底部Tab | 4-5个Tab切换 | `<nav>` |
| 卡片 | 产品/内容卡片 | `<div class="card">` |
| 列表项 | 左图右文结构 | `<ul><li>` |
| 按钮 | 主按钮/次按钮 | `<button>` |
| 输入框 | 表单输入 | `<input>` |
| 弹窗 | Modal/Dialog | `<dialog>` |
| 轮播图 | 图片轮播 | JS实现 |

### 配色方案

| 风格 | 主色 | 辅色 | 背景色 |
|------|------|------|--------|
| 专业商务 | #1a73e8 | #34a853 | #f8f9fa |
| 活力年轻 | #ff6b6b | #4ecdc4 | #ffffff |
| 简约科技 | #6366f1 | #8b5cf6 | #fafafa |

## 依赖工具

- `write_file` - 保存HTML文件
- `terminal` - 可选：启动本地服务器测试

## 输出文件

```
保存位置：~/.hermes/pm-prototypes/[产品名]_[时间戳].html
例如：~/.hermes/pm-prototypes/电商App_20250430_143020.html
```

## 注意事项

1. **尺寸适配**：根据目标平台选择合适尺寸
   - Web: 1920px / 1440px / 1024px
   - iOS: 375px (iPhone) / 414px (大屏)
   - Android: 360px / 412px

2. **交互适度**：原型交互应服务于功能表达，不要过度设计

3. **可读性**：代码需有注释，方便后续修改

4. **无外部依赖**：使用CDN，生成文件可离线打开

5. **浏览器兼容**：使用标准HTML5 + CSS3

## 验证方式

- HTML文件可正常在浏览器中打开
- 包含至少3个页面
- 有Tab导航或页面切换功能
- 至少一个交互功能可用（弹窗/表单等）
- UI风格现代化
