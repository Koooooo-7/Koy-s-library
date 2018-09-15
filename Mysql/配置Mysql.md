### 配置文件地址  
    ```vim  /etc/my.cnf```



### 配置数据库可以远程访问
    ```
    配置mysql端口，默认是3306，显然我改了，对应的，防火墙的开放端口也要记得添加。
    在/etc/my.cnf  配置文件中添加自己更改的端口。
    [mysqld]
    port=我的端口号。
    ....
    datadir=/var/lib/mysql
    socket=/var/lib/mysql/mysql.sock
    user=mysql
    grant all privileges on *.* to 'root'@'%' identified by '123456' with grant option; ```
    最好不要直接用root用户和弱密码登录。mysqlroot   A..@
