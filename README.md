CREATE DATABASE ecommerce_db;
USE ecommerce_db;
CREATE TABLE PRODUCTS(
PRODUCT_ID INT auto_increment PRIMARY KEY,
PRODUCT_NAME VARCHAR (100),
CATEGORY VARCHAR (50),
PRICE DECIMAL (10,2),
STOCK INT 
);
CREATE TABLE SALES(
SALE_ID INT auto_increment PRIMARY KEY,
PRODUCT_ID INT,
CUSTOMER_NAME VARCHAR (100),
CUSTOMER_PHONE VARCHAR (15),
QUANTITY int,
SALE_DATE DATE 
);
INSERT INTO PRODUCTS ( PRODUCT_NAME, CATEGORY, PRICE, STOCK)
VALUES ('Asua ROG Laptop','Electronics', 125000, 15)
, (' Sumsang Galaxy S24', 'Electronics', 95000, 25)
,(' Sony Wireless Headphone',' Accessories', 15000,50)
,( 'Mechanical Keyboard', 'Accessories', 5500,40)
,( 'Ergonomic Office Chair',' Furniture', 18000, 10)
,('Logitech Gaming Mouse','Accessories', 3500, 0)
,(' HP Pavilion laptop',' Electronics' ,75000, 8);
INSERT INTO SALES ( PRODUCT_ID, CUSTOMER_NAME, CUSTOMER_PHONE, QUANTITY, SALE_DATE)
VALUES ( 1,'Tamim Iqbal','01346794152',1, '2026-10-01')
,(3,'Karim Ahmed','01987654321', 2,'2026-10-02')
,(2,'Nusrat Jahan','01555666777', 1,'2026-10-03')
,(4,'Tanjina Khatun','01311223344',3,'2026-10-04')
,(5,'Sadia Afrose','01933887711', 2,'2026-10-05')
,(2,'Farhana Roxy','01344266823', 3,'2026-10-06')
,(2,'Salma Sarkar','01731055692', 6,'2026-10-07');

SELECT*FROM SALES;

### Output:
| SALE_ID | PRODUCT_ID | CUSTOMER_NAME | CUSTOMER_PHONE | QUANTITY | SALE_DATE |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 1 | Tamim Iqbal | 01346794152 | 1 | 2026-10-01 |
| 2 | 3 | Karim Ahmed | 01987654321 | 2 | 2026-10-02 |
| 3 | 2 | Nusrat Jahan | 01555666777 | 1 | 2026-10-03 |
| 4 | 4 | Tanjina Khatun | 01311223344 | 3 | 2026-10-04 |
| 5 | 5 | Sadia Afrose | 01933887711 | 2 | 2026-10-05 |
| 6 | 2 | Farhana Roxy | 01344266823 | 3 | 2026-10-06 |
| 7 | 2 | Salma Sarkar | 01731055692 | 6 | 2026-10-07 |

-- Question 1: Unique Categories
-- Write a query to find all unique product categories available in the products table.
SELECT DISTINCT CATEGORY FROM PRODUCTS;

### Output:
| CATEGORY |
| :--- |
| Electronics |
|  Accessories |
| Accessories |
|  Furniture |

-- Question 2: Product Search
-- Write a query to find all unique products from the products table whose names contain the word 'Headphone or 'Laptop'.
SELECT * FROM PRODUCTS
WHERE PRODUCT_NAME LIKE '%Headphone%' or
PRODUCT_NAME LIKE '%Laptop';

### Output:
| PRODUCT_ID | PRODUCT_NAME | CATEGORY | PRICE | STOCK |
| :--- | :--- | :--- | :--- | :--- |
| 1 | Asua ROG Laptop | Electronics | 125000.00 | 15 |
| 3 | Sony Wireless Headphone | Accessories | 15000.00 | 50 |
| 7 | HP Pavilion laptop | Electronics | 75000.00 | 8 |

-- Question 3: name formatting:
-- Display all customer names from the sales table in uppercase.
SELECT UPPER(CUSTOMER_NAME) FROM SALES;

### Output:
| UPPER(CUSTOMER_NAME) |
| :--- |
| TAMIM IQBAL |
| KARIM AHMED |
| NUSRAT JAHAN |
| TANJINA KHATUN |
| SADIA AFROSE |
| FARHANA ROXY |
| SALMA SARKAR |

-- Question 4: 
-- For customer privacy, display the customer's name and mask their phone number by showing only the first 5 digits and replacing the rest with ******.
SELECT CUSTOMER_NAME, CONCAT(SUBSTRING(CUSTOMER_PHONE, 1,5),'******') AS MASKED_PHONE FROM SALES;

### Output:
| CUSTOMER_NAME | MASKED_PHONE |
| :--- | :--- |
| Tamim Iqbal | 01346****** |
| Karim Ahmed | 01987****** |
| Nusrat Jahan | 01555****** |
| Tanjina Khatun | 01311****** |
| Sadia Afrose | 01933****** |
| Farhana Roxy | 01344****** |
| Salma Sarkar | 01731****** |

-- Question 5: Top expensive products.
-- retrieve the top 5 most expensive products from the products table , ordered from highest price to lowest.
SELECT*FROM PRODUCTS
ORDER BY PRICE DESC
LIMIT 5;

### Output:
| PRODUCT_ID | PRODUCT_NAME | CATEGORY | PRICE | STOCK |
| :--- | :--- | :--- | :--- | :--- |
| 1 | Asua ROG Laptop | Electronics | 125000.00 | 15 |
| 2 | Sumsang Galaxy S24 | Electronics | 95000.00 | 25 |
| 7 | HP Pavilion laptop | Electronics | 75000.00 | 8 |
| 5 | Ergonomic Office Chair | Furniture | 18000.00 | 10 |
| 3 | Sony Wireless Headphone | Accessories | 15000.00 | 50 |

-- Question 6: Out of stoct Alert. 
-- List all products from the products table that currently have a stock level of exactly 0. 
SELECT*FROM PRODUCTS
WHERE STOCK = 0;

### Output:
| PRODUCT_ID | PRODUCT_NAME | CATEGORY | PRICE | STOCK |
| :--- | :--- | :--- | :--- | :--- |
| 6 | Logitech Gaming Mouse | Accessories | 3500.00 | 0 |

-- Question 8: Premium Electronincs. 
-- Find all products in the 'Electronics' category that cost more than 80000. 
SELECT*FROM PRODUCTS
WHERE CATEGORY='Electronics' AND PRICE>80000 AND STOCK>0;

### Output:
| PRODUCT_ID | PRODUCT_NAME | CATEGORY | PRICE | STOCK |
| :--- | :--- | :--- | :--- | :--- |
| 1 | Asua ROG Laptop | Electronics | 125000.00 | 15 |
| 2 | Sumsang Galaxy S24 | Electronics | 95000.00 | 25 |

-- Question 9: Update Price. 
-- Update the price of the product with product_id =5 to 130000 in the PRODUCTS table. 
UPDATE PRODUCTS
SET PRICE= 130000
WHERE PRODUCT_ID = 5;

### Output:
Query OK, 1 row affected.

-- Question 10: Product level generation. 
-- Generate a custop product label for all items by combining the product_name and its category. 
SELECT CONCAT( PRODUCT_NAME,' - ', CATEGORY) AS PRODUCT_LABEL, PRICE FROM PRODUCTS;

### Output:
| PRODUCT_LABEL | PRICE |
| :--- | :--- |
| Asua ROG Laptop - Electronics | 125000.00 |
| Sumsang Galaxy S24 - Electronics | 95000.00 |
| Sony Wireless Headphone - Accessories | 15000.00 |
| Mechanical Keyboard - Accessories | 5500.00 |
| Ergonomic Office Chair - Furniture | 130000.00 |
| Logitech Gaming Mouse - Accessories | 3500.00 |
| HP Pavilion laptop - Electronics | 75000.00 |