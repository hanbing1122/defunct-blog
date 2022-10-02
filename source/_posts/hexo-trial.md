---
title: Hexo 踩坑小记
date: 2022-10-01 22:00:00
tags: logs
---
## Intro
距离上一次用 Hexo 写博客已经过去四年。  
参考 [用Hexo搭建个人部落格](https://yogapan.github.io/2017/08/11/%E7%94%A8Hexo-Github-Pages%E6%90%AD%E5%BB%BA%E5%80%8B%E4%BA%BA%E9%83%A8%E8%90%BD%E6%A0%BC/) 教程搭建，在此记录踩坑过程。
<!--more-->
## 安装 Hexo  
macOS 下使用 `npm / yarn` 安装 Hexo  
```
$ brew install yarn
$ yarn global add hexo
```
创建博客
```
$ mkdir defunct-blog
$ hexo init defunct-blog
```
## 更换主题
### NexT 安装
本博客使用了 [theme-next/hexo-theme-next](https://github.com/theme-next/hexo-theme-next) 主题  

***
注意不要根据官方文档使用 git clone 方式安装！！！  
会引起 submodule 问题导致远程仓库无法同步主题  
Download ZIP 复制到 themes 文件夹即可
***

安装主题后修改 _config.yml 
```
post_asset_folder: true #自动生成素材文件夹
theme: next
```
### 设置 Scheme 并关闭无用动画
```
scheme: Pisces
motion:
  enable: false
```
启动 server 查看效果
```
$ hexo server
```
## 关于作者
### 头像
新建一个文件夹用于存放 avatar
```
$ mkdir source/uploads
```
把头像放入文件夹，在 themes/next/_config.yml 中设置头像路径
```
avatar: /uploads/avatar.jpg
```
### 作者
在网站设定 _config.yml 中设置名字、标题、副标题
```
title: <标题>
subtitle: <副标题>
description: <描述>
author: <名字>
```
### 社交网络链接
修改主题设定 themes/next/_config.yml
```
social:
  GitHub: https://github.com/xxx
  Twitter: https://twitter.com/xxx
```
### About me page
创建 about page
```
$ hexo new page "about"
```
去除 themes/next/_config.yml 中 about 的注释
```
menu:
  home: /
  archives: /archives
  tags: /tags
  about: /about
```
## 文章分类
新建一个名为 "tags" 的页面
```
$ hexo new page "tags"
```
编辑 source/_posts/tags/index.md，将 type 设成 tags
```
---
title: tags
date: 2022-10-01 00:00:00
type: "tags"
---
```
此后在文章中添加 tags 就可以自动分类了。
## 首页文章预览
在需要切断的两部分之间添加
```
<!--more-->
```
## 部署
使用 CloudFlare Pages 进行部署，绑定自定义域名更加便捷。  
也顺便可以利用上 CloudFlare 的全球网络。
### GitHub 配置
建立仓库后
```
$ cd my-hexo-site
$ git init
$ git remote add origin https://github.com/xxx/xxxrepo
$ git branch -M main
$ git add --all
$ git push -u origin main
```
### CloudFlare Pages 配置
参见 [Cloudflare Docs](https://developers.cloudflare.com/pages/framework-guides/deploy-a-hexo-site/)

CloudFlare Pages 将会在 GitHub 仓库更新后自动构建页面。
## 指令备忘录
```
$ hexo init
$ hexo new post <title>
$ hexo new page tags
$ hexo server -p 8000 --debug
```
删除文章只需删除对应 Markdown 文件和文件夹即可。

## Markdown 快速入门
推荐教程 [Markdown Tutorial](https://www.markdowntutorial.com/)
```
** 粗体
_ 斜体
# 标题

链接 [search for it](www.google.com)

带引用的链接 [description][reference]
[reference]: “reference links”

图片 ![description](image links)
带引用的图片（用法同上） ![description][reference]

引用块 >

无序列表
* flour
* cheese
* tomatoes

有序列表
1. cut the cheese
2. slice the tomatoes
3. rub the tomatoes in flour

子列表（缩进）
* Calculus
    * A professor, 
    * Has no hair
    * Often wears green
* Castafiore
    * An opera singer
    * Has white hair
    * Is possibly mentally unwell

在行末写两个空格可以在两行间添加一个空行

``` 代码块
```