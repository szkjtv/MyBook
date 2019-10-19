## CentOS安装

### 首先安装 wget

```nginx
yum -y install wget
yum -y install setup
yum -y install perl
yum -y install git  //
yum  install git //不用-y也可以安装的上
```

### centos没有安装vim

```nginx
yum -y install vim*
```

以下，下载golang安装命令有相对应的版本输入数字即可//go升级到13版

```nginx
wget https://storage.googleapis.com/golang/go1.13.linux-amd64.tar.gz
```

解压刚刚下载好的安装命令//go升级到13版

```nginx
tar zxvf go1.13.linux-amd64.tar.gz -C /usr/local
```

新建一个go项目的目录//-p后面可自定义

```nginx
mkdir -p /var/opt/wwwroot/goblog
```

配置环境变量

```nginx
vim /etc/profile  //进到这个文件以下命令粘贴到最下面
export GOROOT=/usr/local/go
export GOBIN=$GOROOT/bin
export PATH=$PATH:$GOBIN
export GOPATH=/var/opt/wwwroot/goblin  //设置自己的path路径
source /etc/profile   //返回到root行执行此命令
```

![1570080212560](C:\Users\DELL\Desktop\MyBook\img\model.go)

![1571471719350](C:\Users\DELL\AppData\Roaming\Typora\typora-user-images\1571471719350.png)	



安装结束，验证

```nginx
go version
```





linux编译go运行环境

```
在xx.go所在的的文件夹下按sheet+鼠标右键在dos下打开，执行下面的命令

set GOARCH=amd64

set GOOS=linux

go build xx.go

会生成一个没有后缀的xx二进制文件

将该文件放入linux系统某个文件夹下

赋予权限

chmod 777 xx

执行

./xx

运行成功，该二进制文件不需要go的任何依赖，可以直接运行。
————————————————
版权声明：本文为CSDN博主「马克Markorg」的原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/csgarten/article/details/80299059
```

# Linux下编译运行Go程序

```go
编译

go build test.go 
1
指定输出文件

go build -o mygameserver
1
修改权限命令

chmod 777 程序名称
1
后台运行的命令

nohup ./程序名 & 
1
不输出错误信息

nohup ./程序名 >/dev/null 2>&1 &
1
如果要关闭程序，可以使用命令”ps” 查看后台程序的pid，然后使用“kill 程序pid”命令，关闭程序比如程序名为test，可以用如下命令查询

ps aux|grep test
1

```



