## 创建表
```sql
SHOW DATABASES;
-- 显示当前拥有的数据库

SHOW TABLES
-- 显示拥有的表

CREATE DATABASE $database_name;

DROP DATABASE $database_name;
-- 删除数据库

USE $database_name;
-- 选中当前数据库

CREATE TABLE $table_name (
    id INT,
    name VARCHAR(100)
);
-- 创建表

DESC $table_name;
-- 描述表

DROP TABLE $table_name;
```
## 修改表
```sql
ALTER TABLE $table_name MODIFY COLUMN $table_column_name $new_type; 
-- 修改列的类型

ALTER TABLE $table_name RENAME COLUMN $table_column_name to $new_name;
-- 修改列为新名称

ALTER TABLE $table_name ADD COLUMN $new_name $newtype;
-- 添加新列

ALTER TABLE $table_name DROP COLUMN $new_name; 
-- 删除列
```
## 数据的增删改查
```sql
SELECT * FROM $table_name;
-- 查看所有数据

INSERT INTO $table_name (id, name, level, exp) VALUES (1, 'zyzds', 4, 5);
-- 插入

INSERT INTO $table_name VALUES (1, 'zyzds', 4, 5);
-- 符合形式则可以直接插入

-- 如果 UPDATE 语句报错, 需要执行 SET SQL_SAFE_UPDATES = 0;
UPDATE $table_name SET $column_name = $new_data;
-- 修改所有列的该数据

UPDATE $table_name SET $column_name = $new_data WHERE $unique_name = '$some_data';
-- 更新数据

DELETE FROM $table_name WHERE $condition = $condition_data
```

