

# Linux日常开发命令总结：

> 发展历史（简单描述）
>



## a) 基本命令 （上）

### 1>Ls命令 (查看文件列表)

ls   [文件目录]  

---- -----参数:

  -l   等价于 ll

  -a   查询包括隐藏文件  （组合使用 ls -al   /  ll -a）

​    注意:   隐藏文件以 . 开头，文件夹d、文件-

  -h  以kb的形式显示文件大小

 -t ：  按照时间降序   -tr按照时间升序

 -S :  按照文件大小降序   -Sr ：按照文件大小升序   （注意大写）

**常用： ll   、ll  -t 、ll -h**

如何显示出完整的时间：

​		ls -l --time-style="+%Y-%m-%d $newline%m-%d %H:%M"

​        ls --full-time



### 2> mkdir  (创建文件夹)

mkdir  文件1    [文件2]   [文件3]      （可以指定具体目录如： mkdir /home/test）

mkdir   -p /父目录/子目录



### 3> touch (创建文件/夹)

touch  文件名1  [文件名2]   （可以指定具体目录，如：touch /home/test.java）



### 4> cp (拷贝文件/文件夹)

cp  文件目录   要拷贝的文件目录  （如： cp  /home/123.txt   /etc/234.txt，拷贝的目录一定要存在）

cp -r  文件夹目录  要拷贝的文件夹目录



### 5> mv (移动命令/重命名)

mv  原始文件/文件夹    新路径     （如  rm /home/123.txt   	/etc/  ,这里不加名字相当于不改名）

重命名： 新目录和原始目录一致，名字不同即可



### 6> rm (删除文件/文件夹)

rm   文件1  [文件2]   ...    （注意文件可以使用通配符，如： rm   *.java ）

   -r : 表示递归删除 （文件夹）

   -f  表示强制删除，不询问（询问要输入n确认）

 **一般情况下我们直接使用 rm -rf  文件/文件夹 即可**



### 7>  >/>> (重定向输出)

​    ls   /  >  /123.txt    , 即将ls /  的内容输出到 123.txt，会覆盖

   ls  /  >> 123.txt   ，两个>>表示追加



### 8>  cat（简单查看文件/合并文件）

cat  文件1  [文件2]   [文件3]   (注意：cat会一下列出所有的数据)

配合>>/>完成输出共能 ： cat  123.txt  234.txt  >> hello.txt





### 9> head (查看文件头部数据)

head -n 文件路径     ： n表示行数，不写默认为10



### 10> tail (查看文件尾部数据)

tail -n 文件路径   ： n 表示行数，默认查看最后10行

参数： -f 表示监控查看，常用来跟踪查看日志信息如： tail -f catalina.out



### 11> less （查看文件内容可下拉操控）

less  需要查看的文件路径

操作：

​	    下：可以下拉一行

​        数字 + Enter 可以向下下拉数字行

​        空格 可翻页大概20行

​        q  ：退出



### 12 > wc (统计行数、文字、大小)

wc  文件名字   等价于  wc -lwc   ，及统计行数、字数、大小

这些参数都可以单独使用



### 13 clear  （清屏）

clear 清屏 等价于 Ctrl + L ， 注意并不是真正的清掉而是隐藏在上方，可滚动查看



## b） 基本命令（下）



### 1>  | (管道命令)  、grep 过滤命令

  管道可以理解为将前者的输出作为后者的输入

​				如： ll   /root | wc -l  ,查看root目录按下有多少行内容

   过滤命令经常管道命令连用标识筛选过滤

​			  如： ll  /root |grep  co ， 表示查看/root下带有co的文件/文件夹

​                 

### 2> ps (查看进程信息) 

processes status，查看服务器的进程状态   

-e：等价于-A，表示查看所有进程

-f ： 查看所有属性

  <div align="center">
  <img src="../../resource\linux\ng2.png" width = 80% height = 80% />
</div>

```
UID：该进程执行的用户id；
PID：进程id；(重点)
PPID：该进程的父级进程id，如果一个程序的父级进程找不到，该程序的进程称之为僵尸进程（parent process ID）；
C：Cpu的占用率，其形式是百分数；
STIME：进行的启动时间；
TTY：终端设备，发起该进程的设备识别符号，如果显示“?”则表示该进程并不是由终端设备发起；
TIME：进程的执行时间；
CMD：该进程的名称或者对应的路径；
```

ps经常和管道,过滤命令一起使用,**如查看tomcat运行pid：ps -ef |grep tomcat**



### 3> du (查看文件/文件夹大小)

du   文件/文件夹路径  （比wc -c 更强大，可以统计文件并且以高可用的方式展示）

-s: 只显示汇总文件的大小，如：du -s /root 会显示root目录下所有文件的大小，如果不加-s则会显示每一个文件的大小

-h  表示以加K/M高可用的方式进行展示

**常用操作直接 du -sh /etc ，查看etc下所有文件的大小**



### 4> find (查找文件)

类似于 ll  /文件路径  |grep 文件名，这种感觉

find    文件路径    [参数]  （其参数有55个之多）

-name ： 根据名字

-type ： 根据文件类型  -f标识文件 -d标识文件夹

如： find ./  -name nginx.conf -type d



### 5> kill (杀死进程命令)

常用带参数： kill -9  pid 

​                        killall -9 tomcat  ，表示杀死一类进程



### 6> service(启动/停止一些软件服务)

service  服务名 start/stop/restart

例如： service httpd start，可以通过ps -ef|grep httpd 判断是否启动成功



### 7> 查看系统版本信息

​	**查看内核版本命令**

​		 1) cat /proc/version 

​		 2) uname -a 

​	**查看linux版本：**

​		 1)lsb_release -a 

 		**2) cat /etc/redhat-release**



## 7) 进阶指令	



###  1> ping  (查看网络是否通)

### 2> telnet (查看指定ip端口是否通)

1. 安装

   ```
    yum list telnet*        列出telnet相关的安装包
    yum install telnet-server      安装telnet服务
    yum install telnet.*      安装telnet客户端
   ```

2. 使用

      **telnet  ip /域名  端口** 

### 3> ssh  (远程登录)

加密远程登录，需要传输密钥，这也是于telnet的主要区别，telnet是明文传输的

 **ssh [-p port] user@remote**

端口号默认为22， telnet默认为21



### 4> nohup & （不关闭/后台运行）

​	& : 表示让程序在后台执行，即使发出Ctrl+c (SIGINT信号)也不会停止，但是关闭session(SIGHUP信号)会停止执行。

   nohup ：忽略SIGHUP信号，默认将日志输出到nohup.out中。

**实际中我们通过nohup  命令  &  ，完成脚本后台处理操作**



### 5> firewall （防火墙）

- 查看firewall防火墙状态 ：   firewall-cmd --state   或者  systemctl status firewalld

- 打开防火墙 ： systemctl start firewalld

- 关闭防火墙： systemctl stop firewalld

- 重启防火墙 ： firewall-cmd –reload 或者 systemctl reload firewalld

- 开机自动启动防火墙 ： systemctl enable firewalld

- 开机禁用防火墙： systemctl disable firewalld

- 查看已经打开的端口 ：  firewall-cmd --list-ports

- 打开端口：  firewall-cmd --permanent --zone=public --add-port=80/tcp  

  ​                           （permanent表示永久生效，public表示作用域，8080/tcp表示端口和类型）

- 关闭端口：  firewall-cmd --permanent --zone=public --remove-port=80/tcp

### 6> chomd赋 (赋权限)

  <div align="center">
  <img src="../../resource\linux\ng1.png" width = 80% height = 80% />
</div>

共10为，可分为三组1-3-3-3

首位表示文件类型：  d表示文件夹、-表示文件、l表示链接文件

其后可分为： u （所属者/创建人）、g（同组下）、o：其他人

**其中 r：读权限（4）、w：写权限（2）、x：执行权限（1） -：表示无权限**

例如： **chomd 777 文件/目录** ，表示给u、g、o赋所有权限

​             chomd 776， 表示不同组的其他用户没有执行权限

参数： -R  表示递归操作即当前文件夹下的所有文件都赋予权限



#### 7> 硬链接软链接

软链接： ln -s    源文件/目录(注意目录最后要加上/)   链接名

硬链接： ln -s 源文件/目录  链接名



区别：软链接相当于快捷方式，硬链接相当于复制了源文件，但是会随着源文件的修改而修改，如果删除了源文件则软链接不能正常使用，硬链接依旧可以使用。

删除方式 rm删除即可， 如：rm 链接名   