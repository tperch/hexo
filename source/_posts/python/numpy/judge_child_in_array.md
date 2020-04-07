---
mathjax: false
date: 2020-02-26 19:45:16
title: numpy 中判断某字符串 array 是否含有子字符串
tags: 
- Numpy
- Python
categories:
- [Python, Numpy]
cover: https://cdn.jsdelivr.net/gh/yunwanjia-cloud/blog/python/numpy/judge_child_in_array/judge_child_in_array.jpg
---
本想着有什么函数可以直接调用的, 结果网上找了一大圈没找到, 还有好多错的...
<!-- more -->
```python
numpy.char.count(a, sub, start=0, end=None)
```
　　该函数是用来计数 sub 在 a 中出现多少次, 我们稍加修改就能达到我们要的效果.
```python
numpy.char.count(a, sub, start=0, end=None) != 0
```
　　函数的具体介绍看[官方文档](https://numpy.org/devdocs/reference/generated/numpy.char.count.html#numpy.char.count).

举例:
```python
import numpy as np
a = np.array(['abc', 'akjs', '23ha', 'sdfg', 'arge', '8908d', 'aaaab', 'hhdaa', 'wer'], dtype='str')
np.char.count(a, 'a')
# array([1, 1, 1, 0, 1, 0, 4, 2, 0])
np.char.count(a, 'a') != 0
# array([ True,  True,  True, False,  True, False,  True,  True, False])
```