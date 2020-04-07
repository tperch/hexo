---
mathjax: false
date: 2020-04-06 09:58:57
title: "git clone 速度太慢? 一招教你加速 git (效果显著)"
tags:
- Git
categories:
- Git
cover: https://cdn.jsdelivr.net/gh/yunwanjia-cloud/blog/git/quickly_git_clone/quickly_git_clone.jpg
---
　　在天朝, 由于众所周知的原因, git clone github 仓库的速度非常的慢, 所以这里就介绍一个加速 git 的方法.
<!-- more -->
# fork 仓库

　　如果是自己的仓库可以跳过, 如果要 git clone 别人的仓库, 那就先 fork 到自己的 github 仓库中.

# 注册码云

　　首先注册一个码云账号 (可以用 github 账号登陆) , [点此进入](https://gitee.com/). 

![](https://cdn.jsdelivr.net/gh/yunwanjia-cloud/blog/git/quickly_git_clone/1.png)

点击 `从 GitHub/GitLab 导入仓库` 

![](https://cdn.jsdelivr.net/gh/yunwanjia-cloud/blog/git/quickly_git_clone/2.png)

找到你要 git clone 的仓库, 然后导入.

# git clone 码云仓库

　　成功导入后, 进入你已经导入成功的码云仓库, 然后使用 https 方式 clone.

![](https://cdn.jsdelivr.net/gh/yunwanjia-cloud/blog/git/quickly_git_clone/3.png)

然后你就会发现...简直是飞速!!!

　　如果想要 git push 到 github 而不是码云, 那么只要更改远程仓库地址为 github 就好了.