---
layout: post
title:  "使用 jekyll & github 创建博客"
categories: 个人随笔
tags: jekyll
author: ZhangWei
---

* content
{:toc}

> Hello, 这是第一篇博文：论如何copy别人的blog

## 一、抄袭别人的作文

找到这个前端小哥的repo，fork之 https://github.com/Gaohaoyang/gaohaoyang.github.io

好了，您的repo下有 gaohaoyang.github.io 这个库了

只需要rename成 yourname.github.io 就可以在 http://yourname.github.io 访问了

## 二、掩盖抄袭痕迹

调整您的页面，随便找两个jekyll的blog看看就知道怎么做了

我在原文的基础上，修改了一些描述性文字，并做了顶部导航的中文化，也删除了一些我不需要的页面

可以在本地安装环境，在本地调试后再push，github更新很慢很慢

```shell
# 配置环境
zhangwei@zw:potaski.github.io$ gem install jekyll bundler
# 启动本地服务
zhangwei@zw:potaski.github.io$ jekyll build; jekyll server
 ...
 Auto-regeneration: enabled for '/mnt/d/zhangwei/potaski.github.io'
    Server address: http://127.0.0.1:4000/
  Server running... press ctrl-c to stop
```

## 三、最后感谢 Gaohaoyang

页脚已按您的要求留下designed作者信息，如果仍有其它不妥之处，请随时与我联系