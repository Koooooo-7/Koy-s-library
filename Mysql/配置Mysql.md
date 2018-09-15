### 配置文件地址  
    ```vim  /etc/my.cnf```



### 配置数据库可以远程访问
    ```grant all privileges on *.* to 'root'@'%' identified by '123456' with grant option; ```
    最好不要直接用root用户和弱密码登录。
