---
mathjax: false
date: 2020-02-26 22:14:47
title: jupyter 公式渲染问题
tags: 
- Jupyter
- LaTeX
- 问题
categories:
- [Python,Jupyter]
cover: https://cdn.jsdelivr.net/gh/yunwanjia-cloud/blog/python/jupyter/jupyter_formula_render/jupyter_formula_render.png
---
<!-- more -->
　　jupyter lab 中的公式有时候很丑, 想要变得好看一点, 于是找到了 jupyter 中的一个插件解决该问题. 具体怎么装看[官方文档](https://jupyterlab.readthedocs.io/en/stable/user/extensions.html). 开启插件后搜索 katex-extension 装上, 然后等一会它会告诉你是否 `rebuild` 啥的, 一路点 `是` , 等一会就好了.

成果:
![](https://cdn.jsdelivr.net/gh/yunwanjia-cloud/blog/python/jupyter/jupyter_formula_render/1.png)
　　好看多了.