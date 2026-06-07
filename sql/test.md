# 30 道 MySQL 基础练习题（题目版）

### 准备工作：测试数据表结构

为了完成后面的题目，我们先虚拟两张经典的表格：

1. **学生表 (`students`)**：保存学生基本信息。
    
2. **成绩表 (`scores`)**：保存学生的学科成绩。
    

```
-- 创建学生表
CREATE TABLE students (
    id INT AUTO_INCREMENT PRIMARY KEY COMMENT '学生ID',
    name VARCHAR(50) NOT NULL COMMENT '姓名',
    gender VARCHAR(10) COMMENT '性别',
    age INT COMMENT '年龄',
    class_name VARCHAR(50) COMMENT '班级',
    join_date DATE COMMENT '入学日期'
);

-- 创建成绩表
CREATE TABLE scores (
    id INT AUTO_INCREMENT PRIMARY KEY COMMENT '成绩ID',
    student_id INT COMMENT '学生ID',
    subject VARCHAR(50) COMMENT '学科',
    score DECIMAL(5,2) COMMENT '分数',
    exam_date DATE COMMENT '考试日期'
);
```

### 一、 数据库与表结构操作 (DDL) 篇 (第 1 - 5 题)

- **第 1 题**：创建一个名为 `school_db` 的数据库，并指定字符集为 `utf8mb4`。
    
- **第 2 题**：在学生表 `students` 中添加一个名为 `email` 的字段，类型为 `VARCHAR(100)`。
    
- **第 3 题**：将学生表 `students` 中 `gender` 字段的长度修改为 `VARCHAR(20)`。
    
- **第 4 题**：删除学生表 `students` 中的 `email` 字段。
    
- **第 5 题**：安全地删除一个名为 `temp_scores` 的临时表（即如果存在才删除）。
    

### 二、 数据增删改 (DML) 篇 (第 6 - 10 题)

- **第 6 题**：向学生表 `students` 中插入一条记录：姓名 '张三'，性别 '男'，年龄 18，班级 '一班'，入学日期 '2025-09-01'。
    
- **第 7 题**：向成绩表 `scores` 中同时插入三条记录：
    
    1. 学生ID为 1，学科 '数学'，分数 90，考试日期 '2026-01-10'。
        
    2. 学生ID为 1，学科 '语文'，分数 85，考试日期 '2026-01-11'。
        
    3. 学生ID为 2，学科 '数学'，分数 55，考试日期 '2026-01-10'。
        
- **第 8 题**：将学生表 `students` 中名为 '张三' 的学生的年龄修改为 19 岁。
    
- **第 9 题**：将成绩表 `scores` 中所有低于 60 分的成绩提高 5 分。
    
- **第 10 题**：删除成绩表 `scores` 中所有学生ID为 2 且科目为 '语文' 的成绩记录。
    

### 三、 基础查询 (DQL) 篇 (第 11 - 20 题)

- **第 11 题**：查询学生表 `students` 中的所有学生的全部信息。
    
- **第 12 题**：查询所有学生的姓名和班级，并将列名显示为“学生姓名”和“所属班级”。
    
- **第 13 题**：查询学生表 `students` 中年龄大于等于 18 岁的所有男生。
    
- **第 14 题**：查询年龄在 18 到 20 岁之间（包含 18 和 20）的所有学生信息。
    
- **第 15 题**：查询班级为 '一班'、'二班' 或 '三班' 的学生。
    
- **第 16 题**：查询学生表中姓名以 '张' 开头的所有学生。
    
- **第 17 题**：查询学生表 `students` 中没有分配班级（即 `class_name` 为空）的学生。
    
- **第 18 题**：查询所有学生的姓名 and 年龄，并按照年龄从大到小（降序）排序；如果年龄相同，按姓名升序排序。
    
- **第 19 题**：查询学生表中年龄最大的前 3 名学生的信息。
    
- **第 20 题**：查询学生们都分布在哪些不同的班级（去掉重复的班级名）。
    

### 四、 聚合与分组查询 (DQL 进阶) 篇 (第 21 - 25 题)

- **第 21 题**：统计学生表 `students` 中一共有多少名学生。
    
- **第 22 题**：查询成绩表 `scores` 中，'数学' 科目的最高分、最低分以及平均分。
    
- **第 23 题**：按班级分组，统计每个班级各有多少名学生。
    
- **第 24 题**：求出每个班级的平均年龄，但只显示平均年龄大于 18 岁的班级。
    
- **第 25 题**：在成绩表 `scores` 中，按学科分组，统计每科及格（大于等于60分）的学生人数。
    

### 五、 多表关联与复杂查询 篇 (第 26 - 30 题)

- **第 26 题**：查询学生的姓名、考试科目和考试成绩（只显示有成绩的学生信息）。
    
- **第 27 题**：查询所有学生的姓名、科目和成绩。要求即使某些学生没有考试成绩，也要把他们的姓名列出来（成绩字段显示为 NULL）。
    
- **第 28 题**：查询成绩表 `scores` 中，比“数学”平均分高的所有学生的 ID 和成绩。
    
- **第 29 题**：查询平均成绩大于 85 分的学生的姓名和他们的平均成绩。
    
- **第 30 题**：查询“数学”科目考试成绩前 3 名的学生姓名和其数学成绩。
    

## 第三部分：参考答案与详细解析

### 一、 数据库与表结构操作 (DDL) 答案

#### 1. 创建数据库

```
CREATE DATABASE school_db CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;
```

#### 2. 新增表字段

```
ALTER TABLE students ADD email VARCHAR(100);
```

#### 3. 修改表字段属性

```
ALTER TABLE students MODIFY gender VARCHAR(20);
```

#### 4. 删除表字段

```
ALTER TABLE students DROP COLUMN email;
```

#### 5. 删除表

```
DROP TABLE IF EXISTS temp_scores;
```

### 二、 数据增删改 (DML) 答案

#### 6. 单条数据插入

```
INSERT INTO students (name, gender, age, class_name, join_date)
VALUES ('张三', '男', 18, '一班', '2025-09-01');
```

#### 7. 批量数据插入

```
INSERT INTO scores (student_id, subject, score, exam_date) VALUES 
(1, '数学', 90.00, '2026-01-10'),
(1, '语文', 85.00, '2026-01-11'),
(2, '数学', 55.00, '2026-01-10');
```

#### 8. 数据条件更新

```
UPDATE students SET age = 19 WHERE name = '张三';
```

#### 9. 批量数据更新

```
UPDATE scores SET score = score + 5 WHERE score < 60;
```

#### 10. 数据条件删除

```
DELETE FROM scores WHERE student_id = 2 AND subject = '语文';
```

### 三、 基础查询 (DQL) 答案

#### 11. 全表查询

```
SELECT * FROM students;
```

#### 12. 指定字段查询与别名

```
SELECT name AS '学生姓名', class_name AS '所属班级' FROM students;
```

#### 13. 条件过滤 (WHERE)

```
SELECT * FROM students WHERE age >= 18 AND gender = '男';
```

#### 14. 范围查询 (BETWEEN AND)

```
SELECT * FROM students WHERE age BETWEEN 18 AND 20;
-- 或者：SELECT * FROM students WHERE age >= 18 AND age <= 20;
```

#### 15. 集合查询 (IN)

```
SELECT * FROM students WHERE class_name IN ('一班', '二班', '三班');
```

#### 16. 模糊查询 (LIKE)

```
SELECT * FROM students WHERE name LIKE '张%';
```

#### 17. 空值查询 (IS NULL)

```
SELECT * FROM students WHERE class_name IS NULL;
```

#### 18. 结果排序 (ORDER BY)

```
SELECT name, age FROM students ORDER BY age DESC, name ASC;
```

#### 19. 分页查询 (LIMIT)

```
SELECT * FROM students ORDER BY age DESC LIMIT 3;
```

#### 20. 去重查询 (DISTINCT)

```
SELECT DISTINCT class_name FROM students WHERE class_name IS NOT NULL;
```

### 四、 聚合与分组查询 (DQL 进阶) 答案

#### 21. 聚合函数 (COUNT)

```
SELECT COUNT(*) AS total_students FROM students;
```

#### 22. 聚合函数综合 (SUM, AVG, MAX, MIN)

```
SELECT 
    MAX(score) AS max_score, 
    MIN(score) AS min_score, 
    AVG(score) AS avg_score 
FROM scores 
WHERE subject = '数学';
```

#### 23. 分组统计 (GROUP BY)

```
SELECT class_name, COUNT(*) AS student_count 
FROM students 
GROUP BY class_name;
```

#### 24. 分组后过滤 (HAVING)

```
SELECT class_name, AVG(age) AS avg_age 
FROM students 
GROUP BY class_name 
HAVING AVG(age) > 18;
```

- **解析**：
    
    - `WHERE` 关键字在 `GROUP BY` 之前过滤原始数据，不可以使用聚合函数。
        
    - `HAVING` 在分组统计之后对各组结果进行过滤，通常配合聚合函数（如 `AVG()`、`COUNT()` 等）使用。
        

#### 25. 统计每科及格人数

```
SELECT subject, COUNT(*) AS passed_count 
FROM scores 
WHERE score >= 60 
GROUP BY subject;
```

### 五、 多表关联与复杂查询 答案

#### 26. 内连接查询 (INNER JOIN)

```
SELECT s.name, sc.subject, sc.score
FROM students s
INNER JOIN scores sc ON s.id = sc.student_id;
```

#### 27. 左外连接查询 (LEFT JOIN)

```
SELECT s.name, sc.subject, sc.score
FROM students s
LEFT JOIN scores sc ON s.id = sc.student_id;
```

#### 28. 子查询 (Subquery)

```
SELECT student_id, score 
FROM scores 
WHERE subject = '数学' 
  AND score > (SELECT AVG(score) FROM scores WHERE subject = '数学');
```

#### 29. 多表关联 + 分组过滤 (复杂综合)

```
SELECT s.name, AVG(sc.score) AS avg_score
FROM students s
INNER JOIN scores sc ON s.id = sc.student_id
GROUP BY s.id, s.name
HAVING AVG(sc.score) > 85;
```

- **解析**：
    
    - 使用 `INNER JOIN` 将学生基本信息和成绩连接起来。
        
    - 使用 `GROUP BY s.id, s.name` 进行分组。为了防止同名同姓冲突，分组字段应当加上主键 `s.id`。
        
    - 分组后使用 `HAVING` 过滤出平均分大于 85 的学生。
        

#### 30. 多表关联 + 排序限制 (综合应用)

```
SELECT s.name, sc.score
FROM students s
INNER JOIN scores sc ON s.id = sc.student_id
WHERE sc.subject = '数学'
ORDER BY sc.score DESC
LIMIT 3;
```