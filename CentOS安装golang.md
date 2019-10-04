## CentOS安装

### 首先安装 wget

```nginx
yum -y install wget
yum -y install setup
yum -y install perl
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
export GOPATH=/var/opt/wwwroot/goblin
source /etc/profile   //返回到root行执行此命令
```

![1570080212560](C:\Users\DELL\Desktop\MyBook\img\model.go)

安装结束，验证

```nginx
go version
```







