# SQL

## 索引

索引：`ALTER TABLE students`
`ADD INDEX idx_score(name,score);`
唯一索引：`ALTER TABLE students`
`ADD UNIQUE INDEX uni_name UNIQUE(name);`

## 查询数据

### 基本查询

`SELECT * FROM <表名>;`可以查询一个表的所有行和所有列的数据

### 条件查询

`SELECT * FROM student WHERE score >= 80;`根据条件查询数据   节省内存和带宽
`SELECT * FROM students WHERE score >= 80 AND gender = 'M';` 并列查询
`SELECT * FROM students WHERE score >= 80 OR gender = 'M';` 条件查询  满足一条即可
`SELECT * FROM students WHERE NOT class_id = 2;` NOT查询
`SELECT * FROM students WHERE (score < 80 OR score > 90) AND gender = 'M';`复合查询

优先级：NOT AND OR;
判断不相等表达式：score<>80
LIKE判断相似：name LIKE 'ab%'   name LIKE '%bc%'

### 投影查询

`SELECT id, score, name FROM student;`  只查询3列
`SELECT id, score point, name FROM student;` 改名后查询
`SELECT id, score point, name FROM student WHERE gender = 'M';` 投影条件查询

命名时若使用中文 则应 `分数` 或者 [分数]

### 排序

`SELECT id, name, score FROM students ORDER BY score;` 升序
`SELECT id, name, score FROM students ORDER BY score DESC` 降序
`SELECT id, name, score FROM students ORDER BY score DESC, gender` 先按score降序 若有相同，然后按gender升序
`SELECT id, name, score FROM students WHERE class_id = 1 ORDER BY score DESC` 结合条件查询 排序的语句在其后

### 分页查询

`SELECT id, name, gender, score FROM students ORDER BY score DESC LIMIT 3 OFFSET 0;`  每页3行 索引是从0开始的

注意
OFFSET是可选的，如果只写`LIMIT 15`，那么相当于`LIMIT 15 OFFSET 0`。

在MySQL中，`LIMIT 15 OFFSET 30`还可以简写成`LIMIT 30, 15`。

使用`LIMIT <M> OFFSET <N>`分页时，随着N越来越大，查询效率也会越来越低。

小结
使用`LIMIT <M> OFFSET <N>`可以对结果集进行分页，每次查询返回结果集的一部分；

分页查询需要先确定每页的数量和当前页数，然后确定LIMIT和OFFSET的值。
`SELECT class_id,gender,AVG(score) FROM students GROUP BY class_id,gender;`

### 聚合查询

`SELECT count(*) FROM students;` 查询总记录
`SELECT count(*) num FROM students;` 重命名
`SELECT count(*) boys FROM students WHERE gender = 'M';` 聚合条件查询

函数     说明
SUM      计算某一列的合计值，该列必须为数值类型
AVG      计算某一列的平均值，该列必须为数值类型
MAX      计算某一列的最大值
MIN      计算某一列的最小值

要特别注意：如果聚合查询的WHERE条件没有匹配到任何行，COUNT()会返回0，而SUM()、AVG()、MAX()和MIN()会返回NULL；

`SELECT class_id, gender, COUNT(*) num FROM students GROUP BY class_id, gender;` 分组聚合查询

### 多表查询

`SELECT * FROM students, classes;`

    SELECT 
         students.id sid,
         students.name,
         students.gender,
         students.score,
         classes.id cid
         classes.name cname
         FROM students, classes;

    SELECT
        s.id sid,
        s.name,
        s.gender,
        s.score,
        c.id cid,
        c.name cname
        FROM students s, classes c;
    
    SELECT
        s.id sid,
        s.name,
        s.gender,
        s.score,
        c.id cid,
        c.name cname
        FROM students s, classes c
    WHERE s.gender = 'M' AND c.id = 1;

### 连接查询

1. 内连接(INNER JOIN)：`SELECT s.id, s.class_id, c.name class_name, s.gender, s.score FROM students s INNER JOIN classes c ON s.class_id = c.id;`

2. 外连接(OUTER JOIN)：`SELECT s.id, s.class_id, c.name class_name, s.gender, s.score FROM students s RIGHT OUTER JOIN classes c ON s.class_id = c.id;`

3. `FULL OUTER JOIN：SELECT s.id, s.name, s.class_id, c.name class_name, s.gender, s.score FROM students s FULL OUTER JOIN classes c ON s.class_id = c.id;`

小结：

有`RIGHT OUTER JOIN`，就有`LEFT OUTER JOIN`，以及`FULL OUTER JOIN`。它们的区别是：

`INNER JOIN`只返回同时存在于两张表的行数据，由于students表的class_id包含1，2，3，classes表的id包含1，2，3，4，所以，INNER JOIN根据条件`s.class_id = c.id`返回的结果集仅包含1，2，3。

`RIGHT OUTER JOIN`返回右表都存在的行。如果某一行仅在右表存在，那么结果集就会以NULL填充剩下的字段。

`LEFT OUTER JOIN`则返回左表都存在的行。如果我们给students表增加一行，并添加class_id=5，由于classes表并不存在id=5的行，所以，LEFT OUTER JOIN的结果会增加一行。

最后，我们使用`FULL OUTER JOIN`，它会把两张表的所有记录全部选择出来。

## 修改数据

### INSERT

`INSERT INTO students (class_id, name, gender, score) VALUES (2, '大牛', 'M', 80);` 单条插入

多条插入
    INSERT INTO students (class_id, name, gender, score) VALUES
      (1, '大宝', 'M', 87),
      (2, '二宝', 'M', 81);

### UPDATE

`UPDATE students SET name='大牛', score=66 WHERE id=1;`
`UPDATE students SET name='大牛', score=66 WHERE id>=5 AND id<=7;` 一次更新多条结果
`UPDATE students SET score=score+10 WHERE score<80;`

注意：
不使用WHERE时，UPDATE会把所有的表中数据都修改; 所以最好先用SELECT语句来测试WHERE条件是否筛选除了期望的记录集，然后再用UODATE更新。

### DALETE

`DELETE FROM students WHERE id=1;`

注意：和UPDATE类似，不带WHERE条件的DELETE语句会删除整个表的数据。

## 管理MySQL

进入Mysql：`mysql -u root -p`  离开：`exit;`

1.`SHOW DATABASES;` 显示所有数据库
2.`CREATE DATABASE test;` 创建数据库
3.`DROP DATABASE test;` 删除数据库
4.`USE test;` 选择进入数据库
5.`SHOW TABLES;` 显示数据表
6.`DESC students;` 查看某个数据表的结构
7.`SHOW CREATE TABLE students;` 显示创建数据表时的语句
 CREATE TABLE `students` (
 `id` bigint(20) NOT NULL AUTO_INCREMENT,
 `class_id` bigint(20) NOT NULL,
 `name` varchar(100) NOT NULL,
 `gender` varchar(1) NOT NULL,
 `score` int(11) NOT NULL,
 PRIMARY KEY (`id`)
 );

8.`DROP TABLE students;` 删除数据表
9.`ALTER TABLE students ADD COLUMN birth VARCHAR(10) NOT NULL;` 给数据表新增一列
10.`ALTER TABLE students CHANGE COLUMN birth birthday VARCHAR(20) NOT NULL;` 给数据表的某一列改名
11.`ALTER TABLE students DROP COLUMN birthday` 删除数据表的某一列

## 实用SQL语句

在编写SQL时，灵活运用一些技巧，可以大大简化程序逻辑。

插入或替换
如果我们希望插入一条新记录（INSERT），但如果记录已经存在，就先删除原记录，再插入新记录。此时，可以使用REPLACE语句，这样就不必先查询，再决定是否先删除再插入：

`REPLACE INTO students (id, class_id, name, gender, score) VALUES (1, 1, '小明', 'F', 99);`
若id=1的记录不存在，REPLACE语句将插入新记录，否则，当前id=1的记录将被删除，然后再插入新记录。

插入或更新
如果我们希望插入一条新记录（INSERT），但如果记录已经存在，就更新该记录，此时，可以使用INSERT INTO ... ON DUPLICATE KEY UPDATE ...语句：

`INSERT INTO students (id, class_id, name, gender, score) VALUES (1, 1, '小明', 'F', 99) ON DUPLICATE KEY UPDATE name='小明', gender='F', score=99;`
若id=1的记录不存在，INSERT语句将插入新记录，否则，当前id=1的记录将被更新，更新的字段由UPDATE指定。

插入或忽略
如果我们希望插入一条新记录（INSERT），但如果记录已经存在，就啥事也不干直接忽略，此时，可以使用INSERT IGNORE INTO ...语句：

`INSERT IGNORE INTO students (id, class_id, name, gender, score) VALUES (1, 1, '小明', 'F', 99);`
若id=1的记录不存在，INSERT语句将插入新记录，否则，不执行任何操作。

快照
如果想要对一个表进行快照，即复制一份当前表的数据到一个新表，可以结合CREATE TABLE和SELECT：

-- 对class_id=1的记录进行快照，并存储为新表students_of_class1:
`CREATE TABLE students_of_class1 SELECT * FROM students WHERE class_id=1;`
新创建的表结构和SELECT使用的表结构完全一致。

写入查询结果集
如果查询结果集需要写入到表中，可以结合INSERT和SELECT，将SELECT语句的结果集直接插入到指定表中。

例如，创建一个统计成绩的表statistics，记录各班的平均成绩：

CREATE TABLE statistics (
    id BIGINT NOT NULL AUTO_INCREMENT,
    class_id BIGINT NOT NULL,
    average DOUBLE NOT NULL,
    PRIMARY KEY (id)
);
然后，我们就可以用一条语句写入各班的平均成绩：

`INSERT INTO statistics (class_id, average) SELECT class_id, AVG(score) FROM students GROUP BY class_id;`
确保INSERT语句的列和SELECT语句的列能一一对应，就可以在statistics表中直接保存查询的结果：

> SELECT * FROM statistics;
+----+----------+--------------+
| id | class_id | average      |
+----+----------+--------------+
|  1 |        1 |         86.5 |
|  2 |        2 | 73.666666666 |
|  3 |        3 | 88.333333333 |
+----+----------+--------------+
3 rows in set (0.00 sec)
强制使用指定索引
在查询的时候，数据库系统会自动分析查询语句，并选择一个最合适的索引。但是很多时候，数据库系统的查询优化器并不一定总是能使用最优索引。如果我们知道如何选择索引，可以使用FORCE INDEX强制查询使用指定的索引。例如：

`SELECT * FROM students FORCE INDEX (idx_class_id) WHERE class_id = 1 ORDER BY id DESC;`
指定索引的前提是索引idx_class_id必须存在。

------------------------------------------------------------------------------------------------------------

参考文献：廖雪峰老师的官方网站：<https://www.liaoxuefeng.com/>

------------------------------------------------------------------------------------------------------------
