# Week 7：SQL (SQL)
[首页](00：目录 (Table of Contents).md)

## 目录
* [[#关系型数据库 (Relational Databases)]]
* [[#CRUD 操作 (CRUD Operations)]]
* [[#SQLite 常用命令 (SQLite Commands)]]
* [[#数据库设计 (Database Design)]]
* [[#连接表 (JOINs)]]
* [[#索引 (Indexes)]]
* [[#SQL 注入与安全 (SQL Injection and Security)]]

## 关系型数据库 (Relational Databases)

*   用于大规模存储数据的系统。
*   **CRUD 操作：** 创建 (Create)、读取 (Read)、更新 (Update) 和删除 (Delete)。
*   **SQLite：** 一种轻量级的数据库引擎。

## SQL 常用命令

*   `SELECT`, `INSERT`, `UPDATE`, `DELETE`。
*   **聚合函数：** `AVG`, `COUNT`, `DISTINCT`, `MAX`, `MIN`。
*   **子句：** `WHERE`, `LIKE`（配合 `%` 通配符）, `ORDER BY`, `LIMIT`, `GROUP BY`。

## 数据库设计 (Database Design)

*   为了避免空间浪费，将数据拆分为多个相关的表。
*   **主键 (Primary Key)：** 表中记录的唯一标识符。
*   **外键 (Foreign Key)：** 指向另一个表的主键，用于建立联系。
*   **数据类型：** `INTEGER`, `TEXT`, `REAL`, `NUMERIC`, `BLOB`。

## 连接表 (JOINs)

*   用于临时合并多个表以进行查询。
*   示例：`SELECT * FROM shows JOIN ratings ON shows.id = ratings.show_id`。

## 索引 (Indexes)

*   用于加速查询的优化结构（如 B-树）。
*   **权衡：** 搜索速度更快，但会占用更多存储空间。

## SQL 注入与安全 (SQL Injection and Security)

*   **竞态条件 (Race Conditions)：** 当多个用户同时访问数据时发生。通过事务 (`BEGIN TRANSACTION`, `COMMIT`) 解决。
*   **SQL 注入：** 一种安全漏洞，攻击者通过输入恶意 SQL 代码。通过使用 `?` 占位符（参数化查询）来防止。
