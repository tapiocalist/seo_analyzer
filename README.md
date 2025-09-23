# SEO 分析工具 (SEO Analyzer)

一个强大的客户端 SEO 分析工具，支持批量 URL 下载和多文件 SEO 分析，具备完整的数据导出功能。

## 🌟 功能特色

### 📥 批量 URL 下载

- 多行 URL 输入，批量下载 HTML 文件
- 实时进度跟踪，错误处理
- 自动文件命名：`hostname_timestamp_index.html`

### 📊 多文件 SEO 分析

- 支持多个 HTML 文件同时上传
- 增量文件添加（不覆盖已有文件）
- 智能重复文件检测
- 个性化补充信息输入

### 🔍 全面 SEO 分析

- **页面基础信息**：标题、描述、H1/H2 标签
- **内容统计**：单词数统计（纯内容，排除代码）
- **关键词密度**：1-4 词组合频率分析
- **SERP 竞争分析**：支持 Google 搜索结果格式

### 📋 数据导出功能

- **批量 Excel 导出**：TSV 格式，包含 19 个数据列
- **个人详情查看**：完整可视化分析界面
- **历史记录**：最近 10 条分析记录
- **数据持久化**：基于 localStorage 的状态管理

## 🚀 快速开始

### 方法 1：直接使用（推荐）

1. 下载或克隆项目
2. 直接在浏览器中打开 `index.html`
3. 开始使用

### 方法 2：HTTP 服务器

```bash
# 安装依赖
npm install

# 启动开发服务器
npm run dev

# 访问 http://localhost:8080
```

## 📖 使用指南

### 批量 URL 下载（第一部分）

1. 在文本框中输入 URL 列表（每行一个）
2. 点击"批量下载"
3. 等待下载完成，文件自动保存

### 多文件 SEO 分析（第二部分）

1. **上传文件**：选择多个 HTML 文件
   - 支持多次选择，新文件会累加到列表
   - 重复文件会自动跳过
2. **添加补充信息**：为每个文件填写个性化信息
   - 关键词数据（Tab 分隔格式）
   - SERP 链接（Google 搜索结果格式）
3. **批量分析**：点击"分析全部"
   - 实时显示分析进度
   - 支持错误处理和重试
4. **查看结果**：
   - **复制全部到 Excel**：获得多行 TSV 数据
   - **查看详情**：查看单个文件的完整分析

## 📊 Excel 导出格式

导出的 Excel 数据包含 19 列：

| 列名              | 说明             | 数据来源   |
| ----------------- | ---------------- | ---------- |
| 文件名            | HTML 文件名      | 上传的文件 |
| 关键词            | 目标关键词       | 补充信息   |
| URL               | 目标网址         | 补充信息   |
| 获得流量          | 预估流量         | 补充信息   |
| 搜索结果数量      | 搜索结果总数     | 补充信息   |
| Intitle           | Intitle 搜索结果 | 补充信息   |
| KD 难度           | 关键词难度       | 补充信息   |
| KGR               | 关键词黄金比例   | 自动计算   |
| 页面标题          | HTML 标题标签    | HTML 解析  |
| 页面描述          | Meta 描述标签    | HTML 解析  |
| H1                | H1 标签内容      | HTML 解析  |
| H2                | H2 标签内容      | HTML 解析  |
| 单词数            | 内容单词统计     | HTML 解析  |
| 1 词              | 单词关键词密度   | HTML 解析  |
| 2 词              | 双词关键词密度   | HTML 解析  |
| 3 词              | 三词关键词密度   | HTML 解析  |
| 4 词              | 四词关键词密度   | HTML 解析  |
| SERP 竞争分析标题 | 竞争对手标题     | 补充信息   |
| SERP 竞争分析网址 | 竞争对手网址     | 补充信息   |

## 📝 补充信息格式

### 关键词信息格式（Tab 分隔）

```
Keyword	URL	Search Volume	Traffic	Difficulty	CPC	Results	Intitle	Competition	Trend
ai kissing	https://example.com	1000	500	45	1.2	50000	200	Medium	Stable
```

### Google SERP 格式 - 直接从 Google 搜索结果复制

```
Generate AI Kissing Scenes from Two Photos for Free
Free AI Hug Video Generator: Make Two People Hug with AI

Fotor
https://www.fotor.com › AI Video Generator
Make people hugging video with Fotor AI hug video generator right now! Our AI can easily turn two images into an animated hugging video in a short time.
AI Hug Generator - Bring Emotions to Life

Dzine AI
https://www.dzine.ai › tools › ai-hug-generator
Dzine's hug generator makes two people hug with AI in just a few seconds, just by uploading a photo. No need to bother with complex prompts or perform any extra ...

```

## 🔧 技术架构

### 核心技术

- **纯前端应用**：无需后端服务器
- **单文件架构**：所有功能集成在 `index.html`
- **现代 JavaScript**：ES6+，async/await，FileReader API
- **数据持久化**：localStorage API
- **响应式设计**：适配不同屏幕尺寸

### 浏览器兼容性

支持现代浏览器（Chrome, Firefox, Safari, Edge）：

- Fetch API
- DOMParser
- FileReader API
- localStorage API
- Clipboard API

### 代理服务配置

为解决 CORS 问题，使用多个代理服务：

- `api.codetabs.com`
- `thingproxy.freeboard.io`
- `cors-anywhere.herokuapp.com`
- `crossorigin.me`
- `api.allorigins.win`

## 🎨 界面设计

### 设计理念

- **简洁高效**：专注核心功能，避免冗余
- **渐进式操作**：逻辑清晰的操作流程
- **状态管理**：智能按钮状态和进度显示

### 色彩方案

- **主色调**：`#644a40` (棕色)
- **背景色**：`#f9f9f9` (浅灰)
- **卡片色**：`#fcfcfc` (白色)
- **边框色**：`#d8d8d8` (灰色)
- **状态色**：绿色(良好)、橙色(警告)、红色(错误)

## 🐛 故障排除

### 常见问题

1. **SERP 链接不显示**

   - 检查格式是否包含 › 符号
   - 确保使用正确的 Google 搜索结果格式

2. **文件不持久化**

   - 检查浏览器 localStorage 权限
   - 清除浏览器缓存后重试

3. **分析失败**

   - 验证 HTML 文件格式和内容
   - 检查文件大小限制

4. **Excel 复制失败**

   - 使用手动复制对话框
   - 检查剪贴板权限

5. **重复文件检测**
   - 基于文件名和大小匹配
   - 修改文件名可绕过检测

### 调试信息

- 查看浏览器控制台的解析日志
- "Parsing completed. Found X SERP links" 表示解析成功
- 文件状态自动保存到 localStorage

### 性能提示

- 大文件(>5MB)处理时间较长
- 批量分析按顺序处理文件
- localStorage 有浏览器相关的大小限制(约 5-10MB)

## 📁 项目结构

```
seo_analyzer/
├── index.html                 # 主应用文件
├── README.md                  # 项目说明文档
├── CLAUDE.md                  # Claude Code开发文档
├── seo_tool_requirements.md   # 原始需求文档
├── settings.local.json        # Claude Code权限配置
├── vercel.json               # Vercel部署配置
└── package.json              # Node.js项目元数据
```

## 🚀 部署说明

### Vercel 部署

项目已配置 Vercel 自动部署：

- 推送到主分支自动触发部署
- 静态文件托管，无需构建过程
- 自动 HTTPS 和 CDN 加速

### 本地部署

无需构建过程，直接使用：

- 下载所有文件到本地
- 用浏览器打开 `index.html`
- 或使用任何 HTTP 服务器托管

## 🤝 贡献指南

1. Fork 项目
2. 创建功能分支
3. 提交变更
4. 推送到分支
5. 创建 Pull Request

## 📄 许可证

MIT License - 详见项目文件

## 🆘 支持

如遇问题或建议：

1. 查看故障排除部分
2. 检查浏览器控制台日志
3. 创建 Issue 描述问题

---

**开发者提示**：本项目专为 SEO 分析师和内容营销人员设计，提供高效的批量分析和数据导出功能。
