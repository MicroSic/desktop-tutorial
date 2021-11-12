---
title: "Hugo | 记录MemE主题美化过程"
date: 2021-11-11T17:20:38+08:00
draft: false
enabletoc: true
tags:
  - Hugo
categories:
  - 建站笔记
---

## MemE

目前我的博客采用[MemE主题](https://github.com/reuixiy/hugo-theme-meme)，这款主题由[reuixiy](https://io-oi.me/tech/documentation-of-hugo-theme-meme/)制作，设计理念是轻量、极简主义，但不简陋，同时也对高度自定义非常友好，甚至还提供了简繁体中文的配置文档，也就是`config.toml`，以下是开发者reuixiy对MemE主题的介绍：

>MemE 是一个强大且可高度定制的 GoHugo 博客主题，专为个人博客设计。MemE 主题专注于优雅、简约、现代，以及代码的正确性。MemE 主题对习惯了 Hexo 的用户非常友好，是从 Hexo 迁移到 Hugo 的不错选择。

>为什么要起名为 MemE 呢？这四个字母的含义是基于这个单词本身的，即希望你的博客以及文章能够像模因一样传播、影响。当然，希望这个主题也是如此，并给你带来欢乐。至于这四个字母的形式（MemE），则是受 Taylor Swift 的 ME! 中的「you can’t spell “awesome” without “me”」启发。同时，这两个字母的大写就将这个单词分成了两部分——ME 和 em，中间两个字母组成 em，这也给人一种可爱的感觉。此外，em 也是 me 的反写，这又是我非常喜欢的形式！

>MemE 主题践行极简主义，没有使用现有的流行前端库，主题的 HTML 和 CSS 皆由我纯手工从零雕琢而成。同时，MemE 的 CSS 也是按需生成的，比如：如果你不需要代码高亮的功能，那么代码高亮的样式就不会被加入 MemE 的 CSS 文件中。更甚，MemE 无需加载任何图标库——主题的图标是通过 Hugo 的数据模板直接将 SVG 嵌入到 HTML 中实现的——这使得 MemE 不会去加载图标库中大量你所不需要的图标，节约了很多资源。当然，这也意味着你可以方便地自定义属于自己的图标。

不过我自己也是小白哈哈哈，所以也参考了很多大佬的配置。在这篇文章的最后我列出了我参考的资料。感谢各位，万物皆互联。

## 基础部分
### 目录
在`config.toml`中将`enableTOC`设为true，然后在文章的 Front-Matters 加上`toc: true`即可。
需要注意的是目录只能显示二级以下的标题。如果需要显示一级标题，可以将`startLevel`修改为 1（默认2）。
>不过，并不建议在文章内用一级标题，因为一级标题为文章标题。所以，文章内还是建议以二级标题开始，这更符合逻辑，也更有利于[SEO(search engine optimization)](https://developer.mozilla.org/zh-CN/docs/Glossary/%E8%AF%AD%E4%B9%89#HTML_%E4%B8%AD%E7%9A%84%E8%AF%AD%E4%B9%89)。

关于目录的位置，请看[这里](https://github.com/reuixiy/hugo-theme-meme/issues/64)

### 网络字体
请看[这篇博客](https://ztygcs.github.io/posts/meme%E4%B8%BB%E9%A2%98%E4%BC%98%E5%8C%96%E4%BA%8C/#%E7%BD%91%E7%BB%9C%E5%AD%97%E4%BD%93%E9%93%BE%E6%8E%A5)

## 进阶部分
### 页脚添加今日诗词
参考：https://guanqr.com/tech/website/add-jinrishici-in-meme/
在 MemE 主题的自定义页脚文件中添加以下代码即可：
```
<!-- 文件位置：~/layouts/partials/custom/footer.html -->

<script src="https://sdk.jinrishici.com/v2/browser/jinrishici.js" charset="utf-8"></script>
<text class="poem_sentence"></text>
<text class="poem_info"></text>
<script type="text/javascript">
  jinrishici.load(function(result) {
    var sentence = document.querySelector(".poem_sentence")
    var info = document.querySelector(".poem_info")
    sentence.innerHTML = result.data.content
    info.innerHTML = '——' + result.data.origin.author
  });
</script>
```
这里我出现了一个问题，因为设置了诗句和作者之间用破折号「——」连接，而我按照教程在`~/layouts/partials/custom/footer.html`中添加了代码后发现破折号显示乱码，而且生成的诗句被放在了最下方，而我希望诗句处在作者和版权之间，所以我在`~/layouts/partials/footer.html`的适当位置添加代码。
>需要注意我直接修改了meme主题的页脚文件而不是主题的自定义页脚文件，只适用于手动安装主题，如果是 git submodule 方式安装主题则不要直接修改主题页脚文件，否则不利于主题后续更新。

### 加载进度条
参考：https://zhixuan2333.github.io/posts/ac760353/#加载进度条 

```
<!-- layouts/partials/footer/custom.html -->
<script
    src="https://cdn.jsdelivr.net/gh/zhixuan2333/gh-blog@v0.1.0/js/nprogress.min.js"
    integrity="sha384-bHDlAEUFxsRI7JfULv3DTpL2IXbbgn4JHQJibgo5iiXSK6Iu8muwqHANhun74Cqg"
    crossorigin="anonymous"
></script>
<link
    rel="stylesheet"
    href="https://cdn.jsdelivr.net/gh/zhixuan2333/gh-blog@v0.1.0/css/nprogress.css"
    integrity="sha384-KJyhr2syt5+4M9Pz5dipCvTrtvOmLk/olWVdfhAp858UCa64Ia5GFpTN7+G4BWpE"
    crossorigin="anonymous"
/>
<script>
    NProgress.start();
    document.addEventListener("readystatechange", () => {
        if (document.readyState === "interactive") NProgress.inc(0.8);
        if (document.readyState === "complete") NProgress.done();
    });
</script>
```
需要注意stack和meme的页脚文件位置不太一样，meme的在`~/layouts/partials/custom/footer.html`。不过进度条是在页面顶端，所以我选择在`header.html`添加代码。

## 短代码
### 在博客中插入B站视频
参考：https://mogeko.me/posts/zh-cn/079/
虽然我个人相当不喜欢bilibili，但bili在哪都能看，而油管不行。
#### 添加代码
在`layouts/shortcodes`文件夹中创建文件`bilibili.html`(如果没有那个文件夹就自己新建一个)，我选择在博客根目录下建`layouts/shortcodes`文件夹，后续换主题的时候方便管理。然后粘贴如下代码：
```
{{ $videoID := index .Params 0 }}
{{ $pageNum := index .Params 1 | default 1}}

{{ if (findRE "^[bB][vV][0-9a-zA-Z]+$" $videoID) }}
<div><iframe id="biliplayer" src="//player.bilibili.com/player.html?bvid={{ $videoID }}&page={{ $pageNum }}" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true" loading="lazy" > </iframe></div>
{{ else }}
<div><iframe id="biliplayer" src="//player.bilibili.com/player.html?aid={{ $videoID }}&page={{ $pageNum }}" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true" loading="lazy" > </iframe></div>
{{ end }}
```
然后用 CSS 修改播放器的尺寸，最好能根据不同的屏幕大小 (PC 和手机) 动态调整。在`/assets/scss/components/_post-meta.scss`中插入：
```
// 嵌入 BiliBili 视频
#biliplayer {
  width: 100%;
  height: 550px;
}
@media only screen and (min-device-width: 320px) and (max-device-width: 480px) {
  #biliplayer {
    width: 100%;
    height: 250px;
  }
}
```
或者直接在刚刚的`layouts/shortcodes/bilibili.html`中添加：
```
<style>
// 嵌入 BiliBili 视频
#biliplayer {
  width: 100%;
  height: 550px;
}
@media only screen and (min-device-width: 320px) and (max-device-width: 480px) {
  #biliplayer {
    width: 100%;
    height: 250px;
  }
}
</style>
```
我在这里做了一点改动，第二步css/html的id应该是biliplayer而不是bilibili，如果看不懂的话直接复制我的代码即可。

### 黑幕文字
可以直接参考：https://mogeko.me/posts/zh-cn/080/
### 还有更多...
甩[链接](https://guanqr.com/tech/website/hugo-shortcodes-customization/)，实在肝不动了Orz

## 配置Waline评论
待更新

## 特别鸣谢

- [Hugo 主题 MemE 文档](https://io-oi.me/tech/documentation-of-hugo-theme-meme/)
>MemE主题的官方文档

- [Guan Qirui的个人博客源代码](https://github.com/guanqr/blog/blob/master/config.toml)
>`config.toml`可供参考

- [Guan Qirui的个人博客：荷戟独彷徨](https://guanqr.com/tech/website/)
>建站笔记，包括Waline评论、短代码、今日诗词等

- [天涯共此时的meme主题优化](https://ztygcs.github.io/categories/hugo/)
>`config.toml`解读以及网络字体如何添加

- [Hugo theme stack主题 正确的魔改方式](https://zhixuan2333.github.io/posts/ac760353/)
>stack主题的魔改教程，参考了加载进度条

- [Mogeko's Blog](https://mogeko.me/tags/hugo/)
>参考了短代码配置

