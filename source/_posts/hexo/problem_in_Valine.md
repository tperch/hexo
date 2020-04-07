---
mathjax: false
date: 2020-03-02 10:41:39
title: 解决 Hexo 配置 Valine 报错问题
tags:
- Hexo
- 问题
categories:
- [Hexo]
cover: https://cdn.jsdelivr.net/gh/yunwanjia-cloud/blog/hexo/problem_in_Valine/problem_in_Valine.jpg
---
解决报错:
Code: undefined [410 GET https://avoscloud.com/1.1/classes/Comment]
Code 403: 访问被api域名白名单拒绝，请检查你的安全域名设置
<!-- more -->
　　很多 Hexo 主题都会集成很多评论系统, 我了解了一下最满意的还是 Valine. Valine 不用登陆就可以评论, 我本人就很讨厌登陆来登陆去的.
　　在主题的 "_config.yml" 文件中应该有关于 Valine 的配置, 可能长这个样子
```yaml
valine:
  enable: true # if you want use valine,please set this value is true
  appId:  # leancloud application app id
  appKey:  # leancloud application app key
  notify: true # valine mail notify (true/false) https://github.com/xCss/Valine/wiki
  verify: true # valine verify code (true/false)
  pageSize: 10 # comment list page size
  avatar: monsterid # gravatar style https://valine.js.org/#/avatar
  lang: zh-cn # i18n: zh-cn/en
  placeholder: 快快献上你的评论~ # valine comment input placeholder(like: Please leave your footprints )
  guest_info: nick,mail,link #valine comment header info
  bg: /img/comment_bg.png # valine background
  count: true # top_img显示评论数
```
　　appId 与 appKey 自己注册 [leancloud](https://www.leancloud.cn/) 然后创建应用获取, 但是配置完出现报错: `Code: undefined [410 GET https://avoscloud.com/1.1/classes/Comment]`, 出现问题的原因在于何处? 上谷歌查了查, 有人说是华东节点有 bug, 可是我选的是华北节点啊, 然后看到[这篇文章](https://rightofriver.github.io/2019/10/30/ValineBug1/#fn:3), 成功解决了我的问题. 首先是 "_config.yml" 里的配置和注释 '#' 号不能连在一起, 也就是 "xxxx# xxx" 要改成 "xxxx # xxx".
然后可能又出现一个报错: `Code 403: 访问被api域名白名单拒绝，请检查你的安全域名设置`, 这个报错就很简洁明了了, 把你的域名添加到 "安全中心" 的 "Web 安全域名" 里, 注意端口等等要完全正确.
![](https://cdn.jsdelivr.net/gh/yunwanjia-cloud/blog/hexo/problem_in_Valine/1.png)
　　最后问题顺利解决!