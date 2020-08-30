---
title: HTML 语义化浅入浅出
date: 2020-08-30 16:51:20
tags:
 - HTML
categories: 技术
---

# 前言
语义化这个话题，可以说是伴随 `HTML` 出生就出现的。毕竟对于搜索引擎的爬虫，再花里胡哨的 `CSS` 样式，对你的网页排序也没什么用。本篇文章对 `HTML` 语义化进行稍微系统的回顾和介绍，毕竟这也是作为前端工程师的基本功。

首先抛一个结论，所谓的 `HTML` 语义，就是这些东西的组合：元素 + 属性 + 属性值 (+ 文档结构)

# 全局属性
全局属性，是指所有的标签都可以设置的属性。

## `id` 属性
标示符 (用于引用)，不应依赖其语义处理相应元素。

## `class` 属性
用来描述内容的性质。
> Authors are encouraged to use values that describe the nature of the content

## `title` 属性
- 链接 - 描述目标信息
- 图片 - 版权 / 描述
- 引用 - 来源信息
- 交互元素 - 操作指南
- ...

## `lang` 属性
内容的语言

# 元数据 (metadata)
所谓元数据，我理解是指不需要呈现的页面上的 `HTML` 标签，单对整个页面的展示呈现具有一些特定的功效。

## `head` 元素
一组元数据

## `title` 元素
文档对外的标题
> 窗口标题 / 历史记录 / 搜索结果标题 / ...

## `meta` 元素
- `name` / `http-equiv` / `charset`
- `name` 属性决定种类， `content` 属性表示内容
- 标准名称 (`application-name`, `author`, `description`, `generator`, `keywords`)
- 扩展名称 (`WHATWG` `Wiki` `MetaExtensions`)
  - Baidu: `mobile-agent`, `baiduspider`
  - Twitter: `twitter:card`, `twitter:image`, `twitter:creator:id`
  - Google: `application-url`, `google-site-verification`, `googlebot`
  - 360: `renderer` (未注册)

# 链接 (links)
在 Web 世界中，各个页面之间的跳转是通过链接语义实现的。
链接有两种类型:
- 外部资源链接:指向用来组成当前文档的外部资源，通常由 `UA` 自动处理
- 用来「导航」到其他资源 (可以在 `UA` 中打开, 下载, ...)

具有链接功能的元素有三种：`link`, `a`, `area`

## `link` 元素
- 元数据，用来描述文档本身与其他资源的关系
- 必须包含`rel`及 `href`属性

形如：
``` html
<link rel="author license" href="/about">
```
在`link`元素中， `link` + `rel` + `author`, `link` + `rel` + `license` 都有预定义的语义。

### `link` + `rel`
- `rel="stylesheet" `
  链接到样式表 (外部资源)

- `rel="alternate"`
  链接到当前文档的其他形式 (超链接)

``` html
<link rel="alternate" type="application/rss+xml" title="Matt Mullenweg » Feed" href="http://ma.tt/feed/" />
```
- `rel="alternate stylesheet"`
   链接到可替换的样式表 (外部资源)

- `rel="prev"`, `rel="next"`
   链接到文档的前一篇 / 后一篇 / 前一页 / 后一页 (超链接) 在生成站点目录、归档视图时很有帮助

- `rel="icon"`
  当前文档的 favicon (外部资源)

## a 元素
- 存在 `href` 属性时为超链接
- 缺少 `href` 属性时为链接占位符
``` html
<nav>
  <ul>
    <li><a href="/">Home</a></li>
    <li><a href="/news">News</a></li>
    <li><a>Examples</a></li>
  </ul>
</nav>
```
与`link`元素不同，`a`元素代表的超链接都是显式的。

### `a` + `rel`
- `rel="prev"`, `rel="next"`
链接到文档的前一篇 / 后一篇 / 前一页 / 后一页 (超链接)
- rel="nofollow"
  当前文档的作者并不推荐超链接指向的文档 (超链接标注)

# 区块 (sections)

## `article` 元素
- 独立的文档、页面、应用、站点
- 可以单独发布、重用
- 可以是...
  - 一篇帖子
  - 一篇文章
  - 一则用户评论
  - 一个可交互的 widget
  - ...

## `section` 元素
- 按主题将内容分组，通常会有标题 (heading)
- 并非「语义化的 div」
那么何时建议使用`section`元素呢？
一个简单的评判标准：当你希望这个元素的内容体现在文档的提纲 (outline) 中时，用 `section` 是合适的。

## `nav` 元素
``` html
<nav>
  <ul>
    <li><a href="/">Home</a></li>
    <li><a href="/news">News</a></li>
    <li><a>Examples</a></li>
  </ul>
</nav>
```
可以帮助 `UA` 迅速获得导航内容，例如读屏器可以省去很多渲染直接跳到导航位置。

## `aside` 元素
- 表示与周围内容关系不太密切的内容 (eg. 广告)
- 通常表现为侧边栏内容 (eg. 相关背景内容)、引述内容

## `h1`–`h6` 元素
语义上是等价的，`UA`会渲染为不同的字体大小。

## `header` 元素
- 一组介绍性描述或导航信息 (目录 / 搜索框 / logo / ...)
- 用来描述最近的父级区块
- 通常包含 `h1`–`h6`
- 不影响文档提纲的生成
``` html
<header>
  <p>Welcome to...</p>
  <h1>Voidwars!</h1>
</header>
```

## `footer` 元素
- 代表最近的父级区块内容的页脚
- 作者信息 / 相关文档 / 版权信息
- 不影响文档提纲的生成
``` html
<footer><!-- site footer -->
  <nav>
    <p>
      <a href="/credits.html">Credits</a> —
      <a href="/tos.html">Terms of Service</a> —
      <a href="/index.html">Blog Index</a>
    </p>
  </nav>
  <p>Copyright © 2009 Gordon Freeman</p>
</footer>
```

## `address`元素
代表与最近父级 `article` 或整个文档关联的联系人信息
``` html
<address>
  <a href="../People/Raggett/">Dave Raggett</a>,
  <a href="../People/Arnaud/">Arnaud Le Hors</a>,
  contact persons for the <a href="Activity">W3C HTML Activity</a>
</address>
```

> 未完待续