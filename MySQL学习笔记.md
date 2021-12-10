# 安装

安装成功截图

![image-20211128171146810.png](https://s2.loli.net/2021/12/09/HRsJdnEwTYgNBmD.png)

路径

C:\Program Files\MySQL\MySQL Server 8.0\bin

# 几个概念

## **数据库**

database ，简称：**DB**。按照一定格式存储数据的一些文件的组合。

顾名思义：存储数据的仓库，实际上就是一堆文件。这些文件中存储了具有特定格式的数据。    

## **数据库管理系统**

databasemanagement，简称：**DBMS**。//类似于mysql的软件

数据库管理系统是专门用来管理数据库中的数据的，数据库管理系统可以对数据库当中的数据进行增删改查（tools）。MySQL属于其中一种

## **SQL**

结构化查询语言

程序员编写SQL语句，然后DBMS负责执行SQL语句，最终完成数据库中数据的增删查改工作

**主要学习SQL语句**，然后在DBMS中使用（MySQL，DB2，Oracle(甲骨文的软件/好/贵)...）

**关系**：

DBMS--执行-->sql--操作-->DB

# MySQL的服务

## 路径

控制面板\系统和安全\管理工具 找到服务

![image-20211202174139697.png](https://s2.loli.net/2021/12/09/4iHgn5BUj3oq68a.png)


## 启动与关闭服务

net stop MySQL

net start MySQL

# 基本知识

## 启动和登录

登录

1.cd C:\Program Files\MySQL\MySQL Server 8.0\bin

2.mysql  -uroot -p123456（显示密码的形式）

​    mysql -uroot  -p              （不显示密码，回车后再输入密码）

退出

1.exit

2.exit执行后，在执行cls可以清空命令行

## MySQL的常用命令

1. 退出mysql： exit
2.  查看MySQL中有哪些数据库： show databases;   
![image-20211202211318201.png](https://s2.loli.net/2021/12/09/DazHlsq7TnBb4mF.png)
​       MySQL默认自带数据库有四个

   3.使用数据库：use 数据库名;

4. 创建数据库：create database  要创建的数据库名 ；

5. mysql> select version(); 查询版本号

6. mysql> select database();查询当前使用的数据库

7. 查看某个数据库下有那些表： show tables；

   **ps**：1.以上命令不区分大小写,此外命令得加分号

   ​		2.不见分号不执行，分号表示结束

   ​		3.\c可用来终止一条命令的输入

## 基本单元：表（table）

数据库中以表的形式储存数据，任何一张表都有行和列

行（row）：被称为数据/记录

列（column）：被称为字段

每一个字段都有：字段名，数据类型，约束等特性。（后期说）（唯一性约束添加后该字段数据不能重复）

## MySQL概述

MySQL是mysqlAB公司的，mysqlAB被sun收购，sun被Oracle收购

## SQL语句的分类(必须记)

**DQL**：数据查询语言（凡是带有select关键字的都是查询语句）

**DML**: 数据操纵语言（对表中数据进行增删改）

​			insert:增

​			delete:删

​			update:改

DDL：数据定义语言（操作表的结构）

​			create：增

​			drop：删

​			alter：改

TCL：事务控制语言

​			包括：事务提交：commit

​						事务回滚：rollback

DCL：数据控制语言

​			授权：grant

​			撤销权限：revoke...

## 导入数据

先创建数据库，再选择数据库，最后导入数据

注意：路径中不要有中文 （我这里导入的时候好像有中文）

```mysql
mysql> source C:\Users\郝锦杰\Desktop\木犀\MySQL学习资料\document\bjpowernode.sql  //导入数据
```

## 关于导入的这几张表

 ![image-20211203080432390.png](https://s2.loli.net/2021/12/09/scCPXDlpJSKoULe.png)

dept：部门表

emp：员工表

salgrade：工资等级表

## 查看表中数据

**select * from 表名;**  （统一使用此SQL语句）（*代表所有，前面句代表查询所有结构）

 ![image-20211203080807621.png](https://s2.loli.net/2021/12/09/kBQM9Eav8SIZA5f.png)
![image-20211203080827396.png](https://s2.loli.net/2021/12/09/DXbwI6v9YGgxBJO.png)

![image-20211203080849080.png](https://s2.loli.net/2021/12/09/aLOw5kEP1ihRo2s.png)
## desc 只看表的结构

不看表中数据，只看**表的结构**：**desc 表名；** 

部门编号/部门名字/地理位置

![image-20211203081334442.png](https://s2.loli.net/2021/12/09/QgC4Ho8bktujhWp.png)

员工编号/

![image-20211203081402014.png](https://s2.loli.net/2021/12/09/7nKjOIJ4ENDialA.png)

![image-20211203081418401.png](https://s2.loli.net/2021/12/10/3XyRnChfF2mGPt4.png)

varchar是字符型相当于string

# 简单查询DQL（SQL）

## DQL（查询语句）(基础查询)

#### 查询一个字段

select 字段名 from 表名；

<!--select from是关键字。-->

<!--字段名和表名是标识符。-->

eg：查询部门名字

![image-20211203083127717.png](https://s2.loli.net/2021/12/10/jV1Z8WnqLbcwQlM.png)
#### 查询两个以上的字段

使用逗号隔开

eg：查询部门编号和部门名

```mysql
	select deptno,dname from dept;
```

#### 查询所有字段

1.把每个字段都写上:select a,b,c,... from tablename;

```mysql
select * from dept; 
```

2.可以用 *：select * from dept;  缺点：效率低，可行性差。实际开发中不建议，自己玩可以

#### 给查询列起别名

使用as关键字起别名：

eg：mysql> select deptno,dname as deptname from dept;

注意：只是将查询结果列明显示为deptname，原表列名还叫：dname

​     	  select语句永远不会进行修改操作（只查询）

![image-20211203083934076.png](https://s2.loli.net/2021/12/10/paFz2YyuLlX3tmk.png)

此外as关键字可以省略

eg：mysql> select deptno,dname deptname from dept;

​         <!--dname deptname后面这个是前面的别名-->

![image-20211203084417220.png](https://s2.loli.net/2021/12/10/gyUXnFER4qsDH7x.png)

如果别名里有空格：用单引号或双引号将别名括起来

eg：mysql> select deptno,dname 'dept name' from dept;

​		mysql> select deptno,dname  "dept name" from dept;


![image-20211203084832239.png](https://s2.loli.net/2021/12/10/iKZgs9aftSeyRwW.png)

<!--在所有数据库中，字符串用单引号括起来是标准，双引号在mysql中可用但在Oracle中不可用-->

#### 计算员工年薪

select ename,sal from emp;(先查询有哪些员工及其对应工资)

![image-20211203085433903.png](https://s2.loli.net/2021/12/10/P81g5AzQjs2uaLy.png)

select ename,sal*12 from emp; (在执行计算的命令)//(字段可以使用数学表达式)

![image-20211203085550176.png](https://s2.loli.net/2021/12/10/zDAsXGQUF1huemv.png)

select ename,sal*12 as yearsal from emp; //起别名

```mysql
select ename,sal*12 as '年薪' from emp;   //别名是中文用单引号括起来
```

## 条件查询

#### 定义

查询表中符合条件的数据

#### 语句

select

​	字段1，字段2，

from

​	表名

where

​	条件；

#### 条件类型

##### = 等于

eg：查询工资等于800的员工的姓名和编号

​		select empno,ename from emp where sal = 800;

​		查询SMITH的编号和薪资

​		select  empno,sal from emp where ename='SMITH';

##### <>或!= 不等于

eg：查询工资不等于800的员工的姓名和编号

​		select empno,ename from emp where sal != 800;

​    	select empno,ename from emp where sal <> 800;

##### < 小于

eg：查询工资小于2000的员工的姓名和编号和工资

​		select empno,ename,sal from emp where sal < 2000;

##### <= 小于等于

eg：查询工资小于等于3000的员工的姓名和编号和工资

​		select empno,ename,sal from emp where sal <= 3000;

##### 还有： > 大于    >= 大于等于

eg：查询工资大于等于3000的员工的姓名和编号和工资

​		select empno,ename,sal from emp where sal >= 3000;

##### between ... and ...

eg：查询薪资在2450和3000之间的员工信息包括2450和3000

select empno,ename,sal from emp where sal >=2450 and sal <=3000;		

select empno,ename,sal from emp where sal between 2450 and 3000;(between and左小右大,且为闭区间)

##### 关于null

练习题：查询那些员工的津贴或补助为null

~~select ename,comm from emp where comm = null;~~     (数据库中的null不能使用等号衡量，得用**is null**或**is not null**)

select ename,comm from emp where comm is null;

查询那些员工的津贴或补助不为null

select ename,comm from emp where comm is not null;  

##### and 并且

查询工作岗位是manager并且工资大于2500的员工信息

select empno,ename,job,sal from emp where job = 'manager' and sal >2500;

##### or 或者

eg：查询工作岗位是manager和salesman的员工

​		select empno,ename,job from emp where job = 'manager'  or job = 'salesman';

##### 关于and和or的优先级

and优先级高于or

eg：查询工资大于2500，并且部门编号为10和20的员工的所有数据

~~select * from emp where sal > 2500 and deptno = 10 or deptno = 20;~~    没有考虑到and优先于or

更正：

```mysql
select * from emp where sal > 2500 and (deptno = 10 or deptno = 20); 
```

如果想让or先执行记得加**小括号**

以后如果不确定优先级，就加小括号就行了

##### in 包含 相当于多个or

eg：查询工作岗位是manager和salesman的员工

​		select empno,ename,job from emp where job = 'manager'  or job = 'salesman';

​        select empno,ename,job from emp where job in ('manager','salesman');

注意：in不是一个区间，in里包含的是具体的值。  （区间是between and）

​			查询薪资是800或5000的员工全部信息

​		   select * from emp where sal in (800,5000);  

​			查询薪资不是800或5000的员工全部信息

​		   select * from emp where sal not in (800,5000);  

##### not

not可以取非主要用在is 和 in 中

eg： is null/is not null    in/not in 

## 模糊查询

"**like**"

支持%和下划线查询：

%:匹配任意多个字符

_:下划线匹配任意单个字符

eg：找出名字中含有o的员工名字

​		 select ename from emp where ename like '%o%';  ![image-20211203152651377.png](https://s2.loli.net/2021/12/10/2pzOlS7eRoUZHLi.png)

找出名字中以T结尾的员工名字

​		 select ename from emp where ename like '%T';  

找出名字中以K开始的员工名字

​		 select ename from emp where ename like 'K%';  

找出名字第二个字母是A的员工名字

​		 select ename from emp where ename like '_A%';  

找出名字中第三个字母是R的员工名字

​		 select ename from emp where ename like '__R%';  

找出名字中有下划线的名字    （注意：这里需要一个转义字符\\)

​		 select ename from emp where ename like **'%\\_%';**  

## 排序

关键字：**order  by**

### 升序

```mysql
select ename,sal from emp order by sal ;   //默认是升序
```

select ename,sal from emp order by sal asc ; //指定升序（这条命令和上一条等效） 

![image-20211203195117593.png](https://s2.loli.net/2021/12/10/NcFvJtnUkrDQRb3.png)
### 降序

eg:指定按照薪资降序

```mysql
select ename,sal from emp order by sal desc; //默认后面加desc即为降序
```

![image-20211203195305619.png](https://s2.loli.net/2021/12/10/XxKMmlu61a8PnzQ.png)
### 按多个字段排序

查询员工名字和薪资，要求按照薪资升序，若薪资一样，再按名字升序排列

```mysql
select ename,sal from emp order by sal asc,ename asc; //sal在前起主导，只有sal相同时才考虑ename
```

### 根据字段位置排序

select ename,sal from emp order by 2; //不建议这么写

### 综合案例

找出工资在1250到3000之间的员工信息，要求按照薪资降序排列

select ename,sal from emp where sal between 1250 and 3000 order by sal desc;

![image-20211203200538389.png](https://s2.loli.net/2021/12/10/6srtuvlI3eqgFLV.png)

语句执行顺序：from--where--select--order

## 数据处理函数

### 相关概念

数据处理函数又被称为单行处理函数

单行处理函数特点：一个输入对应一个输出

与其相对的是：多行处理函数

多行处理函数特点：多个输入对应一个输出

### 类别

#### lower 转小写

​			select lower(ename) from emp;

​         	可以显示别的字段名：

​			select lower(ename) as ename from emp;

![image-20211203201629641.png](https://s2.loli.net/2021/12/10/AKBzokDcPVRi73w.png)

#### upper 转大写 

用法同lower

#### substr 取子串

(substr(被截取的字符串，起始下标，截取的长度)

eg:~~select substr(ename, 0 ,1)  as ename from emp;~~ 

​	select substr(ename, 1 ,1)  as ename from emp; 

注意：起始下标从1开始，没有0

例题：找出员工名字第一个字母是A的人的名字

方法一：模糊查询：select ename from emp where ename like 'A%';

方法二：substr函数： select ename from emp where substr(ename,1,1) = 'A';  

#### concat 拼接字符串

eg: select concat(empno,ename) from emp; 


![image-20211203203451401.png](https://s2.loli.net/2021/12/10/bPyBdqHfVvlCh7Y.png)

#### length 取长度

select length(ename) enamelength from emp;

![image-20211203203749637.png](https://s2.loli.net/2021/12/10/15LFhUgRm7ntrCi.png)

#### trim 去空格

eg:select * from emp where ename = trim( '  KING           ');

#### round 四舍五入

select 字段名 from 表名；	                                        /	select  'abc' from emp;

select 后面可以加某个表的字段名（等同于变量名），也可以跟字面量/字面值（数据(需要加引号)）

eg：保留整数：select round(1236.567,0) as result from emp;

![image-20211203205018351.png](https://s2.loli.net/2021/12/10/m6fWe3AqXNRn5UE.png)
保留1位小数：select round(1236.567,1) as result from emp;

保留2位小数：select round(1236.567,2) as result from emp;

保留到十位：select round(1236.567,-1) as result from emp;

保留到百位：select round(1236.567,-2) as result from emp;

#### rand() 生成随机数

生成随机数：select rand() from emp;


![image-20211203205751726.png](https://s2.loli.net/2021/12/10/eN8qGp49skK1TXb.png)
生成一百以内的随机数：select round( rand()*100, 0 ) from emp;

![image-20211203205811746.png](https://s2.loli.net/2021/12/10/DPE6pmVngTlrQWv.png)

#### ifnull 空处理函数

可以将null转换为一个具体值，专门处理空值

数据库中有null参与的运算最终结果都是null，所以引进ifnull函数，避免这种情况

用法: ifnull(数据，被当作哪个值)

如果数据是null时把这个数据结构当做哪个值

eg：计算年薪：

```mysql
select ename, (sal + ifnull(comm, 0))*12  as yealsal from emp;
```

//如果数据是null时把这个数据结构当做0来处理

#### case...when..then..when..then..else..end

eg:当员工工作岗位是manager时上调10%，工作岗位是salesman时上调50%，其他正常。

（不改变数据库，只是将查询结果显示为工资上调）

select ename,job ,sal,(case job when 'manager' then sal*1.1 when 'salesman' then sal *1.5 else sal end) as newsal from emp;

![image-20211203211525928.png](https://s2.loli.net/2021/12/10/Wx6iV134ezRADMl.png)
## 分组函数

多行处理函数：输入多行最终输出一行

**max求最大值		min求最小值		sum求和		avg求平均数		count计数**

注意：分组函数必须先分组再使用，若没有对数据分组，整张表默认为一组

找出最高工资

select max(sal) from emp;

找出最低工资

select min(sal) from emp;

计算工资和：

select sum(sal) from emp;

计算平均工资：

select avg(sal) from emp;

计算员工数量:

select count(ename) from emp;

分组函数使用的注意事项：

1.分组函数自动忽略null，不需要提前对null处理  //null就是空

​	eg：select sum(comm) from emp;

2.分组函数中count(*)和count(具体字段)的区别

​	count(具体字段)：统计该字段下所有不为null的元素总数

​	count(*): 统计表当中的总行数 //因为不会有一行全为null

3.分组函数不能直接使用在where语句中

​	~~select ename,sal from emp where sal > min(sal);~~    

4.所有分组函数可以组合起来一起用

​	eg： select sum(sal),max(sal),min(sal),avg(sal),count(sal) from emp;

## **分组查询**（重要）

先分组，再对每一组数据进行操作

#### 语句 (group by)

```mysql
select
		...
from
		...
group by
		...
```

将之前的关键字全部组合

```mysql
select
			...
from
			...
where
			...
group by
			...
order by
			...
```

以上关键字顺序不能颠倒，需要记忆

#### 执行顺序

第一步.from 		  选表

第二步.where		 过滤     （where后面用不了分组函数，因为它在分组之前执行）

第三步.group by    分组

第四步.select          查询

第五步.order by     排序输出

#### 例子分析

select ename,sal from emp where sal > min(sal); 	//报错

因为分组函数在使用时必须先分组再使用，此处函数用在where后面，where执行的时候还没有分组，所以where后面不能出现分组函数

select sum (sal) from emp;

这个没group by，但默认整张表分为一组， 而且select 在group by 后面执行

#### 找出每个工作岗位的工资和

按照工作岗位分组，然后对工资求和

select job,sum(sal) from emp group by job;

~~select ename,job,sum(sal) from emp group by job;~~// 该语句在mysql中可执行，但无意义，在Oracle中会报错

重点结论：

在一条select语句中，如果有group  by 语句的话，select后面只能跟：参加分组的字段，以及分组函数。其他一律不能跟。

#### 找出每个部门的最高薪资

按照部门编号分组，求每一组的最大值

select deptno,max(sal) from emp group by deptno;

#### 找出每个部门不同工作岗位的最高薪资

先找出数据：select ename,sal,job,deptno from emp;

![image-20211203223142071.png](https://s2.loli.net/2021/12/10/vphWwFjs8u1GMSK.png)

#### **按两个字段进行分组**

select deptno,job,max(sal) from emp group by deptno,job order by deptno;

技巧：两个字段联合成一个字段看

#### having 语句

使用having语句可对分组后的数据进行过滤

where过滤在group by前执行，如果想在分组之后过滤的话，可以使用having语句

##### 找出每个部门的最高薪资，要求显示最高薪资大于3000的

找出每个部门最高薪资，再筛选：

select deptno,max(sal) from emp group by deptno having max(sal) > 3000;//该语句执行效率较低

尝试先筛选，再分组找出薪资:

select deptno,max(sal) from emp group by deptno where sal > 3000;

select deptno,max(sal) from emp where sal > 3000 group by deptno ;

优化策略：**where和having优先选择where，where无法完成的，用having**

不能用where的例子：

找出每个部门的平均薪资，要求显示平巨额薪资高于2500的

select  deptno,avg(sal) from emp group by deptno having avg(sal) >2500;

## 对以上所学内容大总结

到目前单表的查询已学完

### 语句

```mysql
select
		...
from
		...
where
		...
group by
		...
having
		...
order by
		...
```

### 执行顺序

第一步.from 		  选表

第二步.where		 过滤，筛选     （where后面用不了分组函数，因为它在分组之前执行）

第三步.group by    分组

第四步.having        分组后可用having再次筛选

第四步.select          查询

第五步.order by     排序输出

eg：找出每个岗位的平均薪资，要求显示平均薪资大于1500的，除manager岗位以外，要求按平均薪资降序排列

select job,avg(sal) as avgsal from emp  where job <> 'manager' group by job having avg(sal) > 1500 order by avgsal desc;

![image-20211204084053372.png](https://s2.loli.net/2021/12/10/xipgJlVdjK6ry1f.png)

select
		job,avg(sal) as avgsal

from
		emp

where
		job <> 'manager'

group by
		job

having
		avg(sal) > 1500

order by
		avgsal desc;

## 去除重复（distinct）

注意：原表数据不会修改，只是把查询结果去重

关键字：distinct

eg: 

```mysql
select distinct job from emp;
```

~~select ename distinct job from emp;~~   //distinct 只能出现在所有字段之前

```mysql
select distinct job，deptno  from emp; //用在两个字段之前，表示两个字段联合起来去重
```

统计工作岗位的数量：

```mysql
select count(distinct(job)) from emp;   //去重后，可以用分段函数
```

## 连接查询（超级重点）

### 定义

多张表联合起来查询数据称为连接查询（从一张表中单独查询叫做单表查询）

### 连接查询分类

1.根据年代分类

SQL92：1992年出现的语法

SQL99：1999年出现的语法（重点学习SQL99）

2.根据表连接的方式分类

内连接

​		等值连接

​		非等值连接

​		自连接

外连接

​		左外连接（左连接）

​		右外连接（右连接）

全连接（不讲）(A,B两张表都是主表)

### 笛卡尔积现象

#### 定义及示例

当两张表表进行连接查询，没有任何条件限制时，最终查询结果条数是，两张表条数的乘积



![image-20211205103430525.png](https://s2.loli.net/2021/12/10/2RgyaeunG8EvCDh.png)
![image-20211205103605348.png](https://s2.loli.net/2021/12/10/qrkyEj4g5KeDzTU.png)

查询每个员工所在的部门名称:

```mysql
select ename,dname from emp,dept;
```
![image-20211205104125705.png](https://s2.loli.net/2021/12/10/2uJRbxLsdOWNZ8w.png)

​                                                                  ......

一共出现14*4=56条数据

**如何避免笛卡尔积现象**

连接时加条件，满足该条件的被筛选出来

```mysql
select ename,dname from emp,dept  where emp.deptno = dept.deptno;
```

注意：匹配次数没有减少，还是56次，只不过进行了4选1

可以给表**起别名**，提高效率

最终解法：

```mysql
select 
	e.ename,d.dname
from
	emp e,dept d
where
	e.deptno = d.deptno;   //SQL92语法
```
![image-20211205105242897.png](https://s2.loli.net/2021/12/10/MOPRGkDwHc2r84U.png)

通过笛卡尔积现象，可以看出表的连接次数越多效率越低，应尽量降低表的连接次数

### 内连接

#### 内连接之等值连接

等值连接（关系是等量关系）

sql92语法：

```mysql
select 
	e.ename,d.dname
from
	emp e,dept d
where
	e.deptno = d.deptno;   
```

缺点：结构不清晰，标的连接条件和后期进一步筛选的条件，都放在where后面

sql99语法：

```mysql
select 
	...
from
	a
join
	b
on
	a和b的连接条件
where
	筛选条件
```

案例：

```mysql
select 
	e.ename,d.dname
from
	emp e
inner join
	dept d
on
	e.deptno = d.deptno;  
//inner可以省略，带着inner可读性更高，可看出是内连接	
select 
	e.ename,d.dname
from
	emp e
join
	dept d
on
	e.deptno = d.deptno;   
```

优点：表连接条件独立，连接后进一步筛选，再往后继续添加where

#### 内连接之非等值连接

非等值连接：表连接条件条件不是等量关系

eg：找出每个员工的薪资等级，要求显示员工名，薪资，薪资等级

![image-20211205132813191.png](https://s2.loli.net/2021/12/10/FrnY95NTfbQ6uip.png)

显然：若是没有条件限制，根据笛卡尔积现象将会显示70条记录

正确代码演示:

```mysql
select 
	e.ename,s.grade
from
	emp e
join
	salgrade s
on
	e.sal between s.losal and s.hisal;
```

![image-20211205133239466.png](https://s2.loli.net/2021/12/10/9lWYZU7JVatNOLr.png)

#### 内连接之自连接

自连接：一张表看成两张表

eg：查询员工的上级领导，要求显示员工名和对应的领导名

ps:没有King，King无领导

![image-20211205133744763.png](https://s2.loli.net/2021/12/10/gJlIOm943FRSquv.png)![image-20211205134727735.png](https://s2.loli.net/2021/12/10/lkwVWrgQ7aZsfqu.png)![image-20211205133744763.png](https://s2.loli.net/2021/12/10/gJlIOm943FRSquv.png)

技巧:一张表看成两张表

```mysql
select 
	a.ename as '员工名', b.ename as '领导名'
from
	emp a
join
	emp b
on
	a.mgr = b.empno;		//员工的领导编号等于领导的员工编号
```

### 外连接

外连接中两张表连接出现了主次关系

ps：开发中外连用的较多

eg1：查询每个员工的职业，并把所有职业显示出来
![image-20211205135226054.png](https://s2.loli.net/2021/12/10/mXAQU16DJHzf39g.png)![image-20211205135241752.png](https://s2.loli.net/2021/12/10/75f1BPnEixWlmqe.png)

内连接的特点：将完全能够匹配上这个条件的数据查询出来（A,B 两张是平等关系，没主次之分）

```mysql
//内连接：
select 
	e.ename,d.dname
from
	emp e
join
	dept d
on
	e.deptno = d.deptno;   
//右外连接:
select 
	e.ename,d.dname
from
	emp e 
right outer join 		//左右连接中outer可以省略，带着可读性强
	dept d
on
	e.deptno = d.deptno;   
//这条命令把dname中的所有数据都显示出来
```

![image-20211205135823261.png](https://s2.loli.net/2021/12/10/azBPJbF3kqOscUH.png)![image-20211205135843337.png](https://s2.loli.net/2021/12/10/wrdUPlTBg7548Qp.png)

right：表示将join关键字右边的这张表看成主表，主要是为了将这张表的数据全部查询出来，捎带着关联查询左边的表

```mysql
//外连接(左外连接)：
select 
	e.ename,d.dname
from
	dept d 
left join
    emp e
on
	e.deptno = d.deptno;   
```

注意：带有right的是右外连接，又叫做右连接

​			带有left的是左外连接，又叫做左连接

​			任意 左连接 都可与 右连接 相互转化

ps：inner和outer其实没什么大的用处，主要看有没有right和left来区分内外连接

eg2：查询每个员工的上级领导，要求显示所有员工的名字和领导名

```mysql
select
	a.ename '员工名', b.ename '领导名'
from
	emp a
left join
    emp b
on
	a.mgr = b.empno;
```
![image-20211205142221864.png](https://s2.loli.net/2021/12/10/w2DAWcGKOMa7zr9.png)

### 多表连接

````mysql
select
	...
from
	a
join
	b
on
	a和b的连接条件
join
	c
on
	a和c的连接条件
right join
	d
on
	a和d的连接条件
````

注：一条sql中内外链接可以混合，都可以出现

案例：找出每个员工的部门名称，以及工资等级，要求显示员工名，部门名，薪资，薪资等级

将这三张表其别称为e，s，d
![image-20211205143250505.png](https://s2.loli.net/2021/12/10/KDcQx4WgEbBaYUN.png)![image-20211205143314798.png](https://s2.loli.net/2021/12/10/F42edqvOJzyuhHY.png)

```mysql
select 
	e.ename, e.sal,d.dname,s.grade
from
	emp e
join
	dept d
on
	e.deptno = d.deptno
join
	salgrade s
on
	e.sal between s.losal and s.hisal;
```

结果如下：
![image-20211205143937346.png](https://s2.loli.net/2021/12/10/qhDgjmJeO5lFZtM.png)

案例升级：找出每个员工的部门名称，以及工资等级，还有上级领导，要求显示员工名，领导名，部门名，薪资，薪资等级

```mysql
select 
	e.ename '员工名',x.ename '领导名', e.sal,d.dname,s.grade
from
	emp e
left join
	emp x
on
	e.mgr = x.empno
join
	dept d
on
	e.deptno = d.deptno
join
	salgrade s
on
	e.sal between s.losal and s.hisal;
```

结果如下：

<img src="C:\Users\郝锦杰\AppData\Roaming\Typora\typora-user-images\image-20211205144721956.png" alt="image-20211205144721956" style="zoom:67%;" />

## 子查询

#### 定义

select语句中嵌套select语句被嵌套的select语句称为子查询

#### 子查询可以出现的位置

```mysql
select
	..(select)
from
	..(select)
where
	..(select)
```

#### where语句中的子查询

案例：找出比最低工资高的员工姓名和工资

```mysql
select
	ename,sal
from
	emp
where
	sal > min(sal);
//错误：where子句中不能直接使用分组函数
```

第一步：查询最低工资是多少

```mysql 
select min(sal) from emp;
```

<img src="C:\Users\郝锦杰\AppData\Roaming\Typora\typora-user-images\image-20211205145918768.png" alt="image-20211205145918768" style="zoom: 80%;" />

第二步：找出大于最低工资的数据

```mysql
select ename,sal from emp where sal > 800;
```

第三步：合并

```mysql
select ename,sal from emp where sal > (select min(sal) from emp);
```

<img src="C:\Users\郝锦杰\AppData\Roaming\Typora\typora-user-images\image-20211205150115435.png" alt="image-20211205150115435" style="zoom:80%;" />

#### from子句中的子查询

注意:from后面的子查询，可以将**子查询的查询结果当成一张临时表**（技巧）

案例：找出每个岗位平均工资的薪资等级

第一步：按照岗位分组求平均值

```mysql
select
	job,avg(sal)
from
	emp
group by
	job;
```

<img src="C:\Users\郝锦杰\AppData\Roaming\Typora\typora-user-images\image-20211205150845353.png" alt="image-20211205150845353" style="zoom:80%;" /><img src="C:\Users\郝锦杰\AppData\Roaming\Typora\typora-user-images\image-20211205151606368.png" alt="image-20211205151606368" style="zoom:80%;" />

第二步：克服心理障碍，把以上查询结果当做一张真实存在的表t。（左边表为t，右边的表为s）

​			   t和s表进行表连接，条件t表avg(sal) between s.losal and s.hisal;  

```mysql
select
	t.*, s.grade
from
	(select job,avg(sal) from emp group by job) t
join 
	salgrade s
on
	t.avg(sal) between losal and hisal; //报错
//t.avg(sal)中的avg被当作是分组函数里的关键字，而不是t表里的字段名
//更改方法：起别名
select
	t.*, s.grade
from
	(select job,avg(sal) as avgsal from emp group by job) t
join 
	salgrade s
on
	t.avgsal between losal and hisal;
```

结果如下：

<img src="C:\Users\郝锦杰\AppData\Roaming\Typora\typora-user-images\image-20211205152519682.png" alt="image-20211205152519682" style="zoom:80%;" />

#### select后面出现的子查询（了解即可）

案例：找出每个员工的部门名称，要求显示员工名，部门名

```mysql
select 
	e.ename,e.deptno,(select d.dname from dept d where e.deptno = d.deptno) as dname
from
	emp e;
```

注意：select后面的子查询，只能一次返回一条结果，多与一条就报错

## union

合并查询结果集

案例：查询工作岗位是manager和salesman的员工？

```mysql
select ename,job from emp where job = 'manager' or job = 'salesman';
select ename,job from emp where job in('manager','salesman');

select ename,job from emp where job = 'manager'
union
select ename,job from emp where job = 'salesman';
```

union的效率高一些，在表连接的笛卡尔积现象中，union可以减少匹配的次数（把乘法变成加法运算）

注意：union在进行结果集合并的时候要求两个结果集列数相同

列的数据类型也应该相同（mysql中不严格，Oracle中会报错）

## limit（非常重要）

**概要**：将查询结果集的一部分取出来，通常使用在分页查询中

​			分页的作用是为了提高用户体验（百度一页默认给出10个结果）

**用法**: limit startIndex,length

​		  startindex是起始下标，length是长度

​		  下标从0开始

缺省用法：limit 5；取前五（默认起始下标从0开始）

案例：按照薪资降序，取出排名在前五名的员工

```mysql
select
	ename,sal
from
	emp
order by
	sal desc
limit 5;
```

<img src="C:\Users\郝锦杰\AppData\Roaming\Typora\typora-user-images\image-20211205155637533.png" alt="image-20211205155637533" style="zoom:67%;" />

注意：mysql中limit实在order by 后执行

案例:找出工资排名在3-5名的员工

```mysql
select
	ename,sal
from
	emp
order by
	sal desc
limit 2,3;
//2表示起始位置从下标2（第三个数据开始），取三个元素
```

## 分页

案例：每页显示3条数据

pageno:页数

pageSize：每页显示pageSize条数据

​	第pageNo页：limit （pageno-1） * pageSize , pageSize

## DQL语句大总结

```mysql
select
	...	
from
	...
where
	...
group by
	...
having
	...
order by
	...
limit
	...
```

执行顺序：

1.from

2.where

3.group by

4.having

5.select

6.order by

7.limit

难点：多表连查，多看看

# DDL语句

DDL包括：create drop alter

## 建表

语法格式：

create table 表名（字段名1 数据类型，字段名3，数据类型，字段名3，数据类型）;

create table 表名（

字段名1 数据类型，

字段名3 数据类型，

字段名3 数据类型

）;

表名和字段名都属于标识符

表名：建议以t_ 或者tbl_开始，

字段名：见明知意

## MySQL中的数据类型

常见数据类型：

### varchar（最长255）

​	**可变长度的字符串**。会更据实际的数据长度，**动态的分配空间**

​	节省空间，但需要动态分配空间，速度慢

### char（最长255）

​	**定长字符串**。不管实际数据长度是多少，分配固定长度空间，存储数据

​	速度快，但使用不当会造成空间浪费

​    varchar和char的选用取决于储存数据的具体情况

### int（最长11）

​	数字中的整数型

### bigint

​	数字中的长整型

### double

​	单精度浮点型数据

### float

​	双精度浮点型数据

### date

​	短日期类型：只包括年月日信息

### datetime

​	长日期类型：包括年月日时分秒信息

### clob

​	字符大对象

​	最多可储存4G的字符串

​	超过255个字符都需要使用clob字符大对象来存储

### blob

​	二进制大对象

​	专门存储图片，声音，视频等流媒体数据

​	往blob类型的字段上插入数据时，例如插入一个图片，视频等，需要使用IO流才行

eg: t_movie 电影表

编号				名字						描述信息						上映日期				  时长  					海报					类型

no(bigint)  	name(varchar)      description(clob)		 playdate(date)		time(double)	   image(blob)	  type(char)

## 创建一个学生表

```mysql
create table t_student(

        no int,

        name varchar(32),

        sex char(1),

        age int(3),

        email varchar(255)

);
```

```mysql
create table t_student(no int, name varchar(32),sex char(1),age int(3), email varchar(255));
```

## 快速创建表(了解内容)

```mysql
create table emp2 as select * from emp;
```

//原理：将一次查询结果当做一张表新建

​			   这个可以完成表的快速复制，表建出来，其中数据也存在了；

## 将查询结果插入到一张表中（了解内容）

```mysql
create table dept_bak as select *from dept;
insert into dept_bak  select *from dept;
```

## 删除表

```mysql
drop table t_student;//当这张表不存在的时候会报错
drop table if exists t_student;//如果这张表存在的话删除
```

## 对表结构的增删改

alter语句（DDL）

不做深度学习

第一：实际开发中，需求一旦确立后，表一旦设计好，很少修改表结构。因为开发过程中，修改表结构，成本比较高

​			修改表的结构对应的代码需要进行大量的修改，成本是比较高的。这个责任应该由设计人员承担！

第二：由于修改表结构的操作很少，所以不需要掌握，如果有一天真的需要修改表的结构，可以使用工具!

​			修改表的结构是不需要写在程序中的。

# DML语句

## 插入数据(DML)

### 语法格式

insert into 表名（字段名1，字段名2，字段名3...）values(值1，值2，值3);

注意：字段名和值要一一对应。即：数量要对应，数据类型要对应。

```mysql
insert into t_student (no,name,sex,age,email) values(1,'zhangsan','m','20','zhangsan@123.com');
```

```mysql
insert into t_student (name,no,sex,age,email) values('lisi',2,'f','20','lisi@123.com');
```

注意:insert语句但凡执行成功，那么必然会多一条记录

没有的给其他字段名指定值的话，默认值是null

eg：

```mysql
insert into t_student (name) values('wangwu');
```

<img src="C:\Users\郝锦杰\AppData\Roaming\Typora\typora-user-images\image-20211204102606782.png" alt="image-20211204102606782" style="zoom:80%;" />

不过默认值可以自定义，在建表的时候用default指定一个默认值//示例如下

create table t_student(

```mysql
 create table t_student(
    no int,

    name varchar(32),

    sex char(1), default('m')

    age int(3),

    email varchar(255)
 );
```

注意:insert 中的字段名可以省略,省略的话等于都写上了！所以值也要都写上！

eg：

```mysql
insert into t_student values(2,'zhaoliu','f',20,'wangwu@123.com');
```

不过还是建议把字段名写上，这样可读性强一点

### insert 插入日期

格式化数字：format（数字，'格式'）

eg：

```mysql
select ename,format(sal,'$999,999') from emp;//相当于加入了千分位
```

日期格式和字符串格式的轉換

**str_to_date**:将字符串varchar类型转换成date类型

**date_format**:将date类型转换成具有一定格式的varchar字符串类型

```mysql
drop table if exists t_user;
create table t_user(
		id int,
    	name varchar(32),
    	birth date    	
);
	//生日可以使用date日期类型
create table t_user(
		id int,
    	name varchar(32);
    	birth char(10)    	
);
	//生日可以使用字符串
```

<img src="C:\Users\郝锦杰\AppData\Roaming\Typora\typora-user-images\image-20211204110740652.png" alt="image-20211204110740652" style="zoom: 80%;" />

生日：2002-09-18（10个字符）

注意：数据库中有一条命名规范：

​			所有标识符全是小写，单词和单词之间用下划线连接。

插入数据：

```mysql
insert into t_user(id,name,birth) values (1,'zhangsan','01-10-1990');//报错
```

报错原因：birth 是date类型，’01-10-1990‘是字符串类型，类型不匹配

**可以用str_to_date进行类型转换**

#### str_to_date

语法格式：

​		str_to_date('字符串日期'，'日期格式')

通常使用在插入insert方面，因为插入的时候需要一个日期类型的数据，

需要通过该函数将字符串转化成date类型

```
mysql的日期格式：
%Y 年
%m 月
%d 日
%h 时
%m 分
%s 秒
```

```mysql
insert into t_user(id,name,birth) values (1,'zhangsan',str_to_date('01-10-1990','%d-%m-%Y'));//修改
```

![image-20211204112005543](C:\Users\郝锦杰\AppData\Roaming\Typora\typora-user-images\image-20211204112005543.png)

**不过如果你提供的日期字符串是这个格式，str_to_date函数就不需要了,mysql会进行自动类型转换**

```mysql
insert into t_user(id,name,birth) values (2,'lisi','1990-11-05');
```



#### date_format

将date类型转换成具有一定格式的varchar字符串类型

语法：

date_format(日期数据类型，‘想要的日期格式’)

主要用在日起日期查询当中

eg: 查询的时候以某个特定日期格式展示

```mysql
select id,name,date_format(birth, '%m/%d/%Y')  as  birth from t_user;
```

<img src="C:\Users\郝锦杰\AppData\Roaming\Typora\typora-user-images\image-20211204172011642.png" alt="image-20211204172011642" style="zoom:80%;" />

#### date和datetime的区别

datetime:长日期包括年月日时分秒

短日期默认格式：%Y-%m-%d

长日期默认格式：%Y-%m-%d  %h: %i: %s

```mysql
drop table if exists t_user;
create table t_user(
		id int,
    	name varchar(32),
    	birth date,
    	create_time datetime  
);
insert into t_user(id,name,birth,create_time) values(1,'zhangsan','1990-10-01','2021-12-04 17:49:50');
```

insert into t_user(id,name,birth,create_time) values(2,'lisi','1990-10-02',now());

#### now() 函数

```mysql
insert into t_user(id,name,birth,create_time) values(2,'lisi','1990-10-02',now());
```



<img src="C:\Users\郝锦杰\AppData\Roaming\Typora\typora-user-images\image-20211204181011565.png" alt="image-20211204181011565" style="zoom:80%;" />

获取系统当前时间，或取得时间带有时分秒，是datetime类型

### insert一次插入多条语句

语法格式： insert into 表名（字段名1，字段名2，字段名3...）values (),(), (),()...;

```mysql
insert into t_user (id,name,birth,create_time) values 
(1,'zs','2002-09-18',now()),
(2,'lisi','2003-09-18',now()),
(3,'wangwu','2005-09-18',now());
```

结果如下：

<img src="C:\Users\郝锦杰\AppData\Roaming\Typora\typora-user-images\image-20211205165133588.png" alt="image-20211205165133588" style="zoom:80%;" />

## 修改update(DML)

语法格式:

update 表名 set 字段名1=值1，字段名2=值2，字段名3=值3...   where 条件；

注意：没有数据限制会导致所有数据更新

```mysql
update t_user set name='jack',birth = '2000-10-11',create_time = now() where id = 2;
//把id为2的那行数据进行更改，记得加where条件，不然整张表都改了
```

<img src="C:\Users\郝锦杰\AppData\Roaming\Typora\typora-user-images\image-20211204181435860.png" alt="image-20211204181435860" style="zoom:80%;" />

## 删除数据 delete（DML）

语法格式：

delete from 表名 where 条件；

删除原理：表中的数据被删除了，但数据在硬盘上占据的空间不会被释放

​					缺点：删除效率低  优点：可以回滚，恢复数据

注意：没有条件整张表的数据会全部删除

```mysql
delete from t_user where id = 2;
```

<img src="C:\Users\郝锦杰\AppData\Roaming\Typora\typora-user-images\image-20211204182826620.png" alt="image-20211204182826620" style="zoom:80%;" />

```mysql
delete from t_user;//删整张表
```

## 删除数据truncate语句（DDL）（重要）

```mysql
truncate from debt_bak;
```



物理删除，效率高，表被一次截断

缺点：不可以回滚 优点：效率高	

注意：有上亿条数据的大表，删除时用delete可能需1h+，效率低

​			可以选择使用truncate，只需1s。不过通知客户删了后不可以恢复

​			truncate是删除数据表还在，不能删单条数据

# 约束（很重要）

**constraint** 

在创建表的时候，我们可以在表中的字段上加一些约束，来表征这个表中数据的**完整性**，**有效性**！

## 类型

非空约束: not null

唯一性约束: unique 

主键约束: primary key（简称FK）

外键约束: foreign key（简称PK）

检查约束: check(mysql不支持，Oracle支持)

重点学习前四个

## 非空约束not null

非空约束not null 约束的字段不能为null

```mysql
drop table if exists t_vip;
create table t_vip(
	id int,
    name varchar(255) not null
);
insert into t_vip (id,name) values (1,'zhangsan'),(2,'lisi');
```

```mysql
insert into t_vip (id) values (3);//报错，因为已经进行了非空约束，name必须有相应的值
```

//not null 只有列级约束，没有表级约束

小插曲：xxxxx.sql这种文件称为sql脚本文件

​				sql脚本文件中编写了大量SQL语句。

​				执行SQL脚本文件时，该文件中所有sql语句会全部执行!

​				批量执行sql语句可以使用sql脚本文件。

​				执行方法：source 后面把文件拖下来

<img src="C:\Users\郝锦杰\AppData\Roaming\Typora\typora-user-images\image-20211205180844579.png" alt="image-20211205180844579" style="zoom:80%;" />

​				实际工作中：第一天到公司，把上面给你的sql文件，之间用source语句，导入公司相关项目的数据库

## 唯一性约束

unique

### 列级约束

约束

约束的字段不能重复，具有唯一性，但可以为null

```mysql
//先创建一张表，用来测试
drop table if exists t_vip;
create table t_vip(
	id int,
    name varchar(255) unique,
    email varchar(255) 
);
insert into t_vip (id,name,email) values 
(1,'zhangsan','zhansan@123.com'),
(2,'lisi','lisi@123.com'),
(3,'wangwu','wangwu@123.com');
//测试唯一性约束
insert into t_vip (id,name,email) values (4,'wangwu','wangwu@xinlang.com');//报错如下：wangwu（name）重复
insert into t_vip (id) values (4),(5);
```

![image-20211205200428391](C:\Users\郝锦杰\AppData\Roaming\Typora\typora-user-images\image-20211205200428391.png)

![image-20211205200723533](C:\Users\郝锦杰\AppData\Roaming\Typora\typora-user-images\image-20211205200723533.png)

name字段虽然被unique约束了，但是可以为null

### 表级约束

为多个字段联合起来添加某一个约束称为表级约束

新需求：name和email两个字段**联合起来**具有唯一性

```mysql
drop table if exists t_vip;
create table t_vip(
	id int,
    name varchar(255) unique,
    email varchar(255) unique 
);
//这种创建方式是各自具有唯一性，不符合新需求
```

```mysql
//以下数据符合新需求
insert into t_vip (id,name,email) values (1,'zhangsan','zhangsan@123.com');
insert into t_vip (id,name,email) values (2,'zhangsan','zhangsan@xinlang.com');
```

```mysql
//正确创建方式
drop table if exists t_vip;
create table t_vip(
	id int,
    name varchar(255) ,
    email varchar(255) ,
    unique(name,email)
);
insert into t_vip (id,name,email) values (1,'zhangsan','zhangsan@123.com');
insert into t_vip (id,name,email) values (2,'zhangsan','zhangsan@xinlang.com');
//name和email连个字段联合起来唯一
```

<img src="C:\Users\郝锦杰\AppData\Roaming\Typora\typora-user-images\image-20211205201828142.png" alt="image-20211205201828142" style="zoom:80%;" />

###  unique和not null可以联合使用

eg：

```mysql
drop table if exists t_vip;
create table t_vip(
	id int,
    name varchar(255) not null unique
);
```

<img src="C:\Users\郝锦杰\AppData\Roaming\Typora\typora-user-images\image-20211205204928779.png" alt="image-20211205204928779" style="zoom:80%;" />

在MySQL当中一个字段被not null 和unique联合约束后，该字段自动变成主键字段（Oracle中不一样）

```mysql
insert into t_vip(id,name) values (1,'zhangsan');
insert into t_vip(id,name) values (2,'zhangsan');//错误 name不能重复
insert into t_vip(id) values (2); //错误 name不能为null
```

## 主键约束（非常重要）

**（primary key，简称PK）**

主键约束的相关术语

​	主键约束：就是一种约束

​	主键字段：该字段上添加了主键约束，这样的字段叫做：主键字段

​	主键值：主键字段中的每一个值都可以叫做主键值

**概念及用处**

主键值是每一行记录的唯一标识

主键值是每一行记录的身份证号!

记住：任何一行记录都应该有主键，没有主键，表无效！！！

**主键的特征**

not null + unique（主键值不能是null，同时也不能重复！）

**如何添加主键约束**

**单一主键**：一个字段做主键叫做单一主键

```mysql
drop table if exists t_user;
create table t_vip(
	id int primary key,
    name varchar(255)
);
insert into t_vip(id,name) values(1,'zhangsan');
insert into t_vip(id,name) values(2,'lisi');
insert into t_vip(id,name) values(2,'wangwu');//错误，不能重复
insert into t_vip(name) values('zhaoliu');//错误，不能为null

//也可以用表级约束创建
drop table if exists t_user;
create table t_vip(
	id int,
    name varchar(255),
	primary key(id)
);
```

**复合主键**：多个字段联合做主键叫复合主键

注意:在实际开发中不建议使用复合主键，建议使用用单一主键，

​		 主键值存在的意义就是为了加个身份证号，单一主键可达到目的

```mysql
drop table if exists t_vip;
create table t_vip(
	id int,
    name varchar(255),
    email varchar(255),
	primary key(id,name)
);
insert into t_vip(id,name,email) values(1,'zhangsan','zhangsan@123.com');
insert into t_vip(id,name,email) values(1,'lisi','lisi@123.com');//正确
insert into t_vip(id,name,email) values(1,'lisi','lisi@123.com');//错误：重复
```

![image-20211205212156274](C:\Users\郝锦杰\AppData\Roaming\Typora\typora-user-images\image-20211205212156274.png)

注意：一张表主键约束只能添加一个（一个复合主键算一个主键）

**建议**

主键值建议使用：int，bigint，char等类型

不建议使用：varchar

主键值一般都是数字，是定长的

**主键除了单一主键和复合主键外**，**还可以按别的方法分类**

自然主键：主键值是一个自然数，和业务没关系

业务主键：主键值和业务紧密相关，例如拿银行卡账号做主键，这就是业务主键

注意：开发中，自然主键用的多，主键做到不重复即可，不需要有意义。

​			业务主键不好，因为主键一旦和业务挂钩，那么业务一旦发生变动，可能会影响到主键值，故不建议用业务主键

​			最好主键值是一个自然数

**MySQL中有一种机制，可以自动帮我们维护主键值**

​    **auto_increment**//表示自增，从一开始，以一递增

 ```mysql
 drop table if exists t_vip;
 create table t_vip(
 	id int primary key auto_increment,
     name varchar(255)
 );
 insert into t_vip(name) values('zhangsan');
 insert into t_vip(name) values('zhangsan');
 insert into t_vip(name) values('zhangsan');
 insert into t_vip(name) values('zhangsan');
 insert into t_vip(name) values('zhangsan');
 insert into t_vip(name) values('zhangsan');
 select * from t_vip;
 ```

![image-20211205213740595](C:\Users\郝锦杰\AppData\Roaming\Typora\typora-user-images\image-20211205213740595.png)

## 外键约束（非常重要）

**foreign key 简称 fK**

**相关术语**

外键约束：一种约束

外键字段：该字段上添加了外键约束

外键值：外键字段当中的每一个值

**业务背景**

请设计数据库表，来描述'班级和学生‘的信息

**第一种方案**：**班级学生存在一张表中**

t_student

no(PK)         name       classno             classname

1				   jack           100                   高三1班

2				   lucy		   100                   高三1班

3				   mike		  100                   高三1班

4				   lisi		      101                   高三2班

5				   wangwu    101                   高三2班

5				   zhaoliu      101                   高三2班

缺点：数据冗余，空间浪费

**第二种方案**：**班级，学生各一张表**

t_class 班级表

classno（PK）          classname

100                             高三1班

 101                            高三2班

t_student 学生表

no（PK）               name              cno（班级编号）（FK引用t_class中的classno）

1				 			  jack          		 100                   

2							   lucy		 		  100               

3							   mike		 		 100                   

4							   lisi		      		101                

5				  			 wangwu    		 101                

6				   			zhaoliu 		      102    

**为什么要添加外键约束**      

当cno字段没任何约束时，可能会导致数据无效，可能出现一个102，但是102班级不存在，

所以为了保证cno字段中的值是100和101，需要给cno字段添加外键约束。

那么：cno字段就是外键字段，cno字段中的每一个值就是外键值

**注意**：

t_class是父表，t_student是子表

删除表的顺序：先删子表，再删父表

创建表的顺序：先建父表，再建子表

删除数据的顺序：先删子表，再删父表

插入数据的顺序：先插入父表，再插入子表

```mysql
drop table if exists t_student;
drop table if exists t_class;

create table t_class(
	classno int primary key,
    classname varchar(255)
);

create table t_students(
	no int primary key auto_increment,
    name varchar(255),
    cno int,
    foreign key (cno) references t_class(classno)
);

insert into t_class(classno,classname) values 
(100, '高三1班'),
(101,'高三2班');

insert into t_students(name,cno) values
('jack',100),
('lucy',100),
('mike',100),
('lisi',101),
('wangwu',101),
('zhaoliu',101);
select * from t_students;
select * from t_class;

```

**注意**：

```mysql
insert into t_students(no,name,cno) values('jack',100)//错误语法，auto_increment类型的字段不需要自行插入数据

外键作用演示：
insert into t_students(name,cno) values('wangqi',102)//错误语法，cno在父表中没有102这一数据
```

**测试**

1.外键值可以为空吗？  

​	外键值可以为空。

2.子表中的字段引用父表中的字段，被引用的字段必须是主键吗？

​	不一定是主键，但**至少具有unique约束**

ps：约束的增删改在开发过程中不常用，此处不加赘述

# 存储引擎（了解内容）

## 定义及作用

存储引擎是mysql中特有的的术语，其它数据库中没有（Oracle中油，但不叫这个名字）

存储引擎是一个表存储/组织数据的一种方式，不同的存储引擎，表存储数据的方式不同

## 怎么给表添加/指定存储引擎

可以在建表的时候，给表指定存储引擎

再建表的时候可以再最后的小括号“ ) ”右边使用：

​			engine 来指定存储引擎

​			charset 来指定这张表的字符编码方式

```mysql
show create table t_students;
```

<img src="C:\Users\郝锦杰\AppData\Roaming\Typora\typora-user-images\image-20211206101734891.png" alt="image-20211206101734891" style="zoom:80%;" />

**默认存储引擎**：**InnoDB**

**默认的字符编码方式**：utf8(教程中)   我这里默认的是**utf8mb4**

 utf8mb4 字符编码，是utf8的超集， utf8mb4 是目前最大的一个字符编码,支持任意文字	（gbk字符编码方式也可以存储中文）

**指定存储引擎和字符编码方式示例**：

```mysql
drop table if exists t_product;
create table t_product(
	id int primary key,
    name varchar(255)
) 	engine = innodb default charset = gbk;
show create table t_product;
```

![image-20211206102852195](C:\Users\郝锦杰\AppData\Roaming\Typora\typora-user-images\image-20211206102852195.png)

## 查看mysql支持那些存储引擎

```mysql
show engines \G;
```

```
mysql> show engines \G;
*************************** 1. row ***************************
      Engine: MEMORY
     Support: YES
     Comment: Hash based, stored in memory, useful for temporary tables
Transactions: NO
          XA: NO
  Savepoints: NO
*************************** 2. row ***************************
      Engine: MRG_MYISAM
     Support: YES
     Comment: Collection of identical MyISAM tables
Transactions: NO
          XA: NO
  Savepoints: NO
*************************** 3. row ***************************
      Engine: CSV
     Support: YES
     Comment: CSV storage engine
Transactions: NO
          XA: NO
  Savepoints: NO
*************************** 4. row ***************************
      Engine: FEDERATED
     Support: NO
     Comment: Federated MySQL storage engine
Transactions: NULL
          XA: NULL
  Savepoints: NULL
*************************** 5. row ***************************
      Engine: PERFORMANCE_SCHEMA
     Support: YES
     Comment: Performance Schema
Transactions: NO
          XA: NO
  Savepoints: NO
*************************** 6. row ***************************
      Engine: MyISAM
     Support: YES
     Comment: MyISAM storage engine
Transactions: NO
          XA: NO
  Savepoints: NO
*************************** 7. row ***************************
      Engine: InnoDB
     Support: DEFAULT		
     Comment: Supports transactions, row-level locking, and foreign keys
Transactions: YES
          XA: YES
  Savepoints: YES
*************************** 8. row ***************************
      Engine: BLACKHOLE
     Support: YES
     Comment: /dev/null storage engine (anything you write to it disappears)
Transactions: NO
          XA: NO
  Savepoints: NO
*************************** 9. row ***************************
      Engine: ARCHIVE
     Support: YES
     Comment: Archive storage engine
Transactions: NO
          XA: NO
  Savepoints: NO
9 rows in set (0.01 sec)
```

mysql支持九个存储引擎，版本不同，支持情况不同，8.0.27支持8种

![image-20211206103635747](C:\Users\郝锦杰\AppData\Roaming\Typora\typora-user-images\image-20211206103635747.png)

## **常见存储引擎**：

### **1.MEMORY**

其数据，索引存储在内存当中，目的就是快

不能包含blob或text字段

优势：查询效率最高，不需和硬盘交互

劣势：不安全，关机以后数据消失

ps：内存是直接取，光速，电流的速度；从硬盘上取，是机械行为，慢

### 2.**MyISAM**

使用三个文件表示每个表：

​			格式文件(.frm)/数据文件(.MYD)/索引文件(.MYI)

​	对于一张表：只要是主键，或者是有unique约束的就会自动添加索引

优势：可被转化为压缩，只读来节省存储空间

### 3.**InnoDB**

mysql默认存储引擎，重量级

**支持事务**，支持数据库崩溃后自动恢复机制

优势：非常安全，最大特点：支持事务以保证数据的安全

但效率低，不能压缩，只读

在目录中以.frm格式文件存在, InnoDB表空间tablespace 被用于存储表的内容

提供一组用来记录事务性活动的日志文件

# 事务（非常重要）

**必须理解**，**必须掌握**

## 基本知识

**概要**

一个事务就是一个完整的业务逻辑

是一个最小的工作单元，不可再分，一个事务就是要完成一件事

**本质**

一条事务就是批量的DML语句同时成功，或者同时为失败

**什么是完整的业务逻辑**

​	假设转账，从A账户向B账户转账10000，

​	将A账户上的钱减去10000（update语句）

​	将B账户上的钱加上10000（update语句）

这就是一个完整的业务逻辑

以上的操作是一个最小的工作单元，要么同时成功，要么同时失败，不可再分

以上两个update语句必须同时成功或者同时失败，这样才能保证钱是正确的

**只有DML语句（数据操纵语言）才会有事务这一说，其他语句与事务无关**

insert   update   delete

只有以上三个语句和事务有关系，因为只有以上三个语句是对数据进行增删改的

只要操作涉及数据的增，删，改，那么就一定要考虑安全问题

数据安全第一位！！！

**注意**：正是因为做某件事的时候，需要多条DML语句共同联合起来才能完成，所以需要事务的存在

假设所有业务，只有一条DML语句就能完成，没必要存在事务机制

**事务如何做到多条DML语句同时成功同时失败**

InnoDB存储引擎提供一组用来记录事务性活动的日志文件

事务开启了：

insert

insert

delete

update

事务结束了！

事务的执行过程中，每一条DML 语句都会被记录到“事务性活动的日志文件”中

在事务的执行过程中，我们可以提交事务，也可以回滚事务

**提交事务**

​	清空事务性活动的日志文件，将数据全部彻底持久化到数据库表中

​	提交事务，标志着事务结束，并且是一种全部成功的结束

**回滚事务**

​	将之前的所有的DML操作全部撤销，并且清空事务性活动的日志文件

​	回滚事务标志着事物的结束，并且是一种全部失败的结束

## 怎么提交事务，回滚事务

**提交事务**：commit; 语句

**回滚事务**：rollback; 语句	（回滚每次只能回滚到上一次的提交点!）

事务对应的英语单词是：transaction

**测试一下mysql中默认的事务行为**

​	mysql默认情况下是支持自动提交事务的。（自动提交）

​	什么是自动提交？

​	每执行一条DML语句，则提交一次 ；

这种自动提交实际上不符合开发习惯，为保数据安全，需要多条DML语句同时执行成功后再提交，所以不能执行一条就提交一条

**如何关闭mysql的自动提交机制呢**？

```mysql
start transaction;		//开启事务，关闭自动提交

insert...
delete...
update...
...

rollback; //执行DML语句后，直接输入rollback;即可回滚
commit; //同理执行DML语句后，直接输入commit;即可提交
```

## 事务包括四个特性

### 特性类别

A  : 原子性

​		说明事务是最小的工作单元，不可再分

C  :一致性

​		所有事务要求，在同一个事务中，所有操作必须同时成功，或者同时失败，以保证数据的一致性

I   :隔离性

​		A事务和B事务之间具有一定的隔离

​		A事务在操作一张表的时候，B事务也操作这张表

D :持久性

​		事务最终结果的一个保障，事务提交，就相当于没有保存到硬盘上的数据保存到硬盘上

### 重点研究事务的隔离性

**隔离级别**

A教室和B教室中间有一道墙，这道墙可以很厚，也可以很薄，这就是事务的隔离级别，这道墙越厚，表示隔离级别越高。

**事务和事务的隔离级别分类**

#### 	1.读未提交：read uncommmitted  （最低隔离级别）

​		《没有提交就读到了》

​		**概要**：事务A可以读取到事务B未提交的数据

​		**问题**：这种隔离级别存在的问题就是：脏读现象！（Dirty Read） 我们称读到了脏数据

​		**注意**：这种隔离级别一般都是理论上的，大多数数据库隔离级别都是二档起步

#### 	2.读已提交： read committed	 

​		《提交之后才读到》

​		**概要**：事务A只能读取到事务B提交之后的数据

​		**优点**：这种隔离级别解决了脏读的现象

​		**缺点**：这种隔离级别的问题是不可重复读取数据

​		**不可重复读取数据**：事务开启后，第一次读到的数据时3条，当前事务还没有结束，可能第二次再读取的时候，读取到的数据是4条，										   3 != 4,称为不可重复读取

​		**注意**：这种隔离级别是比较**真实**的数据，每次读到的数据是绝对的真实

​					Oracle数据库默认的隔离级别是：read committed

#### 	3.可重复读： repeatable read		

​		《提交之后也读不到，读取到的都是刚开启事务时的数据》

​		**概要**：事务A开启之后，不管多久，每一次在事务A中读取到的数据都是一致的。即使事务B将数据已经修改，并且提交了，事务A读		取到的数据，还是没有发生改变，这就是可重复读

​		**优点**：解决了不可重复读的问题

​		**缺点**：可能出现幻影读。每一次读取到的数据都是幻想，不真实

​		**注意**：早上9点开启事务，只要事务不结束，到晚上9点，读到的事务还是那样！

​					mysql中默认的事务隔离级别是这个！！！

#### 	4.序列化/串行化：	serializable	  （最高隔离级别）

​		**概要**：这是最高隔离级别，效率最低，解决了所有的问题，这种隔离级别表示事务排队，不能并发！

​		每次读到的数据是最真实的，并且效率最低

### 验证各种隔离级别

查看隔离级别： 

```mysql
select @@transaction_isolation;
```

![image-20211206194857742](C:\Users\郝锦杰\AppData\Roaming\Typora\typora-user-images\image-20211206194857742.png)

mysql 默认隔离级别

**验证：read uncommmitted** 

```mysql
set global transaction isolation level read uncommitted;
```

注意：设置之后，退出来重进才能生效；验证时开两个DOS窗口，模拟两个事务

```MYSQL
事务A                                            事务B
------------------------------------------------------------------------------------------------------
use study;                                      
												 use study;
start transaction;                               
												 start transaction;
												 insert into t_user values('zhangsan');
select * from t_user;//查到了插入的数据												 
```

**验证：read commit**

```mysql
set global transaction isolation level read commit;//设置后记得重进

事务A                                            事务B
------------------------------------------------------------------------------------------------------
use study;                                       
												 use study;
start transaction;                               
												 start transaction;
select * from t_user;												 
												 insert into t_user values('jack');
select * from t_user;//查不到插入的数据	
												 commit;
select * from t_user;//查到了插入的数据	
```

**验证：repeatable read**

```mysql
set global transaction isolation level repeatable read;//设置后记得重进

事务A                                            事务B
------------------------------------------------------------------------------------------------------
use study;                                       
												 use study;
start transaction;                               
												 start transaction;
select * from t_user;												 
												 insert into t_user values('lisi');
												 insert into t_user values('wangwu');
select * from t_user;//查不到插入的数据	
												 commit;
select * from t_user;//查不到插入的数据	
```

**验证：serializable**

```mysql
set global transaction isolation level serializable;//设置后记得重进

事务A                                            事务B
------------------------------------------------------------------------------------------------------
use study;                                       
												 use study;
start transaction;                               
												 start transaction;
select * from t_user;												 
insert into t_user values('abc');												 
												 select * from t_user;
												 //执行这条查询后光标一直闪烁
commit;
												 //A事务提交后这边立刻显示出查询结果
```

# 索引

## 概要

索引是在数据库表的字段上添加的，是为了提高查询效率存在的一种机制

一张表的一个字段可以添加一个索引，当然，多个字段联合起来也可以添加索引

索引相当于一本书的目录，是为了**缩小扫描范围**，而存在的一种机制

**类比说明**

对于一本字典来说，查找某个汉字有两种方式

第一种方式：一页一页挨着找，直到找到为止，这种查找方式相当于全字典扫描，效率较低

第二种方式：先通过目录（索引）去定位一个大概的位置，然后直接定位到这个位置，做局域性扫描，缩小扫描的范围，快速的查找，这种查找方式属于通过索引查找，效率较高

**MySQL在查询的两种方式**

第一种：全表查询

第二种：根据索引检索

注意：在实际中汉语字典前面的目录是排序的，因为只有排序了才会有区间查找这一说（缩小扫描范围其实就是扫描某个区间罢了）

索引是一个，B-tree数据结构，遵循左小右大原则存放，采用中序遍历方式，遍历数据

......

## 索引的实现原理

缩小扫描范围，避免全表扫描

表中字段不会动，索引会自动排序

假设有一张用户表t_user

```mysql
id(PK)					name				每一行记录在硬盘上都有一个物理存储编号
------------------------------------------------------------------------------
100						zhangsan			0x1111
120						lisi				0x2222
99						wangwu				0x8888
88						zhaoliu				0x9999
101						jack				0x6666
55						lucy				0x5555
130						tom					0x7777
```

提醒1：在任何数据库当中主键上都会自动添加索引对象，id(PK)字段上自动有索引

另外在mysql中，一个字段上如果有unique约束的话，也会自动创建索引对象

提醒2：在任何数据库当中，任何一张表的任何一条记录在硬盘存储上都有一个硬盘的物理存储编号

提醒3：在mysql中索引是一个单独的对象，不同的存储引擎以不同的形式存在，在myisam存储引擎中，索引存储在.MYI文件中，在InnoDB存储引擎中索引存储在一个逻辑名称叫做tablespace当中。在memory存储引擎中索引被存储在内存当中。不管索引存储在哪里，**索引在MySQL中都是以树的形式存在（自平衡二叉树：B-tree）**

## 需要添加索引的情况

在MySQL中，主键上，以及unique字段上，都会自动添加索引

条件1：数据量庞大（多大算庞大，需要测试，因为每一个硬件环境下不同）

条件2：该字段经常出现在where后面，以条件的形式存在，也就是说这个字段总是被扫描

条件3：该字段很少的DML操作。（因为DML语句后，索引需要重新排序）

建议不要随意添加索引，因为索引需要维护，太多的话反而会降低系统的性能，建议通过主键查询，通过unique约束的字段进行查询，效率是比较高的

## 创建与删除

**创建索引**

<img src="C:\Users\郝锦杰\AppData\Roaming\Typora\typora-user-images\image-20211207171255805.png" alt="image-20211207171255805" style="zoom:80%;" />

案例：为emp表的ename字段添加索引，起名：index_emp_index

```mysql
create index emp_index_index on emp(ename);
```

**删除索引**

将emp表上的emp_ename_index索引对象删除

```mysql
drop index_emp_index on emp;
```

**在MySQL当中，怎么查看一个sql语句是否使用了索引进行检索**

```mysql
explain select * from emp where ename = 'king';
```

![image-20211207172714155](C:\Users\郝锦杰\AppData\Roaming\Typora\typora-user-images\image-20211207172714155.png)

扫描14条记录，说明没有使用索引。（type=ALL）

```mysql
//添加算法
create index emp_index_index on emp(ename);
explain select * from emp where ename = 'king';
```

![image-20211207173036106](C:\Users\郝锦杰\AppData\Roaming\Typora\typora-user-images\image-20211207173036106.png)

扫描了1条记录

mysql索引底层是B-tree,二叉树

## 索引的失效

**失效的第一种情况**

模糊匹配中以'%'开头了

eg：

```mysql
select * from emp where ename like '%T';
```

ename上添加了索引，也不会走索引，为什么？

原因是因为模糊匹配中以'%'开头了，尽量避免某户查询时以’%‘开始

这是一种优化手段

**失效的第二种情况：**

​	使用or时会失效，如果使用or那么要求or两边的条件字段都要有索引，

​	才会走索引，如果其中一个字段没有索引，那么另一个字段上的索引也会实现。

​	所以这就是不建议使用or的原因

**失效的第三种情况：**

​	使用复合索引的时候，没有使用左侧的列查找，索引失效

​	复合索引：两个字段，或者多个字段联合起来添加一个索引，叫做复合索引

**失效的第四种情况：**

在where中索引列参加了运算

**失效的第五种情况：**

## 索引的分类

索引是各种数据库进行优化的重要手段。优化的时候优先考虑的因素就是索引

单一索引：一个字段上添加索引

复合索引：两个或者更多的字段上添加索引



主键索引：主键上添加索引

唯一性索引：具有unique约束的字段上添加索引

.......

注意：唯一性比较弱的字段上添加索引用处不大，越唯一，越高效

# 视图（view）

## 概念

view：站在不同的角度，看待同一份数据

## 怎么创建，删除视图对象

```mysql
create table dept2 as select * from dept; //先复制一个新表
create view dept2_view as select * from dept2;//创建
drop view dept2_view;//删除
```

注意：只有DQL语句才能以view的形式创建

```mysql
create view view_name as 这里的语句必须是DQL语句;
```

## 作用

我们可以面向视图对象进行增删改查，对视图对象增删改查，会导致原表被操作

```mysql
//面向视图查询
select * from dept2_view;
//面向试图插入
insert into dept2_view(deptno,dname,loc) values (60 ,'sales','beijing')
//面向原表查询
select * from  dept2;//改变视图数据后，原表数据被改变
```

### 实际开发中的作用《方便 简化开发 利于维护》

视图是用来简化sql语句的

假设有一条非常长的sql语句，而这条sql语句需要在不同的位置上反复使用，每一次使用这个sql语句的时候都要重新编写，很长很麻烦这时可以，把这条复杂的sql语句以视图对象的形式新建，在需要编写SQL语句的位置直接使用视图对象，可以大大简化开发，而且利于后期的维护，因为修改时只需修改一个位置就行，只需要修改视图对象所映射的SQL语句

以后面向试图开发的时候，使用视图可以向使用table一样。试图对象不是存在内存当中的，而是存在硬盘上的，不会消失。

**注意**：视图对应的语句只能是DQL语句，但试图对象创建完成后，可以对视图进行增删改查的操作

**小插曲**：增删改查，又叫做：CRUD

CRUD是在公司程序员之间沟通的术语，一般我们很少说增删改查，一般都说CRUD。

C：create（增）R：retrive（查：检索）U：update（改）D：（删）

# DBA常用命令

数据库管理员（Database [Administrator](https://baike.sogou.com/lemma/ShowInnerLink.htm?lemmaId=251395&ss_c=ssc.citiao.link)，简称DBA）是一个负责管理和维护[数据库服务器](https://baike.sogou.com/lemma/ShowInnerLink.htm?lemmaId=17843&ss_c=ssc.citiao.link)的人，其职责是一般监视、备份、修改密码、[深层次管理](https://baike.sogou.com/lemma/ShowInnerLink.htm?lemmaId=103438042&ss_c=ssc.citiao.link)和研究等。数据库管理员负责全面管理和控制数据库系统。(百科)

新建用户，和授权相关的命令属于DBA的活

我们重点掌握数据的导入导出（数据的备份），其他命令了解一下即可

## 数据导出

注意：需要先登录到mysql数据库服务器上

mysqldump study >C:\study.sql -uroot -p密码

(需要有mysqldump.exe才可以进行)

可以导出指定的表

mysqldump study emp >C:\study.sql -uroot -p密码

## 数据导入

注意：需要先登录到mysql数据库服务器上

```mysql
//然后创建数据库：
create database study;
//使用数据库
use study;
//然后初始化数据库
source C:\study.sql
```

# 数据库设计的三范式（重要）

## 概要

数据库表的设计依据。教你怎么进行数据库表的设计。

第一范式：要求任何一张表必须有主键，每一个字段原子性不可再分

第二范式：建立在第一范式的基础之上，要求所有非主键字段完全依赖于主键，不要产生部分依赖

第三范式：建立在第二范式的基础之上，要求所有非主键字段直接依赖主键，不要产生传递依赖

声名：三范式是面试官经常问的，所以一定要熟记在心！

设计数据库表的时候，按照以上范式进行，可以避免表中数据的冗余，空间的浪费

## 第一范式

最核心，最重要的范式，所有表的设计都需要满足。

必须有主键，并且每一个字段都是原子性不可再分

案例：

```mysql
学生编号    学生姓名     联系方式
------------------------------------------------------------------
1001	   张三       zs@gmail.com,13994822222
1002	   李四		ls@gmail.com,13699999999
1001	   王五		ww@gmail.com,13488789564
```

以上学生表不满足第一范式：

第一：没有主键，第二：联系方式可以分为邮箱地址和电话

更改：

```mysql
学生编号(PK)    学生姓名    邮箱地址 		  电话
------------------------------------------------------------------
1001	  		张三      zs@gmail.com	13994822222
1002	   		李四		ls@gmail.com	13699999999
1003	   		王五		ww@gmail.com	13488789564
```

## 第二范式

建立在第一范式的基础之上，要求所有非主键字段完全依赖于主键，不要产生部分依赖

**案例**：

描述老师和学生关系：

```mysql
学生编号    	学生姓名    教师编号		  教师姓名
------------------------------------------------------------------
1001	  		张三      001				王老师		
1002	   		李四		002				赵老师
1003	   		王五		001				王老师
1001	  		张三      002				赵老师
```

**分析**：

​	不满足第一范式：没有主键

 （一个学生可能有多个老师，一个老师有多个学生，**非常典型的：多对多关系！**）

**修改**为满足第一范式：

```mysql
学生编号 + 教师编号(PK)		学生姓名   		  教师姓名
------------------------------------------------------------------
1001	    001			张三   		王老师		
1002	   	002			李四			赵老师
1003	   	001			王五			王老师
1001	  	002			张三    		赵老师
```

学生编号，教师编号：两个字段联合做主键，复合主键（PK：学生编号+教师编号）	

**分析**：

不满足第二范式，张三依赖1001，王老师依赖001.显然产生了部分依赖

产生部分依赖的缺点：数据冗余，空间浪费，张三重复了，王老师重复了

为了让以上的表满足第二范式，需要这样设计：

**为了使以上的表满足第二范式，需这样设计**：

使用三张表来表示多对多关系！

学生表

```mysql
学生编号(PK)     学生名字
------------------------------
1001			张三
1002			李四
1003			王五
```

教师表

```mysql
教师编号(PK)     教师名字
001				王老师
002				赵老师
```

学生教师关系表

```mysql
id(PK)			学生编号(fk)		教师编号(fk)
1				1001				001
2				1002				002
3				1003				001
4				1001				002
```

### 背口诀

​	多对多怎么设计？

​	多对多，三张表，关系表两个外键！！！！！！！！！！！

## 第三范式

建立在第二范式的基础之上，要求所有非主键字段直接依赖主键，**不要产生传递依赖**

**案例**

```mysql
学生编号(PK)   	学生姓名    班级编号	  班级名称
------------------------------------------------------------------
1001	  		张三      01			 一年一班
1002	   		李四		02			 一年二班
1003	   		王五		03			 一年三班
1004	  		赵六      03			 一年三班
```

以上表的设计：是描述班级和学生的关系，很显然是**一对多**的关系

**分析**：

满足第一范式：有主键；

满足第二范式：主键不是复合主键，没有产生部分依赖，主键是单一主键

不满足第三范式：产生了传递依赖

​								一年一班依赖01, 01依赖1001，产生了传递依赖，不符合第三范式的要求，产生了数据的冗余

**修改**

```mysql
班级表(一)
班级编号(PK)     班级名称
---------------------------
01				一年一班
02				一年二班
03				一年三班

学生表(多)
学生编号(PK)   	学生姓名    班级编号(fk)	  
--------------------------------------
1001	  		张三       01			 
1002	   		李四	     02			 
1003	   		王五		 03			
1004	  		赵六       03			 
```

一对多的设计

### 背口诀

​	一对多，两张表，多的表加外键！！！

## 总结表的设计

**一对多**：一对多，两张表，多的表加外键！！

**多对多**：多对多，三张表，关系表两个外键！！

**一对一**：一对一，外键唯一！！

实际开发过程中，可能存在一张表字段太多，太庞大，这时需要拆分表

```mysql
//未拆分之前
t_user
id		login_name		login_pwd		real_name		email		address...
-------------------------------------------------------------------------------
1       zhangsan		123				张三			zhangsan@xxx
2		lisi			123				李四			lisi@xxx
...
```

这种庞大的表建议拆分为两张

t_login	登录信息表

```mysql
id(PK)		login_name		login_pwd	
-----------------------------------
1       zhangsan		123				
2		lisi			123				
...
```

t_user	用户详细信息表

```mysql
id(PK)		real_name		email		address...	login_id(fk+unique)	
------------------------------------------------------------------------
100			张三			zhangsan@xxx				1
200			李四			lisi@xxx					2
...
```

口诀：一对一，外键唯一！！！！

# 嘱咐一句话

```mysql
数据库设计三范式是理论上的。
实际和理论有的时候有偏差
最终的目的都是为了满足客户的需求，有时候会拿冗余换执行速度。
因为在sql中，表和表连接线次数越多，效率越低（笛卡尔积）
有的时候可能会存在冗余，但是为了减少表的连接顺序，这样做也是合理的
并且对于来发人员来说，sql语句的编写难度也会降低
```

注意：面试的时候把这句话说上，他就不会认为你是初级程序员了！！！
