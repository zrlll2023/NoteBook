### 1. 数据库与表结构操作公式 (DDL)

#### 【公式 1-1】创建数据库（带字符集）

```
CREATE DATABASE 数据库名 CHARACTER SET 字符集名 COLLATE 校对规则;
-- 常用实战公式：
CREATE DATABASE school_db CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;
```

#### 【公式 1-2】修改表结构（加、改、删列）

- **添加新列**：`ALTER TABLE 表名 ADD 列名 数据类型 [约束];`
    
- **修改列属性**：`ALTER TABLE 表名 MODIFY 列名 新数据类型 [新约束];`
    
- **删除列**：`ALTER TABLE 表名 DROP COLUMN 列名;`
    

#### 【公式 1-3】安全删除表

```
DROP TABLE IF EXISTS 表名;
```

### 2. 数据增删改公式 (DML)

#### 【公式 2-1】数据插入 (INSERT)

- **单条插入**：`INSERT INTO 表名 (列1, 列2, ...) VALUES (值1, 值2, ...);`
    
- **批量插入**：
    
    ```
    INSERT INTO 表名 (列1, 列2, ...) VALUES 
    (值1_1, 值1_2, ...),
    (值2_1, 值2_2, ...),
    (值3_1, 值3_2, ...);
    ```
    

#### 【公式 2-2】数据条件更新 (UPDATE)

```
UPDATE 表名 SET 列1 = 新值1, 列2 = 新值2 WHERE 过滤条件;
-- 警惕：如果不加 WHERE 条件，整张表的所有行都会被修改！
```

#### 【公式 2-3】数据条件删除 (DELETE)

```
DELETE FROM 表名 WHERE 过滤条件;
-- 警惕：如果不加 WHERE 条件，整张表的数据会被全部清空！
```

### 3. 单表基础查询公式 (DQL)

#### 【公式 3-1】基础查询与别名 (AS)

- **查询全部**：`SELECT * FROM 表名;`
    
- **查询指定列并起别名**：`SELECT 列名1 AS '别名1', 列名2 AS '别名2' FROM 表名;` (AS 可以省略，但建议保留以增强可读性)
    
- **去重查询**：`SELECT DISTINCT 列名 FROM 表名;`
    

#### 【公式 3-2】条件过滤常用运算符 (WHERE 后接公式)

| 运算符类型     | 语法公式                      | 释义与示例                                       |
| --------- | ------------------------- | ------------------------------------------- |
| **比较运算符** | =, <,>, !=, >, <, >=, <=  | WHERE age >= 18 (年龄大于等于18)                  |
| **逻辑运算符** | `AND`, `OR`, `NOT`        | WHERE gender = '男' AND age >= 18            |
| **区间范围**  | `BETWEEN 值1 AND 值2`       | 包含值1和值2：`WHERE age BETWEEN 18 AND 20`       |
| **集合范围**  | `IN (值1, 值2, ...)`        | 在列表内：`WHERE class_name IN ('一班', '二班')`     |
| **模糊匹配**  | `LIKE '模式'`               | `%`代表任意多字符，`_`代表单个字符：`WHERE name LIKE '张%'` |
| **空值判断**  | `IS NULL` / `IS NOT NULL` | 不能用 `=` 判断空：`WHERE class_name IS NULL`      |

#### 【公式 3-3】排序与分页 (ORDER BY & LIMIT)

```
SELECT 列名 FROM 表名
ORDER BY 列1 DESC, 列2 ASC  
-- DESC 为降序（大到小），ASC 为升序（小到大，默认）
LIMIT [偏移量,] 限制条数;     
-- LIMIT 3 表示取前3条；LIMIT 2, 5 表示从第3条开始取5条
```

### 4. 聚合函数与分组过滤公式 (DQL 进阶)

#### 【公式 4-1】常用聚合函数

聚合函数会对一组值进行计算，并返回单个值。**注意：聚合函数一般不能直接放在 WHERE 后面！**

- **统计行数**：`COUNT(*)` 或 `COUNT(列名)` （忽略 NULL 值）
    
- **求最大值**：`MAX(列名)`
    
- **求最小值**：`MIN(列名)`
    
- **求总和**：`SUM(列名)`
    
- **求平均值**：`AVG(列名)`
    

#### 【公式 4-2】分组统计 (GROUP BY & HAVING)

```
SELECT 分组列, 聚合函数(计算列)
FROM 表名
[WHERE 过滤条件]             
-- 步骤①：在分组前，过滤原始数据行（不可用聚合函数）
GROUP BY 分组列              
-- 步骤②：进行分组
HAVING 聚合函数(计算列) > 值; 
-- 步骤③：在分组后，对聚合结果进行过滤（必须用聚合函数）
```

### 5. 多表关联与复杂查询公式 (核心精髓)

当数据分散在多张表时，我们需要建立表与表之间的通道。

#### 【公式 5-1】多表内连接通用推导式 (N张表 INNER JOIN)

只保留所有表里**完全匹配**的数据行。

- **双表内联公式**：
    
    ```
    SELECT a.列1, b.列2 
    FROM 表A a 
    INNER JOIN 表B b ON a.关联键 = b.关联键;
    ```
    
- **三表内联公式 (向后追加 INNER JOIN 即可)**：
    
    ```
    SELECT a.列1, b.列2, c.列3 
    FROM 表A a 
    INNER JOIN 表B b ON a.关联键 = b.关联键
    INNER JOIN 表C c ON b.关联键 = c.关联键; -- 或者是 a.关联键 = c.关联键
    ```
    

#### 【公式 5-2】左/右外连接公式 (LEFT/RIGHT JOIN)

保留“主表”的所有行，副表不匹配的字段用 `NULL` 填充。

```
SELECT a.列1, b.列2 
FROM 表A a                  -- 【表A】为左表（主表），所有行强制保留
LEFT JOIN 表B b             -- 【表B】为右表（副表）
ON a.关联键 = b.关联键;
```

> **黄金法则**：在实际开发中，`LEFT JOIN` 使用率超过 95%，`RIGHT JOIN` 完全可以通过调换表的左右顺序写成 `LEFT JOIN`。

#### 【公式 5-3】子查询三大标准公式 (Nested Subquery)

子查询即“查询中嵌套查询”。根据嵌套位置和返回值，分为三大公式：

1. **标量子查询公式**（子查询返回**单个值**，用作比较运算符的值）：
    
    ```
    SELECT * FROM 表A WHERE 列1 > (SELECT 聚合函数(列) FROM 表B WHERE 条件);
    ```
    
2. **列子查询公式**（子查询返回**一列多行**，通常配合 `IN`、`ANY`、`ALL` 使用）：
    
    ```
    SELECT * FROM 表A WHERE 列1 IN (SELECT 列1 FROM 表B WHERE 条件);
    ```
    
3. **表子查询公式**（子查询返回**多行多列**，直接作为“临时表”参与 JOIN 关联）：
    
    ```
    SELECT a.列1, temp.聚合列
    FROM 表A a
    INNER JOIN (
        SELECT 关联键, 聚合函数(列) AS 聚合列 FROM 表B GROUP BY 关联键
    ) temp ON a.关联键 = temp.关联键;
    ```
    

#### 【公式 5-4】万能终极查询公式 (多表联查 + 分组 + 过滤 + 排序 + 分页)

这是 SQL 语法的**终极形态**。任何复杂的报表和查询，都可以完美套入以下执行顺序模板中：

```
SELECT 
    a.分组键, 
    b.非分组列 (通常需要配合聚合函数), 
    SUM(c.数值列) AS 别名
FROM 表A a
INNER JOIN 表B b ON a.关联主键 = b.外键
LEFT JOIN 表C c ON b.关联主键 = c.外键
WHERE a.状态列 = '有效'                       -- 【步骤①】关联前/后行过滤
GROUP BY a.分组键, b.非分组列                 -- 【步骤②】分组（保证 SELECT 非聚合列都在这里）
HAVING SUM(c.数值列) > 100                    -- 【步骤③】分组后的聚合结果过滤
ORDER BY 别名 DESC                            -- 【步骤④】排序
LIMIT 偏移量, 限制条数;                       -- 【步骤⑤】分页
```