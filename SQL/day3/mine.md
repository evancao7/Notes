查询没有奖金，且工资小于18000的salary和last_name
SELECT salary , last_name
FROM employees
WHERE commission_pct IS NULL && salary<18000;

查询employees表中，job_id不为'IT'或者工资为12000的员工信息
SELECT *
FROM employees	
WHERE job_id != "IT" || salary =12000;

查询departments表的结构
DESC departments;

查询表中涉及了那些位置编号，去重
SELECT DISTINCT location_id
FROM departments;