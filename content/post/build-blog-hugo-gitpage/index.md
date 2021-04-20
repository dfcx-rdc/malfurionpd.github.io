+++



title = "使用Hugo和Github Pages搭建博客"
description = "介绍使用Hugo和Github Pages搭建个人博客的方法"
author = "adeng"
tags = [
    "github",
    "golang",
    "hugo",
    "devops",
]
date = "2021-03-12"
categories = [
    "DevOps", "Write"
]

image = "WX20210420-201336@2x.png"



+++

本文即是本站的搭建方式。

目前Github Pages还挺稳定，托管起来也比较省心。



## Github Pages 仓库新建

按照 [Github Pages官网](https://pages.github.com/) 说明，新建一个和github用户名一样的Repo，格式为 `username.github.io`。

![image-20210312135040716](https://notebook.qiniu.adenghub.club/image-20210312135040716.png)



## Hugo 安装

参考 [Hugo官网](https://gohugo.io/getting-started/installing/) 本地安装hugo，笔者Mac使用brew安装:

```
$ brew install hugo
···

$ hugo version
Hugo Static Site Generator v0.80.0/extended darwin/amd64 BuildDate: unknown
```



## Site 初始化

```
## 新建hugo站点
$ hugo new site malfurionpd.github.io
$ cd malfurionpd.github.io

## 初始化git库
$ echo "# malfurionpd.github.io" >> README.md
$ git init
$ git add README.md
$ git commit -m "first commit"
$ git branch -M main
$ git remote add origin git@github.com:malfurionpd/adenghub.github.io.git
$ git push -u origin main
```





## 主题安装

选用 [hugo-theme-stack](https://github.com/CaiJimmy/hugo-theme-stack) 主题，下载主题，复制Example到根目录，跑起来看看效果。

```
git submodule add https://github.com/CaiJimmy/hugo-theme-stack/ themes/hugo-theme-stack
cp -R themes/hugo-theme-stack/exampleSite .

hugo server
```

![image-20210420203228398](https://notebook.qiniu.adenghub.club/image-20210420203228398.png)







## Github Pages配置

做如下图2处配置：

1. 选用根目录下docs文件夹内容为站点目录（这里要配合修改 config.yaml，添加配置项 `publishdir: docs`）
2. 配置自定义域名

![image-20210312141034064](https://notebook.qiniu.adenghub.club/image-20210312141034064.png)



## 写作

```
hugo new post/xxxx-xxx/index.md

hugo server 

hugo
```



## 发布

写个简单脚本，方便发布git就ok了。



## 参考鸣谢

[GitHub Pages 搭建教程](https://sspai.com/post/54608)