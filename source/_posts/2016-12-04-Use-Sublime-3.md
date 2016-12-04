---
title: Use Sublime 3
date: 2016-12-04 19:53:59
tags: [工具]
---
# 前言

Sublime Text 3 文本处理神器。

<!--more-->
# 快捷键篇

Ctrl+D 选词

Ctrl+L 选中整行

Ctrl+← 向左单位性地移动光标，快速移动光标。

Ctrl+→ 向右单位性地移动光标，快速移动光标。

Ctrl+/ 注释整行或选中内容

Ctrl+K+B 开启/关闭侧边栏

Ctrl+K+U 改为大写

Ctrl+K+L 改为小写

未完待遇，先记住几个常用的

# 插件篇

## Package Control 安装

通过 ` ctrl + `` ` 或者 ` View > Show Console ` 菜单打开命令控制台输入：

```python
import urllib.request,os,hashlib; h = 'df21e130d211cfc94d9b0905775a7c0f' + '1e3d39e33b79698005270310898eea76'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)
```

## Markdown 支持

markdown 写作插件：MarkdownEditing

MarkDown 预览插件：OmniMarkupPreviewer（支持 Tex 公式）

## Python 支持

SublimeCodeIntel：代码补全，好像是个通用语言查件

## 中文编码友好支持

GBK Support
