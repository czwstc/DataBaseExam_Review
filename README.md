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

```sql
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

建立一个S表，定义SN+SEX为唯一键。CONSTRAINT S_UNIQ 为 CONSTRAINT 约束名

```
USE STUDENT
CREATE TABLE S 
( SNO CHAR(5),
SN CHAR(8),
SEX CHAR(2),
CONSTRAINT S_UNIQ UNIQUE(SN,SEX));
```

FOREIGN KEY约束指定某一个列或一组列作为外部键，其中，包含外部键的表称为从表，包含外部键所引用的主键或唯一键的表称主表。

```sql
USE STUDENT
CREATE TABLE SC
(SNO CHAR(5) NOT NULL CONSTRAINT S_FORE FOREIGN KEY REFERENCES S(SNO),
CNO CHAR(5) NOT NULL CONSTRAINT C_FORE FOREIGN KEY REFERENCES C(CNO),
SCORE NUMERIC(3),
CONSTRAINT S_C_PRIM PRIMARY KEY (SNO,CNO));
```

CHECK约束用来检查字段值所允许的范围，如，一个字段只能输入整数，而且限定在0-100的整数，以此来保证域的完整性。[ CONSTRAINT<约束名>] CHECK (<条件>)

建立一个SC表，定义SCORE的取值范围为0到100之间。

```sql
USE STUDENT
CREATE TABLE SC
(SNO CHAR(5),
CNO CHAR(5),
SCORE NUMERIC(5,1) CONSTRAINT SCORE_CHK CHECK(SCORE>=0 AND SCORE <=100));
```

```sql
USE STUDENT
CREATE TABLE S
(SNO CHAR(6) CONSTRAINT S_PRIM PRIMARY KEY,
SN CHAR(8) CONSTRAINT SN_CONS NOT NULL,
AGE NUMERIC(2) CONSTRAINT AGE_CONS NOT NULL
CONSTRAINT AGE_CHK CHECK (AGE BETWEEN 15 AND 50),
SEX CHAR(2) DEFAULT '男',
DEPT CHAR(10) CONSTRAINT DEPT_CONS NOT NULL);
```

SQL语言使用ALTER TABLE命令来完成修改基本表，有如下三种修改方式：

SQL语言使用ALTER TABLE命令来完成修改基本表，有如下三种修改方式：

1.ADD方式

```sql
USE STUDENT
ALTER TABLE S 
（添加字段）
ADD
CLASS_NO CHAR(6),
ADDRESS CHAR(40)
	（添加完整性）
CONSTRAINT SCORE_CHK CHECK(SCORE BETWEEN 0 AND 100)

```

2.ALTER 方式	

> ​	（只能修改NULL|NOT NULL约束，其它类型的约束在修改之前必须先删除，然后再重新添加修改过的约束定义。 ）

把S表中的SNO列加宽到8位字符宽度

```sql
USE STUDENT
ALTER TABLE S 
ALTER COLUMN
SNO CHAR(8)
```

3.DROP方式

```sql
USE STUDENT
ALTER TABLE S
DROP 
CONSTRAINT AGE_CHK
```

删除表STUDENT

```sql
USE STUDENT 	
DROP TABLE STUDENT
```

索引的分类

\1. 按照索引记录的存放位置可分为聚集索引与非聚集索引

Ø聚集索引：按照索引的字段排列记录，并且依照排好的顺序将记录存储在表中。

Ø非聚集索引：按照索引的字段排列记录，但是排列的结果并不会存储在表中，而是另外存储。

\2. 唯一索引的概念

Ø唯一索引表示表中每一个索引值只对应唯一的数据记录，

Ø这与表的PRIMARY KEY的特性类似，因此唯一性索引常用于PRIMARY KEY的字段上，以区别每一笔记录。

Ø当表中有被设置为UNIQUE的字段时，SQL SERVER会自动建立一个非聚集的唯一性索引。

Ø而当表中有PRIMARY KEY的字段时，SQL SERVER会在PRIMARY KEY字段建立一个聚集索引。

\3. 复合索引的概念

Ø复合索引是将两个字段或多个字段组合起来建立的索引，而单独的字段允许有重复的值。



为表SC在SNO和CNO上建立唯一索引。

```sql
建立索引的语句是CREATE INDEX，其语法格式为：
		CREATE [UNIQUE] [CLUSTER] INDEX <索引名> ON <表名> (<列名> [次序] [{,<列名>}] [次序]…)
USE STUDENT
CREATE UNIQUE INDEX SCI ON SC(SNO,CNO)

删除表SC的索引SCI		
DROP INDEX SC.SCI
```

SELECT 查询

```sql
SELECT〈列名〉[{，〈列名〉}]
FROM〈表名或视图名〉[{，〈表名或视图名〉}]
[WHERE〈检索条件〉]
[GROUP BY <列名1>[HAVING <条件表达式>]]
[ORDER BY <列名2>[ASC|DESC]];
```

完全格式

```sql
SELECT语句的格式：
SELECT	[ALL|DISTINCT][TOP N [PERCENT][WITH TIES]]
列名1 [AS 别名1]
[, 列名2 [ AS 别名2]…]
[INTO 新表名]
FROM 表名 1[[AS] 表1别名]
[INNER|RIGHT|FULL|OUTER][OUTER]JOIN
    表名2 [[AS] 表2别名]
ON 条件
```

| 运算符            | 含义   |
| -------------- | ---- |
| =,>,<,>=,<=,!= | 比较大小 |
| AND、OR         | 多重条件 |
| BETWEEN、AND    | 确定范围 |
| IN             | 确定集合 |
| LIKE           | 字符匹配 |
| IS NULL        | 空值   |

```sql
SELECT SNO,CNO,SCORE FROM SC WHERE
SCORE>85

SELECT SNO,SCORE FROM SC WHERE CNO=’C1’


SELECT SNO，CNO，SCORE
FROM SC
WHERE（CNO=’C1’ OR CNO=’C2’） AND SCORE>=85 


查询工资在1000至1500之间的教师的教师号、姓名及职称。
SELECT TNO,TN,PROF
FROM T
WHERE SAL BETWEEN 1000 AND 1500
等价于
SELECT TNO,TN,PROF
FROM T
WHERE SAL>=1000 AND SAL<=1500

```

利用“IN”操作可以查询属性值属于指定集合的元组。

```sql
查询选修C1或C2的学生的学号、课程号和成绩。
SELECT SNO, CNO, SCORE 
FROM SC 
WHERE CNO IN(‘C1’, ‘C2’)
此语句也可以使用逻辑运算符“OR”实现。
SELECT SNO, CNO, SCORE 
FROM SC 
WHERE CNO=‘C1’ OR CNO= ‘C2’

```

上例均属于完全匹配查询，当不知道完全精确的値时，用户还可以使用LIKE或NOT LIKE进行部分匹配查询（也称模糊查询）。

LIKE定义的一般格式为：

  <属性名> LIKE <字符串常量>

属性名必须为字符型，字符串常量的字符可以包含如下两个特殊符号：

%：表示任意知长度的字符串；

_：表示任意单个字符。

例3.32 查询所有姓张的教师的教师号和姓名。

```sql
SELECTTNO, TN 
FROMT
WHERETN LIKE ‘张%’

查询姓名中第二个汉字是“力”的教师号和姓名
SELECT TNO, TN 
FROM T
WHERE TN LIKE ‘_ _力%’ 
一个汉字占两个字符

查询没有考试成绩的学生的学号和相应的课程号
SELECT SNO, CNO
FROM SC
WHERE SCORE IS NULL

```

```sql
求学号为S1学生的总分和平均分。
SELECT SUM(SCORE) AS TotalScore, AVG(SCORE) AS AveScore
FROM SC
WHERE (SNO = 'S1') 

求选修C1号课程的最高分、最低分及之间相差的分数
SELECT MAX(SCORE) AS MaxScore, MIN(SCORE) AS MinScore, MAX(SCORE) - MIN(SCORE) 
      AS Diff
FROM SC
WHERE (CNO = 'C1') 

求计算机系学生的总数
SELECT COUNT(SNO) FROM S
WHERE DEPT='计算机'

```

```sql
例3.38 求学校中共有多少个系
SELECT COUNT(DISTINCT DEPT) AS DeptNum 
FROM S
注意：加入关键字DISTINCT后表示消去重复行，可计算字段“DEPT“不同值的数目。
COUNT函数对空值不计算，但对零进行计算。

例3.39  统计有成绩同学的人数
SELECT COUNT (SCORE) 
FROM SC

上例中成绩为零的同学计算在内，没有成绩（即为空值）的不计算。 

```

分组查询

```sql
GROUP BY子句可以将查询结果按属性列或属性列组合在行的方向上进行分组，每组在属性列或属性列组合上具有相同的值。
查询各位教师的教师号及其任课的门数。

SELECT TNO,COUNT(*) AS C_NUM
FROM TC
GROUP BY TNO 

若在分组后还要按照一定的条件进行筛选，则需使用HAVING子句。 

例3.43 查询选修两门以上课程的学生学号和选课门数
SELECT SNO,COUNT(*) AS SC_NUM 
FROM SC
GROUP BY SNO       
HAVING COUNT(*)>=2 

GROUP BY子句按SNO的值分组，所有具有相同SNO的元组为一组，对每一组使用函数COUNT进行计算，统计出每位学生选课的门数。
HAVING子句去掉不满足COUNT（*）>=2的组。

当在一个SQL查询中同时使用WHERE子句，GROUP  BY 子句和HAVING子句时，其顺序是WHERE－GROUP  BY－ HAVING

HAVING子句作用于组，选择满足条件的组，必须用于GROUP BY子句之后，但GROUP BY子句可没有HAVING子句。

求选课在三门以上且各门课程均及格的学生的学号及其总成绩，查询结果按总成绩降序列出。
SELECT SNO,SUM(SCORE) AS TotalScore  FROM SC
WHERE SCORE>=60
GROUP BY SNO
HAVING COUNT(*)>=3
ORDER BY SUM(SCORE) DESC

此语句为分组排序，执行过程如下：
1.（FROM）取出整个SC
2.（WHERE）筛选SCORE>=60的元组
3.（GROUP BY）将选出的元组按SNO分组
4.（HAVING）筛选选课三门以上的分组
5.（SELECT）以剩下的组中提取学号和总成绩
6.（ORDER BY）将选取结果排序


SELECT S.SNO,SN,CN,SCORE
FROM S,C,SC
WHERE S.SNO=SC.SNO AND SC.CNO=C.CNO


检索所有学生姓名，年龄和选课名称。
方法1：
SELECT SN,AGE,CN
FROM S,C,SC
WHERE S.SNO=SC.SNO AND SC.CNO=C.CNO

查询与刘伟教师职称相同的教师号、姓名。
SELECT TNO,TN
FROM T
WHERE PROF=(SELECT PROF 
FROM T
WHERE TN='刘伟')


```

