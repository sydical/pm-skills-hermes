---
name: pm-excalidraw-prototype
description: PM Excalidraw草图转原型 - 将Excalidraw手绘线框图转换为可交互HTML原型
category: productivity
---

# pm-excalidraw-prototype

将 Excalidraw 手绘线框图转换为可交互 HTML 原型的技能。识别 Excalidraw JSON 中的图形元素，映射为标准 UI 组件，生成可交互原型。

## 使用场景

- 产品经理手绘草图快速转化为高保真原型
- 设计评审时快速验证交互逻辑
- 团队沟通时的可视化原型展示
- 低保真到中保真原型的快速升级

## 输入

用户提供：
- **Excalidraw JSON**：从 Excalidraw 导出的 `.json` 文件
- **目标平台**（可选）：Web / iOS / Android / 通用
- **交互需求**（可选）：页面跳转 / 弹窗 / 表单 等

## 工作流程

### Step 1: 获取 Excalidraw JSON

用户提供文件，或从以下位置读取：
```
1. 本地文件路径：~/.hermes/excalidraw/*.json
2. 用户直接粘贴 JSON 内容
3. Excalidraw 导出的文件
```

### Step 2: 解析 Excalidraw 结构

```python
# Excalidraw JSON 结构
{
  "type": "excalidraw",
  "version": 2,
  "elements": [
    {
      "id": "xxx",
      "type": "rectangle",      # rectangle/ellipse/line/text/image
      "x": 100,
      "y": 100,
      "width": 200,
      "height": 100,
      "fillStyle": "solid",
      "strokeColor": "#1a1a1a",
      "backgroundColor": "#ffffff",
      "text": "按钮文字",        # 如果是文字元素
      "links": {},              # 链接信息
      "boundElements": []       # 绑定元素（用于交互）
    }
  ]
}
```

### Step 3: 元素分类映射

| Excalidraw 元素 | 映射为 HTML 组件 |
|----------------|----------------|
| Rectangle | `<button>` / `<div>` 卡片 |
| Ellipse | `<button>` 圆形元素 |
| Text | `<span>` / `<label>` 文字 |
| Line / Arrow | `<hr>` / `<svg>` 箭头 |
| Image | `<img>` 图片 |
| 页面分组 (Page) | `<div>` 多个页面 |

### Step 4: 识别交互绑定

```
Excalidraw 绑定元素 (boundElements) 解析：
1. 点击区域 → 绑定目标页面/弹窗
2. 箭头连接 → 页面跳转关系
3. 文字标注 → 交互说明
```

### Step 5: 生成 HTML 原型

```
输出包含：
- 完整 HTML + CSS + JavaScript
- 多页面支持（通过 Tab/导航切换）
- 弹窗交互
- 响应式布局
```

### Step 6: 文件交付

```
1. 保存 HTML 文件到本地
2. 返回文件路径
3. 可选：提供浏览器预览方式
```

## 解析脚本逻辑

```python
# 伪代码：Excalidraw JSON → HTML 转换

def parse_excalidraw(json_data):
    elements = json_data["elements"]
    
    # 1. 按页面分组
    pages = group_by_page(elements)
    
    # 2. 识别组件
    components = []
    for elem in elements:
        if elem["type"] == "rectangle":
            # 判断是按钮还是卡片
            if is_button(elem):
                components.append(Button(elem))
            else:
                components.append(Card(elem))
        elif elem["type"] == "text":
            components.append(Text(elem))
        # ... 其他类型
    
    # 3. 识别交互
    interactions = find_bindings(elements)
    
    return pages, components, interactions

def generate_html(pages, components, interactions):
    html = Template.render(pages, components, interactions)
    return html
```

## 元素识别规则

### 按钮识别
```
条件：
- width < 200px
- height < 60px
- 形状为圆角矩形
- 位置在可点击区域

映射：<button class="btn-primary">
```

### 卡片识别
```
条件：
- width >= 200px
- 包含内部元素
- 无绑定交互

映射：<div class="card">
```

### 页面识别
```
条件：
- 元素数量 > 10
- 占满整个画布
- 或有明确的"页面标题"文字

映射：多个 HTML <div class="page">
```

## 生成的原型特点

### 样式保持
```
- 线条颜色 → CSS border/color
- 填充颜色 → CSS background
- 圆角 → CSS border-radius
- 字体 → 映射为系统字体
- 位置 → CSS absolute 定位
```

### 交互实现
```
1. 页面切换
   - Tab 导航栏
   - 点击按钮跳转页面

2. 弹窗交互
   - 点击触发弹窗显示
   - 点击遮罩关闭弹窗

3. 表单交互
   - 输入框聚焦效果
   - 提交按钮反馈
```

## 提示语模板

```
你是 Excalidraw 原型转换专家，擅长将手绘线框图转换为高保真可交互原型。

请将用户提供的 Excalidraw JSON 转换为 HTML 原型：

**要求**：
1. 解析 Excalidraw JSON 中的所有元素
2. 将矩形映射为按钮/卡片/容器
3. 将文字映射为标签/标题
4. 识别页面结构（多个场景分组）
5. 实现基础交互（页面切换/弹窗）
6. 使用 TailwindCSS CDN 进行样式美化
7. 保持原始草图的布局结构

**转换规则**：
- 矩形(小) + 圆角 → 按钮
- 矩形(大) → 卡片/容器
- 文字 → 文本标签
- 箭头 → 页面跳转指示

请生成完整的 HTML 代码，包含多页面和交互功能。
```

## 依赖工具

- `read_file` - 读取 Excalidraw JSON 文件
- `write_file` - 保存生成的 HTML 文件
- `execute_code` - 执行 Python 脚本进行 JSON 解析和转换

## 输出文件

```
保存位置：~/.hermes/pm-prototypes/excalidraw_[原文件名]_[时间戳].html
例如：~/.hermes/pm-prototypes/excalidraw_sketch_20250430_143020.html
```

## 注意事项

1. **JSON 格式**：确保用户提供的是 Excalidraw 导出的标准 JSON

2. **元素完整性**：复杂草图可能需要手动补充

3. **尺寸单位**：Excalidraw 使用 1x 坐标，需按比例转换

4. **中文支持**：确保字体支持中文显示

5. **多页面识别**：建议在 Excalidraw 中用不同页面区分不同界面

## 验证方式

- HTML 文件可在浏览器中打开
- 草图中的主要元素被正确识别
- 页面切换功能正常
- 弹窗交互可正常使用
- UI 相比原草图有美化提升

## 进阶功能（可选）

1. **样式增强**：在原草图基础上添加配色和图标
2. **数据模拟**：添加模拟数据展示
3. **响应式适配**：生成多端响应式版本
4. **导出分享**：生成可在线访问的链接
