---
title: Web | CSS
id: web-css
comments: true
tags:
  - Web前端
categories: Web前端
date: 2018-04-05 17:21:22
toc: true
reward: true
copyright: true
---

<!--# CSS-->

CSS（Cascading Style Sheets，层叠样式表），主要通过为HTML元素增添样式的方式修饰静态页面，实现了页面内容与样式分离。目前主流网页布局均采用 **div+CSS** 方式实现。

<!-- more -->

# 1. CSS基础

## 1.1 CSS三大特性

1. **层叠**性：权重高的样式会覆盖权重低的样式；
2. 继承性：子元素继承父元素的样式；
3. 优先级：作用域越小，优先级越大；
  - 不同级别：行内样式>id选择器>类选择器>标签选择器>通配符>继承；
  - 同一级别：后写的会覆盖先写的样式；

## 1.2 CSS语法规则

CSS注释：`/* CSS注释内容 */`

```css
/* CSS注释内容 */
选择器{ 
	样式属性1:值1;
	样式属性2:值2;
}
```

## 1.3 引入CSS样式表

1.行内样式表（内联表）：

```html
<标签 style="属性1:值1;属性2:值2;"></标签>
```

2.内部样式表（内嵌表）

```html
  <style>
      选择器{ 
        样式属性1:值1;
        样式属性2:值2;
      }
  </style>
```

3.外部样式表（外联表）：外部**.css**文件

4.引入外部样式表：

```html
<link rel="stylesheet" type="text/css" href="url" />
```

5.三种样式表总结

| 样式表     | 优点               | 缺点             | 使用情况     | 控制范围 |
| ---------- | ------------------ | ---------------- | ------------ | -------- |
| 行内样式表 | 权重高             | 样式与结构未分离 | 较少         | 单个标签 |
| 内部样式表 | 样式与结构部分分离 | 未彻底分离       | 较多         | 整个页面 |
| 外部样式表 | 样式与结构完全分离 | 需引入           | 多，**推荐** | 整个站点 |



# 2. CSS样式

## 2.1 CSS字体-font★

1.字体系列：

```css
font-family : "宋体","微软雅黑";
```

font-family是一个字体族的优先表，如果浏览器不支持第一个字体，则会尝试下一个。

2.字体风格：

```css
font-style : normal/italic/oblique;
/*
- normal：标准
- italic：斜体
- oblique：倾斜
*/
```

3.字体粗细：

```css
font-weight : 400;
/* 加粗度：100,200,300,400,500,600,700,800,900 */
/* normal=400 | blod=700 */
/* bolder：更粗 | lighter：更细*/
```

4.字体大小：

```css
font-size : px/em/%
```

5.font综合设置：

```css
font : font-style font-weight font-size/line-height font-family
```

```css
注意：
- ！英文字体名一般不需要加引号，设置英文字体名必须位于中文字体名之前；
- ！加粗度没有单位，而且`x00`只有9个值，不存在`123`这种值；
- ！网页普遍是`14px`；尽量设偶数px，奇数px在IE6存在bug；
```

## 2.2 CSS文本-text★
1.文本缩进：

```css
text-indent : em/px/%;
```

2.水平对齐：

```css
text-align : left/center/right;
```

3.单词间隔（只适用于英文）:

```css
word-spacing : em/px;
```

4.字符间隔：

```css
letter-spacin : em/px;
```

5.文本装饰：

```css
text-decoration : none/underline/overline/line-through/blink;
/* 
- none：无
- underline：下划线
- overline：上划线
- line-through：穿过一条线
- blink：闪
*/
```

6.行高：

```css
line-height : px/em/%;  
/* 一般文本行高比字号大7-8像素即可 */
```

7.文本阴影：

```css
text-shadow : 水平位置 垂直位置 模糊偏移 阴影颜色;
```

8.【CSS3】**颜色透明度**：

```css
rgba(0~255, 0~255, 0~255, 0~1);
/* 模糊度：0~1 */
```

## 2.3 CSS背景-background★
1.背景色：

```css
background-color：rgb();
```

2.背景图：

```css
background-image : url();
```

3.背景平铺：

```css
background-repeat : repeat/no-repeat;
/*
- repeat：平铺
- no-repeat：不平铺
- repeat-x：横向平铺
- repeat-y：纵向平铺
*/
```

3.背景定位：

```css
background-position : X坐标/位置 Y坐标/位置;
/* 坐标：px/em/% */
/* 位置：top，bottom，center，left，right； 
   若只设了一个值，那么第二个值将是center； */
```

4.背景关联：

```css
backgrount-attchment : fixed/scroll;
/*
- scroll：默认值。背景图像会随着页面其余部分的滚动而移动；
- fixed：图像固定；当页面的其余部分滚动时，背景图像不会移动；
*/
```

5.背景综合设置：

```css
background: bg-color bg-image bg-repeat bg-attchment bg-position(x,y);
```



6.【CSS3】背景尺寸：

```css
background-size : contain/cover;
/*
- contain：保证背景图片完整性；
- cover：保证背景图片完全覆盖整个区域；
- width&height：设置背景的宽&高；（一般设置1个参数，设置2个参数会导致图片变形）
*/
```

## 2.4 *CSS列表-list-style

1.列表项标志：

```css
list-style-type : none/disc/circle/square/decimal...;
/* 
none：无
disc：实心圆
circle：空心圆
square：实心方块
decimal：数字
*/
```

2.列表项图像：

```css
list-style-image : url();
```

3.列表标志位置：

```css
list-style-position : inside/outside;
/*
outside：默认值。保持标记位于文本的左侧。列表项目标记放置在文本以外，且环绕文本不根据标记对齐。
inside：列表项目标记放置在文本以内，且环绕文本根据标记对齐。
*/
```

4.列表综合设置：

```css
list-style : image type position;
```

## 2.5 *CSS表格

1.折叠边框

```css
border-collapse : collapse;
```

2.水平对齐

```css
text-align : left/center/right;
```

3.垂直对齐

```css
vertical-align : top/center/bottom;
```

4.空单元格显示/隐藏

```css
empty-cells : show/hide;
```

5.表格标题在上/在下

```css
caption-side : top/bottom;
```

## 2.6 *CSS轮廓-outline

1.轮廓颜色：

```css
outline-color : rgb()
```

2.轮廓样式：

```css
outline-style : solid/dotted/dashed/double...;
/*
- soild：实线
- dotted：点线
- dashed：虚线
- double：双实线
*/
```

3.轮廓宽度：

```css
outline-width : thick/medium/thin/px;
/*
- thick：粗
- medium：中
- thin：细
*/
```

4.轮廓综合设置：

```css
outline : color style width;
```

## 2.7 标签显示模式★

| display        | 描述       |
| -------------- | ---------- |
| `none`         | 不显示     |
| `block`        | 块级元素   |
| `inline`       | 行内元素   |
| `inline-block` | 行内块元素 |

## 2.8 内容溢出盒子★

| overflow  | 描述                                                         |
| --------- | ------------------------------------------------------------ |
| `visible` | 默认值。内容溢出部分显示在盒子外；                           |
| `hidden`  | 隐藏内容溢出部分                                             |
| `scroll`  | 如果内容溢出会被修剪，则浏览器会显示滚动条以便查看其余的内容； |
| `auto`    | 如果内容溢出被修剪，则浏览器会显示滚动条以便查看其余的内容； |



# 3. CSS选择器

## 3.1 元素选择器

```css
标签{ 
	属性:值;
}
```

## 3.2 类选择器

```css
.类名{
	属性:值;
}
```

单类名调用：`class="类名"`；
多类名调用：`class="类名1 类名2 ..."`；

## 3.3 id选择器

```css
#id{
	属性:值;
}
```

## 3.4 通配符选择器

```css
*{                
	属性:值;
}
```

> 作用域：整个HTML页面
>

## 3.5 交集选择器

```css
选择器1选择器2{
    属性:值;
}
```

## 3.6 并集选择器

```css
选择器1,选择器2{
    属性:值;
}
```

## 3.7 后代选择器★

```css
先代选择器 后代选择器{
    属性:值;
}
```

> 作用于先代元素内的[所有的后代元素]；

## 3.8 子元素选择器★

```css
父选择器 > 子选择器{
    属性:值;
}
```

> 只作用于父元素内的[直接子元素]；

## 3.9 相邻兄弟选择器

```
伯选择器 + 仲选择器{
    属性:值;
}
```

> 作用于**紧接在**伯元素后的[仲元素]；

## 3.10 属性选择器

```css
[属性]{
    属性:值;
}
```

```css
标签[属性=值]{
    属性:值;
}
```

## 3.11 伪类选择器

```css
选择器:伪类{
	属性:值;
}
```

**1.`<a>`链接伪类：**
- `a:link`：未访问的链接；
- `a:visited`：已访问的链接；
- `a:hover`：鼠标移动到链接；
- `a:active`：鼠标点击时的连接；

**2.位置结构伪类：**
- `first-child`：第一个子元素；
- `last-child`：最后一个子元素；
- `nth-child(n)`：第n个元素（n=1,2,3...）；
- `nth-last-child(n)`：倒数第n个元素（n=1,2,3...）;
  [n=`odd`：奇数 | n=`even`：偶数]

```css
注意：
- ！不是第一个HTML标签，而是第一个HTML元素
	html元素：文本，图像，链接；
```

**3.【CSS3】目标伪类：**

```css
/*:target 选择器用于选取当前活动的目标元素*/
:target{
    属性:值;
}
```
## 3.12 伪元素选择器

```css
标签::伪元素{
    属性:值;
}
```

**伪元素：**

- `first-line`：第一行；

- `first-letter`：第一个字符；

- `before`：在标签之前添加`content:新内容`；

```
标签::before{
	content:新内容;
}
```

- `after`：在标签之后添加`content:新内容`；

```
标签::after{
	content:新内容;
}
```

- `selection`：选中区域；




# 4. CSS框模型（Box Model）★

![BoxModel](http://p6uturdzt.bkt.clouddn.com/css-boxmodel.gif)

## 4.1 边框-border

1.边框宽度：

```css
border-width : px;
```

2.边框样式：

```css
border-style : solid/dashed/dotted/double;
/*
- solid：实线
- dashed：虚线
- dotted：点线
- double：双实线
*/
```

3.边框颜色：

```css
border-color : rgb();
```

4.边框综合设置：

```css
border : width style color;
```

5.单边边框：

```css
border-top/right/bottom/left-属性:值;
/* 单独设置某一边，设置方式与border同理 */
```

6.圆角边框：

```css
border-radius : 左上角半径px 右上角半径px 右下角半径px 左下角半径px;
```

## 4.2 内边距-padding

1.内边距：

```css
padding : top-px right-px bottom-px left-px
```

2.单边内边距：

```css
padding-top/right/bottom/left : px
```

## 4.3 外边距-margin

1.外边距：

```css
margin:top-px right-px bottom-px left-px;
```

2.单边外边距：

```css
margin-top/right/bottom/left : px;
```

```css
border/padding/margin综合设置提示：
- 可设置四个参数，分别对应top-right-bottom-left，顺时针遍历设置；
- 若只设置了1个value，则top=right=bottom=left=value；
- 若只设置了2个value，则top=val_1,right=val_2,bottom=val_1,left=val_2；顺时针遍历赋值；
- 若只设置了3个value，则top=val_1,right=val_2,bottom=val_3,left=val_1；顺时针遍历赋值；
- border-radius半径设置顺序：左上-右上-右下-坐下；顺时针遍历；
```


## 4.4 垂直外边距合并现象★
1.**相邻盒子**垂直外边距合并，margin合并取最大值；

&nbsp;&nbsp;&nbsp;解决方案：只设置一个margin；

2.**嵌套盒子**垂直外边距合并。

&nbsp;&nbsp;&nbsp;解决方案①：**`overflow:hidden`**；

&nbsp;&nbsp;&nbsp;解决方案②：使用`border`，`padding`；

## 4.5 CSS3盒子&IE6盒子
- IE6框模型：`box-sizing:content-box`

```css
IE6框的大小：【width+左右padding+左右border+左右margin】
		×【height+上下padding+上下border+上下margin】
```

- CSS3框模型：`box-sizing:border-box`

```css
CSS3框的大小：【width+左右margin】×【height+上下margin】
		- CSS3盒的[width&height]包含[padding+border]
```



# 5. 浮动

## 5.1 浮动-float（难点）
**浮动：浮动块不在文档流中，不占文档流位置；但占浮动位置**。

```css
float:left/right;
```

（未完待详细解释）

## 5.2 清除浮动-clear★
clear 属性规定元素的哪一侧不允许其他浮动元素。

```css
clear:left/right/both
```

**清除浮动的方式：**

1.【W3C推荐】在盒子末尾再添加一个如下的空盒子：

```html
<div style="clear:both;"></div> 
```

2.在盒子样式中添加溢出隐藏样式：

```css
overflow:hidden
```

3.为盒子添加如下样式，在每次结束后都清除浮动：

```css
.clearfix:after{clear:both}  /* 只适用于IE6、IE7。 */
```




# 6. 定位

## 6.1 定位简介（难点）

| position             | 是否占文档流   | 定位策略                   |
| -------------------- | -------------- | -------------------------- |
| `static`：静态定位   | 占文档流       |                            |
| `fixed`：固定定位    | 不占文档流     | 相对于视窗进行定位         |
| `relative`：相对定位 | 占文档流原位置 | 相对于原位置进行边偏移     |
| `absolute`：绝对定位 | 不占文档流     | 相对于其已定位的包含块定位 |

## 6.2 边偏移
1. 前提：float || position || 不占文档流；
2. 边偏移：`top`，`bottom`，`left`，`right`；

## 6.3 相对定位★
```css
position:relative
```

1.相对于在文档流中的原位置进行边偏移；

2.仍占据文档流中的原位置；

![relative](http://p6uturdzt.bkt.clouddn.com/css-relative.gif)

## 6.4 绝对定位★
```css
position:absolute
```

1.相对于[**其已定位的包含块**]进行边偏移；

2.已从**文档流**中**完全删除**，就好像该元素原来不存在一样；

3.元素定位后生成一个**块级框**，而不论原来它在正常流中生成何种类型的框；

4.绝对定位与文档流无关，所以可以覆盖在页面其他元素上；

5.可通过`z-index`控制堆叠次序；`z-index` 仅能在定位元素上奏效；

6.一般采取[子绝父相]策略；


# 7. 页面日常开发习惯

页面布局：div+CSS；

使用外部样式表，引入外部.css文件；

例行设置：

```css
1.清除盒子内外边距：*{padding:0;margin:0;}；
2.链接取消下划线：a{text-decoration:none}；
3.列表取消列表项标志：ul{list-style:none}；
```

功能型样式：

```html
-外边距实现盒子水平居中：margin:0 auto；
-垂直居中：line-height:盒高；
-清除浮动：<div style="clear:both;"></div>；
```




# 附：

## CSS长度

| 相对长度单位 | 描述                           |
| ------------ | ------------------------------ |
| px           | 像素值                         |
| em           | 相对于当前字符的尺寸（自适应） |
| %            | 百分比                         |

| 绝对长度单位 | 描述               |
| ------------ | ------------------ |
| cm           | 厘米               |
| mm           | 毫米               |
| in           | 英寸               |
| pt           | 磅（1pt=1/72英寸） |

## CSS颜色

| 单位                     | 描述                             |
| ------------------------ | -------------------------------- |
| `color_name`             | 颜色名称（如red）                |
| `rgb(0~255,0~255,0~255)` | RGB值（如rgb(0,0,0)）            |
| `rgb(x%,x%,x%)`          | RGB百分比值（如rgb(100%,0%,0%)） |
| `#rrggbb`                | 十六进制数（如#c3c3c3）          |


