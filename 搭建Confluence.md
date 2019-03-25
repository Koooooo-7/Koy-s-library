## 搭建Confluence

Confluence是一个团队wiki管理工具，可以归纳整理很多内容。

系统  CentOS 7.2


1.安装Mysql  
```sudo yum install -y mariadb mariadb-server```
启动并且开机启动
```
$ sudo systemctl start mariadb  
$ sudo systemctl enable mariadb
```
###### 配置文件
解决中文乱码等问题
$ sudo vim /etc/my/cnf 

```
init_connect='SET collation_connection =utf8_unicode_ci'
init_connect='SET NAMES utf8'
character-set-server=utf8
collation-server=utf8_unicode_ci
skip-character-set-client-handshake
max_allowed_packet=256M
transaction-isolation=READ-COMMITTED
```
$ sudo vim /etc/my.cnf.d/mysql-clients.cnf ---> # 在[mysql]下面添加如下

    default-character-set=utf8

$ sudo vim /etc/my.cnf.d/client.cnf ---> # 在[client]下面添加如下

    default-character-set=utf8
进行安装配置
$ sudo mysql_secure_installation
Remove anonymous users? [Y/n] <– 是否删除匿名用户，回车
Disallow root login remotely? [Y/n] <–是否禁止root远程登录,回车,
Remove test database and access to it?[Y/n] <– 是否删除test数据库，回车
Reload privilege tables now? [Y/n] <– 是否重新加载权限表，回车
创建数据库、用户名和密码
create databaseconfluence default character set utf8 collate utf8_bin;

赋予confluence用户任意主机访问confluence数据库，密码是admin
grant all on confluence.* to 'admin'@'%' identified by 'admin';
grant all on confluence.* to 'admin'@'localhost' identified by'admin';
权限刷新
flush privileges;
查看用户表
select user,host,password from mysql.user;

2.安装JDK1.8
  之前有写过安装过程，[这里](https://github.com/Koooooo-7/Koy-s-library/blob/master/%E5%AE%89%E8%A3%85JDK1.8u201)。
  
  
### 开始安装Confluence
下载，可以下载了传上去，也可以直接下载wget下载。
wget https://www.atlassian.com/software/confluence/downloads/binary/atlassian-confluence-6.14.1-x64.bin
