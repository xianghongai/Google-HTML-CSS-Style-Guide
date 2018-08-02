# Google HTML/CSS代码风格指南

## 1.背景

本文档定义了HTML/CSS的编写格式和风格规则。它旨在提高合作和代码质量,并使其支持基础架构。它适用于HTML/CSS文件。只要代码质量是可以被维护的，就能很好的被工具混淆、压缩和合并。


## 2. 总则

### 2.1 样式规则

#### 2.1.1 协议 / Protocol

尽可能将 HTTPS 协议用于嵌入式资源。

始终对图像（images）和其他媒体文件，样式文件（style sheets）和脚本文件（scripts）使用 HTTPS 协议 `https:`，除非相应的文件不能通过　HTTPS　获得。

```html bad
<!-- Not recommended: omits the protocol (省略了协议) -->
<script src="//ajax.googleapis.com/ajax/libs/jquery/3.1.0/jquery.min.js"></script>

<!-- Not recommended: uses the HTTP protocol -->
<script src="http://ajax.googleapis.com/ajax/libs/jquery/3.1.0/jquery.min.js"></script>
```

```html good
<!-- Recommended -->
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.0/jquery.min.js"></script>
```

```css bad
/* Not recommended: omits the protocol */
@import '//fonts.googleapis.com/css?family=Open+Sans';

/* Not recommended: uses the HTTP protocol */
@import 'http://fonts.googleapis.com/css?family=Open+Sans';
```

```css good
/* Recommended */
@import 'https://fonts.googleapis.com/css?family=Open+Sans';
```

### 2.2 排版规则

#### 2.2.1 缩进 / Indentation

一次缩进2个空格。

不要使用制表符（Tab）或混合制表符和空格来缩进。

```html good
<ul>
  <li>Fantastic</li>
  <li>Great</li>
</ul>
```

```css good
.example {
  color: blue;
}
```

#### 2.2.2 大小写 / Capitalization

仅使用小写。

所有代码必须为小写：这适用于 HTML 元素名称、属性和属性值（除了 text/CDATA），CSS的选择器、属性和属性值（字符串除外）。

```html bad
<!-- Not recommended -->
<A HREF="/">Home</A>
```

```html google
<!-- Recommended -->
<img src="google.png" alt="Google">
```

```css bad
/* Not recommended */
color: #E5E5E5;
```

```css good
/* Recommended */
color: #e5e5e5;
```

#### 2.2.3 行尾空格

删除行尾白空格。

行尾空格没必要存在。

```html bad
<!-- Not recommended -->
<p>What? </p>
```

```html good
<!-- Recommended -->
<p>Yes please.</p>
```


### 2.3 文件 Meta 规则

#### 2.3.1 编码 / Encoding

使用 UTF-8 编码 (不带 BOM 头)

让你的编辑器用没有字节顺序标记的 UTF-8 编码格式进行编写。

在HTML模板和文件中指定编码 `<meta charset="utf-8">` . 不需要制定样式表的编码，它默认为 UTF-8.

#### 2.3.2 注释 / Comments

根据需要尽可能的去解释你写的代码。

用注释来解释代码：它涵盖了什么、它的目的是什么、为什么使用或优先使用这个解决方案？

（本规则可选，要求对代码进行完整的注释并不现实，注释也会增重 HTML 和 CSS 的代码体积。注释取决于项目的复杂程度。）

#### 2.3.3 事项

用 `TODO` 标记待办事项和处于活动状态事项。

`TODO` 仅使用关键字突出显示待办事项，而不是其他常见格式 `@@`。

在括号中附加联系人（用户名或邮件列表），格式为 `TODO(contact)`。

在冒号后附加操作项，如 `TODO: action item`。

```html
<!-- TODO: remove optional tags -->
<ul>
  <li>Apples</li>
  <li>Oranges</li>
</ul>
```

    译者注：代码常用注释标记：

    - `NOTE`: 代码如何工作的描述（比较复杂需要解释）
    - `XXX`: 警告可能存在的陷阱 `NOTE:XXX:陷阱`
    - `HACK`: 用于规避问题、错误，代码不健壮或存在异常。 `HACK:FIXME:临时填坑`
    - `FIXME`: 虽然实现功能，但应该有更优的代码方案，需要重构
    - `BUG`: 这里有问题
    - `TODO`: 没问题，但需要编写额外的代码 (当前工作被中断，未来得及完成)

    需要配置编辑器以高亮显示这些注释标记

## 3. HTML

### 3.1 HTML 代码风格规则

#### 3.1.1 Document 类型

使用HTML5。

HTML5（HTML 语法）是所有 HTML 文档的首选：`<!DOCTYPE html>`。

（推荐使用 HTML，即 `text/html`。不要使用 XHTML。XHTML `application/xhtml+xml` 文档标记缺少浏览器和基础架构 / infrastructure 支持，并且存储空间优化比 HTML 少。）

#### 3.1.2 HTML 代码有效性 / Validity

尽可能使用有效的 HTML。

编写有效的HTML代码，否则很难提升性能。

使用 [W3C HTML validator](https://validator.w3.org/nu/) 等工具进行测试。

HTML 代码有效性是代码质量衡量的重要标准，并且有助于学习技术规范，以确保正确使用 HTML 代码。

```html bad
<!-- Not recommended -->
<title>Test</title>
<article>This is only a test.
```

```html good
<!-- Recommended -->
<!DOCTYPE html>
<meta charset="utf-8">
<title>Test</title>
<article>This is only a test.</article>
```

#### 3.1.3 语义 / Semantics

根据 HTML 用途合理使用之。

使用 HTML 元素（称之为“标记 / tags”是不正确的）来创建和描述文档。例如，使用 heading 元素作为标题，p 元素用于段落，a 元素用于锚点等。

合理使用 HTML 对可访问性、代码重用和编码效率各方面有重要的影响。

```html bad
<!-- Not recommended -->
<div onclick="goToRecommendations();">All recommendations</div>
```

```html good
<!-- Recommended -->
<a href="recommendations/">All recommendations</a>
```

#### 3.1.4 多媒体备选方案

为多媒体提供备选内容。

对于多媒体，如图像，视频，通过 `canvas` 读取的动画元素，请确保提供替代访问方案。 对于图像提供有意义的替代文本 `alt` ，对于视频和音频提供有效的副本和字幕说明。

提供备选内容是很重要的，原因：给盲人用户以一些提示性的文字，用 `@alt` 告诉他这图像是关于什么的，给可能没理解视频或音频内容的用户以文字提示。

（图像的 alt 属性会产生冗余，纯粹装饰性的图像，不需使用替代文本，直接用 `alt=""` 属性加以说明 。）

```html bad
<!-- Not recommended -->
<img src="spreadsheet.png">
```

```html good
<!-- Recommended -->
<img src="spreadsheet.png" alt="Spreadsheet screenshot.">
```

#### 3.1.5 分离

将结构、表象和行为分离。

严格保持结构 / structure （标记 / markup），表象 / presentation （样式 / styling），和行为 / behavior （脚本 / scripting）的分离, 并尽量让三者之间的交互保持最低限。

确保文档和模板只包含用于结构化文档目的的 HTML，把所有表象的都纳入样式表中，把所有行为的都放进脚本中。

此外，使联系区域尽可能小，文档和模板中尽可能地减少样式表和脚本的链接。（一是减少链接数，二是减少代码作用范围）

基于可维护性，将结构从表象和行为分离非常重要。更改 HTML 文档和模板比更新样式表和脚本成本要高。

```html bad
<!-- Not recommended -->
<!DOCTYPE html>
<title>HTML sucks</title>
<link rel="stylesheet" href="base.css" media="screen">
<link rel="stylesheet" href="grid.css" media="screen">
<link rel="stylesheet" href="print.css" media="print">
<h1 style="font-size: 1em;">HTML sucks</h1>
<p>I’ve read about this on a few sites but now I’m sure:
  <u>HTML is stupid!!1</u>
<center>I can’t believe there’s no way to control the styling of
  my website without doing everything all over again!</center>
```

```html good
<!-- Recommended -->
<!DOCTYPE html>
<title>My first CSS-only redesign</title>
<link rel="stylesheet" href="default.css">
<h1>My first CSS-only redesign</h1>
<p>I’ve read about this on a few sites but today I’m actually
  doing it: separating concerns and avoiding anything in the HTML of
  my website that is presentational.</p>
<p>It’s awesome!</p>
```

#### 3.1.6 实体引用

不要使用实体引用。

不需要使用类似 `&mdash;`、`&rdquo;` 和 `&#x263a;` 等的实体引用, 假定团队之间所用的文件和编辑器是同一编码（UTF-8）。

唯一的例外适用于HTML中具有特殊含义的字符（如 `<` 和 `&`）以及控件或“invisible / 不可见”字符（如不间断空格）。

```html bad
<!-- Not recommended -->
The currency symbol for the Euro is &ldquo;&eur;&rdquo;.
```

```html good
<!-- Recommended -->
The currency symbol for the Euro is “€”.
```

#### 3.1.7 可选标签

省略可选标签（可选）。

出于优化文件大小和校验， 可以考虑省略可选标签，哪些是可选标签可以参考 [HTML5 specification](http://www.whatwg.org/specs/web-apps/current-work/multipage/syntax.html#syntax-tag-omission)。

（这种方法需要更精准的规范来制定，众多的开发者对此的观点也都不同。考虑到一致性和简洁的原因，省略所有可选标记是有必要的。）

#### 3.1.8 type 属性

在样式表和脚本的标签中忽略 type 属性

在样式表（除非不用 CSS）和脚本（除非不用 JavaScript）的标签中 不写 type 属性。

HTML5默认 type 为 `text/css` 和 `text/javascript` 类型，所以没必要指定。即便是老浏览器也是支持的。

```html bad
<!-- Not recommended -->
<link rel="stylesheet" href="https://www.google.com/css/maia.css" type="text/css">
```

```html good
<!-- Recommended -->
<link rel="stylesheet" href="https://www.google.com/css/maia.css">
```

```html bad
<!-- Not recommended -->
<script src="https://www.google.com/js/gweb/analytics/autotrack.js" type="text/javascript"></script>
```

```html good
<!-- Recommended -->
<script src="https://www.google.com/js/gweb/analytics/autotrack.js"></script>
```

### 3.2 HTML 代码格式规则

#### 3.2.1 一般格式

为每个块 / block，列表 / list 或表 / table 元素使用一个新行，子元素相对于父元素进行缩进。

将元素撇开样式（CSS 允许元素用 display 属性赋予不同的性质），将每个块，列表或表元素放在新行上。

另外，块元素、列表元素或表格元素的子元素需要缩进。

（如果遇到列表项之间的空白问题，可以将所有 li 元素放在一行中。让 linter 抛出警告而不是错误。）


```html good
<blockquote>
  <p><em>Space</em>, the final frontier.</p>
</blockquote>
```

```html good
<ul>
  <li>Moe</li>
  <li>Larry</li>
  <li>Curly</li>
</ul>
```

```html good
<table>
  <thead>
    <tr>
      <th scope="col">Income</th>
      <th scope="col">Taxes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>$ 5.00</td>
      <td>$ 4.50</td>
    </tr>
  </tbody>
</table>
```


#### 3.2.2 HTML 行包裹

长行换行（可选）。

虽然没有针对 HTML 代码列长度的限制和建议，但如果能明显提高可读性，则可以考虑长行换行。

换行时，新延续的行在原始行缩进基础上再缩进4个空格。

```html good
<md-progress-circular md-mode="indeterminate" class="md-accent"
    ng-show="ctrl.loading" md-diameter="35">
</md-progress-circular>
```

```html good
<md-progress-circular
    md-mode="indeterminate"
    class="md-accent"
    ng-show="ctrl.loading"
    md-diameter="35">
</md-progress-circular>
```

```html good
<md-progress-circular md-mode="indeterminate"
                      class="md-accent"
                      ng-show="ctrl.loading"
                      md-diameter="35">
</md-progress-circular>
```

#### 3.2.3 HTML 引号

属性值，使用双引号。

属性值包裹使用双引号（""）而不是单引号（''）。

```html bad
<!-- Not recommended -->
<a class='maia-button maia-button-secondary'>Sign in</a>
```

```html good
<!-- Recommended -->
<a class="maia-button maia-button-secondary">Sign in</a>
```

## 4. CSS

### 4.1 CSS 代码风格规则

#### 4.1.1 CSS 有效性 / Validity

尽可能使用有效的CSS。

使用有效的CSS代码，除非处理 CSS 验证程序错误或需要专有语法。

使用 [W3C CSS validator](https://jigsaw.w3.org/css-validator/) 这类工具进行测试。

CSS 代码有效性是代码质量衡量的重要标准，如果发现 CSS 代码没有任何效果可以删除它，并确保正确的使用 CSS。

#### 4.1.2 ID/Class 命名

使用有意义且通用的 ID/Class 名。

命名不可表象、生僻和模糊，通过 ID/Class 命名能知道元素有什么用途，或者是其它通用命名方式。

首选具有特定名称并反映元素用途的命名，这些名称最容易理解且不易改变，以减少更新。

通用命名方式是对元素进行简单的补充，各相邻元素是没有特殊意义的、歧义的，如同命名为"helpers"。

使用功能性或通用命名方式，会减少不必要的文档或模板修改。

```css bad
/* Not recommended: meaningless */
#yee-1901 {}

/* Not recommended: presentational */
.button-green {}
.clear {}
```

```css good
/* Recommended: specific */
#gallery {}
#login {}
.video {}

/* Recommended: generic */
.aux {}
.alt {}
```

    译者注: 项目样式声明中不能用 ID 定义规则！

#### 4.1.3 ID/Class 命名风格

ID/Class 命名，如无必要短小精确，如有需要详尽清晰。

ID/Class 名尽可能包含语义语境。

采用这样的命名方式，代码易读、易懂且高效。

```css bad
/* Not recommended */
#navigation {}
.atr {}
```

```css good
/* Recommended */
#nav {}
.author {}
```

#### 4.1.4 类型选择器 Type Selectors

避免使用类型选择器限定 ID/Class 名。

如无必要，元素名和 ID/Class 不进行组合使用。

出于[性能原因](http://www.stevesouders.com/blog/2009/06/18/simplifying-css-selectors/)，避免使用不必要的父辈节点选择器，以减少层级和嵌套。

```css bad
/* Not recommended */
ul#example {}
div.error {}
```

```css good
/* Recommended */
#example {}
.error {}
```

#### 4.1.5 速记属性

尽可能使用速记属性。

CSS 提供了各种速记属性（如 font ），应尽可能使用，即使在只显式设置一个值的情况下也是如此。

使用缩写可以提高编码效率和可理解性。

```css bad
/* Not recommended */
border-top-style: none;
font-family: palatino, georgia, serif;
font-size: 100%;
line-height: 1.6;
padding-bottom: 2em;
padding-left: 1em;
padding-right: 1em;
padding-top: 0;
```

```css good
/* Recommended */
border-top: 0;
font: 100%/1.6 palatino, georgia, serif;
padding: 0 1em 2em;
```

#### 4.1.6 0 和 单位/Units

除非需要，否则省略“0”值后的单位。

非必要的情况下 `0` 后面不加单位。

```css good
flex: 0px; /* This flex-basis component requires a unit. */
flex: 1 1 0px; /* Not ambiguous without the unit, but needed in IE11. */
margin: 0;
padding: 0;
```

#### 4.1.7 前导数字 0

0开头的浮点数值省略前导 0 。

值或长度在 -1 与 1 之间的小数，小数前的 0 可以忽略不写。

```css good
font-size: .8em;
```

#### 4.1.8 十六进制表示法

可能使用3个字符的十六进制表示法。

对于许可的颜色值，3个字符的十六进制表示法更短更简洁。

```css bad
/* Not recommended */
color: #eebbcc;
```

```css good
/* Recommended */
color: #ebc;
```

#### 4.1.9 前缀

选择器前面加上特殊应用标识的前缀（可选）。

在大型项目，以及嵌入其他项目代码、外部站点代码，在 ID/Class 名字前加上标识性前缀（命名空间），使用简短的唯一标识符，后面使用短破折号 `-` 链接。

使用命名空间有助于防止命名冲突，便于维护，例如在搜索和替换操作中。

```css good
.adw-help {} /* AdWords */
#maia-note {} /* Maia */
```

#### 4.1.10 ID/Class 名分隔符

用连字符 `-` 分隔 ID/Class 名中的单词。

除了连字符之外，不要通过任何字符（或无任何符号）连接选择器中的单词和简称，以便提高可读性和可扫描性。

```css bad
/* Not recommended: does not separate the words “demo” and “image” */
.demoimage {}

/* Not recommended: uses underscore instead of hyphen */
.error_status {}
```

```css good
/* Recommended */
#video-id {}
.ads-sample {}
```

#### 4.1.11 Hacks

避免用户代理 (user agent) 检测以及 CSS "hacks" —— 优先尝试使用其他的解决方案。

通过用户代理检测、特殊的 CSS filters、变通灵活的方法、hacks等技术手段解决样式差异问题虽然很诱人，但是为了可实现、可维护、高效率、易管理的代码管理，这些都应该是在万不得已、最后才采用的技术方案。项目倾向于采取阻力最小的方式，频繁使用代理检测和 hacks ，如此以往，会损害整个项目。

### 4.2 CSS 代码格式

#### 4.2.1 声明顺序

按字母顺序声明样式。

按字母顺序声明样式，易于记忆和维护。

用于浏览器兼容性前缀的声明在排序中应忽略。但是，CSS 属性中用于多个浏览器的兼容性前缀声明，应该进行排序（例如 -moz 前缀在 -webkit 之前）。

```css good
background: fuchsia;
border: 1px solid;
-moz-border-radius: 4px;
-webkit-border-radius: 4px;
border-radius: 4px;
color: black;
text-align: center;
text-indent: 2em;
```

    译者注：不要按字母顺序声明样式！

    因为：如 `position` 相关的 `top/right/bottom/left/z-index` 定位声明，如 `width/height` 声明，
    中间会有其它属性间隔，不能便捷的、逻辑上的添加和修改。

    建议按以下顺序声明样式，便于维护：

    - 影响文档流的属性(display/visibility/float/clear/position)
    - 盒模型的属性(width/height/margin/padding/border/outline)
    - 排版属性(font/line-height/text-align/text-indent/text-decoration/white-space/color)
    - 背景装饰属性(background/opacity/cursor/list-style)
    - 生成内容属性(content/quotes)
    - 其它CSS3属性，兼容性前缀打包自动添加 (border-radius/box-shadow/transition/transform/animation)

#### 4.2.2 代码块内容缩进

缩进所有代码块 ( `{}`之间的声明 ) 内容。

缩进所有[代码块](https://www.w3.org/TR/CSS21/syndata.html#block)内容，即规则和声明，以反映层次结构并提高可读性。

```css good
@media screen, projection {

  html {
    background: #fff;
    color: #444;
  }

}
```

#### 4.2.3 声明结束

每个声明都要用分号 `;` 结尾。

出于一致性和可扩展性的原因，以分号结束每个声明。

```css bad
/* Not recommended */
.test {
  display: block;
  height: 100px
}
```

```css good
/* Recommended */
.test {
  display: block;
  height: 100px;
}
```

#### 4.2.4 属性名结束

在属性名称冒号后面加一个空格。

出于一致性原因，声明中的属性和值之间添加一个空格（属性和冒号之间不要空格）。

```css bad
/* Not recommended */
h3 {
  font-weight:bold;
}
```

```css good
/* Recommended */
h3 {
  font-weight: bold;
}
```

#### 4.2.5 声明间隔

选择器和声明块之间加一个空格。

在最后一个选择器和[声明块](https://www.w3.org/TR/CSS21/syndata.html#rule-sets)开始的左大括号 `{` 之间添加一个空格。

左大括号与规则中的最后一个选择器处于一行。

```css bad
/* Not recommended: missing space */
#video{
  margin-top: 1em;
}

/* Not recommended: unnecessary line break */
#video
{
  margin-top: 1em;
}
```

```css good
/* Recommended */
#video {
  margin-top: 1em;
}
```

#### 4.2.6 选择器和声明间隔

将选择器和声明隔行分开。

每个选择器之间，每个声明之间都隔行分开。

```css bad
/* Not recommended */
a:focus, a:active {
  position: relative; top: 1px;
}
```

```css good
/* Recommended */
h1,
h2,
h3 {
  font-weight: normal;
  line-height: 1.2;
}
```

#### 4.2.7 规则间隔

从新的一行开始每个规则。

规则之间隔一个空白行。

```css good
html {
  background: #fff;
}

body {
  margin: auto;
  width: 50%;
}
```

#### 4.2.8 CSS 引号

对属性选择器和属性值使用单引号 `''` 而不是双引号 `""`。

不要在URI值 `url()` 中使用引号。

例外： `@charset` 规则中使用双引号 - [single quotation marks are not permitted.](https://www.w3.org/TR/CSS21/syndata.html#charset)。

```css bad
/* Not recommended */
@import url("https://www.google.com/css/maia.css");

html {
  font-family: "open sans", arial, sans-serif;
}
```

```css good
/* Recommended */
@import url(https://www.google.com/css/maia.css);

html {
  font-family: 'open sans', arial, sans-serif;
}
```

### 4.3 CSS Meta 规则

#### 4.3.1 注释

分组注释 (可选)。

如果可以，按功能、层级等方式对样式分组后统一写注释。独立成行。

```css good
/* Header */

#adw-header {}

/* Footer */

#adw-footer {}

/* Gallery */

.adw-gallery {}
```



## 最后

追求一致性。

如果要编辑代码，先查看已有代码的风格，与之保持一致。

约束一致性的编码环境需要一份公共的编码风格指南，参与者可以清晰明了要做成什么样，而不是考虑你 balabala 什么。这里仅介绍了统一风格的规则，以便开发者去了解和借鉴。保持自己的编码风格固然重要，但是你把自己代码添加到文件中，与现有的代码风格完全不同，这样会降低代码的可读性和可理解性，避免这样做。

山茶树和葡萄树 于 2018-08-02 译。
