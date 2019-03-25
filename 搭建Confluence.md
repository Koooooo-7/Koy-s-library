## 搭建Confluence

Confluence是一个团队wiki管理工具，可以归纳整理很多内容。

系统  CentOS 7.2
安装 Confluence 6.14.1
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
参考https://blog.csdn.net/Dsky7/article/details/87717684
    https://blog.csdn.net/qq_34889607/article/details/81118106
下载，可以下载了传上去，也可以直接下载wget下载。
wget https://www.atlassian.com/software/confluence/downloads/binary/atlassian-confluence-6.14.1-x64.bin
```
给予安装权限
chmod +x atlassian-confluence-6.14.1-x64.bin 
进行安装./atlassian-confluence-6.14.1-x64.bin 
使用了uses default settings即1
查看端口
lsof -i:8090
注意firewalld防火墙的8090端口有没有开放...。
此时访问服务器8090端口已经可以看到界面了。
这时候开始破解
``
参考https://blog.csdn.net/XunCiy/article/details/81981944
    https://blog.csdn.net/Dsky7/article/details/87717684
破解的生成器：https://pan.baidu.com/s/1pJX9VjovMiTl0o1VyAaitw   m2jz   
具体破解步骤
运行jira_keygen.jar，
将ServerID粘贴填入，
姓名Name、邮箱Email、组织Organization可随意填写，也可根据实际情况填写，会作为系统信息显示，但不影响破解，
然后点击.gen!，生成key
将下载的原atlassian-extras-decoder-版本可能不一样.jar（建议先拷贝个副本备份）更名为atlassian-extras-2.2.2.jar
然后点击.patch，并选择atlassian-extras-2.2.2.jar打开，
提示Jar successfully patched，并且生成了一个.bak文件
然后改回原来的名字把原来的给换掉。


 


