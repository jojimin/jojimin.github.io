---
title: 为主题安装scss插件时的一个小插曲
date: 2019-10-20 15:28:11
tags: [hexo, nodejs]
---

在配置snark主题时<https://github.com/Litreily/hexo-theme-snark>，需要安装两个渲染插件:

```shell
npm install hexo-renderer-pug --save
npm install hexo-renderer-sass --save
```

<!--more-->

前者为模板渲染引擎，后者为css的预处理器。

经过简单的安装配置，本地验证无误后便把更新提交上了git，等待travis-ci的部署。却不料，线上的站点没有任何样式，于是到travis页面上查看发现如下错误日志：

{% asset_img sass1.JPG sass错误日志 %}

简单说，就是找不到travis上linux虚拟机系统对应版本的binding文件，只有我本地windows系统的。css处理器出了问题，自然就没有样式了。

但是，我的本地环境通过npm是无法获取到linux版本的文件的。于是，偷懒了一下，去scss的git发布页<https://github.com/sass/node-sass/releases>上找到linux-x64-72版本的binding文件，按照日志中指定路径放了进去，再提交，便成功渲染了css样式。