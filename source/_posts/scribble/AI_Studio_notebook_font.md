---
mathjax: false
date: 2020-02-26 19:45:16
title: 百度 AI Studio 的 notebook 字体问题
tags: 问题
categories: 杂文
cover: https://cdn.jsdelivr.net/gh/yunwanjia-cloud/blog/scribble/AI_Studio_notebook_font/AI_Studio_notebook_font.png
---
<!-- more -->
　　在用百度 AI Studio 中的 notebook 时, 发现光标会偏移, 有时字体也很难看, 浏览器怎么设置都没有用, 例如下图就是光标偏移.
![](https://cdn.jsdelivr.net/gh/yunwanjia-cloud/blog/scribble/AI_Studio_notebook_font/1.png)
　　然后发现了一个很好用的插件可以解决问题: Stylus (怎么下载安装自己百度)

　　就这玩意
![](https://cdn.jsdelivr.net/gh/yunwanjia-cloud/blog/scribble/AI_Studio_notebook_font/2.png)
　　编写样式给 aistudio.baidu.com , 填写以下内容:
```css
pre, code, kbd, samp {
    font-family: monospace !important;
}
.cc .ace_editor {
    font-family: monospace !important;
}
.cc pre {
    font-family: Arial !important;
}
```
　　解决!
　　摸索一下就可以随便改网页字体了.
注: 我的是 ubuntu 系统.