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
	最后更新时间：2024年6月14日 13:48:30
{% endnote %}


#  存储过程

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

###　参数验证

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

