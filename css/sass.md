## 一、安装和使用


- 安装Ruby
```bash
// MAC下的安装方式
brew install ruby
vim ~/.bash_profile

// 如果是安装到/usr/local/bin下，且这个还没配置的话
export PATH=/usr/local/bin:$PATH

// 检测ruby是否安装成功
ruby --version
```
- 安装SASS
```bash
gem install sass
```

- 使用
```bash
1 sass test.scss
2 sass test.scss test.css
3 sass --style compressed test.sass test.css
```

- 监听使用
```bash
// watch a file
sass --watch input.scss:output.css

// watch a directory
sass --watch app/sass:public/stylesheets
```

- 在线转换器
[在线转换器](http://sassmeister.com/)

- SASS编译风格

> nested: 嵌套缩进的css代码，它是默认值

> expanded: 没有缩进的、扩展的css代码

> compact: 简洁格式的css代码

> compressed: 压缩后的css代码

## 二、基本用法

> **变量**

- 变量以$开头

```sass
$blue: blue;
div {
    color: blue;
}
```

- 变量在字符串中，就必须写在#{}中

```sass
$side: left;
.rounded {
    border-#{$side}-radius: 5px;
}
```
> **计算功能**

```sass
$width: 100px;
div {
    margin: (14px / 2);
    top: 50px + 100px;
    left: $width * 10%;
}
```

> **嵌套**

- 嵌套方式一

```sass
span a,div a {
    color: red;
}
可以写成
span,div {
    a {
        color: red;
    }
}
```
- 嵌套方式二
```sass
#content span, #content div {
    color: red;
}
可以写成
#content {
    span,div {
        color: red;
    }
}
```
- 嵌套方式三
```sass
p {
    border-width: 1px;
    border-color: red;
    border-style: solid;
}
可以写成
p {
    border: {
        width: 1px;
        color: red;
        style: solid;
    }
}
```
- 引用父元素
```sass
a {
    &:hover {
        color: red;
    }
}
编译以后的效果是
a:hover {
    color: red;
}
```
> **导入外部文件**

- sass文件，如果不生成独立的文件，则文件名以\_开头，导入时可省略\_与后缀名
```sass
// 有个_head.sass
@import "head";
```
- css文件
```sass
// 有个head.css
@import "head.css";
```

> **颜色函数**

```sass
lighten(#cc3,10%) // #d6d65c
darken(#cc3,10%) // #a3a329
grayscale(#cc3) // #808080
complement(#cc3) // 33c
```

> **注释**

SASS共有2种注释方式
- /* 注释内容 */    保留到编译后的文件中
- // 注释内容       不保存在编译后的文件中
- /*! 重要注释内容 */ 保留到编译后的文件中，哪怕是压缩版本也会保留的。

## 混合器
重用代码块
- 简洁版mixin
```sass
@mixin rounded-corners{
    -webkit-border-radius: 5px;
    -moz-border-radius: 5px;
    border-radius: 5px;
}
调用
.notice{
    border: 1px solid red;
    @include rounded-corners;
}
```
- 带参数的mixin
```sass
@mixin link-colors($normal,$hover,$visited) {
    color: $normal;
    &:hover { color: $hover; }
    &:visited { color: $visited; }
}
调用
a {
    @include link-colors(blue,red,green);
}
也可以这样调用
a {
    @include link-colors(
        $normal: blue,
        $visited: green,
        $hover: red
    );
}
```

- 带默认参数值的mixin
```sass
@mixin link-colors($normal,$hover: $normal,$visited: $normal) {
    color: $normal;
    &:hover { color: $hover; }
    &:visited { color: $visited; }
}
调用
a {
    @include link-colors(blue);
}
```

## 继承

> 简单选择器的继承

<code>.serious-error</code>继承<code>.error</code>
以class="serious-error"修饰的html，最终展示的效果是class="serious-error error"

```sass
.error {
    border: 1px solid red;
    background-color: #fdd;
}
.serious-error {
    @extend .error;
    border-width: 3px;
}
```

> 一条样式继承复杂选择器

<code>.serious-error</code> <code>@extend</code> <code>.important.error</code>

<code>.important.error</code> 和 <code>h1.important.error</code>的样式都会被<code>.serious-error</code>继承

<code>.important</code> 和 <code>.error</code>的样式不会被<code>.serious-error</code>继承

> 完全命中才继承

<code>( #main .serious-error)</code> <code>@extend</code> <code>.error</code>

<code>#main .error</code>这种选择器是不能被继承的

## 高级用法

> **条件语句**

- @if
```sass
p {
    @if 1 + 1 == 2 { border: 1px solid red; }
    @if 5 < 3 { border: 2px solid blue; }
}
```
- @if...else
```sass
@if lightness($color) > 30% {
    background-color: #000;
} @else {
    background-color: #fff;
}
```

> **循环语句**

- @for循环
```sass
// 第一种方式包括end
@for $i from 1 to 10 {
    .border-#{$i} {
        border: #{$i}px solid blue;
    }
}

// 第二种方式不包括end
@for $i from 1 through 10 {
    .border-#{$i} {
        border: #{$i}px solid blue;
    }
}
```
- @while循环
```sass
$i: 6;
@while $i > 0 {
    .item-#{$i} { width: 2em * $i; }
    $i: $i - 2;
}
```

> **自定义函数**

```sass
@function double($n){
    @return $n * 2;
}

#sidebar {
    width: double(5px);
}
```




