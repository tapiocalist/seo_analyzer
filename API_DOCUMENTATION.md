# API文档 - SEO分析工具

本文档详细说明了SEO分析工具中的主要函数和接口。

## 核心分析函数

### `analyzePage(html, url)`
主要的HTML页面分析函数。

**参数：**
- `html` (string): HTML内容字符串
- `url` (string): 页面URL或文件名

**返回值：**
```javascript
{
  url: string,           // 页面URL
  title: string,         // 页面标题
  description: string,   // Meta描述
  h1: array,            // H1标签数组
  headings: array,      // 所有标题标签 [{level: 1, text: "标题"}]
  wordCount: number,    // 单词数
  charCount: number,    // 字符数
  keywords: object,     // 关键词密度 {single:[], double:[], triple:[], quadruple:[]}
  images: number,       // 图片数量
  links: number         // 链接数量
}
```

**示例：**
```javascript
const analysis = analyzePage('<html>...</html>', 'example.html');
console.log(analysis.title); // 页面标题
```

### `parseKeywordAndSerpData(data)`
解析补充信息中的关键词和SERP数据。

**参数：**
- `data` (string): 补充信息文本

**返回值：**
```javascript
{
  keywordInfo: {
    keyword: string,     // 关键词
    url: string,         // 目标URL
    volume: string,      // 搜索量
    traffic: string,     // 获得流量
    difficulty: string,  // 难度
    cpc: string,         // CPC
    results: string,     // 搜索结果数
    intitle: string,     // Intitle结果数
    competition: string, // 竞争度
    trend: string        // 趋势
  },
  serpLinks: [
    {
      title: string,     // SERP标题
      url: string,       // SERP URL
      site: string       // 网站名称
    }
  ]
}
```

## 文件处理函数

### `handleFileSelection(event)`
处理文件选择事件，支持多文件累加。

**参数：**
- `event` (Event): 文件输入事件对象

**功能：**
- 将新选择的文件添加到现有列表
- 自动检测重复文件（基于文件名和大小）
- 更新文件列表显示

### `analyzeFileContent(file)`
异步分析单个文件内容。

**参数：**
- `file` (File): HTML文件对象

**返回值：**
- Promise<analysis> - 返回分析结果对象

**示例：**
```javascript
const analysis = await analyzeFileContent(file);
console.log(analysis.wordCount);
```

### `analyzeAllFiles()`
批量分析所有上传的文件。

**功能：**
- 遍历所有上传文件进行分析
- 显示实时进度
- 处理分析错误
- 更新按钮状态

**流程：**
1. 验证文件列表
2. 循环处理每个文件
3. 解析补充信息
4. 存储分析结果
5. 启用操作按钮

## 数据导出函数

### `copyAllToExcel()`
将所有分析结果导出为Excel格式。

**功能：**
- 生成19列的TSV格式数据
- 包含文件名、关键词指标、页面信息、SERP数据
- 支持剪贴板API和手动复制

**导出列结构：**
```javascript
const headers = [
  '文件名', '关键词', 'URL', '获得流量', '搜索结果数量', 'Intitle', 'KD难度', 'KGR',
  '页面标题', '页面描述', 'H1', 'H2', '单词数',
  '1词', '2词', '3词', '4词',
  'SERP竞争分析标题', 'SERP竞争分析网址'
];
```

### `copyToExcel()`
单文件Excel导出（用于详情查看）。

**功能：**
- 导出单个文件的分析结果
- 与批量导出格式一致
- 支持当前显示的分析数据

## 界面管理函数

### `displayFileList()`
显示文件列表界面。

**功能：**
- 生成文件项HTML
- 创建补充信息输入框
- 管理按钮状态
- 绑定事件处理器

### `displayResults(analysis, supplementInfo)`
显示分析结果的主界面。

**参数：**
- `analysis` (object): 分析结果对象
- `supplementInfo` (object): 补充信息对象

**功能：**
- 渲染页面信息
- 显示关键词密度
- 展示SERP竞争分析
- 生成可视化图表

### `viewFileDetails(fileIndex)`
查看单个文件的详细分析。

**参数：**
- `fileIndex` (number): 文件在列表中的索引

**功能：**
- 获取分析结果
- 使用原有界面显示
- 添加导航控制

## 数据持久化函数

### `saveFileData(fileName, htmlContent, analysisData)`
保存文件数据到localStorage。

**参数：**
- `fileName` (string): 文件名
- `htmlContent` (string): HTML内容
- `analysisData` (object): 分析数据

### `restoreDataOnLoad()`
页面加载时恢复数据。

**功能：**
- 从localStorage恢复文件状态
- 恢复补充信息
- 更新界面显示

### `saveToHistory(fileName, url, title, data, supplementText)`
保存分析记录到历史。

**参数：**
- `fileName` (string): 文件名
- `url` (string): URL
- `title` (string): 页面标题
- `data` (object): 分析数据
- `supplementText` (string): 补充信息文本

## 工具函数

### `calculateKGR(intitle, results)`
计算关键词黄金比例。

**参数：**
- `intitle` (string|number): Intitle搜索结果数
- `results` (string|number): 总搜索结果数

**返回值：**
- string: KGR值或"N/A"

**公式：**
```javascript
KGR = intitle / results
```

### `processKeywords(words, totalWords, limit)`
处理关键词数据，计算频率和密度。

**参数：**
- `words` (array): 单词数组
- `totalWords` (number): 总单词数
- `limit` (number): 返回数量限制

**返回值：**
```javascript
[
  {
    word: string,    // 关键词
    count: number,   // 出现次数
    density: number  // 密度百分比
  }
]
```

### `parseGoogleFormat(lines, startIndex)`
解析Google搜索结果格式。

**参数：**
- `lines` (array): 文本行数组
- `startIndex` (number): 开始解析的行索引

**返回值：**
- array: SERP链接对象数组

**格式识别：**
- 第1行: 搜索结果标题
- 第2行: 网站名称
- 第3行: URL（包含›符号）
- 第4行: 描述

## 事件处理函数

### `removeFile(index)`
移除指定索引的文件。

**参数：**
- `index` (number): 文件索引

**功能：**
- 从文件列表中移除
- 清理对应的分析结果
- 更新界面显示

### `closeTempDetailView()`
关闭临时详情查看。

**功能：**
- 移除临时导航按钮
- 隐藏结果区域
- 返回文件列表界面

## 错误处理

### 文件处理错误
```javascript
try {
  const analysis = await analyzeFileContent(file);
} catch (error) {
  console.error(`分析文件 ${file.name} 时出错:`, error);
  // 存储错误信息
  allAnalysisResults.push({
    fileName: file.name,
    analysis: null,
    supplementInfo: null,
    error: error.message
  });
}
```

### 数据解析错误
```javascript
try {
  supplementInfo = parseKeywordAndSerpData(supplementData);
} catch (error) {
  console.warn('补充信息解析失败', error);
  // 继续处理，不中断流程
}
```

### 剪贴板错误
```javascript
try {
  await navigator.clipboard.writeText(content);
} catch (error) {
  // 降级到手动复制
  fallbackCopyToClipboard(content);
}
```

## 数据结构说明

### 全局变量
```javascript
let uploadedFiles = [];           // 上传的文件列表
let allAnalysisResults = [];      // 所有分析结果
```

### localStorage结构
```javascript
// 文件数据
'fileData_filename.html': {
  htmlContent: string,
  analysisData: object,
  timestamp: number,
  expiryTime: number
}

// 历史记录
'analysisHistory': [
  {
    fileName: string,
    url: string,
    title: string,
    timestamp: number,
    data: object
  }
]
```

## 配置常量

### CORS代理列表
```javascript
const proxyUrls = [
  'https://api.codetabs.com/v1/proxy?quest=',
  'https://thingproxy.freeboard.io/fetch/',
  'https://cors-anywhere.herokuapp.com/',
  'https://crossorigin.me/',
  'https://api.allorigins.win/get?url='
];
```

### 缓存配置
```javascript
const CACHE_DURATION = 24 * 60 * 60 * 1000; // 24小时
const MAX_HISTORY_RECORDS = 10;             // 最大历史记录数
```

---

**注意事项：**
1. 所有异步函数都使用async/await模式
2. 错误处理采用try-catch结构
3. 数据持久化有时间限制和大小限制
4. 浏览器兼容性需要支持ES6+特性