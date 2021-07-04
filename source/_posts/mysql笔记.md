---
title: mysql笔记
categories: mysql
cover: lab/img/cover1.webp
abbrlink: 27226
date: 2020-12-19 09:57:50
updated:
tags:
keywords:
description:
comments:
toc:
toc_number:
copyright:
copyright_author:
copyright_author_href:
copyright_url:
copyright_info:
mathjax:
katex:
aplayer:
highlight_shrink:
aside:
---
# 今日内容

1. 数据库的基本概念


2. MySQL数据库软件
	1. 安装
	2. 卸载
	3. 配置

3. SQL


## 数据库的基本概念
	1. 数据库的英文单词： DataBase 简称 ： DB
	2. 什么数据库？
		* 用于存储和管理数据的仓库。
	
	3. 数据库的特点：
		1. 持久化存储数据的。其实数据库就是一个文件系统
		2. 方便存储和管理数据
		3. 使用了统一的方式操作数据库 -- SQL


​	
​	4. 常见的数据库软件
​		* 参见《MySQL基础.pdf》


# MySQL数据库软件
	1. 安装
		* 参见《MySQL基础.pdf》
	2. 卸载
		1. 去mysql的安装目录找到my.ini文件
			* 复制 datadir="C:/ProgramData/MySQL/MySQL Server 5.5/Data/"
		2. 卸载MySQL
		3. 删除C:/ProgramData目录下的MySQL文件夹。
		
	3. 配置
		* MySQL服务启动
			1. 手动。
			2. cmd--> services.msc 打开服务的窗口
			3. 使用管理员打开cmd
				* net start mysql : 启动mysql的服务
				* net stop mysql:关闭mysql服务
		* MySQL登录
			1. mysql -uroot -p密码
			2. mysql -hip -uroot -p连接目标的密码
			3. mysql --host=ip --user=root --password=连接目标的密码
		* MySQL退出
			1. exit
			2. quit
	
		* MySQL目录结构
			1. MySQL安装目录：basedir="D:/develop/MySQL/"
				* 配置文件 my.ini
			2. MySQL数据目录：datadir="C:/ProgramData/MySQL/MySQL Server 5.5/Data/"
				* 几个概念
					* 数据库：文件夹
					* 表：文件
					* 数据：数据



# SQL

	1.什么是SQL？
		Structured Query Language：结构化查询语言
		其实就是定义了操作所有关系型数据库的规则。每一种数据库操作的方式存在不一样的地方，称为“方言”。
		
	2.SQL通用语法
		1. SQL 语句可以单行或多行书写，以分号结尾。
		2. 可使用空格和缩进来增强语句的可读性。
		3. MySQL 数据库的 SQL 语句不区分大小写，关键字建议使用大写。
		4. 3 种注释
			* 单行注释: -- 注释内容 或 # 注释内容(mysql 特有) 
			* 多行注释: /* 注释 */
		
	3. SQL分类
		1) DDL(Data Definition Language)数据定义语言
			用来定义数据库对象：数据库，表，列等。关键字：create, drop,alter 等
		2) DML(Data Manipulation Language)数据操作语言
			用来对数据库中表的数据进行增删改。关键字：insert, delete, update 等
		3) DQL(Data Query Language)数据查询语言
			用来查询数据库中表的记录(数据)。关键字：select, where 等
		4) DCL(Data Control Language)数据控制语言(了解)
			用来定义数据库的访问权限和安全级别，及创建用户。关键字：GRANT， REVOKE 等

## DDL:操作数据库、表

	1. 操作数据库：CRUD
		1. C(Create):创建
			* 创建数据库：
				* create database 数据库名称;
			* 创建数据库，判断不存在，再创建：
				* create database if not exists 数据库名称;
			* 创建数据库，并指定字符集
				* create database 数据库名称 character set 字符集名;
	
			* 练习： 创建db4数据库，判断是否存在，并制定字符集为gbk
				* create database if not exists db4 character set gbk;
		2. R(Retrieve)：查询
			* 查询所有数据库的名称:
				* show databases;
			* 查询某个数据库的字符集:查询某个数据库的创建语句
				* show create database 数据库名称;
		3. U(Update):修改
			* 修改数据库的字符集
				* alter database 数据库名称 character set 字符集名称;
		4. D(Delete):删除
			* 删除数据库
				* drop database 数据库名称;
			* 判断数据库存在，存在再删除
				* drop database if exists 数据库名称;
		5. 使用数据库
			* 查询当前正在使用的数据库名称
				* select database();
			* 使用数据库
				* use 数据库名称;


	2. 操作表
		1. C(Create):创建
			1. 语法：
				create table 表名(
					列名1 数据类型1,
					列名2 数据类型2,
					....
					列名n 数据类型n
				);
				* 注意：最后一列，不需要加逗号（,）
				* 数据库类型：
					1. int：整数类型
						* age int,
					2. double:小数类型
						* score double(5,2)
					3. date:日期，只包含年月日，yyyy-MM-dd
					4. datetime:日期，包含年月日时分秒	 yyyy-MM-dd HH:mm:ss
					5. timestamp:时间错类型	包含年月日时分秒	 yyyy-MM-dd HH:mm:ss	
						* 如果将来不给这个字段赋值，或赋值为null，则默认使用当前的系统时间，来自动赋值
	
					6. varchar：字符串
						* name varchar(20):姓名最大20个字符
						* zhangsan 8个字符  张三 2个字符


			* 创建表
				create table student(
					id int,
					name varchar(32),
					age int ,
					score double(4,1),
					birthday date,
					insert_time timestamp
				);
			* 复制表：
				* create table 表名 like 被复制的表名;	  	
		2. R(Retrieve)：查询
			* 查询某个数据库中所有的表名称
				* show tables;
			* 查询表结构
				* desc 表名;
		3. U(Update):修改
			1. 修改表名
				alter table 表名 rename to 新的表名;
			2. 修改表的字符集
				alter table 表名 character set 字符集名称;
			3. 添加一列
				alter table 表名 add 列名 数据类型;
			4. 修改列名称 类型
				alter table 表名 change 列名 新列别 新数据类型;
				alter table 表名 modify 列名 新数据类型;
			5. 删除列
				alter table 表名 drop 列名;
		4. D(Delete):删除
			* drop table 表名;
			* drop table  if exists 表名 ;

* 客户端图形化工具：SQLYog

## DML：增删改表中数据

	1. 添加数据：
		* 语法：
			* insert into 表名(列名1,列名2,...列名n) values(值1,值2,...值n);
		* 注意：
			1. 列名和值要一一对应。
			2. 如果表名后，不定义列名，则默认给所有列添加值
				insert into 表名 values(值1,值2,...值n);
			3. 除了数字类型，其他类型需要使用引号(单双都可以)引起来
	2. 删除数据：
		* 语法：
			* delete from 表名 [where 条件]
		* 注意：
			1. 如果不加条件，则删除表中所有记录。
			2. 如果要删除所有记录
				1. delete from 表名; -- 不推荐使用。有多少条记录就会执行多少次删除操作
				2. TRUNCATE TABLE 表名; -- 推荐使用，效率更高 先删除表，然后再创建一张一样的表。
	3. 修改数据：
		* 语法：
			* update 表名 set 列名1 = 值1, 列名2 = 值2,... [where 条件];
	
		* 注意：
			1. 如果不加任何条件，则会将表中所有记录全部修改。



## DQL：查询表中的记录
	* select * from 表名;
	
	1. 语法：
		select
			字段列表
		from
			表名列表
		where
			条件列表
		group by
			分组字段
		having
			分组之后的条件
		order by
			排序
		limit
			分页限定


	2. 基础查询
		1. 多个字段的查询
			select 字段名1，字段名2... from 表名；
			* 注意：
				* 如果查询所有字段，则可以使用*来替代字段列表。
		2. 去除重复：
			* distinct
		3. 计算列
			* 一般可以使用四则运算计算一些列的值。（一般只会进行数值型的计算）
			* ifnull(表达式1,表达式2)：null参与的运算，计算结果都为null
				* 表达式1：哪个字段需要判断是否为null
				* 如果该字段为null后的替换值。
		4. 起别名：
			* as：as也可以省略


	3. 条件查询
		1. where子句后跟条件
		2. 运算符
			* > 、< 、<= 、>= 、= 、<>
			* BETWEEN...AND  
			* IN( 集合) 
			* LIKE：模糊查询
				* 占位符：
					* _:单个任意字符
					* %：多个任意字符
			* IS NULL  
			* and  或 &&
			* or  或 || 
			* not  或 !
			
				-- 查询年龄大于20岁
	
				SELECT * FROM student WHERE age > 20;
				
				SELECT * FROM student WHERE age >= 20;
				
				-- 查询年龄等于20岁
				SELECT * FROM student WHERE age = 20;
				
				-- 查询年龄不等于20岁
				SELECT * FROM student WHERE age != 20;
				SELECT * FROM student WHERE age <> 20;
				
				-- 查询年龄大于等于20 小于等于30
				
				SELECT * FROM student WHERE age >= 20 &&  age <=30;
				SELECT * FROM student WHERE age >= 20 AND  age <=30;
				SELECT * FROM student WHERE age BETWEEN 20 AND 30;
				
				-- 查询年龄22岁，18岁，25岁的信息
				SELECT * FROM student WHERE age = 22 OR age = 18 OR age = 25
				SELECT * FROM student WHERE age IN (22,18,25);
				
				-- 查询英语成绩为null
				SELECT * FROM student WHERE english = NULL; -- 不对的。null值不能使用 = （!=） 判断
				
				SELECT * FROM student WHERE english IS NULL;
				
				-- 查询英语成绩不为null
				SELECT * FROM student WHERE english  IS NOT NULL;



				-- 查询姓马的有哪些？ like
				SELECT * FROM student WHERE NAME LIKE '马%';
				-- 查询姓名第二个字是化的人
				
				SELECT * FROM student WHERE NAME LIKE "_化%";
				
				-- 查询姓名是3个字的人
				SELECT * FROM student WHERE NAME LIKE '___';


​				
​				-- 查询姓名中包含德的人
​				SELECT * FROM student WHERE NAME LIKE '%德%';



# 今日内容

	1. DQL:查询语句
		1. 排序查询
		2. 聚合函数
		3. 分组查询
		4. 分页查询
	
	2. 约束
	3. 多表之间的关系
	4. 范式
	5. 数据库的备份和还原

# DQL:查询语句
	1. 排序查询
		* 语法：order by 子句
			* order by 排序字段1 排序方式1 ，  排序字段2 排序方式2...
	
		* 排序方式：
			* ASC：升序，默认的。
			* DESC：降序。
	
		* 注意：
			* 如果有多个排序条件，则当前边的条件值一样时，才会判断第二条件。


	2. 聚合函数：将一列数据作为一个整体，进行纵向的计算。
		1. count：计算个数
			1. 一般选择非空的列：主键
			2. count(*)
		2. max：计算最大值
		3. min：计算最小值
		4. sum：计算和
		5. avg：计算平均值


		* 注意：聚合函数的计算，排除null值。
			解决方案：
				1. 选择不包含非空的列进行计算
				2. IFNULL函数
	
	3. 分组查询:
		1. 语法：group by 分组字段；
		2. 注意：
			1. 分组之后查询的字段：分组字段、聚合函数
			2. where 和 having 的区别？
				1. where 在分组之前进行限定，如果不满足条件，则不参与分组。having在分组之后进行限定，如果不满足结果，则不会被查询出来
				2. where 后不可以跟聚合函数，having可以进行聚合函数的判断。
	
			-- 按照性别分组。分别查询男、女同学的平均分
	
			SELECT sex , AVG(math) FROM student GROUP BY sex;
			
			-- 按照性别分组。分别查询男、女同学的平均分,人数
			
			SELECT sex , AVG(math),COUNT(id) FROM student GROUP BY sex;
			
			--  按照性别分组。分别查询男、女同学的平均分,人数 要求：分数低于70分的人，不参与分组
			SELECT sex , AVG(math),COUNT(id) FROM student WHERE math > 70 GROUP BY sex;
			
			--  按照性别分组。分别查询男、女同学的平均分,人数 要求：分数低于70分的人，不参与分组,分组之后。人数要大于2个人
			SELECT sex , AVG(math),COUNT(id) FROM student WHERE math > 70 GROUP BY sex HAVING COUNT(id) > 2;
			
			SELECT sex , AVG(math),COUNT(id) 人数 FROM student WHERE math > 70 GROUP BY sex HAVING 人数 > 2;


​			
​	4. 分页查询
​		1. 语法：limit 开始的索引,每页查询的条数;
​		2. 公式：开始的索引 = （当前的页码 - 1） * 每页显示的条数
​			-- 每页显示3条记录 
​	
​			SELECT * FROM student LIMIT 0,3; -- 第1页
​			
​			SELECT * FROM student LIMIT 3,3; -- 第2页
​			
			SELECT * FROM student LIMIT 6,3; -- 第3页
	
		3. limit 是一个MySQL"方言"


## 约束
	* 概念： 对表中的数据进行限定，保证数据的正确性、有效性和完整性。	
	* 分类：
		1. 主键约束：primary key
		2. 非空约束：not null
		3. 唯一约束：unique
		4. 外键约束：foreign key
	
	* 非空约束：not null，某一列的值不能为null
		1. 创建表时添加约束
			CREATE TABLE stu(
				id INT,
				NAME VARCHAR(20) NOT NULL -- name为非空
			);
		2. 创建表完后，添加非空约束
			ALTER TABLE stu MODIFY NAME VARCHAR(20) NOT NULL;
	
		3. 删除name的非空约束
			ALTER TABLE stu MODIFY NAME VARCHAR(20);
	
	* 唯一约束：unique，某一列的值不能重复
		1. 注意：
			* 唯一约束可以有NULL值，但是只能有一条记录为null
		2. 在创建表时，添加唯一约束
			CREATE TABLE stu(
				id INT,
				phone_number VARCHAR(20) UNIQUE -- 手机号
			);
		3. 删除唯一约束
			ALTER TABLE stu DROP INDEX phone_number;
		4. 在表创建完后，添加唯一约束
			ALTER TABLE stu MODIFY phone_number VARCHAR(20) UNIQUE;
	
	* 主键约束：primary key。
		1. 注意：
			1. 含义：非空且唯一
			2. 一张表只能有一个字段为主键
			3. 主键就是表中记录的唯一标识
	
		2. 在创建表时，添加主键约束
			create table stu(
				id int primary key,-- 给id添加主键约束
				name varchar(20)
			);
	
		3. 删除主键
			-- 错误 alter table stu modify id int ;
			ALTER TABLE stu DROP PRIMARY KEY;
	
		4. 创建完表后，添加主键
			ALTER TABLE stu MODIFY id INT PRIMARY KEY;
	
		5. 自动增长：
			1.  概念：如果某一列是数值类型的，使用 auto_increment 可以来完成值得自动增长
	
			2. 在创建表时，添加主键约束，并且完成主键自增长
			create table stu(
				id int primary key auto_increment,-- 给id添加主键约束
				name varchar(20)
			);


​			
​			3. 删除自动增长
​			ALTER TABLE stu MODIFY id INT;
​			4. 添加自动增长
​			ALTER TABLE stu MODIFY id INT AUTO_INCREMENT;


	* 外键约束：foreign key,让表于表产生关系，从而保证数据的正确性。
		1. 在创建表时，可以添加外键
			* 语法：
				create table 表名(
					....
					外键列
					constraint 外键名称 foreign key (外键列名称) references 主表名称(主表列名称)
				);
	
		2. 删除外键
			ALTER TABLE 表名 DROP FOREIGN KEY 外键名称;
	
		3. 创建表之后，添加外键
			ALTER TABLE 表名 ADD CONSTRAINT 外键名称 FOREIGN KEY (外键字段名称) REFERENCES 主表名称(主表列名称);


​		
​		4. 级联操作
​			1. 添加级联操作
​				语法：ALTER TABLE 表名 ADD CONSTRAINT 外键名称 
​						FOREIGN KEY (外键字段名称) REFERENCES 主表名称(主表列名称) ON UPDATE CASCADE ON DELETE CASCADE  ;
​			2. 分类：
​				1. 级联更新：ON UPDATE CASCADE 
​				2. 级联删除：ON DELETE CASCADE 


## 数据库的设计

	1. 多表之间的关系
		1. 分类：
			1. 一对一(了解)：
				* 如：人和身份证
				* 分析：一个人只有一个身份证，一个身份证只能对应一个人
			2. 一对多(多对一)：
				* 如：部门和员工
				* 分析：一个部门有多个员工，一个员工只能对应一个部门
			3. 多对多：
				* 如：学生和课程
				* 分析：一个学生可以选择很多门课程，一个课程也可以被很多学生选择
		2. 实现关系：
			1. 一对多(多对一)：
				* 如：部门和员工
				* 实现方式：在多的一方建立外键，指向一的一方的主键。
			2. 多对多：
				* 如：学生和课程
				* 实现方式：多对多关系实现需要借助第三张中间表。中间表至少包含两个字段，这两个字段作为第三张表的外键，分别指向两张表的主键
			3. 一对一(了解)：
				* 如：人和身份证
				* 实现方式：一对一关系实现，可以在任意一方添加唯一外键指向另一方的主键。
	
		3. 案例
			-- 创建旅游线路分类表 tab_category
			-- cid 旅游线路分类主键，自动增长
			-- cname 旅游线路分类名称非空，唯一，字符串 100
			CREATE TABLE tab_category (
				cid INT PRIMARY KEY AUTO_INCREMENT,
				cname VARCHAR(100) NOT NULL UNIQUE
			);
			
			-- 创建旅游线路表 tab_route
			/*
			rid 旅游线路主键，自动增长
			rname 旅游线路名称非空，唯一，字符串 100
			price 价格
			rdate 上架时间，日期类型
			cid 外键，所属分类
			*/
			CREATE TABLE tab_route(
				rid INT PRIMARY KEY AUTO_INCREMENT,
				rname VARCHAR(100) NOT NULL UNIQUE,
				price DOUBLE,
				rdate DATE,
				cid INT,
				FOREIGN KEY (cid) REFERENCES tab_category(cid)
			);
			
			/*创建用户表 tab_user
			uid 用户主键，自增长
			username 用户名长度 100，唯一，非空
			password 密码长度 30，非空
			name 真实姓名长度 100
			birthday 生日
			sex 性别，定长字符串 1
			telephone 手机号，字符串 11
			email 邮箱，字符串长度 100
			*/
			CREATE TABLE tab_user (
				uid INT PRIMARY KEY AUTO_INCREMENT,
				username VARCHAR(100) UNIQUE NOT NULL,
				PASSWORD VARCHAR(30) NOT NULL,
				NAME VARCHAR(100),
				birthday DATE,
				sex CHAR(1) DEFAULT '男',
				telephone VARCHAR(11),
				email VARCHAR(100)
			);
			
			/*
			创建收藏表 tab_favorite
			rid 旅游线路 id，外键
			date 收藏时间
			uid 用户 id，外键
			rid 和 uid 不能重复，设置复合主键，同一个用户不能收藏同一个线路两次
			*/
			CREATE TABLE tab_favorite (
				rid INT, -- 线路id
				DATE DATETIME,
				uid INT, -- 用户id
				-- 创建复合主键
				PRIMARY KEY(rid,uid), -- 联合主键
				FOREIGN KEY (rid) REFERENCES tab_route(rid),
				FOREIGN KEY(uid) REFERENCES tab_user(uid)
			);


​		
​	2. 数据库设计的范式
​		* 概念：设计数据库时，需要遵循的一些规范。要遵循后边的范式要求，必须先遵循前边的所有范式要求
​	
​			设计关系数据库时，遵从不同的规范要求，设计出合理的关系型数据库，这些不同的规范要求被称为不同的范式，各种范式呈递次规范，越高的范式数据库冗余越小。
​			目前关系数据库有六种范式：第一范式（1NF）、第二范式（2NF）、第三范式（3NF）、巴斯-科德范式（BCNF）、第四范式(4NF）和第五范式（5NF，又称完美范式）。
​	
​		* 分类：
​			1. 第一范式（1NF）：每一列都是不可分割的原子数据项
​			2. 第二范式（2NF）：在1NF的基础上，非码属性必须完全依赖于码（在1NF基础上消除非主属性对主码的部分函数依赖）
​				* 几个概念：
​					1. 函数依赖：A-->B,如果通过A属性(属性组)的值，可以确定唯一B属性的值。则称B依赖于A
​						例如：学号-->姓名。  （学号，课程名称） --> 分数
​					2. 完全函数依赖：A-->B， 如果A是一个属性组，则B属性值得确定需要依赖于A属性组中所有的属性值。
​						例如：（学号，课程名称） --> 分数
​					3. 部分函数依赖：A-->B， 如果A是一个属性组，则B属性值得确定只需要依赖于A属性组中某一些值即可。
​						例如：（学号，课程名称） -- > 姓名
​					4. 传递函数依赖：A-->B, B -- >C . 如果通过A属性(属性组)的值，可以确定唯一B属性的值，在通过B属性（属性组）的值可以确定唯一C属性的值，则称 C 传递函数依赖于A
​						例如：学号-->系名，系名-->系主任
​					5. 码：如果在一张表中，一个属性或属性组，被其他所有属性所完全依赖，则称这个属性(属性组)为该表的码
​						例如：该表中码为：（学号，课程名称）
​						* 主属性：码属性组中的所有属性
​						* 非主属性：除过码属性组的属性
​						
			3. 第三范式（3NF）：在2NF基础上，任何非主属性不依赖于其它非主属性（在2NF基础上消除传递依赖）


## 数据库的备份和还原

	1. 命令行：
		* 语法：
			* 备份： mysqldump -u用户名 -p密码 数据库名称 > 保存的路径
			* 还原：
				1. 登录数据库
				2. 创建数据库
				3. 使用数据库
				4. 执行文件。source 文件路径
	2. 图形化工具：

# 今日内容

	1. 多表查询
	
	2. 事务
	
	3. DCL


## 多表查询：
	* 查询语法：
		select
			列名列表
		from
			表名列表
		where....
	* 准备sql
		# 创建部门表
		CREATE TABLE dept(
			id INT PRIMARY KEY AUTO_INCREMENT,
			NAME VARCHAR(20)
		);
		INSERT INTO dept (NAME) VALUES ('开发部'),('市场部'),('财务部');
		# 创建员工表
		CREATE TABLE emp (
			id INT PRIMARY KEY AUTO_INCREMENT,
			NAME VARCHAR(10),
			gender CHAR(1), -- 性别
			salary DOUBLE, -- 工资
			join_date DATE, -- 入职日期
			dept_id INT,
			FOREIGN KEY (dept_id) REFERENCES dept(id) -- 外键，关联部门表(部门表的主键)
		);
		INSERT INTO emp(NAME,gender,salary,join_date,dept_id) VALUES('孙悟空','男',7200,'2013-02-24',1);
		INSERT INTO emp(NAME,gender,salary,join_date,dept_id) VALUES('猪八戒','男',3600,'2010-12-02',2);
		INSERT INTO emp(NAME,gender,salary,join_date,dept_id) VALUES('唐僧','男',9000,'2008-08-08',2);
		INSERT INTO emp(NAME,gender,salary,join_date,dept_id) VALUES('白骨精','女',5000,'2015-10-07',3);
		INSERT INTO emp(NAME,gender,salary,join_date,dept_id) VALUES('蜘蛛精','女',4500,'2011-03-14',1);
	* 笛卡尔积：
		* 有两个集合A,B .取这两个集合的所有组成情况。
		* 要完成多表查询，需要消除无用的数据
	* 多表查询的分类：
		1. 内连接查询：
			1. 隐式内连接：使用where条件消除无用数据
				* 例子：
				-- 查询所有员工信息和对应的部门信息
	
				SELECT * FROM emp,dept WHERE emp.`dept_id` = dept.`id`;
				
				-- 查询员工表的名称，性别。部门表的名称
				SELECT emp.name,emp.gender,dept.name FROM emp,dept WHERE emp.`dept_id` = dept.`id`;
				
				SELECT 
					t1.name, -- 员工表的姓名
					t1.gender,-- 员工表的性别
					t2.name -- 部门表的名称
				FROM
					emp t1,
					dept t2
				WHERE 
					t1.`dept_id` = t2.`id`;


​	
​			2. 显式内连接：
​				* 语法： select 字段列表 from 表名1 [inner] join 表名2 on 条件
​				* 例如：
​					* SELECT * FROM emp INNER JOIN dept ON emp.`dept_id` = dept.`id`;	
​					* SELECT * FROM emp JOIN dept ON emp.`dept_id` = dept.`id`;	
​	
​			3. 内连接查询：
​				1. 从哪些表中查询数据
​				2. 条件是什么
​				3. 查询哪些字段
​		2. 外链接查询：
​			1. 左外连接：
​				* 语法：select 字段列表 from 表1 left [outer] join 表2 on 条件；
​				* 查询的是左表所有数据以及其交集部分。
​				* 例子：
​					-- 查询所有员工信息，如果员工有部门，则查询部门名称，没有部门，则不显示部门名称
​					SELECT 	t1.*,t2.`name` FROM emp t1 LEFT JOIN dept t2 ON t1.`dept_id` = t2.`id`;
​			2. 右外连接：
​				* 语法：select 字段列表 from 表1 right [outer] join 表2 on 条件；
​				* 查询的是右表所有数据以及其交集部分。
​				* 例子：
​					SELECT 	* FROM dept t2 RIGHT JOIN emp t1 ON t1.`dept_id` = t2.`id`;
​		3. 子查询：
​			* 概念：查询中嵌套查询，称嵌套查询为子查询。
​				-- 查询工资最高的员工信息
​				-- 1 查询最高的工资是多少 9000
​				SELECT MAX(salary) FROM emp;
​				
​				-- 2 查询员工信息，并且工资等于9000的
​				SELECT * FROM emp WHERE emp.`salary` = 9000;
​				
				-- 一条sql就完成这个操作。子查询
				SELECT * FROM emp WHERE emp.`salary` = (SELECT MAX(salary) FROM emp);
	
			* 子查询不同情况
				1. 子查询的结果是单行单列的：
					* 子查询可以作为条件，使用运算符去判断。 运算符： > >= < <= =
					* 
					-- 查询员工工资小于平均工资的人
					SELECT * FROM emp WHERE emp.salary < (SELECT AVG(salary) FROM emp);
				2. 子查询的结果是多行单列的：
					* 子查询可以作为条件，使用运算符in来判断
					-- 查询'财务部'和'市场部'所有的员工信息
					SELECT id FROM dept WHERE NAME = '财务部' OR NAME = '市场部';
					SELECT * FROM emp WHERE dept_id = 3 OR dept_id = 2;
					-- 子查询
					SELECT * FROM emp WHERE dept_id IN (SELECT id FROM dept WHERE NAME = '财务部' OR NAME = '市场部');
	
				3. 子查询的结果是多行多列的：
					* 子查询可以作为一张虚拟表参与查询
					-- 查询员工入职日期是2011-11-11日之后的员工信息和部门信息
					-- 子查询
					SELECT * FROM dept t1 ,(SELECT * FROM emp WHERE emp.`join_date` > '2011-11-11') t2
					WHERE t1.id = t2.dept_id;
					
					-- 普通内连接
					SELECT * FROM emp t1,dept t2 WHERE t1.`dept_id` = t2.`id` AND t1.`join_date` >  '2011-11-11'
	
		* 多表查询练习
	
				-- 部门表
				CREATE TABLE dept (
				  id INT PRIMARY KEY PRIMARY KEY, -- 部门id
				  dname VARCHAR(50), -- 部门名称
				  loc VARCHAR(50) -- 部门所在地
				);
				
				-- 添加4个部门
				INSERT INTO dept(id,dname,loc) VALUES 
				(10,'教研部','北京'),
				(20,'学工部','上海'),
				(30,'销售部','广州'),
				(40,'财务部','深圳');


​				
​				
​				-- 职务表，职务名称，职务描述
​				CREATE TABLE job (
​				  id INT PRIMARY KEY,
​				  jname VARCHAR(20),
​				  description VARCHAR(50)
​				);
​				
​				-- 添加4个职务
​				INSERT INTO job (id, jname, description) VALUES
​				(1, '董事长', '管理整个公司，接单'),
​				(2, '经理', '管理部门员工'),
​				(3, '销售员', '向客人推销产品'),
​				(4, '文员', '使用办公软件');


​				
​				
​				-- 员工表
​				CREATE TABLE emp (
​				  id INT PRIMARY KEY, -- 员工id
​				  ename VARCHAR(50), -- 员工姓名
​				  job_id INT, -- 职务id
​				  mgr INT , -- 上级领导
​				  joindate DATE, -- 入职日期
​				  salary DECIMAL(7,2), -- 工资
​				  bonus DECIMAL(7,2), -- 奖金
​				  dept_id INT, -- 所在部门编号
​				  CONSTRAINT emp_jobid_ref_job_id_fk FOREIGN KEY (job_id) REFERENCES job (id),
​				  CONSTRAINT emp_deptid_ref_dept_id_fk FOREIGN KEY (dept_id) REFERENCES dept (id)
​				);
​				
​				-- 添加员工
​				INSERT INTO emp(id,ename,job_id,mgr,joindate,salary,bonus,dept_id) VALUES 
​				(1001,'孙悟空',4,1004,'2000-12-17','8000.00',NULL,20),
​				(1002,'卢俊义',3,1006,'2001-02-20','16000.00','3000.00',30),
​				(1003,'林冲',3,1006,'2001-02-22','12500.00','5000.00',30),
​				(1004,'唐僧',2,1009,'2001-04-02','29750.00',NULL,20),
​				(1005,'李逵',4,1006,'2001-09-28','12500.00','14000.00',30),
​				(1006,'宋江',2,1009,'2001-05-01','28500.00',NULL,30),
​				(1007,'刘备',2,1009,'2001-09-01','24500.00',NULL,10),
​				(1008,'猪八戒',4,1004,'2007-04-19','30000.00',NULL,20),
​				(1009,'罗贯中',1,NULL,'2001-11-17','50000.00',NULL,10),
​				(1010,'吴用',3,1006,'2001-09-08','15000.00','0.00',30),
​				(1011,'沙僧',4,1004,'2007-05-23','11000.00',NULL,20),
​				(1012,'李逵',4,1006,'2001-12-03','9500.00',NULL,30),
​				(1013,'小白龙',4,1004,'2001-12-03','30000.00',NULL,20),
​				(1014,'关羽',4,1007,'2002-01-23','13000.00',NULL,10);


​				
​				
​				-- 工资等级表
​				CREATE TABLE salarygrade (
​				  grade INT PRIMARY KEY,   -- 级别
​				  losalary INT,  -- 最低工资
​				  hisalary INT -- 最高工资
​				);
​				
​				-- 添加5个工资等级
​				INSERT INTO salarygrade(grade,losalary,hisalary) VALUES 
​				(1,7000,12000),
​				(2,12010,14000),
​				(3,14010,20000),
​				(4,20010,30000),
​				(5,30010,99990);
​				
​				-- 需求：
​				
				-- 1.查询所有员工信息。查询员工编号，员工姓名，工资，职务名称，职务描述
				/*
					分析：
						1.员工编号，员工姓名，工资，需要查询emp表  职务名称，职务描述 需要查询job表
						2.查询条件 emp.job_id = job.id
				
				*/
				SELECT 
					t1.`id`, -- 员工编号
					t1.`ename`, -- 员工姓名
					t1.`salary`,-- 工资
					t2.`jname`, -- 职务名称
					t2.`description` -- 职务描述
				FROM 
					emp t1, job t2
				WHERE 
					t1.`job_id` = t2.`id`;


​				
​				
​				-- 2.查询员工编号，员工姓名，工资，职务名称，职务描述，部门名称，部门位置
​				/*
​					分析：
​						1. 员工编号，员工姓名，工资 emp  职务名称，职务描述 job  部门名称，部门位置 dept
​						2. 条件： emp.job_id = job.id and emp.dept_id = dept.id
​				*/
​				
​				SELECT 
​					t1.`id`, -- 员工编号
​					t1.`ename`, -- 员工姓名
​					t1.`salary`,-- 工资
​					t2.`jname`, -- 职务名称
​					t2.`description`, -- 职务描述
​					t3.`dname`, -- 部门名称
​					t3.`loc` -- 部门位置
​				FROM 
​					emp t1, job t2,dept t3
​				WHERE 
​					t1.`job_id` = t2.`id` AND t1.`dept_id` = t3.`id`;
​				   
​				-- 3.查询员工姓名，工资，工资等级
​				/*
​					分析：
​						1.员工姓名，工资 emp  工资等级 salarygrade
​						2.条件 emp.salary >= salarygrade.losalary and emp.salary <= salarygrade.hisalary
​							emp.salary BETWEEN salarygrade.losalary and salarygrade.hisalary
​				*/
​				SELECT 
​					t1.ename ,
​					t1.`salary`,
​					t2.*
​				FROM emp t1, salarygrade t2
​				WHERE t1.`salary` BETWEEN t2.`losalary` AND t2.`hisalary`;


​				
​				
​				-- 4.查询员工姓名，工资，职务名称，职务描述，部门名称，部门位置，工资等级
​				/*
​					分析：
​						1. 员工姓名，工资 emp ， 职务名称，职务描述 job 部门名称，部门位置，dept  工资等级 salarygrade
​						2. 条件： emp.job_id = job.id and emp.dept_id = dept.id and emp.salary BETWEEN salarygrade.losalary and salarygrade.hisalary
​							
​				*/
​				SELECT 
​					t1.`ename`,
​					t1.`salary`,
​					t2.`jname`,
​					t2.`description`,
​					t3.`dname`,
​					t3.`loc`,
​					t4.`grade`
​				FROM 
​					emp t1,job t2,dept t3,salarygrade t4
​				WHERE 
​					t1.`job_id` = t2.`id` 
​					AND t1.`dept_id` = t3.`id`
​					AND t1.`salary` BETWEEN t4.`losalary` AND t4.`hisalary`;


​				
​				
​				-- 5.查询出部门编号、部门名称、部门位置、部门人数
​				
​				/*
​					分析：
​						1.部门编号、部门名称、部门位置 dept 表。 部门人数 emp表
​						2.使用分组查询。按照emp.dept_id完成分组，查询count(id)
​						3.使用子查询将第2步的查询结果和dept表进行关联查询
​						
​				*/
​				SELECT 
​					t1.`id`,t1.`dname`,t1.`loc` , t2.total
​				FROM 
​					dept t1,
​					(SELECT
​						dept_id,COUNT(id) total
​					FROM 
​						emp
​					GROUP BY dept_id) t2
​				WHERE t1.`id` = t2.dept_id;


​				
​				-- 6.查询所有员工的姓名及其直接上级的姓名,没有领导的员工也需要查询
​				
​				/*
​					分析：
​						1.姓名 emp， 直接上级的姓名 emp
​							* emp表的id 和 mgr 是自关联
​						2.条件 emp.id = emp.mgr
​						3.查询左表的所有数据，和 交集数据
​							* 使用左外连接查询
​					
​				*/
​				/*
​				select
​					t1.ename,
​					t1.mgr,
​					t2.`id`,
​					t2.ename
​				from emp t1, emp t2
​				where t1.mgr = t2.`id`;
​				
				*/
				
				SELECT 
					t1.ename,
					t1.mgr,
					t2.`id`,
					t2.`ename`
				FROM emp t1
				LEFT JOIN emp t2
				ON t1.`mgr` = t2.`id`;


## 事务

	1. 事务的基本介绍
		1. 概念：
			*  如果一个包含多个步骤的业务操作，被事务管理，那么这些操作要么同时成功，要么同时失败。
			
		2. 操作：
			1. 开启事务： start transaction;
			2. 回滚：rollback;
			3. 提交：commit;
		3. 例子：
			CREATE TABLE account (
				id INT PRIMARY KEY AUTO_INCREMENT,
				NAME VARCHAR(10),
				balance DOUBLE
			);
			-- 添加数据
			INSERT INTO account (NAME, balance) VALUES ('zhangsan', 1000), ('lisi', 1000);


​			
​			SELECT * FROM account;
​			UPDATE account SET balance = 1000;
​			-- 张三给李四转账 500 元
​			
​			-- 0. 开启事务
​			START TRANSACTION;
​			-- 1. 张三账户 -500
​			
​			UPDATE account SET balance = balance - 500 WHERE NAME = 'zhangsan';
​			-- 2. 李四账户 +500
​			-- 出错了...
​			UPDATE account SET balance = balance + 500 WHERE NAME = 'lisi';
​			
			-- 发现执行没有问题，提交事务
			COMMIT;
			
			-- 发现出问题了，回滚事务
			ROLLBACK;
		4. MySQL数据库中事务默认自动提交
			
			* 事务提交的两种方式：
				* 自动提交：
					* mysql就是自动提交的
					* 一条DML(增删改)语句会自动提交一次事务。
				* 手动提交：
					* Oracle 数据库默认是手动提交事务
					* 需要先开启事务，再提交
			* 修改事务的默认提交方式：
				* 查看事务的默认提交方式：SELECT @@autocommit; -- 1 代表自动提交  0 代表手动提交
				* 修改默认提交方式： set @@autocommit = 0;


	2. 事务的四大特征：
		1. 原子性：是不可分割的最小操作单位，要么同时成功，要么同时失败。
		2. 持久性：当事务提交或回滚后，数据库会持久化的保存数据。
		3. 隔离性：多个事务之间。相互独立。
		4. 一致性：事务操作前后，数据总量不变
	3. 事务的隔离级别（了解）
		* 概念：多个事务之间隔离的，相互独立的。但是如果多个事务操作同一批数据，则会引发一些问题，设置不同的隔离级别就可以解决这些问题。
		* 存在问题：
			1. 脏读：一个事务，读取到另一个事务中没有提交的数据
			2. 不可重复读(虚读)：在同一个事务中，两次读取到的数据不一样。
			3. 幻读：一个事务操作(DML)数据表中所有记录，另一个事务添加了一条数据，则第一个事务查询不到自己的修改。
		* 隔离级别：
			1. read uncommitted：读未提交
				* 产生的问题：脏读、不可重复读、幻读
			2. read committed：读已提交 （Oracle）
				* 产生的问题：不可重复读、幻读
			3. repeatable read：可重复读 （MySQL默认）
				* 产生的问题：幻读
			4. serializable：串行化
				* 可以解决所有的问题
	
			* 注意：隔离级别从小到大安全性越来越高，但是效率越来越低
			* 数据库查询隔离级别：
				* select @@tx_isolation;
			* 数据库设置隔离级别：
				* set global transaction isolation level  级别字符串;
	
		* 演示：
			set global transaction isolation level read uncommitted;
			start transaction;
			-- 转账操作
			update account set balance = balance - 500 where id = 1;
			update account set balance = balance + 500 where id = 2;



## DCL：
	* SQL分类：
		1. DDL：操作数据库和表
		2. DML：增删改表中数据
		3. DQL：查询表中数据
		4. DCL：管理用户，授权
	
	* DBA：数据库管理员
	
	* DCL：管理用户，授权
		1. 管理用户
			1. 添加用户：
				* 语法：CREATE USER '用户名'@'主机名' IDENTIFIED BY '密码';
			2. 删除用户：
				* 语法：DROP USER '用户名'@'主机名';
			3. 修改用户密码：
				
				UPDATE USER SET PASSWORD = PASSWORD('新密码') WHERE USER = '用户名';
				UPDATE USER SET PASSWORD = PASSWORD('abc') WHERE USER = 'lisi';
				
				SET PASSWORD FOR '用户名'@'主机名' = PASSWORD('新密码');
				SET PASSWORD FOR 'root'@'localhost' = PASSWORD('123');
	
				* mysql中忘记了root用户的密码？
					1. cmd -- > net stop mysql 停止mysql服务
						* 需要管理员运行该cmd
	
					2. 使用无验证方式启动mysql服务： mysqld --skip-grant-tables
					3. 打开新的cmd窗口,直接输入mysql命令，敲回车。就可以登录成功
					4. use mysql;
					5. update user set password = password('你的新密码') where user = 'root';
					6. 关闭两个窗口
					7. 打开任务管理器，手动结束mysqld.exe 的进程
					8. 启动mysql服务
					9. 使用新密码登录。
			4. 查询用户：
				-- 1. 切换到mysql数据库
				USE myql;
				-- 2. 查询user表
				SELECT * FROM USER;
				
				* 通配符： % 表示可以在任意主机使用用户登录数据库
	
		2. 权限管理：
			1. 查询权限：
				-- 查询权限
				SHOW GRANTS FOR '用户名'@'主机名';
				SHOW GRANTS FOR 'lisi'@'%';
	
			2. 授予权限：
				-- 授予权限
				grant 权限列表 on 数据库名.表名 to '用户名'@'主机名';
				-- 给张三用户授予所有权限，在任意数据库任意表上
				
				GRANT ALL ON *.* TO 'zhangsan'@'localhost';
			3. 撤销权限：
				-- 撤销权限：
				revoke 权限列表 on 数据库名.表名 from '用户名'@'主机名';
				REVOKE UPDATE ON db3.`account` FROM 'lisi'@'%';


​				
# 今日内容

	1. JDBC基本概念
	2. 快速入门
	3. 对JDBC中各个接口和类详解


## JDBC：
	1. 概念：Java DataBase Connectivity  Java 数据库连接， Java语言操作数据库
		* JDBC本质：其实是官方（sun公司）定义的一套操作所有关系型数据库的规则，即接口。各个数据库厂商去实现这套接口，提供数据库驱动jar包。我们可以使用这套接口（JDBC）编程，真正执行的代码是驱动jar包中的实现类。
	
	2. 快速入门：
		* 步骤：
			1. 导入驱动jar包 mysql-connector-java-5.1.37-bin.jar
				1.复制mysql-connector-java-5.1.37-bin.jar到项目的libs目录下
				2.右键-->Add As Library
			2. 注册驱动
			3. 获取数据库连接对象 Connection
			4. 定义sql
			5. 获取执行sql语句的对象 Statement
			6. 执行sql，接受返回结果
			7. 处理结果
			8. 释放资源
	
		* 代码实现：
		  	//1. 导入驱动jar包
	        //2.注册驱动
	        Class.forName("com.mysql.jdbc.Driver");
	        //3.获取数据库连接对象
	        Connection conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/db3", "root", "root");
	        //4.定义sql语句
	        String sql = "update account set balance = 500 where id = 1";
	        //5.获取执行sql的对象 Statement
	        Statement stmt = conn.createStatement();
	        //6.执行sql
	        int count = stmt.executeUpdate(sql);
	        //7.处理结果
	        System.out.println(count);
	        //8.释放资源
	        stmt.close();
	        conn.close();
	
	3. 详解各个对象：
		1. DriverManager：驱动管理对象
			* 功能：
				1. 注册驱动：告诉程序该使用哪一个数据库驱动jar
					static void registerDriver(Driver driver) :注册与给定的驱动程序 DriverManager 。 
					写代码使用：  Class.forName("com.mysql.jdbc.Driver");
					通过查看源码发现：在com.mysql.jdbc.Driver类中存在静态代码块
					 static {
					        try {
					            java.sql.DriverManager.registerDriver(new Driver());
					        } catch (SQLException E) {
					            throw new RuntimeException("Can't register driver!");
					        }
						}
	
					注意：mysql5之后的驱动jar包可以省略注册驱动的步骤。
				2. 获取数据库连接：
					* 方法：static Connection getConnection(String url, String user, String password) 
					* 参数：
						* url：指定连接的路径
							* 语法：jdbc:mysql://ip地址(域名):端口号/数据库名称
							* 例子：jdbc:mysql://localhost:3306/db3
							* 细节：如果连接的是本机mysql服务器，并且mysql服务默认端口是3306，则url可以简写为：jdbc:mysql:///数据库名称
						* user：用户名
						* password：密码 
		2. Connection：数据库连接对象
			1. 功能：
				1. 获取执行sql 的对象
					* Statement createStatement()
					* PreparedStatement prepareStatement(String sql)  
				2. 管理事务：
					* 开启事务：setAutoCommit(boolean autoCommit) ：调用该方法设置参数为false，即开启事务
					* 提交事务：commit() 
					* 回滚事务：rollback() 
		3. Statement：执行sql的对象
			1. 执行sql
				1. boolean execute(String sql) ：可以执行任意的sql 了解 
				2. int executeUpdate(String sql) ：执行DML（insert、update、delete）语句、DDL(create，alter、drop)语句
					* 返回值：影响的行数，可以通过这个影响的行数判断DML语句是否执行成功 返回值>0的则执行成功，反之，则失败。
				3. ResultSet executeQuery(String sql)  ：执行DQL（select)语句
			2. 练习：
				1. account表 添加一条记录
				2. account表 修改记录
				3. account表 删除一条记录
	
				代码：
					Statement stmt = null;
			        Connection conn = null;
			        try {
			            //1. 注册驱动
			            Class.forName("com.mysql.jdbc.Driver");
			            //2. 定义sql
			            String sql = "insert into account values(null,'王五',3000)";
			            //3.获取Connection对象
			            conn = DriverManager.getConnection("jdbc:mysql:///db3", "root", "root");
			            //4.获取执行sql的对象 Statement
			            stmt = conn.createStatement();
			            //5.执行sql
			            int count = stmt.executeUpdate(sql);//影响的行数
			            //6.处理结果
			            System.out.println(count);
			            if(count > 0){
			                System.out.println("添加成功！");
			            }else{
			                System.out.println("添加失败！");
			            }
			
			        } catch (ClassNotFoundException e) {
			            e.printStackTrace();
			        } catch (SQLException e) {
			            e.printStackTrace();
			        }finally {
			            //stmt.close();
			            //7. 释放资源
			            //避免空指针异常
			            if(stmt != null){
			                try {
			                    stmt.close();
			                } catch (SQLException e) {
			                    e.printStackTrace();
			                }
			            }
			
			            if(conn != null){
			                try {
			                    conn.close();
			                } catch (SQLException e) {
			                    e.printStackTrace();
			                }
			            }
			        }
				
		4. ResultSet：结果集对象,封装查询结果
			* boolean next(): 游标向下移动一行，判断当前行是否是最后一行末尾(是否有数据)，如果是，则返回false，如果不是则返回true
			* getXxx(参数):获取数据
				* Xxx：代表数据类型   如： int getInt() ,	String getString()
				* 参数：
					1. int：代表列的编号,从1开始   如： getString(1)
					2. String：代表列名称。 如： getDouble("balance")
			
			* 注意：
				* 使用步骤：
					1. 游标向下移动一行
					2. 判断是否有数据
					3. 获取数据
	
				   //循环判断游标是否是最后一行末尾。
		            while(rs.next()){
		                //获取数据
		                //6.2 获取数据
		                int id = rs.getInt(1);
		                String name = rs.getString("name");
		                double balance = rs.getDouble(3);
		
		                System.out.println(id + "---" + name + "---" + balance);
		            }
	
			* 练习：
				* 定义一个方法，查询emp表的数据将其封装为对象，然后装载集合，返回。
					1. 定义Emp类
					2. 定义方法 public List<Emp> findAll(){}
					3. 实现方法 select * from emp;
						
		5. PreparedStatement：执行sql的对象
			1. SQL注入问题：在拼接sql时，有一些sql的特殊关键字参与字符串的拼接。会造成安全性问题
				1. 输入用户随便，输入密码：a' or 'a' = 'a
				2. sql：select * from user where username = 'fhdsjkf' and password = 'a' or 'a' = 'a' 
	
			2. 解决sql注入问题：使用PreparedStatement对象来解决
			3. 预编译的SQL：参数使用?作为占位符
			4. 步骤：
				1. 导入驱动jar包 mysql-connector-java-5.1.37-bin.jar
				2. 注册驱动
				3. 获取数据库连接对象 Connection
				4. 定义sql
					* 注意：sql的参数使用？作为占位符。 如：select * from user where username = ? and password = ?;
				5. 获取执行sql语句的对象 PreparedStatement  Connection.prepareStatement(String sql) 
				6. 给？赋值：
					* 方法： setXxx(参数1,参数2)
						* 参数1：？的位置编号 从1 开始
						* 参数2：？的值
				7. 执行sql，接受返回结果，不需要传递sql语句
				8. 处理结果
				9. 释放资源
	
			5. 注意：后期都会使用PreparedStatement来完成增删改查的所有操作
				1. 可以防止SQL注入
				2. 效率更高

## 抽取JDBC工具类 ： JDBCUtils
	* 目的：简化书写
	* 分析：
		1. 注册驱动也抽取
		2. 抽取一个方法获取连接对象
			* 需求：不想传递参数（麻烦），还得保证工具类的通用性。
			* 解决：配置文件
				jdbc.properties
					url=
					user=
					password=


		3. 抽取一个方法释放资源
	
	* 代码实现：
		public class JDBCUtils {
	    private static String url;
	    private static String user;
	    private static String password;
	    private static String driver;
	    /**
	     * 文件的读取，只需要读取一次即可拿到这些值。使用静态代码块
	     */
	    static{
	        //读取资源文件，获取值。
	
	        try {
	            //1. 创建Properties集合类。
	            Properties pro = new Properties();
	
	            //获取src路径下的文件的方式--->ClassLoader 类加载器
	            ClassLoader classLoader = JDBCUtils.class.getClassLoader();
	            URL res  = classLoader.getResource("jdbc.properties");
	            String path = res.getPath();
	            System.out.println(path);///D:/IdeaProjects/itcast/out/production/day04_jdbc/jdbc.properties
	            //2. 加载文件
	           // pro.load(new FileReader("D:\\IdeaProjects\\itcast\\day04_jdbc\\src\\jdbc.properties"));
	            pro.load(new FileReader(path));
	
	            //3. 获取数据，赋值
	            url = pro.getProperty("url");
	            user = pro.getProperty("user");
	            password = pro.getProperty("password");
	            driver = pro.getProperty("driver");
	            //4. 注册驱动
	            Class.forName(driver);
	        } catch (IOException e) {
	            e.printStackTrace();
	        } catch (ClassNotFoundException e) {
	            e.printStackTrace();
	        }
	    }


​	
​	    /**
​	     * 获取连接
​	     * @return 连接对象
​	     */
​	    public static Connection getConnection() throws SQLException {
​	
​	        return DriverManager.getConnection(url, user, password);
​	    }
​	
​	    /**
​	     * 释放资源
​	     * @param stmt
​	     * @param conn
​	     */
​	    public static void close(Statement stmt,Connection conn){
​	        if( stmt != null){
​	            try {
​	                stmt.close();
​	            } catch (SQLException e) {
​	                e.printStackTrace();
​	            }
​	        }
​	
	        if( conn != null){
	            try {
	                conn.close();
	            } catch (SQLException e) {
	                e.printStackTrace();
	            }
	        }
	    }


​	
​	    /**
​	     * 释放资源
​	     * @param stmt
​	     * @param conn
​	     */
​	    public static void close(ResultSet rs,Statement stmt, Connection conn){
​	        if( rs != null){
​	            try {
​	                rs.close();
​	            } catch (SQLException e) {
​	                e.printStackTrace();
​	            }
​	        }
​	
​	        if( stmt != null){
​	            try {
​	                stmt.close();
​	            } catch (SQLException e) {
​	                e.printStackTrace();
​	            }
​	        }
​	
​	        if( conn != null){
​	            try {
​	                conn.close();
​	            } catch (SQLException e) {
​	                e.printStackTrace();
​	            }
​	        }
​	    }
​	
	}
	
	* 练习：
		* 需求：
			1. 通过键盘录入用户名和密码
			2. 判断用户是否登录成功
				* select * from user where username = "" and password = "";
				* 如果这个sql有查询结果，则成功，反之，则失败
	
		* 步骤：
			1. 创建数据库表 user
				CREATE TABLE USER(
					id INT PRIMARY KEY AUTO_INCREMENT,
					username VARCHAR(32),
					PASSWORD VARCHAR(32)
				
				);
	
				INSERT INTO USER VALUES(NULL,'zhangsan','123');
				INSERT INTO USER VALUES(NULL,'lisi','234');
	
			2. 代码实现：
				public class JDBCDemo9 {
	
				    public static void main(String[] args) {
				        //1.键盘录入，接受用户名和密码
				        Scanner sc = new Scanner(System.in);
				        System.out.println("请输入用户名：");
				        String username = sc.nextLine();
				        System.out.println("请输入密码：");
				        String password = sc.nextLine();
				        //2.调用方法
				        boolean flag = new JDBCDemo9().login(username, password);
				        //3.判断结果，输出不同语句
				        if(flag){
				            //登录成功
				            System.out.println("登录成功！");
				        }else{
				            System.out.println("用户名或密码错误！");
				        }


​				
​				    }


​				
​				
​				    /**
​				     * 登录方法
​				     */
​				    public boolean login(String username ,String password){
​				        if(username == null || password == null){
​				            return false;
​				        }
​				        //连接数据库判断是否登录成功
​				        Connection conn = null;
​				        Statement stmt =  null;
​				        ResultSet rs = null;
​				        //1.获取连接
​				        try {
​				            conn =  JDBCUtils.getConnection();
​				            //2.定义sql
​				            String sql = "select * from user where username = '"+username+"' and password = '"+password+"' ";
​				            //3.获取执行sql的对象
​				            stmt = conn.createStatement();
​				            //4.执行查询
​				            rs = stmt.executeQuery(sql);
​				            //5.判断
​				           /* if(rs.next()){//如果有下一行，则返回true
​				                return true;
​				            }else{
​				                return false;
​				            }*/
​				           return rs.next();//如果有下一行，则返回true
​				
​				        } catch (SQLException e) {
​				            e.printStackTrace();
​				        }finally {
​				            JDBCUtils.close(rs,stmt,conn);
​				        }


​				
​				        return false;
​				    }
​				}


## JDBC控制事务：
	1. 事务：一个包含多个步骤的业务操作。如果这个业务操作被事务管理，则这多个步骤要么同时成功，要么同时失败。
	2. 操作：
		1. 开启事务
		2. 提交事务
		3. 回滚事务
	3. 使用Connection对象来管理事务
		* 开启事务：setAutoCommit(boolean autoCommit) ：调用该方法设置参数为false，即开启事务
			* 在执行sql之前开启事务
		* 提交事务：commit() 
			* 当所有sql都执行完提交事务
		* 回滚事务：rollback() 
			* 在catch中回滚事务
	
	4. 代码：
		public class JDBCDemo10 {
	
		    public static void main(String[] args) {
		        Connection conn = null;
		        PreparedStatement pstmt1 = null;
		        PreparedStatement pstmt2 = null;
		
		        try {
		            //1.获取连接
		            conn = JDBCUtils.getConnection();
		            //开启事务
		            conn.setAutoCommit(false);
		
		            //2.定义sql
		            //2.1 张三 - 500
		            String sql1 = "update account set balance = balance - ? where id = ?";
		            //2.2 李四 + 500
		            String sql2 = "update account set balance = balance + ? where id = ?";
		            //3.获取执行sql对象
		            pstmt1 = conn.prepareStatement(sql1);
		            pstmt2 = conn.prepareStatement(sql2);
		            //4. 设置参数
		            pstmt1.setDouble(1,500);
		            pstmt1.setInt(2,1);
		
		            pstmt2.setDouble(1,500);
		            pstmt2.setInt(2,2);
		            //5.执行sql
		            pstmt1.executeUpdate();
		            // 手动制造异常
		            int i = 3/0;
		
		            pstmt2.executeUpdate();
		            //提交事务
		            conn.commit();
		        } catch (Exception e) {
		            //事务回滚
		            try {
		                if(conn != null) {
		                    conn.rollback();
		                }
		            } catch (SQLException e1) {
		                e1.printStackTrace();
		            }
		            e.printStackTrace();
		        }finally {
		            JDBCUtils.close(pstmt1,conn);
		            JDBCUtils.close(pstmt2,null);
		        }


​		
​		    }
​		
​		}

# 今日内容
	1. 数据库连接池
	
	2. Spring JDBC : JDBC Template



## 数据库连接池
	1. 概念：其实就是一个容器(集合)，存放数据库连接的容器。
		    当系统初始化好后，容器被创建，容器中会申请一些连接对象，当用户来访问数据库时，从容器中获取连接对象，用户访问完之后，会将连接对象归还给容器。
	
	2. 好处：
		1. 节约资源
		2. 用户访问高效
	
	3. 实现：
		1. 标准接口：DataSource   javax.sql包下的
			1. 方法：
				* 获取连接：getConnection()
				* 归还连接：Connection.close()。如果连接对象Connection是从连接池中获取的，那么调用Connection.close()方法，则不会再关闭连接了。而是归还连接
	
		2. 一般我们不去实现它，有数据库厂商来实现
			1. C3P0：数据库连接池技术
			2. Druid：数据库连接池实现技术，由阿里巴巴提供的


	4. C3P0：数据库连接池技术
		* 步骤：
			1. 导入jar包 (两个) c3p0-0.9.5.2.jar mchange-commons-java-0.2.12.jar ，
				* 不要忘记导入数据库驱动jar包
			2. 定义配置文件：
				* 名称： c3p0.properties 或者 c3p0-config.xml
				* 路径：直接将文件放在src目录下即可。
	
			3. 创建核心对象 数据库连接池对象 ComboPooledDataSource
			4. 获取连接： getConnection
		* 代码：
			 //1.创建数据库连接池对象
	        DataSource ds  = new ComboPooledDataSource();
	        //2. 获取连接对象
	        Connection conn = ds.getConnection();
	5. Druid：数据库连接池实现技术，由阿里巴巴提供的
		1. 步骤：
			1. 导入jar包 druid-1.0.9.jar
			2. 定义配置文件：
				* 是properties形式的
				* 可以叫任意名称，可以放在任意目录下
			3. 加载配置文件。Properties
			4. 获取数据库连接池对象：通过工厂来来获取  DruidDataSourceFactory
			5. 获取连接：getConnection
		* 代码：
			 //3.加载配置文件
	        Properties pro = new Properties();
	        InputStream is = DruidDemo.class.getClassLoader().getResourceAsStream("druid.properties");
	        pro.load(is);
	        //4.获取连接池对象
	        DataSource ds = DruidDataSourceFactory.createDataSource(pro);
	        //5.获取连接
	        Connection conn = ds.getConnection();
		2. 定义工具类
			1. 定义一个类 JDBCUtils
			2. 提供静态代码块加载配置文件，初始化连接池对象
			3. 提供方法
				1. 获取连接方法：通过数据库连接池获取连接
				2. 释放资源
				3. 获取连接池的方法


		* 代码：
			public class JDBCUtils {
	
			    //1.定义成员变量 DataSource
			    private static DataSource ds ;
			
			    static{
			        try {
			            //1.加载配置文件
			            Properties pro = new Properties();
			            pro.load(JDBCUtils.class.getClassLoader().getResourceAsStream("druid.properties"));
			            //2.获取DataSource
			            ds = DruidDataSourceFactory.createDataSource(pro);
			        } catch (IOException e) {
			            e.printStackTrace();
			        } catch (Exception e) {
			            e.printStackTrace();
			        }
			    }
			
			    /**
			     * 获取连接
			     */
			    public static Connection getConnection() throws SQLException {
			        return ds.getConnection();
			    }
			
			    /**
			     * 释放资源
			     */
			    public static void close(Statement stmt,Connection conn){
			       /* if(stmt != null){
			            try {
			                stmt.close();
			            } catch (SQLException e) {
			                e.printStackTrace();
			            }
			        }
			
			        if(conn != null){
			            try {
			                conn.close();//归还连接
			            } catch (SQLException e) {
			                e.printStackTrace();
			            }
			        }*/
			
			       close(null,stmt,conn);
			    }


​			
​			    public static void close(ResultSet rs , Statement stmt, Connection conn){


​			
​			        if(rs != null){
​			            try {
​			                rs.close();
​			            } catch (SQLException e) {
​			                e.printStackTrace();
​			            }
​			        }


​			
​			        if(stmt != null){
​			            try {
​			                stmt.close();
​			            } catch (SQLException e) {
​			                e.printStackTrace();
​			            }
​			        }
​			
​			        if(conn != null){
​			            try {
​			                conn.close();//归还连接
​			            } catch (SQLException e) {
​			                e.printStackTrace();
​			            }
​			        }
​			    }
​			
​			    /**
​			     * 获取连接池方法
​			     */
​			
			    public static DataSource getDataSource(){
			        return  ds;
			    }
			
			}

## Spring JDBC
	* Spring框架对JDBC的简单封装。提供了一个JDBCTemplate对象简化JDBC的开发
	* 步骤：
		1. 导入jar包
		2. 创建JdbcTemplate对象。依赖于数据源DataSource
			* JdbcTemplate template = new JdbcTemplate(ds);
	
		3. 调用JdbcTemplate的方法来完成CRUD的操作
			* update():执行DML语句。增、删、改语句
			* queryForMap():查询结果将结果集封装为map集合，将列名作为key，将值作为value 将这条记录封装为一个map集合
				* 注意：这个方法查询的结果集长度只能是1
			* queryForList():查询结果将结果集封装为list集合
				* 注意：将每一条记录封装为一个Map集合，再将Map集合装载到List集合中
			* query():查询结果，将结果封装为JavaBean对象
				* query的参数：RowMapper
					* 一般我们使用BeanPropertyRowMapper实现类。可以完成数据到JavaBean的自动封装
					* new BeanPropertyRowMapper<类型>(类型.class)
			* queryForObject：查询结果，将结果封装为对象
				* 一般用于聚合函数的查询
	
		4. 练习：
			* 需求：
				1. 修改1号数据的 salary 为 10000
				2. 添加一条记录
				3. 删除刚才添加的记录
				4. 查询id为1的记录，将其封装为Map集合
				5. 查询所有记录，将其封装为List
				6. 查询所有记录，将其封装为Emp对象的List集合
				7. 查询总记录数
	
			* 代码：
				
				import cn.itcast.domain.Emp;
				import cn.itcast.utils.JDBCUtils;
				import org.junit.Test;
				import org.springframework.jdbc.core.BeanPropertyRowMapper;
				import org.springframework.jdbc.core.JdbcTemplate;
				import org.springframework.jdbc.core.RowMapper;
				
				import java.sql.Date;
				import java.sql.ResultSet;
				import java.sql.SQLException;
				import java.util.List;
				import java.util.Map;
				
				public class JdbcTemplateDemo2 {
				
				    //Junit单元测试，可以让方法独立执行


​				
​				    //1. 获取JDBCTemplate对象
​				    private JdbcTemplate template = new JdbcTemplate(JDBCUtils.getDataSource());
​				    /**
​				     * 1. 修改1号数据的 salary 为 10000
​				     */
​				    @Test
​				    public void test1(){
​				
​				        //2. 定义sql
​				        String sql = "update emp set salary = 10000 where id = 1001";
​				        //3. 执行sql
​				        int count = template.update(sql);
​				        System.out.println(count);
​				    }
​				
​				    /**
​				     * 2. 添加一条记录
​				     */
​				    @Test
​				    public void test2(){
​				        String sql = "insert into emp(id,ename,dept_id) values(?,?,?)";
​				        int count = template.update(sql, 1015, "郭靖", 10);
​				        System.out.println(count);
​				
				    }
				
				    /**
				     * 3.删除刚才添加的记录
				     */
				    @Test
				    public void test3(){
				        String sql = "delete from emp where id = ?";
				        int count = template.update(sql, 1015);
				        System.out.println(count);
				    }
				
				    /**
				     * 4.查询id为1001的记录，将其封装为Map集合
				     * 注意：这个方法查询的结果集长度只能是1
				     */
				    @Test
				    public void test4(){
				        String sql = "select * from emp where id = ? or id = ?";
				        Map<String, Object> map = template.queryForMap(sql, 1001,1002);
				        System.out.println(map);
				        //{id=1001, ename=孙悟空, job_id=4, mgr=1004, joindate=2000-12-17, salary=10000.00, bonus=null, dept_id=20}
				
				    }
				
				    /**
				     * 5. 查询所有记录，将其封装为List
				     */
				    @Test
				    public void test5(){
				        String sql = "select * from emp";
				        List<Map<String, Object>> list = template.queryForList(sql);
				
				        for (Map<String, Object> stringObjectMap : list) {
				            System.out.println(stringObjectMap);
				        }
				    }
				
				    /**
				     * 6. 查询所有记录，将其封装为Emp对象的List集合
				     */
				
				    @Test
				    public void test6(){
				        String sql = "select * from emp";
				        List<Emp> list = template.query(sql, new RowMapper<Emp>() {
				
				            @Override
				            public Emp mapRow(ResultSet rs, int i) throws SQLException {
				                Emp emp = new Emp();
				                int id = rs.getInt("id");
				                String ename = rs.getString("ename");
				                int job_id = rs.getInt("job_id");
				                int mgr = rs.getInt("mgr");
				                Date joindate = rs.getDate("joindate");
				                double salary = rs.getDouble("salary");
				                double bonus = rs.getDouble("bonus");
				                int dept_id = rs.getInt("dept_id");
				
				                emp.setId(id);
				                emp.setEname(ename);
				                emp.setJob_id(job_id);
				                emp.setMgr(mgr);
				                emp.setJoindate(joindate);
				                emp.setSalary(salary);
				                emp.setBonus(bonus);
				                emp.setDept_id(dept_id);
				
				                return emp;
				            }
				        });


​				
​				        for (Emp emp : list) {
​				            System.out.println(emp);
​				        }
​				    }
​				
​				    /**
​				     * 6. 查询所有记录，将其封装为Emp对象的List集合
​				     */
​				
​				    @Test
​				    public void test6_2(){
​				        String sql = "select * from emp";
​				        List<Emp> list = template.query(sql, new BeanPropertyRowMapper<Emp>(Emp.class));
​				        for (Emp emp : list) {
​				            System.out.println(emp);
​				        }
​				    }
​				
				    /**
				     * 7. 查询总记录数
				     */
				
				    @Test
				    public void test7(){
				        String sql = "select count(id) from emp";
				        Long total = template.queryForObject(sql, Long.class);
				        System.out.println(total);
				    }
				
				}


​				
​					
​	

