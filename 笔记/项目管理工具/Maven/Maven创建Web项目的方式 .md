# Maven创建/运行Web项目

##  1>创建Web

### 方式1：Archetype模板创建





### 方式2：不使用模板直接创建

1. **新建Maven项目不使用任何模板**

   <div align="center">
     <img src="../../../resource\projectManager\maven\bg2.png" width = 80% height = 80% />
   </div>

2. **引入web Facets将项目转变为web项目**

    使用空模板创建的目录为：

   <div align="center">
     <img src="../../../resource\projectManager\maven\bg1.png" width = 50% height = 50% />
   </div>

​      配置Web的Facets

<div align="center">
  <img src="../../../resource\projectManager\maven\bg3.png" width = 50% height = 50% />
</div>



指定webapp和web.xml的位置：

<div align="center">
  <img src="../../../resource\projectManager\maven\bg4.png" width = 50% height = 50% />
</div>



3.**将maven中的打包方式改为war包**

<div align="center">
  <img src="../../../resource\projectManager\maven\bg5.png" width = 70% height = 70% />
</div>



4.**部署tomcat/maven package测试**









## 2> 将项目部署到webapp下：

​	idea默认将项目部署到当前工程下，如果想要完成类似eclipse的操作，将项目部署到tomcat的webapp下则只需要修改项目的输出位置即可。

​    参考： https://blog.csdn.net/sinat_34104446/article/details/82896898



