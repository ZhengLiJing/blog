---
title: hexo配置学习
date: 2018-06-20 09:17:34
tags: hexo
categories: hexo
---
<img src="http://p8rhahhu3.bkt.clouddn.com/201801/1529460122000.png" width="655"/>
1. 记录hexo的配置过程。
2. 购买服务器digitalcloud。
3. 部署到服务器上。
4. 购买域名。
5. hexo配置。
这一篇主要记录hexo配置的过程。首先是自己遇到的问题，然后是一些普通的配置。

### 遇到的问题
首先遇到的问题是：nex主题只想显示标题和文章部分。
搜索到的一个解决方法是：通过在文章头部加入以下部分。这个方法是要手动加入摘要。
```bash
title: Hexo示例文档
---

本篇为Hexo示例文档.  # 这里是摘要部分,写1~2句话,就实现不全显示博文了..

<!-- more -->


### 下面是正常的 markdown 博客,就可以了.......
```

另一个方法是，在配置文件_config.yml查找到auto_excerpt,意思是自动摘录，通过设置:
```xml
auto_excerpt:
    enable: false
    length
```

遇到另一个问题是给文章添加阅读数量。参考的文章是：《为NexT主题添加文章阅读量统计功能》
报错：Cannot read property 'enable_sync' of undefined
解决：在blog站点下的配置文件_config.yml添加以下代码

```bash
leancloud_counter_security:
  enable_sync: true
  app_id: rjEGiCa******-gzGzoHsz
  app_key: zWE2Bry******8HmPyTpBQa
  username: # Will be asked while deploying if is left blank
  password: # Recommmended to be left blank. Will be asked while deploying if is left blank
```
在next-reloaded主题下的配置文件_config.yml中修改
```
leancloud_visitors:
  enable: true
  app_id: rjEGiCa******-gzGzoHsz
  app_key: zWE2Bry******8HmPyTpBQa
  security: true
  betterPerformance: true
```
添加了百度统计
添加了阅读数量，LeanCloud后台管理阅读数量。
添加评论DISQUS
一开始加载错误，查找后发现需要注册，https://help.disqus.com/installation/whats-a-shortname
注册完后，就正常了。
添加了搜索Algolia
### 主题配置
参考：https://theme-next.iissnan.com/theme-settings.html
### 普通配置项
#### hexo常用命令
`hexo init [floder]`, 初始化一个文件夹为一个站点
`hexo new [layout] <title>`,创建一篇文章，可以配置布局选项，默认使用default_layout的值。如果文章标题有空格，使用双引号括起来。
`hexo generate`,简写为`hexo g`,将markdown文章转换为静态网页。
`hexo server`,简写为`hexo s`,本地启动一个服务。
`hexo deploy`,简写为`hexo d`,部署站点，有一个参数，`hexo d -g`,表示在部署之前先重新生成一下站点。
`hexo clean`,删除缓存文件db.json以及生成的pulic目录，当修改了某些样式或者配置时，发现`hexo g`没有作用时，可以执行该命令来解决。