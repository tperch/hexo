---
mathjax: false
date: 2020-04-04 11:58:18
title: "hexo d 命令后 github 无法更新问题"
tags: 
- 问题
- Hexo
categories:
- [Hexo]
cover: https://cdn.jsdelivr.net/gh/yunwanjia-cloud/blog/hexo/hexo_d_github_problem/hexo_d_github_problem.png
---
<!-- more -->
# 问题

　　`hexo d` 后查看仓库, 发现根本没有更新, 仔细观察 shell 的输出, 还会看到如下报错

```shell
Branch master set up to track remote branch master from git@github.com:xxxx/xxxx.github.io.git.
```

其中 xxxx 是你的 github 用户名.

# 解决方案

　　删除 `hexo/.deploy_git` 文件, 然后重新尝试 `hexo d` , 就可以成功更新了.

~~这应该不算水文吧.~~