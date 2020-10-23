# Appendix 01 Aurora MySQL
1. Max Connection
In Parameter Group [Link](https://docs.aws.amazon.com/zh_tw/AmazonRDS/latest/AuroraUserGuide/AuroraMySQL.Managing.Performance.html)  

| Instances type | Max connections default value |
| -------------- | ----------------------------- |
| db.t2.small    | 45                            |
| db.t2.medium   | 90                            |
| db.t3.small    | 45                            |
| db.t3.medium   | 90                            |
| db.r5.large    | 1000                          |
| db.r5.xlarge   | 2000                          |
| db.r5.2xlarge  | 3000                          |

2. Connection Success
- Gerenal Log
```
2020-10-23T08:36:48.508034Z   50 Connect	admin@1.34.6.81 on  using SSL/TLS
```
- Audit Log
```
1603442208508100,database-1-instance-1,admin,1.34.6.81,50,0,CONNECT,,,0
```

3. Connection fail
- Audit Log
```
2020-10-23T07:13:26.298081Z 34 [Note] Access denied for user 'admin'@'58.182.98.237' (using password: YES)
```

4. Create database
- SQL
```sql
create database mysqldemo;
```
- Audit Log
```
1603438736650167,database-1-instance-1,admin,1.34.6.81,30,964317,QUERY,world,'create database mysqldemo',0
```
- General Log
```
2020-10-23T07:38:56.637123Z 30 Query create database mysqldemo
```

5. Create Table
- SQL
```sql
CREATE TABLE customers (
  C_Id INT,
  Name varchar(50),
  Address varchar(255),
  Phone varchar(20)
);
```
- General Log
```
2020-10-23T07:47:31.319556Z   30 Query	CREATE TABLE customers (
  C_Id INT,
  Name varchar(50),
  Address varchar(255),
  Phone varchar(20)
)
```
- Audit Log
```
1603439251354761,database-1-instance-1,admin,1.34.6.81,30,966941,CREATE,world,customers,
```
```
1603439251360772,database-1-instance-1,admin,1.34.6.81,30,966941,QUERY,world,'CREATE TABLE customers (   C_Id INT,   Name varchar(50),   Address varchar(255),   Phone varchar(20) )',0
```

6. Alter Table
- SQL
```sql
ALTER TABLE customers ADD Discount VARCHAR(10);
```
- General Log
```
2020-10-23T08:42:46.477013Z   50 Query	ALTER TABLE customers ADD Discount VARCHAR(10)
```
- Audit Log
```
1603442566556527,database-1-instance-1,admin,1.34.6.81,50,984383,QUERY,mysqldemo,'ALTER TABLE customers ADD Discount VARCHAR(10)',0
```

7. Drop Table
- SQL
```sql
DROP TABLE customers;
```
- General Log
```
2020-10-23T08:44:22.845107Z   50 Query	DROP TABLE customers
```
- Audit Log
```
1603442662867983,database-1-instance-1,admin,1.34.6.81,50,984868,QUERY,mysqldemo,'DROP TABLE customers',0
```

8. Insert Table
- SQL
```sql
INSERT INTO customers (C_Id, Name, Address, Phone)
VALUES (3, 'ethan', 'abcd street', '07-12345678');
```
- General Log
```
2020-10-23T08:09:31.467191Z   30 Query	INSERT INTO customers (C_Id, Name, Address, Phone)
VALUES (3, 'ethan', 'abcd street', '07-12345678')
2020-10-23T08:
```
- Audit Log
```
1603440571474649,database-1-instance-1,admin,1.34.6.81,30,973788,QUERY,mysqldemo,'INSERT INTO customers (C_Id, Name, Address, Phone) VALUES (3, \'ethan\', \'abcd street\', \'07-12345678\')',0
```

9. Update Table
- SQL
```sql
UPDATE customers SET Phone = '0912345678' WHERE C_Id = 3;
```
- General Log
```
2020-10-23T08:19:58.891329Z   30 Query	UPDATE customers SET Phone = '0912345678' WHERE C_Id = 3
```
- Audit Log
```
1603441198899209,database-1-instance-1,admin,1.34.6.81,30,977018,QUERY,mysqldemo,'UPDATE customers SET Phone = \'0912345678\' WHERE C_Id = 3',0
```

10. Delete Table
- SQL
```sql
DELETE FROM customers WHERE Name='ethan';
```
- General Log
```
2020-10-23T08:23:51.288195Z   30 Query	DELETE FROM customers WHERE Name='ethan'
```
- Audit Log
```
1603441431296080,database-1-instance-1,admin,1.34.6.81,30,978195,QUERY,mysqldemo,'DELETE FROM customers WHERE Name=\'ethan\'',0
```

11. Create USER
- SQL
```sql
CREATE USER 'ethan'@'%' IDENTIFIED WITH 'mysql_native_password' AS '<secret>'
```
- General Log
```
2020-10-23T08:26:30.609189Z   45 Query	CREATE USER 'ethan'@'%' IDENTIFIED WITH 'mysql_native_password' AS '<secret>'
```
- Audit Log
```
1603441586611643,database-1-instance-1,admin,1.34.6.81,45,979048,QUERY,mysql,'CREATE USER \'ethan\'@\'%\' IDENTIFIED WITH \'mysql_native_password\' AS \'*F846B31F10DD4389C384272E70B9BBA3AD9E1F94\'',0
```

12. Alter USER
- SQL
```sql
ALTER USER 'ethan'@'%' IDENTIFIED WITH 'mysql_native_password' AS '<secret>'
```
- General Log
```
2020-10-23T08:27:37.341888Z   47 Query	ALTER USER 'ethan'@'%' IDENTIFIED WITH 'mysql_native_password' AS '<secret>'
```
- Audit Log
```
1603441657347720,database-1-instance-1,admin,1.34.6.81,47,979491,QUERY,mysql,'ALTER USER \'ethan\'@\'%\' IDENTIFIED WITH \'mysql_native_password\' AS \'*F846B31F10DD4389C384272E70B9BBA3AD9E1F94\'',0
```

13. Grant USER
- SQL
```sql
GRANT DROP, EXECUTE, CREATE ROUTINE, CREATE USER, CREATE, SHOW DATABASES, RELOAD, ALTER, DELETE, ALTER ROUTINE, INSERT, INDEX, CREATE TEMPORARY TABLES, CREATE VIEW, EVENT, SELECT, SHOW VIEW, UPDATE, LOCK TABLES, PROCESS, TRIGGER ON *.* TO 'ethan'@'%' WITH MAX_QUERIES_PER_HOUR 0 MAX_CONNECTIONS_PER_HOUR 0 MAX_UPDATES_PER_HOUR 0 MAX_USER_CONNECTIONS 0
```
- General Log
```
2020-10-23T08:28:37.742495Z   47 Query	GRANT DROP, EXECUTE, CREATE ROUTINE, CREATE USER, CREATE, SHOW DATABASES, RELOAD, ALTER, DELETE, ALTER ROUTINE, INSERT, INDEX, CREATE TEMPORARY TABLES, CREATE VIEW, EVENT, SELECT, SHOW VIEW, UPDATE, LOCK TABLES, PROCESS, TRIGGER ON *.* TO 'ethan'@'%' WITH MAX_QUERIES_PER_HOUR 0 MAX_CONNECTIONS_PER_HOUR 0 MAX_UPDATES_PER_HOUR 0 MAX_USER_CONNECTIONS 0
```
- Audit Log
```
1603441717744113,database-1-instance-1,admin,1.34.6.81,47,979851,QUERY,mysql,'GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, RELOAD, PROCESS, INDEX, ALTER, SHOW DATABASES, CREATE TEMPORARY TABLES, LOCK TABLES, EXECUTE, CREATE VIEW, SHOW VIEW, CREATE ROUTINE, ALTER ROUTINE, CREATE USER, EVENT, TRIGGER ON *.* TO \'ethan\'@\'%\' WITH MAX_QUERIES_PER_HOUR 0 MAX_UPDATES_PER_HOUR 0 MAX_CONNECTIONS_PER_HOUR 0 MAX_USER_CONNECTIONS 0',0
```

14. Drop USER
- SQL
```sql
DROP USER 'ethan'@'%'
```
- General Log
```
2020-10-23T08:34:08.216920Z   47 Query	DROP USER 'ethan'@'%'
```
- Audit Log
```
1603442048227886,database-1-instance-1,admin,1.34.6.81,47,981659,QUERY,mysql,'DROP USER \'ethan\'@\'%\'',0
```

15. Slow QUERY
- SQL
```sql
SELECT * FROM mysqldemo.customers WHERE Address='abcd street'
```
- Slow Query Log
```
# Time: 2020-10-23T08:46:32.817274Z
# User@Host: admin[admin] @  [1.34.6.81]  Id:    50
# Query_time: 0.000299  Lock_time: 0.000144 Rows_sent: 1  Rows_examined: 1
SET timestamp=1603442792;
SELECT * FROM mysqldemo.customers WHERE Address='abcd street'
LIMIT 0, 1000;
```

16. ALTER SYSTEM CRASH
- SQL
```sql
ALTER SYSTEM CRASH NODE
```
- General Log
```
2020-10-23T08:53:58.167384Z    6 Query	ALTER SYSTEM CRASH NODE
```
- Error Log
```
2020-10-23T08:53:58.167728Z 6 [Note] Forcing a crash of type 2
```
[LINK](https://dev.classmethod.jp/articles/recovery-test-aurora/)