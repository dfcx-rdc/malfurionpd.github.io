+++

title = "Jenkins 初探"

description = "Jenkins 初探"

author = "adeng"

tags = [

  "jenkins",

  "devops",

]

date = "2017-01-04"

categories = [

  "Jenkins", "DevOps"

]

image = "WX20211009-091723@2x.png"

mermaid = false

+++



# 缘由
本来尝试DockerFile加DaoCloud搞定持续集成的，发现还是很多地方绕不开，比如Docker镜像构建速度，Play项目构建时依赖解析速度，可视化等等，开始重新考虑Jenkins。

之前对[Jenkins](https://jenkins.io/index.html)印象不好估计是受UI影响了，这次打开官网，Blue Ocean眼前一亮啊，兴致大起。

![Blue Ocean1.png](https://notebook.qiniu.adenghub.club/1240.png)



![Blue Ocean2.png](https://notebook.qiniu.adenghub.club/1240-20211009091302813.png)





# 安装
直接docker走起。

```
docker pull jenkins
```

这里Mac用户推荐用Docker官网的dmg安装，配合[DaoCloud的加速器](http://guide.daocloud.io/dcs/daocloud-9153151.html#docker-toolbox)，镜像下载速度飞起。

#运行
```
docker run -d -p 49001:8080 -v /Users/xxx/Documents/Docker/Volume/Jenkins:/var/jenkins_home -t jenkins
```

启动后访问 http://localhost:49001/ 会要求输入secrets token。

![Secrets.png](https://notebook.qiniu.adenghub.club/1240-20211009091337344.png)




可以在本地Volume里找到，也可以进入镜像查看。

```
docker exec -it 4b7112ec2f2c /bin/sh

cat /var/jenkins_home/secrets/initialAdminPassword
```

输入后，开始初始化，安装默认Plugins。

![Plugins.png](https://notebook.qiniu.adenghub.club/1240-20211009091414913.png)



然后添加一个Admin账号，就进入控制台了。

![Console.png](https://notebook.qiniu.adenghub.club/1240-20211009091438020.png)

