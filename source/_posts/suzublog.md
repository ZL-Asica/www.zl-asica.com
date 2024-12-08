---
title: SuzuBlog 介绍
date: 2024-12-08 00:00:00
tags:
  - frontend
categories:
  - 随想
---

## SuzuBlog 是什么？

可以发现我的 [ZLA小站](https://www.zla.pub) 从之前的 WordPress 改成了现在全新的样式，这个全新的样式就是 SuzuBlog。

SuzuBlog 是一个由我自己个人从 0 开发的基于 Next.js 的博客系统，它的名字来源于日语中的铃铛 Suzu。代表着清脆的声音，也代表着我对这个博客系统的期望。

## 为什么要开发 SuzuBlog？

之前使用的 WordPress 是基于 PHP+MySQL 的，是在几年前基本上每个人都会选择的博客系统。但是随着时间的推移，我发现 WordPress 的一些问题：

1. **性能问题**：太慢，太慢，而且我也不是很擅长优化 WordPress 的性能。
2. **安全问题**：MySQL 数据库的安全问题，WordPress 的安全问题，插件的安全问题。
3. **不够灵活**：主题和插件虽然很多，但是我总是找不到一个满足我需求的主题。
4. **不够简洁**：后台管理界面太复杂，我只是想写一篇文章，为什么要让我看到那么多东西？
5. **不够现代**：前端界面虽然可以通过主题定制，但是总是感觉不够现代。（比如我之前所使用的 Sakura 主题，感觉有非常多人在用，但主题本身已经没有在继续更新和维护了）

还有一点，WordPress 并非为 Serverless 环境设计，也就意味着你需要一台自己的运行了 LNMP 环境的服务器，并且需要自己去维护这个服务器。我在 15 年的时候维护的 AIFans 站点，也是采用的 WordPress，数据库确实是被人攻破过，这并不是一个好的体验。

## SuzuBlog 的特点

我不是很想在这篇文章中长篇大论的介绍 SuzuBlog 的特点，如果你对此很感兴趣，可以查看我特地为 SuzuBlog 编写的文档站点 [SuzuBlog Docs](https://suzu.zla.app)，或者直接查看 SuzuBlog 的 GitHub 仓库 [SuzuBlog](https://github.com/ZL-Asica/SuzuBlog)。我在文档站点中非常详细的介绍了如何上手和如何使用 SuzuBlog，同样的你若是对我的实现感兴趣，也可以直接查看源码。

简单来说，SuzuBlog 是基于 Next.js 的博客系统。文章可以使用纯 Markdown 编写（这也是为了我自己可以一篇文章同时在多个平台一起发布的原因），同样的 SEO 优化也是我进行了特定优化的一个部分，实现了完整的 robots.txt、sitemap.xml、manifest.json、LD-JSON 等等。会根据文章内容去动态生成对应的 SEO 信息。同样的，我也构建了自动的 RSS 生成器，可以让你的文章在发布的同时自动生成 RSS。

作为一个博客系统，而非一个主题/CMS，为了更好的用户体验和自定义，我借鉴了 Hexo 中的 `config.yml` 的方法，将个性化配置选项放置在了这里面，让用户可以轻松自定义去配置自己的博客系统。

## 选择 SuzuBlog 的原因

我觉得易上手是一个非常重要的特点

1. 点击 `Use this template` 按钮，就可以直接创建一个属于你自己的仓库。
2. 更改 `config.yml` 中的配置。
3. 然后将你的文章放置在 `posts` 文件夹中。
4. 最后只需要新建一个 `vercel` 账户，把 `GitHub` 仓库绑定上去，就可以直接自动部署了。

就是这么简单，仅需4步，全程可能用不了 10 分钟。无需配置服务器、无需配置数据库、无需安装 `nodejs`，只需要一个 `GitHub` 和一个 `Vercel` 账户，就可以实现一个现代化、高性能、高安全性的博客搭建。

## 结语

SuzuBlog 是我为了解决自己的问题而开发的一个博客系统，我希望它能够帮助到更多的人。如果你对 SuzuBlog 有任何问题或者建议，欢迎在 [GitHub Issues](https://github.com/ZL-Asica/SuzuBlog/issues) 中提出，我会尽快回复。
