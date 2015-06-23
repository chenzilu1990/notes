## 下载安装
- [官网下载](http://www.sublimetext.com/)
- 双击安装

## 插件管理
> 安装Install Package

快捷键：<code>ctrl + `</code>
```python
import  urllib.request,os;pf='Package Control.sublime-package';ipp=sublime.installed_packages_path();urllib.request.install_opener(urllib.request.build_opener(urllib.request.ProxyHandler()));open(os.path.join(ipp,pf),'wb').write(urllib.request.urlopen('http://sublime.wbond.net/'+pf.replace(' ','%20')).read())
```

> 安装ConvertToUTF8

快捷键： <code>cmd + shift + p</code>

说明： 支持GBK GB2312

> 安装Markdown Preview

说明：对Markdown文本进行预览
- 设置语言：cmd + shift + p  输入ssm 回车
- 预览： cmd + shift + p 输入mpp 回车

> 安装Monokai Extended

说明：markdown高亮显示

> 安装Emmet

说明：快速编辑HTML代码

> 安装JsFormat

说明：格式化js
- 快捷键 ctrl + option + f

> 安装 ColorPicker

说明： 调色板

这个快捷键与ConvertToUTF8冲突，所以更改下ConvertToUTF8的快捷键
<code>Sublime Text --> Preferences --> Browse Packages</code>
```bash
Default.sublime-keymap
```

> 安装 AutoFileName

说明：自动完成文件名或是图片路径的选择

- 快捷键 cmd + shift + c

> 安装 SideBarEnhancements与SideBarFolders

说明： 管理项目，在菜单栏最后一个多了个Folders可以操作

## 快捷键
- 支持VIM，按ESC进入VIM模式
Preferences -> Settings - User
```json
{
	"ignored_packages":[]
}
```
- 小窗口并列
<code>cmd + option + 1,2,3,4</code>

- 小窗口并排
<code>cmd + option + shift + 2,3,4</code>

- 显示隐藏菜单栏
<code>cmd + k  + b</code>

- 跳转到第几行
<code>ctrl + g</code>

## 小问题

> SASS编译不支持中文？

找engine.rb文件[<code>ruby安装目录下去找</code>]

```bash
/Library/Ruby/Gems/2.0.0/gems/sass-3.4.8/lib/sass/engine.rb
```
更改engine.rb文件

在require完之后加个：<code>Encoding.default_external = Encoding.find('utf-8')</code>




