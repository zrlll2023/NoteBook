---

---

---
column:列，字段
row：行

集合查询：
SELECT * FROM table_name WHERE column IN （ , , );

---

ORDER BY：排序方式
DESC:降序，从大到小，从高到低
ASC：升序，从小到大，A 到 Z

排序：
ORDER BY column1 ASC/DESC ，column2 ASC/DESC（是指如果column1出现一样，那么用column作参考）;

---

LIMIT（限制）：规定最多返回多少条数据。
OFFSET（偏移/跳过）：规定跳过前面的多少条数据再开始读取

分页查询：
LIMIT 5 OFFSET 10;
简写形式：LIMIT 10, 5;

跳过排在最前面的前 10 个人，从第 11 个人开始，只连续拿 5 个人的数据

分页公式（写代码超常用）：
如果你在写后端代码做分页，前端传给你两个参数：page（当前页码，从 1 开始）和 pageSize（每页显示多少条）。

你可以直接套用这个公式来计算 LIMIT 和 OFFSET 的值：

LIMIT = pageSize
OFFSET = (page - 1) \times pageSize

---

DISTINCT:去重
IS NOT NULL：不是空值，“把那些填了信息的、有具体数据的挑出来。”

去重查询：
SELECT DISTINCT column1 FROM tablename WHERE column IS NOT NULL;

---

AS ... :起别名

比如：count(student_id) AS total_count
这样输出的结果的表头就是 total_count 而不是 count(student_id)  

其实AS可以省略
所以以后多表关联查询当中也能运用这个起别名

---



7,10,15,18,19,20,25，26-30