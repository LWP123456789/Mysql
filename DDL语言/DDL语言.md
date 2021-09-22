## DDL语言

/*

数据定义语言

库和表的管理

*/

### 库的管理

#1、库的创建

语法：CREATE DATABASE [if not exists]库名;

#案例：创建库Books

CREATE DATABASE **IF NOT EXISTS** books;



#2、库的修改

#更改库的字符集

ALTER DATABASE books CHARACTER SET gbk;



#3、库的删除

DROP DATABASE books;

### 表的管理

#1、表的创建

/*

CREATE TABLE 表名{

​	列名 列的类型【(长度) 约束】,

​	列名 列的类型【(长度) 约束】,

​	列名 列的类型【(长度) 约束】,

​	......

​	列名 列的类型【(长度) 约束】,

}

*/

#案例：创建表Book

CREATE TABLE book{

​	id INT,

​	bName,VARCHAR(20),

​	price DOUBLE,

​	author INT,

​	publishData DATETIME

};

DESC book;

#案例：创建表author

CREATE TABLE author{

​	id INT,

​	au_name VARCHAR(20),

​	nation VARCHAR(10)

};

DESC author;

#2、表的修改

#①修改列名

ALTER TABLE book CHANGE COLUMN  publishdata pubDate DATETIME;

#②修改列的类型或约束

ALTER TABLE book MODIFY COLUMN pubdate TIMESTAMP;

#③添加新列

ALTER TABLE author ADD COLUMN annual DOUBLE;

#④删除列

ALTER TABLE author DROP COLUMN IF EXISTS annual;

#⑤修改表名

ALTER TABLE author RENAME TO book_author;

#3、表的删除

DROP TABLE book_author;

SHOW TABLES; #查看当前库的所有表

#4、表的复制

INSERT INTO author VALUES

(1,'村上春树','日本'),

(2,'莫言','中国'),

(3,'冯唐','中国'),

(4,'金庸','中国');



#1、仅仅复制表的结构

CREATE TABLE copy LIKE author;



#2、复制表的结构+数据

CREATE TABLE copy2

SELECT * FROM author;



#3、只复制部分数据

CREATE TABLE copy3

SELECT id,au_name

FROM author

WHERE nation='中国';



#4、仅仅复制某些字段

CREATE TABLE copy4

SELECT id,au_name

FROM author

WHERE 0;





### 常见的数据类型

/*

数值型：

​	整型

​	小数：定点数

​				浮点数

字符型：

​	较短的文本：char、varchar

​	较长的文本：text、blob(较长的二进制数据)

日期型

*/

一、数值型
1、整型
tinyint、smallint、mediumint、int/integer、bigint
1         2        3          4            8

特点：
①都可以设置无符号和有符号，默认无符号，通过unsigned设置无符号(Mysql8.0后默认无符号)
②如果超出了范围，会报out or range异常，插入临界值
③长度可以不指定，默认会有一个长度
长度代表显示的最大宽度，如果不够则左边用0填充，但需要搭配zerofill，并且默认变为无符号整型

2、浮点型
定点数：decimal(M,D)
浮点数:
	float(M,D)   4
	double(M,D)  8

特点：
①M代表整数部位+小数部位的个数，D代表小数部位
②如果超出范围，则报out or range异常，并且插入临界值
③M和D都可以省略，但对于定点数，M默认为10，D默认为0
④如果精度要求较高，则优先考虑使用定点数

二、字符型
char、varchar、binary、varbinary、enum、set、text、blob

char：固定长度的字符，写法为char(M)，最大长度不能超过M，其中M可以省略，默认为1
varchar：可变长度的字符，写法为varchar(M)，最大长度不能超过M，其中M不可以省略

三、日期型
year年
date日期
time时间
datetime 日期+时间          8      
timestamp 日期+时间         4   比较容易受时区、语法模式、版本的影响，更能反映当前时区的真实时间