+++

title = "使用Hugo和Github Pages搭建博客"
description = ""
author = "adeng"
tags = [
    "github",
    "golang",
    "hugo",
    "devops",
]
date = "2021-03-12"
categories = [
    "DevOps",
]
menu = "main"

+++



本文



## Github Pages







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
$ hugo new site malfurionpd.github.io
cd malfurionpd.github.io



git init



```







## 主题安装

[hugo-book](https://github.com/alex-shpak/hugo-book)



```
git submodule add https://github.com/alex-shpak/hugo-book themes/book
cp -R themes/book/exampleSite/content .

hugo server --minify --theme book
```



## 配置

docs





域名



![image-20210312141034064](https://notebook.qiniu.adenghub.club/image-20210312141034064.png)







## 发布





```
hugo new site malfurionpd.github.io
cd malfurionpd.github.io


echo "# malfurionpd.github.io" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:malfurionpd/adenghub.github.io.git
git push -u origin main






```



## Refs

[GitHub Pages 搭建教程](https://sspai.com/post/54608)