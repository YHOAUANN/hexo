---
title: sql基础
date: 2024-06-12 18:21:23
categories: 
- 技术
- 数据库
tags:
- sql

---




{% note success %}
	最后更新时间：2024年6月17日 14:18:30
{% endnote %}

# 选择语句
```mysql
SELECT *
FROM table_name;
```

### 选择子句

```mysql
SELECT (column1, column2, column3)
FROM table_name;
```

### WHERE子句

```mysql
SELECT *
FROM table_name
WHERE condition;
```

### AND、OR、NOT运算符

```mysql
SELECT *	
FROM table_name
WHERE condition1 AND condition2;

SELECT *	
FROM table_name
WHERE condition1 OR condition2;

SELECT *	
FROM table_name
WHERE NOT condition;
```

### IN运算符

```mysql
SELECT *	
FROM table_name
WHERE column IN (value1, value2, value3);
```

### BETWEEN运算符

```mysql
SELECT *	
FROM table_name
WHERE column BETWEEN value1 AND value2;
```

### LIKE运算符

```mysql
SELECT *	
FROM table_name
WHERE column LIKE pattern;
```

### REGEXP运算符

```mysql
SELECT *	
FROM table_name
WHERE column REGEXP pattern;
```

### NULL运算符

```mysql	
SELECT *	
FROM table_name
WHERE column IS NULL;
```

### ORDER BY子句

```mysql
SELECT *	
FROM table_name
ORDER BY column1, column2;
```

### LIMIT子句

```mysql
SELECT *		
FROM table_name
LIMIT number;
```

# 内连接	

```mysql
SELECT *
FROM table1 t1
INNER JOIN table2 t2
ON t1.column1 = t2.column1;
```

### 跨表连接

```mysql
SELECT *
FROM table1 t1
CROSS JOIN table2 t2;
```

### 自连接

```mysql
SELECT *
FROM table1 t1, table1 t2
WHERE t1.column1 = t2.column1;
```

### 多表连接

```mysql
SELECT *
FROM table1 t1
JOIN table2 t2
ON t1.column1 = t2.column1
JOIN table3 t3
ON t1.column1 = t3.column1;
```

### 复合连接

```mysql	
SELECT *
FROM table1 t1
JOIN table2 t2
ON t1.column1 = t2.column1
JOIN table3 t3
ON t1.column1 = t3.column1
WHERE t1.column2 = 'value1'
AND t2.column2 = 'value2'
AND t3.column2 = 'value3';
```


### 隐式连接

```mysql
SELECT *
FROM table1 t1, table2 t2
WHERE t1.column1 = t2.column1;
```
### USING子句

```mysql
SELECT *
FROM table1 t1
JOIN table2 t2
USING (column1);
```

### 自然连接

```mysql
SELECT *
FROM table1 t1
NATURAL JOIN table2 t2;
```
### 交叉连接

```mysql
SELECT *
FROM table1 t1
CROSS JOIN table2 t2;
```

### 联合

```mysql
SELECT *
FROM table1 t1
UNION
SELECT *
FROM table2 t2;
```

# 增删改

### 插入数据

```mysql
INSERT INTO table_name (column1, column2, column3)
VALUES (value1, value2, value3);
```

### 更新数据

```mysql
UPDATE table_name	
SET column1 = value1, column2 = value2, column3 = value3
WHERE condition;
```
### 删除数据

```mysql
DELETE FROM table_name
WHERE condition;
```
# 聚合函数
	
### GROUP BY子句
	 
```mysql
SELECT column1, column2, SUM(column3)
FROM table_name
GROUP BY column1, column2;
```

### HAVING子句

```mysql	
SELECT column1, column2, SUM(column3)
FROM table_name
GROUP BY column1, column2
HAVING condition;
```

### ROLLUP运算符

```mysql
SELECT column1, column2, SUM(column3)
FROM table_name
GROUP BY ROLLUP(column1, column2);
```

# 复杂查询

### 子查询

```mysql
SELECT *
FROM table1 t1
WHERE column1 = (SELECT column2 FROM table2 t2 WHERE t1.column1 = t2.column1);
```

### IN运算符

```mysql	
SELECT *
FROM table1 t1
WHERE column1 IN (SELECT column2 FROM table2 t2 WHERE t1.column1 = t2.column1);
```	

### ALL关键字
```mysql
SELECT *
FROM table1 t1
WHERE column1 = ALL (SELECT column2 FROM table2 t2 WHERE t1.column1 = t2.column1);
```

### ANY关键字

```mysql
SELECT *
FROM table1 t1
WHERE column1 = ANY (SELECT column2 FROM table2 t2 WHERE t1.column1 = t2.column1);
```

### 相关子查询

```mysql	
SELECT *
FROM table1 t1
WHERE column1 = (SELECT column2 FROM table2 t2 WHERE t1.column1 = t2.column1)
AND column3 = (SELECT column4 FROM table3 t3 WHERE t1.column1 = t3.column1);
```

### EXISTS运算符

```mysql
SELECT *
FROM table1 t1
WHERE EXISTS (SELECT * FROM table2 t2 WHERE t1.column1 = t2.column1);
```	

### SELEC子句中的子查询

```mysql
SELECT *
FROM table1 t1
WHERE column1 IN (SELECT column2 FROM table2 t2 WHERE t1.column1 = t2.column1)
AND column3 = (SELECT column4 FROM table3 t3 WHERE t1.column1 = t3.column1);
```

### FROM子句中的子查询

```mysql
SELECT *
FROM (SELECT column1, column2 FROM table1) t1
WHERE column1 IN (SELECT column2 FROM table2 t2 WHERE t1.column1 = t2.column1);
```
# 数值函数

### 字符串函数
```mysql
SELECT LENGTH(column1), UPPER(column2), LOWER(column3), SUBSTRING(column4, 1, 5), REPLACE(column5, 'old', 'new')
FROM table_name;
```
### 日期函数

```mysql
SELECT CURDATE(), CURTIME(), NOW(), DATE_FORMAT(NOW(), '%Y-%m-%d %H:%i:%s'), TIMESTAMP(NOW()), TIMESTAMP('2024-06-12 18:21:23'), DATEDIFF(NOW(), '2024-06-12 18:21:23'), DATE_ADD(NOW(), INTERVAL 1 DAY), DATE_SUB(NOW(), INTERVAL 1 DAY)
FROM table_name;
```

### IFNULL函数和COALESCE函数

```mysql	
SELECT IFNULL(column1, 'default_value')
FROM table_name;

SELECT COALESCE(column1, column2, column3)
FROM table_name;
```

### IF函数

```mysql
SELECT IF(column1 > 10, 'greater than 10', 'less than or equal to 10')
FROM table_name;
```
### CASE运算符

```mysql
SELECT CASE column1
    WHEN value1 THEN 'value1'
    WHEN value2 THEN 'value2'
    ELSE 'other'
END
FROM table_name;
```

# 视图
	
### 创建视图

```mysql
CREATE VIEW view_name AS
SELECT column1, column2, column3
FROM table_name
WHERE condition;
```

### 更改或删除视图

```mysql
ALTER VIEW view_name AS
SELECT column1, column2, column3
FROM table_name
WHERE condition;


DROP VIEW view_name;
```
### WITH OPTION CHECK子句

```mysql
CREATE VIEW view_name AS
SELECT column1, column2, column3
FROM table_name
WHERE condition
WITH CHECK OPTION;
```

# 存储过程

存储过程身一个包含一堆SQL代码的数据库对象，在我们的应用代码里，我们调用这些过程来获取或者保存数据，所以我们使用存储过程来存储和挂历SQL代码



### 创建一个存储过程

```mysql
DELIMITER $$ -- 修改分隔符
CREATE PROCEDURE get_clients() 
BEGIN
	SELECT * FROM clients;
END$$

DELIMITER ;  -- 修改分隔符
```

 ### 调用存储过程

```mysql
CALL get_clients() 
```

### 删除存储过程

```mysql
DROP PROCEDURE get_clients
```

```mysql
DROP PROCEDURE IF EXISTS get_clients
-- 更安全的删除过程方法
```

### 参数

```mysql
DROP PROCEDURE IF EXISTS get_clients;

DELIMITER $$
CREATE PROCEDURE get_clients(
	state CHAR(2)
)
BEGIN
	SELECT * FROM clients c
    WHERE c.state = state;
END $$

DELIMITER ;
```

```mysql
CALL get_clients('CA')	
```

### 带有默认值的参数

```mysql
DROP PROCEDURE IF EXISTS get_clients;

DELIMITER $$
CREATE PROCEDURE get_clients(
	state CHAR(2)
)
BEGIN
	IF state IS NULL THEN
		SET state = 'CA';
	END IF;
    
	SELECT * FROM clients c
    WHERE c.state = state;
END $$

DELIMITER ;
```

```mysql
CALL get_clients(NULL)
```

### 参数验证

```mysql
DELIMITER $$
CREATE PROCEDURE make_payment
(
	invoices_id INT,
    payment_amount DECIMAL(9,2),
    payment_date DATE
)
BEGIN
	IF payment_amount < 0 THEN 
		SIGNAL SQLSTATE '22003' 
			SET MESSAGE_TEXT = 'Invalid payment amount';
    END IF;
	UPDATE invoices i
    SET 
		i.payment_total = payment_amount,
        i.payment_date = payment_date
	WHERE i.invoice_id = invoice_id;
END $$

DELIMITER ;
```

### 输出参数

```mysql
DELIMITER $$
CREATE PROCEDURE get_unpaid_invoices_for_client
(
	client_id INT
)
BEGIN
	SELECT COUNT(*),SUM(invoice_total)
    FROM invoices i
    WHERE i.client_id = client_id
		AND payment_total = 0;
END $$

DELIMITER ;
```

### 变量

```mysql
DELIMITER $$
CREATE PROCEDURE get_risk_factor()
BEGIN
	DECLARE risk_factor DECIMAL(9,2) DEFAULT 0;
    DECLARE invoices_total DECIMAL(9,2);
    DECLARE invoices_count INT;
    
    SELECT COUNT(*), SUM(invoice_total)
    INTO invoices_count,invoices_total
    FROM invoices;
    
    SET risk_factor = invoices_total - invoices_count * 5;
    SELECT risk_factor;
END $$

DELIMITER ;
```
### 函数

```mysql
DELIMITER $$
CREATE FUNCTION get_risk_factor_for_client
(
	client_id INT
)
RETURNS INTEGER
READS SQK DATA
BEGIN
	DECLARE risk_factor DECIMAL(9,2) DEFAULT 0;
    DECLARE invoices_total DECIMAL(9,2);
    DECLARE invoices_count INT;
    
    SELECT COUNT(*), SUM(invoice_total)
    INTO invoices_count,invoices_total
    FROM invoices i
	WHERE i.client_id = client_id;
    
    SET risk_factor = invoices_total - invoices_count * 5;
    SELECT risk_factor;

	RETURN IFNULL(risk_factor,0);
END
```
# 触发器

### 创建触发器
```mysql
DELIMITER $$

CREATE TRIGGER payment_after_insert
	AFTER INSERT ON payments
    FOR EACH ROW
BEGIN
	UPDATE invoices
    SET payment_total = payment_total + NEW.amount
    WHERE invoice_id = NEW.invoice_id;
END $$

DELIMITER ;	
```
### 查看触发器

```mysql
SHOW TRIGGERS;
```

### 删除触发器

```mysql
DROP TRIGGER payment_after_insert
```

### 记录触发器

```mysql
DELIMITER $$

CREATE TRIGGER payment_after_insert
	AFTER INSERT ON payments
    FOR EACH ROW
BEGIN
	UPDATE invoices
    SET payment_total = payment_total + NEW.amount
    WHERE invoice_id = NEW.invoice_id;
    
    INSERT INTO payments_audit
    VALUES (NEW.client_id, NEW.date, NEW.amount, 'Insert', NOW());
END $$


DELIMITER ;
```

