+++

title = "Hugo博客中加入百度统计"
description = "Hugo博客中加入百度统计"
author = "adeng"
tags = [
    "mysql"
]
date = "2021-04-16"
categories = [
    "MySQL", "DB"
]
menu = "main"

mermaid = true

+++







注册一个百度账号，登录 [百度统计官网](https://tongji.baidu.com/)



可选的还有 Goolge 和 不蒜子





![image-20210419153047478](https://notebook.qiniu.adenghub.club/image-20210419153047478.png)





![image-20210419152959536](https://notebook.qiniu.adenghub.club/image-20210419152959536.png)







/layouts/partials/head/script.html



```
<script>
var _hmt = _hmt || [];
(function() {
  var hm = document.createElement("script");
  hm.src = "https://hm.baidu.com/hm.js?51a26ee9b826c848e0f3eb1665792cce";
  var s = document.getElementsByTagName("script")[0]; 
  s.parentNode.insertBefore(hm, s);
})();
</script>



```

