---
title: "Hugo | 静态博客搭建有感"
date: 2021-11-06T15:22:10+08:00
draft: false
tags:
  - Hugo
categories:
  - 建站笔记
hidetoc: false
---
## 一些碎碎念

搭建自己的静态博客这件事，对我本人来说还没有什么真实感。不过既然都已经为了建站捣鼓了域名和服务器，那多一个blog（个人网站）也是完全可以预料到的事，更何况不是部署在服务器内的动态博客，而是只需要一台普通电脑就能搞定的静态博客。

不过本鸽王之前打算用友邻搭建的pleroma实例写blog，理由是支持我最爱的BBCode，当然还有markdown和HTML。缺点是没有主页推荐和搜索功能，全靠我置顶嘟文那现实吗！后来我发现了Writefreely，凭借着简单的二进制文件安装方式和简约的白纸黑字视觉体验，我火速在服务器里搭建了个站，结果悲剧地发现——这货不支持BBCode，但胜在太简单了，简单到无需docker安装，于是被我压箱底了（。

后来？其实当时只是想做一个静态网页的，连主题都不需要的居中显示的网页，但是Google一下发现好多用的都是wordpress动态博客（连在自己博客里加喜欢的脚本都要付费吗魂淡），又或是装好多依赖的静态博客。作为一个常年躺平人士这显然不合适（喂），于是我终于找到了不完全依赖本地又能轻松修改配置的博客搭建方式：Hugo静态网页渲染+Vercel网页托管自动部署+Github代码托管，主题截止目前敲定了[MemE](https://github.com/reuixiy/hugo-theme-meme)，可能以后会改，毕竟我连css全称是什么都不知道XDD...

嘛，总而言之我blog就是这样在机缘巧合之下诞生了，难道不值得おめでとう一下吗！

## 这次不会也压箱底吧

大概...不会的，不过我在冰水混合物的[这篇博客](https://binghuohunhewu.com/2020/03/02/personalblog/)里发现了[Typecho](https://typecho.org/)，如果有机会的话我可能要尝试一下用这个搭建动态博客，到时候可能会选择性拆迁一个博客。所以...结果谁知道呢。

[Writefreely](https://zone.tantalum.life/Roelxy)那边我用来发长毛象运维教程了，这边的话目测会发更多奇奇怪怪的东西（？）反正也不会有人看，千万不要期待就没问题了！

## 特别鸣谢

皮塔丘（ [@Hydrangea@o3o.ca](https://o3o.ca/@Hydrangea)）的[Hugo简明搭建笔记](https://mantyke.icu/2021/hugo-build-blog)