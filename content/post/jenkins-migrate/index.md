+++

title = "Jenkins Job迁移"

description = "Jenkins Job迁移"

author = "adeng"

tags = [

  "jenkins",

  "devops",

]

date = "2021-04-21"

categories = [

  "Jenkins", "DevOps"

]

image = "WX20211009-091723@2x.png"

mermaid = false

+++



# 手工方式

参考 [Jenkins迁移job](https://www.jianshu.com/p/76465d12171c) 主要是Jobs文件夹的拷贝，需要注意版本差异不要太大



# 插件方式

### 安装插件

搜索 [Job Import](https://plugins.jenkins.io/job-import-plugin/#documentation) 插件进行安装

### 配置远程服务

在系统配置 => Job Import Plugin 配置 remote jenkins

![image-20211009115415407](https://notebook.qiniu.adenghub.club/image-20211009115415407.png)

### 导入

点击 Job Import Plugin后选择之前配置的远程jenkins，点击query

![image-20211009115811750](https://notebook.qiniu.adenghub.club/image-20211009115811750.png)

选择需要导入的Job导入即可，还可勾选是否安装依赖的插件

![image-20211009120201514](https://notebook.qiniu.adenghub.club/image-20211009120201514.png)





# Jenkins CLI方式

`Jenkins CLI ` 方式可以将job导出为xml格式，然后在目的jenkins导入即可。

Configure => Show API Token 配置一个token，用于导出认证使用。

![image-20211009140114317](https://notebook.qiniu.adenghub.club/image-20211009140114317.png)

相关命令如下：

```
//导出
java -jar jenkins-cli.jar -s http://127.0.0.1:8080/jenkins -auth admin:11xxxxxxxxxxxxxx get-job "test-job" > test-job.xml

//导入 需要新配置API Token
java -jar jenkins-cli.jar -s http://127.0.0.1:8080/jenkins -auth admin:22xxxxxxxxxxxxxx create-job test-job <  test-job.xml
```



# 遇到问题

## Unable to read /usr/xxx/xxx/config.xml

导入时某2个job报错，最后发现是由于目的jenkins未装maven插件导致（导入时已经勾选了安装依赖插件），手动安装后再导入就ok了。

