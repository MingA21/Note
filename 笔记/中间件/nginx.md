# nginx

### 1. 简介

##### 1.1 > 来源

<div align="center">
  <img src="../../resource\middleware\nginx\ng2.png" width = 80% height = 80% />
  <img src="../../resource\middleware\nginx\ng1.png" width = 80% height = 80% />
</div>



​	  为了减轻传统WEB项目中单节点的服务压力，进而采取批量部署的方式(集群)，但是总要有一台服务器来充当门面服务，相较于其他服务器它需要具备更强的并发，并需要根据每台服务器的负载量，按照不同的比例分发请求(负载均衡)，Nginx就是这样一种服务器。



### 2. 下载/安装

##### 2.1 > windows 

1. 下载： http://nginx.org/en/download.html

   <div>
       <img src="../../resource\middleware\nginx\ng3.png" width =90% height = 80%/>
   </div>

   

2. 安装一路next即可

3. 启动测试windows下，启动根目录下nginx.exe即可，默认配置80端口

   <div>
       <img src="../../resource\middleware\nginx\ng4.png" width =70% height = 80%/>
   </div>

##### 2.2> Linux

1. wget下载或者通过ftp工具上传

   **wget http://nginx.org/download/nginx-1.13.7.tar.gz  **  （若无该命令**yum install wget**下载）

   <div>
       <img src="../../resource\middleware\nginx\nng1.png" width =70% height = 80%/>
   </div>

2. 解压  

    **tar -zxvf nginx-1.13.7**

3. 安装编译依赖包

   ```HTML
   yum install gcc
   yum install pcre-devel
   yum install zlib zlib-devel
   yum install openssl openssl-devel
   
   <!--一键安装上面四个依赖-->
   yum -y install gcc zlib zlib-devel pcre-devel openssl openssl-devel
   ```

   > ​	gcc，安装nginx需要先将官网下载的源码进行编译，编译依赖gcc环境，如果没有gcc环境，需要安装
   > 
   > ​	PCRE(Perl Compatible Regular Expressions)是一个Perl库，包括 perl 兼容的正则表达式库。nginx的http模块使用pcre来解析正则表达式，所以需要在linux上安装pcre库。
   > 
   > ​	pcre-devel是使用pcre开发的一个二次开发库。nginx也需要此库。
   > 
   > ​	zlib库提供了很多种压缩和解压缩的方式，nginx使用zlib对http包的内容进行gzip，所以需要在linux上安装zlib库。
   > 
   > ​	OpenSSL 是一个强大的安全套接字层密码库，囊括主要的密码算法、常用的密钥和证书封装管理功能及SSL协议，并提供丰富的应用程序供测试或其它目的使用。nginx不仅支持http协议，还支持https（即在ssl协议上传输http），所以需要在linux安装openssl库。
   
4. 编译配置准备**在 var下创建temp/nginx文件夹，用于nginx运行临时目录**

5. 执行编译配置命令

   ```java
   ./configure \
   --prefix=/usr/local/nginx \
   --pid-path=/var/run/nginx/nginx.pid \
   --lock-path=/var/lock/nginx.lock \
   --error-log-path=/var/log/nginx/error.log \
   --http-log-path=/var/log/nginx/access.log \
   --with-http_gzip_static_module \
   --http-client-body-temp-path=/var/temp/nginx/client \
   --http-proxy-temp-path=/var/temp/nginx/proxy \
   --http-fastcgi-temp-path=/var/temp/nginx/fastcgi \
   --http-uwsgi-temp-path=/var/temp/nginx/uwsgi \
   --http-scgi-temp-path=/var/temp/nginx/scgi
   ```

   Prefix表示nginx的安装位置其他都是一些日志，临时文件的位置( **如果嫌麻烦可以直接./configure**)

 6. 编译配置完后后发现多了一个makefile文件

 7. 执行编译命令  **make**

<div style="margin-left:30px">
        <img src="../../resource\middleware\nginx\nng2.png" width =70% height = 80%/>
</div>

 8. 安装 **make install**

 9. 启动测试进入 **/usr/local/nginx**，后 **./nginx**启动

 10. 测试是否启动成功 **ps -ef|grep nginx**

 <div style="margin-left:30px">
        <img src="../../resource\middleware\nginx\nng4.png" width =70% height = 80%/>
</div>

 11. 浏览器访问：

<div style="margin-left:30px">
   		 <img src="../../resource\middleware\nginx\nng5.png" width =70% height = 80%/>
</div>

### 3. 基本命令

##### 3.1 启动

​    **./nginx**

> 注意：执行./nginx启动nginx，这里可以-c指定加载的nginx配置文件，如下：
>
> ​			./nginx -c /usr/local/nginx/conf/nginx.conf
>
> 如果不指定-c，nginx在启动时默认加载conf/nginx.conf文件，此文件的地址也可以在编译安装nginx时指定./configure的参数（--conf-path= 指向配置文件（nginx.conf）

##### 3.2 停止

  1> 快速停止  .**./nginx -s stop**   此命令相当于先查询出pid然后kill

  2> 待任务执行完毕后停止   **./nginx -s quit**

##### 3.3 重启

​	  **./nginx -s reload** 



### 4. 虚拟主机/静态代理

> **虚拟主机**：所谓的虚拟主机就类似互联网下单独的一台服务器，提供一个外部访问的端口，nginx默认启动的是80端口，访问的目录资源是nginx根目录的html文件，
>
> <div style="margin-left:30px">
> 		 <img src="../../resource\middleware\nginx\ng21.png" width =70% height = 80%/>
> </div>
>
> nginx下实现虚拟主机的方式有两种：
>
> 		1. 配置不同端口，类似原始80端口可以在配置一个81端口指定目录即可，如html2
>
>   		2. 通过不同的域名访问，例如同一个ip下配置了两个域名，也可以针对这两个域名配置不同的资源目录

> **静态代理**： nginx代理某个服务器的某个目录，可以配合ftp服务器一起使用访问静态资源，可以说 **静态代理是虚拟主机的一种应用方式。**



##### 4.1 端口方式配置虚拟主机



### 5. 反向代理/负载均衡

