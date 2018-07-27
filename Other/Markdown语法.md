---
title: Markdown语法
comments: true
date: 2018-05-07 15:46:55
id: markdown-grammer
tags: 
- Markdown
categories: Markdown
toc: true
reward: true
copyright: true
---

<!--# Markdown 语法-->

Markdown是一种简单的、用于文本排版的轻量级标记语言，它使用简洁的语法代替排版，让作者更专注于作品的内容。并且允许人们使用易读易写的纯文本格式编写文档，然后转换成有效的HTML文档，非常适用于网络书写。

<!--more-->

## 标题

```markdown
# 一级标题 h1
## 二级标题 h2
### 三级标题 h3
#### 四级标题 h4
##### 五级标题 h5
###### 六级标题 h6
```

**效果**：

# 一级标题 h1
## 二级标题 h2
### 三级标题 h3
#### 四级标题 h4
##### 五级标题 h5
###### 六级标题 h6

## 加粗

```markdown
**Bold**
```

```markdown
__Bold__
```

**效果**：

**Blod**

## 斜体

```markdown
*italic*
```

```markdown
_italic_
```

**效果**：

*italic*

## 删除线

```markdown
~~delete~~
```

**效果**：

~~delete~~

## 分割线

```markdown
***
```

```markdown
---
```

**效果**：

---


## 引用

```markdown
> 引用
```

**示例**：

```markdown
> 谁家玉笛暗飞声，
> 散入春风满洛城。
> 此夜曲中闻折柳，
> 何人不起故园情。 
```

**效果**：

> 谁家玉笛暗飞声，
> 散入春风满洛城。
> 此夜曲中闻折柳，
> 何人不起故园情。 

## 代码

```
`code`
```

**示例**：

```markdown
`<br/>`
```

**效果**：

`<br/>`

## 代码块

---
\`\`\`type
codeblock
\`\`\`

---

**示例**：

---

\`\`\`java
public class HelloWorld {
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;public static void main(String[] args) {
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;System.out.println("HelloWorld");
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}
}
\`\`\`

---

**效果**：

```markdown
public class HelloWorld {
	public static void main(String[] args) {
		System.out.println("HelloWorld");
	}
}
```

## 图片

```markdown
![Alt](http://)
```

**示例**：

```markdown
![示例图片](http://p6uturdzt.bkt.clouddn.com/markdown-logo.jpg)
```

**效果**：

![示例图片](http://p6uturdzt.bkt.clouddn.com/markdown-logo.jpg)

## 链接

```markdown
[Link](http://)
```

**示例**：

```markdown
[百度](http://www.baidu.com)
```

**效果**：

[百度](http://www.baidu.com)

## 无序列表

```markdown
- Red
- Green
- Blue
```

```markdown
+ Red
+ Green
+ Blue
```

```markdown
* Red
* Green
* Blue
```

**效果**：

- Red
- Green
- Blue

## 有序列表

```markdown
1. Red
2. Green
3. Blue
```

**效果**：

1. Red
2. Green
3. Blue

## 表格

```markdown
| 列名 | 列名 |
| ---- | ---- |
| 表项 | 表项 |
| 表项 | 表项 |
```

**效果**：

| 列名 | 列名 |
| ---- | ---- |
| 表项 | 表项 |
| 表项 | 表项 |

## 空格

```html
&nbsp; //半角空格（英文）
&emsp; //全角空格（中文）
```

## 居中

```html
<center>居中文本</center>
```

## 换行

```html
<br/>
```

## 锚-页内跳转

```html
[跳转到锚点](#jump)
......
<span id = "jump">锚点</span>
```

**示例**：

```markdown
目录
[1.Java入门](#1)
[2.Java基础](#2)
正文
<span id = 1>1.Java入门</span>
some_text......
<span id = 2>2.Java基础</span>
some_text......
```

**效果**：

目录

[1.Java入门](#1)

[2.Java基础](#2)

正文

<span id = 1>1.Java入门</span>

some_text......

<span id = 2>2.Java基础</span>

some_text......

















