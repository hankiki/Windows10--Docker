# Windows10--Docker
引用我的CSDN文档-Windows10 环境下的 Docker使用(https://blog.csdn.net/hanjupiter/article/details/100173356)

**Docker是什么？**

Docker是 虚拟机的一种，是在一个有限资源的软件环境中（可以看做是一台虚拟机）运行多台体积非常小的linux/Windows操作系统，每一个linux操作系统中仅存在一个或者多个 特定需求的软件。 
可以理解为 现实中的大海 就是一台真实的计算机操作系统，docker软件就是大海中的特定容量的一艘货船（分配的固定内存大小），每一个通过docker软件运行的linux操作系统就是货船上一个集装箱，在这艘船上可以存放多少个集装箱，取决于这个货船有多大。
相对比于传统的虚拟机（如 VMware，VirtulBox），通过系统镜像ISO 安装一个完整的操作系统占用大量的系统资源（内存），相当于占用了一个大的岛屿，在一个操作中有时仅仅安装一个软件，这样会导致浪费了大量的系统资源。Docker的优势是在最简单的linux/Windows操作系统中安装这个软件后，仅占用货船上很少的资源（如100M内存）。

Windows10 安装Docker软件
**1.注册账号**
在Docker官方网站上注册一个DockerID
https://hub.docker.com/signup
**2.下载**
https://docs.docker.com/docker-for-windows/install/ 中点击【Download from Docker Hub】，
进入到下载画面后，点击【Download Docker Desktop for windows】进行下载 Community 版本

![https://hub.docker.com/?overlay=onboarding](https://img-blog.csdnimg.cn/2019083115451981.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hhbmp1cGl0ZXI=,size_16,color_FFFFFF,t_70)
**3.安装**
3.1虚拟化确认
 1. 在任务管理器中的性能选项卡的CPU画面中 虚拟化 = **已启用** 的状态。
 2. **未启用**状态的话，需要打开BIOS中的支持虚拟化技术 https://docs.docker.com/docker-for-windows/troubleshoot/#virtualization-must-be-enabled
![虚拟化确认](https://img-blog.csdnimg.cn/20190831155329711.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hhbmp1cGl0ZXI=,size_16,color_FFFFFF,t_70)
3.2开启HYPER-V
 a.打开控制面板中的程序和功能选项
 b.点击【启用或关闭Windows功能】

![HYPER-V启动](https://img-blog.csdnimg.cn/20190831155805160.png)
c.在Windows功能中，勾选Hyper-V虚拟机功能
![Hyper-V](https://img-blog.csdnimg.cn/20190831160233705.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hhbmp1cGl0ZXI=,size_16,color_FFFFFF,t_70)
d.打开Docker for Windows Installer.exe 进行默认安装
![Docker for Windows Installer](https://img-blog.csdnimg.cn/20190831160520401.png)
e.在系统的托盘中找到docker图标，**右键**打开，点击**Setting**
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019083116105576.png)
f.https://hub.docker.com网站延迟大或者无法登陆的场合， 需要设定替代的镜像下载地址
在Daemon的画面中，勾选Advanced，并且设定下面的配置，配置后，点击Apply，Docker服务会重新启动。
```powershell
{
  "registry-mirrors": [
    "https://mirror.ccs.tencentyun.com",
    "https://hub-mirror.c.163.com",
    "https://registry.docker-cn.com",
    "https://dockerhub.azk8s.cn",
    "https://docker.mirrors.ustc.edu.cn"
  ],
  "insecure-registries": [],
  "debug": true,
  "experimental": false
}
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190831161514763.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hhbmp1cGl0ZXI=,size_16,color_FFFFFF,t_70)
g.设定Docker软件的资源容量
打开Advanced画面，按实际计算机进行配置使用的CPU，内存的资源大小，点击Apply，Docker自动重启后生效。
**PS：内存设定大小后，会永久占用系统资源**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190831161642987.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hhbmp1cGl0ZXI=,size_16,color_FFFFFF,t_70)
h.上面的操作完成后，在开始菜单中，搜索Hyper-V，并打开【Hyper-V管理器】
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190831162000852.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hhbmp1cGl0ZXI=,size_16,color_FFFFFF,t_70)
在管理器中可以看到Docker虚拟机软件 已经启动，并且占用系统的1024M内存（货船已经造好了）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190831162200656.png)
i.开始菜单上右键，启动Windows PowerShell（管理员）
使用-v命令查下docker 软件的版本，返回对应的版本，安装成功

```powershell
docker -v
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190831163211198.png)

**4.使用Docker**
a.下载镜像
在https://hub.docker.com/search?q=&type=image 中搜索想要下载的镜像名称(把集装箱从工厂运输到港口)
windows的docker镜像请参考
https://docs.microsoft.com/en-us/virtualization/windowscontainers/

这里以tomcat进行举例

 1. 打开相应的tomcat镜像，点击打开

![tomcat](https://img-blog.csdnimg.cn/2019083116284736.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hhbmp1cGl0ZXI=,size_16,color_FFFFFF,t_70)
2.拷贝image的pull命令
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190831163022142.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hhbmp1cGl0ZXI=,size_16,color_FFFFFF,t_70)
3.在PowerShell中 执行命令
```
docker pull tomcat
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190831163432297.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hhbmp1cGl0ZXI=,size_16,color_FFFFFF,t_70)
4.镜像下载成功后，使用命令进行镜像列表确认
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190831164110221.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hhbmp1cGl0ZXI=,size_16,color_FFFFFF,t_70)

```powershell
docker images
```
可以看到本地的仓库中已经存在最新的镜像（港口中的集装箱列表）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190831164229542.png)
5.启动tomcat（把港口的tomcat集装箱[容器]装上船），并返回一个船上的集装箱[容器]的ID
```powershell
 docker run -d -p 30001:8080 --name test_tomcat tomcat
 参数：
 run :运行新镜像
 -d  :后台运行镜像
 -p  :主机本地端口与容器内的端口的映射，即访问主机的30001端口 等于访问tomcat的8080端口
 --name : 给集装箱[容器] 起个别名
 tomcat  : 被执行的镜像名称
返回值 : containerID 新做成的容器的ID
 ```
![启动tomcat](https://img-blog.csdnimg.cn/201908311805424.png)
 PS:其他参数
 ```powershell
-m 512m --memory-swap 1G --restart=always 
 参数：
 -m  : 内存限制，格式是数字加单位，单位可以为 b,k,m,g。最小为 4M
--memory-swap   :  内存+交换分区大小总限制。格式同上。必须必-m设置的大
 --restart : HOST主机-容器开机启动设定
 always -> 开机自动启动
文档连接: https://docs.docker.com/config/containers/start-containers-automatically/
 ```
6.查看运行中的docker容器列表（船上都有哪些正在被使用的集装箱）
```powershell
 docker ps
 ```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190831181332980.png)
7.本地访问测试
```powershell
http://localhost:30001
 ```
返回tomcat的管理画面
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190831181527998.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hhbmp1cGl0ZXI=,size_16,color_FFFFFF,t_70)
8.登录到容器系统中，查看tomcat的log
```powershell
docker exec -it {容器ID} shell类型
例如: docker exec -it b49ab11143fc bash
 ```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190831181749679.png)
9.指定登录用户（某些镜像中的默认登录者是非root用户，可以指定登录的用户）
```powershell
docker exec -it {容器ID} --user 指定登录用户 shell类型
例如: docker exec -it --user root b49ab11143fc bash
 ```
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190831182018414.png)
 10.本地磁盘的目录与容器内的目录/文件 进行映射
 Windows环境，需要建立共享文件夹，将共享文件夹与容器内的文件夹进行映射
 

 - 新建共享文件夹 c:\docker_share
 - 开放共享，文件夹 右键属性
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190831182756701.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hhbmp1cGl0ZXI=,size_16,color_FFFFFF,t_70)![在这里插入图片描述](https://img-blog.csdnimg.cn/2019083118272254.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hhbmp1cGl0ZXI=,size_16,color_FFFFFF,t_70)![在这里插入图片描述](https://img-blog.csdnimg.cn/2019083118270377.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hhbmp1cGl0ZXI=,size_16,color_FFFFFF,t_70)
 - 在本地的C:\docker_share中 创建文件夹 webapps
 - 在文件夹内创建test文件夹，在test文件夹中添加index.html，并添加内容

```powershell
<html>
<body>
Hello World !
</body>
</html>
```

 - 创建一个新docker 容器，并且将tomcat的容器中的目录/usr/local/tomcat/webapps与本地的C:\docker_share\webapps进行映射
 - 初次添加映射时，会提示是否允许将驱动器进行分享，点击[share]
```powershell
 docker run -d -p 30002:8080 --name test_tomcat_mount -v /c/docker_share/webapps:/usr/local/tomcat/webapps tomcat
 参数：
 -v : 本地磁盘目录或文件路径:容器内的目录或文件路径 windows环境下，指定的磁盘的驱动器要写成 /驱动器号 例如/c
 ```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190831184223672.png)
 
 - 验证tomcat是否被启动

 ```powershell
 docker ps
 ```
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190831184246361.png)

 - 访问30002端口的 test下index.html网页
```powershell
http://localhost:3002/test/index.html
 ```
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190831184507321.png)
 

 - 修改本地C:\docker_share\webapps\test的index.html文件内容
```powershell
<html>
<body>
Hello World !  -> first modify
</body>
</html>
```
 - 再次访问30002端口的 test下index.html网页，内容被成功同步
```powershell
http://localhost:3002/test/index.html
 ```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190831184658915.png)
11.重启容器
有些应用程序，再更新后，需要重新启动服务
在docker中，可以直接重启容器对象
```powershell
docker restart 容器ID
例如 docker restart 2901d3d61c20
 ```
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190831185132854.png)
 - 验证容器ID 2901d3d61c20是否被启动

 ```powershell
 docker ps
 ```
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190831185219328.png)
 12.停止一个运行中的容器
 ```powershell
docker stop 容器ID
例如 docker stop 2901d3d61c20
 ```
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190831185408687.png)
 - 验证容器ID 2901d3d61c20是否被成功停止

 ```powershell
 docker ps
 ```
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190831185436519.png)
 13.查询所有的docker容器，包含运行中及停止的
 ```powershell
 docker ps -a
 ```
 2901d3d61c20 的状态显示为停止
 b49ab11143fc 的状态显示为运行中，已经启动了50分钟
即30002端口不可以访问，30001端口可以访问
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019083118555328.png)
14.启动已经停止运行的容器
```powershell
docker restart 容器ID
例如 docker restart 2901d3d61c20
 ```
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190831185806635.png)
 验证是否启动成功
 ```powershell
docker ps
 ```
 ![30002端口已经在运行状态](https://img-blog.csdnimg.cn/20190831185836612.png)
 15.查询容器的资源占用
  ```powershell
 docker stats
  ```
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190831190048347.png)
16.删除一个容器
对已经停止（docker ps -a -> STATUS = Exited）的容器进行删除
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019090114580772.png)
```powershell
docker rm 容器ID
例如 docker rm d6959ff9238c
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190901145928677.png)
  17.桥接（bridge ）网络
  在创建docker的容器对象时，可以指定容器的IP地址，并且指定容器在哪个创建的子网内
  docker默认有3种网络模式，默认使用桥接类型
  

 - host：容器将不会虚拟出自己的网卡，配置自己的IP等，而是使用宿主机的IP和端口。
 - None：该模式关闭了容器的网络功能。
 - Bridge：此模式会为每一个容器分配、设置IP等，并将容器连接到一个docker0虚拟网桥，通过docker0网桥以及Iptables nat表配置与宿主机通信。

Container：创建的容器不会创建自己的网卡，配置自己的IP，而是和一个指定的容器共享IP、端口范围。



 - 创建一个新定义的IP子网段
 
  ```powershell
  docker network create --driver bridge --subnet 172.19.0.0/16 网络别名
  参数：
  network : 网络命令
  create   :创建一个新的网络
  --driver : 网络驱动类型 例如：bridge 
  --subnet : 子网的网段
  网络别名  : 例如 : php-net
  
  例如：  docker network create --driver bridge --subnet 172.19.0.0/16 php-net
  ```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190831191232150.png)
 - 查看网络列表
  ```powershell
docker network ls
  ```
  新的php-net网络创建成功
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/2019083119130822.png)
 - 在指定网段中，创建容器 并且指定IP地址
 
  ```powershell
docker run -d --name test_network_tomcat --network php-net --ip 172.19.0.11 tomcat
参数：
--network : 要加入的网络名称 例如 php-net
--ip : 对应网络中的IP地址 例如: 172.19.0.11
  ```
  在这个镜像中，并没有设置端口映射，所以本地无法访问到此容器
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190831191754517.png)
  验证是否创建成功
 ```powershell
docker ps
 ```
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190831191809942.png)
 
 - 登录到容器，查看IP地址
  ```powershell
docker exec -it fad2a6942635 bash
 ```
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190831200649727.png)
由于镜像中的操作系统，没有集成ip addr命令，需要手动通过apt-get自动升级 进行安装
  ```powershell
apt-get update
apt-get -y install iptables
 ```
 ```powershell
ip addr
 ```
 可以看到ip地址 **172.19.0.11**已经被设置
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190831201513891.png)
 
 - 在相同的网络中，安装Nginx容器，使用代理转发，访问 **172.19.0.11**的tomcat
 
a.在docker的镜像库中检索Nginx容器的镜像
 ```powershell
docker search nginx
 ```
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190831201839737.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hhbmp1cGl0ZXI=,size_16,color_FFFFFF,t_70)
 b.通过镜像的名称 ，下载镜像，并且在同一个网络中运行
 ```powershell
docker pull nginx
 docker run -d --name test_network_nginx -p 30003:80 --network php-net --ip 172.19.0.12 nginx
 ```
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190831203438240.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hhbmp1cGl0ZXI=,size_16,color_FFFFFF,t_70)
c. 使用30003端口进行访问,nginx画面显示
```powershell
http://localhost:30003
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190831204027835.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hhbmp1cGl0ZXI=,size_16,color_FFFFFF,t_70)
d.拷贝nginx容器内的配置文件到主机

```powershell
docker cp 源路径 目标路径
参数:
cp  : 拷贝命令
源文件路径 :容器ID:/文件名 或者 windows主机目录/文件名   
目标路径 : windows主机目录/文件名 或者 容器ID:/文件名 
注: windows主机目录的格式为 磁盘驱动器:/   例如c:/...
例如 docker cp 8489b0234116:/etc/nginx/conf.d/default.conf c:/docker_share/default.conf
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190831205902623.png)
e.修改本地的nginx配置

```powershell
#代理网址列表，多个地址的场合，Nginx自动对地址列表进行负载均衡,在tomcat8以上的场合，upstream的名字不能带下划线(_)
upstream tomcatproxy {
     server 172.19.0.11:8080;
      }
server {
    listen       80;
    server_name  localhost;

    #charset koi8-r;
    access_log  /var/log/nginx/host.access.log  main;

    location / {
        #
        proxy_pass http://tomcatproxy/test/;
    }

    #charset koi8-r;
    #access_log  /var/log/nginx/host.access.log  main;

    #error_page  404              /404.html;

    # redirect server error pages to the static page /50x.html
    #
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }
}
```
f.拷贝至nginx容器中，并重启nginx，
```powershell
docker cp 源路径 容器ID:目标路径
例如:docker cp c:/docker_share/default.conf 8489b0234116:/etc/nginx/conf.d/default.conf
docker restart 容器ID
例如:docker restart 8489b0234116
```
g.登录到tomcat容器中，在/usr/local/tomcat/webapps/路径中，创建test文件夹，并且在test文件夹中，安装vim插件，添加index.html文件，重启tomcat容器
index.html内容：
```powershell
<html>
<body>
Nginx -> tomcat 
</body>
</html>
```

```powershell
docker exec -it  容器ID bash
例如:docker exec -it fad2a6942635 bash
#apt-get update
#apt-get -y install vim
#cd webapps/
#mkdir test
#cd test/
# vim index.html
#exit
docker restart 容器ID
例如:docker restart fad2a6942635 
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190831213645376.png)
h.本地访问
```powershell
http://localhost:30003/
```
跳转顺序:
本地网页访问http://localhost:30003/ 
第一次跳转到  nginx（**172.19.0.12**）的80端口
第二次跳转到 tomcat（**172.19.0.11**）的 8080端口的test文件夹的index.html
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190901141024825.png)

i.Nginx的负载均衡实现

 - 新建一个tomcat 容器指定IP为（**172.19.0.13**）
 ```powershell
docker run -d --name test_network_tomcat2 --network php-net --ip 172.19.0.13 tomcat
```
- 登录到 test_network_tomcat2 中 , 在/usr/local/tomcat/webapps/中创建test文件夹，并在test文件夹中，添加index.html
index.html内容如下:
```powershell
<html>
<body>
Nginx -> tomcat 2
</body>
</html>
```
 - 修改nginx容器的配置文件，在tomcatproxy 的 upstream 中 添加新的节点，拷贝到nginx容器中，并重启nginx容器
 ```powershell
upstream  tomcatproxy  {
     server 172.19.0.11:8080;
     server 172.19.0.13:8080;
      }
```
测试访问，多次刷新画面:
```powershell
http://localhost:30003/
```
访问到1号机
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190901142539333.png)
 访问到2号机
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190901142524408.png)


**Docker UI 管理工具**

**kitematic**
桌面版本管理工具 
1.下载地址：https://github.com/docker/kitematic/releases/ 
下载 最新版本的Kitematic-*-Windows.zip的客户端，然后解压缩到 C:\Program Files\Docker\Kitematic中
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190901143137230.png)
2.启动Kitematic
右键打开docker客户端的系统托盘，点击Kitematic按钮
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190901143403343.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hhbmp1cGl0ZXI=,size_16,color_FFFFFF,t_70)
3.在桌面客户端中，可以下载镜像，启动镜像，查看镜像的实时log，登录到镜像等功能。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190901142847904.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hhbmp1cGl0ZXI=,size_16,color_FFFFFF,t_70)

**Portainer**
Web版本管理工具
Portainer是一个docker的镜像
下载访问: 
docker pull
```powershell
docker pull portainer/portainer
```
部署 
https://portainer.readthedocs.io/en/latest/deployment.html
1.建立本地磁盘存储c:/docker_share/portainer/data文件夹
```powershell
docker run -d -p 9000:9000 --restart=always --name portainer -v /var/run/docker.sock:/var/run/docker.sock -v /c/docker_share/portainer/data:/data portainer/portainer
```
登录
输入8位密码，点击【Create user】
```powershell
http://localhost:9000/#/init/admin
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190901144349317.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hhbmp1cGl0ZXI=,size_16,color_FFFFFF,t_70)
连接方式:
1.本地模式（Local）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190901144426101.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hhbmp1cGl0ZXI=,size_16,color_FFFFFF,t_70)
2.远程方式(Remote)
```powershell
Windows 版本 Endpoint URL: docker.for.win.localhost:2375
```
![Remote](https://img-blog.csdnimg.cn/20200114210844699.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hhbmp1cGl0ZXI=,size_16,color_FFFFFF,t_70)
在主画面中，可以看到docker常用的功能
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190901145405478.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hhbmp1cGl0ZXI=,size_16,color_FFFFFF,t_70)
暂停/恢复 Windows的 Docker Hyper-V虚拟机
暂停:
在Hyper-V管理器中，在DockerDesktopVM 右键，点击【保存】,主机系统释放，docker无法使用
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190901180452106.png)
在Hyper-V管理器中，在DockerDesktopVM 右键，点击【启动】,主机系统内存被占用，可以正常使用docker
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190901180612612.png)
**Docker 开启 tcp 连接 及api访问**
桌面版本的docker 默认是不开启tcp远程连接，所以无法进行api调用，
使用docker -H tcp://0.0.0.0:2375 ps 命令后，返回无法连接的异常

```powershell
PS C:\Users\Administrator> docker -H tcp://0.0.0.0:2375 ps
error during connect: Get http://0.0.0.0:2375/v1.40/containers/json: dial tcp 0.0.0.0:2375: connectex: No connection could be made because the target machine actively refused it.
```
开启方法，在桌面版本的Settings中 General选项卡中 开启Expose daemon on tcp 勾选
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190928095246911.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hhbmp1cGl0ZXI=,size_16,color_FFFFFF,t_70)
再次使用docker -H tcp://0.0.0.0:2375 ps，可以使用网络请求连接到docker服务

```powershell
PS C:\Users\Administrator> docker -H tcp://0.0.0.0:2375 ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
PS C:\Users\Administrator>
```
Api 参考文档https://docs.docker.com/develop/sdk/
获取当前docker使用的API版本号
命令:curl http://127.0.0.1:2375/info

```powershell
PS C:\Users\Administrator> curl http://127.0.0.1:2375/info
返回值:
RawContent        : HTTP/1.1 200 OK
                    Api-Version: 1.40
```

Java 开发
**Pom.xml**

```yaml
<!-- https://mvnrepository.com/artifact/com.github.docker-java/docker-java -->
		<dependency>
			<groupId>com.github.docker-java</groupId>
			<artifactId>docker-java</artifactId>
			<version>3.1.5</version>
		</dependency>
```

```java
import com.github.dockerjava.api.DockerClient;
import com.github.dockerjava.api.model.Info;
import com.github.dockerjava.core.DefaultDockerClientConfig;
import com.github.dockerjava.core.DockerClientBuilder;
import com.github.dockerjava.core.DockerClientConfig;

public class DockerManage {
	public static void main(String[] args) {
		DockerManage app = new DockerManage();
		app.initDocker();
	}

	private DockerClient initDocker() {
		DockerClientConfig config = DefaultDockerClientConfig.createDefaultConfigBuilder()
				.withDockerHost("tcp://127.0.0.1:2375").withDockerTlsVerify(false)
				.withDockerConfig("C:\\Users\\Administrator\\.docker").withApiVersion("使用的版本号")
				.withRegistryUrl("https://index.docker.io/v1/").build();
		DockerClient dockerClient = DockerClientBuilder.getInstance(config).build();
		Info info = dockerClient.infoCmd().exec();
		System.out.println("docker的环境信息如下：=================");
		System.out.println(info);
		return dockerClient;
	}
}
```
程序执行结果

```bash
docker的环境信息如下：=================
com.github.dockerjava.api.model.Info@539d019[architecture=x86_64,....
```
