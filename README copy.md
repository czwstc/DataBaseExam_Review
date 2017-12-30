##  数据库复习

辨别：规范化原理 12% 

简答：数据库概论 10%  数据库安全 10% 数据库完整性 12%  

设计：数据模型 5%  E-R图 10%

##### 1.数据库管理数据的特点：

​	1、数据共享性高、冗余少

​	2、数据结构化

​	3、数据独立性高 （逻辑独立性 总体逻辑改变，局部逻辑结构不变。物理独立性：数据的存储结构改变时，数据的逻辑结构不变 ）

​	4、有统一的数据控制功能（多用户共享时的 1.安全性控制 2.完整性控制 3.并发控制 4.数据恢复）

##### 2.数据库理论

​	1.数据库理论的研究主要集中于关系规范化理论、关系数据理论等 

​	2.数据库特点如下 1. 集成性 2. 共享性 

​	3.三级模式

​		1. 模式       中间层 现实世界所有信息内容集合的表示。“DBA视图” 

​		2.外模式   最外层 外视图称为用户数据库 个别用户看到和使用的数据库内容 

​		3.内模式   最内层 最靠近物理存储，与实际存储数据方式有关。但不必关心具体的存储位置。

​	4.三级模式的优点 1.内外分开 保证数据的独立性 2.简化用户接口 3.有利于数据共享 4.有利于保密

##### 3.数据模型

​	数据模型通常由数据结构、数据操作和数据的约束条件三个要素组成。

​	层次模型用“树结构”来表示数据之间的联系；

​	网状模型是用“图结构”来表示数据之间的联系；

​	关系模型是用“二维表”来表示数据之间的联系

​	定义： 

​		关系：一个关系对应一张二维表 

​		元组：表格里的一行 

​		属性：表格中的一列（一个字段，比如学号）

​		关键字：	称为关系键或主码

​		域：取值范围 比如：性别（男，女）

​		分量：每一行对应的列的属性值。

​		关系模式：对关系的描述，如：学生（学号，姓名，性别，年龄，系别）

​		

##### 4.E_R概念模型

> 	实体间的联系：

​		一对一联系：（1:1）比如观众与座位

​		一对多联系：（1:n）比如公司与职员，班级与学生

​		多对多联系：（m:n) 比如教师与学生

> ##### 	E-R图

​		![E_R](https://github.com/czwstc/DataBaseExam_Review/blob/master/photo/完整.png)

##### 5.关系的键

​	候选键：唯一标示关系中元组的属性或属性集。

​	主键：多个候选键可以选一个座位查询、删除的操作变量的，称为 主关系键（主键）

​	主属性：包含在主键中的属性。

​	实体完整性和参照完整性：实体就是主键不为空。

##### 6.关系代数

​	σ(选择)，∏（投影），∞（连接），*（自然连接），÷（除）；	

​	∧（与）,∨（或）,┐（非）

​	查询计算机系的全体学生：

​	![查询1](https://github.com/czwstc/DataBaseExam_Review/blob/master/photo/查询1.jpg)

![查询2](https://github.com/czwstc/DataBaseExam_Review/blob/master/photo/查询2.jpg)

​	投影：选择出若干属性列，组成新的关系

​	![投影](https://github.com/czwstc/DataBaseExam_Review/blob/master/photo/投影.jpg)

![投影2](https://github.com/czwstc/DataBaseExam_Review/blob/master/photo/投影2.jpg)

​	连接：等值连接中属性名可以不同，自然（*）就一定要相同。![连接](https://github.com/czwstc/DataBaseExam_Review/blob/master/photo/连接.jpg)

​	如何用？

![查询](https://github.com/czwstc/DataBaseExam_Review/blob/master/photo/查询.jpg)

![table1](https://github.com/czwstc/DataBaseExam_Review/blob/master/photo/table1.png)

![陈](https://github.com/czwstc/DataBaseExam_Review/blob/master/photo/陈.jpg)

##### 语句：

​	整数：INT 浮点数：FLOAT 时间：DATETIME 字符串：CHAR 、VARCHAR

​	SQL：

CREATE TABLE 表名 ( 列名 数据类型 （default）（列约束）， 列名 数据类型 （列约束）)

```Sql
USE STUDENT
CREATE TABLE S	创建表S
(SNO CHAR(8) ,	
SN VARCHAR(20),
AGE INT,	
SEX CHAR(2) DEFAULT '男' ,//默认 男
DEPT VARCHAR(20));

```

约束：NULL/NOT NULL 非空，UNIQUE约束 PRIMARY KEY约束。unique可以有多个，primary只能有一个。

```sql
USE STUDENT
CREATE TABLE S
(SNO CHAR(10) NOT NULL ,
SN CHAR(8) UNIQUE,
AGE INT,
SEX CHAR(2) DEFAULT '男' ,
DEPT VARCHAR(20));  
```

