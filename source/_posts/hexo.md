---
title: Hexo 搭建github博客 
date: 2017-09-02 22:58:52
tags: [hexo,github] 
categories: 搭建
---

*Hexo官网 https://hexo.io/*

## 创建github网站账号

### 先创建一个仓库
![image](/assets/hexo_images/4.png)

## 安装git,Node.js

## 使用git Bash程序

输入：npm install -g hexo-cli

安装hexo
![image](/assets/hexo_images/1.png)

输入:npm install hexo-deployer-git --save

安装hexo-deployer
![image](/assets/hexo_images/2.png)

## 创建hexo

### 先创建放Hexo的目录

### 到该目录
（PS：如果需要删除目录，使用
rm -rf h:/MyHexo，clear 清屏）

### 创建Hexo


```
mkdir h:/MyHexo
cd h:/MyHexo
hexo init
```

![image](/assets/hexo_images/3.png)

## 目录下_config.yml 配置文件修改
H:/MyHexo/_config.yml  

**title: hexo 键值对冒号后面空格隔开
（yaml标记语言语法  #注释）**


```
title: 标题 
subtitle: 子标题
description: 描述
author: 作者
language: 语言（中文简体 zh-Hans）
timezone:
```

```
# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: next （更换主题）
```


```
deploy: 
   type: git
   repo: https://github.com/obelieve/obelieve.-github.io.git
   branch: master
   message: '更新'(git commit的日志信息，可不填)
```
## 修改Hexo主题
### 查看主题,(官网上有Themes选项可以浏览下)
目录 H:\MyHexo\themes下，可以看到默认主题landscape

### 从github上，clone 主题

这里选择Next主题

cd h:/MyHexo 目录下执行

```
git clone https://github.com/iissnan/hexo-theme-next themes/next
```
### 修改主题 _config.yml配置文件


```
# Set default keywords (Use a comma to separate)
主要作用是告诉搜索引擎，这个网站内容是什么。
keywords: "obelieve,java blog"
```

```
#导航菜单
menu:
  home: /
  #分类
  categories: /categories/
  about: /about/
  #归档
  archives: /archives/
  #标签
  tags: /tags 
  #sitemap: /sitemap.xml
  #commonweal: /404/
```

```
#菜单图标设置
menu_icons:
  enable: true
  #KeyMapsToMenuItemKey: NameOfTheIconFromFontAwesome
  home: home
  about: user
  categories: th
  schedule: calendar
  tags: tags
  archives: archive
  sitemap: sitemap
  commonweal: heartbeat


# ---------------------------------------------------------------
# Scheme Settings
# ---------------------------------------------------------------
#页面布局设置
# Schemes
#scheme: Muse
#scheme: Mist
scheme: Pisces
#scheme: Gemini
```

```
# 头像设置
# Sidebar Avatar
# in theme directory(source/images): /images/avatar.jpg
# in site  directory(source/uploads): /uploads/avatar.jpg
avatar: /assets/images/obelieve.jpg
```


```
#社交模块
social:
  GitHub: https://github.com/obelieve
  新浪微博: http://weibo.com/ihaoxinqing
  #LinkLabel: Link
```

```
#侧边栏设置
sidebar:
  # Sidebar Position, available value: left | right
  #position: left
  position: right 

  # Sidebar Display, available value:
  #  - post    expand on posts automatically. Default.
  #  - always  expand for all pages automatically
  #  - hide    expand only when click on the sidebar toggle icon.
  #  - remove  Totally remove sidebar including sidebar toggle.
  #display: post
  display: always
  #display: hide
  #display: remove

  # Sidebar offset from top menubar in pixels.
  offset: 12
  offset_float: 12

  # Back to top in sidebar
  b2t: false

  # Scroll percent label in b2t button
  scrollpercent: false
  
  # Enable sidebar on narrow view
  onmobile: false
  
  #侧栏在 use motion: false 的情况下不会展示。
  # Motion
  use_motion: false
```

```
#文章摘要限制字数
auto_excerpt:
  enable: true
  length: 150
```

```
#统计文章阅读次数
#需要到leanCloud网站注册账号->创建应用->
#(应用左下角)存储->创建Class->
#(左边最下面按键)设置->应用Key获取
# Show number of visitors to each article.
# You can visit https://leancloud.cn get AppID and AppKey.
leancloud_visitors:
  enable: true
  app_id: <app_id>
  app_key: <app_key>
```
### 创建tags和categories文件夹

H:/MyHexo目录下创建

```
hexo new page tags
hexo new page categories
```

tags/index.md

```
---
title: tags
date: 2017-09-02 13:11:19
type: tags
comments: false
---
```
categories/index.md

```
---
title: categories
date: 2017-09-02 13:11:04
type: categories
comments: false
---
```
## 新建文章

```
#生成文件
#(hexo主目录下)H:\MyHexo\source\_posts\helloWorld.md
hexo new helloWorld
```
helloWorld.md下

```
---
title: HelloWorld
date: 2017-09-02 20:16:58
tags: hexo (标签设置多个:[hexo1,hexo2,hexo3])
categories: hello(分类)
---
内容
```

## 部署到github

### 设置Git的user name和email


```
github账号使用的邮箱

$ git config --global user.name "your_name"
$ git config --global user.email "your_email@example.com"
```


### 配置github的ssh验证登陆

```
ssh-keygen -t rsa -C "your_email@example.com"
```
得到两个文件
id_rsa和id_rsa.pub

使用下面命令拷贝ssh key
```
clip < ~/.ssh/id_rsa.pub
```
直接ctrl+v 粘贴到


```
登陆github账号(点击头像)
-> Settings
-> SSH and GPG keys
-> New SSH key保存
```

### 部署hexo


```
hexo clean  清理之前public文件
hexo g (generate) 生成文件
hexo s (server) 本地查看localhost:4000/
hexo d (deploy) 部署到github
```
## 遇到的问题


```
hexo deploy 异常Fatal: TaskCanceledException encountered. 
可能
1.github ssh没有设置
2.github 暂时无法提交，有延时等一会儿
```













































