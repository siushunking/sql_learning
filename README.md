# sql_learning
記錄一些常用的sql 語法，內容參考連結如下。

 [SQL- Fooish 程式技術](https://www.fooish.com/sql/distinct.html)
 
 [SQL - The Complete Developer's Guide (MySQL, PostgreSQL)](https://www.udemy.com/course/sql-the-complete-developers-guide-mysql-postgresql/)
 

## Create database
CREATE DATABASE database_name

## DROP DATABASE database
delete DATABASE database_name

## CREATE TABLE 

用法
CREATE TABLE table_name (
  column_name1 data_type,
  column_name2 data_type,
  column_name3 data_type,
  ···
);

1. 設為主鍵  SERIAL PRIMARY KEY //postgresql 語法
2. 設為默認 DEFAULT（）
3. 不可以是空值NOT NULL
4. 檢查/定條件 CHECK

```
CREATE TABLE sales (
    id SERIAL PRIMARY KEY,
    data_create DATE DEFAULT (CURRENT_DATE),
    date_fulfilled DATE,
    customer_name VARCHAR(300) NOT NULL,
    product_name VARCHAR(300) NOT NULL,
    volume NUMERIC(10,3) NOT NULL CHECK (volume >= 0),
    is_recurring BOOLEAN DEFAULT FALSE,
    is_disputed BOOLEAN DEFAULT FALSE
)
```
## DELETE column
DELETE FROM sales
WHERE id = 9

## insert column
```
INSERT INTO sales (
  data_create,
  date_fulfilled,
  customer_name,
  product_name,
  volume,
  is_disputed,
  is_recurring
)
VALUES (
  '2022-01-18',
  '2022-03-11',
  'Company A',
  'A Nice Product',
  489.99,
  FALSE,
  TRUE
), (
  '2022-01-18',
  '2022-05-01',
  'Company B',
  'Video Game Collection',
  3859.12,
  FALSE,
  FALSE
)
```

## select

### 大於 小於 >= <= > < 是 = IS   AND OR
```
SELECT * FROM sales
where (is_disputed IS TRUE) AND (volume > 5000)
```

```
SELECT * FROM sales
where data_create BEWTEEN '2021-01-21' AND '2021-2-4'
```
## date and data diffences  計算差異

```
SELECT * FROM sales
where data_fulfilled - date_create
```

## EXTRACT(unit FROM datetime)
 EXTRACT() 函數來取出日期和時間中特定的部分，比如年、月、日、時、分、秒等。
```
 SELECT EXTRACT(YEAR FROM '2019-07-02');
```
## order 
我們可以將 SELECT 取得的資料集依某欄位來作排序，而排序分別可以由小至大 (ascending; 預設)，或由大至小 (descending)。
SELECT * FROM employees ORDER BY Title;
```
SELECT table_column1, table_column2...
FROM table_name
ORDER BY column_name1 ASC|DESC, column_name2 ASC|DESC...
```

## limit 
用來限制SQL 查詢語句最多有幾筆資料
```
SELECT table_column1, table_column2...
FROM table_name LIMIT number;
```
## offset
select x number of rows after skipping y number of rows
```
SELECT table_column1, table_column2...
FROM table_name LIMIT number;
OFFSET <Y>
```

## find top 10 
```
SELECT * FROM sales
WHERE is_dispute IS TRUE
ORDER BY volume DESC 
LIMIT 10
```

## INNER JOIN 關鍵字 (SQL INNER JOIN Keyword) - 內部連接
INNER JOIN (內部連接) 為等值連接，必需指定等值連接的條件，而查詢結果只會返回符合連接條件的資料。
```
SELECT table_column1, table_column2...
FROM table_name1
INNER JOIN table_name2 AS table_name2簡寫
ON table_name1.column_name=table_name2.column_name;
ON table_name2.column_name=table_name3.column_name;
``` 

### DISTINCT
可使用 DISTINCT 過濾重複出現的紀錄值。
```
SELECT DISTINCT table_column1, table_column2...
FROM table_name;
```

## CREATE NEW SUBQUERIES
```
SELECT customer_name, product_name 
FROM (SELECT * FROM sales
WHERE volume > 1000) AS base_result
```

# LEFT JOIN
left join(左聯接) ：返回包括左表中的所有記錄和右表中聯結欄位相等的記錄

# RIGHT JOIN
返回包括右表中的所有記錄和左表中聯結欄位相等的記錄

# INNER JOIN
只返回兩個表中聯結欄位相等的行

#  cross JOIN
兩個資料表在結合時，不指定任何條件，即將兩個資料表中所有的可能排列組合出來

# uniON JOIN
```
SELECT column_name(s) FROM table_name1
UNION
SELECT column_name(s) FROM table_name2;
```
# union all
```
SELECT P_Name FROM products_taiwan
UNION ALL
SELECT P_Name FROM products_china;
```
