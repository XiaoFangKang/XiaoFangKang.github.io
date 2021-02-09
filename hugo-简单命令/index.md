# hugo 使用方法


## 1. 创建文章
`$ hugo new *.md`
解释：about.md 自动生成到了 content/about.md

## 2. 部署服务
`$ hugo`
解释： 使用 hugo 生成 pages 修改的文件用于显示内容

## 3.使用皮肤
`$ git clone https://hub.fastgit.org/liuzc/leaveit.git`

皮肤的使用说明： https://liuzhichao.com/2018/hugo-theme-leaveit/

## 4. 皮肤使用的一些问题
配置文件中 menu 中的是页面中的标签栏。
```toml
[[menu.main]]
name = "类型"
url = "/categories/"
weight = 2
```
weight 代表标签头的位置 越小越靠前

## 5. 文章编写时的抬头描述
```markdown
---
title: "java 远程调试"
date: "2020-12-07"
tags: ["java","调试"]
categories: ["java调试"]
---
```
title ：文件头
date: 文件创建时间
tags: 标签  -----> 在配置文件中也会使用到
categories: 类型 ---> 在配置文件中也会使用到


***
# 配置文件设置
根目录下的 config.toml 文件是主要的配置文件。

```toml
baseURL = "https://xiaofangkang.gitee.io/blog"
languageCode = "en-us"
title = "小小的交流博客"
theme = "LeaveIt"
```

