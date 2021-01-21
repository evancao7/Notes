USE myemployees;

#1.查询表中的单个字段
SELECT last_name FROM employees;

#2.查询表中多个字段
SELECT last_name,salary,email FROM employees;

#3.查询表中的所有字段
SELECT * FROM employees;

#4.查询常量
# select 常量值;
# 注意：字符型和日期型的常量值必须用单引号引起来，数值型不需要
SELECT 100;
SELECT 'join';

#5.查询函数
#select 函数名(实参列表);
SELECT VERSION();

#6.查询表达式 
SELECT 100%98;

#7.起别名
/*
1.便于理解
2.如果要查询的字段有重名的情况,使用别名区分
*/
#方式一:使用AS
SELECT 100%98 AS 结果;
SELECT last_name AS 姓,first_name AS 名 FROM employees;

#方式二:使用空格
SELECT last_name 姓,first_name 名 FROM employees;

#案例:查询salary,结果显示 out put
SELECT salary AS "out put" FROM employees;

#8.去重
# select distinct 字段名 from 表名;只能对一个去重，例如select distinct 字段名1 , distinct 字段名2 from 表名；这样是不行的
#案例:查询员工表中涉及的所有部门编号
SELECT DISTINCT department_id FROM employees;

#9.+号的作用
#案例:查询员工的名和姓,并显示为姓名
/*
java中的+号:
1.运算符:两个操作数都为数据型
2.连接符:只要有一个操作数为字符串


mysql中的+号:
只能作为运算符

select 100+90; 两个操作数都为数值型,做加法运算
select '123+90';其中一方为字符型,试图将字符型数值转换为数值型
		如果转换成功,则继续做加法运算
select 'john'+90; 如果转换失败,则将字符型数值转换成0

select null+0; 只要其中一方为null,则结果肯定为null.
*/
SELECT last_name+first_name AS 姓名 FROM employees; 

#10.【补充】concat函数 
/*
功能：拼接字符
select concat(字符1，字符2，字符3,...);
*/
SELECT CONCAT('a','b','c') AS 结果 FROM employees;

SELECT CONCAT(last_name,first_name) AS 姓名 FROM employees;

#11.【补充】ifnull函数
#功能：判断某字段或表达式是否为null，如果为null 返回指定的值，否则返回原本的值
此处如果commission_pct为null则返回0
SELECT IFNULL(commission_pct,0) FROM employees;

#12.【补充】isnull函数
#功能：判断某字段或表达式是否为null，如果是，则返回1，否则返回0

一、按条件表达式筛选
	条件运算符:> < =(mysql中只有一个=) != <>前两个都能表示不等于  >= <= <=>安全等于
二、按逻辑表达式筛选
	逻辑运算符:&& || !
	and or not
	
	&& 和 and:两个条件都为true，结果为true，反之为false
	|| 和 or:只要有一个条件为true，结果为true，反之为false
	! 或 not:如果连接的条件本身为false，结果为true，反之为false	
	
三、模糊查询
	like:一般搭配通配符使用，可以判断字符型或数值型
	通配符：%任意多个字符，_任意单个字符
	like、between and、in、is null


#一.按条件表达式筛选

#案例1:查询工资>12000的员工信息
SELECT * FROM employees WHERE salary>12000;

#案例2:查询部门编号不等于90号的员工名和部门编号
SELECT last_name,department_id FROM employees WHERE department_id <> 90;

#二、按逻辑表达式筛选

#案例1:查询工资z在10000到20000之间的员工名、工资及奖金
SELECT last_name,salary,commission_pct FROM employees WHERE salary>=10000 AND salary<=20000;

SELECT
	last_name,salary,commission_pct
FROM
	employees	
WHERE	salary>=10000 AND salary<=20000;

#案例2:查询部门编号不是在90-110之间,或者工资高于15000的员工信息
SELECT * FROM employees WHERE department_id <90 OR department_id>110 OR salary>15000;

SELECT *
FROM employees
WHERE !(department_id>=90 AND department_id<=110)||(salary>=15000);


#三、模糊查询

#1.like  可以判断数字和字符

#案例1:查询员工名中包含字符a的员工信息
SELECT * FROM employees WHERE last_name LIKE '%a%';   %在这里代表通配符表示任意多个字符，也可以代表0个字符，单双引号都行，默认不屈分大小写

#案例2:查询员工名中第三个字符为b，第五个字符为a的员工名和工资
SELECT last_name,salary FROM employees WHERE last_name LIKE '__b_a%';       _只能代表单个字符

#案例3:查询员工名种第二个字符为_的员工名
SELECT last_name FROM employees WHERE last_name LIKE '_\_%';        通过\转译

SELECT 
	*
FROM  
	employees
WHERE
	last_name LIKE "_a_%" ESCAPE "a";       表示a在这里起着转译功能

#2.between and

#案例1:查询员工编号在100到120之间的员工信息
SELECT * FROM employees WHERE employee_id>=100 AND employee_id<=120;

SELECT * FROM employees WHERE employee_id BETWEEN 100 AND 120;

/*注意事项：
1.提高语句简洁度
2.包含临界值
3.两个临界值不能调换顺序
*/

#3.in
/*
含义:判断某字段的值是否属于in列表中的某一项
特点:
 1.使用in提高语句简洁度
 2.in列表的值类型必须一致或兼容！！
 3.不支持通配符
*/
#案例1:查询员工的工种编号是IT_PROG、AD_VP、AD_PRES中的一个员工名和工种编号

SELECT last_name,job_id FROM employees WHERE job_id='IT_PROG' OR job_id='AD_PRES' OR job_id='AD_VP';or可以用||代替

SELECT last_name,job_id FROM employees WHERE job_id IN('IT_PROG','AD_PRES','AD_VP');

#4.is null
/*
=或<>不能用于判断null值！！
is null 或 is not null 可以判断null值 ！！
*/
#案例1:查询没有奖金的员工名和奖金率

SELECT last_name,commission_pct FROM employees WHERE commission_pct IS NULL;
查询有奖金的员工名和奖金率
SELECT last_name,commission_pct FROM employees WHERE commission_pct IS NOT NULL;

#安全等于 <=>
即可以判断null值，也能判断普通类型的null值
#案例1:查询没有奖金的员工名和奖金率

SELECT last_name,commission_pct FROM employees WHERE commission_pct <=> NULL;

#案例2:查询工资为12000的员工信息
SELECT last_name,commission_pct FROM employees WHERE salary <=> 12000;

#is null 比较 安全等于 <=>
#	      普通类型的数值	null值		可读性
# is null	×		        √		  √
# <=>		√		        √		  ×



#案例1:查询员工信息,要求工资从高到低排序
SELECT * FROM employees ORDER BY salary DESC;
SELECT * FROM employees ORDER BY salary;

#案例2:查询部门编号是>=90，按入职时间的先后进行排序
SELECT * FROM employees WHERE department_id>=90 ORDER BY hiredate ASC;

#案例3:按年薪的高低显示员工的信息和年薪【按表达式排序】
SELECT *,salary*12*(1+IFNULL(commission_pct,0)) 年薪 FROM employees 
ORDER BY salary*12*(1+IFNULL(commission_pct,0)) DESC; 

#案例4:按年薪的高低显示员工的信息和年薪【按别名排序】

SELECT *,salary*12*(1+IFNULL(commission_pct,0)) 年薪 FROM employees 
ORDER BY salary*12*(1+IFNULL(commission_pct,0)) 年薪 DESC; 

#案例5:按姓名的长度显示员工的姓名和工资【按函数排序】
SELECT LENGTH(last_name) 字节长度,last_name,salary
FROM employees
ORDER BY LENGTH(last_name) DESC;

#案例6:查询员工共信息,要求按工资排序，再按员工编号排序【按多个字段排序】
SELECT * FROM employees
ORDER BY salary ASC,employee_id DESC;
