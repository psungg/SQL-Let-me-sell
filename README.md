# SQL-Let me sell
## Relationship Diagram
![Relationship Diagram](https://github.com/psungg/SQL-Let-me-sell/blob/main/Images/Relationship_Diagram.png)

## 1. Customer Name in Bangkok

```
SELECT Fname, Lname
FROM customer LEFT JOIN post_code on customer.Post_code = Post_code.Post_code
WHERE post_code.Province = 'Bangkok';
```

![Fig01](https://github.com/psungg/SQL-Let-me-sell/blob/main/Images/Fig01.png)

## 2. Amount of orders by product

```
SELECT 
	Product_ID, 
    SUM(Amount)
FROM ordering
GROUP BY
	Product_ID;
```

![Fig02](https://github.com/psungg/SQL-Let-me-sell/blob/main/Images/Fig02.png)


## 3. Best selling products

```
SELECT 
	Product_ID, 
    SUM(Amount) AS total_amt
FROM ordering
GROUP BY
	Product_ID
ORDER BY
	total_amt DESC;
```

![Fig03](https://github.com/psungg/SQL-Let-me-sell/blob/main/Images/Fig03.png)

## 4. Amount of order by product

```
SELECT
  o.Product_ID,
  o.Amount,
  p.price
FROM
  ordering o LEFT JOIN product p ON o.Product_ID = p.Product_ID;
```

![Fig04](https://github.com/psungg/SQL-Let-me-sell/blob/main/Images/Fig04.png)

## 5. Best Selling Product by overall_amt

```
SELECT Product_ID, SUM(total_price) as overall_amt
FROM (SELECT *,	Amount * Price AS total_price
      FROM (SELECT o.Product_ID, o.Amount, p.Price
            FROM ordering o LEFT JOIN product p ON o.Product_ID = p.Product_ID) t1) t2
GROUP BY
	Product_ID
ORDER BY
	overall_amt DESC;
```

![Fig05](https://github.com/psungg/SQL-Let-me-sell/blob/main/Images/Fig05.png)

## 6. Ordering amount by customer

```
SELECT 
	c.Customer_ID, 
	SUM(o.Amount * p.Price) AS total_amt
FROM customer c LEFT JOIN ordering o ON c.Customer_ID = o.Customer_ID LEFT JOIN product p ON o.Product_ID = p.Product_ID
GROUP BY c.Customer_ID
ORDER BY total_amt DESC
LIMIT 10;
```

![Fig06](https://github.com/psungg/SQL-Let-me-sell/blob/main/Images/Fig06.png)

## 7. Customer with the most total orders

```
SELECT 
	c.Fname, 
    c.Lname, 
    COUNT(o.Order_ID) AS total_order
FROM customer c LEFT JOIN ordering o ON c.Customer_ID = o.Customer_ID
GROUP BY c.Fname, c.Lname
ORDER BY total_order DESC
LIMIT 10;
```

![Fig07](https://github.com/psungg/SQL-Let-me-sell/blob/main/Images/Fig07.png)

