```sql
USE [tableName] --使用哪张表

--添加项目
ALTER TABLE department  
ADD PersoNum INT,   
Office VARCHAR(50)  

--更改行的数据类型
ALTER TABLE department
ALTER COLUMN Manger VARCHAR(50);

--重命名行
EXEC sp_RENAME 'Manager', 'ManagerName', 'COLUMN';    --将Manager重命名为ManagerName

GO --用于分割语句，等上面执行完再执行下方

--添加约束
--例1
ALTER TABLE department
ADD CONSTRAINT uk_dp139 UNIQUE(DepartmentName); --UNIQUE表示唯一约束
--例2
ALTER TABLE Employee
ADD CONSTRAINT DepartmentID DEFAULT '销售部' FOR department;--添加默认约束

--删除约束
ALTER TABLE department
DROP CONSTRAINT uk_dp139

--SELECT
SELECT TOP 20* FROM Product     --查询Product表从头开始的20行数据

SELECT id, CustomName, phone FROM Customer 
WHERE CompanyName LIKE '%华'    --'%'为通配符，用来代指查询字符前的某某文字段

SELECT id, name, price FROM Product
ORDER BY price DESC     --"ORDER BY"为排序，DESC 为逆序，ASC为正序

--INSERT INTO
INSERT INTO Employee(EmployeeID)
VALUES('123456')    --新增一名id为123456的员工

UPDATE Employee 
SET BirthDate = '2004-2-2'  
WHERE EmployeeID = 123456;   --更新id为123456的生日为'2004-2-2'

DELETE FROM Employee
WHERE EmployeeID = 123456;   --删除id为123456的员工

--寻找牵扯到其他表的项目
UPDATE Product
SET price = price*1.1
WHERE ProductID IN(     --将提供商为'杭州浦沿量具厂'的产品价格上调10%
    SELECT ProductID FROM Provider
    WHERE ProviderName = '杭州浦沿量具厂'
);

--计算时间差值使用DATEDIFF函数
SELECT EmployeeID, EmployeeName FROM Employee
WHERE DepartmentID = '销售部' AND DATEDIFF(YEAR, HireDate, GETDATE()) > 20;
--原题目
--公司原来的销售部主管离职，请在该部门选出符合主管条件的员工名单（工龄大于20年）


--GROUP BY 语句
--当查询中包含了函数时，语句中要加GROUP BY语句来分组，除了函数其他的查询变量都要加入GROUP BY语句中

SELECT CustomerID, SUM(TotalAmount) AS TotalOrderAmount
FROM Orders
GROUP BY CustomerID;

--JOIN语句
当使用的查询内容包含其他表中的变量就要用JOIN语句
SELECT Customers.CustomerID, , Email, OrderID, OrderDate, TotalAmount FROM Customers
INNER JOIN Orders ON Customers.CustomerID = Orders.CustomerID;
--JOIN语句后加xx.xx = yy.xx是为了同步变量 
```
