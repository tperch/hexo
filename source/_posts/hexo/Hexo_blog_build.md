---
mathjax: false
date: 2020-03-07 17:37:47
title: 史上最全的 Hexo 博客搭建配置完全指南
tags: 
- Hexo
- 教程
categories:
- [Hexo]
cover: https://cdn.jsdelivr.net/gh/yunwanjia-cloud/blog/hexo/Hexo_blog_build/Hexo_blog_build.png
---
　　本篇博客基于 `Centos 7.x` root 用户.
　　最近利用 Hexo + Github Pages 搭建了一个博客, 总体来说比较满意, 中间也踩了不少坑. 于是将我的配置过程全部记录下来, 就有了这篇博文.
　　关于 Hexo 搭建配置的博文网上还是挺多的, 但是零零散散, 这篇博文就当成是一个大合集吧. 废话不多说, 下面开始我们的正篇.
<!-- more -->
# 搭建

## 准备环境

### 安装 Git

```shell
sudo yum install git-core
```

### 安装 Node.js

```shell
wget -qO- https://raw.github.com/creationix/nvm/master/install.sh | sh
source ~/.bash_profile
nvm install stable
```

### 安装 Hexo

```shell
mkdir hexo
npm install -g hexo-cli
cd hexo/
hexo init
```

测试服务

```shell
hexo server
```

　　这时你可以打开浏览器访问 [http://localhost:4000](http://localhost:4000) 就可以看到你刚刚搭建成功的博客页面了. 当然如果你使用的是云服务器, 那么同样可以打开 [(云服务器的 ip):4000]() 来访问博客.

## 将博客部署到 Github

　　把博客部署到 Github 是大多数站长的选择. 

### 注册 Github 账号

　　首先你要有一个 Github 账号 (已有账号可以跳过), [点此](https://github.com/)前往注册. 输入你的邮箱和你起的用户名, 密码就可以注册了. 这里我们假设你的用户名为 `yunwanjia-cloud` 邮箱为 `371622558@qq.com` (下面所有出现用户名和邮箱的内容换成你自己的就好了).

### 设置 user.name 和 user.email

　　这里要给 git 设置变量.

```shell
git config --global user.name "yunwanjia-cloud"
git config --global user.email "371622558@qq.com"
```

### 配置 SSH 密匙

```shell
ssh-keygen -t rsa -C user.email
/root/.ssh/id_rsa
```

　　然后直接输入回车回车.
　　这时进入到 `/root/.ssh/` 目录下查看 `id_rsa.pub` 文件, 你可以使用如下命令

```
vi /root/.ssh/id_rsa.pub
```

　　这时就用 vim 打开了该文件, 复制文件里的所有内容 (所有内容, 一个字符都不要漏) . 然后[到 Github 添加 ssh 密匙](https://github.com/settings/keys).
　　点击 `New SSH key` 按钮进行添加
![](https://cdn.jsdelivr.net/gh/yunwanjia-cloud/blog/hexo/Hexo_blog_build/1.png)
![](https://cdn.jsdelivr.net/gh/yunwanjia-cloud/blog/hexo/Hexo_blog_build/2.png)
　　点击 `Add SSH key`确认添加.

### 创建仓库

　　在登陆状态下打开 [Github 主页](https://github.com/), 点击 `New` 创建新仓库.
![](https://cdn.jsdelivr.net/gh/yunwanjia-cloud/blog/hexo/Hexo_blog_build/3.png)
　　这里要注意, 这个仓库的命名是有一定格式的, 格式是: 用户名.github.io,
比如我的就是 yunwanjia-cloud.github.io (还记得我之前说的吗, 出现用户名和邮箱通通换成你自己的就好了).
![](https://cdn.jsdelivr.net/gh/yunwanjia-cloud/blog/hexo/Hexo_blog_build/4.png)
　　点击 `Create repository` 创建该仓库. 由于我已经创建了这个仓库, 所以有报错.

### 配置 _config.yml

　　进入到博客根目录 (也就是一个名字叫 hexo 的目录, 一般在你的主目录下), 
打开一个名字叫 _config.yml 的文件, 找到 `deploy` 这个部分, 修改成如下内容:

```yml
deploy:
    type: git
    repo: git@github.com:yunwanjia-cloud/yunwanjia-cloud.github.io.git
    branch: master
```

保存一下. (将所有用户名和邮箱都改成自己的, 这已经是第三次提醒了哦~)

### 部署

清空静态页面

```shell
hexo cl
```

生成静态页面

```shell
hexo g
```

先运行下面这条命令否则直接部署会报错

```shell
npm install hexo-deployer-git --save
```

然后将 public 文件内容部署到 Github 仓库

```shell
hexo d
```

`hexo cl&&hexo g&&hexo d` 称为部署三件套.
　　此时你的个人博客就部署成功啦! 你可以通过访问 [https://yunwanjia-cloud.github.io](https://yunwanjia-cloud.github.io) 来浏览你的博客页面 (还记得前面提示了三次啥吗~) .
　　这已经算是一个完整的 Hexo 博客了, 之后会有进一步的美化配置教程.

## Hexo 发布文章简单介绍

　　在 Hexo 博客目录内 (包括其子目录) 执行

```shell
hexo new "文章名"
```

就会在 `hexo/source/_posts` 下创建一个 `文章名.md` 文件, 里面可以写下你的 markdown 文章, 然后通过执行部署三件套, 就能部署到你的个人博客里.
　　在文章正文前, 一般都有由两行 `---` 包起来的内容, 称为 Front-matter .在 Hexo 官方文档里, 是这么说的

> Front-matter 是文件最上方以 `---` 分隔的区域，用于指定个别文件的变量.

比如

```markdown
---
title: Hello World
date: 2013/7/13 20:46:25
---
```

干什么的应该从名字就能看出来. 这里不过多介绍如何写文章, [官方文档](https://hexo.io/zh-cn/docs/)已经写得很详细了.

## _config.yml 配置介绍

　　_config.yml 这个文件我们前面已经更改过它一次了, 就是在配置部署的时候, 还记得吗? 这是整个 Hexo 博客的配置文件, 现在我们列出主要需要更改的地方, 按照关键字去查找更改就好了.

* **所有配置的配置名和配置值都要隔一个空格, 比如说 title 这个配置, 必须要写成 `title: 云玩家` 而不可以写成 `title:云玩家`. 前后是一个空格的区别!!! 这是 yaml (即以 `.yml` 为后缀的文件) 的语法, 要严格遵守.**

### site

```yml
# Site
title: # 网站标题
subtitle: # 网站副标题
description: # 网站描述
keywords: # 网站关键词
author: # 网站作者
language: # 语言, 一般填 'zh-CN'
timezone: # 时区, 可以不填
```

暂时就这一项需要配置.

# 美化

## 更换域名

　　我们常常看到别人的博客域名并不是 xxxx.github.io 形式的, 而是其他的域名. 这是因为别人绑定了自己的域名. 下面就来教你如何绑定自己的域名.

### 购买域名

　　首先, 你要拥有一个域名, 域名可以在很多地方买到, 比如阿里云, 腾讯云等等. 不同的域名价格也不同, 但是基本上首次购买的费用都要远远低于续费的费用, 所以如果看准了一个域名, 就尽量买久一点吧. 我的 `cloudplayaer.site` 域名购买 10 年花了 170 左右, 个人觉得不是很贵. 购买域名过程中的实名等等步骤这里就不再详细讲解.

### 域名解析

　　购买了域名后, 可以添加解析到你的 Github Pages. 下面我们以腾讯云为例. 首先在你的域名管理处找到你要解析的域名, 点击 `解析` 按钮, 进入解析界面. 然后点添加记录, 就可以添加解析记录了.
　　这条解析记录我们需要填的有 6 个值, 分别是 `主机记录`, `记录类型`, `线路类型`, `记录值`, `TTL`. 下面我们来一一说明.

主机记录: 主机记录其实就是域名前缀, 比如说 www.xxxx.com, 域名其实就是 xxxx.com, 而主机记录是 www. 一般博客的主机记录可以设置为 blog, 比如我的博客就是 [blog.cloudplayer.site](https://blog.cloudplayer.site). blog 是我的域名主机记录, 我的域名是 cloudplayer.site. 当然有些前缀比较特殊, 比如说 `*`, `*` 是指泛解析, 就是说可以解析所有前缀. 还有就是 `@`, 这个前缀是说解析主域名, 也就是不带任何前缀.

记录类型: 这里不详细说明所有的记录类型, 只说明我们要用到的 `CHAME` 解析, 即指向另一个域名 (所以你这里应该知道要填啥了吧. 对了! 就是 CHAME).

线路类型: 我们这里填默认就好 (其他选项到后面双部署的时候会用到).

TTL: 这个值是你的解析记录在 DNS 中的缓存时间, 你可以简单理解为, TTL 值越大, 解析会越快, 但是一旦更改, 更改生效的时间就会更久. 我是设置为默认的 600秒, 即 10 分钟.

所有值填完之后就可以点击 `保存` 添加解析记录了.

### Github Pages 添加解析

创建 CHAME 文件

进入 hexo 主目录并输入以下命令

```shell
touch source/CNAME
```

　　进入该文件并添加你刚刚解析的域名, 记得要加上你的前缀, 比如你解析的是 blog 主机记录, 你就要写上 blog.xxxx.com (这里域名为 xxxx.com). 比如我的就写 [blog.cloudplayer.site](https://blog.cloudplayer.site).
　　最后执行部署三件套 `hexo cl&&hexo g&&hexo d` 后就可以用你自己的域名访问你的博客啦!

## 修改博客默认主题

　　大家可以看到[我的博客](https://blog.cloudplayer.site)界面很好看, 而且还有很多不同的博客界面, 这就涉及到主题的配置了. 这里配置主题以 [Butterfly](https://github.com/jerryc127/hexo-theme-Butterfly) 这个主题为例.

### 下载主题并使用

　　在 Hexo 根目录下执行命令

```shell
git clone -b master https://github.com/jerryc127/hexo-theme-Butterfly.git themes/Butterfly
```

如果没有 cheerio 则需要安装

```shell
npm install cheerio --save
```

下载 Butterfly 主题. 然后就会看到根目录下 theme 这个文件夹里多了一个 Butterfly 文件夹. 进入博客根目录的 _config.yml 文件 (不是 theme 里的哦), 找到 theme 这一项, 把值改为 Butterfly.
![](https://cdn.jsdelivr.net/gh/yunwanjia-cloud/blog/hexo/Hexo_blog_build/5.png)
　　然后部署三件套, 之后再打开你的博客, 大概率会发现无法正常打开, 那么这时候需要安装 pug 以及 stylus 的渲染器

```shell
npm install hexo-renderer-pug hexo-renderer-stylus --save
```

重新部署就会发现你的博客大变样了.

### 配置主题

　　此时就要配置我们的主题了, 配置项大多都在 `hexo/themes/Butterfly/_config.yml` 这个文件里. 我们打开它. 同样的这里列出建议改动的地方.
　　再次提醒

* **所有配置的配置名和配置值都要隔一个空格, 比如说 title 这个配置, 必须要写成 `title: 云玩家` 而不可以写成 `title:云玩家`. 前后是一个空格的区别!!! 这是 yaml (即以 `.yml` 为后缀的文件) 的语法, 要严格遵守.**

banner: 查找 banner 关键字, 可以修改默认 banner 为你自己的图片. 什么是banner 呢, 其实就是博客里页面中的各种图片 (不是文章里的图片).
　　比如这三项

```yml
# the banner image of archive page
archive_img: https://cdn.jsdelivr.net/gh/yunwanjia-cloud/yunwanjia-cloud.github.io/img/banner/new_3.jpg

# the banner image of tag page
tag_img: https://cdn.jsdelivr.net/gh/yunwanjia-cloud/yunwanjia-cloud.github.io/img/banner/7.jpg

# the banner image of category page
category_img: https://cdn.jsdelivr.net/gh/yunwanjia-cloud/yunwanjia-cloud.github.io/img/banner/new_5.jpg
```

分别代表归档, 标签, 分类页的 banner (该页面上面的大图). 当然还有 index 的banner (主页). 这里要注意, 所谓标签, 分类页的 banner 代表的是具体标签, 分类里的图, 而不是标签, 分类. 分类的图 ~~(好吧你们肯定听不懂我在说啥)~~. 下面看例子
这是标签
![标签](https://cdn.jsdelivr.net/gh/yunwanjia-cloud/yunwanjia-cloud.github.io/hexo/Hexo_blog_build/6.png)
这是具体标签
![具体标签](https://cdn.jsdelivr.net/gh/yunwanjia-cloud/yunwanjia-cloud.github.io/hexo/Hexo_blog_build/7.png)
明白区别了吗, 标签包含了具体标签, 具体标签被标签包含!!
所以上面更改的是具体标签的图, 当然两个都可以改成同一个, 我就是这么做的. 标签页如何更改要具体看下面 `文章 cover` 的内容.

favicon: 即网站图标

social: 可以更改为你的社交账号如 Github, QQ邮箱等

avatar: 即头像

canvas_ribbon: 即各种彩带特效, 可以自己一个个开启试试效果

## menu 介绍

　　通过修改 menu , 可以实现增加, 减少页面. 比如有些博客有 `关于我(about)` 页面, 有些博客有 `影视`, `音乐` 等界面. 这些都是通过生成页面并修改 menu 实现的.

### 修改 menu

　　进入博客主题的 _config.yml 配置文件, 搜索 `menu` 关键字, 就可以快速找到 menu 的配置项. 可能长这个样子

```yml
menu:
  Home: / || fa fa-home
  Archives: /archives/ || fa fa-archive
  Tags: /tags/ || fa fa-tags
  Categories: /categories/ || fa fa-folder-open
  Link: /link/ || fa fa-link
  About: /about/ || fa fa-heart
  List||fa fa-list:
    - Music || /music/ || fa fa-music
    - Movie || /movies/ || fa fa-film
```

下面我们来详细介绍.
　　添加一个页面的格式是

```yml
页面名: /路径/ || fa fa-图标名
```

页面名就是页面名 ~~(废话)~~ , 路径是相对于你的博客路径, 比如说你的博客主页是 [blog.cloudplayer.site](https://blog.cloudplayer.site) , 那么相对路径 `/tags/` 就是 [blog.cloudplayer.site/tags/](https://blog.cloudplayer.site/tags/)而图标名可能要说明一下,  hexo博客菜单所使用的图标都是用的 Font Awesome , 它并不是一张图片，你可以理解他就是一种字体. 它为您提供可缩放矢量图标, 它可以被定制大小、颜色、阴影以及任何可以用CSS的样式. 想要了解更多可以看[中文官网](http://www.fontawesome.com.cn/), 想要什么图标也可以上去查它的名字.
　　这里还有一个比较特殊的一项

```yml
  List||fa fa-list:
    - Music || /music/ || fa fa-music
    - Movie || /movies/ || fa fa-film
```

这项其实是生成了一个子菜单, 格式就是

```yml
子菜单名||fa 图标名:
  - 页面1 || /路径1/ || fa fa-图标名1
  - 页面2 || /路径2/ || fa fa-图标名2
  - ....(依此类推)
```

### 分类, 标签页等的生成

　　修改了 menu 后, 页面其实并没有生成, 博客一开始是没有这些页面的, 点击会 404. 如何生成这些页面呢?
![](https://cdn.jsdelivr.net/gh/yunwanjia-cloud/blog/hexo/Hexo_blog_build/8.png)
　　执行以下代码

```shell
hexo new page tags
hexo new page categories
```

就可以生成相应页面, 更进一步的, 你可以根据你配置的 menu 生成任意的自定义页面, 即使用

```shell
hexo new page xxxx
```

来生成 `xxxx` 这个页面. 如 `about` 关于我页面, 只需要执行

```shell
hexo new page about
```

就好了.

# 增加功能

## 添加 mathjax 引擎使博客支持 LaTeX

　　LaTeX 数学公式对于我这种写文章经常用数学公式的非常重要, 当然如果你不需要完全可以跳过这段.
　　有很多主题其实已经配置好了 mathjax, 这里来说明如何配置.
　　进入主题的 _config.yml 文件, 找到 mathjax 这一项配置, 改成如下

```yml
mathjax:
  enable: true
  # true 表示每一頁都加載mathjax.js
  # false 需要時加載，須在使用的Markdown Front-matter 加上 mathjax: true
  per_page: false
```

`per_page` 这一项最好为 `false` 这样在不需要数学公式的时候可以节省加载时间. 如果你想在某篇文章使用 mathjax 引擎的话, 就在这个文章的 Front-matter (还记得这是什么吗) 里加入 `mathjax: true` 就好了.
　　当然有些主题本身没有集成 mathjax, 怎么办呢. 这里给出解决方案.

### 使用 Kramed 代替 Marked

　　Hexo 默认的渲染引擎是 marked，但是 marked 不支持 mathjax. kramed 是在 marked 的基础上进行修改而来的.
　　执行以下命令

```shell
npm uninstall hexo-renderer-marked --save
npm install hexo-renderer-kramed --save
```

### 安装 hexo-renderer-mathjax 包

```shell
npm install hexo-renderer-mathjax --save
```

重新部署, 成功显示数学公式. 样例[看这](https://blog.cloudplayer.site/machine_learning/watermelon_book/answer/7/).

* **mathjax 默认不渲染 `$$` 内的公式 (即所谓行内公式), 只渲染 `$$$$` 内公式 (即所谓行间公式), 而各大博客网站 (如简书, 博客园, CSDN) 所用数学引擎都是 katex , 因此迁移会有一点问题. 而且还有一个问题就是 LaTeX 中的下划线 `_` 在 markdown 中的含义是斜体, 会发生歧义, 所以我采用了一种笨拙的方法来解决这个问题, 我写了一个 Python 脚本当作 "转换器", 主要原理就是把所有单个的 `$` 都变成 `$$`, 这样啥问题都解决了. **

### 开启使用

　　一般来说在主题的配置文件中都会有 mathjax 的选项, 设置值为 `true` . 由于渲染 mathjax 会比较慢, 所以默认应该是并非每个页面都渲染, 如果要使用需要在要渲染的文章的 Front-matter 里加入

```markdown
mathjax: true
```

这样就能开启使用了.

## Valine 评论功能

　　为什么是 Valine 呢? 因为我喜欢. ~~(不用登陆啥的太方便了)~~
　　同样的, 很多 Hexo 主题集成了 Valine 评论系统, 我们先在主题的 _config.yml 文件中找到 `Valine` 这个配置

```yml
# valine comment system. https://valine.js.org
valine:
  enable: false # if you want use valine,please set this value is true
  appId: # leancloud application app id
  appKey: # leancloud application app key
  notify: false # valine mail notify (true/false) https://github.com/xCss/Valine/wiki
  verify: false # valine verify code (true/false)
  pageSize: 10 # comment list page size
  avatar: monsterid # gravatar style https://valine.js.org/#/avatar
  lang: en # i18n: zh-cn/en
  placeholder: Please leave your footprints # valine comment input placeholder(like: Please leave your footprints )
  guest_info: nick,mail,link #valine comment header info
  bg: /img/comment_bg.png # valine background
  count: false # top_img顯示評論數
```

`enable` 改成 `true` appId 与 appKey 这两项的值需要通过 [LeanCloud](https://www.leancloud.cn/) 获得.
　　首先当然是先注册, 如何进入到[控制台](https://leancloud.cn/dashboard/applist.html#/apps), 创建一个应用, 自己随便填应用名称, 选择开发版, 然后进入这个应用, 进入 `设置->应用 keys` 就可以看到你的 appId 和 appKey了.
![](https://cdn.jsdelivr.net/gh/yunwanjia-cloud/blog/hexo/Hexo_blog_build/9.png)
　　将这两个值填入, 就可以使用 Valine 了, 但是如果使用评论的时候报错, 那么可以看[我的这篇文章](https://blog.cloudplayer.site/hexo/problem_in_Valine/), 解决了 Valine 报错的问题.

## cnzz统计

　　进入[友盟官网](https://web.umeng.com)注册一个账号, 然后进入[工作台](https://workbench.umeng.com/home), 点击 `添加Web`, 按照要求填写, 然后会要求在你的网站添加统计代码. 我们一般将这段统计代码添加到网页的页脚.
　　博客页脚布局一般在主题下的 `layout/includes/footer.ejs` 下, 在最后添加你选择的代码. 当然, 页脚布局有可能是 `layout/includes/footer.pug` (比如说 Butterfly 主题就是这样) , 那么又稍有不同.
　　比如其中一个代码是

```html
<script type="text/javascript" src="https://s4.cnzz.com/z_stat.php?id=1278667709&web_id=1278667709"></script>
```

那么要改成

```pug
script(
    type="text/javascript"
    src="https://s4.cnzz.com/z_stat.php?id=1278667709&web_id=1278667709"
    )
```

再比如

```html
<script type="text/javascript">document.write(unescape("%3Cspan id='cnzz_stat_icon_1278667709'%3E%3C/span%3E%3Cscript src='https://s4.cnzz.com/z_stat.php%3Fid%3D1278667709' type='text/javascript'%3E%3C/script%3E"));</script>
```

要改成

```pug
script(type="text/javascript") document.write(unescape("%3Cspan id='cnzz_stat_icon_1278667709'%3E%3C/span%3E%3Cscript src='https://s4.cnzz.com/z_stat.php%3Fid%3D1278667709' type='text/javascript'%3E%3C/script%3E"));
```

(注意 `document.write` 前面有一个空格)
　　那么到底要怎么改呢, 聪明的同学可能已经找出了规律, 即 `script()` 括号里的内容其实是每一个代码开头的 `<script>` 标签里的内容, 然后 `script()` 后的内容 (注意要隔一个空格) 就是被两对尖括号包起来的内容, 比如

```html
document.write(unescape("%3Cspan id='cnzz_stat_icon_1278667709'%3E%3C/span%3E%3Cscript src='https://s4.cnzz.com/z_stat.php%3Fid%3D1278667709' type='text/javascript'%3E%3C/script%3E"));
```

当然如果里面没有内容就空着.
　　根据这个规律, 我们可以得出其他代码的写法
　　再再比如

```html
<script type="text/javascript">document.write(unescape("%3Cspan id='cnzz_stat_icon_1278667709'%3E%3C/span%3E%3Cscript src='https://s4.cnzz.com/z_stat.php%3Fid%3D1278667709%26show%3Dpic' type='text/javascript'%3E%3C/script%3E"));</script>
```

应该改成

```pug
script(type="text/javascript") document.write(unescape("%3Cspan id='cnzz_stat_icon_1278667709'%3E%3C/span%3E%3Cscript src='https://s4.cnzz.com/z_stat.php%3Fid%3D1278667709%26show%3Dpic' type='text/javascript'%3E%3C/script%3E"));
```

　　以上其实是 [pug](https://pugjs.org/) 语言的语法, pug 是一个 HTML 模板工具, 想更多的了解 pug, 建议查看[官方文档](https://pugjs.org/zh-cn/api/getting-started.html).

## 让博客支持脑图 (思维导图)

 ```shell
npm install hexo-simple-mindmap
 ```

　　然后只要在 markdown 文件中按照下面的语法就能写出脑图啦~

```markdown
{% pullquote mindmap mindmap-md %}
- demo
  - 这是一个分支
  - 这是另一个分支
    - 分支的分支哦
    - 分支的另一个分支哦
  - 没有分支的分支
  - 没有分支的另一个分支
{% endpullquote %}
```

{% pullquote mindmap mindmap-md %}
- demo
  - 这是一个分支
  - 这是另一个分支
    - 分支的分支哦
    - 分支的另一个分支哦
  - 没有分支的分支
  - 没有分支的另一个分支
{% endpullquote %}

# 加速博客

　　Github Pages 的服务器在国外, 所以速度其实并不咋地, 所以这里给出优化方案.

## [CloudFlare](https://www.cloudflare.com) 加速

　　CloudFlare 是一家国外的 CDN 加速服务商. 事实上, 我并不推荐 CloudFlare 对你的博客进行 CDN 加速, 因为 CloudFlare 在国内并没有多少节点, 还很不稳定, 而且挂了 CF 后速度似乎还更慢了些, 所以这里不详细讲解, 想用的自己去了解吧.

## [Jsdelivr](https://www.jsdelivr.com/) 加速

　　绝对要推荐这个, 加速利器, **你不需要注册, 甚至连登陆它的网站都不用, 就可以免费使用 Jsdelivr 加速, 简直业界良心啊有木有.** Jsdelivr 可以加速 Github 上的静态文件, 很多主题都有配置, 我们这里介绍如何通过 Jsdelivr 引用 Github 资源.
　　比如你的 Github 用户名为 `yunwanjia-cloud`, 你有一个仓库叫 `CDN` (当然叫别的名字也行, 比如 `abc`, `bcd` 啥的), 仓库里有一个文件夹, 名字叫 `img`, 然后里面有个图片名字叫 `abc.jpg`, 那么通过 https://raw.githubusercontent.com/yunwanjia-cloud/CDN/master/img/abc.jpg 这个 url 来引用这个图片, 这是通过 Github 来引用. 但是同样的, 你可以通过 Jsdelivr 来引用这个资源, 格式是: https://cdn.jsdelivr.net/gh/user/repo@version/file , 中间那个 @version 是仓库版本, 我们一般用不上它, 可以不管它. 那么用 Jsdelivr 来引用这个资源就是 https://cdn.jsdelivr.net/gh/yunwanjia-cloud/CDN/img/abc.jpg . 用法很简单, 效果很强大. 可以简单对比一下两个的加载速度就知道加速有多么显著
[https://raw.githubusercontent.com/yunwanjia-cloud/yunwanjia-cloud.github.io/master/img/banner/0.jpg](https://raw.githubusercontent.com/yunwanjia-cloud/yunwanjia-cloud.github.io/master/img/banner/0.jpg)
这是 Gighub
[https://cdn.jsdelivr.net/gh/yunwanjia-cloud/yunwanjia-cloud.github.io/img/banner/0.jpg](https://cdn.jsdelivr.net/gh/yunwanjia-cloud/yunwanjia-cloud.github.io/img/banner/0.jpg)
这是 Jsdelivr

## 图床

　　相信很多人都有使用图床的经历, 在文章中直接引用外链也能显著的加速, 但是上面已经介绍了 Jsdelivr 加速了, 所有图片都可以通过 Jsdelivr 加速, 已经没有使用图床的必要了. 但是还是有人想用图床, 那么这里介绍一种发生, 搭建自己的图床. 利用的原理还是 Jsdelivr 加速, 即将 Github 当成图床, 然后通过 Jsdelivr 引用. 这里利用了一个方便的工具 [Picgo](), 它可以方便的上传图片到 Github (但是经常出错, ~~非常玄学, 时灵时不灵~~, 经过本人测试, 只有 2.0.4 这个版本勉强能用, 但还是经常出错, ~~反正就是玄学~~).

## 网页预加载脚本 instant.page

　　这个脚本可以实现页面的预加载, 将用户想要访问的页面缓存下来, 需要时直接从缓存读取. 

* **Butterfly 自带该脚本, 因此如果使用 Butterfly 主题可以不用配置.**

### 特性

* 在用户点击网站链接之前, 他们将鼠标悬停在该链接上. 当用户徘徊 65 毫秒时, 他们将点击该链接有两个机会, 因此 instant.page 此时开始预加载, 平均超过 300 毫秒, 以便页面预加载.
* instant.page 是渐进式增强 - 对不支持它的浏览器没有影响.
* instant.page 对站内访问速度的提升的确很给力。然而它只会预加载自己的站内链接，而不会预加载其他外链。

### 使用方法

　　将这段代码放到主题目录下的 `layout/includes/layout.ejs` 文件中的 `</body>` 标签前就可以了.

```html
<script src="https://cdn.jsdelivr.net/gh/yunwanjia-cloud/yunwanjia-cloud.github.io/js/instant_page.js" type="module"></ script>
```

　　当然, 同样也有 `layout/includes/layout.pug` 的情况 (同样比如 Butterfly), 那么可以将以下代码放到 `head` 前

```pug
script(
  src="https://cdn.jsdelivr.net/gh/yunwanjia-cloud/yunwanjia-cloud.github.io/js/instant_page.js"
  type="module"
  )
```

![](https://cdn.jsdelivr.net/gh/yunwanjia-cloud/blog/hexo/Hexo_blog_build/10.png)

# Butterfly 主题升级

 　　 进入到 Butterfly 主题目录, 然后执行命令

```shell
git pull
```

事实上, 只要你改过 _config.yml , 那么肯定是会报错的, 所以要将本地的所有修改先暂时存储起来:

```shell
git stash
```

然后再

```shell
git pull
```

最后还原暂时存储的内容

```shell
git stash pop
```

这时, 就需要你去修改一些冲突的地方了, 冲突的地方挺好找的, 观察一下就发现规律了. 可以执行 `hexo g` 然后查看报错的地方, 一般来说报错的地方就是和更新内容有冲突的地方, 需要自己一个个去改.

# Butterfly 主题魔改

　　记录下我对 Butterfly 主题的魔改, 一方面可供参考, 另一方面可以记录下自己的修改方便查找.

## 随机 banner

　　Butterfly 主题的 banner 大图一个页面是只有一张的, 并且主题配置里也没有多张的设置, 因此如果你想要实现 banner 能够随机显示, 那么就需要魔改主题.

### 2.1.0

　　在 `Butterfly/layout/includes/nav.pug` 文件中添加以下内容

```pug
script document.getElementById("nav").style = 'background-image: url("https://cdn.jsdelivr.net/gh/yunwanjia-cloud/yunwanjia-cloud.github.io/img/banner/' + Math.round(Math.random()*8) + '.jpg"); background-attachment: fixed;'
```

在以上的代码中需要将 `yunwanjia-cloud` 换成你自己的 github 用户名 (如果你是部署在 github 上的话). 其原理就是利用 js 生成 0-8 的随机数, 然后修改 banner 图.

　　当然仅仅加这段代码是没有用的, 还要在 `Butterfly/source/img/banner/` 下 (没有文件夹就自己创建) 放你自己想用的 banner 大图, 名字限定在 [0-8].jpg. 如果要增加 banner 图片的话名字就继续递增, 同时上面的代码中的 `8` 改成你的 banner 图数量减 1 . 当然如果数量不足 9 张, 那么同样也要改成你的 banner 图数量减 1 .

　　这段代码还会把文章的 banner 也变为随机 banner 而不是 cover, 于是如果想要文章的 banner 还是原来的图的话, 那就再加一个条件判断.

```markdown
if !is_post()
  script document.getElementById("nav").style = 'background-image: url("https://cdn.jsdelivr.net/gh/yunwanjia-cloud/yunwanjia-cloud.github.io/img/banner/' + Math.round(Math.random()*8) + '.jpg"); background-attachment: fixed;'
```

### 2.2.5

　　升级到 2.2.5 版本后, 发现原来的随机 banner 效果居然失效了! 然后查看源码才发现 `nav.png` 这个文件似乎被作者抛弃了, 将 banner 图的功能放在了 `Butterfly/layout/includes/header/index.pug` 里. 因此只要把以上代码放进这个文件里就行了, 代码的说明和上面是一样的, 至于 `nav.pug` 里的内容改不改都一样的.

---

暂时就这么多, 以后可能还会补充.