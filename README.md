# Bubble Typst Template

这是一个基于 `@preview/bubble:0.2.2` 修改的 Typst 报告模板，可用于复旦大学相关文档模板，并已经针对中文排版做了本地化调整。模板入口是 `main.typ`，样式定义在 `lib.typ`。

## 文件结构

```text
bubble/
├── main.typ   # 文档入口，修改标题、作者和正文内容
├── lib.typ    # 模板样式，定义字体、颜色、封面、标题、代码块等
├── logo.png   # 封面右上角 logo
└── main.pdf   # 编译输出，可重新生成
```

## 字体依赖

请先在系统中安装以下字体，否则 Typst 会自动 fallback 到其他字体，效果会不一致。

- `LXGW WenKai`：正文中文字体
- `ChillKai`：标题和封面信息字体
- `JetBrains Mono NL`：代码块字体

当前字体配置在 `lib.typ` 中：

```typst
let body-font = "LXGW WenKai"
let title-font = ("ChillKai", "LXGW WenKai")
let code-font = "JetBrains Mono NL"
```

如果 VS Code/Tinymist 预览没有更新字体，可以执行：

```text
Tinymist: Restart Server
```

或：

```text
Developer: Reload Window
```

## 编译方式

在 `bubble` 目录所在项目中运行：

```bash
typst compile bubble/main.typ bubble/main.pdf
```

如果你没有安装 Typst CLI，也可以直接使用 VS Code 的 Tinymist 预览：

```text
Typst Preview: Preview
```

## 基本使用

在 `main.typ` 顶部修改模板参数：

```typst
#show: bubble.with(
  title: "Bubble template",
  subtitle: "Simple and colorful template",
  author: "david",
  affiliation: "复旦大学",
  date: datetime.today().display(),
  year: "Year",
  class: "Class",
  other: ("Made with Typst", "https://typst.com"),
  main-color: "0E419C",
  logo: image("logo.png"),
)
```

常用参数说明：

| 参数          | 作用                              |
| ------------- | --------------------------------- |
| `title`       | 封面标题，同时用于页眉            |
| `subtitle`    | 封面副标题，可设为 `none`         |
| `author`      | 作者                              |
| `affiliation` | 学校、机构或单位                  |
| `date`        | 日期                              |
| `year`        | 年级、年份或其他信息              |
| `class`       | 班级或课程信息                    |
| `other`       | 封面底部补充信息，传入字符串数组  |
| `main-color`  | 模板主色，使用十六进制 RGB 字符串 |
| `logo`        | 封面右上角图片，可设为 `none`     |

## 修改正文

模板参数下面就是正文区域：

```typst
= Introduction

This is a simple template that can be used for a report.

= 中文字体测试

以下是中文测试的样例。
```

Typst 标题语法：

```typst
= 一级标题
== 二级标题
=== 三级标题
```

当前模板只给一级和二级标题自动编号。

## 颜色

通过 `main-color` 修改主色：

```typst
main-color: "0E419C"
```

可以换成其他十六进制颜色，例如：

```typst
main-color: "2E7D32" // 绿色
main-color: "C62828" // 红色
main-color: "6A1B9A" // 紫色
```

主色会影响标题、链接、列表符号、行内代码背景和封面装饰。

## Logo

默认使用同目录下的 `logo.png`：

```typst
logo: image("logo.png")
```

如果不想显示 logo：

```typst
logo: none
```

如果想替换 logo，直接替换 `logo.png`，或改成其他图片路径：

```typst
logo: image("images/logo.png")
```

## 代码块

行内代码：

```typst
这是 `inline code` 示例。
```

块级代码：

````typst
```rust
fn main() {
  println!("Hello Typst!");
}
```
````

模板会自动使用 `JetBrains Mono NL`，块级代码会显示为斜体，并带浅色背景。

## 引用块

`lib.typ` 提供了一个简单的引用块样式：

```typst
#blockquote[
  这是一段引用内容。
]
```

## 从原版 Bubble 模板的变化

这个版本相对 `@preview/bubble:0.2.2` 做了这些调整：

- 使用本地 `lib.typ`，便于直接修改模板样式
- 正文字体改为 `LXGW WenKai`
- 标题字体改为 `ChillKai`
- 代码字体改为 `JetBrains Mono NL`
- 设置中文语言环境 `lang: "zh"`
- 调整代码块背景、圆角和间距
- 调整正文行距，使中文阅读更舒适

## 常见问题

### 字体没有变化

先确认字体已经安装到系统。然后重启 Tinymist：

```text
Tinymist: Restart Server
```

如果仍然不生效，检查 `lib.typ` 中的字体名称是否和系统字体名称一致。

### 想换字体

修改 `lib.typ` 里的这三行：

```typst
let body-font = "LXGW WenKai"
let title-font = ("ChillKai", "LXGW WenKai")
let code-font = "JetBrains Mono NL"
```

### 想改标题编号样式

修改 `lib.typ` 中的：

```typst
set heading(numbering: (..nums) => {
  ...
})
```

当前一级标题使用罗马数字样式，二级标题使用类似 `I.1.` 的样式。
