## 安装
说明：在ruby的基础上安装
如果下载不下来。更改源为：http://ruby.taobao.org 
- 查看源 <code>gem sources</code>
- 添加源 <code>gem sources -a url地址</code>
- 删除源 <code>gem sources -r url地址</code>
- 更新源缓存 <code>gem sources -u</code>
```bash
sudo gem install compass
```

## 初始化

> 创建项目

```bash
compass create myproject
```

> 编译项目

- 默认编译
```bash
compass compile
```

- 完全压缩编译
```bash
compass compile --output-style compressed
```
- 编译发生改动与未改动的所有文件
```bash
compass compile --force
```

- 在配置中直接配置编译类型
```bash
vim config.rb
output_style = :compressed
```
- 监听编译
```bash
compass watch
```

## Compass模块的使用
五种模块：reset、css3、layout、typography、utilities

> reset模块【重置浏览器默认样式】

```sass
@import "compass/reset";
```

> css3模块【提供19种css3命令】

```sass
@import "compass/css3"
```
- 圆角
```sass
.rounded {
	@include border-radius(5px);	
}
```
- 透明
```sass
.opacity {
	@include opacity(0.5);
}
```
- 行内区块
.inline-block {
	@include inline-block;
}

> layout模块【提供布局功能】

```sass
@import "compass/layout"
```
- 指定页面总是出现在浏览器最底端
.footer {
	@include sticky-footer(54px);
}
- 指定子元素占满父元素的空间
.stretch-full {
	@include stretch;	
}

> typography模块【提供版式功能】

```sass
@import "compass/typography";
a { @include link-colors($normal,$hover,$active,$visited,$focus)}
```
> utilities模块【提供一些公用的】

- 清除浮动
```sass
@import "compass/utilities";
.clearfix {
	@include clearfix;
}
```
- 表格
@import "compass/utilities";
table {
	@include table-scaffolding;
}

> Helper函数

- 将图片转成data协议的数据
```sass
@import "compass";
.icon {background-image: inline-image("icon.png")}
```
- 获取图片宽度与高度[image-width()、image-height()]




