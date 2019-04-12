#### 1.进入gitlab配置文件gitlab.rb中。
```
gitlab_rails['ldap_enabled'] = true  //开启 LDAP服务
gitlab_rails['ldap_servers'] = {  //服务配置
'main' => {
  'label' => 'GitLab AD',  //配置名称 自定义就好
  'host' =>  'mt.com',  // 配置域名
  'port' => 389,  // 389端口，如果使用SSL时用636
  'uid' => 'sAMAccountName',  //用户名属性
  #'encryption' =>'simple_tls',  //配置加密编码，未配置，即使用默认明文
  'verify_certificates' => false,  //是否开启证书验证 因为都没有用SSL颁发证书，所以false
  'bind_dn' => 'CN=mt,DC=dgyiheda,DC=com',    //配置登录AD域的认证用户名
  'password' => '******',  //配置用户密码
  'active_directory' => true,  //是不是使用AD域方式，true
  'base' => 'DC=dgyiheda,DC=com',  //基本DN，指明从哪里开始搜索
 #'group_base' => 'OU=Global Groups,OU=GitLab INT,DC=GitLab,DC=org', //指明搜索的组
 #'admin_group' => 'Global Admins'  //admin组，可配置使其也成为Gitlab上的Admin用户。
  }
}
```
 
#### 2.重新加载配置  
`gitlab-ctl reconfigure`
 
#### 3.检查用户是否可以检出用户  
`gitlab-rake gitlab:ldap:check`


参考文档：  
https://docs.gitlab.com/ee/administration/auth/how_to_configure_ldap_gitlab_ce/  
https://docs.gitlab.com/ee/administration/auth/how_to_configure_ldap_gitlab_ee/  
https://www.linuxidc.com/Linux/2018-01/150516.htm  
