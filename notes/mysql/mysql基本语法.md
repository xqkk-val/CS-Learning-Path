mysql --version

  

mysql -uroot -p

123

  
  

2.1创建数据库的语法

  

CREATE DATABASE [IF NOT EXISTS] 数据库名称 DEFAULT CHARACTER SET 字符集 COLLATE 排序规则；

  

示例：创建数据库lesson，并指定字符集为GBK，排序规则为GBK_CHINESE_CI

CREATE DATABASE IF NOT EXISTS lesson DEFAULT CHARACTER SET GBK COLLATE GBK_CHINESE_CI;

  

2.2修改数据库的语法

  

ALTER DATABASE 数据库名称 CHARACTER SET 字符集 COLLATE 排序规则；

  

示例：修改数据库lesson的字符集为UTF8，排序规则为UTF8_GENERAL_CI

ALTER DATABASE lesson CHARACTER SET UTF8 COLLATE UTF8_GENERAL_CI;

2.3删除数据库的语法

  

DROP DATABASE [IF EXISTS] 数据库名称；

  

示例：删除数据库lesson

DROP DATABASE IF EXISTS lesson;

  

2.4查看数据库语法

SHOW DATABASES;

  

2.5使用数据库的语法

USE 数据库名称；

  

3.列类型

decimal

3.2 日期时间类型

  

DATE

YYYY-MM-dd，日期格式

1000-01-01～´9999-12-31

TIME

HH:mm:ss，时间格式

-838:59:59.000000～838:59:59.000000

DATETIME

YY-MM-dD HH:MM:SS

1000-01-01 00:00:00.000000～ 9999-12-31 23:59:59.999999

TIMESTAMP

YYYY-MM-ddHH:mm:ss格式表示的时间载

1970-01-01 00:00:01.000000～ 2038-01-19 03:14:07.999999

YEAR

YYYY格式的年份值

1901~2155

3.3 字符串类型

  

char[(M)]

固定长字符串，检索快但费空间，0<=M<=255

M字符

char（50）；--不论插入的值占用多少位空间，在数据库中都会占50个长度

varchar [(M)]

可变字符串0<= M <= 65535

变长度

varchar（50）;--最大占用50个长度。

text

文本串

216-1字节

3.4列类型修饰属性

  

UNSIGNED

无符号，只能修来修饰数值类型，表名该列数据不能出现负数

UNSIGNEDINT(4)，表示只能为4位大于等于O的整数

  

ZEROFILL

不足的位数使用0来填充

INT(4)ZEROFILL，如果给定的值为10，此时只有2位，而该列需要4位，不足的2位由0来填充，最终值为0010

  

NOT NULL

表示该列类型的值不能为空

VARCHAR(20)NOTNULL，表示该列数据不能为空值

  

DEFAULT

表示设置默认值

INT(4)DEFAULT0，表示该列不赋值时默认为0

  

AUTO_INCREMENT

表示自增长，只能应用于数值列类型，该列类型必须为键，且不能为空

INT(1 1) AUTO_INCREMENT NOT NULL PRIMARY KEY。第一次

为该列中插入值时为1，第二次为2

  

4.数据表操作

  

4.3创建数据表

CREATE TABLE [IF NOT EXISTS]数据表名称（

字段名1 列类型（长度）[修饰属性][键/索引][注释]，

字段名2 列类型（长度）[修饰属性][键/索引][注释]，

字段名3 列类型（长度）[修饰属性][键/索引][注释]，

字段名n 列类型（长度）[修饰属性][键/索引][注释]

）[ENGINE=数据表类型][CHARSET=字符集编码][COMMENT=注释]；

示例：创建学生表，表中有字段学号、姓名、性别、年龄和成绩

  

CREATE TABLE IF NOT EXISTS student(

number VARCHAR(30) NOT NULL PRIMARY KEY COMMENT '学号，主键',

name VARCHAR(30) NOT NULL COMMENT'姓名',

sex TINYINT(1) UNSIGNED DEFAULT 0 COMMENT '性别：0-男，1-女 2-其他',

age TINYINT(3) UNSIGNED DEFAULT 0 COMMENT '年龄',

score DOUBLE(5,2) UNSIGNED COMMENT '成绩'

)ENGINE=InnoDB CHARSET=UTF8 COMMENT='学生表';

  

4.4修改数据表

  

·修改表名

ALTER TABLE 表名 RENAME AS 新表名；

  

示例：将student表名称修改为stu

ALTER TABLE student RENAME AS stu;

  

·增加字段

ALTER TABLE 表名 ADD 字段名 列类型（长度）[修饰属性][键/索引][注释];

示例：在stu表中添加字段联系电话（phone)，类型为字符串，长度为11，非空

ALTER TABLE stu ADD phone VARCHAR(11) NOT NULL COMMENT '联系电话';

  

·查看表结构

DESC 表名；--查看表结构

DESC student;

·查看表数据

SELECT * FROM course;

  

·修改字段

--MODIFY只能修改字段的修饰属性

ALTER TABLE 表名 MODIFY 字段名 列类型（长度）[修饰属性][键/索引][注释]；

示例：将stu表中的sex字段的类型设置为VARCHAR，长度为2，默认值为’男’，注释为"性别，男，女，其他"

ALTER TABLE stu MODIFY sex VARCHAR(2) DEFAULT '男' COMMENT '性别，男，女，其他';

  

--CHANGE可以修改字段的名字以及修饰属性

ALTER TABLE 表名 CHANGE 字段名 新字段名 列类型（长度）[修饰属性][键/索引][注释]；

示例：将stu表中phone字段修改为mobile，属性保持不变

ALTER TABLE stu CHANGE phone mobile VARCHAR(11) NOT NULL COMMENT '联系电话';

  

删除字段

ALTER TABLE 表名DROP字段名；

  

示例：将stu表中的mobile字段删除

ALTER TABLE stu DROP mobile;

  

4.5删除数据表

DROP TABLE [IF EXISTS]表名；

DROP TABLE IF EXISTS stu;

  

第一节DML语句

2. INSERT 语句

--需要注意，VALUES后的字段值必须与表名后的字段名一一对应

  

INSERT INTO 表名（字段名1，字段名2，···,字段名n）VALUES(字段值1，字段值1，··.，字段值n)；

需要注意，VALUES 后的字段值必须与创建表时的字段顺序保持一一对应

INSERT INTO 表名 VALUES(字段值1，字段值1，··.，字段值n)；

--一次性插入多条数据

INSERT INTO 表名(字段名1，字段名2，··字段名n)VALUES(字段值1，字段值1，··，字段值n)，(字段值1，字段值1，··，字段值

，，（字段值，字段值，·字段值n)；

INSERT INTO 表名 VALUES(字段值1，字段值1，…，字段值n)，(字段值1，字段值1，·，字段值n)，·，字段值1，字段值1，

字段值n；

示例

向课程表中插入数据

INSERT INTO course('number'， name, score, 'time') VALUES (1, 'Java基础', 4, 40);

INSERT INTO course VALUES（2，'数据库'，3，20)；

INSERT INTo course('number'， score, name, 'time') VALUEs (3,5, 'Jsp', 40);

INSERT INTo course('number', name, score, 'time') VALUEs (4, 'Spring', 4, 5),(5, 'Spring Mvc', 2, 5)；

INSERT INTO course VALUES (6， 'SSM',2，3)，(7, 'spring Boot'，2,2)

  

3.UPDATA语句

UPDATA 表名 SET 字段名1=字段值1[，字段名2=字段值2,...，字段名n-字段值n][WHERE修改条件]

  

3.1 WHERE条件子句

在Java中，条件的表示通常都是使用关系运算符来表示，在SQL语句中也是一样，使用>,<,>=,<=,！=来表示。不同的是，除此之外，

SQL中还可以使用SQL专用的关键字来表示条件。这些将在后面的DQL语句中详细讲解。

在Java中，条件之间的衔接通常都是使用逻辑运算符来表示，在SQL语句中也是一样，但通常使用AND来表示逻辑与&&），使用OR来表

示逻辑或（||）

示例

WHEREtime >20 && time 40; <=> WHERE time > 20 and time <40;

3.2UPDATA语句

示例

--将数据库的学分更改为3，学时更改为15

UPDATE course SET score=4，'time'=15 WHERE name='数据库'；

  

4. DELETE语句

DELETE FROM 表名[WHERE 删除条件]；

示例

删除课程表中课程编号为1的数据

DELETE FROM course WHERE 'number'=1;

5.TRUNCATE语句

--清空表中数据

TRUNCATE [TABLE] 表名;

示例

清空课程表数据

TRUNCATE course:

6.DELETE 与 TRUNCATE 区别

·DELETE 语句根据条件删除表中数据，而 TRUNCATE 语句则是将表中数据全部清空；如果 DELETE 语句要删除表中所有数据，那么在效

 率上要低于TRUNCATE语句。

·如果表中有自增长列，TRUNCATE语句会重置自增长的计数器，但DELETE语句不会。

·TRUNCATE语句执行后，数据无法恢复，而DELETE语句执行后，可以使用事务回滚进行恢复。

  
  
  

第二节DQL语句

1.什么是DQL

DQL全称是 Data Query Language，表示数据查询语言。体现在数据的查询操作上，因此，DQL仅包括SELECT语句。

2. SELECT语句

SELECT ALL/DISTINCT*|字段名1 AS 别名1[,字段名1 AS 别名1，···，字段名nAS别名n]FROM 表名 WHERE 查询条件

解释说明

ALL表示查询所有满足条件的记录，可以省略；DISTINCT表示去掉查询结果中重复的记录

AS可以给数据列、数据表取一个别名

  

示例：从课程表中查询课程编号小于5的课程名称

SELECT name FROM course WHERE number<5;

  

从课程表中查询课程名称为”Java基础”的学分和学时

SELECT score，time FROM course WHERE name='Java基础';

  

一列的别名

SELECTscoreAS'学分'，｀time｀AS'学时'FROM course WHERE name='Java基础'；

  

一表的别名

SELECT c.name '课程名称',c.score'学分',c.time '学时' FROM course c WHE*5E c.name='Java基础';

  

SELECT * FROM course WHERE name IS NOT NULL;

  

SELECT * FROM course WHERE score BETWEEN 2 AND 4;

--查询课程名包含ing的课程信息

SELECT * FROM course WHERE name LIKE '%ing%';

--查询课程名包含ing结尾的课程信息

SELECT * FROM course WHERE name LIKE '%ing';

--查询课程名包含ing开头的课程信息

SELECT * FROM course WHERE name LIKE 'ing%';

--查询课程名只有3个字符的课程信息

SELECT * FROM course WHERE name LIKE '   ';

--查询课程名以s开始且只有3个字符的课程信息

SELECT * FROM course WHERE name LIKE 's  ';

--从课程表查询课程编号为1，3，5的课程信息

SELECT * FROM COURSe WHERE `number` IN (1,3,5);

  
  

数据表准备：新建学生表student，包含字段学号(no)，类型为长整数，长度为20，是主键，自增长，非空；姓名（name），类型为

字符串，长度为20，非空；性别(sex)，类型为字符串，长度为2，默认值为”男”；年龄（age），类型为整数，长度为3，默认值为0;

成绩(score)，类型为浮点数，长度为5，小数点后面保留2位有效数字

  

DROP TABLE IF EXISTS student;

CREATE TABLE student(

 no BIGINT(20) AUTO_INCREMENT NOT NULL PRIMARY KEY COMMENT '学号,主键',

 name VARCHAR(20) NOT NULL COMMENT '姓名',

 sex VARCHAR(2) DEFAULT '男' COMMENT'性别',

 age INT(3) DEFAULT 0 COMMENT'年龄',

 score DOUBLE(5,2) COMMENT '成绩'

)ENGINE=InnoDB CHARSET=UTF8 COMMENT='学生表';

  

插入测试数据：

-- 第1条

INSERT INTO student(no,name,sex,age,score) VALUES (DEFAULT,'张三','男',20,59);

  

-- 第2条

INSERT INTO student(no,name,sex,age,score) VALUES (DEFAULT,'李四','女',19,62);

  

-- 第3条

INSERT INTO student(no,name,sex,age,score) VALUES (DEFAULT,'王五','其他',21,62);

  

-- 第4条

INSERT INTO student(no,name,sex,age,score) VALUES (DEFAULT,'龙华','男',22,75);

  

-- 第5条

INSERT INTO student(no,name,sex,age,score) VALUES (DEFAULT,'金风','女',18,80);

  

-- 第6条

INSERT INTO student(no,name,sex,age,score) VALUES (DEFAULT,'张华','其他',27,88);

  

-- 第7条

INSERT INTO student(no,name,sex,age,score) VALUES (DEFAULT,'李刚','男',30,88);

  

-- 第8条

INSERT INTO student(no,name,sex,age,score) VALUES (DEFAULT,'潘玉明','女',28,81);

  

-- 第9条

INSERT INTO student(no,name,sex,age,score) VALUES (DEFAULT,'凤飞飞','其他',32,90);

4.1 分组查询{

    -- 临时修改当前会话的 SQL 模式

SET SESSION sql_mode = (SELECT REPLACE(@@sql_mode, 'ONLY_FULL_GROUP_BY', ''));

}

SELECT ALL/DISTINCT * |字段名1 AS 别名1[,字段名1AS别名1，···，字段名nAS别名n]FROM 表名 WHERE 查询条件 GROUP

BY 字段名,字段名2,...字段名n

  

--从学生表查询成绩在80分以上的学生信息并按性别分组

SELECT * FROM student WHERE score>80 group(order) BY sex;

SELECT * FROM student WHERE score>80 GROUP BY sex;

  

--从学生表查询成绩60-80并按性别和年龄分组

SELECT * FROM student WHERE score BETWEEN 60 AND 80 GROUP BY sex,age;

  

4.2 聚合函数

·COUNT()：统计满足条件的数据总条数

示例：从学生表查询成绩在80分以上的学生人数

SELECT COUNT(*) FROM student WHERE score>80;

SELECT COUNT(*) total FROM student WHERE score>80;

·SUM()：只能用于数值类型的字段或者表达式，计算该满足条件的字段值的总和

示例：从学生表查询不及格的学生人数和总成绩

SELECT COUNT(*),SUM(score) FROM student WHERE score<60;

SELECT COUNT(*) totalCount,SUM(score) totalScore FROM student WHERE score<60;

·AVG()：只能用于数值类型的字段或者表达式，计算该满足条件的字段值的平均值

示例：从学生表查询男生、女生、其他类型的学生的平均成绩

SELECT sex,AVG(score) FROM student GROUP BY sex;

--SELECT name,sex,AVG(score) FROM student GROUP BY sex;

--SELECT * AVG(score) FROM student GROUP BY sex;

.MAX()：只能用于数值类型的字段或者表达式，计算该满足条件的字段值的最大值

示例：从学生表查询学生的最大年龄

SELECT MAX(age) FROM student;

SELECT name,age FROM student WHERE age = (SELECT MAX(age) FROM student);

MINO：只能用于数值类型的字段或者表达式，计算该满足条件的字段值的最小值

示例：从学生表查询学生的最低分

SELECT MIN(score) FROM student;

  

4.3分组查询结果筛选

SELECT ALL/DISTINCT*|字段名1AS别名1[,字段名1AS别名1，···，字段名nAS别名n]FROM表名WHERE查询条件GROUP

BY字段名1，字段名2,..，字段名n HAVING 筛选条件

示例：从学生表查询年龄在20~30之间的学生信息并按性别分组，找出组内平均分在60分以上的组

SELECT * FROM student wHERE age BETwEEN 20 AND 30 GROUP BY sex HAVING avg(score)>74;

  

5.排序

SELECTALL/DISTINCT*|字段名1AS别名1[,字段名1AS别名1，···，字段名nAS别名n]FROM表名WHERE查询条件ORDER

BY字段名1ASC|DESC，字段名2ASC|DESC,··.,字段名nASC|DESC

ORDER BY必须位于WHERE条件之后。

1

示例：从学生表查询年龄在18~30岁之间的学生信息并按成绩从高到低排列，如果成绩相同，则按年龄从小到大排列

手机尾号7714用户-u_68db6e73ed3a

SELECT * FROM student wHERE age BETwEEN 18 AND 30 ORDER BY score DESC,age ASC;

  

6.分页

SELECTALL/DISTINCT*|字段名1AS别名1[,字段名1AS别名1，···，字段名nAS别名n]FROM表名WHERE查询条件LIMIT偏

移量，查询条数

LIMIT的第一个参数表示偏移量，也就是跳过的行数。

LIMIT的第二个参数表示查询返回的最大行数，可能没有给定的数量那么多行。

示例：从学生表分页查询成绩及格的学生信息，每页显示3条，查询第2页学生信息

SELECT * FROM student WHERE score>=60 LIMIT 3，3;

注意：

sql

如果一个查询中包含分组、排序和分页，那么它们之间必须按照分组>排序>分页的先后顺序排列。

  
  

CREATE TABLE IF NOT EXISTS emp(

)ENGINE=InnoDB CHARSET=UTF8 COMMENT'员工表'