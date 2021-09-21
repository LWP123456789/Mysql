## DML语言

/*

数据操作语言

*/

### 插入 insert

语法：

insert into 表名(列名,...) values(值1,...);

特点：
1、要求值的类型和字段的类型要一致或兼容
2、字段的个数和顺序不一定与原始表中的字段个数和顺序一致
但必须保证值和字段一一对应
3、假如表中有可以为null的字段，注意可以通过以下两种方式插入null值
①字段和值都省略
②字段写上，值使用null
4、字段和值的个数必须一致
5、字段名可以省略，默认所有列



#1、要求值的类型和字段的类型要一致或兼容

INSERT INTO beauty(id,NAME,sex,borndate,phone,photo,boyfriend_id)

VALUES(13,'唐艺昕','女','1990-4-23','189888888',NULL,'2');

#2、不可一味null得列必须插入值,可以为null的列是如何插入值？

#方式一：

INSERT INTO beauty(id,NAME,sex,borndate,phone,photo,boyfriend_id)

VALUES(13,'唐艺昕','女','1990-4-23','189888888',NULL,'2');

#方式二：(为空的去掉不写)

INSERT INTO beauty(id,NAME,sex,borndate,phone,boyfriend_id)

VALUES(13,'唐艺昕','女','1990-4-23','189888888','2');



### 修改 update

### 删除 delete