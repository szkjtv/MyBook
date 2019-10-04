## CentOS 7安装 数据 库极开启远程连接上步骤

### 首先安装 wget

```html
yum -y install wget  //安装这个即可
yum -y install setup
yum -y install perl
```

### centos没有安装vim

```mysql
yum -y install vim*
```

### 下载mysql的源

```mysql
wget http://dev.mysql.com/get/mysql57-community-release-el7-7.noarch.rpm
```

### 安装yum库

```mysql
yum localinstall -y mysql57-community-release-el7-7.noarch.rpm
```

### 安装MySQL

```mysql
yum install -y mysql-community-server
```

### 启动MySQL服务

```mysql
systemctl start mysqld.service
```

MySQL5.7加强了root用户的安全性，因此在第一次安装后会初始化一个随机密码，
以下为查看初始随机密码的方式

```mysql
grep 'temporary password' /var/log/mysqld.log
```

### 安装好数据库使用以下命令输入初始密码登录

```mysql
mysql -u root -p
```

不能登录时进入

```mysql
vim /etc/my.cnf
```

在最后插入以下内容

```mysql
skip-grant-tables
```

![1570201881083](C:\Users\DELL\Desktop\MyBook\img\1570201881083.png)

登录进mysql后直接修改就好

### 然后修改密码

```mysql
SET PASSWORD = PASSWORD('your new .aA1451418');
ALTER USER 'root'@'localhost' PASSWORD EXPIRE NEVER;
flush privileges;
```

然后退出后即可用新密码登录。

远程连接授权

```mysql
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY '数据库密码' WITH GRANT OPTION;
```

的root下执行

```mysql
firewall-cmd --add-port=3306/tcp
```







mysql的一些命令

```mysql
1.启动命令

[root@xufeng Desktop]# service mysqld start
Redirecting to /bin/systemctl start mysqld.service
2.关闭命令

[root@xufeng ~]# service mysqld stop
Redirecting to /bin/systemctl stop mysqld.service
3.重启命令

[root@xufeng ~]# service mysqld restart
Redirecting to /bin/systemctl restart mysqld.service

4.查看服务状态

[root@xufeng ~]# service mysqld status
Redirecting to /bin/systemctl status mysqld.service
● mysqld.service - MySQL Server
Loaded: loaded (/usr/lib/systemd/system/mysqld.service; disabled; vendor preset: disabled)
Active: active (running) since Wed 2018-07-18 22:34:06 EDT; 1min 11s ago
Docs: man:mysqld(8)
http://dev.mysql.com/doc/refman/en/using-systemd.html
Process: 4366 ExecStart=/usr/sbin/mysqld --daemonize --pid-file=/var/run/mysqld/mysqld.pid $MYSQLD_OPTS (code=exited, status=0/SUCCESS)
Process: 4345 ExecStartPre=/usr/bin/mysqld_pre_systemd (code=exited, status=0/SUCCESS)
Main PID: 4370 (mysqld)
CGroup: /system.slice/mysqld.service
└─4370 /usr/sbin/mysqld --daemonize --pid-file=/var/run/mysqld/mysqld.pid

```











