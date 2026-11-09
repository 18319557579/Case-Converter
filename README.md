# Case Converter

一个在浏览器中运行的离线文本大小写与命名格式转换工具。适合整理英文文本，以及转换变量名、类名、常量名、路径片段等，无需安装应用、注册账号或配置开发环境。

## 快速开始

1. 下载项目文件，使用现代浏览器（如 Chrome、Edge 或 Firefox）打开 `index.html`。
2. 在任意一个转换区域的 **Input Text** 中输入或粘贴文本。
3. 点击所需的格式按钮，**Output Text** 会立即显示转换结果；继续输入时，结果也会实时更新。
4. 点击 **Copy** 复制结果，或点击 **Clear** 清空当前区域的输入和输出。

页面默认使用 `lowercase`。选择其他格式后，浏览器会分别记住两个转换区域的选择，下次打开时恢复。

## 主要功能

- **15 种转换格式**：覆盖常见的大小写转换、驼峰命名、下划线命名和连接符命名。
- **两个独立转换区域**：Converter 1 和 Converter 2 各自维护输入与格式，方便同时处理两段文本，或手动粘贴同一段文本进行对比。
- **实时转换**：输入文本或切换格式后立即更新结果，无需提交。
- **一键复制与清空**：复制成功显示 `Copied`；清空后可直接继续输入。
- **离线运行**：HTML、CSS 和 JavaScript 均包含在一个文件中，没有外部依赖或网络请求。
- **适应不同屏幕**：宽屏下输入和输出并排显示，窄屏下改为上下排列。

## 支持的转换格式

以下示例统一以 `Hello World` 作为输入：

| 格式按钮 | 转换规则 | 输出示例 |
| --- | --- | --- |
| `lowercase` | 全部转为小写 | `hello world` |
| `UPPERCASE` | 全部转为大写 | `HELLO WORLD` |
| `camelCase` | 首词小写，后续各词首字母大写，直接连接 | `helloWorld` |
| `Capital Case` | 每个词首字母大写，以空格连接 | `Hello World` |
| `CONSTANT_CASE` | 全部大写，以下划线连接 | `HELLO_WORLD` |
| `dot.case` | 全部小写，以点号连接 | `hello.world` |
| `kebab-case` | 全部小写，以连字符连接 | `hello-world` |
| `no case` | 全部小写，以空格连接 | `hello world` |
| `PascalCase` | 每个词首字母大写，直接连接 | `HelloWorld` |
| `Pascal_Snake_Case` | 每个词首字母大写，以下划线连接 | `Hello_World` |
| `path/case` | 全部小写，以斜杠连接 | `hello/world` |
| `Sentence case` | 合并为小写文本后，仅将整体首字母大写 | `Hello world` |
| `snake_case` | 全部小写，以下划线连接 | `hello_world` |
| `sWAP cASE` | 逐个反转字母大小写 | `hELLO wORLD` |
| `Train-Case` | 每个词首字母大写，以连字符连接 | `Hello-World` |

## 转换规则与使用说明

### 原样保留空格、标点的格式

`lowercase`、`UPPERCASE` 和 `sWAP cASE` 直接处理原始文本中的字母，保留空格、换行、标点和其他非字母字符。例如：

```text
输入：Hello, World!
lowercase：hello, world!
UPPERCASE：HELLO, WORLD!
sWAP cASE：hELLO, wORLD!
```

### 分词后重新组合的格式

其余格式先提取字母和数字组成的词，再按所选规则连接。工具可识别常见的驼峰边界、缩写边界，以及数字后接字母的边界，例如：

```text
helloWorld   → snake_case → hello_world
XMLHttpRequest → kebab-case → xml-http-request
version2Test → snake_case → version2_test
Hello, World! → camelCase → helloWorld
```

这些格式会移除原有标点、表情等非字母数字字符，将空格、换行和分隔符统一替换为目标格式的连接方式。因此，`path/case` 适合生成路径样式的文本，不能用于保留已有完整路径或 URL 的结构。

`Sentence case` 只将整个转换结果的首字母大写，不会识别多个句子并分别处理。工具能识别 Unicode 字母和数字，但不提供中文自然语言分词；中文等没有大小写的字符也不会产生字母大小写变化。

### 本地存储与隐私

- 文本转换完全在当前浏览器中完成，工具本身不上传输入或输出。
- 仅通过 `localStorage` 保存每个转换区域选中的格式，不保存输入文本和转换结果。刷新或关闭页面前，请自行复制需要保留的内容。
- 格式记忆依赖浏览器允许本地存储；不同浏览器、隐私模式或不同文件位置之间不保证共享设置。

### 复制结果

点击 **Copy** 后，工具会尝试写入剪贴板，并提供兼容的备用复制方式。如果显示 `Copy failed`，可手动选中 **Output Text** 中的内容，使用系统复制快捷键复制。

## 项目结构

```text
Case Converter/
├── index.html   # 完整工具页面，包含样式、转换逻辑与交互
└── README.md    # 功能与使用说明
```

项目使用原生 HTML、CSS 和 JavaScript，无需安装依赖或执行构建命令，也可将 `index.html` 部署到静态网站服务上使用。
