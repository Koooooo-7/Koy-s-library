# 常规操作:
```
select `ff_admin_user`.`id` AS `user_id`,`ff_admin_user`.`user_login` AS `user_name` from `ff_admin_user` 
where (`ff_admin_user`.`user_status` = 1) 
union all
select `ff_firm`.`id` AS `user_id`,`ff_firm`.`firm_name` AS `user_name` from `ff_firm` 
where ((`ff_firm`.`user_status` = 0) and (`ff_firm`.`delete_time` = 0))
```

# 骚操作
### 添加一个原表中不存在的字段作为flag位。
```
select `ff_admin_user`.`id` AS `user_id`,`ff_admin_user`.`user_login` AS `user_name`,         0 AS `flag`            from `ff_admin_user`
where (`ff_admin_user`.`user_status` = 1) 
union all 
select `ff_firm`.`id` AS `user_id`,`ff_firm`.`firm_name` AS `user_name`,                      1 AS `flag`            from `ff_firm` 
where ((`ff_firm`.`user_status` = 0) and (`ff_firm`.`delete_time` = 0))
```

原因  as 在字段存在时作为别名，在字段不存在时，创建这个字段      值 AS  字段名
